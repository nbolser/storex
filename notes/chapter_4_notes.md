# Phoenix for Rails Developers: Chapter 4
## Application Structure
**Phoenix application structure** 
```
├── README.md
├── _build
├── assets
├── config
├── deps
├── lib
├── mix.exs
├── mix.lock
├── priv
└── tes

```
**Rails application structure**
```
├── Gemfile
├── Gemfile.lock
├── README.md
├── Rakefile
├── app
├── bin
├── config
├── config.ru
├── db
├── lib
├── log
├── package.json
├── public
├── test
├── tmp
```
### _build
1. Phoenix compelled artifacts go here. Rails projects don’t compile so there isn’t a similar directory.

### assets
1. Images, CSS, JS, static files are all placed here; very similar to `app/assets` Also contains `package.json` and `node_module` directory here, instead of the application root
2. After asset processing the file versions are put into `priv/static`

### config
1. Contains application configuration and dependencies. This is also a standard ins Elixir applications; much smaller `config` directory than Rails. 
2. Looking at  `config\config.exs`:
	1. The `config` function defines app configuration; ex `config(app, opts)`.
	2. `config(:storex)` defines configuration of our app.
	3. `import_config “#{Mix.env}.exs”` handles environment specific configurations
	4. `config\dev.exs` handles configs for the development environment 
	5. Phoenix database config, similar to `database.yml` 
```
config :storex, Storex.Repo,
	adapter: Ecto.Adapters.Postgres,
	username: “postgres”,
	password: “postgres”,
	database: “storex_dev”,
	hostname: “localhost”,
	pool_size: 10 
```
3. The reason Elixir connotations are so slim is that Elixir has a concept that confirmation built in. It defines a standard way to configure applications and project dependencies abide by the same rules. Ruby doesn’t have configuration primitives in its’ standard library, hence forth YAML configuration and project initializers. 

### deps
1. Contains the source code for dependencies. In Rails this directory would be the `*\gems\*` dumping ground.

### lib
1. The application home divided into two:
	1. Business domain and application code: `storex`
	2. Web layer: `storex_web`
2.  

