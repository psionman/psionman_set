---
    layout: page
    title:  ""
---

## Python snippets

1. Walk all files and directories:
    ```python
    import os

    rootDir = '.'
    for directory_name, subdir_list, file_list in os.walk(rootDir):
        for file_name in file_list:
            file_path = os.sep.join([directory_name, file_name])
            print('\t%s' % file_path)
    ```
