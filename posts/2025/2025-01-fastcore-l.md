---
date: "2025-01-19T14:30:00.00Z"
description: "An exploration of Fastcore's enhanced list-like structure"
published: true
tags:
  - python
  - fastcore
  - howto
time_to_read: 2
title: "Fastcore L"
type: post
---

In September of 2023 after a 5 year hiatus from creating new Python packages I decided to re-explore how to package Python code for distribution. This was before [uv](https://docs.astral.sh/uv/) existed so it was worth knowing all the nitty-gritty details. My sample project was [listo](https://github.com/pydanny/listo), an enhanced list for Python with these planned features:

- More consistent behavior . No more methods with "in-place" changes. Every method call returns a value
- Added methods that are missing from the list type, like `.map()` and `.filter()`, which I never got around to implementing

It was a fun little exploratory package. Alas, at the time my open source efforts went more towards [dj-notebook](https://github.com/pydanny/dj-notebook). Nevertheless I sometimes thought about revisiting and finishing the project.

Then I discovered `fastcore.foundation.L`. This handy sequence tool is similar in concept to my own `listo` but much more complete. Let's go over some of its features and compare it to the standard Python `list` structure.

## Basic usage

```python {.marimo}
from fastcore.foundation import L
```

Let's create a L sequence and example it:

```python {.marimo}
lst1 = L(range(100))
lst1
```

The print representation of an L sequence has two interesting features. For starters, it provides a count of items, in this case 100 of them. It also truncates the output so if you have a large sequence you aren't given an oversized block of values.

Like `listo()`, every method provided by `L` returns an `L` object. This allows for chaining of operations. Let's see what that works with a list of duplicated values.

```python {.marimo}
lst2 = L(list(range(5))+list(range(5)))
lst2
```

We'll remove duplicates while preserving order and keeping only even values.

```python {.marimo}
lst2.unique().filter(lambda x: not x % 2 and x)
```

This line of code is using two L methods:
- `.unique()` for removing duplicate elements but maintaining the order of the sequence
- `.filter()` for running a function that based on a boolean response keeps or removes values. In this case we use a lambda that returns a boolean to tell it to only keep even values

While I could do this with a regular Python list it's bit more verbose.

```python {.marimo}
seen = set()
[x for x in lst2 if not (x in seen or seen.add(x)) if not x % 2 and x]
```

While I love regular expressions and use them constantly, I have to say that L is more legible. Take a look at both and you'll see what I mean:

- `lst2.unique().filter(lambda x: not x % 2 and x)`
- `seen = set(); [x for x in lst2 if not (x in seen or seen.add(x)) if not x % 2 and x]`

## Why not use L for every sequence?

There's no one-size fits all structure for sequences. Here's two reasons why it's good to keep up your list comprehension skills.

1. `Fastcore` is another Python dependency, sometimes you can't control the libraries you are using. This is why list comprehension is such an important skill for any Python dev.
2. `L` is not a generator expression, meaning large sizes in terms of number of elements or the size of individual elements can be problematic. The ability to convert a list comprehension like `[x for x in range(100)]` to a generator expression like `(x for x in range(100))` simply by converting square brackets to parenthesis is one of Python's greatest superpowers

```python {.marimo hide_code="true"}
mo.md(
    r"""

    """
)
```

```python {.marimo}
import marimo as mo
```