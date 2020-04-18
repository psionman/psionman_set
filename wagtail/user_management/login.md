---
layout: page
title: ""
---
[Introduction]({{ site.baseurl }}{% link wagtail/user_management/introduction.md %})
[Logout user]({{ site.baseurl }}{% link wagtail/user_management/logout.md %})
[Change password]({{ site.baseurl }}{% link wagtail/user_management/change_password.md %})

### User login

This assumes that the *user* app has already been created (see [introduction]({{ site.baseurl }}{% raw %}{%{% endraw %} link wagtail/user_management/introduction.md %}))

## User login

To support *tabindex* in the *login* we need to create a Django filter

1. In the *home* directory create a directory call *templatetags* with an *__init__.py*

1. in *templatetags* create *app_filters.py*:

    ```python     
    from django import template

    register = template.Library()    

    @register.filter
    def tabindex(value, index):
        """Add a tabindex attribute to the widget for a bound field."""
        value.field.widget.attrs['tabindex'] = index
        return value
    ```
    This will be used in the template (see below).

1. In *forms.py*

    ```python    
    from django import forms
    from django.contrib.auth.models import User


    class LoginForm(forms.ModelForm):
        username = forms.CharField(label='User name', max_length=30)
        password = forms.PasswordInput()

        class Meta:
            model = User
            fields = '__all__'

            widgets = {'password': forms.PasswordInput()}

    ```

1. In *users/urls.py*:

    ```python
    urlpatterns = [
            ...
            path(r'login/', views.login_view, name='login'),
        ]
    ```
1. In *views.py*

    (This assumes the *import* statements in [logout]({{ site.baseurl }}{% raw %}{%{% endraw %} link wagtail/user_management/logout.md %}) have already been inserted.)

    ```python
    from django.http import HttpResponseRedirect

    def login_view(request):
        form_context = {'login_form': LoginForm,}
        url = "users/login.html"
        if request.method == 'POST':
            username = request.POST['username']
            password = request.POST['password']
            user = authenticate(username=username, password=password)
            if user is not None:
                if user.is_active:
                    login(request, user)
                    return HttpResponseRedirect(RETURN_FROM_LOGIN_URL)
                else:
                    messages.error(request, 'Your account is not enabled!')
                context = {}
            else:
                messages.error(request, 'Your username or password was not recognized!')
                context = form_context
        else:
            context = form_context
        return render(request, url, context)
    ```
<br>
1. And in *login.html*

    ```html
    {% raw %}{%{% endraw %} extends "base.html" %}
    {% raw %}{%{% endraw %} load app_filters %}
    {% raw %}{%{% endraw %} block content %}
        <br>
        {% raw %}{%{% endraw %} if form.errors %}
            <p>Your username and password didn't match. Please try again.</p>
        {% raw %}{%{% endraw %} endif %}

        {% raw %}{%{% endraw %} if next %}
            {% raw %}{%{% endraw %} if user.is_authenticated %}
                <p>Your account doesn't have access to this page. To proceed,
                please login with an account that has access.</p>
            {% raw %}{%{% endraw %} else %}
                <p>Please login to see this page.</p>
            {% raw %}{%{% endraw %} endif %}
        {% raw %}{%{% endraw %} endif %}

        <form method="post" action="{% raw %}{%{% endraw %} url 'login' %}">
        {% raw %}{%{% endraw %} csrf_token %}
            <table>
                <tr>
                    <td>{{ login_form.username.label_tag }}</td>
                    <td><div>{{ login_form.username|tabindex:2 }}</div></td>
                    <td rowspan="2"><div tabindex="3"><button type="submit" class="btn btn-success">Login</button></div></td>
                </tr>
                <tr>
                    <td>{{ login_form.password.label_tag }}</td>
                    <td><div>{{ login_form.password|tabindex:2 }}</div></td>
                </tr>
            </table>
        </form>
        {% raw %}{%{% endraw %} if messages %}
            <ul class="messages">
                {% raw %}{%{% endraw %} for message in messages %}
                <li {% raw %}{%{% endraw %} if message.tags %} class="{{ message.tags }}"{% raw %}{%{% endraw %} endif %}>{{ message }}</li>
                {% raw %}{%{% endraw %} endfor %}
            </ul>
        {% raw %}{%{% endraw %} endif %}
    {% raw %}{%{% endraw %} endblock %}
    ```

<br>
[Introduction]({{ site.baseurl }}{% link wagtail/user_management/introduction.md %})
[Logout user]({{ site.baseurl }}{% link wagtail/user_management/logout.md %})
[Change password]({{ site.baseurl }}{% link wagtail/user_management/change_password.md %})
