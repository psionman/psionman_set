---
    layout: page
    title:  ""
---


### Python Scaffold

(N.B. good version of basic wx screen, UserManagement, and Database at github:bridgeclub)

To set up a python project  (e.g. a wxPython project):

1. Create  a respository on github called *\<project>*.

1. Clone the respository. This will create a directory *\<project>*.

1. Create the directory structure below *\<project>*

        .
        ├── <project>
        │   ├── application
        │   │   ├── application.py
        │   │   ├── config.py
        │   │   ├── __init__.py
        │   │   ├── main.py
        │   │   ├── screen_objects.py
        │   │   └── screen.py
        │   ├── __init__.py
        │   └── __main__.py
        └── README.md

1. *\_\_main\_\_.py* looks like:

    ```python
    """
    Application launcher for <project>
    """

    import sys
    from .application.main import ProjectClass


    def main(args=None):
      """The main routine."""
      if args is None:
        args = sys.argv[1:]

      print("This is the main routine for <project>.")
      ProjectClass()


      if __name__ == "__main__":
        main()
    ```
1. In *\<project>/main.py*:

    ```python
    """Run ProjectClass."""

    import wx

    from .application import App
    from .screen import MainFrame


    class Application(object):
        """Run the application."""
        def __init__(self):
            app = App()
            MainFrame(app)
            pass


    class ProjectClass(object):
        """Start the wxPython loop."""
        wx_app = wx.App()
        Application()
        wx_app.MainLoop()


    if __name__ == '__main__':
        ProjectClass()
    ```
1. This can then be run form the main *\<project>* directory
  ```console
  python -m <project>
  ```
