---
titlt: How to format string in Python
date: 2022-03-20 00:00
description: Learn the different ways to format a string in Python
tags: Python Basic
path: 
author: Shweta Goyal
---

# Formatting Strings in Python

Formatting a string is a very important tool to know when you are coding in Python. Whenever you write a program, you have to format the output into a string before you print it or display it in some form.

There are times when you want to control the formatting of your output rather than simply printing it. There are four different ways to perform string formatting:

## Formatting String with the % Operator

This method is the oldest method of string formatting which uses the modulo(%) operator. Let’s see an example:

```python

name = 'world'
print('Hello, %s!' % name)
 
year = 2022
print('Hello %s, this year is %d.' % (name, year))

# Output:
Hello, world!
Hello world, this year is 2022.
```

This operator formats a set of variables enclosed in a tuple together with a format string. The string contains a normal text together with the `argument specifiers`, special symbols are used like %s, and %d. These special symbols act as a placeholder.

In the second example, there are two arguments specifiers - the first one represents a string and the second represents an integer, and the actual string value is enclosed in a tuple (parentheses).

## Formatting String with the format() method

This method inserts the specified values inside the string's placeholder. The placeholder is defined by a pair of curly braces  { }. The placeholder can be used as the named indexes {name}, numbered indexes {0}, or empty placeholders { }.

Let’s understand through an example:

```python

# Default / empty arguments
print('Hello {}, this year is {}.'.format('world', 2022))
 
# Positional arguments
print('Hello {0}, this year is {1}.'.format('world', 2022))
 
# Keyword arguments
print('Hello {name}, this year is {yr}.'.format(name='world', yr=2022))
 
# Mixed arguments
print('Hello {0}, this year is {yr}.'.format('world', yr=2022))


# Output:

Hello world, this year is 2022.
Hello world, this year is 2022.
Hello world, this year is 2022.
Hello world, this year is 2022.
```

The first example is the basic example with the `default arguments`. In this case, empty placeholders are used.

The second example is of the `positional arguments`. In this case, a number in the bracket refers to the position of the object passed into the .format() method. In other words, values of these arguments can be accessed using an index number inside the { }.

The third example is of the `keyword arguments`. In this case, the argument consists of a key-value pair. Values of these arguments can be accessed by using the key inside the { }.

The fourth example is of the `mixed arguments`. In this case, positional and keyword arguments can be used together.

**Note:** In the case of mixed arguments, keyword arguments always follow positional arguments.

## Formatted String Literals (f-strings)

This method is known as Literal String Interpolation or f-strings. It makes the string interpolation simpler by embedding the Python expressions inside string constants.

It works by prefixing the string either with **f** or **F**. The string can be formatted in the same way as the str.format() method. It provides a very concise and convenient way of formatting string literals.

Let’s go through with the example:

```python
# Simple example
 
name = 'world'
print(f'Hello, {name}!')

# Output:
Hello, world!
```

This was a simple example. This method also evaluates expressions in real-time. Let’s see another simple example:

```python
# Performing an arithmetic operation
 
print(F'Two minus Ten is {2 - 10}')


# Output:
Two minus Ten is -8
```

This method is very easy and powerful as the real-time implementation makes it faster.

## Formatting with Template Class

This is the standard library, all you have to do is to import the `Template` class from Python’s built-in string module. It is simple but less powerful. Let’s see an example.

```python

from string import Template
 
t = Template('Hello $name, this year is $yr')
print(t.substitute(name='world', yr=2022))

# Output:
Hello world, this year is 2022
```

This format uses $ as a placeholder. First, you have to create a template that is used to pass the variables, and then later in the print statement, we pass the parameters into the template string. `.substitute` is used to replace placeholders.

## Conclusion

In this tutorial, we have used four types of methods to format a string in python. These are the basic examples that will help you to understand which method to use. To know more about them, refer to their [official documentation](https://docs.python.org/3/tutorial/inputoutput.html#fancier-output-formatting).

There are different ways to handle string formatting in Python. Each method has its pros and cons. It depends on your use case which method you want to use.
