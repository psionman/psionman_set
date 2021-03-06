---
layout: "page"
title: ""
---
## Wx Python from scratch

[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson08.md %}) \|  [next]({{ site.baseurl }}{% link wx_python/lesson10.md %})

### Building a larger application

So far, I have concentrated on creating one or two widgets and placing
them in a sizer on the panel. In this lesson I will look at the challenges
involved in implementing a more complex layout and structuring the code
for maintainability, readability and reuseability.

The application that I want to construct is shown in Fig 1. I will
concentrate on placing the widgets in the correct location and in
organising the code. The application specific code behind the GUI is
relatively straightforward and I will not take up space on describing
that.

![]({{ site.baseurl }}/wx_python/images/booking_01.png)

Fig 1. A frame for hotel bookings

#### The layout

The first stage in implementing a GUI requirement is to decide on how
the widgets are to be layed out. In Fig 2., I have divided the screen
into regions do demonstrate how a GridBagSizer could be used to create
the gross pattern.

![]({{ site.baseurl }}/wx_python/images/booking_02.png)

Fig 2. Boundaries for GridBagSizer

1.  The top left cell (cell (0, 0)) contains personal details (the
    [PersonPanel](#the-person-panel));
2.  the top right (cell (0, 1)) contains a horizontal *BoxSizer* for the
    room preferences (the [ExtrasPanel](#the-extras-panel) and the
    [RoomPanel](#the-room-panel) );
3.  the middle left (cell (1, 0) contains the city selection, ([the
    CityPanel](#the-city-panel));
4.  the middle right (cell(1, 1)) the [DatePanel](#the-date-panel);
5.  the bottom row (cells(2, 0) and (2, 1)) holds the
    [ButtonPanel](#the-button-panel).

All of the text boxes in the top left cell are left-aligned, and so it
makes sense to place these boxes and their labels in their own
*GridBagSizer*.

The room preference widgets are in separate StaticBoxes which can be
placed in a horizontal *BoxSizer*.

The city selection is in a StaticBox, as are the date fields.

The buttons can be placed in a horizontal *BoxSizer* which will need to
span two columns in the main *GridBagSizer*.

#### The code

I will build up the code for the application in incremental steps and
prsent the full code for the application at then of the lesson.

### The frame

We will start with a basic frame:

``` python
from datetime import datetime
import wx


class MainFrame(wx.Frame):
   def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        self.Show()


if __name__ == "__main__":
    screen_app = wx.App()
    main_frame = MainFrame(parent=None)
    screen_app.MainLoop()
```

I have imported *datetime* from *datetime*. This will be used in the
[DatePanel](#the-date-panel)

### The menu bar

I will add a menu bar to the basic frame . To simplify the code, I have
only used two *menus* and three *menu items* in the **File** menu:

``` python
class MainFrame(wx.Frame):
  def __init__(self, *args, **kwargs):
      super(MainFrame, self).__init__(*args, **kwargs)
      panel = MainPanel(self)
      self.SetMenuBar(MenuBar())
      sizer = wx.BoxSizer()
      sizer.Add(panel)
      self.SetSizerAndFit(sizer)
      self.Show()
```

> class MenuBar(wx.MenuBar):
> :   def \_\_init\_\_(self):
>     :   wx.MenuBar.\_\_init\_\_(self) file\_menu =
>         self.create\_file\_menu() help\_menu =
>         self.create\_help\_menu() self.Append(file\_menu, '&File')
>         self.Append(help\_menu, '&Help')
>
>     def create\_file\_menu(self):
>     :   menu = wx.Menu() clear\_menu\_item =
>         wx.MenuItem(parentMenu=menu, id=wx.ID\_CLEAR) save\_menu\_item
>         = wx.MenuItem(parentMenu=menu, id=wx.ID\_SAVE)
>         quit\_menu\_item = wx.MenuItem(parentMenu=menu,
>         id=wx.ID\_EXIT) menu.Append(clear\_menu\_item)
>         menu.Append(save\_menu\_item) menu.Append(quit\_menu\_item)
>         return menu
>
>     def create\_help\_menu(self):
>     :   help\_menu = wx.Menu() return help\_menu
>
### The status bar

The code to implement the status bar is quite straightforward:

``` python
class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        self.SetMenuBar(MenuBar())
        self.status_bar = self.CreateStatusBar()
        self.status_bar.SetStatusText('New client')
        self.Show()
```

### The panel

Next, I will create the main panel and place it in its sizer in the
frame:

``` python
class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        panel = MainPanel()
        self.SetMenuBar(MenuBar())
        self.status_bar = self.CreateStatusBar()
        self.status_bar.SetStatusText('New client')
        sizer = wx.BoxSizer()
        sizer.Add(panel)
        self.SetSizerAndFit(sizer)
        self.Show()


class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)
        sizer = wx.GridBagSizer(5, 5)
        sizer.Add((200, 100), pos=(0, 0))
        self.SetSizer(sizer)
```

I have created the *GridBagSizer* and added a dummy spacer, (200, 100),
so that we can see that all is well.

### The person sizer

I am going to create the three text boxes and labels relating to name
and email address in a sizer of their own returned by the function
**create\_person\_sizer**. This sizer will be a *GridBagSizer* with
three rows and two columns.

``` python
class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)
        sizer = wx.GridBagSizer(5, 5)
        person_sizer = self.create_person_sizer()

        sizer = wx.GridBagSizer(10, 10)
        sizer.Add(self.person_sizer, pos=(0, 0), flag=wx.TOP|wx.LEFT, border=10)
        self.SetSizer(sizer)

    def create_person_sizer(self):
        lbl_first_name = wx.StaticText(parent=self, label="First name")
        lbl_last_name = wx.StaticText(parent=self, label="Last name")
        lbl_email = wx.StaticText(parent=self, label="Email")
        self.txt_first_name = wx.TextCtrl(parent=self, size=(150, -1))
        self.txt_last_name = wx.TextCtrl(parent=self, size=(150, -1))
        self.txt_email = wx.TextCtrl(parent=self, size=(250, -1))
        sizer = wx.GridBagSizer(5, 5)
        sizer.Add(lbl_first_name, pos=(0, 0))
        sizer.Add(lbl_last_name, pos=(1, 0))
        sizer.Add(lbl_email, pos=(2, 0))
        sizer.Add(self.txt_first_name, pos=(0, 1))
        sizer.Add(self.txt_last_name, pos=(1, 1))
        sizer.Add(self.txt_email, pos=(2, 1))
        return sizer
```

There is nothing new here, but note that I have created the text boxes
as class wide variables. This is essential when we come to handling the
values in these fields programatically in the **MainPanel**.

### The extras sizer

The room sizer is a simple sizer that contains a *StaticBox* and the
three *checkboxes*.

``` python
class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):

        self.extras_list = ["Breakfast", "Newpaper", "Flowers"]
        extras_sizer = self.create_extras_sizer()

    def create_extras_sizer(self):
        extras_box = wx.StaticBox(parent=self, label="Extras")
        sizer = wx.StaticBoxSizer(box=extras_box, orient=wx.VERTICAL)
        self.cb_extras_list = []
        for extras in self.extras_list:
            cb_extras = wx.CheckBox(parent=extras_box, label=extras, name=extras)
            sizer.Add(cb_extras, flag=wx.ALL, border=0)
            self.cb_extras_list.append(cb_extras)
        return sizer
```

Note that here, for convenience in this lessoning, I have defined the
*extras\_list* in the **MainPanel**. The coding in the **ExtrasPanel**
is very similar that used when we covered
[checkboxes](lesson05.html#the-checkbox).

### The room sizer

This sizer contains a *RadioBox*. The code for this was [covered
earlier](lesson06.html#the-radiobutton):

``` python
class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):
        self.room_types = ["Single", "Twin", "Double"]
        room_sizer = self.create_room_sizer()

        preferences_sizer = wx.BoxSizer(wx.HORIZONTAL)
        preferences_sizer.Add(extras_sizer, flag= wx.RIGHT, border=10)
        preferences_sizer.Add(room_sizer)

        sizer.Add(preferences_sizer, pos=(0, 1), flag=wx.TOP, border=10)



    def create_room_sizer(self):
        self.room_box = wx.RadioBox(parent=self, label="Room",
                                    choices=self.room_types,
                                    style=wx.RA_SPECIFY_ROWS)
        sizer = wx.BoxSizer(orient=wx.HORIZONTAL)
        sizer.Add(self.room_box)
        return sizer
```

Here, the **extras\_sizer** and **room\_sizer** have been placed in a
horizontal *BoxSizer* and then added to the *GridBagSizer* in first row
and second column.

### The city sizer

The code to create a *listbox* has already been
[seen](lesson07.html#the-listbox). I have created a sizer to contain the
cities listbox:

``` python
class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):

        self.cities = sorted(["London", "Birmingham", "Glasgow", "Leeds", ...])

        city_sizer = self.create_city_sizer()

        sizer.Add(city_sizer, pos=(1, 0), flag=wx.LEFT, border=10)

    def create_city_sizer(self):
        city_box = wx.StaticBox(parent=self, label="Destination")
        sizer = wx.StaticBoxSizer(box=city_box, orient=wx.HORIZONTAL)
        self.lst_cities = wx.ListBox(parent=self, size=(300, 150), choices=self.cities)
        sizer.Add(self.lst_cities)
        return sizer
```

### The date sizer

In this application, the date is selected by three
[comboboxes](lesson07.html#the-combobox) placed in a horizontal
*BoxSizer*:

``` python
class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):
        self.days = [str(day) for day in range(1, 32)]
        this_year = datetime.now().year
        self.years = [str(year) for year in range(this_year, this_year+10)]
        self.months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
                       "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]

        date_sizer = self.create_date_sizer()

        sizer.Add(date_sizer, pos=(1, 1), flag=wx.RIGHT, border=10)

    def create_date_sizer(self):
        date_box = wx.StaticBox(parent=self, label="Booking date")
        sizer = wx.StaticBoxSizer(box=date_box, orient=wx.HORIZONTAL)
        self.cmb_day = wx.ComboBox(parent=self, size=(100, -1), choices=self.days)
        self.cmb_month = wx.ComboBox(parent=self, size=(100, -1), choices=self.months)
        self.cmb_year = wx.ComboBox(parent=self, size=(100, -1), choices=self.years)
        sizer.Add(self.cmb_day, flag=wx.ALL, border=10)
        sizer.Add(self.cmb_month, flag=wx.TOP|wx.BOTTOM, border=10)
        sizer.Add(self.cmb_year, flag=wx.ALL, border=10)
        return sizer
```

### The button sizer

The last widgets that we need to place on the panel are the *buttons*.
Following the [spacer technique](lesson07.html#using-spacers) for aligning
the buttons demonstrated earlier:

``` python
class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):
        button_sizer = self.create_button_sizer()
        sizer.Add(button_sizer, pos=(2, 0), span=(1, 2),
                    flag=wx.LEFT|wx.BOTTOM|wx.RIGHT|wx.EXPAND,
                    border=10)

    def create_button_sizer(self):
        cmd_clear = wx.Button(parent=self, id=wx.ID_CLEAR)
        cmd_save = wx.Button(parent=self, id=wx.ID_SAVE)
        cmd_quit = wx.Button(parent=self, id=wx.ID_EXIT)

        cmd_clear.Bind(wx.EVT_BUTTON, self.on_cmd_clear_click)
        cmd_save.Bind(wx.EVT_BUTTON, self.on_cmd_save_click)
        cmd_quit.Bind(wx.EVT_BUTTON, self.on_cmd_quit_click)

        sizer = wx.BoxSizer(orient=wx.HORIZONTAL)
        sizer.Add(cmd_clear)
        sizer.Add(cmd_save)
        sizer.Add((0, 0), proportion=1)
        sizer.Add(cmd_quit, flag=wx.ALIGN_RIGHT)
        return
```

As I want the button sizer to take the whole horizontal width of the
*GridBagSizer*, I have spanned two columns.

### Handling events

I have bound the buttons to methods defined in the **ButtonPanel**'s
parent, i.e. the **MainPanel**. The code for the **Save** button has not
been attempted here because that will depend on the implementation of
the data in the larger system.

``` python
class MainPanel(wx.Panel):
    def on_cmd_clear_click(self, event):
        del event
        self.clear_controls()

    def on_cmd_save_click(self, event):
        del event
        print('Save button pressed')

    def on_cmd_quit_click(self, event):
        del event
        quit()
```

The **clear\_controls** method is defined within the **MainPanel**. It
is called when the **Clear** button is clicked and when the panel is
created to ensure a consistent state.

``` python
class MainPanel(wx.Panel):

    def clear_controls(self):
        self.txt_first_name.SetValue('')
        self.txt_last_name.SetValue('')
        self.txt_email.SetValue('')
        for cb_extra in self.cb_extras_list:
            cb_extra.SetValue(False)
        self.room_box.SetSelection(0)
        self.lst_cities.SetSelection(0)
        self.lst_cities.SetSelection(-1)
        self.cmb_day.SetValue('Day')
        self.cmb_month.SetValue('Month')
        self.cmb_year.SetValue('Year')
```

#### Summary

In this lesson I have used many of the elements covered in earlier lessons
to create a larger and more complex application. I have paid attention
to structuring the code to optimise the three pillars of sound
programming in Python: readability, maintainability and reusability. The
complete code for the application follows
([booking.py](snippets/booking.py)).

In the next lesson I will cover dialogs.

``` python
from datetime import datetime
import wx


class MainFrame(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(MainFrame, self).__init__(*args, **kwargs)
        panel = MainPanel(self)
        self.SetMenuBar(MenuBar())
        self.status_bar = self.CreateStatusBar()
        self.status_bar.SetStatusText('New client')
        sizer = wx.BoxSizer()
        sizer.Add(panel)
        self.SetSizerAndFit(sizer)
        self.Show()


class MenuBar(wx.MenuBar):
    def __init__(self):
        wx.MenuBar.__init__(self)
        file_menu = self.create_file_menu()
        help_menu = self.create_help_menu()
        self.Append(file_menu, '&File')
        self.Append(help_menu, '&Help')

    def create_file_menu(self):
        menu = wx.Menu()
        clear_menu_item = wx.MenuItem(parentMenu=menu, id=wx.ID_CLEAR)
        save_menu_item = wx.MenuItem(parentMenu=menu, id=wx.ID_SAVE)
        quit_menu_item = wx.MenuItem(parentMenu=menu, id=wx.ID_EXIT)
        menu.Append(clear_menu_item)
        menu.Append(save_menu_item)
        menu.Append(quit_menu_item)
        return menu

    def create_help_menu(self):
        help_menu = wx.Menu()
        return help_menu


class MainPanel(wx.Panel):
    def __init__(self, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)
        self.days = [str(day) for day in range(1, 32)]
        this_year = datetime.now().year
        self.years = [str(year) for year in range(this_year, this_year+10)]
        self.months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
                       "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
        self.extras_list = ["Breakfast", "Newpaper", "Flowers"]
        self.room_types = ["Single", "Twin", "Double"]
        cities_raw = ["London", "Birmingham", "Glasgow", "Leeds", "Bristol",
                      "Liverpool", "Manchester", "Sheffield", "Edinburgh",
                      "Cardiff", "Leicester", "Stoke-on-Trent", "Bradford",
                      "Coventry", "Nottingham", "Kingston-upon-Hull",
                      "Belfast", "Newcastle-upon-Tyne", "Sunderland",
                      "Brighton", "Derby", "Plymouth", "Wolverhampton",
                      "Southampton", "Swansea ", "Salford", "Portsmouth",
                      "Milton Keynes", "Aberdeen", "Reading", "Northampton",
                      "Luton", "Swindon", "Warrington", "Dudley", "York"]
        self.cities = sorted(cities_raw)

        person_sizer = self.create_person_sizer()
        extras_sizer = self.create_extras_sizer()
        room_sizer = self.create_room_sizer()
        city_sizer = self.create_city_sizer()
        date_sizer = self.create_date_sizer()
        button_sizer = self.create_button_sizer()

        preferences_sizer = wx.BoxSizer(orient=wx.HORIZONTAL)
        preferences_sizer.Add(extras_sizer, flag=wx.RIGHT, border=10)
        preferences_sizer.Add(room_sizer)
        sizer = wx.GridBagSizer(10, 10)
        sizer.Add(person_sizer, pos=(0, 0), flag=wx.TOP|wx.LEFT, border=10)
        sizer.Add(preferences_sizer, pos=(0, 1), flag=wx.TOP, border=10)
        sizer.Add(city_sizer, pos=(1, 0), flag=wx.LEFT, border=10)
        sizer.Add(date_sizer, pos=(1, 1), flag=wx.RIGHT, border=10)
        sizer.Add(button_sizer, pos=(2, 0), span=(1, 2),
                  flag=wx.LEFT|wx.BOTTOM|wx.RIGHT|wx.EXPAND,
                  border=10)
        self.SetSizer(sizer)
        self.clear_controls()

    def clear_controls(self):
        self.txt_first_name.SetValue('')
        self.txt_last_name.SetValue('')
        self.txt_email.SetValue('')
        for cb_extra in self.cb_extras_list:
            cb_extra.SetValue(False)
        self.room_box.SetSelection(0)
        self.lst_cities.SetSelection(0)
        self.lst_cities.SetSelection(-1)
        self.cmb_day.SetValue('Day')
        self.cmb_month.SetValue('Month')
        self.cmb_year.SetValue('Year')

    def on_cmd_clear_click(self, event):
        del event
        self.clear_controls()

    def on_cmd_save_click(self, event):
        del event
        print('First name: %s' % self.txt_first_name.GetValue())
        print('Last name: %s' % self.txt_first_name.GetValue())
        print('Email: %s' % self.txt_first_name.GetValue())
        for index, cb_extra in enumerate(self.cb_extras_list):
            print(self.extras_list[index]+': %s' % str(cb_extra.GetValue()))
        print('Room type: %s' % self.room_types[self.room_box.GetSelection()])
        print('City: %s' % self.cities[self.lst_cities.GetSelection()])
        date_string = 'Date: {day} {month} {year}'
        print(date_string.format(day=self.cmb_day.GetValue(),
                                 month=self.cmb_month.GetValue(),
####                                  year=self.cmb_year.GetValue()))
        self.clear_controls()

    @staticmethod
    def on_cmd_quit_click(event):
        del event
        quit()

    def create_person_sizer(self):
        lbl_first_name = wx.StaticText(parent=self, label="First name")
        lbl_last_name = wx.StaticText(parent=self, label="Last name")
        lbl_email = wx.StaticText(parent=self, label="Email")
        self.txt_first_name = wx.TextCtrl(parent=self, size=(150, -1))
        self.txt_last_name = wx.TextCtrl(parent=self, size=(150, -1))
        self.txt_email = wx.TextCtrl(parent=self, size=(250, -1))
        sizer = wx.GridBagSizer(5, 5)
        sizer.Add(lbl_first_name, pos=(0, 0))
        sizer.Add(lbl_last_name, pos=(1, 0))
        sizer.Add(lbl_email, pos=(2, 0))
        sizer.Add(self.txt_first_name, pos=(0, 1))
        sizer.Add(self.txt_last_name, pos=(1, 1))
        sizer.Add(self.txt_email, pos=(2, 1))
        return sizer

    def create_extras_sizer(self):
        extras_box = wx.StaticBox(parent=self, label="Extras")
        sizer = wx.StaticBoxSizer(box=extras_box, orient=wx.VERTICAL)
        self.cb_extras_list = []
        for extras in self.extras_list:
            cb_extras = wx.CheckBox(parent=extras_box, label=extras, name=extras)
            sizer.Add(cb_extras, flag=wx.ALL, border=0)
            self.cb_extras_list.append(cb_extras)
        return sizer

    def create_room_sizer(self):
        self.room_box = wx.RadioBox(parent=self, label="Room",
                                    choices=self.room_types,
                                    style=wx.RA_SPECIFY_ROWS)
        sizer = wx.BoxSizer(orient=wx.HORIZONTAL)
        sizer.Add(self.room_box)
        return sizer

    def create_city_sizer(self):
        city_box = wx.StaticBox(parent=self, label="Destination")
        sizer = wx.StaticBoxSizer(box=city_box, orient=wx.HORIZONTAL)
        self.lst_cities = wx.ListBox(parent=self, size=(300, 150), choices=self.cities)
        sizer.Add(self.lst_cities)
        return sizer

    def create_date_sizer(self):
        date_box = wx.StaticBox(parent=self, label="Booking date")
        sizer = wx.StaticBoxSizer(box=date_box, orient=wx.HORIZONTAL)
        self.cmb_day = wx.ComboBox(parent=self, size=(100, -1), choices=self.days)
        self.cmb_month = wx.ComboBox(parent=self, size=(100, -1), choices=self.months)
        self.cmb_year = wx.ComboBox(parent=self, size=(100, -1), choices=self.years)
        sizer.Add(self.cmb_day, flag=wx.ALL, border=10)
        sizer.Add(self.cmb_month, flag=wx.TOP|wx.BOTTOM, border=10)
        sizer.Add(self.cmb_year, flag=wx.ALL, border=10)
        return sizer

    def create_button_sizer(self):
        cmd_clear = wx.Button(parent=self, id=wx.ID_CLEAR)
        cmd_save = wx.Button(parent=self, id=wx.ID_SAVE)
        cmd_quit = wx.Button(parent=self, id=wx.ID_EXIT)

        cmd_clear.Bind(wx.EVT_BUTTON, self.on_cmd_clear_click)
        cmd_save.Bind(wx.EVT_BUTTON, self.on_cmd_save_click)
        cmd_quit.Bind(wx.EVT_BUTTON, self.on_cmd_quit_click)

        sizer = wx.BoxSizer(orient=wx.HORIZONTAL)
        sizer.Add(cmd_clear)
        sizer.Add(cmd_save)
        sizer.Add((0, 0), proportion=1)
        sizer.Add(cmd_quit, flag=wx.ALIGN_RIGHT)
        return sizer


if __name__ == "__main__":
    screen_app = wx.App()
    main_frame = MainFrame(parent=None, title="Hotel booking")
    screen_app.MainLoop()
```

[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson08.md%}) \|  [next]({{ site.baseurl }}{% link wx_python/lesson10.md%})