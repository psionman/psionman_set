Introduction
************

Jekyll is a tool for building static websites; particularly thiose hosted on  github.

To install Jekyll on linux, follow `these instructions <https://jekyllrb.com/docs/installation/ubuntu/>`_.

Create a new site
=================

1. To create a site called *ga_blog*, in your project directory:

.. code-block:: console

    $ jekyll new ga_blog
    
    $ cd ga_blog
    
2. To run the webserver For the first time:

.. code-block:: console

    bundle exec jekyll serve
    
Thereafter:

.. code-block:: console

    jekyll serve

3. Main files and dirtectories:

* *_posts* is the source folder;
* *_site* is where the built html is placed;
* *_config.yml* file holds site settings;
* *Gemfile* stores the *Ruby* dependencies for the site.
