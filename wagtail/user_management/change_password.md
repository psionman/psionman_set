---
layout: page
title: ""
---

[Introduction]({{ site.baseurl }}{% link wagtail/user_management/introduction.md %})
[Logout user]({{ site.baseurl }}{% link wagtail/user_management/logout.md %})
[Login user]({{ site.baseurl }}{% link wagtail/user_management/login.md %})

### Change Password

This assumes that the *user* app has already been created (see [introduction]({{ site.baseurl }}{% raw %}{%{% endraw %} raw %}{% raw %}{%{% endraw %}{% raw %}{%{% endraw %} endraw %} link wagtail/user_management/introduction.md %}))

In this  process we will use the Django provided *PasswordChangeForm* form.

1. In *urls.py*
    ```python

      urlpatterns = [
          ...
          path(r'change-password/', views.change_password, name='change_password'),
          ]
    ```

1. in *views.py*

    ```python
    from django.contrib.auth.forms import PasswordChangeForm

    def change_password(request):
        display_form = True
        if request.method == 'POST':
            form = PasswordChangeForm(request.user, request.POST)
            if form.is_valid():
                user = form.save()
                update_session_auth_hash(request, user)
                messages.success(request, 'Your password was successfully updated!')
                display_form = False
                # return redirect('change_password')
            else:
                messages.error(request, 'Please correct the error below.')
        else:
            form = PasswordChangeForm(request.user)
        url = 'users/change_password.html'
        return render(request, url, {'form': form, 'display_form': display_form})

    ```
1. In *change_password.html*
    ```html
    {% raw %}{%{% endraw %} extends "base.html" %}

    {% raw %}{%{% endraw %} block content %}
        {% raw %}{%{% endraw %} if messages %}
            <ul class="messages">
                {% raw %}{%{% endraw %} for message in messages %}
                <li {% raw %}{%{% endraw %} if message.tags %} class="{{ message.tags }}"{% raw %}{%{% endraw %} endif %}>{{ message }}</li>
                {% raw %}{%{% endraw %} endfor %}
            </ul>
        {% raw %}{%{% endraw %} endif %}
        <br>
        {% raw %}{%{% endraw %} if display_form %}
            {% raw %}{%{% endraw %} if user.username %}
                Your are logged in as: {{ user.username }}
                <br>
                <form method="post">
                    {% raw %}{%{% endraw %} csrf_token %}
                    {{ form }}
                    <button type="submit">Save changes</button>
                </form>
            {% raw %}{%{% endraw %} else %}
                You are not logged in!
            {% raw %}{%{% endraw %} endif %}
        {% raw %}{%{% endraw %} endif %}
        <a href="/">Home</a>
    {% raw %}{%{% endraw %} endblock %}
    ```

[Introduction]({{ site.baseurl }}{% link wagtail/user_management/introduction.md %})
[Logout user]({{ site.baseurl }}{% link wagtail/user_management/logout.md %})
[Login user]({{ site.baseurl }}{% link wagtail/user_management/login.md %})
