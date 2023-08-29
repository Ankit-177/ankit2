---
toc: True
comments: False
layout: post
title: Python Emoji Print
description: This is the installation and implementation of emojis using Python.
type: hacks
courses: {'compsci': {'week': 2}}
---

```python
pip install emoji
```

    Defaulting to user installation because normal site-packages is not writeable
    Collecting emoji
      Downloading emoji-2.8.0-py2.py3-none-any.whl (358 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m358.9/358.9 KB[0m [31m7.6 MB/s[0m eta [36m0:00:00[0ma [36m0:00:01[0m
    [?25hInstalling collected packages: emoji
    Successfully installed emoji-2.8.0
    Note: you may need to restart the kernel to use updated packages.



```python
from emoji import emojize 
print(emojize(":thumbs_up: Python is awesome! :grinning_face:"))
```

    👍 Python is awesome! 😀

