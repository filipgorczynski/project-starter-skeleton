{{cookiecutter.project_name}}
{{ '=' * cookiecutter.project_name|length }}

{{cookiecutter.description}}

.. image:: https://img.shields.io/badge/built%20with-Cookiecutter%20Django-ff69b4.svg
     :target: https://github.com/pydanny/cookiecutter-django/
     :alt: Built with Cookiecutter Django
.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
     :target: https://github.com/ambv/black
     :alt: Black code style
{% if cookiecutter.open_source_license != "Not open source" %}

:License: {{cookiecutter.open_source_license}}
{% endif %}

Settings
--------

Moved to settings_.

.. _settings: http://cookiecutter-django.readthedocs.io/en/latest/settings.html

Basic Commands
--------------

Setting Up Your Users
^^^^^^^^^^^^^^^^^^^^^

* To create a **normal user account**, just go to Sign Up and fill out the form. Once you submit it, you'll see a "Verify Your E-mail Address" page. Go to your console to see a simulated email verification message. Copy the link into your browser. Now the user's email should be verified and ready to go.

* To create an **superuser account**, use this command::

    $ python manage.py createsuperuser

For convenience, you can keep your normal user logged in on Chrome and your superuser logged in on Firefox (or similar), so that you can see how the site behaves for both kinds of users.

Type checks
^^^^^^^^^^^

Running type checks with mypy:

::

  $ mypy {{cookiecutter.project_slug}}

Test coverage
^^^^^^^^^^^^^

To run the tests, check your test coverage, and generate an HTML coverage report::

    $ coverage run -m pytest
    $ coverage html
    $ open htmlcov/index.html

Running tests with py.test
~~~~~~~~~~~~~~~~~~~~~~~~~~

::

  $ pytest

Live reloading and Sass CSS compilation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Moved to `Live reloading and SASS compilation`_.

.. _`Live reloading and SASS compilation`: http://cookiecutter-django.readthedocs.io/en/latest/live-reloading-and-sass-compilation.html

{% if cookiecutter.use_celery == "y" %}

Celery
^^^^^^

This app comes with Celery.

To run a celery worker:

.. code-block:: bash

    cd {{cookiecutter.project_slug}}
    celery -A config.celery_app worker -l info

Please note: For Celery's import magic to work, it is important *where* the celery commands are run. If you are in the same folder with *manage.py*, you should be right.

{% endif %}
{% if cookiecutter.use_mailhog == "y" %}

Email Server
^^^^^^^^^^^^
{% if cookiecutter.use_docker == 'y' %}
In development, it is often nice to be able to see emails that are being sent from your application. For that reason local SMTP server `MailHog`_ with a web interface is available as docker container.

Container mailhog will start automatically when you will run all docker containers.
Please check `cookiecutter-django Docker documentation`_ for more details how to start all containers.

With MailHog running, to view messages that are sent by your application, open your browser and go to ``http://127.0.0.1:8025``
{% else %}
In development, it is often nice to be able to see emails that are being sent from your application. If you choose to use `MailHog`_ when generating the project a local SMTP server with a web interface will be available.

#. `Download the latest MailHog release`_ for your OS.

#. Rename the build to ``MailHog``.

#. Copy the file to the project root.

#. Make it executable: ::

    $ chmod +x MailHog

#. Spin up another terminal window and start it there: ::

    ./MailHog

#. Check out `<http://127.0.0.1:8025/>`_ to see how it goes.

Now you have your own mail server running locally, ready to receive whatever you send it.

.. _`Download the latest MailHog release`: https://github.com/mailhog/MailHog/releases
{% endif %}
.. _mailhog: https://github.com/mailhog/MailHog
{% endif %}
{% if cookiecutter.use_sentry == "y" %}

Sentry
^^^^^^

Sentry is an error logging aggregator service. You can sign up for a free account at  https://sentry.io/signup/?code=cookiecutter  or download and host it yourself.
The system is setup with reasonable defaults, including 404 logging and integration with the WSGI application.

You must set the DSN url in production.
{% endif %}

Deployment
----------

The following details how to deploy this application.
{% if cookiecutter.use_heroku.lower() == "y" %}

Heroku
^^^^^^

See detailed `cookiecutter-django Heroku documentation`_.

.. _`cookiecutter-django Heroku documentation`: http://cookiecutter-django.readthedocs.io/en/latest/deployment-on-heroku.html
{% endif %}
{% if cookiecutter.use_docker.lower() == "y" %}

Docker
^^^^^^

See detailed `cookiecutter-django Docker documentation`_.

