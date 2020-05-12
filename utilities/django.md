---
    layout: page
    title:  ""
---

## Django

To remove all of the *migration* files in the current directory

Get the [instructions here](https://simpleisbetterthancomplex.com/tutorial/2016/07/26/how-to-reset-migrations.html)

```bash
find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
```
