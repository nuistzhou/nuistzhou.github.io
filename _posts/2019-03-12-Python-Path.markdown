---
layout:     post
title:      "PYTHONPATH: solve custom module importing problem"
subtitle:   " \"Insights\""
date:       2019-03-12 17:00:00
author:     "Ping"
header-img: "img/in-post/tutorial_pythonpath/post-head-python.jpg"
catalog: true
tags:
    - Technology
    - Python
---

## Working with PYTHONPATH environmental variables

I have been suffering from a situation where I was not able to import my python module from a custom path.

Let's take my Python project "nagini" as an example:

When the project path is not added:

![console-no-nagini](img/in-post/tutorial_pythonpath/post_console_no_nagini.JPG)

The problem is that, when the Python interpreter was importing a module, it searches for all
possible locations defined in the `sys.path` variable, if not found, an error is raised.

Thus, we just need to create an ENVIRONMENTAL VARIABLE named **"nagini"** and its **nagini's** absolute project path:

![environmental-variable](img/in-post/tutorial_pythonpath/post_added_pythonpath.jpg)

Now let's open a **NEW** CMD window and try same thing again:

![console-nagini](img/in-post/tutorial_pythonpath/post_console_has_nagini.JPG)

Succeed! Right?!
