# Javascript

When writing JavaScript for the front end of a Django REST Framework (DRF) project, you’re primarily working to integrate your front-end application with a DRF-powered back-end API. Here’s a comprehensive guide to ensure you cover everything you need to know.

Author

Benedict Thekkel

### 1. **Understanding the Architecture:**

- **Django REST Framework (DRF)** provides the backend, offering an API that returns data (typically JSON) in response to HTTP requests.
- **JavaScript (JS)** on the front end is responsible for interacting with the DRF API to send and receive data asynchronously (usually via AJAX or `fetch`).

### 2. **Setting Up the Front End:**

- DRF and Django are typically used with templates, but if you’re building a single-page application (SPA), the front end may be separated from Django’s template system.
- You might still use Django’s built-in templating, but increasingly, front-end frameworks like **React**, **Vue.js**, or **Vanilla JavaScript** with build tools (Webpack, Vite) are preferred.

### 3. **Using APIs:**

- DRF’s role is to expose data as a REST API. You’ll use **JavaScript** (or a framework) to interact with this API.
- Use **`fetch`** or **Axios** (or any HTTP client) to send HTTP requests from the front end to the API.

#### Example of Fetching Data in JavaScript:

``` javascript
fetch('http://localhost:8000/api/items/')
  .then(response => response.json())
  .then(data => {
    console.log(data);  // Handle the JSON data
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

- **Methods**: You’ll need to know how to send different types of requests:
  - **GET**: To retrieve data from the API.
  - **POST**: To send data for creating new objects.
  - **PUT/PATCH**: To update data.
  - **DELETE**: To delete resources.

#### Example of Sending Data:

``` javascript
fetch('http://localhost:8000/api/items/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer <token>'  // If using token-based auth
  },
  body: JSON.stringify({name: 'Item', description: 'A new item'})
})
  .then(response => response.json())
  .then(data => console.log('Item created:', data))
  .catch(error => console.error('Error:', error));
```

### 4. **Cross-Origin Resource Sharing (CORS):**

- When using JavaScript to make API requests from a front-end hosted on a different domain or port, you’ll need to handle **CORS**.
- **Django-cors-headers** can be used to configure CORS in your DRF project.

#### Install and Configure `django-cors-headers`:

``` bash
pip install django-cors-headers
```

In `settings.py`: \`\`\`python INSTALLED_APPS = \[ …, ‘corsheaders’, \]

MIDDLEWARE = \[ ‘corsheaders.middleware.CorsMiddleware’, …, \]

\# Allow all origins (for development purposes): CORS_ALLOW_ALL_ORIGINS = True \`\`\`

- For production, configure **CORS_ALLOWED_ORIGINS** with specific origins.

### 5. **Handling Authentication:**

- **JWT (JSON Web Tokens)** or **Token-based authentication** are common in DRF projects.
- Use the front end to send the token along with requests for protected routes.

#### Example of Adding Authorization Header:

``` javascript
fetch('http://localhost:8000/api/protected/', {
  headers: {
    'Authorization': 'Bearer ' + localStorage.getItem('access_token')  // Add the token here
  }
});
```

- Store the token securely on the client side (e.g., in `localStorage` or `sessionStorage`).

### 6. **Error Handling in JavaScript:**

- Handle errors that come from the DRF API, such as 400 (bad request), 401 (unauthorized), 403 (forbidden), or 500 (server error).

Example: `javascript fetch('http://localhost:8000/api/resource/') .then(response => { if (!response.ok) { throw new Error('Network response was not ok ' + response.statusText); } return response.json(); }) .then(data => console.log(data)) .catch(error => console.error('There was a problem with your fetch operation:', error));`

### 7. **Handling Forms and File Uploads:**

- For **HTML forms**, use JavaScript’s `FormData` to send form data, including file uploads, to DRF.

Example of File Upload: \`\`\`javascript const formData = new FormData(); formData.append(‘file’, fileInput.files\[0\]);

fetch(‘http://localhost:8000/api/upload/’, { method: ‘POST’, body: formData }) .then(response =\> response.json()) .then(data =\> console.log(‘File uploaded:’, data)) .catch(error =\> console.error(‘Error:’, error)); \`\`\`

### 8. **Front-End Frameworks:**

- **React** and **Vue.js** are popular frameworks to work with DRF. They offer better state management, routing, and modularity for building complex front-end applications.

\#### Example in React: \`\`\`javascript import React, { useState, useEffect } from ‘react’;

function Items() { const \[items, setItems\] = useState(\[\]);

     useEffect(() => {
       fetch('http://localhost:8000/api/items/')
         .then(response => response.json())
         .then(data => setItems(data))
         .catch(error => console.error('Error:', error));
     }, []);

     return (
       <div>
         <h1>Items List</h1>
         <ul>
           {items.map(item => (
             <li key={item.id}>{item.name}</li>
           ))}
         </ul>
       </div>
     );

}

export default Items; \`\`\`

### 9. **Frontend Build Tools:**

- If you use modern front-end tooling like **Webpack** or **Vite**, you can bundle your JavaScript assets for Django.

#### Example: Using Webpack with Django

1.  Install Webpack:

    ``` bash
    npm install webpack webpack-cli --save-dev
    ```

2.  Configure `webpack.config.js`:

    ``` javascript
    const path = require('path');

    module.exports = {
      entry: './src/index.js',
      output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'static/js')
      },
      mode: 'development'
    };
    ```

3.  Use the generated `bundle.js` in your Django templates.

### 10. **Debugging and Testing:**

- Use **Chrome DevTools** or **Firefox Developer Tools** for debugging JavaScript and network requests.
- For automated testing of your JavaScript code interacting with DRF APIs, consider tools like **Jest** for unit tests and **Cypress** or **Puppeteer** for end-to-end testing.

Back to top
