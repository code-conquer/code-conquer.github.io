---
title: 我的第一篇博文
commentable: true
Edit: 2019-12-30
mathjax: true
mermaid: true
tags: 学习生活
categories: 生活区
description: This is a sample post testing and demonstrating all the markdown syntaxes. In the description you can also use markdowns to do *A* **B** ***C*** and `D` and other stuff like a [link](https://code-conquer.github.io).
---

# 写这篇文章是为了学习MD

Don't use  ` [ ] ` in YAML front matter.

Use `\newline` instead of `\\` in inline math.

`\substack` is a very useful command.

`<img src= " " width=80%>` will be rendered by typora but Jekyll only renders `<img ="  " width="80%">`

```markdown
some normal text

$$
E = mc^2
$$

Some more text
```

不要使用`{{` 在任何地数学公式里面。使用`{  {  `代替

Jeklly will parse that as liquid tags

不要使用`x_1` 在数学公式里面，使用`x _ 1`代替



# Highlights

*this is italic.*   **This is Bold  **  *if asterisk is surrounded by spaces,it is not parsed.*

_This is also italic_  __This is also Bold__ . _if underscore is surrounded by space,it is not parsed._

~~This is strike through~~

there is no underline in markdown .You can use html tags <u>Hello</u>

`This is a code block`.

You can mix them like [*this*](https://baidu.com),[`this`](https://baidu/com)  **[this](https:baidu.com)**.

# Blocks

> This is a quote block

> > This is a quete block in side another



```python
import numpy as np
ptint(""" This is a python code fence""")
```

```fortran
"This is a fortran code fence"
implicit none
```



```
This is a simple code fence.You can use is to display text. The fonts are mono spaced.
```



You can mix them as well,like

> ```
> This
> ```

# Other Elements

This is horizontal line

------

# Math Blocks

This is inline math $\sum_{i=1}^{N} i$. This is display math.
$$
\sum_{i=1}^{N} i
$$


The extra empty inline matters,or you will end up with
$$
\sum_{i=1}^{N} i
$$


[Mathjax](http://docs.mathjax.org/en/latest/tex.html) systax is likely latex. You cannot use `\usepackge`.but you can use `\newcommand` like this:
$$
\newcommand{\NewOp}[2]{\lbrace{#1}\mid \otimes{#2}\rbrace}
$$
And `\NewOp`will be available in all later math blocks,whether inline $\NewOp{x}{y}$ or display
$$
\NewOp{x}{y}
$$

# Images 

MarkDown uses `![caption](link)`  to reference picures,caption is optional.You cannot control the size.

![caption](https://raw.githubusercontent.com/yk-liu/yk-liu.github.io/master/_posts/2018-11-01-Introduction-to-Homology/assets/triangles.png)

So I preper using HTML tags like this:

<img src="https://raw.githubusercontent.com/yk-liu/yk-liu.github.io/master/_posts/2018-11-01-Introduction-to-Homology/assets/triangles.png" width="60%">

# Lists

- This is unordered list 
  - sub item
    - subsub item
      - subsubsub item
        - subsubsubsub ...



------

- List can have multiple lines

like this:

------

1. This ordered list
   1. sub item
2. This is as well
3. it can keep going

------



# Tables

|  1   |  2   |  3   |
| :--: | :--: | :--: |
|  4   |  5   |  6   |
|  7   |  8   |  9   |



# Foot Notes

This is a note[^1]. Footnotes can have captions like[^this]. You can reference to the same note multiple times like[^this]. Foot notes can have many other options like[^this-one]. Or just like [^that]. This is a [reference style link][https://www.baidu.com] to a page. And [this][https://www.baidu/com] is also a link.As is [this][] and [that].

