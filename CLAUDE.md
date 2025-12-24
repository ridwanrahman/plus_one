# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Django 6.0 web application using the `src` directory pattern for project configuration. The project uses `uv` for dependency management and SQLite for the database.

## Development Commands

### Environment Setup
```bash
# Activate virtual environment
source .venv/bin/activate

# Install dependencies
uv sync

# Install with dev dependencies
uv sync --group dev

# Install with production dependencies
uv sync --group prod
```

### Running the Application
```bash
# Start development server
python manage.py runserver

# Start on custom port
python manage.py runserver 8080
```

### Database Management
```bash
# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Open database shell
python manage.py dbshell
```

### Django Shell
```bash
# Interactive Python shell with Django context
python manage.py shell
```

### Testing
```bash
# Run all tests
python manage.py test

# Run tests for specific app
python manage.py test app_name

# Run specific test
python manage.py test app_name.tests.TestClassName.test_method_name

# Run with verbose output
python manage.py test --verbosity=2
```

### Static Files
```bash
# Collect static files (for production)
python manage.py collectstatic
```

## Project Architecture

### Configuration Structure
- **Settings Module**: `src.settings` - Main Django configuration
- **URL Configuration**: `src.urls` - Root URL routing (currently only admin)
- **WSGI/ASGI**: Entry points in `src/wsgi.py` and `src/asgi.py`

### Settings Configuration
- **Django Version**: 6.0
- **Database**: SQLite (`db.sqlite3` in project root)
- **Secret Key**: Development key present in settings (should be moved to environment variable for production)
- **Debug Mode**: Currently enabled (DEBUG = True)
- **Installed Apps**: Only default Django apps (admin, auth, contenttypes, sessions, messages, staticfiles)

### Project Layout
- The Django project uses the `src/` directory pattern rather than having settings at the root
- `manage.py` references `src.settings` as the settings module
- Django apps should be created as siblings to the `src/` directory or within a dedicated `apps/` directory

### Creating New Apps
When creating new Django apps:
```bash
# Create app in project root
python manage.py startapp app_name

# Or create in an apps directory
mkdir -p apps
python manage.py startapp app_name apps/app_name
```

After creating an app:
1. Add it to `INSTALLED_APPS` in `src/settings.py`
2. Create app-specific URLs and include them in `src/urls.py`
3. Run migrations if models are added

### Development vs Production
- **Dev dependencies**: `django-debug-toolbar` for debugging
- **Prod dependencies**: `gunicorn` for production WSGI server
- Remember to set `DEBUG = False` and configure `ALLOWED_HOSTS` for production
- Use environment variables for sensitive settings (SECRET_KEY, database credentials, etc.)
