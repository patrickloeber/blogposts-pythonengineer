---
titlt: datetime Module in Python
date: 2022-02-27 00:00
description: Learn the basics of datetime module in Python
tags: Python, Basics
path: datetime-module
author: Shweta Goyal
---

To work with date and time, you can import a module named **datetime** which comes built-in with Python. The date and time do not have a data type on their own in Python instead Python provides classes to work with date and time.

There are six types of classes in the datetime module that helps to work with the date and time objects:

## date class

[date](https://docs.python.org/3/library/datetime.html#datetime.date) class assumes the Georgian calendar. Its attributes are year, month, and day. Let's see an example of how to represent a date with a date object.

```python
import datetime

# date object to represent the date
dt = datetime.date(2022, 2, 24)
print(dt)
```

Output:
```console
2022-02-24
```

Here, date() is the constructor of the date class with three arguments - year, month, and day. `dt` is the object from the date class. Let's take another example to get the current date, year, month, and day.

```python
from datetime import date

# date object of today's date
today = date.today()

# Get current date
print("Current date:", today)

# Get day, month, and year of the week
print("Current year:", today.year)
print("Current month:", today.month)
print("Current day:", today.day)
```

The outputs are:

```terminal
Current date: 2022-02-24
Current year: 2022
Current month: 2
Current day: 24
```

There are other constructors from the date class that you can use like `weekday`, `strftime`, `replace`, `fromtimestamp`, etc. You can get those methods from their [official site](https://docs.python.org/3/library/datetime.html#datetime.date).

## time class

[time](https://docs.python.org/3/library/datetime.html#datetime.time) class gives time-related functions where you don’t need dates and assumes every day has 24\*60\*60 seconds. Its attributes are second, minute, hour, microsecond, etc.

Let's take an example of how to represent a time with a time object. Time object represents a local time of the day.

```python
from datetime import time

# without arguments
t1 = time()
print("t1:", t1)

# with arguments - time(hour, minute, second)
t2 = time(12, 11, 9)
print("t2:", t2)
```

The outputs are:

```terminal
t1: 00:00:00
t2: 12:11:09
```

Here, t1 and t2 are the objects from the time class and time() is the constructor from the time class. Let’s take another example to access the attributes like an hour, minute, second, and microsecond.

```python
from datetime import time

t = time(6, 11, 12, 999)

print("Hour:", t.hour)
print("Minute:", t.minute)
print("Second:", t.second)
print("Microsecond:", t.microsecond)
```

The outputs are:

```terminal
Hour: 6
Minute: 11
Second: 12
Microsecond: 999
```

By default, the microsecond value is 0. There are other constructors from the time class that you can use like `strftime`, `replace`, `min`, `max`, etc. You can get those methods from their [official site](https://docs.python.org/3/library/datetime.html#datetime.time).

## datetime class

[datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime) class is a combination of date and time which contains all the information of date and time objects. Its attributes are year, month, day, hour, minute, second, microsecond, etc. Let’s take an example:

```python
from datetime import datetime

# without time arguments
dt1 = datetime(2022, 2, 24)
print("dt1:", dt1)

# with time arguments 
dt2 = datetime(2022, 2, 24, 11, 10, 36, 1214)
print("dt2:", dt2)
```

The outputs are:

```terminal
dt1: 2022-02-24 00:00:00
dt2: 2022-02-24 11:10:36.001214
```

The first three arguments i.e. arguments of date object are mandatory and the default value of the time object is 0. Let’s take another example to access the attributes of date and time objects:

```python
from datetime import datetime

# Accessing today's datetime
today = datetime.now()

# Accessing the attributes
print("Today's Day:", today.day)
print("Today's Month:", today.month)
print("Today's Year:", today.year)
print("Today's Hour:", today.hour)
print("Today's Minute:", today.minute)
print("Today's Second:", today.second)
```

The outputs are:

```terminal
Today's Day: 24
Today's Month: 2
Today's Year: 2022
Today's Hour: 3
Today's Minute: 53
Today's Second: 30
```

There are other constructors from the time class that you can use like `utc`, `combine`, `utcnow`, etc. You can get those methods from their [official site](https://docs.python.org/3/library/datetime.html#datetime.datetime).

## timedelta class

[timedelta](https://docs.python.org/3/library/datetime.html#datetime.timedelta) class is used to calculate the differences between the two dates and times and measured in durations. The result can be either positive or negative. Its attributes are days, seconds, microseconds, milliseconds, minutes, hours, weeks.

Let’s see an example:

```python
from datetime import datetime, timedelta

# Creating datetime objects
date1 = datetime(2021, 6, 24)
date2 = datetime(2020, 4, 20)

# Difference between date objects
diff = date2 - date1
print("Difference between dates:", diff)

# Subtracting days from date1
date1 -= timedelta(days=13)
print("Date1 before 13 days:", date1)

# Adding weeks to date2
date2 += timedelta(weeks=12)
print("Date2 after 12 weeks:", date2)
```

The outputs are:

```terminal
Difference between dates: -430 days, 0:00:00
Date1 before 13 days: 2021-06-11 00:00:00
Date2 after more weeks: 2020-07-13 00:00:00
```

Here, the default value of the time objects is 0. There are other constructors from the timedelta class that you can use like `total_seconds`, `min`, `max`, etc. You can get those methods from their [official site](https://docs.python.org/3/library/datetime.html#datetime.timedelta).

## tzinfo class

[tzinfo](https://docs.python.org/3/library/datetime.html#datetime.tzinfo) class is an abstract base class which means you can not instantiate it directly. It gives timezone information objects. It is used by datetime and time class to give more control over timezones.

There are various methods available that you can use like `utcoffset`, `dst`, `fromutc`, etc. You can learn more about it from their [official site](https://docs.python.org/3/library/datetime.html#datetime.tzinfo).

## timezone class

[timezone](https://docs.python.org/3/library/datetime.html#datetime.timezone) class implements the tzinfo abstract base class and is defined by the fixed offset from the UTC. This helps to represent timezone according to a specific region and to handle the timezones, we use [pytz module](http://pytz.sourceforge.net/).

Also, it would be good to know about strftime and strptime from their [official site](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior) as the strftime method creates a string representing a time and strptime method creates a datetime object from a string representing a date and a time object.

## Conclusion

In this article, you have learned about the six different classes in the datetime module and to know more about it, you can visit Python’s official site.
