# elixir-phoenix-rest-api


https://www.dairon.org/2020/07/06/simple-rest-api-with-elixir-phoenix.html

Steps 

1.
``` 
    $ mix phx.new books_api --no-html --no-webpack --binary-id && cd books_api
    * creating books_api/config/config.exs
* creating books_api/config/dev.exs
* creating books_api/config/prod.exs
* creating books_api/config/prod.secret.exs
* creating books_api/config/test.exs
* creating books_api/lib/books_api/application.ex
* creating books_api/lib/books_api.ex
* creating books_api/lib/books_api_web/channels/user_socket.ex
* creating books_api/lib/books_api_web/views/error_helpers.ex
* creating books_api/lib/books_api_web/views/error_view.ex
* creating books_api/lib/books_api_web/endpoint.ex
* creating books_api/lib/books_api_web/router.ex
* creating books_api/lib/books_api_web/telemetry.ex
* creating books_api/lib/books_api_web.ex
* creating books_api/mix.exs
* creating books_api/README.md
* creating books_api/.formatter.exs
* creating books_api/.gitignore
* creating books_api/test/support/channel_case.ex
* creating books_api/test/support/conn_case.ex
* creating books_api/test/test_helper.exs
* creating books_api/test/books_api_web/views/error_view_test.exs
* creating books_api/lib/books_api/repo.ex
* creating books_api/priv/repo/migrations/.formatter.exs
* creating books_api/priv/repo/seeds.exs
* creating books_api/test/support/data_case.ex
* creating books_api/lib/books_api_web/gettext.ex
* creating books_api/priv/gettext/en/LC_MESSAGES/errors.po
* creating books_api/priv/gettext/errors.pot

Fetch and install dependencies? [Yn] Y
* running mix deps.get
* running mix deps.compile

We are almost there! The following steps are missing:

    $ cd books_api

Then configure your database in config/dev.exs and run:

    $ mix ecto.create

Start your Phoenix app with:

    $ mix phx.server

You can also run your app inside IEx (Interactive Elixir) as:

    $ iex -S mix phx.server

```

``` 
$ cd books_api/

$ mix ecto.create
Compiling 11 files (.ex)
Generated books_api app
The database for BooksApi.Repo has already been created
```

``` 
$ mix phx.server
[info] Running BooksApiWeb.Endpoint with cowboy 2.9.0 at 0.0.0.0:4000 (http)
[info] Access BooksApiWeb.Endpoint at http://localhost:4000
```

DB changes 
``` 


```

```
connect to db Image pacto


```

``` 
drop schema

$ mix ecto.drop   
** (Mix) The database for BooksApi.Repo couldn't be dropped: ERROR 55006 (object_in_use) database "books_api_dev" is being accessed by other users
There is 1 other session using the database.
```

Close postico connection
``` 
$ mix ecto.drop
The database for BooksApi.Repo has been dropped
```

``` 
$ mix ecto.create
The database for BooksApi.Repo has been created
```

``` 
mix phx.gen.context Store Book books \
> title:string isbn:text:unique description:text price:float authors:array:string
* creating lib/books_api/store/book.ex
* creating priv/repo/migrations/20210607133628_create_books.exs
* creating lib/books_api/store.ex
* injecting lib/books_api/store.ex
* creating test/books_api/store_test.exs
* injecting test/books_api/store_test.exs

Remember to update your repository by running migrations:

    $ mix ecto.migrate

```


``` 
$ mix ecto.migrate
Compiling 2 files (.ex)
Generated books_api app

19:08:46.734 [info]  == Running 20210607133628 BooksApi.Repo.Migrations.CreateBooks.change/0 forward

19:08:46.739 [info]  create table books

19:08:46.749 [info]  create index books_isbn_index

19:08:46.755 [info]  == Migrated 20210607133628 in 0.0s

```

TODO >>image3


``` 
$ mix phx.gen.json Store Book books \
> title:string isbn:text:unique description:text price:float authors:array:string --no-context --no-schema
You are generating into an existing context.

The BooksApi.Store context currently has 6 functions and 1 files in its directory.

  * It's OK to have multiple resources in the same context as long as they are closely related. But if a context grows too large, consider breaking it apart

  * If they are not closely related, another context probably works better

The fact two entities are related in the database does not mean they belong to the same context.

If you are not sure, prefer creating a new context over adding to the existing one.

Would you like to proceed? [Yn] Y
* creating lib/books_api_web/controllers/book_controller.ex
* creating lib/books_api_web/views/book_view.ex
* creating test/books_api_web/controllers/book_controller_test.exs
* creating lib/books_api_web/views/changeset_view.ex
* creating lib/books_api_web/controllers/fallback_controller.ex

Add the resource to your :api scope in lib/books_api_web/router.ex:

    resources "/books", BookController, except: [:new, :edit]

```

change router.ex
``` 
  scope "/api", BooksApiWeb do
    pipe_through :api
    resources "/books", BookController, except: [:new, :edit]
  end
```

``` 
$ mix phx.server
Compiling 5 files (.ex)
Generated books_api app
[info] Running BooksApiWeb.Endpoint with cowboy 2.9.0 at 0.0.0.0:4000 (http)
[info] Access BooksApiWeb.Endpoint at http://localhost:4000

```

