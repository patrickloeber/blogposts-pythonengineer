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

### Installation

You can install quo via the Python Package Index (PyPI)

```console
pip install -U quo
```

Run the following to test Quo output on your terminal:

```console
python -m quo
```

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

 echo(f"Quo is ", nl=False)
 echo(f"scalable", bg="red", fg="black") 
```

![Scalable](https://github.com/secretum-inc/quo/raw/master/pics/scalable.png)

### Quo print

Alternatively, you can import [print](https://quo.readthedocs.io/en/latest/printing_text.html#print)

```python
from quo import print
from quo.text import Text

print(Text('<b>This is bold</b>'))
print(Text('<i>This is italic</i>'))
print(Text('<u>This is underlined</u>'))                        
# Colors from the ANSI palette.
print(Text('<red>This is red</red>'))
print(Text('<style fg="green" bg="red">Green on red background</stlye>'))
```

## Prompts

### Quo prompt

- Using ``quo.prompt`` method.

```python
from quo import prompt

prompt("What is your name?")
```

![quo.prompt](https://github.com/secretum-inc/quo/raw/master/pics/prompt.png)

- Using ``quo.prompt.Prompt`` object

```python
from quo.prompt import Prompt
   
session = Prompt()
session.prompt("Type something:") 
```

Read more on [Prompt](https://quo.readthedocs.io/en/latest/prompt.html).

## ``Launching Applications``

Quo supports launching applications through `Console.launch`. This can be used to open the default application associated with a URL or filetype.

```python
from quo.console import Console
   
console = Console()
console.launch("https://quo.rtfd.io/")
```

Read more on [Console](https://quo.readthedocs.io/en/latest/console.html).

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
from quo.prompt import Prompt
from quo.completion import AutoSuggestFromHistory
from quo.history import InMemoryHistory

history = InMemoryHistory(
history.append("import os")
history.append('print("hello")') 
history.append('print("world")')  
history.append("import path"

session = Prompt(auto_suggest=AutoSuggestFromHistory(), history=history)

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

if __name__ == "__main__:
          hello()
```

And what it looks like after executing:

```console
python example.py --help
```

![Help Text](https://raw.githubusercontent.com/secretum-inc/quo/master/docs/images/help-text.png)

## Progress
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

## Key Binding

A key binding is an association between a physical key on a keyboard and a parameter.

```python
from quo import echo
from quo.keys import bind
from quo.prompt import Prompt
 
session = Prompt() 
# Print "Hello world" when ctrl-h is pressed
@bind.add("ctrl-h")
def _(event):
    echo("Hello, World!")
session.prompt(">>")
```

Read more on [Key bindings](https://quo.readthedocs.io/en/latest/kb.html).

## Dialogs

This is a high level API for displaying dialog boxes to the user for informational purposes, or get input from the user.

1) Example of a message box dialog.

```python
from quo.dialog import MessageBox

MessageBox(
        title="Message pop up window",
        text="Do you want to continue?\nPress ENTER to quit.")                                    
```

The above code produces the following output
![Message Box](https://github.com/secretum-inc/quo/raw/master/docs/images/messagebox.png)

2) Example of a prompt box dialog

```python
from quo.dialog import InputBox

InputBox(
          title="InputBox shenanigans",
          text="What Country are you from?:")
```

![Prompt Box](https://github.com/secretum-inc/quo/raw/master/docs/images/promptbox.png)

Read more on [Dialogs](https://quo.readthedocs.io/en/latest/dialogs.html).

## Tables

Function [Table](https://quo.readthedocs.io/en/latest/table.html) offers a number of configuration options to set the look and feel of the table, including how borders are rendered and the style and alignment of the columns.

Example

```python
from quo import echo
from quo.table import Table

data = [
  ["Name", "Gender", "Age"],
  ["Alice", "F", 24],
  ["Bob", "M", 19],
  ["Dave", "M", 24]
]
echo(Table(data))
```

![tabulate](https://raw.githubusercontent.com/secretum-inc/quo/master/docs/images/table.png)

## Widgets

A collection of reusable components for building full screen applications.

### Label

Widget that displays the given text. It is not editable or focusable.

```python
from quo import container
from quo.keys import bind
from quo.widget import Label

content = Label("Hello, World", style="fg:black bg:red")
  
# Ctrl-c to exit
@bind.add("ctrl-c")
def _(event):
   event.app.exit()

container(content, bind=True, full_screen=True)

```

Read more on [Widgets](https://quo.readthedocs.io/en/latest/widgets.html).

Quo is _simple_. If you know Python you can  easily use quo and it can integrate with just about anything.