.. _`cookiecutter-django Docker documentation`: http://cookiecutter-django.readthedocs.io/en/latest/deployment-with-docker.html
{% endif %}

{% if cookiecutter.custom_bootstrap_compilation == "y" %}
Custom Bootstrap Compilation
^^^^^^

The generated CSS is set up with automatic Bootstrap recompilation with variables of your choice.
Bootstrap v4 is installed using npm and customised by tweaking your variables in ``static/sass/custom_bootstrap_vars``.

You can find a list of available variables `in the bootstrap source`_, or get explanations on them in the `Bootstrap docs`_.

{% if cookiecutter.js_task_runner == 'Gulp' %}
Bootstrap's javascript as well as its dependencies is concatenated into a single file: ``static/js/vendors.js``.
{% endif %}

.. _in the bootstrap source: https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss
.. _Bootstrap docs: https://getbootstrap.com/docs/4.1/getting-started/theming/

{% endif %}



# {{ cookiecutter.project_name }}

[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

### List of services: ###

* Dev server: [https://{{ cookiecutter.domain_name }}/](https://{{ cookiecutter.domain_name }}/)

### Documentation: ###

* [Architecture overview](docs/architecture_overview.md)
* [Backend: Routine tasks](docs/commands.md)
* [Backend: Pre-commit hook](docs/pre_commit_hook.md)

### API documentation: ###

* ReDoc web UI: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/redoc/](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/redoc/)
* Swagger web UI: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger/](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger/)
* Swagger JSON: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.json](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.json)
* Swagger YAML: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.yaml](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.yaml)

### First run: ###

Install Python {{ cookiecutter.python_version }} & setup virtual environment. We recommend to use [pyenv](https://github.com/pyenv/pyenv) & [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv):

```bash
pyenv install {{ cookiecutter.python_version }}
pyenv virtualenv {{ cookiecutter.python_version }} {{ cookiecutter.project_slug }}
pyenv activate {{ cookiecutter.project_slug }}
```

Update `pip` & `setuptools`, install `fabric`, `invoke` & `pip-tools`:

```bash
pip install -U fabric invoke pip pip-tools setuptools
```

Install Python requirements:

```bash
fab pip.sync
```

Copy initial settings for Django project:

```bash
cp ./api/.env.example ./api/.env
```

Generate `SECRET_KEY`:

```bash
./api/manage.py generate_secret_key
```

and write it to `./api/.env`:

```
{{ cookiecutter.project_slug | upper() }}_SECRET_KEY=<your-generated-key>
```

Run backing services (require Docker):

```bash
fab compose.up -d
```

Run migrations:

```bash
./api/manage.py migrate
```

Run Django server:

```bash
fab run
```


# {{ cookiecutter.project_name }}

[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

### List of services: ###

* Dev server: [https://{{ cookiecutter.domain_name }}/](https://{{ cookiecutter.domain_name }}/)

### Documentation: ###

* [Architecture overview](docs/architecture_overview.md)
* [Backend: Routine tasks](docs/commands.md)
* [Backend: Pre-commit hook](docs/pre_commit_hook.md)

### API documentation: ###

* ReDoc web UI: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/redoc/](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/redoc/)
* Swagger web UI: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger/](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger/)
* Swagger JSON: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.json](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.json)
* Swagger YAML: [https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.yaml](https://{{ cookiecutter.domain_name }}/_platform/docs/v1/swagger.yaml)

### First run: ###

Install Python {{ cookiecutter.python_version }} & setup virtual environment. We recommend to use [pyenv](https://github.com/pyenv/pyenv) & [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv):

```bash
pyenv install {{ cookiecutter.python_version }}
pyenv virtualenv {{ cookiecutter.python_version }} {{ cookiecutter.project_slug }}
pyenv activate {{ cookiecutter.project_slug }}
```

Update `pip` & `setuptools`, install `fabric`, `invoke` & `pip-tools`:

```bash
pip install -U fabric invoke pip pip-tools setuptools
```

Install Python requirements:

```bash
fab pip.sync
```

Copy initial settings for Django project:

```bash
cp ./api/.env.example ./api/.env
```

Generate `SECRET_KEY`:

```bash
./api/manage.py generate_secret_key
```

and write it to `./api/.env`:

```
{{ cookiecutter.project_slug | upper() }}_SECRET_KEY=<your-generated-key>
```

Run backing services (require Docker):

```bash
fab compose.up -d
```

Run migrations:

```bash
./api/manage.py migrate
```

Run Django server:

```bash
fab run
```
