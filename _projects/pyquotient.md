---
name: PyQuotient
desc: Python bindings for libQuotient
# add a short one line description of your project
requirements:
 - Necessary: C++11 and Qt
 - Helpful: C++17
 - Big plus: PySide/PyQt knowledge
difficulty: average
issues:
 - TBD
mentors:
 - kitsune
initiatives:
 - GSoC
tags:
 - Python
 - Qt
---

#### Description

This is a relatively straightforward (especially if you have the right background -
see the requirements) project to add Python bindings to libQuotient, a Qt-based
library to make client applications for Matrix. You'll use Shiboken Generator to
produce the wrappers in Python for libQuotient's classes and implement a basic
client application in Python using these wrappers.

#### Milestones

##### GSOC CODING STARTS

* Produce the first draft of bindings and iterate on it.

##### GSOC MIDTERM

* Make a minimal workable client application using PyQuotient modules.

##### GSOC FINAL

* Advanced use of PyQuotient by adding functionality to the application.
