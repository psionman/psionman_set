---
layout: page
title: ""
---

#### Start project

1. Enter your virtualenv for wagtail (mine is *wagtail*)

    ```console
    workon wagtail
    ```

1.  Create your wagtail project (e.g. **wagtail\_blog**). *NB the wagtail\_blog directory is created by this*.

    ``` console
    wagtail start wagtail_blog
    ```

1.  Change directory to the project directory:

    ``` console
    cd wagtail_blog
    ```

1.  Install requirements:

    ``` console
    pip install -r requirements.txt
    ```

1. Create the *migration* command *mm*:

    ``` console
    python manage.py makemigrations
    python manage.py migrate
    ```
    Save as *mm* and make runnable.

1.  Migrate:

    ``` console
    python manage.py migrate
    ```

1. Create superuser:

    ``` console
    python manage.py createsuperuser
    ```

1. Check it works by running the server and opening url: 127.0.0.1 (to use the default port 8000)

    ``` console
    python manage.py runserver
    ```

    or if you want to use port 8100:

    ``` console
    python manage.py runserver 8100
    ```

The default wagtail site page should appear.

This basic project contains three apps:
* my app *wagtail\_blog*;
* home;
* search.
