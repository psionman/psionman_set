---
layout: 'page'
---
## WxPython from Scratch

### Introduction

This series of pages is intended to guide a competent Python programmer
through the stages needed to buld GUI programs using the wxPython
framework.

### Why I am writing this

I taught myself to write GUI applications in
[wxPython](https://www.wxpython.org/); a sometimes painful and
protracted experience. Here, I want to share with others what little
wisdom I have amassed in this process. I wish I'd have had this guide by
my side when I started; it would have saved many hours of trial and
error.

### Why choose wx python?

I assume that you are already committed to using
[Python](https://www.python.org/) to develop applications and that you
now need or want to develop GUI applications. There is a "native" python
GUI framework, [tkinter](https://docs.python.org/3/library/tk.html), but
on my initial investigation I felt that wxPython looked better. I freely
admit that I might have been wrong about that. That said, wxPython does
have all of the necessary widgets that I want and, in my opinion, looks
great on linux, Windows and OSX.

### Style

I have chosen to assume that the reader knows nothing about wxPython. A
few web searches will find lots of examples of wxPython code snippets,
but these have often been put together to demonstrate a point and they
assume familiarity with the basics of wxPython. I am not claiming that
my style is optimal, but it does have the advantage of providing
solutions that are consistent, effective and compatable with the main PC
platforms: linux, Windows and OSX.

This series of postings is not intended to cover all aspects of wxPython
programming and should not be considered as a reference document.
Instead, I hope you will read, follow and implement for yourself the
examples I give in detail and in sequence. Each posting should take no
more than 30 minutes to work through, and so, if you pace youself over a
week, you will gain an mastery of wxPython in very little time. You will
really understand how to use it and not just parrot recipes from
examples.

I have followed the [Style Guide for wxPython
code](https://wiki.wxpython.org/wxPython%20Style%20Guide) and
[PEP8](https://www.python.org/dev/peps/pep-0008/) (except on line length
and docstrings) wherever possible; I apologise for any lapses.

The code for each topic can be downloaded. A link is provided at the
appropriate point on each lesson.

Wherever I use the term *wx* on its own, it is intended to be read as *wxPython*.

### Prerequisites

I am assuming that you have [downloaded
wxPython](https://wxpython.org/pages/downloads/index.html) and that you
have a working knowledge of Python; in particular object based
programming techniques including [class
definition](https://docs.python.org/3/tutorial/classes.html),
[inheritance](https://docs.python.org/3/tutorial/classes.html#inheritance)
and Python's treatment of a function or method call as an object.

Throughout, I have assumed that you will be using Python 3.

[home]({{ site.baseurl }}{% link index.md%}) [next]({{ site.baseurl }}{% link wx_python/lesson01.md %})