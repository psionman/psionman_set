---
layout: page
title: ""
---

[Introduction]({{ site.baseurl }}{% link wagtail/user_management/introduction.md %})
[Login user]({{ site.baseurl }}{% link wagtail/user_management/login.md %})
[Change password]({{ site.baseurl }}{% link wagtail/user_management/change_password.md %})

### User logout

This assumes that the *user* app has already been created (see [introduction]({{ site.baseurl }}{% raw %}{%{% endraw %} link wagtail/user_management/introduction.md %}))

1. In *users/urls.py*:

    ```python    
    from django.urls import path

    from . import views

    urlpatterns = [
            path(r'logout/', views.logout_view, name='logout'),
        ]
    ```
1. In *users/views.py*:

    ```python    
    from django.contrib import messages
    from django.shortcuts import render, redirect
    from django.contrib.auth import authenticate, login, logout

    RETURN_FROM_LOGIN_URL = 'home/home_page.html'
    RETURN_FROM_LOGOUT_URL = RETURN_FROM_LOGIN_URL   

    def logout_view(request):
        logout(request)
        messages.success(request, 'You are now logged out!')
        url = RETURN_FROM_LOGOUT_URL
        return render(request, url)
    ```
[Introduction]({{ site.baseurl }}{% link wagtail/user_management/introduction.md %})
[Login user]({{ site.baseurl }}{% link wagtail/user_management/login.md %})
[Change password]({{ site.baseurl }}{% link wagtail/user_management/change_password.md %})
