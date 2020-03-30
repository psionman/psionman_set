---
layout: "page"
title: ""
---
[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson07.md %}) \|  [next]({{ site.baseurl }}{% link wx_python/lesson09.md %})

### A menu bar and status bar

So far, all of the widgets that we have built and used have been placed
on a panel, which was itself, a child of the main frame. Menu bars and
status panels are different in that they are themselves directly
children of the frame.

#### A menu bar

### Terminology

To start with, let us consider the terminology used in the construction
and use of a menu.

![]({{ site.baseurl }}/wx_python/images/menu_00.png)

Fig 1. A simple menu bar

In Fig 1, we can see a simple menu bar:

1.  each element **File**, **Edit**, and **Help** are termed *menus*;
2.  the elements that have dropped down from the **File** menu (**New**,
    **Open**, etc.) are *menu items*;
3.  the whole structure appearing on the frame is the *menu bar*.

### Constructing a menu bar

In order to keep the frame simple and clean, and to separate concerns,
we will build the menu bar in its own class.

Let us start with a simple basic frame containing no panels or widgets:

``` python
import wx

class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        self.Show()

if __name__ == "__main__":
    screen_app = wx.App()
    main_frame = MainFrame(parent=None, title="Frame with menu and status panel")
    screen_app.MainLoop()
```

In order to use a menu bar it is necessary to call the **SetMenuBar**
method for the frame. The argument for this method must be an instance
of a *wx.MenuBar* class.

``` python
class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        self.SetMenuBar(MenuBar(self))
        self.Show()

class MenuBar(wx.MenuBar):
    def __init__(self, parent):
        wx.MenuBar.__init__(self)
        pass
```

So far, the menu bar does nothing: no menus have been created yet.

### Menus

First we need to define the *menus* that will appear on the menu bar,
for example, **File**, **Edit**, **Help**. Then we proceed to create
*menu items*, for example **New**, **Open**, **Save** etc., that will be
attached to their respective menus.

A *menu* is an instance of *wx.Menu* which is created and then
**appended** to the menu bar. As each menu can, potentially, have many
items, I will abstract the creation of each menu to its own class to
simplify maintenance and to aid readability and reusability:

``` python
class MenuBar(wx.MenuBar):
    def __init__(self, parent):
        wx.MenuBar.__init__(self)
        file_menu = FileMenu(self)
        self.Append(file_menu, '&File')

class FileMenu(wx.Menu):
    def __init__(self, parent):
        wx.Menu.__init__(self)
```

Now the file menu appears on the frame, but still, it does nothing. We
need to add menu items:

![]({{ site.baseurl }}/wx_python/images/menu_01.png)

Fig 2. A Frame with menu bar

### Menu items

Menu items will drop down when the mouse is clicked on a menu.
Typically, there will be many menu items associated with a menu. To
start with I will create a single item for the **File** menu: the
**Open** menu item. A *menu item* is an instance of the *wx.MenuItem*
class. It has the menu as its parent and, like a button, can be given a
[StandardID](https://wxpython.org/Phoenix/docs/html/wx.StandardID.enumeration.html)
or a label; in this case I will use a StandardID:

``` python
class MenuBar(wx.MenuBar):
    def __init__(self, parent):
        wx.MenuBar.__init__(self)
        file_menu = FileMenu(self)
        self.Append(file_menu, '&File')

class FileMenu(wx.Menu):
    def __init__(self, parent):
        wx.Menu.__init__(self)
        new_menu_item = wx.MenuItem(parentMenu=self, id=wx.ID_NEW)
        self.Bind(wx.EVT_MENU, self.on_new_menu_click, id=wx.ID_NEW)
        self.Append(new_menu_item)

    def on_new_menu_click(self, event):
        print('New clicked')
```

Note that here, I have not only created the menu item, but bound it to a
method and appended it to the menu itself using its **Append** method.
When the menu is clicked it now appears as:

![]({{ site.baseurl }}/wx_python/images/menu_02.png)

Fig 3. A menu with a menu item

Creating more menus and more menu items is simply a case of repeating
the above steps ([menu.py](snippets/menu.py)).

#### A Status bar

In order to demonstrate the use of a status bar I will start with the
same basic frame used at the top of this lesson. As the status bar is
closely bound to the frame and its implementation is quite simple I will
not be abstracting it to a separate class. To create it, simply use the
line:

``` python
self.status_bar = self.CreateStatusBar()
```

To set the text, use the **SetStatusText** method:

``` python
self.status_bar.SetStatusText('This is the status bar')
```

![]({{ site.baseurl }}/wx_python/images/statusbar_01.png)

Fig 4. A frame with a status bar

The full code for this frame is ([menu.py](snippets/menu.py)):

``` python
import wx
class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        self.status_bar = self.CreateStatusBar()
        self.status_bar.SetStatusText('This is the status bar')
        self.Show()

if __name__ == "__main__":
    screen_app = wx.App()
    main_frame = MainFrame(parent=None, title="Frame with status bar")
    screen_app.MainLoop()
```

#### Summary

In this lesson I have described the use of two widgets that are linked
directly to the frame: the menu bar and the status bar
([menu.py](snippets/menu.py)). In the next lesson I will create a larger
application from many of the elements that we have seen so far and show
how code can be organised to simplify coding and maintenance.

[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson07.md%}) \|  [next]({{ site.baseurl }}{% link wx_python/lesson09.md%})