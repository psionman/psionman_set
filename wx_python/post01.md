---
layout: "page"
---

## WxPython from Scratch

### Getting started: the frame

Let's define a few terms used by wxPython:

[frame](https://wxpython.org/Phoenix/docs/html/wx.Frame.html):
:   the rectangular window that contains all of the GUI elements, (in
    fact it is usually called a window outside of wxPython (see this
    wiki [article](https://en.wikipedia.org/wiki/Window_(computing)))).
    It usually has a title bar with control buttons, an area to display
    panels, and optionally a menu bar, a tool bar and a status bar;

[widget](https://wxpython.org/Phoenix/docs/html/gallery.html):
:   an element of GUI programming, like a label, a button or, a text
    box;

[panel](https://wxpython.org/Phoenix/docs/html/wx.Panel.html):
:   an area on the frame that contains widgets. For most simple GUI
    applications you will have one panel and it will cover the whole
    frame.

[sizer](https://wxpython.org/Phoenix/docs/html/sizers_overview.html):
:   an invisible rectangular container for widgets. Sizers can contain
    sizers and each panel or frame can have at most one designated
    sizer.

![](psionman_set/wx_python/images/raw_frame.png)

Fig 1. A basic frame

Figure 1. shows a wxPython frame with a title bar. It has no menu bar,
tool bar, status bar, nor any widgets. (It is created by wxPython using
the default size 400x250.) Before we look at how this was constructed,
let's first consider the wxPython main loop.

#### The wxPython main loop

A moment's thought will convince you that a GUI application must run
some sort of loop. Most of the time, the screen sits there waiting for
the user to do something. The application will stay in this loop,
reacting to user events, until it is closed down.

In wxPython the loop is handled by the
[wx.APP](https://wxpython.org/Phoenix/docs/html/wx.App.html) class. The
most basic code for a wxPython loop is
([raw\_frame.py](snippets/raw_frame.py)):

``` python
import wx
screen_app = wx.App()
main_frame = wx.Frame(parent=None, title="Raw frame")
main_frame.Show()
screen_app.MainLoop()
```

and I have used this to code produce the frame shown in Figure 1.

1.  In the first line we import the wxPython module;
2.  then, we create an instance of a wx application (wx.App);
3.  thirdly, we create an instance of a wx Frame (see below). The *None*
    argument is for the frame's parent: in this case there is none;
4.  then tell the system to show the frame;
5.  and finally we start the wx main loop (app.MainLoop).

These five lines sum up the whole application; all of the complexity and
wizardry is involved in creating the frame.

###  The wxPython Frame

In this section we will see how to abstract the frame into its own
class. Later articles will take this simple basis and build more complex
solutions.

The following code takes the frame definition and places it in a class
that inherits wx.Frame:

``` python
class MainFrame(wx.Frame):
     def __init__(self, *args, **kwargs):
         super(MainFrame, self).__init__(*args, **kwargs)
         self.Show()
```

In this snippet, we have:

1.  defined the class **MainFrame** which inherits *wx.Frame*;
2.  defined the dunder-init method for the class;
3.  called the wx.Frame dunder-init method to ensure that the frame is
    correctly initialised;
4.  called the **Show** method for the frame.

In the dunder-init calls I have include *\*args* and *\*\*kwargs*. This
ensures that all of the functionality of *wx.Window*, the base-class of
*wx.Frame*, is inherited by the frame. One use is the ability to set the
frame's title in wxPython loop code stub which condenses the frame's
initialisation argument list.

And that's it. In a few lines of code we have created a frame and
displayed it. It can be maximised, minimised and closed using the
control buttons. Note that the frame picks up the theme that you have
selected for your system (or uses the default if it has not been
changed).

### Summary

The most basic basic element of a GUI program running wxPython is the
*frame*. A frame is created by instantiating an instance of a wx.Frame
class within the wxPython main loop and calling its **Show** method. The
full code is presented below
([basic\_frame.py](snippets/basic_frame.py)):

``` python
import wx


class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        self.Show()

if __name__ == "__main__":
    screen_app = wx.App()
    main_frame = MainFrame(parent=None, title="Basic frame")
    screen_app.MainLoop()
```

In the next post I will show how to create a label and introduce the
concept of a sizer and I will elaborate on the way that I suggest that
code for wxPython is organised.

[home]({{ site.baseurl }}{% link index.md%}) [previous]({{ site.baseurl }}{% link wx_python/introduction.md %}) [next]({{ site.baseurl }}{% link wx_python/post02.md %})
