---
layout: page
title: ""
---

### Set up a Wagtail user login system

This document assumes that you have a Wagtail application up and running ([see]({{ site.baseurl }}{% link wagtail/start_project.md %})). It will take you through the steps that you need to follow to set up pages and links that will allow a *registered* user to login, log out and change their password.

To run this project I am using a menu page:

``` html
{% raw %}{% block content %}{% endraw %}
Your are logged in as: {{ user.username }}
<p></p>
<a href="">Logout</a>
<p></p>
<a href="">Login</a>
<p></p>
<a href="">Change password</a>
{% raw %}{% endblock %}{% endraw %}
```

1. Create a new app *users*

    ```console
    ./manage.py startapp users
    ```
1. Update *base.py*

    ```python
    INSTALLED_APPS = [
        ...
        'users',
        ...
    ```
1. In *\<project>/urls.py*:

    ```python
    urlpatterns = [
        ...
        url(r'^users/', include('users.urls')),
        ...
    ```
1. In *users/urls.py*:

    ```python    
    from django.urls import path

    from . import views

    urlpatterns = [
            path(r'logout/', views.logout, name='logout'),
        ]
    ```

#### The logout screen

This is the simplest function to provide.
