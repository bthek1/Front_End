# HTTP Message Headers

**Everything to Know About HTTP Message Headers, Nginx, and CORS**

Author

Benedict Thekkel

## **1. What are HTTP Message Headers?**

HTTP headers are key-value pairs sent between the client and server to pass additional information about the request or response.

### **Types of HTTP Headers**

1.  **Request Headers** – Sent by the client (e.g., browser)\
2.  **Response Headers** – Sent by the server\
3.  **Entity Headers** – Provide metadata about the body of the resource\
4.  **General Headers** – Applied to both requests and responses\
5.  **Custom Headers** – Defined by developers, prefixed with `X-` (e.g., `X-Request-ID`)

------------------------------------------------------------------------

## **2. Common HTTP Headers**

### **Request Headers**

| Header | Description | Example |
|----|----|----|
| `Accept` | Media types the client can handle | `Accept: text/html, application/json` |
| `Authorization` | Credentials for authentication | `Authorization: Bearer <token>` |
| `User-Agent` | Identifies the client software | `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)` |
| `Cookie` | Sends cookies to the server | `Cookie: sessionId=abc123` |
| `Referer` | The URL of the referring page | `Referer: https://example.com` |
| `Content-Type` | Media type of the request body | `Content-Type: application/json` |
| `Origin` | The origin of the request (for CORS) | `Origin: https://example.com` |

### **Response Headers**

| Header | Description | Example |
|----|----|----|
| `Content-Type` | Media type of the response body | `Content-Type: application/json` |
| `Cache-Control` | Caching directives | `Cache-Control: no-cache, no-store` |
| `Set-Cookie` | Sets cookies in the client | `Set-Cookie: sessionId=abc123; HttpOnly` |
| `Location` | Redirect URL | `Location: https://new-url.com` |
| `Access-Control-Allow-Origin` | Controls CORS | `Access-Control-Allow-Origin: *` |
| `Content-Security-Policy` | Security policy for resources | `Content-Security-Policy: default-src 'self'` |

------------------------------------------------------------------------

## **3. CORS (Cross-Origin Resource Sharing)**

**CORS** is a mechanism that allows restricted resources (like fonts, APIs) on a web page to be requested from another domain.

### **Why is CORS needed?**

- Browsers block cross-origin requests by default for security (Same-Origin Policy).\
- CORS defines headers to explicitly allow or deny these requests.

### **Key CORS Headers**

| Header | Description | Example |
|----|----|----|
| `Access-Control-Allow-Origin` | Specifies allowed origins | `Access-Control-Allow-Origin: *` or `https://example.com` |
| `Access-Control-Allow-Methods` | Allowed HTTP methods | `Access-Control-Allow-Methods: GET, POST, PUT` |
| `Access-Control-Allow-Headers` | Allowed custom headers | `Access-Control-Allow-Headers: Content-Type, Authorization` |
| `Access-Control-Allow-Credentials` | Allow sending credentials | `Access-Control-Allow-Credentials: true` |
| `Access-Control-Expose-Headers` | Expose custom headers to JS | `Access-Control-Expose-Headers: X-Custom-Header` |
| `Access-Control-Max-Age` | Caching duration for preflight | `Access-Control-Max-Age: 86400` |

------------------------------------------------------------------------

## **4. Implementing HTTP Headers in Nginx**

Nginx can be configured to add, modify, or remove HTTP headers using the `add_header` and `proxy_set_header` directives.

### **Adding Security Headers in Nginx**

``` nginx
server {
    listen 80;
    server_name example.com;

    location / {
        root /var/www/html;
        index index.html;

        # Security Headers
        add_header X-Frame-Options "DENY";
        add_header X-Content-Type-Options "nosniff";
        add_header X-XSS-Protection "1; mode=block";
        add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
        add_header Content-Security-Policy "default-src 'self'";
    }
}
```

### **Setting CORS Headers in Nginx**

``` nginx
server {
    listen 80;
    server_name api.example.com;

    location / {
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS';
        add_header 'Access-Control-Allow-Headers' 'Origin, X-Requested-With, Content-Type, Accept, Authorization';
        add_header 'Access-Control-Allow-Credentials' 'true';
        
        # Handle Preflight Requests
        if ($request_method = OPTIONS ) {
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'Origin, X-Requested-With, Content-Type, Accept, Authorization';
            add_header 'Access-Control-Max-Age' '86400';
            return 204;
        }
    }
}
```

### **Custom Headers in Nginx**

``` nginx
server {
    listen 80;
    server_name example.com;

    location / {
        add_header X-Custom-Header "MyCustomValue";
    }
}
```

------------------------------------------------------------------------

## **5. CORS Preflight Requests**

- **Preflight Requests** are made using the `OPTIONS` method to check if the actual request is safe.
- These are triggered when:
  - Using methods other than GET or POST (e.g., PUT, DELETE)
  - Using custom headers (e.g., Authorization)
  - Sending JSON or non-simple content types

### **Handling Preflight Requests in Nginx**

``` nginx
location /api/ {
    if ($request_method = OPTIONS) {
        add_header Access-Control-Allow-Origin '*';
        add_header Access-Control-Allow-Methods 'GET, POST, PUT, DELETE, OPTIONS';
        add_header Access-Control-Allow-Headers 'Authorization, Content-Type';
        add_header Access-Control-Max-Age '86400';
        return 204;
    }
}
```

------------------------------------------------------------------------

## **6. Debugging CORS Issues**

1.  **Check Console Errors in Browser DevTools**:
    - `No 'Access-Control-Allow-Origin' header` → Add the header in Nginx
    - `Method not allowed by Access-Control-Allow-Methods` → Include the method in Nginx config
2.  **Use Browser Extensions for Testing**:
    - [Allow CORS: Access-Control-Allow-Origin](https://chrome.google.com/webstore/detail/allow-cors-access-control/)
3.  **Use Curl for Testing**

``` bash
curl -I -X OPTIONS https://api.example.com \
-H "Origin: https://example.com" \
-H "Access-Control-Request-Method: POST" \
-H "Access-Control-Request-Headers: Content-Type, Authorization"
```

------------------------------------------------------------------------

## **7. Best Practices for Using HTTP Headers in Nginx and CORS**

- **Security Headers**:
  - `X-Frame-Options` → Prevent Clickjacking
  - `X-Content-Type-Options` → Prevent MIME type sniffing
  - `Content-Security-Policy` → Control resources loading
- **Performance Headers**:
  - `Cache-Control` → Browser caching
  - `ETag` → Conditional requests
- **CORS**:
  - Use specific origins instead of `*` for better security.
  - Avoid exposing credentials (`Access-Control-Allow-Credentials`) unless necessary.

------------------------------------------------------------------------

## **8. Testing and Verification**

- Use browser **Developer Tools** (Network tab) to inspect request and response headers.
- Online tools like:
  - [Postman](https://www.postman.com/)
  - [Curl](https://curl.se/)
  - [Request Headers Check](https://www.test-cors.org/)

------------------------------------------------------------------------

## **Conclusion**

- HTTP headers are essential for **security, caching, and CORS** management.
- **Nginx** provides powerful configuration options for setting HTTP headers.
- **CORS** is critical for **cross-origin requests**, especially in SPA and API-driven architectures.

------------------------------------------------------------------------

Back to top
