Juntagrico Heroku Template for cookiecutter
===========

This template sets up a project to be used with juntagrico.science as hosting.

# Local development

Install [uv](https://docs.astral.sh/uv/), then create the pinned Python 3.11 environment and install the locked dependencies:

```shell
uv sync
```

The application uses PostgreSQL by default. A disposable local instance can be started with Docker:

```shell
docker run --name solila-db \
  -e POSTGRES_USER=solila \
  -e POSTGRES_PASSWORD=solila \
  -e POSTGRES_DB=juntagrico \
  -p 5432:5432 \
  -v solila-db-pg15:/var/lib/postgresql/data \
  -d postgres:15
```

On subsequent starts, use `docker start solila-db`. See [notes.md](notes.md) if you need to restore an existing database dump.

Initialize Django and create a local administrator:

```shell
uv run manage.py migrate
uv run manage.py createsuperuser
uv run manage.py create_member_for_superusers
```

Optionally create test data:

```shell
uv run manage.py generate_testdata
# Or, for a larger data set:
uv run manage.py generate_testdata_advanced
```

Run the development server:

```shell
uv run manage.py runserver
```

The environment is managed by `pyproject.toml` and `uv.lock`; use `uv add <package>` when adding a dependency.

# Heroku

you have to login to a heroku bash and setup the db and create the admin user as desbribed in the UNIX section
    
    




