---
layout: "page"
title: ""
---
## Wx Python from scratch

[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson04.md %}) \|  [next]({{ site.baseurl }}{% link wx_python/lesson06.md %})

### Check-boxes, getting and setting values, abstracting panels

In previous lessonings we have seen how to create various widgets and how
to organise their layout using BoxSizers. In this lesson we will look at a
special case of laying out widgets: the
[StaticBox](https://wxpython.org/Phoenix/docs/html/wx.StaticBox.html)
and the
[StaticBoxSizer](https://wxpython.org/Phoenix/docs/html/wx.StaticBoxSizer.html).
A StaticBox is surrounded by a border that has an optional label and is
useful for creating a logical grouping of widgets (see Figure 1.). The
StaticBoxSizer is a special case of a BoxSizer designed to fit within
the StaticBox.

![]({{ site.baseurl }}/wx_python/images/staticbox_02.png)

Fig 1. StaticBox with check boxes

#### Creating a StaticBox

The code to produce a StaticBox and its StaticBoxSizer is:

``` python
contact_box = wx.StaticBox(parent=self, label="Contact method")
contact_sizer = wx.StaticBoxSizer(box=contact_box, orient=wx.HORIZONTAL)
```

Note that the StaticBox is created with a reference to the panel as its
parent and the text for the label is passed through. On the other hand,
the StaticBoxSizer uses the StaticBox as its parent. It is simplest to
think of the StaticBoxSizer as sitting in the StaticBox. Using the panel
code here:

``` python
class MainPanel(wx.Panel):
    def __init__(self, parent, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)
        contact_box = wx.StaticBox(parent=self, label="Contact method")
        contact_sizer = wx.StaticBoxSizer(box=contact_box, orient=wx.HORIZONTAL)
        sizer = wx.BoxSizer(orient=wx.VERTICAL)
        sizer.Add(contact_sizer, flag=wx.ALL, border=10)
        self.SetSizer(sizer)
```

we get an empty StaticTextBox with its label:

![]({{ site.baseurl }}/wx_python/images/staticbox_01.png)

Fig 2. Empty StaticBox

#### The CheckBox

To make a single
[CheckBox](https://wxpython.org/Phoenix/docs/html/wx.CheckBox.html) the
code follows the pattern for other widgets:

``` python
cb_contact = wx.CheckBox(parent=contact_box, label="Email", name="Email")
```

You can see that the parent of the CheckBox is the StaticBox, and I've
given the CheckBox its label and a name (which will be useful when we
come to perform some action if the CheckBox is clicked).

#### Binding a method to the CheckBox click

As I indicated above, the StaticBox is intended to organise logically
related widgets. Here I have three, and it makes sense to hold them in a
list:

``` python
self.cb_contacts = []
contacts = ["Home phone", "Mobile", "Email"]
for contact in contacts:
    cb_contact = wx.CheckBox(parent=contact_box, label=contact, name=contact)
    cb_contact.Bind(wx.EVT_CHECKBOX, self.on_cb_contact_click)
    contact_sizer.Add(cb_contact, flag=wx.ALL, border=10)
    self.cb_contacts.append(cb_contact)
```

Here, I have created an empty list to hold the CheckBoxes and created a
list of strings that will be used as the labels (and names) of the
CheckBoxes. Then, in a loop, the CheckBoxes as created (using the
StaticBox as their parent), each one bound to the same event which will
be triggered when the user clicks on the CheckBox, and the CheckBoxes
are added to the StaticBoxSizer and then appended to the list of
CheckBoxes.

When this code is inserted into the panel creation code, it produces the
frame shown in Figure 1.

#### Retrieving the value of a widget

From the user's point of view, a CheckBox is either checked or not and
wxPython interprets these values as *True* and *False* respectively. In
the following snippet I show the code that I have written to handle the
user clicking on one of the CheckBoxes. It loops through the list of
CheckBoxes, finds which are checked using the *GetValue* function, and
generates and prints an appropriate string using the *GetName* function
to retrieve the CheckBoxes name:

``` python
def on_cb_contact_click(self, event):
    del event
    contact_string = ""
    for cb_contact in self.cb_contacts:
        if cb_contact.GetValue():
            contact_string = ", ".join([contact_string, cb_contact.GetName()])
    print("Contact methods: {}".format(contact_string[2:]))
```

#### Abstracting widgets to their own function

As you can see, the code for creating the set of CheckBoxes is getting
quite lengthy, and as it is all related to one aspect of the panel, it
makes sense to abstract it to a function of its own that returns the
sizer containing the *StaticBoxSizer*:

``` python
def create_contact_sizer(self):ntact method")
    sizer = wx.StaticBoxSizer(box=contact_box, orient=wx.HORIZONTAL)
    self.cb_contacts = []
    contacts = ["Home phone", "Mobile", "Email"]
    for contact in contacts:
        cb_contact = wx.CheckBox(parent=contact_box, label=contact, name=contact)
        cb_contact.Bind(wx.EVT_CHECKBOX, parent.on_cb_contact_click)
        sizer.Add(cb_contact, flag=wx.ALL, border=10)
        self.cb_contacts.append(cb_contact)
    return sizer
```

This greatly simplifies the coding of the MainPanel:

``` python
class MainPanel(wx.Panel):
    def __init__(self, parent, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)
        sizer = wx.BoxSizer(wx.VERTICAL)
        contact_sizer = self.create_contact_sizer()
        sizer.Add(contact_sizer, flag=wx.ALL, border=10)
        self.SetSizer(sizer)
```

#### Summary

In this lesson we have seen how to use a more complex widget: a StaticBox,
which is used with a StaticBoxSizer. We have placed a number of related
CheckBoxes into the StaticBox and seen how we can retrieve the value of
the widgets. Finally, we have abstracted the code related to a logically
related set of widgets to a separate function. This has made the code
easier to read and, ultimately, simpler to maintain. The complete code
for the main panel and its children is
([staticbox.py](snippets/staticbox.py)):

``` python
import wx

class MainPanel(wx.Panel):
    def __init__(self, parent, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)
        sizer = wx.BoxSizer(orient=wx.VERTICAL)
        contact_sizer = self.create_contact_sizer()
        sizer.Add(contact_sizer, flag=wx.ALL, border=10)
        self.SetSizer(sizer)

    def on_cb_contact_click(self, event):
        del event
        contact_string = ""
        for cb_contact in self.cb_contacts:
            if cb_contact.GetValue():
                contact_string = ", ".join([contact_string, cb_contact.GetName()])
        print("Contact methods: {}".format(contact_string[2:]))

    def on_cmd_quit_click(self, event):
        del event
        quit()

    def create_contact_sizer(self):
        contact_box = wx.StaticBox(parent=self, label="Contact method")
        sizer = wx.StaticBoxSizer(box=contact_box, orient=wx.HORIZONTAL)
        self.cb_contacts = []
        contacts = ["Home phone", "Mobile", "Email"]
        for contact in contacts:
            cb_contact = wx.CheckBox(parent=contact_box, label=contact, name=contact)
            cb_contact.Bind(wx.EVT_CHECKBOX, self.on_cb_contact_click)
            sizer.Add(cb_contact, flag=wx.ALL, border=10)
            self.cb_contacts.append(cb_contact)
        return sizer
```

In the next lesson I will look at the RadioButton and introduce the most
flexible of wxPython's sizers: the GridBagSizer

[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson04.md%}) \|  [next]({{ site.baseurl }}{% link wx_python/lesson06.md%})