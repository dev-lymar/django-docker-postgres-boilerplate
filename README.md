[![Python](https://img.shields.io/badge/Python-3.12.2-3776AB?style=flat&logo=Python&logoColor=yellow)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-5.1.2-092E20?style=flat&logo=django&logoColor=white)](https://www.django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL--336791?style=flat&logo=PostgreSQL&logoColor=white)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker--2496ED?style=flat&logo=Docker&logoColor=white)](https://www.docker.com/)
[![Psycopg2](https://img.shields.io/badge/Psycopg2-2.9.10-4169E1?style=flat)](https://pypi.org/project/psycopg2-binary/)
[![Poetry](https://img.shields.io/badge/Poetry--60A5FA?style=flat&logo=poetry&logoColor=white)](https://python-poetry.org/)

# Django Boilerplate with Docker Compose, Makefile, and PostgreSQL

## Table of Contents

- [Project Description](#Project-Description)
- [Requirements](#Requirements)
- [Quick Start](#Quick-Start)
- [Project Structure](#Project-Structure)
- [Implemented Makefile Commands](#Implemented-Makefile-Commands)
- [License](#license)

## Project Description

This starter template is designed for Django projects and is configured to streamline development with Docker Compose, PostgreSQL, and a Makefile for common commands. 
It provides a production-ready environment with minimal initial configuration, ideal for getting a Django project up and running quickly.

### Features
- ***Django:*** Pre-configured Django project structure with [local.py](#localpy) settings file for easy local setup.
- ***Docker Compose:*** Manages containerized services for the Django application and PostgreSQL database.
- ***PostgreSQL:*** Configured as the default database, ready to run in a Docker container.
- ***Makefile:*** Provides easy-to-use commands for frequent tasks like building containers, starting the development server, running migrations, and managing static files.
- ***Environment Variables:*** .env.example included to simplify configuration of database credentials and other sensitive settings.

## Requirements
*To use this boilerplate, ensure you have the following installed on your machine:*

- ***Docker:*** Required for containerizing the Django application and PostgreSQL database.
  - [Install Docker](https://docs.docker.com/get-docker/)
- ***Docker Compose:*** Used to manage multiple Docker containers in a single setup.
  - Docker Desktop includes Docker Compose. Alternatively, install it separately: [Docker Compose Installation](https://docs.docker.com/compose/install/)
- ***Make:*** Allows simplified command execution using the Makefile.
  - *Linux/macOS:* Make is usually pre-installed. If not, install it via your package manager:
```sh
   # Ubuntu/Debian
   sudo apt install make

   # macOS (with Homebrew)
   brew install make
```
  - *Windows:* Use make with [Git Bash](https://gitforwindows.org/) or [WSL](https://docs.microsoft.com/en-us/windows/wsl/install) (Windows Subsystem for Linux).

## Quick Start

1. **Clone the repository:**

   ```sh
   git clone https://github.com/dev-lymar/django-docker-postgres-boilerplate.git
   cd django-docker-postgres-boilerplate
   ```

2. Setup environment variables from .env.example:
```sh
    cp .env.example .env
```

3. Run project 
```sh
   make app
```

### local.py

For ease of development, you can create a `local.py` file within `core/project/settings` to customize local configurations:
   ```sh
   from .main import *
   
   
   DEBUG = True
   ```
This allows for local overrides without risking accidental changes in the production environment.

## Project Structure

*The project structure is organized to keep core components isolated and manageable:*

```sh
.
├── Dockerfile
├── LICENSE
├── Makefile
├── README.md
├── core
│   ├── apps
│   │   └── products
│   │       ├── admin.py
│   │       ├── apps.py
│   │       ├── migrations
│   │       └── models.py
│   └── project
│       ├── settings
│       │   ├── local.py
│       │   └── main.py
│       ├── urls.py
│       └── wsgi.py
├── docker_compose
│   ├── app.yaml
│   └── storages.yaml
├── entrypoint.sh
├── .env
├── manage.py
├── poetry.lock
└── pyproject.toml
```

- **core/apps/products** - Example application with basic structure files (`admin.py`, `apps.py`, etc.).
- **core/project/settings** - Main settings folder with `main.py` (production settings) and `local.py` (for development overrides).
- **docker_compose** - Contains `app.yaml` and `storages.yaml` for Docker Compose configurations.

### Adding a New Django Application
#### To add a new Django application within the `core/apps` directory:

- Run the following command, replacing `newapp` with your app's name:
```sh
  django-admin startapp newapp core/apps/newapp
```
- Register the new application in `INSTALLED_APPS` in the `core/project/settings/main.py` file:
```sh
    INSTALLED_APPS = [
    # Other installed apps...
    'core.apps.newapp',
]
```

## Implemented Makefile Commands

* `make app` - Starts the application and database/infrastructure.
* `make app-logs` - Follow the logs in app container.
* `make app-down` - Down application and all infrastructure.
* `make storages` - Up only infrastructure. You should run your application locally for debugging/developing purposes.
* `make storages-logs` - Follow the logs in storages containers.
* `make storages-down` - Down all infrastructure.
* `make postgres` - Enter postgres container.

### Most Used Django Specific Commands

* `make migrations` - Make migrations to models
* `make migrate` - Apply all made migrations
* `make collectstatic` - Collect static
* `make superuser` - Create admin user

## License

This project is licensed under the MIT License. See the LICENSE file for more information.