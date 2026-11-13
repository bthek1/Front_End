# React and Django

Here’s **everything you need to know** to **create a full-stack project using Django (with Django REST Framework) and React**, including setup, project structure, communication between backend and frontend, deployment, and best practices.

Author

Benedict Thekkel

## 🧱 1. **Tech Stack Breakdown**

| Layer | Technology | Purpose |
|----|----|----|
| Backend | Django + Django REST Framework | API + ORM + Auth |
| Frontend | React (with Vite or Next.js) | SPA / UI |
| API Format | JSON (via DRF) | Communicate between FE/BE |
| Auth Options | JWT / Session | Token-based auth |
| Deployment | Docker / Gunicorn + Nginx / Vite static build | Production hosting |

------------------------------------------------------------------------

## 📦 2. **Backend Setup (Django + DRF)**

### 📁 Project Structure

    myproject/
    ├── backend/
    │   ├── manage.py
    │   ├── myproject/         # Django settings
    │   └── api/               # Django app for your API
    │       ├── models.py
    │       ├── serializers.py
    │       ├── views.py
    │       ├── urls.py
    ├── frontend/              # React app
    │   ├── package.json
    │   └── src/

### 🧪 Create Backend

``` bash
# Create and activate virtualenv
python -m venv .venv
source .venv/bin/activate

# Install Django + DRF
pip install django djangorestframework djoser django-cors-headers

# Create project and app
django-admin startproject myproject backend
cd backend
python manage.py startapp api
```

### ✍️ Update `settings.py`

``` python
INSTALLED_APPS = [
    ...
    'rest_framework',
    'corsheaders',
    'api',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    ...
]

CORS_ALLOWED_ORIGINS = [
    "http://localhost:5173",  # or Vite dev server
]

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': ['rest_framework.permissions.AllowAny'],
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.BasicAuthentication',
    ],
}
```

### 🔁 Sample API Setup

#### `models.py`

``` python
from django.db import models

class Todo(models.Model):
    title = models.CharField(max_length=100)
    completed = models.BooleanField(default=False)
```

#### `serializers.py`

``` python
from rest_framework import serializers
from .models import Todo

class TodoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Todo
        fields = '__all__'
```

#### `views.py`

``` python
from rest_framework import viewsets
from .models import Todo
from .serializers import TodoSerializer

class TodoViewSet(viewsets.ModelViewSet):
    queryset = Todo.objects.all()
    serializer_class = TodoSerializer
```

#### `urls.py`

``` python
from rest_framework.routers import DefaultRouter
from .views import TodoViewSet

router = DefaultRouter()
router.register(r'todos', TodoViewSet)

urlpatterns = router.urls
```

#### `backend/urls.py`

``` python
from django.urls import path, include

urlpatterns = [
    path('api/', include('api.urls')),
]
```

------------------------------------------------------------------------

## ⚛️ 3. **Frontend Setup (React + Vite)**

``` bash
# From project root
npm create vite@latest frontend -- --template react-ts
cd frontend
npm install
```

### 🧰 Useful Packages

``` bash
npm install axios react-router-dom
```

### 📁 Example Project Structure

    frontend/
    ├── src/
    │   ├── pages/
    │   │   └── TodoPage.tsx
    │   ├── components/
    │   ├── App.tsx
    │   ├── main.tsx

### 🔁 Axios Setup

#### `api/axios.ts`

``` ts
import axios from 'axios';

const api = axios.create({
  baseURL: 'http://localhost:8000/api/',
});

export default api;
```

------------------------------------------------------------------------

## 📄 4. **Sample React Page**

#### `pages/TodoPage.tsx`

``` tsx
import React, { useEffect, useState } from 'react';
import api from '../api/axios';

type Todo = {
  id: number;
  title: string;
  completed: boolean;
};

export default function TodoPage() {
  const [todos, setTodos] = useState<Todo[]>([]);

  useEffect(() => {
    api.get<Todo[]>('todos/').then((res) => setTodos(res.data));
  }, []);

  return (
    <div>
      <h2>Todo List</h2>
      <ul>
        {todos.map((todo) => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

------------------------------------------------------------------------

## 🔑 5. **Authentication (Optional)**

### Use `djoser` or JWT

``` bash
pip install djangorestframework-simplejwt
```

In `settings.py`:

``` python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}
```

Then in frontend, use:

``` tsx
const login = async () => {
  const res = await api.post("token/", { username, password });
  localStorage.setItem("access", res.data.access);
};
```

------------------------------------------------------------------------

## 📦 6. **Deployment Overview**

| Layer    | Tool                            |
|----------|---------------------------------|
| Backend  | Gunicorn + Nginx + PostgreSQL   |
| Frontend | Build with Vite → `dist/`       |
| Hosting  | Render, Heroku, Railway, Docker |

``` bash
# Build frontend
cd frontend
npm run build

# Copy dist to Django
mv dist ../backend/frontend_build/

# Serve with Django staticfiles or Nginx
```

------------------------------------------------------------------------

## ✅ 7. **Best Practices**

| Area        | Best Practice                                      |
|-------------|----------------------------------------------------|
| CORS        | Use `django-cors-headers` in dev, stricter in prod |
| Env vars    | Use `.env` + `python-decouple` or `django-environ` |
| Security    | Use HTTPS, CSRF token if needed                    |
| Performance | Use pagination, limit fields in serializers        |
| API Design  | RESTful endpoints, versioning (`/api/v1/`)         |

------------------------------------------------------------------------

## 📘 Summary Diagram

    Frontend (React)
      ↓ axios
    API Gateway: `/api/`
      ↓
    Backend (Django DRF)
      ↳ DB (PostgreSQL / SQLite)

------------------------------------------------------------------------

Would you like a **GitHub starter template** or **Docker setup** for this stack?

------------------------------------------------------------------------

Back to top
