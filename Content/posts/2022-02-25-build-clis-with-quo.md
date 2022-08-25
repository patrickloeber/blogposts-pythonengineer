---
title: How to build CLIs using Quo
date: 2022-03-11 00:00
description: Learn how you can build CLIs with Quo, a toolkit for writing Command-Line Interface applications.
tags: Python
path: cli-with-quo
author: Gerrishon Sirere
---

[![Logo](https://raw.githubusercontent.com/secretum-inc/quo/master/pics/quo.png)](https://github.com/secretum-inc/quo)

**Quo** is a Python based toolkit for writing Command-Line Interface(CLI) applications. Quo is making headway towards composing speedy and orderly CLI applications while forestalling any disappointments brought about by the failure to execute a CLI API.

Quo is easy to learn, and does not come with needless baggage and contains a number of builtin features you can use to create elegant output in your CLI.

## Compatibility

Quo works flawlessly  with Linux, OSX, and Windows.
Quo requires Python `3.8` or later. 

## Features

- [x] Support for Ansi, RGB and Hex color models
- [x] Support for tabular presentation of data
- [x] Intuitive progressbars
- [x] Code completions
- [x] Nesting of commands
- [x] Customizable Text User Interface _(TUI)_ dialogs.
- [x] Automatic help page generation
- [x] Syntax highlighting
- [x] Autosuggestions
- [x] Key Binders

## Getting Started
## Quo Library
Quo contains a number of builtin features you c
an use to create elegant output in your CLI.

### Installation

You can install quo via the Python Package Index (PyPI)

```console
pip install -U quo
```

Run the following to test Quo output on your terminal:

```console
python -m quo
```
![test](https://github.com/scalabli/quo/raw/master/docs/images/test.png)

## Printing

### Quo echo

To output formatted text to your terminal you can import the [echo](https://quo.readthedocs.io/en/latest/introduction.html#quick-start) method.
Try this:

**Example 1**

```python
 from quo import echo

 echo(f"Hello, World!", fg="red", italic=True, bold=True))
```

![Hello World](https://github.com/secretum-inc/quo/raw/master/pics/print.png)

**Example 2**

```python
 from quo import echo

 echo("Quo is ", nl=False)
 echo("scalable", bg="red", fg="black") 
```

![Scalable](https://github.com/secretum-inc/quo/raw/master/pics/scalable.png)

### Quo print

Alternatively, you can import [print](https://quo.readthedocs.io/en/latest/printing_text.html#print)

```python
from quo import print

print('<b>This is bold</b>')
print('<i>This is italic</i>')
print('<u>This is underlined</u>')                      
# Colors from the ANSI palette.
print('<red>This is red</red>')
print('<style fg="green" bg="red">Green on red background</stlye>')
```

## Quo Prompts

- Using ``quo.prompt`` method.

```python
from quo import prompt

prompt("What is your name?")
```

![quo.prompt](https://github.com/secretum-inc/quo/raw/master/pics/prompt.png)

- Using ``quo.prompt.Prompt`` object

**Example 1**

```python
from quo.prompt import Prompt
   
session = Prompt()
session.prompt("Type something:") 
```

**Example 2**

A prompt with a bottom toolbar

```python

  from quo.prompt import Prompt
  from quo.text import Text

  def toolbar():
        return Text('This is a <b><style bg="red">Toolbar</style></b>!')

  # Returns a callable
  session = Prompt(bottom_toolbar=toolbar)
  session.prompt('> ')

```

![validate](https://raw.githubusercontent.com/scalabli/quo/master/docs/images/bottom-toolbar.png)

Read more on [Prompt](https://quo.readthedocs.io/en/latest/prompt.html).

## Completions

### Autocompletion

Press [Tab] to autocomplete

```python
from quo.prompt import Prompt
from quo.completion import WordCompleter
example = WordCompleter(['USA', 'UK', 'Canada', 'Kenya'])
session = Prompt(completer=example)
session.prompt('Which country are you from?: ')
```

![Autocompletion](https://github.com/secretum-inc/quo/raw/master/docs/images/autocompletion.png)

### Autosuggestion
Auto suggestion is a way to propose some input completions to the user. Usually, the input is compared to the history and when there is another entry starting with the given text, the completion will be shown as gray text behind the current input. Pressing the right arrow → or ctrl-e will insert this suggestion, alt-f willinsert the first word of the suggestion.

```python
from quo.history import MemoryHistory
from quo.prompt import Prompt

MemoryHistory.append("import os")
MemoryHistory.append('print("hello")') 
MemoryHistory.append('print("world")')  
MemoryHistory.append("import path")

session = Prompt(history=MemoryHistory, suggest="history")

while True:
   session.prompt('> ')
```

Read more on [Completions](https://quo.readthedocs.io/en/latest/prompt.html#completion).

## Documenting Scripts

Quo automatically generates help pages for your command-line tools.

```python
from quo import print
from quo.console import command
from quo.console import app

@command()
@app('--count', default=1, help='number of greetings')
@app('--name', prompt="What is your name?", help="The person to greet")

def hello(count: int, name: str):
    """This script prints hello NAME COUNT times."""
       for x in range(count):
           print(f"Hello {name}!")

if __name__ == "__main__":
          hello()
```

And what it looks like after executing:

```console
python example.py --help
```

![Help Text](https://raw.githubusercontent.com/secretum-inc/quo/master/docs/images/help-text.png)

## Quo Dialogs

This is a high level API for displaying dialog boxes to the user for informational purposes, or get input from the user.

**Example 1**

A MessageBox dialog.

```python
from quo.dialog import MessageBox

MessageBox(
        title="Message pop up window",
        text="Do you want to continue?\nPress ENTER to quit.")                                    
```

![Message Box](https://github.com/secretum-inc/quo/raw/master/docs/images/messagebox.png)

**Example 2**

A InputBox dialog

```python
from quo.dialog import InputBox

InputBox(
          title="InputBox shenanigans",
          text="What Country are you from?:")
```

![Prompt Box](https://github.com/secretum-inc/quo/raw/master/docs/images/promptbox.png)

Read more on [Dialogs](https://quo.readthedocs.io/en/latest/dialogs.html).


## Quo Key Binding🔐

A key binding is an association between a physical key on akeyboard and a parameter.

```python

 from quo import echo
 from quo.keys import bind
 from quo.prompt import Prompt

 session = Prompt()

 # Print "Hello world" when ctrl-h is pressed
 @bind.add("ctrl-h")
 def _(event):
      echo("Hello, World!")

 session.prompt("")

```

Read more on [Key bindings](https://quo.readthedocs.io/en/latest/kb.html)

## Quo Progress📈
Creating a new progress bar can be done by calling the class **ProgressBar**
The progress can be displayed for any iterable. This works by wrapping the iterable (like ``range``) with the class **ProgressBar**

```python
import time
from quo.progress import ProgressBar
  
with ProgressBar() as pb:
              for i in pb(range(800)):
                            time.sleep(.01)
```

![Progress](https://raw.githubusercontent.com/secretum-inc/quo/master/docs/images/simple-progress-bar.png)

Read more on [Progress](https://quo.readthedocs.io/en/latest/progress.html).



## Quo Tables

This offers a number of configuration options to set the look and feel of the table, including how borders are rendered and the style and alignment of the columns.

**Example 1**

```python

 from quo.table import Table

 data = [
     ["Name", "Gender", "Age"],
     ["Alice", "F", 24],
     ["Bob", "M", 19],
     ["Dave", "M", 24]
  ]

 Table(data)

```
![tabulate](https://raw.githubusercontent.com/scalabli/quo/master/docs/images/tables/table.png)

**Example 2**

Right aligned table

```python

 from quo.table import Table

 data = [
    ["Name", "Gender", "Age"],
    ["Alice", "F", 24],
    ["Bob", "M", 19],
    ["Dave", "M", 24]
    ]
 Table(data, align="right")

```

![tabulate](https://raw.githubusercontent.com/scalabli/quo/master/docs/images/tables/right-table.png)

**Example 3**

Colored table

```python

 from quo.table import Table

 data = [
    ["Name", "Gender", "Age"],
    ["Alice", "F", 24],
    ["Bob", "M", 19],
    ["Dave", "M", 24]
    ] 
    
 Table(data, style="fg:green")

```


![tabulate](https://raw.githubusercontent.com/scalabli/quo/master/docs/images/tables/colored-table.png)

**Example 4**

Grid table

```python

 from quo.table import Table

 data = [
    ["Name", "Gender", "Age"],
    ["Alice", "F", 24],
    ["Bob", "M", 19],
    ["Dave", "M", 24]
    ]

 Table(data, theme="grid")

```


![tabulate](https://raw.githubusercontent.com/scalabli/quo/master/docs/images/tables/grid-table.png)




Read more on [Table](https://quo.readthedocs.io/en/latest/table.html)


## Quo Widgets
A collection of reusable components for building full screen applications.

``Frame`` 🎞️

Draw a border around any container, optionally with a title.

```python

 from quo import container
 from quo.widget import Frame, Label

 content = Frame(
             Label("Hello, World!"),
               title="Quo: python")

 #Press Ctrl-C to exit
 container(content, bind=True, full_screen=True)

```
![Frame](https://raw.githubusercontent.com/scalabli/quo/master/docs/images/widgets/frame.png)

``Label``

Widget that displays the given text. It is not editable or focusable.

**Example 1**

This will occupy a minimum space in your terminal

```python

 from quo import container
 from quo.widget import Label

 content = Label("Hello, World", style="fg:black bg:red")

 container(content)

```
**Example 2**

This will be a fullscreen application

```python

 from quo import container
 from quo.widget import Label

 content = Label("Hello, World", style="fg:black bg:red")

 # Press Ctrl-C to exit
 container(content, bind=True, full_screen=True)

```

**Example 3**

Full screen application using a custom binding key.

```python

 from quo import container
 from quo.keys import bind
 from quo.widget import Label

 content = Label("Hello, World", style="fg:black bg:red")

 #Press Ctrl-Z to exit
 @bind.add("ctrl-z")
 def _(event):
     event.app.exit()

 container(content, bind=True, full_screen=True)

```

Read more on [Widgets](https://quo.readthedocs.io/en/latest/widgets.html)


Quo is _simple_. If you know Python you can  easily use quo and it can integrate with just about anything.
