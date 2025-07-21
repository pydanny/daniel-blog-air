---
date: '2024-11-01T12:00:00.235742'
description: How did I miss these functions getting added to Python?
image: /public/logos/til-1.png
published: true
tags:
- TIL
- python
title: 'TIL: Using Python to removing prefixes and suffixes'
twitter_image: /public/logos/til-1.png
---

Starting in Python 3.9, `s.removeprefix()` and `s.removesuffix()` were added as `str` built-ins. Which easily covers all the versions of Python I currently support.

## Usage for `removeprefix()`:

```python
>>> 'Spam, Spam'.removeprefix('Spam')
', Spam'
>>> 'Spam, Spam'.removeprefix('This is not in the prefix')
'Spam, Spam'
```

## Usage for `removesuffix()`:

```python
>>> 'Spam, Spam'.removesuffix('Spam')
'Spam, '
>>> 'Spam, Spam'.removesuffix('This is not in the suffix')
'Spam, Spam'
```