# React Docker

Here is a **production-ready Docker setup** for a full-stack project with **Django + DRF + React + PostgreSQL**, using **multi-stage builds**, **Nginx** for static serving, and **Docker Compose** for orchestration.

Author

Benedict Thekkel

------------------------------------------------------------------------

## 🧱 Project Structure (Full Stack + Docker)

    myproject/
    ├── backend/
    │   ├── Dockerfile
    │   ├── requirements.txt
    │   ├── manage.py
    │   ├── myproject/
    │   └── api/
    ├── frontend/
    │   ├── Dockerfile
    │   ├── vite.config.ts
    │   └── src/
    ├── nginx/
    │   └── default.conf
    ├── .env
    ├── docker-compose.yml
    └── README.md

------------------------------------------------------------------------

## ⚙️ 1. `docker-compose.yml`

``` yaml
version: '3.9'

services:
  backend:
    build: ./backend
    command: gunicorn myproject.wsgi:application --bind 0.0.0.0:8000
    volumes:
      - static_volume:/app/static
      - media_volume:/app/media
    env_file: .env
    depends_on:
      - db

  frontend:
    build: ./frontend
    command: ["npm", "run", "preview", "--", "--port", "5173"]
    depends_on:
      - backend

  nginx:
    image: nginx:alpine
    volumes:
      - static_volume:/app/static
      - media_volume:/app/media
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
    ports:
      - "80:80"
    depends_on:
      - backend
      - frontend

  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data/
    env_file: .env

volumes:
  static_volume:
  media_volume:
  postgres_data:
```

------------------------------------------------------------------------

## 🐍 2. `backend/Dockerfile`

``` dockerfile
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY requirements.txt .
RUN pip install --upgrade pip && pip install -r requirements.txt

COPY . .

RUN python manage.py collectstatic --noinput

CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
```

> Make sure `requirements.txt` contains:

``` txt
Django>=4.2
djangorestframework
gunicorn
psycopg2-binary
django-cors-headers
```

------------------------------------------------------------------------

## ⚛️ 3. `frontend/Dockerfile` (Vite + React)

``` dockerfile
# Build stage
FROM node:20-alpine as builder

WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

# Serve stage
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

------------------------------------------------------------------------

## 🌐 4. `nginx/default.conf`

``` nginx
server {
    listen 80;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri $uri/ /index.html;
    }

    location /api/ {
        proxy_pass http://backend:8000/api/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /static/ {
        alias /app/static/;
    }

    location /media/ {
        alias /app/media/;
    }
}
```

------------------------------------------------------------------------

## 🔐 5. `.env` Example

``` env
# Django settings
SECRET_KEY=supersecretkey
DEBUG=0
ALLOWED_HOSTS=*

# Postgres
POSTGRES_DB=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
```

------------------------------------------------------------------------

## 🏁 6. Commands to Run

``` bash
# Build and start
docker-compose up --build

# Run DB migrations
docker-compose exec backend python manage.py migrate

# Create superuser
docker-compose exec backend python manage.py createsuperuser
```

------------------------------------------------------------------------

## ✅ 7. Production Checklist

| Item                  | Recommended Practice                     |
|-----------------------|------------------------------------------|
| `DEBUG = False`       | In production                            |
| `ALLOWED_HOSTS`       | Set actual domains                       |
| Use `django-environ`  | For env variables in Django settings     |
| HTTPS with Nginx      | Use Let’s Encrypt + Certbot              |
| Static/media volume   | Persisted between containers             |
| Frontend build output | `/app/dist` from Vite → served via Nginx |

------------------------------------------------------------------------

## 📦 Bonus: Build Script (Optional)

``` bash
#!/bin/bash

docker-compose down -v
docker-compose build
docker-compose up -d
docker-compose exec backend python manage.py migrate
```

------------------------------------------------------------------------

Back to top
