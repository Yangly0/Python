---
@Author: liuyangly1
@Date  : 2021-07-07 22:13:45
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 时间类型Time, Calendar

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. time

### 1.1 初始化

```python
>>> import time
>>> import time
>>> ticks = time.time()
>>> print("当前时间戳为:", ticks)
当前时间戳为: 1625667316.030298
```

注意：时间戳单位最适于做日期运算。但是1970年之前的日期就无法以此表示了。太遥远的日期也不行，UNIX和Windows只支持到2038年。

### 1.2 时间元组

| 序号 | 属性     | 值                                          |
| :--- | :------- | :------------------------------------------ |
| 0    | tm_year  | 4位数年 2008                                |
| 1    | tm_mon   | 月 1 到 12                                  |
| 2    | tm_mday  | 日 1 到 31                                  |
| 3    | tm_hour  | 小时 0 到 23                                |
| 4    | tm_min   | 分钟 0 到 59                                |
| 5    | tm_sec   | 秒 0 到 61 (60或61 是闰秒)                  |
| 6    | tm_wday  | 一周的第几日 0到6 (0是周一)                 |
| 7    | tm_yday  | 一年的第几日 1 到 366(儒略历)               |
| 8    | tm_isdst | 夏令时 -1, 0, 1, -1是决定是否为夏令时的旗帜 |

从返回浮点数的时间戳方式向时间元组转换，只要将浮点数传递给如localtime之类的函数。

```python
>>> import time
>>> localtime = time.localtime(time.time())
>>> print("本地时间为 :", localtime)
本地时间为 : time.struct_time(tm_year=2021, tm_mon=7, tm_mday=7, tm_hour=22, tm_min=17, tm_sec=58, tm_wday=2, tm_yday=188, tm_isdst=0)
```

### 1.3 格式化时间

- asctime：简单格式化时间

```python
>>> import time
>>> localtime = time.asctime( time.localtime(time.time()))
>>> print("本地时间为 :", localtime)
本地时间为 : Wed Jul  7 22:19:17 2021
```

- strftime：自定义输出格式

```python
>>> import time
# 格式化成2016-03-20 11:45:39形式
>>> print(time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) )
2021-07-07 22:20:25
# 格式化成Sat Mar 28 22:24:24 2016形式
>>> print(time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) )
Wed Jul 07 22:21:00 2021
```

- mktime： 将格式字符串转换为时间戳

```python
>>> import time
>>> a = "Sat Mar 28 22:24:24 2016"
>>> print(time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y")))
1459175064.0
```

- 格式化符号

```python
%y 两位数的年份表示（00-99）
%Y 四位数的年份表示（000-9999）
%m 月份（01-12）
%d 月内中的一天（0-31）
%H 24小时制小时数（0-23）
%I 12小时制小时数（01-12）
%M 分钟数（00-59）
%S 秒（00-59）
%a 本地简化星期名称
%A 本地完整星期名称
%b 本地简化的月份名称
%B 本地完整的月份名称
%c 本地相应的日期表示和时间表示
%j 年内的一天（001-366）
%p 本地A.M.或P.M.的等价符
%U 一年中的星期数（00-53）星期天为星期的开始
%w 星期（0-6），星期天为星期的开始
%W 一年中的星期数（00-53）星期一为星期的开始
%x 本地相应的日期表示
%X 本地相应的时间表示
%Z 当前时区的名称
%% %号本身
```

### 1.4 time属性

| 序号 | 属性及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | **time.timezone** 属性 time.timezone 是当地时区（未启动夏令时）距离格林威治的偏移秒数（>0，美洲<=0大部分欧洲，亚洲，非洲）。 |
| 2    | **time.tzname** 属性time.tzname包含一对根据情况的不同而不同的字符串，分别是带夏令时的本地时区名称，和不带的。 |

```python
import time
>>> print(time.timezone)
-28800
>>> print(time.tzname)
('中国标准时间', '中国夏令时')
```

