---
date: '2024-10-24T16:15:16.836698'
description: Useful for adding Mermaid charts of various types to Jupyter notebooks.
published: true
tags: 
    - jupyter
    - python
    - howto
title: Using Mermaid JS in Jupyter notebook
---


## The code

```python
import base64
from IPython.display import Image, display

def mm(graph):
    graphbytes = graph.encode("utf8")
    base64_bytes = base64.urlsafe_b64encode(graphbytes)
    base64_string = base64_bytes.decode("ascii")
    display(Image(url="https://mermaid.ink/img/" + base64_string))
```


## Usage Example

```python
mm("""
graph LR;
    A--> B & C & D;
    B--> A & E;
    C--> A & E;
    D--> A & E;
    E--> B & C & D;
""")
```


```mermaid
graph LR;
    A--> B & C & D;
    B--> A & E;
    C--> A & E;
    D--> A & E;
    E--> B & C & D;
```

## Notes

- This is actually covered in the mermaid docs [here](https://mermaid.js.org/ecosystem/tutorials.html?#jupyter-integration-with-mermaid-js), albeit with an unnecessary import from matplotlib that I removed in this example
- I discovered this trick back in 2023 while working on the [dj-notebook](https://github.com/pydanny/dj-notebook) library
- [Mermaid](https://mermaid.js.org/) is a JavaScript-powered diagramming and charting tool that's friendly for browsers
- Amusingly enough, [this article is written in pure markdown](https://github.com/pydanny/daniel-blog-fasthtml/blob/main/posts/2024/using-mermaidjs-in-jupyter-notebooks.md) because as of October 24th, 2024 I haven't yet gotten the function to work yet with nb2fasthtml.