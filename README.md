# fdate

Formats date string as 'yyyy-mm-dd' and manipulates date strings.

Installation
---------------

Use one of the following method:

* pip install
```bash
pip --install fdate
pip --install fdate --upgrade
```
* clone repository and install with:
```
python setup.py install
```        
Usage
-------

* Initializations

From a string of format 'yyyy-mm-dd', where the separator '-' can be any non-digital character.
```python
>>> from fdate import *
>>> fd = Fdate('2018/4/7')
>>> fd
'2018-04-07'
>>> fd = Fdate('2018-4-7')
>>> fd
'2018-04-07'
``` 
From exactly 8-length digits or Fdate object.
```python
>>> fd = Fdate('20180407')
>>> fd
'2018-04-07'
>>> fe = Fdate(fd)
>>> fe
'2018-04-07'
```

From unix timestamp, with default time unit: second.
```python
>>> fd = Fdate().from_timestamp(1523030400)
>>> fd
'2018-04-07'
```

In case time unit is not second, say minisecond, set `unit=1000`.
```python
>>> fd = Fdate().from_timestamp(1523030400000, unit=1000)
>>> fd
'2018-04-07'
```

From function `today(shift=0)`
```python
>>> fd = today()  # today
>>> fd = today(-1)  # yesterday
>>> fd = today(1)  # tomorrow
```

* Properties
```python
>>> fd = Fdate('20180407')
>>> fd.year, fd. month, fd.day
(2018, 4, 7)
>>> fd.rank  # 2018-04-07 is the 97th day of the year.
97
>>> fd.is_weekend
True
>>> fd.is_workday
False
>>> fd.is_leap_year
False
>>> fd.is_first_day(of='M')  # first day of the ... ?  'M' -- month (default), 'Y' -- year
False
>>> Fdate('2018-3-31').is_last_day()
True
>>> fd.to_timestamp() # to unix timestamp
1523030400
``` 

* Calculations

```python
>>> fd = Fdate('20180407')
>>> fd + 1
'2018-04-08'
>>> fd -= 1
>>> fd
'2018-04-06'
>>> fd - '2018.3.6'
31
>>> fd - '2018/5/6'
-30
>>> fd > '2018-3-6'
True
>>> fd == '2018.4.6'
True
```

* Iterations

```python
>>> [x for x in drange('2018-03-30', '2018-04-03')]
['2018-03-30', '2018-03-31', '2018-04-01', '2018-04-02', '2018-04-03']
>>> [x for x in drange('2018-04-03', '2018-03-30')]
['2018-04-03', '2018-04-02', '2018-04-01', '2018-03-31', '2018-03-30']
```