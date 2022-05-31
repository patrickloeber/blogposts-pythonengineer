---
title: Calendar Module in Python
date: 2022-05-31 00:00
description: Learn the basics of the calendar module in Python.
tags: Python, Basics
path: calendar-python
author: Shweta Goyal
---

The `Calendar` module is a built-in module in Python. It can be imported from the module `calendar`. It provides functions to work with dates and times. It can be used to generate calendars, and calendar-related operations. You can format the calendar and output it in text or HTML format.

This module uses an idealized calendar i.e. the current Gregorian calendar which is extended in both directions indefinitely. The calendar has the first day of the week as Monday (value - starts from 0) and the last day of the week as Sunday (value - ends at 6).

Let's see how you can use the calendar module in Python.

## Display the calendar of the month of the year.

```python
import calendar

yy = 2022          # year
mm = 4             # month

print(calendar.month(yy, mm))

# Output:
     April 2022
Mo Tu We Th Fr Sa Su
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30
```

In the above example, the month function takes two arguments, year and month. You get a well-formatted output of the calendar of the month.

## Display the calendar of the year.

```python
import calendar

yy = 2022          # year

print(calendar.calendar(yy))

# Output:
                                2022

      January                   February                   March
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
                1  2          1  2  3  4  5  6          1  2  3  4  5  6
 3  4  5  6  7  8  9       7  8  9 10 11 12 13       7  8  9 10 11 12 13
10 11 12 13 14 15 16      14 15 16 17 18 19 20      14 15 16 17 18 19 20
17 18 19 20 21 22 23      21 22 23 24 25 26 27      21 22 23 24 25 26 27
24 25 26 27 28 29 30      28                        28 29 30 31
31

       April                      May                       June
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
             1  2  3                         1             1  2  3  4  5
 4  5  6  7  8  9 10       2  3  4  5  6  7  8       6  7  8  9 10 11 12
11 12 13 14 15 16 17       9 10 11 12 13 14 15      13 14 15 16 17 18 19
18 19 20 21 22 23 24      16 17 18 19 20 21 22      20 21 22 23 24 25 26
25 26 27 28 29 30         23 24 25 26 27 28 29      27 28 29 30
                          30 31

        July                     August                  September
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
             1  2  3       1  2  3  4  5  6  7                1  2  3  4
 4  5  6  7  8  9 10       8  9 10 11 12 13 14       5  6  7  8  9 10 11
11 12 13 14 15 16 17      15 16 17 18 19 20 21      12 13 14 15 16 17 18
18 19 20 21 22 23 24      22 23 24 25 26 27 28      19 20 21 22 23 24 25
25 26 27 28 29 30 31      29 30 31                  26 27 28 29 30

      October                   November                  December
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
                1  2          1  2  3  4  5  6                1  2  3  4
 3  4  5  6  7  8  9       7  8  9 10 11 12 13       5  6  7  8  9 10 11
10 11 12 13 14 15 16      14 15 16 17 18 19 20      12 13 14 15 16 17 18
17 18 19 20 21 22 23      21 22 23 24 25 26 27      19 20 21 22 23 24 25
24 25 26 27 28 29 30      28 29 30                  26 27 28 29 30 31
31
```

In the above example, the calendar function takes one argument, year. It returns a well-formatted output of the calendar of the year with proper spacing between the months.

There are three classes in the calendar module. They are **Calendar**, **TextCalendar**, and **HTMLCalendar**. The first two classes are used to generate calendars in text format. The third class is used to generate calendars in HTML format. Let's see how you can use these classes.

## Calendar Class

The `Calendar` class creates a calendar object which provides various methods to prepare the calendar data for formatting. Formatting is done by subclasses of the Calendar class but not by the class itself. Let's see how you can use the Calendar class.

### 1.) The `iterweekdays()` methods

It returns an iterator which is the list of the numbers of the weekdays.

```python
import calendar

cal = calendar.Calendar()
for day in cal.iterweekdays():
    print(day, end=' ')

# Output:
0 1 2 3 4 5 6
```

### 2.) The `monthdayscalendar()` method

It returns a list of full weeks and each week is a list of the days of the month.

```python
import calendar

cal = calendar.Calendar()
for month in cal.monthdayscalendar(2022, 5):
    print(month)

# Output:
[0, 0, 0, 0, 0, 0, 1]
[2, 3, 4, 5, 6, 7, 8]
[9, 10, 11, 12, 13, 14, 15]
[16, 17, 18, 19, 20, 21, 22]
[23, 24, 25, 26, 27, 28, 29]
[30, 31, 0, 0, 0, 0, 0]
```

