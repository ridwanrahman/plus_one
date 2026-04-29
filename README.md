# plus_one

## Prerequisites

- Python 3.13+
- `uv` installed

## Setup

From the project root, install dependencies:

```bash
uv sync
```

Optional dependency groups:

```bash
uv sync --group dev
uv sync --group prod
```

## Database setup

Apply migrations:

```bash
uv run python manage.py migrate
```

If you add or change models, create migrations first:

```bash
uv run python manage.py makemigrations
uv run python manage.py migrate
```

## Create admin user

```bash
uv run python manage.py createsuperuser
```

## How to run project

Start the development server:

```bash
uv run python manage.py runserver
```

Open:

- `http://127.0.0.1:8000/`
- `http://127.0.0.1:8000/admin/`

## Optional checks

```bash
uv run python manage.py check
uv run python manage.py test
```

