---
layout: page
title: ""
---
[Logout user]({{ site.baseurl }}{% link wagtail/user_management/logout.md %})
[Login user]({{ site.baseurl }}{% link wagtail/user_management/login.md %})
[Change password]({{ site.baseurl }}{% link wagtail/user_management/change_password.md %})

### Wagtail user management

This document assumes that you have a Wagtail project up and running ([see Start Project]({{ site.baseurl }}{% link wagtail/start_project.md %})). It will take you through the steps that you need to follow to set up pages and links that will allow a *registered* user to login, log out and change their password.

1. Create a new app *users*

    ```bash
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

1. To run this project I am using a menu page:

    ``` html
    {% raw %}{% block content %}{% endraw %}
    Your are logged in as: {{ user.username }}
    <p></p>
    <a href="/users/logout">Logout</a>
    <p></p>
    <a href="/users/login">Login</a>
    <p></p>
    <a href="/users/change-password">Change password</a>
    {% raw %}{% endblock %}{% endraw %}
    ```
[Logout user]({{ site.baseurl }}{% link wagtail/user_management/logout.md %})
[Login user]({{ site.baseurl }}{% link wagtail/user_management/login.md %})
[Change password]({{ site.baseurl }}{% link wagtail/user_management/change_password.md %})
