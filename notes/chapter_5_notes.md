# Phoenix for Rails Developers: Chapter 5
## Handling Requests
1. Every request in Phoenix run through the path:
```
Endpoint  -> Router -> Controller 
```
3. **Plugs**
	1. `lib/storex_web/endpoint.ex `is the app’s first point of contact. 
	2. Elixir plugs are used to manipulate the request in different ways:
		1. `Plug.Static` serves static files
		2. `Plug.logger` is responsible for displaying requester information to the logger. 
		3. The final plug within the request lifecycle is `StorexRouter.Plug`. This I the point where the app-specific routes take control of the request. 
4. **Controller**
```
# PageController
def index(conn, _params) do
	render conn, “index.html”
end
```
	1. Phoenix controller receive two parameters by default; `conn` and `params`
		1. `Plug.conn` struct contains host, path, port, query string, etc information
			1. `conn` is widely used in Phoenix; also used to expose values to templates, build links, and forms
		2. `_params` is a map. `request` and `response` in Rails controllers contain most of the values found in `conn`
	2. The call to `render conn, “index.html”`doesn’t just render a view in Phoenix. When you call render with a template you are rendering a Phoenix view.
		1. Phoenix uses the controller, `PageController`,name to determine what view to use; `PageView`
	3. **View**
```
defmodule StorexWeb.PageView  do 
	use StorexWeb, :view 
end
```
1. Phoenix pre-complies all the template files into the view by using the controller name to look up template files located in `lib/storex_web/templates/page`
2. Every template found becomes a function of the view.

## When creating a new Books application page
1. Add the controller: `defmodule StorexWeb.BookController do`…
2. Add the router: `get("/", BookController, :index)`
3. Add the view: `defmodule StorexWeb.BookView do`…
4. Add the template. `templates/book.index.html.eex`

## Notes about application layout
1. Can be found in: `lib/storex_web/templates/layout/app.html.eex `
	1. There are no helpers for stylesheets or including javascript. It relies on `static_path`helper with returns a file path rom `priv/static`
		1. `<link rel=“stylesheet” href=“<%= static_path(@conn, “/css/app.css”) %>”>`

	2. `get_flash(@conn, :info)`is the flash helper similar to `flash[:info]`
	3. `<%= render @view_module, @view_template, assigns %>`is the equivalent   to `yield` in the Rails application layout. 




