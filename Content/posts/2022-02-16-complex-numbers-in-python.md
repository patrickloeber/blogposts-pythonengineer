---
titlt: Complex Numbers in Python
date: 2022-02-16 00:00
description: Learn the basics of Complex Numbers in Python
tags: Python 
path: 
author: Shweta Goyal
---

# Complex Numbers in Python

Python not only works with real numbers but also works with complex numbers. It has many use cases in mathematics. Python helps to tackle and manipulate them.

Complex numbers are created from two real numbers. You can create it directly or you can use the complex function. It is written in the form of `(x + yj)` where x and y are real numbers and j is an imaginary number which is the square root of -1.

Let’s see the syntax of the complex function:

`complex([real[, imag]])`

It consists of two arguments:

**real:** It is a required input and it denotes the real part of the complex number. By default, it is 0. It can also be represented as a string like this ‘1+1j’ and in that case, the second part will be omitted.

**imag:** It is an optional part and it denotes the imaginary part of the complex number. By default, it is 0.

Let’s see some examples:

```python
z = complex(5, 7)
print("Output:", z)
# Output: (5+7j) 

z = complex(3)
print("Output:", z)
# Output: (3+0j)

z = complex()
print("Output:", z)
# Output: 0j

z = complex('1+1j')
print("Output:", z)
# Output: 1+1j

z = complex(1, -4)
print("Output:", z)
# Output: 1-4j
```

You can also use built-in functions to access the general information. Let’s see an example:

```python
z  = 3 + 4j

print(“Real part:”, z.real)
# Real part: 3.0 

print(“Imaginary part:”, z.imag)
# Imaginary part: 4.0

print(“Conjugate value:”, z.conjugate())
# Conjugate value: 3 - 4j
```

You can learn more about conjugate from [here](https://en.wikipedia.org/wiki/Complex_conjugate).

**Note:** This is the basic rule of the imaginary part that satisfies the following equation:

j^2 = -1

So, you can substitute j^2 with -1 whenever you see it.

## Arithmetic operations on Complex Numbers

Like in real numbers, you can perform mathematical calculations on complex numbers such as addition, multiplication, etc. Let’s see some examples:

```python
z1 = 6 + 7j
z2 = 1 + 4j

print("Addition of numbers:", z1 + z2)
print("Subtraction of numbers:", z1 - z2)
print("Multiplication of numbers:", z1 * z2)
print("Division of numbers:", z1 / z2)
```

The outputs are:

```terminal
Addition of numbers: (7+11j)
Subtraction of numbers: (5+3j)
Multiplication of numbers: (-22+31j)
Division of numbers: (2-1j)
```

Real numbers and imaginary numbers are calculated separately.

You can also perform the exponential operation with the binary operator(**) but you can’t perform it with the `math` module.

**Note:** Complex numbers do not support floor division(//) and comparison operators(<, >, <=, =>).

## Python `cmath` module functions

The `cmath` module in python helps to use advanced mathematical functions like trigonometry, logarithmic, power and log functions, etc. You can use the `math` module to use these functions but only for real numbers as it does not support complex numbers. The `cmath` module helps to use these functions for complex numbers.

The `cmath` module also consists of constants like pi, e, inf, nan, and so on that can be used in calculations. You can learn more functions and constants from the [official site](https://docs.python.org/3/library/cmath.html).

Let’s see some of the functions that can be performed on the complex numbers:

```python
import cmath

z = 4 + 2j

# Power and log functions like log2, log10, sqrt
# Power function
print("e^z:", cmath.exp(z))

# Logarithm function
print("log2(z):", cmath.log(z, 2))

# Trigonometric functions
# For sine value
print("Sine Value:", cmath.sin(z))

# For cosine value
print("Arc Sine Value:", cmath.asin(z))

# Hyperbolic functions
# For hyperbolic sine value
print("Hyperbolic Sine Value:", cmath.sinh(z))

# For Inverse hyperbolic sine value
print("Inverse Hyperbolic Sine Value:", cmath.asinh(z))
```

The outputs are:

```terminal
e^z: (-22.720847417619233+49.645957334580565j)
log2(z): (2.1609640474436813+0.6689021062254881j)
Sine Value: (-2.8472390868488278-2.3706741693520015j)
Arc Sine Value: (1.096921548830143+2.183585216564564j)
Hyperbolic Sine Value: (-11.356612711218174+24.83130584894638j)
Inverse Hyperbolic Sine Value: (2.198573027920936+0.4538702099631225j)
```

### Miscellaneous Functions

These functions help us to determine if the complex number is nan, infinite, or finite. They also help us to check if the complex numbers are close. The values returned will be either true or false.

They will return **true** when both the real and the imaginary part is finite, infinite, or nan, otherwise you will get **false**.

Let’s see some examples of complex numbers:

```python
import cmath

# Check if they are finite
print(cmath.isfinite(4 + 1j))               # True

# Check if they are infinite
print(cmath.isinf(4 + 1j))                  # False

# Above result is false as z is already finite, it can't be infinite. 
# We can make it infinite by making real number infinite.
print(cmath.isinf(cmath.inf + 1j))           # True        

# Check if they are nan
print(cmath.isnan(4 + 1j))                   # False

# Above result is false because the real number is true. 
# You can make the result by changing the real number to nan.
print(cmath.isnan(cmath.nan + 1j))            # True

# Check if two numbers are close 
print(cmath.isclose(1 + 1j, 1.02 + 0.8j, rel_tol=0.5))          #True
print(cmath.isclose(1 + 1j, 1.02 + 0.8j, abs_tol=0.05))         # False
```

> rel_tol is relative tolerance which is maximum allowed difference and must be greater than zero.
abs_tol is absolute tolerance which is minimum allowed difference and must be at least zero or near to zero.

You can inverse the results by changing the real numbers.

### Constants

There are some constants which can be used in calculations. Let's see those constants:

```python
import cmath

# Value of pi
print("pi:", cmath.pi)

# Value of e
print("e:", cmath.e)

# Positive Infinity
print("Positive infinity:", cmath.inf)

# Complex number: zero real part and positive infinity imaginary part
print("Positive complex infinity:", cmath.infj)

# Not a number value
print("NaN value:", cmath.nan)

# Complex number: zero real part and NaN imaginary part
print("NaN complex value:", cmath.nanj)
```

The outputs are:

```terminal
pi: 3.141592653589793
e: 2.718281828459045
Positive infinity: inf
Positive complex infinity: infj
NaN value: nan
NaN complex value: nanj
```

## Conclusion

The functions that are defined in the `cmath` module are similar to that with the `math` module but they are not identical. The results that you get after using the `cmath` module will always be a complex number even if the value is a real number, in that case, the value of the imaginary part will be zero.

In this article, you have learned about complex numbers and the cmath module which provides various functions and constants that you can use for complex numbers.
