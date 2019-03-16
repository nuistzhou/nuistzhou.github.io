---
layout:     post
title:      "Black: the magic Python code formatter"
subtitle:   " \"Insights\""
date:       2019-03-15 16:00:00
author:     "Ping"
header-img: "img/in-post/tutorial_pythonpath/post-head-python.jpg"
catalog: true
tags:
    - Technology
    - Python
---

If you have worked with Python, you might be bothered by the [PEP 8](https://www.python.org/dev/peps/pep-0008/)
(Style Guide for Python Code) a lot since it has a list of complicated rules in order to make your code more readable.

A good news is that one of my colleagues introduced a automation tool to smartly format your Python code and it can 
also be integrated into various IDEs and ediotrs like PyCharm,Sublime, Emacs, Vim, Atom, just name a few. 

Following is a very simple example showing how nicely the formatter can make your coding life easier!
 
**Before**
```python
def details(self) -> dict:
    """Fetch and buffer catalog details from platform."""
    if not self._catalog_details:
        self._catalog_details = self.api.get_catalog_details(hrn=self.hrn, lookup_apis=self.apis)
        self._catalog_details['layers_by_id'] = {layer['id']: layer for layer in self._catalog_details['layers']}

```

**After**
```python
def details(self) -> dict:
    """Fetch and buffer catalog details from platform."""
    if not self._catalog_details:
        self._catalog_details = self.api.get_catalog_details(
                hrn=self.hrn, lookup_apis=self.apis
            )
        self._catalog_details["layers_by_id"] = {
                layer["id"]: layer for layer in self._catalog_details["layers"]
            }

```

Much clear, huh?

[Here](https://github.com/ambv/black) you can find the official site of the Black tool including how to install and play with it, have fun!
