# Bootstrap

Bootstrap is a popular front-end framework that makes web development faster and easier by providing a set of CSS and JavaScript components.

Author

Benedict Thekkel

## Getting Started with Bootstrap

- CDN (Content Delivery Network): The easiest way to use Bootstrap is by including it via a CDN.

``` html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
  </body>
</html>
```

- Download: Alternatively, you can download Bootstrap and include it locally in your project.

- Bootstrap Versions: Bootstrap has evolved through several versions, with Bootstrap 5 being the latest. It removed dependency on jQuery, added more features, and improved the overall design and development experience.

## Bootstrap Grid System

- Responsive Grid System: Bootstrap’s grid system uses a series of containers, rows, and columns to layout and align content. It’s based on a 12-column layout.
- Breakpoints: Bootstrap defines several responsive breakpoints (e.g., `xs`, `sm`, `md`, `lg`, `xl`, `xxl`) for different screen sizes.
- Containers: The grid system is wrapped in a `.container` class. Containers can be fixed-width (`.container`) or fluid-width (`.container-fluid`).
- Rows and Columns: Use `.row` to create a horizontal group of columns and `.col-*` classes to define the width of columns.

------------------------------------------------------------------------

``` html
<div class="container">
    <div class="row">
        <div class="col-md-4">Column 1</div>
        <div class="col-md-4">Column 2</div>
        <div class="col-md-4">Column 3</div>
    </div>
</div>
```

## Bootstrap Components

> Bootstrap provides a wide range of components that can be used to create a fully-functional and aesthetically pleasing UI.

------------------------------------------------------------------------

### Buttons: Bootstrap buttons are styled using the `.btn` class, and additional classes like `.btn-primary`, `.btn-secondary`, `.btn-success`, etc., for different colors.

``` html
<button type="button" class="btn btn-primary">Primary Button</button>
```

### Navbar: A responsive navigation bar that can collapse into a hamburger menu on smaller screens.

``` html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
            <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Features</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Pricing</a>
            </li>
        </ul>
    </div>
</nav>
```

### Cards: Flexible content containers with various options for headers, footers, images, and content.

``` html
<div class="card" style="width: 18rem;">
    <img src="..." class="card-img-top" alt="...">
    <div class="card-body">
        <h5 class="card-title">Card title</h5>
        <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
</div>
```

### Forms: Bootstrap styles forms to be more consistent and responsive, with various classes for form controls, validation states, and layout.

``` html
<form>
    <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Email address</label>
        <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
    </div>
    <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1">
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

### Modals: Popup dialogs that can display additional content without leaving the current page.

``` html
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
    Launch demo modal
</button>

<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                ...
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                <button type="button" class="btn btn-primary">Save changes</button>
            </div>
        </div>
    </div>
</div>
```

### Alerts: Provides contextual feedback messages for typical user actions.

``` html
<div class="alert alert-warning" role="alert">
    This is a warning alert—check it out!
</div>
```

### Tables: Bootstrap tables are styled and responsive by default with classes like `.table`, `.table-striped`, `.table-bordered`, etc.

``` html
<table class="table">
    <thead>
        <tr>
            <th scope="col">#</th>
            <th scope="col">First</th>
            <th scope="col">Last</th>
            <th scope="col">Handle</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">1</th>
            <td>Mark</td>
            <td>Otto</td>
            <td>@mdo</td>
        </tr>
    </tbody>
</table>
```

### Carousels: A slideshow component for cycling through elements like images or text.

``` html
<div id="carouselExampleControls" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-inner">
        <div class="carousel-item active">
            <img src="..." class="d-block w-100" alt="...">
        </div>
        <div class="carousel-item">
            <img src="..." class="d-block w-100" alt="...">
        </div>
    </div>
    <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
    </button>
</div>
```

## Custom Bootstrap for Django

### Installs

``` sh
pip install django-sass-processor django-compressor libsass
```

or

``` sh
poetry add django-sass-processor django-compressor libsass

### Set Up Django Project Directory Structure
```

myproject/ ├── static/ │ ├── css/ │ ├── sass/ │ │ └── custom_bootstrap.scss │ └── bootstrap-5/ │ ├── css/ │ └── js/ ├── myapp/ │ └── templates/ │ └── base.html └── manage.py

    ### Configure settings.py

    ```python
    INSTALLED_APPS = [
        ...
        'compressor',
        'sass_processor',
    ]

    STATIC_URL = '/static/'
    STATICFILES_DIRS = [BASE_DIR / 'static']
    STATIC_ROOT = BASE_DIR / 'staticfiles'

    # Enable Django Compressor and Sass Processor settings
    COMPRESS_ENABLED = True
    COMPRESS_OFFLINE = True

    COMPRESS_PRECOMPILERS = (
        ('text/x-scss', 'django_libsass.SassCompiler'),
    )

    SASS_PROCESSOR_ROOT = STATICFILES_DIRS[0]  # Directory where Sass files are located
    STATICFILES_FINDERS = [
        'django.contrib.staticfiles.finders.FileSystemFinder',
        'django.contrib.staticfiles.finders.AppDirectoriesFinder',
        'compressor.finders.CompressorFinder',
    ]

### Offline Compression for Production

``` sh
python manage.py compress
```

Back to top
