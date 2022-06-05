---
title: Exploring statistics library in Python
date: 2022-06-05 00:00
description: Learn all functions in statistics module with examples.
tags: Python, Basics
path: statistics-python
author: Pratik Choudhari
---

The statistics module is a useful yet overlooked module in the Python standard libraries. It provides functions through which one can calculate almost all statistical values such as mean, covariance, etc. 

For simple statistical calculations, instead of installing a third-party library like NumPy, we can use this built-in module. In this blog, we are going to explore the `statistics` module with examples.

## Averages and measures of central location

In this section, we will be discussing functions related to mean, median, mode and quantiles.

### Averages

The statistics module provides users with four functions pertaining to averages:
- mean()
- fmean()
- geometric_mean()
- harmonic_mean()

Every function has the same input parameter, a list of numbers, except harmonic_mean() which along with a list of numbers optionally takes weights input.

fmean() is a faster version of mean() and it always returns a floating value.

Example:

```python
import random
import statistics as st

numbers = [random.randint(1, 100) for _ in range(10)]

print("Generated random list:", numbers)

print("Mean:", st.mean(numbers))

print("Fast Mean:", st.fmean(numbers))

print("Geometric Mean:", st.geometric_mean(numbers))

print("Harmonic Mean:", st.harmonic_mean(numbers))
```

Output:
```console
Generated random list: [69, 23, 10, 25, 98, 49, 98, 70, 49, 25]
Mean: 51.6
Fast Mean: 51.6
Geometric Mean: 69, 23, 10, 25, 98, 49, 98, 70, 49, 25
Harmonic Mean: 31.89983771747745
```

### Median or Measure of Central Tendency

There are four functions related to finding the median of a distribution.

- median(): find median using mean of middle two method
- median_low(): return lower of middle two
- median_high(): return higher of moddle two
- median_grouped(): median of continuous grouped data

All functions take a compulsory argument `data` which is the list of numbers, `median_grouped()` optionally takes another argument `interval` which affect the interpolation on data and hence the result.

Example:

```python
import random
import statistics as st

numbers = sorted([random.randint(1, 100) for _ in range(10)])

print("Generated random list:", numbers)

print("Median:", st.median(numbers))

print("Lower Median:", st.median_low(numbers))

print("Higher Median:", st.median_high(numbers))

print("Grouped Median:", st.median_grouped(numbers))
```

Output:

```console
Generated random list: [10, 21, 26, 30, 41, 70, 78, 95, 97, 98]
Median: 55.5
Lower Median: 41
Higher Median: 70
Grouped Median: 69.5
```

### Mode and Quantiles

Mode is a measure of central location, a collection of nominal values can have one or more modes.
- mode(): returns a single value of most occurring element occurring first in data
- multimode(): returns a list of all modes in a collection

Next, `quantiles()` divides a collection of numbers into 4 intervals and returns a list of all cut points separating the intervals.

Example:

```python
import random
import statistics as st

numbers = sorted([random.randint(1, 100) for _ in range(10)])

print("Generated random list:", numbers)

print("Quantiles:", st.quantiles(numbers))

numbers = [1, 1, 1, 2, 3, 3, 4, 4, 4, 5, 5]

print("Mode:", st.mode(numbers))

print("Multi Mode:", st.multimode(numbers))
```

Output:

```console
Generated random list: [4, 9, 13, 27, 47, 62, 82, 91, 98, 99]
Quantiles: [12.0, 54.5, 92.75]
Mode: 1
Multi Mode: [1, 4]
```

## Variance and Standard Deviation

A distribution has two types of variance and standard deviation namely population and sample.
- pvariance(): returns variance of population
- pstdev(): square root of pvariance() result
- variance(): returns variance of sample
- stdev(): square root of variance() result

pvariance() and pstdev() optionally takes an argument `mu` which should be the mean of data, if any other value is provided variance is calculated around that point.

variance() and stdev() optionally takes an argument `xbar` which should strictly be the mean of data.

Example:

```python
import random
import statistics as st

numbers = sorted([random.randint(1, 100) for _ in range(10)])

print("Generated random list:", numbers)

print("Population variance:", st.pvariance(numbers))

print("Population standard deviation:", st.pstdev(numbers))

print("Sample variance:", st.variance(numbers))

print("Sample standard deviation:", st.stdev(numbers))
```

Output:

```console
Generated random list: [6, 7, 12, 26, 27, 28, 41, 50, 60, 69]
Population variance: 433.24
Population standard deviation: 20.814418079783064
Sample variance: 481.3777777777778
Sample standard deviation: 21.940323101034263
```

## Relation between two inputs

This module provides three ways to check relationship between two inputs, using these functions we can estimate value of another input based on value of one input. Following are the functions available:
- covariance(): returns measure of joint variability between two inputs
- correlation(): returns pearson correlation coefficient value between -1 to +1 
- linear_regression(): calculates the slope and intercept from linear regression concept

Example:

```python
import statistics as st

x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

print("Covariance:", st.covariance(x, y))

print("Correlation:", st.correlation(x, y))

slope, intercept = st.linear_regression(x, y)
print("Slope:", slope, "Intercept:", intercept)

```

Output:

```console
Covariance: -9.166666666666666
Correlation: -1.0
Slope: -1.0 Intercept: 11.0
```
