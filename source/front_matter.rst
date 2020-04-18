Front Matter
************

Front matter is where we store information about the pages on the site, e.g. Tite, Author etc.

Refer to the default page craeted by Jekyll. The front matter is conrtained in the top section delimited by '- - -'.
 
.. code-block:: console

    ---
    layout: post
    title:  "Welcome to Jekyll!"
    date:   2020-03-23 17:03:52 +0000
    categories: jekyll update
    ---
  
Note: these are key-value pairs.

Changing a value, e.g. *title*, immediately updates the html!

Click on the "Welcome to Jekyll!" link on the web page and note that the url is built using data from front matter.

New key value pairs can be created, e.g. 
 
.. code-block:: console

    author; "Jeff"
    
You can create a new front matter valuecall *permalink* to define a url for a page.

