---
layout: "page"
title: ""
---
## Wx Python from scratch

[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson10.md %})

### The Date Picker control and the ObjectListView

In the last lesson I described the use of two of the wxPython dialogs. In
this lesson will deal with two important controls: the Date Picker
control, used for selecting a date, and the ObjectListView used for
displaying data in a list format.

#### The Date Picker control

The **wx.adv** module has a *DatePicker* class.

![]({{ site.baseurl }}/wx_python/images/datepicker.png)

Fig 1. A datepicker

The code to generate this is straightforward:

``` python
import wx
import wx.adv
from datetime import datetime
import locale

locale.setlocale(locale.LC_ALL,'en_GB.UTF-8')

class MainPanel(wx.Panel):
def __init__(self, parent, *args, **kwargs):
        super(MainPanel, self).__init__(parent, *args, **kwargs)

        now = datetime.today()
        day_one = wx.DateTime(year=now.year, month=0, day=1)
        dte_required = wx.adv.DatePickerCtrl(parent=self, dt=day_one)
        self.dte_required.Bind(wx.adv.EVT_DATE_CHANGED, self.on_dte_required_change)

        sizer = wx.BoxSizer(orient=wx.VERTICAL)
        sizer.Add(dte_required, flag=wx.ALL, border=10)
        self.SetSizer(sizer)

def on_dte_required_change(self, event):
    date = self.dte_required.GetValue()
    pydate = self.wxdate2pydate(date)
    print(pydate.strftime("%d %b %Y"))

@staticmethod
def wxdate2pydate(date):
    assert isinstance(date, wx.DateTime)
    if date.IsValid():
        ymd = list(map(int, date.FormatISODate().split('-')))
        year = int(ymd[0])
        month = int(ymd[1])
        day = int(ymd[2])
        return datetime(year, month, day)
    else:
        return None
```

The points to note are:

1.  The datepicker requires its own **wx.DateTime** object (line 13) to
    set the date;
2.  the wx.DateTime month starts at zero for January;
3.  I have used code from
    [here](https://www.blog.pythonlibrary.org/2014/08/27/wxpython-converting-wx-datetime-python-datetime/)
    to help with the date conversion in the **wxdate2pydate** function.


[home]({{ site.baseurl }}{% link index.md%}) \|  [previous]({{ site.baseurl }}{% link wx_python/lesson10.md%})