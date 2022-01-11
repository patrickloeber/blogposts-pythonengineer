# Articles for python-engineer.com

Repo with articles for the python-engineer.com website.

New authors are welcome! Please read the contribution guide and instructions below in oreder to get started.

## Author contributions

All contributors are credited in the authors page
([https://www.python-engineer.com/authors/](https://www.python-engineer.com/authors/)) and get a dedicated page, e.g. [https://www.python-engineer.com/authors/patrick/](https://www.python-engineer.com/authors/patrick/).

## Contribution Guide

You can find possible topics on the [Issues](https://github.com/python-engineer/blogposts-pythonengineer/issues) page. You can take an existing one or suggest your own topic by opening a new issue.

Once the article is written, open a new Pull Request for it.

## First time?

You can add an image, a description, and up to 4 social links that are listed on the website.

Please also submit a markdown file and a corresponding image (400x400 is preferred). See [authors/patrickloeber.md](authors/patrickloeber.md) and [authors/patrickloeber.png](authors/patrickloeber.png) for my example. Have a look at the raw markdown file to see the frontmatter fields with the author information.

## Instructions

Articles are written in [Markdown format](https://docs.github.com/en/github/writing-on-github/).
An example markdown file is [2021-07-21-python-for-loops.md](Content/blog/2021-07-21-python-for-loops.md).

## File name and folder
Use a name in the following format:

```
YYYY-MM-DD-some-topic-name.md
```

If not specified otherwise, articles should be created in the folder [Content/blog](Content/blog).

## Markdown Front Matter
Markdown frontmatter must have these fields.
```
---
title: How to write for loops in Python
date: 2021-07-21 00:00
description: A for loop is used for iterating over a sequence. This artice shows how to use for loops.
tags: Python, Basics
path: topic-name
author: Patrick Loeber
---
```

(Don't worry about tags and path too much, I can easily adapt this during the pull request review.)

## Code snippets
Code snippets have to be written like this (inspect the raw file to see the markdown syntax):

```python
print("Hello World")
```

## Credit sources

#### Credits
If your article or code is heavily inspired by someone else, you should credit them.

This includes text AND code taken from other blogs or official documentation, GitHub, Stack Overflow, and all similar resources. If you're copying and pasting something from a source like that, make sure you credit it and link to it.

#### Quotes
If you are paraphrasing or quoting directly something someone else said (in another article, video, or any other medium), you should credit them by adding a link to the original source and use quote formatting (use a '>'):

> "Hi, I'm Patrick. I’m a passionate Software Engineer who loves Machine Learning, Computer Vision, and Data Science."
> (Source: [Patrick Loeber](https://www.python-engineer.com/about/))


#### Tip
It's always better to use your own words and own code examples when you can. So rather than copy/pasting and quoting other sources, try to digest the information and explain it in your own words.

This way you won't risk plagiarizing someone else's work.

## Thank you
Thank you for sharing your knowledge with the Python community!