You have seen the two methods of the calendar class but there are more methods. If you want to know more about the methods of the calendar class, you can refer to the [official documentation](https://docs.python.org/3/library/calendar.html#calendar.Calendar) of the calendar class.

## TextCalendar Class

The `TextCalendar` class is used to generate calendars in plain text format. This class creates a text calendar object. In this class, you can also edit the calendar. Let's see how you can use the TextCalendar class.

### 1.) The `formatmonth()` method

It returns a month's calendar in a multi-line string.

```python
import calendar

textcal = calendar.TextCalendar()
year = 2022     # year
month = 5       # month
w = 4           # width of date columns
l = 2           # number of lines per week
print(textcal.formatmonth(year, month, w, l))

# Output:

             May 2022

Mon  Tue  Wed  Thu  Fri  Sat  Sun

                                1

  2    3    4    5    6    7    8

  9   10   11   12   13   14   15

 16   17   18   19   20   21   22

 23   24   25   26   27   28   29

 30   31
```

The above function takes four arguments, year, month, the width of date columns, and the number of lines per week. It returns a well-formatted output of the calendar of the month.

### 2.) The `prmonth()` method

It prints a month's calendar as returned by the `formatmonth()` method. It takes the same arguments as the `formatmonth()` method. You can change the output by changing the arguments. This method avoids the need for a print statement.

```python
import calendar

textcal.prmonth(year, month, 6, 3)

# Output:

                    May 2022


 Mon    Tue    Wed    Thu    Fri    Sat    Sun


                                             1


   2      3      4      5      6      7      8


   9     10     11     12     13     14     15


  16     17     18     19     20     21     22


  23     24     25     26     27     28     29


  30     31
```

In the above example, the width of date columns is 6 and the number of lines per week is 3. If you want to know more about the methods of the TextCalendar class, you can refer to the [official documentation](https://docs.python.org/3/library/calendar.html#calendar.TextCalendar) of the TextCalendar class.

## HTMLCalendar Class

The `HTMLCalendar` class is used to generate calendars in HTML format. This class creates an HTML calendar object. Let's see how you can use the HTMLCalendar class.

### 1.) The `formatmonth()` method

It returns a month's calendar in the form of an HTML table.

```python
import calendar

htmlcal = calendar.HTMLCalendar()
print(htmlcal.formatmonth(2022, 5))

# Output:

<table border="0" cellpadding="0" cellspacing="0" class="month">
<tr><th colspan="7" class="month">May 2022</th></tr>
<tr><th class="mon">Mon</th><th class="tue">Tue</th><th class="wed">Wed</th><th class="thu">Thu</th><th class="fri">Fri</th><th class="sat">Sat</th><th class="sun">Sun</th></tr>
<tr><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="sun">1</td></tr>
<tr><td class="mon">2</td><td class="tue">3</td><td class="wed">4</td><td class="thu">5</td><td class="fri">6</td><td class="sat">7</td><td class="sun">8</td></tr>
<tr><td class="mon">9</td><td class="tue">10</td><td class="wed">11</td><td class="thu">12</td><td class="fri">13</td><td class="sat">14</td><td class="sun">15</td></tr>
<tr><td class="mon">16</td><td class="tue">17</td><td class="wed">18</td><td class="thu">19</td><td class="fri">20</td><td class="sat">21</td><td class="sun">22</td></tr>
<tr><td class="mon">23</td><td class="tue">24</td><td class="wed">25</td><td class="thu">26</td><td class="fri">27</td><td class="sat">28</td><td class="sun">29</td></tr>
<tr><td class="mon">30</td><td class="tue">31</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td></tr>
</table>
```

In the above example, the year is 2022 and the month is 5. The `formatmonth()` method returns a well-formatted HTML calendar of the month. If you want to know more about the methods of the HTMLCalendar class, you can refer to the [official documentation](https://docs.python.org/3/library/calendar.html#calendar.HTMLCalendar) of the HTMLCalendar class.

## Simple Text Calendar

This module provides various useful functions which are different from the above classes. Let's see some of them:

### 1.) Check for a leap year

The `isleap()` function checks whether the year is a leap year or not. The function takes one argument, the year. It returns True if the year is a leap year and False otherwise.

```python
import calendar
print(calendar.isleap(2022))

# Output:
False
```

### 2.) Get the abbreviated weekday names

The `weekheader()` function returns a header that contains abbreviated weekday names. The function takes an argument n, which specifies the width in characters for one weekday.

```python
import calendar
print(calendar.weekheader(3))

# Output:
Mon Tue Wed Thu Fri Sat Sun
```

There are various other methods in the module. You can refer to the [official documentation](https://docs.python.org/3/library/calendar.html) for more information.

## Conclusion

In this tutorial, we have covered the calendar module in Python. The calendar module provides functions to generate calendars in various formats. You can use the calendar module to generate calendars in HTML and text formats. We have also covered the HTMLCalendar class and the TextCalendar class.