### 1.5 time方法

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | time.altzone返回格林威治西部的夏令时地区的偏移秒数。如果该地区在格林威治东部会返回负值（如西欧，包括英国）。对夏令时启用地区才能使用。 |
| 2    | time.asctime([tupletime\])接受时间元组并返回一个可读的形式为"Tue Dec 11 18:07:14 2008"（2008年12月11日 周二18时07分14秒）的24个字符的字符串。 |
| 3    | time.clock( ) 用以浮点数计算的秒数返回当前的CPU时间。用来衡量不同程序的耗时，比time.time()更有用。 |
| 4    | time.ctime([secs]) 作用相当于asctime(localtime(secs))，未给参数相当于asctime() |
| 5    | time.gmtime([secs])接收时间戳（1970纪元后经过的浮点秒数）并返回格林威治天文时间下的时间元组t。注：t.tm_isdst始终为0 |
| 6    | [time.localtime([secs]) 接收时间戳（1970纪元后经过的浮点秒数）并返回当地时间下的时间元组t（t.tm_isdst可取0或1，取决于当地当时是不是夏令时）。 |
| 7    | time.mktime(tupletime)接受时间元组并返回时间戳（1970纪元后经过的浮点秒数）。 |
| 8    | time.sleep(secs) 推迟调用线程的运行，secs指秒数。            |
| 9    | [time.strftime(fmt,tupletime\) 接收以时间元组，并返回以可读字符串表示的当地时间，格式由fmt决定。 |
| 10   | time.strptime(str,fmt='%a %b %d %H:%M:%S %Y')根据fmt的格式把一个时间字符串解析为时间元组。 |
| 11   | time.time( )返回当前时间的时间戳（1970纪元后经过的浮点秒数）。 |
| 12   | time.tzset()根据环境变量TZ重新初始化时间相关设置。           |

## 2. calendar

### 2.1 初始化

```python
>>> import calendar
>>> cal = calendar.month(2016, 1)
>>> print("以下输出2016年1月份的日历:")
以下输出2016年1月份的日历:
>>> print(cal)
    January 2016
Mo Tu We Th Fr Sa Su
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31
```

### 2.2 calendar方法

星期一是默认的每周第一天，星期天是默认的最后一天。更改设置需调用calendar.setfirstweekday()函数。

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | **calendar.calendar(year,w=2,l=1,c=6)** 返回一个多行字符串格式的year年年历，3个月一行，间隔距离为c。 每日宽度间隔为w字符。每行长度为21* W+18+2* C。l是每星期行数。 |
| 2    | **calendar.firstweekday( )** 返回当前每周起始日期的设置。默认情况下，首次载入 calendar 模块时返回 0，即星期一。 |
| 3    | **calendar.isleap(year)** 是闰年返回 True，否则为 False。`>>> import calendar >>> print(calendar.isleap(2000)) True >>> print(calendar.isleap(1900)) False` |
| 4    | **calendar.leapdays(y1,y2)** 返回在Y1，Y2两年之间的闰年总数。 |
| 5    | **calendar.month(year,month,w=2,l=1)** 返回一个多行字符串格式的year年month月日历，两行标题，一周一行。每日宽度间隔为w字符。每行的长度为7* w+6。l是每星期的行数。 |
| 6    | **calendar.monthcalendar(year,month)** 返回一个整数的单层嵌套列表。每个子列表装载代表一个星期的整数。Year年month月外的日期都设为0;范围内的日子都由该月第几日表示，从1开始。 |
| 7    | **calendar.monthrange(year,month)** 返回两个整数。第一个是该月的星期几的日期码，第二个是该月的日期码。日从0（星期一）到6（星期日）;月从1到12。 |
| 8    | **calendar.prcal(year,w=2,l=1,c=6)** 相当于 **print calendar.calendar(year,w=2,l=1,c=6)**。 |
| 9    | **calendar.prmonth(year,month,w=2,l=1)** 相当于 **print calendar.month(year,month,w=2,l=1)** 。 |
| 10   | **calendar.setfirstweekday(weekday)** 设置每周的起始日期码。0（星期一）到6（星期日）。 |
| 11   | **calendar.timegm(tupletime)** 和time.gmtime相反：接受一个时间元组形式，返回该时刻的时间戳（1970纪元后经过的浮点秒数）。 |
| 12   | **calendar.weekday(year,month,day)** 返回给定日期的日期码。0（星期一）到6（星期日）。月份为 1（一月） 到 12（12月）。 |

## 3. Datetime

用于处理日期和时间的类。

### 3.1 时间子类

| 类名称             | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| datetime.date      | 表示日期，常用的属性有：year, month和day                     |
| datetime.time      | 表示时间，常用属性有：hour, minute, second, microsecond      |
| datetime.datetime  | 表示日期时间                                                 |
| datetime.timedelta | 表示两个date、time、datetime实例之间的时间间隔，分辨率（最小单位）可达到微秒 |
| datetime.tzinfo    | 时区相关信息对象的抽象基类。它们由datetime和time类使用，以提供自定义时间的而调整。 |
| datetime.timezone  | Python 3.2中新增的功能，实现tzinfo抽象基类的类，表示与UTC的固定偏移量 |

注意：这些类的对象都是不可变的。

#### 3.1.1 datetime.time

**初始化**

```python
class datetime.time(hour, [minute[, second, [microsecond[, tzinfo]]]])
```

hour为必须参数，其他为可选参数。各参数的取值范围为：

| 参数名称    | 取值范围                             |
| :---------- | :----------------------------------- |
| hour        | [0, 23]                              |
| minute      | [0, 59]                              |
| second      | [0, 59]                              |
| microsecond | [0, 1000000]                         |
| tzinfo      | tzinfo的子类对象，如timezone类的实例 |

**类方法和属性**

| 类方法/属性名称 | 描述                                               |
| :-------------- | :------------------------------------------------- |
| time.max        | time类所能表示的最大时间：time(23, 59, 59, 999999) |
| time.min        | time类所能表示的最小时间：time(0, 0, 0, 0)         |
| time.resolution | 时间的最小单位，即两个不同时间的最小差值：1微秒    |

**对象方法和属性**

| 对象方法/属性名称                                            | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| t.hour                                                       | 时                                                           |
| t.minute                                                     | 分                                                           |
| t.second                                                     | 秒                                                           |
| t.microsecond                                                | 微秒                                                         |
| t.tzinfo                                                     | 返回传递给time构造方法的tzinfo对象，如果该参数未给出，则返回None |
| t.replace(hour[, minute[, second[, microsecond[, tzinfo]]]]) | 生成并返回一个新的时间对象，原时间对象不变                   |
| t.isoformat()                                                | 返回一个‘HH:MM:SS.%f'格式的时间字符串                        |
| t.strftime()                                                 | 返回指定格式的时间字符串，与time模块的strftime(format, struct_time)功能相同 |

```python
>>> from datetime import time
>>>
>>> time.max
datetime.time(23, 59, 59, 999999)
>>> time.min
datetime.time(0, 0)
>>> time.resolution
datetime.timedelta(0, 0, 1)
>>>
>>> t = time(20, 5, 40, 8888)
>>> t.hour
20
>>> t.minute
5
>>> t.second
40
>>> t.microsecond
8888
>>> t.tzinfo
>>>
>>> t.replace(21)
datetime.time(21, 5, 40, 8888)
>>> t.isoformat()
'20:05:40.008888'
>>> t.strftime('%H%M%S')
'200540'
>>> t.strftime('%H%M%S.%f')
'200540.008888'
```

#### 3.1.2 datetime.datetime

**初始化**

```python
class datetime.datetime(year, month, day, hour=0, minute=0, second=0, microsecond=0, tzinfo=None)
```

year, month 和 day是必须要传递的参数， tzinfo可以是None或tzinfo子类的实例。各参数的取值范围为：

| 参数名称    | 取值范围                             |
| ----------- | ------------------------------------ |
| year        | [MINYEAR, MAXYEAR]                   |
| month       | [1, 12]                              |
| day         | [1, 指定年份的月份中的天数]          |
| hour        | [0, 23]                              |
| minute      | [0, 59]                              |
| second      | [0, 59]                              |
| microsecond | [0, 1000000]                         |
| tzinfo      | tzinfo的子类对象，如timezone类的实例 |

如果一个参数超出了这些范围，会引起ValueError异常。

**类方法和属性**

| 类方法/属性名称                         | 描述                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| datetime.today()                        | 返回一个表示当前本期日期时间的datetime对象                   |
| datetime.now([tz])                      | 返回指定时区日期时间的datetime对象，如果不指定tz参数则结果同上 |
| datetime.utcnow()                       | 返回当前utc日期时间的datetime对象                            |
| datetime.fromtimestamp(timestamp[, tz]) | 根据指定的时间戳创建一个datetime对象                         |
| datetime.utcfromtimestamp(timestamp)    | 根据指定的时间戳创建一个datetime对象                         |
| datetime.combine(date, time)            | 把指定的date和time对象整合成一个datetime对象                 |
| datetime.strptime(date_str, format)     | 将时间字符串转换为datetime对象                               |

**对象方法和属性**

| 对象方法/属性名称                                            | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| dt.year, dt.month, dt.day                                    | 年、月、日                                                   |
| dt.hour, dt.minute, dt.second                                | 时、分、秒                                                   |
| dt.microsecond, dt.tzinfo                                    | 微秒、时区信息                                               |
| dt.date()                                                    | 获取datetime对象对应的date对象                               |
| dt.time()                                                    | 获取datetime对象对应的time对象， tzinfo 为None               |
| dt.timetz()                                                  | 获取datetime对象对应的time对象，tzinfo与datetime对象的tzinfo相同 |
| dt.replace([year[, month[, day[, hour[, minute[, second[, microsecond[, tzinfo]]]]]]]]) | 生成并返回一个新的datetime对象，如果所有参数都没有指定，则返回一个与原datetime对象相同的对象 |
| dt.timetuple()                                               | 返回datetime对象对应的tuple（不包括tzinfo）                  |
| dt.utctimetuple()                                            | 返回datetime对象对应的utc时间的tuple（不包括tzinfo）         |
| dt.toordinal()                                               | 同date对象                                                   |
| dt.weekday()                                                 | 同date对象                                                   |
| dt.isocalendar()                                             | 同date独享                                                   |
| dt.isoformat([sep])                                          | 返回一个‘%Y-%m-%d                                            |
| dt.ctime()                                                   | 等价于time模块的time.ctime(time.mktime(d.timetuple()))       |
| dt.strftime(format)                                          | 返回指定格式的时间字符串                                     |

```python
>>> from datetime import datetime, timezone
>>>
>>> datetime.today()
datetime.datetime(2017, 2, 4, 20, 44, 40, 556318)
>>> datetime.now()
datetime.datetime(2017, 2, 4, 20, 44, 56, 572615)
>>> datetime.now(timezone.utc)
datetime.datetime(2017, 2, 4, 12, 45, 22, 881694, tzinfo=datetime.timezone.utc)
>>> datetime.utcnow()
datetime.datetime(2017, 2, 4, 12, 45, 52, 812508)
>>> import time
>>> datetime.fromtimestamp(time.time())
datetime.datetime(2017, 2, 4, 20, 46, 41, 97578)
>>> datetime.utcfromtimestamp(time.time())
datetime.datetime(2017, 2, 4, 12, 46, 56, 989413)
>>> datetime.combine(date(2017, 2, 4), t)
datetime.datetime(2017, 2, 4, 20, 5, 40, 8888)
>>> datetime.strptime('2017/02/04 20:49', '%Y/%m/%d %H:%M')
datetime.datetime(2017, 2, 4, 20, 49)
>>> dt = datetime.now()
>>> dt
datetime.datetime(2017, 2, 4, 20, 57, 0, 621378)
>>> dt.year
2017
>>> dt.month
2
>>> dt.day
4
>>> dt.hour
20
>>> dt.minute
57
>>> dt.second
0
>>> dt.microsecond
621378
>>> dt.tzinfo
>>> dt.timestamp()
1486213020.621378
>>> dt.date()
datetime.date(2017, 2, 4)
>>> dt.time()
datetime.time(20, 57, 0, 621378)
>>> dt.timetz()
datetime.time(20, 57, 0, 621378)
>>> dt.replace()
datetime.datetime(2017, 2, 4, 20, 57, 0, 621378)
>>> dt.replace(2016)
datetime.datetime(2016, 2, 4, 20, 57, 0, 621378)
>>> dt.timetuple()
time.struct_time(tm_year=2017, tm_mon=2, tm_mday=4, tm_hour=20, tm_min=57, tm_sec=0, tm_wday=5, tm_yday=35, tm_isdst=-1)
>>> dt.utctimetuple()
time.struct_time(tm_year=2017, tm_mon=2, tm_mday=4, tm_hour=20, tm_min=57, tm_sec=0, tm_wday=5, tm_yday=35, tm_isdst=0)
>>> dt.toordinal()
736364
>>> dt.weekday()
5
>>> dt.isocalendar()
(2017, 5, 6)
>>> dt.isoformat()
'2017-02-04T20:57:00.621378'
>>> dt.isoformat(sep='/')
'2017-02-04/20:57:00.621378'
>>> dt.isoformat(sep=' ')
'2017-02-04 20:57:00.621378'
>>> dt.ctime()
'Sat Feb 4 20:57:00 2017'
>>> dt.strftime('%Y%m%d %H:%M:%S.%f')
'20170204 20:57:00.621378'
```

注意：datetime.datetime类对时间戳与时间字符串进行转换

#### 3.1.3 datetime.timedelta

**初始化**

**类方法和属性**

**对象方法和属性**

```

```



#### 3.1.4 datetime.timedelta

timedelta对象表示连个不同时间之间的差值。如果使用time模块对时间进行算术运行，只能将字符串格式的时间 和 struct_time格式的时间对象 先转换为时间戳格式，然后对该时间戳加上或减去n秒，最后再转换回struct_time格式或字符串格式，这显然很不方便。而datetime模块提供的timedelta类可以让我们很方面的对datetime.date, datetime.time和datetime.datetime对象做算术运算，且两个时间之间的差值单位也更加容易控制。
 这个差值的单位可以是：天、秒、微秒、毫秒、分钟、小时、周。

**初始化**

```python
class datetime.timedelta(days=0, seconds=0, microseconds=0, milliseconds=0, hours=0, weeks=0)
```

所有参数都是默认参数，因此都是可选参数。参数的值可以是整数或浮点数，也可以是正数或负数。内部值存储days、seconds 和 microseconds，其他所有参数都将被转换成这3个单位：

1毫秒转换为1000微秒
1分钟转换为60秒
1小时转换为3600秒
1周转换为7天
然后对这3个值进行标准化，使得它们的表示是唯一的：

microseconds : [0, 999999]
seconds : [0, 86399]
days : [-999999999, 999999999]

**类方法和属性**

| 类属性名称           | 描述                                                         |
| :------------------- | :----------------------------------------------------------- |
| timedelta.min        | timedelta(-999999999)                                        |
| timedelta.max        | timedelta(days=999999999, hours=23, minutes=59, seconds=59, microseconds=999999) |
| timedelta.resolution | timedelta(microseconds=1)                                    |

**对象方法和属性**

| 实例方法/属性名称  | 描述                                                    |
| :----------------- | :------------------------------------------------------ |
| td.days            | 天 [-999999999, 999999999]                              |
| td.seconds         | 秒 [0, 86399]                                           |
| td.microseconds    | 微秒 [0, 999999]                                        |
| td.total_seconds() | 时间差中包含的总秒数，等价于: td / timedelta(seconds=1) |

| 方法/属性                                  | 描述                                                         |
| :----------------------------------------- | :----------------------------------------------------------- |
| datetime.datetime.now()                    | 返回当前本地时间（datetime.datetime对象实例）                |
| datetime.datetime.fromtimestamp(timestamp) | 返回指定时间戳对应的时间（datetime.datetime对象实例）        |
| datetime.timedelta()                       | 返回一个时间间隔对象，可以直接与datetime.datetime对象做加减操作 |

```python
>>> import datetime
>>>
>>> datetime.timedelta(365).total_seconds() # 一年包含的总秒数
31536000.0
>>> dt = datetime.datetime.now()
>>> dt + datetime.timedelta(3) # 3天后
datetime.datetime(2017, 2, 8, 9, 39, 40, 102821)
>>> dt + datetime.timedelta(-3) # 3天前
datetime.datetime(2017, 2, 2, 9, 39, 40, 102821)
>>> dt + datetime.timedelta(hours=3) # 3小时后
datetime.datetime(2017, 2, 5, 12, 39, 40, 102821)
>>> dt + datetime.timedelta(hours=-3) # 3小时前
datetime.datetime(2017, 2, 5, 6, 39, 40, 102821)
>>> dt + datetime.timedelta(hours=3, seconds=30) # 3小时30秒后
datetime.datetime(2017, 2, 5, 12, 40, 10, 102821)
```

### 3.2 常量

| 常量名称         | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| datetime.MINYEAR | datetime.date或datetime.datetime对象所允许的年份的最小值，值为1 |
| datetime.MAXYEAR | datetime.date或datetime.datetime对象所允许的年份的最大值，只为9999 |

### 3.3 对象方法和属性

| 对象方法/属性名称               | 描述                                                         |
| :------------------------------ | :----------------------------------------------------------- |
| d.year                          | 年                                                           |
| d.month                         | 月                                                           |
| d.day                           | 日                                                           |
| d.replace(year[, month[, day]]) | 生成并返回一个新的日期对象，原日期对象不变                   |
| d.timetuple()                   | 返回日期对应的time.struct_time对象                           |
| d.toordinal()                   | 返回日期是是自 0001-01-01 开始的第多少天                     |
| d.weekday()                     | 返回日期是星期几，[0, 6]，0表示星期一                        |
| d.isoweekday()                  | 返回日期是星期几，[1, 7], 1表示星期一                        |
| d.isocalendar()                 | 返回一个元组，格式为：(year, weekday, isoweekday)            |
| d.isoformat()                   | 返回‘YYYY-MM-DD'格式的日期字符串                             |
| d.strftime(format)              | 返回指定格式的日期字符串，与time模块的strftime(format, struct_time)功能相同 |

```python
>>> import time
>>> from datetime import date
>>>
>>> date.max
datetime.date(9999, 12, 31)
>>> date.min
datetime.date(1, 1, 1)
>>> date.resolution
datetime.timedelta(1)
>>> date.today()
datetime.date(2017, 2, 4)
>>> date.fromtimestamp(time.time())
datetime.date(2017, 2, 4)
>>>
>>> d = date.today()
>>> d.year
2017
>>> d.month
2
>>> d.day
4
>>> d.replace(2016)
datetime.date(2016, 2, 4)
>>> d.replace(2016, 3)
>>> d.replace(2016, 3, 2)
datetime.date(2016, 3, 2)
>>> d.timetuple()
time.struct_time(tm_year=2017, tm_mon=2, tm_mday=4, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=5, tm_yday=35, tm_isdst=-1)
>>> d.toordinal()
736364
>>> d.weekday()
5
>>> d.isoweekday()
6
>>> d.isocalendar()
(2017, 5, 6)
>>> d.isoformat()
'2017-02-04'
>>> d.ctime()
'Sat Feb 4 00:00:00 2017'
>>> d.strftime('%Y/%m/%d')
'2017/02/04'
```

## 参考

- [01-runoob-Python 日期和时间-菜鸟教程](https://www.runoob.com/python/python-date-time.html)

- [02-小关enter-python之时间、日期处理模块（datetime）-CSDN](https://blog.csdn.net/gty931008/article/details/80254806)

