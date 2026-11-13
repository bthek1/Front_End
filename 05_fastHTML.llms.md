# fastHTML

fastHTML

Author

Benedict Thekkel

``` sh
pip install python-fasthtml
```

``` python
from fasthtml.common import *
```

``` python
# Assuming the file Front_end/app.py exists and contains some content
file_path = 'Front_end/app.py'

# Reading and displaying the content of the file
with open(file_path, 'r') as file:
    file_content = file.read()
```

``` python
print(file_content)
```

    from fasthtml.common import *

    app,rt = fast_app()


    def NumList(i):
        return Ul(*[Li(o) for o in range(i)])



    @rt('/')
    def get(): 
        nums = NumList(5)
        return Titled('Greeting',
                      Div(nums, id='stuff', hx_get="/change"),
                     )

    @rt('/change')
    def get(): 
        return Div(P('Change is good!'),
                   P(A('Home', href="/"))
                  )


    serve()

``` python
fast_app??
```

    Signature:
    fast_app(
        db: Optional[str] = None,
        render: Optional[<built-in function callable>] = None,
        hdrs: Optional[tuple] = None,
        ftrs: Optional[tuple] = None,
        tbls: Optional[dict] = None,
        before: Optional[tuple] = None,
        middleware: Optional[tuple] = None,
        live: bool = False,
        debug: bool = False,
        routes: Optional[tuple] = None,
        exception_handlers: Optional[dict] = None,
        on_startup: Optional[<built-in function callable>] = None,
        on_shutdown: Optional[<built-in function callable>] = None,
        lifespan: Optional[<built-in function callable>] = None,
        default_hdrs=True,
        pico: Optional[bool] = None,
        ws_hdr: bool = False,
        secret_key: Optional[str] = None,
        key_fname: str = '.sesskey',
        session_cookie: str = 'session_',
        max_age: int = 31536000,
        sess_path: str = '/',
        same_site: str = 'lax',
        sess_https_only: bool = False,
        sess_domain: Optional[str] = None,
        bodykw: Optional[dict] = None,
        **kwargs,
    )
    Docstring: <no docstring>
    Source:   
    def fast_app(
            db:Optional[str]=None, # Database file name, if needed
            render:Optional[callable]=None, # Function used to render default database class
            hdrs:Optional[tuple]=None, # Additional FT elements to add to <HEAD>
            ftrs:Optional[tuple]=None, # Additional FT elements to add to end of <BODY>
            tbls:Optional[dict]=None, # Mapping from DB table names to dict table definitions
            before:Optional[tuple]=None, # Functions to call prior to calling handler
            middleware:Optional[tuple]=None, # Standard Starlette middleware
            live:bool=False, # Enable live reloading
            debug:bool=False, # Passed to Starlette, indicating if debug tracebacks should be returned on errors
            routes:Optional[tuple]=None, # Passed to Starlette
            exception_handlers:Optional[dict]=None, # Passed to Starlette
            on_startup:Optional[callable]=None, # Passed to Starlette
            on_shutdown:Optional[callable]=None, # Passed to Starlette
            lifespan:Optional[callable]=None, # Passed to Starlette
            default_hdrs=True, # Include default FastHTML headers such as HTMX script?
            pico:Optional[bool]=None, # Include PicoCSS header?
            ws_hdr:bool=False, # Include HTMX websocket extension header?
            secret_key:Optional[str]=None, # Signing key for sessions
            key_fname:str='.sesskey', # Session cookie signing key file name
            session_cookie:str='session_', # Session cookie name
            max_age:int=365*24*3600, # Session cookie expiry time
            sess_path:str='/', # Session cookie path
            same_site:str='lax', # Session cookie same site policy
            sess_https_only:bool=False, # Session cookie HTTPS only?
            sess_domain:Optional[str]=None, # Session cookie domain
            bodykw:Optional[dict]=None,
            **kwargs):
        h = (picolink,) if pico or (pico is None and default_hdrs) else ()
        if hdrs: h += tuple(hdrs)
        app_cls = FastHTMLWithLiveReload if live else FastHTML
        app = app_cls(hdrs=h, ftrs=ftrs, before=before, middleware=middleware, debug=debug, routes=routes, exception_handlers=exception_handlers,
                      on_startup=on_startup, on_shutdown=on_shutdown, lifespan=lifespan, default_hdrs=default_hdrs, secret_key=secret_key,
                      session_cookie=session_cookie, max_age=max_age, sess_path=sess_path, same_site=same_site, sess_https_only=sess_https_only,
                      sess_domain=sess_domain, key_fname=key_fname, ws_hdr=ws_hdr, **(bodykw or {}))
        @app.route("/{fname:path}.{ext:static}")
        async def get(fname:str, ext:str): return FileResponse(f'{fname}.{ext}')
        if not db: return app,app.route
        db = database(db)
        if not tbls: tbls={}
        if kwargs:
            if isinstance(first(kwargs.values()), dict): tbls = kwargs
            else:
                kwargs['render'] = render
                tbls['items'] = kwargs
        dbtbls = [get_tbl(db.t, k, v) for k,v in tbls.items()]
        if len(dbtbls)==1: dbtbls=dbtbls[0]
        return app,app.route,*dbtbls
    File:      ~/miniconda3/envs/pfast/lib/python3.12/site-packages/fasthtml/fastapp.py
    Type:      function

Back to top
