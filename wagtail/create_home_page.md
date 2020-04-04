---
layout: page
title: ""
---


### Create Home Page with custom fields

1. In *\<project\>/home/models.py:*

    define the home page html template (this appears to be documentary):

    ``` python
    from wagtail.core.models import Page

    class HomePage(Page):
        """Home page template"""
        template = "home/home_page.html"
    ```

    This points to the html for your home page created in 2. below.

2. Create *\<project\>/\<project\>/templates/home/home\_page.html*

3. In here, place the code:

    ``` html
    {% raw %}{% block content %}{% endraw %}
        "This is my home page"
    {% raw %}{% endblock %}{% endraw %}
    ```

    This overrides the default wagtail site page.

4. Enter the admin page 127.0.0.1/admin and click on Pages\>Home\>Edit and there is only one field: Title. This has the content "Home".

5. To create a custom field (in this case one called "banner\_title"),
    in models:

    ``` python
    from wagtail.admin.edit_handlers import FieldPanel


    class HomePage(Page):
    """Home page template"""
        templates = "home/home_page.html"

        banner_title = models.CharField(max_length=100, blank=False, null=True)
        content_panels = Page.content_panels +[
            FieldPanel("banner_title")
    ```

    This defines a new field, *banner\_title*, for the administrator to use when creating home page content.

6.  To use it, we must perform the migration ritual:

    ``` console
    ./manage.py makemigrations
    ./manage.py mmigrate
    ```

​7. In admin, edit the Home page again, and the text "Banner Title" has appeared. (Note the use of "banner\_title" in models.py and how this relates.) Enter some suitable text.

8.To see this on the site we need to reference it in the html. So in *\<project\>/\<project\>/templates/home/home\_page.html*, revise the code as shown:

    ``` html
    {% raw %}{% block content %}{% endraw %}
        {{ self.banner_title }}
    {% raw %}{% endblock %}{% endraw %}
    ```

9.To ensure that you cannot create another **Home** page, in models.py:

     ``` python
    class HomePage(Page):
        ...
        max_count = 1
    ```

​10. Use the **Meta** class to change the display name of the page in the Wagtail admin page.

Currently, the default is "Home Page" (taken from the class name "HomePage" and parsed appropriately). To make it explicit, in *models.py*:

    ``` python
    class HomePage(Page):
        ...
        class Meta:
            verbose_name = "Home Page"
            verbose_name_plural = "Home Pages"
    ```
