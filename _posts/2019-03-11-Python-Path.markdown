---
layout:     post
title:      "PYTHONPATH: solve custom module importing problem"
subtitle:   " \"Insights\""
date:       2019-03-11 17:00:00
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

![console-no-nagini](/img/in-post/tutorial_pythonpath/post_console_no_nagini.jpg)

The problem is that, when the Python interpreter was importing a module, it searches for all
possible locations defined in the `sys.path` variable, if not found, an error is raised.

Thus, we just need to create an ENVIRONMENTAL VARIABLE named **"nagini"** and its **nagini's** absolute project path, 
take Windows as an example:

![environmental-variable](/img/in-post/tutorial_pythonpath/post_added_pythonpath.jpg)

Now let's open a **NEW** CMD window and try same thing again:

![console-nagini](/img/in-post/tutorial_pythonpath/post_console_has_nagini.jpg)

Succeed! Right?!

**For Linux/Unix users**

*******************

If you want to permanently set your module into the environmental variables, 

- Ubuntu, do:

    `nano ~/.bashrc`

- Mac OS, do:
 
    `nano ~/.bash_profile`

Then add the following line into the file, remember to change the *MODULE PATH* to yours, the brackets need to be 
removed.

`EXPORT PYTHONPATH="{ABSOLUTE PATH TO THE DIR CONTAINS YOUR MODULE}:$PYTHONPATH`

Then save and quit.

To make the change take effect immediately, run this command in the terminal:

`source .bash-profile` OR  `source .bashrc`

**Note:**

If you just want to set the environmentable variable temporarily to not mass up your `bash profile`, let say working 
on this module just this time, then just run the following command in your terminal:

`EXPORT PYTHONPATH="{ABSOLUTE PATH TO THE DIR CONTAINS YOUR MODULE}:$PYTHONPATH`
