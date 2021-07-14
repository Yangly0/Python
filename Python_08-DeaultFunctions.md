---
@Author: liuyangly1
@Date  : 2021-07-08 21:30:06
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 内置函数

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

|                        |             | 内置函数     |                             |                     |
| :--------------------- | :---------- | :----------- | :-------------------------- | :------------------ |
| abs()                  | divmod()    | input()      | open()                      | staticmethod()      |
| all()                  | enumerate() | int()        | ord()                       | str()               |
| any()                  | eval()      | isinstance() | pow()                       | sum()               |
| basestring() [3.x移除] | execfile()  | issubclass() | print()                     | super()             |
| bin()                  | file()      | iter()       | property()                  | tuple()             |
| bool()                 | filter()    | len()        | range()                     | type()              |
| bytearray()            | float()     | list()       | raw_input() [3.x移除]       | unichr() [3.x移除]  |
| callable()             | format()    | locals()     | reduce() [3.x移到functools] | unicode() [3.x移除] |
| chr()                  | frozenset() | long()       | reload()                    | vars()              |
| classmethod()          | getattr()   | map()        | repr()                      | xrange() [3.x移除]  |
| cmp() [3.x移除]        | globals()   | max()        | reversed()                  | zip()               |
| compile()              | hasattr()   | memoryview() | round()                     | \_\_import\_\_()    |
| complex()              | hash()      | min()        | set()                       |                     |
| delattr()              | help()      | next()       | setattr()                   |                     |
| dict()                 | hex()       | object()     | slice()                     |                     |
| dir()                  | id()        | oct()        | sorted()                    | exec 内置表达式     |

## 1. 逻辑算术函数

### 1.1 绝对值函数abs()

返回数字的绝对值。

```python
>>> abs(-1)
1
```

### 1.2 全真判断函数all()

用于判断给定的可迭代参数 iterable 中的所有元素是否都为 TRUE，如果是返回 True，否则返回 False。

等效于：

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

注意，元素除了是 0、空、None、False 外都算 True。

```python
>>> all([1, 2, 3])
True
>>> all([1, 2, 0])
False
>>> all([])
True
>>> all([None, 1, 2])
False
>>> all([False, 1, 2])
False
```

### 1.3 全假判断函数any()

用于判断给定的可迭代参数 iterable 是否全部为 False，则返回 False，如果有一个为 True，则返回 True。

等效于：

```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

注意：元素除了是 0、空、None、FALSE 外都算 TRUE。

```python
>>> any([0, 1, 2])
True
>>> any([0, None, False])
False
```

### 1.4 除余函数divmod()

把除数和余数运算结果结合起来，返回一个包含商和余数的元组(a // b, a % b)。

```python
# divmod(a, b)
>>> divmod(7, 2)
(3, 1)

>>> divmod(1+2j,1+0.5j)
((1+0j), 1.5j)
```

### 1.5  最大值函数max()

返回给定参数的最大值，参数可以为序列。

```python
# max( x, y, z, .... , key)
# x -- 数值表达式。
# y -- 数值表达式。
# z -- 数值表达式。
# key -- 函数

# 最大值
>>> max([1, 2, 3, 4, 2])
4

# 最大长度
>>> max(['1', '22', '3', '4', '21.0'], key=len)
'21.0'
```

注意：合理利用key定义比较函数，提高效率。

### 1.6 最小值函数min()

```python
# min( x, y, z, .... , key)
# x -- 数值表达式。
# y -- 数值表达式。
# z -- 数值表达式。
# key -- 函数

# 最小值
>>> min([1, 2, 3, 4, 2])
1

# 最小长度
>>> min(['1', '22', '3', '4', '21.0'], key=len)
'1'
```

### 1.7 幂函数pow()

返回 x 的 y 次方 的值。

```python
pow(x, y[, z])
# 等效于 math.pow( x, y )

>>> pow(2, 3)
8
```

### 1.8 四舍五入函数round()

返回浮点数x的四舍五入值。

```python
# round( x [, n]  )
# x -- 数值表达式。
# n -- 数值表达式，表示从小数点位数。

>>> round(80.23456, 2)
80.23
>>> round(100.000056, 3)
100.0
>>> round(100.000056)
100
```

### 1.9 求和函数sum()

对序列进行求和计算。

```python
sum(iterable[, start])
# iterable -- 可迭代对象，如：列表、元组、集合。
# start -- 指定相加的参数，如果没有设置这个值，默认为0。

>>> sum([1, 2, 3, 4])
10
>>> sum([1, 2, 3, 4], 2)  # 列表计算总和后再加 2
12
```

## 2. 功能函数

### 2.1 执行函数eval()

用来执行一个字符串表达式，并返回表达式的值

```python
eval(expression[, globals[, locals]])
# expression -- 表达式。
# globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
# locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。

>>>x = 7
>>> eval( '3 * x' )
21
>>> eval('pow(2,2)')
4
>>> eval('2 + 2')
4
>>> n=81
>>> eval("n + 4")
85
```

### 2.2 复杂执行函数exec()

执行储存在字符串或文件中的Python语句，相比于 eval，exec可以执行更复杂的 Python 代码。

```python
exec obj
# obj -- 要执行的表达式。
# exec 返回值永远为 None。

>>> exec('print("Hello World")')
Hello World
```

### 2. 3 过滤函数filter()

用于过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表。

```python
# filter(function, iterable)
# function -- 判断函数。
# iterable -- 可迭代对象。

# 偶数判断
>>> filter(lambda x:x%2==0, [1, 2, 3, 4, 5])
<filter object at 0x00000189A6AA7788>
# list是为了显示可迭代对象。
>>> list(filter(lambda x:x%2==0, [1, 2, 3, 4, 5]))
[2, 4]
```

### 2.4 全局变量函数globals()

会以字典类型返回当前位置的全部全局变量

```python
globals()

>>>a='runoob'
>>> print(globals()) # globals 函数返回一个全局变量的字典，包括所有导入的变量。
{'__builtins__': <module '__builtin__' (built-in)>, '__name__': '__main__', '__doc__': None, 'a': 'runoob', '__package__': None}
```

###  2.5 地址函数id()

全局变量和局部变换函数globals locals

```python
id([object])
# object -- 对象。
# 返回对象的内存地址。

>>> x = 1
>>> y = 1
>>> id(x)
140720019972496
>>> id(y)
140720019972496
```

### 2.6 长度函数len()

返回对象（字符、列表、元组等）长度或项目个数。

```python
# len(s)
# s -- 对象。

>>> len('abc')
3

>>> len([1, 2, 3, 4])
4
```

### 2.7 局部变量函数locals()

会以字典类型返回当前位置的全部局部变量。

对于函数, 方法, lambda 函式, 类, 以及实现了 __call__ 方法的类实例, 它都返回 True。

```python
locals()

>>>def runoob(arg):    # 两个局部变量：arg、z
...     z = 1
...     print (locals())
... 
>>> runoob(4)
{'z': 1, 'arg': 4}      # 返回一个名字/值对的字典
```

### 2.8 映射函数map()

根据提供的函数对指定序列做映射

```python
map(function, iterable, ...)
# function -- 函数
# iterable -- 一个或多个序列

>>> map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
<map object at 0x00000189A6AA7888>
# list为了显示迭代器
list(map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10]))
[3, 7, 11, 15, 19]
```

### 2.9 反向函数reversed()

用于反向列表中元素。

```python
# reversed(list)

>>> reversed([1, 2, 3, 4])
<list_reverseiterator object at 0x00000189A6AA7708>
>>> list(reversed([1, 2, 3, 4]))
[4, 3, 2, 1]
```

### 2.10 排序函数sorted()

对所有可迭代的对象进行排序操作。

```python
sorted(iterable, key=None, reverse=False)

# iterable -- 可迭代对象。
# key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
# reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。

>>> sorted([5,7,6,3,4,1,2])
[1, 2, 3, 4, 5, 6, 7]
>>> sorted([('b',2),('a',1),('c',3),('d',4)], key=lambda x:x[1])
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]
>>> sorted([('b',2),('a',1),('c',3),('d',4)], key=lambda x:x[1], reverse=True)
[('d', 4), ('c', 3), ('b', 2), ('a', 1)]
```

### 2.11 组合函数zip()

用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。

```python
zip([iterable, ...])
# iterabl -- 一个或多个迭代器;

# 组合
>>> zip([1, 2, 3], [4, 5, 6])
<zip object at 0x00000189A6AAB188>
>>> list(zip([1, 2, 3], [4, 5, 6]))
[(1, 4), (2, 5), (3, 6)]

# 解压
>>> x = list(zip([1, 2, 3], [4, 5, 6]))
>>> list(zip(*x))
[(1, 2, 3), (4, 5, 6)]
```

### 2.12 切片函数slice

实现切片对象，主要用在切片操作函数里的参数传递。

```python
class slice(stop)
class slice(start, stop[, step])

# start -- 起始位置
# stop -- 结束位置
# step -- 间距

>>>myslice = slice(5)    # 设置截取5个元素的切片
>>> myslice
slice(None, 5, None)
>>> arr = range(10)
>>> arr
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> arr[myslice]         # 截取 5 个元素
[0, 1, 2, 3, 4]
```



## 3. 数据类型函数

### 3.1 二进制函数bin()

返回一个整数 int 或者长整数 long int 的二进制表示。

```python
bin(x)
# x -- int 或者 long int 数字

>>> bin(10)
'0b1010'
```

### 3.2 布尔函数bool()

用于将给定参数转换为布尔类型，如果没有参数，返回 False。

```python
bool([x])
# x -- 要进行转换的参数。


>>>bool()
False
>>> bool(0)
False
>>> bool(1)
True
>>> bool(2)
True
>>> issubclass(bool, int)  # bool 是 int 子类
True
```

### 3.3 字节函数bytearray()

返回一个新字节数组。这个数组里的元素是可变的，并且每个元素的值范围: 0 <= x < 256。

```python
class bytearray([source[, encoding[, errors]]])
# 如果 source 为整数，则返回一个长度为 source 的初始化数组；
# 如果 source 为字符串，则按照指定的 encoding 将字符串转换为字节序列；
# 如果 source 为可迭代类型，则元素必须为[0 ,255] 中的整数；
# 如果 source 为与 buffer 接口一致的对象，则此对象也可以被用于初始化 bytearray。
# 如果没有输入任何参数，默认就是初始化数组为0个元素。

>>>bytearray()
bytearray(b'')
>>> bytearray([1,2,3])
bytearray(b'\x01\x02\x03')
>>> bytearray('runoob', 'utf-8')
bytearray(b'runoob')
```

### 3.4 字节码函数compile()

将一个字符串编译为字节代码。

```python
compile(source, filename, mode[, flags[, dont_inherit]])

# source -- 字符串或者AST（Abstract Syntax Trees）对象。。
# filename -- 代码文件名称，如果不是从文件读取代码则传递一些可辨认的值。
# mode -- 指定编译代码的种类。可以指定为 exec, eval, single。
# flags -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。。
# flags和dont_inherit是用来控制编译源码时的标志

>>>str = "for i in range(0,10): print(i)" 
>>> c = compile(str,'','exec')   # 编译为字节代码对象 
>>> c
<code object <module> at 0x10141e0b0, file "", line 1>
>>> exec(c)
0
1
2
3
4
5
6
7
8
9
>>> str = "3 * 4 + 5"
>>> a = compile(str,'','eval')
>>> eval(a)
17
```

### 3.5 字节函数chr()

用一个范围在 range（256）内的（就是0～255）整数作参数，返回一个对应的字符。

```python
chr(i)
# i -- 可以是10进制也可以是16进制的形式的数字。
# 返回值是当前整数对应的 ASCII 字符。

>>>print(chr(0x30), chr(0x31), chr(0x61))    # 十六进制
0 1 a
>>> print(chr(48), chr(49), chr(97) )        # 十进制
0 1 a
```

### 3.6 复数函数complex()

用于创建一个值为 $real + imag * j$ 的复数或者转化一个字符串或数为复数。如果第一个参数为字符串，则不需要指定第二个参数。

```python
class complex([real[, imag]])
# real -- int, long, float或字符串；
# imag -- int, long, float；
# 返回一个复数

>>>complex(1, 2)
(1 + 2j)
>>> complex(1)    # 数字
(1 + 0j)
>>> complex("1")  # 当做字符串处理
(1 + 0j)
# 注意：这个地方在"+"号两边不能有空格，也就是不能写成"1 + 2j"，应该是"1+2j"，否则会报错
>>> complex("1+2j")
(1 + 2j)
```

### 3.7 字典函数dict()

用于创建一个字典。

```python
class dict(**kwarg)
class dict(mapping, **kwarg)
class dict(iterable, **kwarg)
# **kwargs -- 关键字
# mapping -- 元素的容器。
# iterable -- 可迭代对象。
# 返回一个字典。

>>>dict()                        # 创建空字典
{}
>>> dict(a='a', b='b', t='t')     # 传入关键字
{'a': 'a', 'b': 'b', 't': 't'}
>>> dict(zip(['one', 'two', 'three'], [1, 2, 3]))   # 映射函数方式来构造字典
{'three': 3, 'two': 2, 'one': 1} 
>>> dict([('one', 1), ('two', 2), ('three', 3)])    # 可迭代对象方式来构造字典
{'three': 3, 'two': 2, 'one': 1}
```

### 3.8  浮点数函数float()

用于将整数和字符串转换成浮点数。

```python
class float([x])
# x -- 整数或字符串
# 返回浮点数。

>>>float(1)
1.0
>>> float(112)
112.0
>>> float(-123.6)
-123.6
>>> float('123')     # 字符串
123.0
```

### 3.9  固定集合函数frozenset()

返回一个冻结的集合，冻结后集合不能再添加或删除任何元素。

```python
class frozenset([iterable])
# iterable -- 可迭代的对象，比如列表、字典、元组等等。
# 返回新的 frozenset 对象，如果不提供任何参数，默认会生成空集合。

>>>frozenset(range(10))     # 生成一个新的不可变集合
frozenset([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
>>>frozenset('runoob') 
frozenset(['b', 'r', 'u', 'o', 'n'])   # 创建不可变集合
```

### 3.10 十六进制hex()

用于将10进制整数转换成16进制，以字符串形式表示。

```python
hex(x)
# x -- 10进制整数
# 返回16进制数，以字符串形式表示。

>>>hex(255)
'0xff'
>>> hex(-42)
'-0x2a'
>>> hex(1L)
'0x1L'
>>> hex(12)
'0xc'
>>> type(hex(12))
<class 'str'>      # 字符串
```

### 3.11 整型函数int()

用于将一个字符串或数字转换为整型。

```python
class int(x, base=10)
# x -- 字符串或数字。
# base -- 进制数，默认十进制。
# 返回整型数据。

>>>int()               # 不传入参数时，得到结果0
0
>>> int(3)
3
>>> int(3.6)
3
>>> int('12',16)        # 如果是带参数base的话，12要以字符串的形式进行输入，12 为 16进制
18
>>> int('0xa',16)  
10  
>>> int('10',8)  
8
```

### 3.12 列表函数list()

用于将元组转换为列表。

**注意：**元组与列表是非常类似的，区别在于元组的元素值不能修改，元组是放在括号中，列表是放于方括号中。

```python
list( tup )
# tup -- 要转换为列表的元组。
# 返回列表。
 
>>> list((123, 'runoob', 'google', 'abc'))
[123, 'runoob', 'google', 'abc']
```

### 3.13 内存查看对象函数memoryview()

返回给定参数的内存查看对象(memory view)。

所谓内存查看对象，是指对支持缓冲区协议的数据进行包装，在不需要复制对象基础上允许Python代码访问。

```python
memoryview(obj)
# obj -- 对象

>>>v = memoryview(bytearray("abcefg", 'utf-8'))
>>> print(v[1])
98
>>> print(v[-1])
103
>>> print(v[1:4])
<memory at 0x10f543a08>
>>> print(v[1:4].tobytes())
b'bce'
>>>
```

### 3.14 八进制oct()

将一个整数转换成 8 进制字符串。 8 进制以 **0o** 作为前缀表示。

```python
oct(x)
# x -- 整数。
# 返回 8 进制字符串。

>>> oct(10)
'0o12'
>>> oct(20)
'0o24'
>>> oct(15)
'0o17'
```

### 3.15  ASCII函数ord()

ord() 函数是 chr() 函数（对于8位的ASCII字符串）或 unichr() 函数（对于Unicode对象）的配对函数，它以一个字符（长度为1的字符串）作为参数，返回对应的 ASCII 数值，或者 Unicode 数值，如果所给的 Unicode 字符超出了你的 Python 定义范围，则会引发一个 TypeError 的异常。

```python
ord(c)
# c -- 字符。
# 返回值是对应的十进制整数。

>>>ord('a')
97
>>> ord('b')
98
>>> ord('c')
99
```

### 3.16 集合函数set()

创建一个无序不重复元素集，可进行关系测试，删除重复数据，还可以计算交集、差集、并集等。

```python
class set([iterable])
# iterable -- 可迭代对象对象；
# 返回新的集合对象。

>>>x = set('runoob')
>>> y = set('google')
>>> x, y
(set(['b', 'r', 'u', 'o', 'n']), set(['e', 'o', 'g', 'l']))   # 重复的被删除
>>> x & y         # 交集
set(['o'])
>>> x | y         # 并集
set(['b', 'e', 'g', 'l', 'o', 'n', 'r', 'u'])
>>> x - y         # 差集
set(['r', 'b', 'u', 'n'])
>>>
```

### 3.17 字符串函数str()

将对象转化为适于人阅读的形式。

```python
class str(object='')
# object -- 对象。
# 返回一个对象的string格式。

>>>s = 'RUNOOB'
>>> str(s)
'RUNOOB'
>>> dict = {'runoob': 'runoob.com', 'google': 'google.com'};
>>> str(dict)
"{'google': 'google.com', 'runoob': 'runoob.com'}"
>>>
```

### 3.18 元组函数tuple()

将列表转换为元组。

```python
tuple( iterable )
# iterable -- 要转换为元组的可迭代序列。
# 返回元组。

>>>tuple([1,2,3,4])
(1, 2, 3, 4)
>>> tuple({1:2,3:4})    #针对字典 会返回字典的key组成的tuple
(1, 3)
>>> tuple((1,2,3,4))    #元组会返回元组自身
(1, 2, 3, 4)
```

## 4. 迭代循环函数

### 4.1 调用函数callable()

用于检查一个对象是否是可调用的。如果返回 True，object 仍然可能调用失败；但如果返回 False，调用对象 object 绝对不会成功。

对于函数、方法、lambda 函式、 类以及实现了 **__call__** 方法的类实例, 它都返回 True。

```python
callable(object)
# object -- 对象
# 可调用返回 True，否则返回 False。

>>>callable(0)
False
>>> callable("runoob")
False

>>> def add(a, b):
...     return a + b
... 
>>> callable(add)             # 函数返回 True
True
```

### 4.2 可遍历函数enumate()

用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

```python
enumerate(sequence, [start=0])
# sequence -- 一个序列、迭代器或其他支持迭代对象。
# start -- 下标起始位置。

>>>seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))       # 下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

### 4.3 迭代器函数iter()

用来生成迭代器。

```python
iter(object[, sentinel])
# object -- 支持迭代的集合对象。
# sentinel -- 如果传递了第二个参数，则参数 object 必须是一个可调用的对象（如，函数），此时，iter 创建了一个迭代器对象，每次调用这个迭代器对象的__next__()方法时，都会调用 object。

>>>lst = [1, 2, 3]
>>> for i in iter(lst):
...     print(i)
... 
1
2
3
```

### 4.4 生成列表函数range()

可创建一个整数列表，一般用在 for 循环中。

```python
range(start, stop[, step])
# start: 计数从 start 开始。默认是从 0 开始。例如range（5）等价于range（0， 5）;
# stop: 计数到 stop 结束，但不包括 stop。例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5
# step：步长，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)

>>>range(10)        # 从 0 开始到 10
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> range(1, 11)     # 从 1 开始到 11
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> range(0, 30, 5)  # 步长为 5
[0, 5, 10, 15, 20, 25]
>>> range(0, 10, 3)  # 步长为 3
[0, 3, 6, 9]
>>> range(0, -10, -1) # 负数
[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
>>> range(0)
[]
>>> range(1, 0)
[]
```

### 4.5 迭代器下一个函数next()

 返回迭代器的下一个项目。

```python
next(iterable[, default])
# iterable -- 可迭代对象
# default -- 可选，用于设置在没有下一个元素时返回该默认值，如果不设置，又没有下一个元素则会触发 StopIteration 异常。

>>> it = iter([1, 2, 3, 4, 5])
>>> while True:
...     try:
...         # 获得下一个值:
...         x = next(it)
...         print(x)
...     except StopIteration:
...         # 遇到StopIteration就退出循环
...         break
...
1
2
3
4
5
```

## 5. 类函数

### 4.1 类方法函数classmethod()

对应的函数不需要实例化，不需要 self 参数，但第一个参数需要是表示自身类的 cls 参数，可以来调用类的属性，类的方法，实例化对象等。

```python
class A(object):
    bar = 1
    def func1(self):  
        print ('foo') 
    @classmethod  # 类方法函数
    def func2(cls):
        print ('func2')
        print (cls.bar)
        cls().func1()   # 调用 foo 方法
 
A.func2()               # 不需要实例化
```

### 4.2 删除属性函数delattr()

用于删除属性。

**delattr(x, 'foobar')** 相等于 **del x.foobar**

```python
delattr(object, name)
# object -- 对象。
# name -- 必须是对象的属性。


>>> class Coordinate:
...     x = 10
...     y = -5
...     z = 0
...
>>> point1 = Coordinate()
>>>
>>> print('x = ',point1.x)
x =  10
>>> print('y = ',point1.y)
y =  -5
>>> print('z = ',point1.z)
z =  0
>>>
>>> delattr(Coordinate, 'z')
>>>
>>> print('--删除 z 属性后--')
--删除 z 属性后--
>>> print('x = ',point1.x)
x =  10
>>> print('y = ',point1.y)
y =  -5
>>>
>>> # 触发错误
>>> print('z = ',point1.z)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Coordinate' object has no attribute 'z'
```

### 4.3 获取属性函数getattr()

用于返回一个对象属性值。

```python
getattr(object, name[, default])
# object -- 对象。
# name -- 字符串，对象属性。
# default -- 默认返回值，如果不提供该参数，在没有对应属性时，将触发 AttributeError。

>>>class A(object):
...     bar = 1
... 
>>> a = A()
>>> getattr(a, 'bar')        # 获取属性 bar 值
1
>>> getattr(a, 'bar2')       # 属性 bar2 不存在，触发异常
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'A' object has no attribute 'bar2'
>>> getattr(a, 'bar2', 3)    # 属性 bar2 不存在，但设置了默认值
3
```

### 4.4 属性判断函数hasattr()

用于判断对象是否包含对应的属性。

```python
hasattr(object, name)

# object -- 对象。
# name -- 字符串，属性名。

>>> class Coordinate:
...     x = 10
...     y = -5
...     z = 0
...
>>> point1 = Coordinate()
>>> print(hasattr(point1, 'x'))
True
>>> print(hasattr(point1, 'y'))
True
>>> print(hasattr(point1, 'z'))
True
>>> print(hasattr(point1, 'no'))  # 没有该属性
False
```

### 4.5 类判断函数isinstance()

判断一个对象是否是一个已知的类型，类似 type()。

- type() 不会认为子类是一种父类类型，不考虑继承关系。
- isinstance() 会认为子类是一种父类类型，考虑继承关系。

如果要判断两个类型是否相同推荐使用 isinstance()。

```python
isinstance(object, classinfo)

# object -- 实例对象。
# classinfo -- 可以是直接或间接类名、基本类型或者由它们组成的元组。
# 如果对象的类型与参数二的类型（classinfo）相同则返回 True，否则返回 False。

>>>a = 2
>>> isinstance (a,int)
True
>>> isinstance (a,str)
False
>>> isinstance (a,(str,int,list))    # 是元组中的一个返回 True
True

# isinstance与type
>>> class A:
...     pass
...
>>> class B(A):
...     pass
...
>>> isinstance(A(), A)    # returns True
True
>>> type(A()) == A        # returns True
True
>>> isinstance(B(), A)    # returns True
True
>>> type(B()) == A        # returns False
False
```

### 4.6 子类判断函数issubclass()

用于判断参数 class 是否是类型参数 classinfo 的子类。

```python
issubclass(class, classinfo)

# class -- 类。
# classinfo -- 类。

>>> class A:
...     pass
...
>>> class B(A):
...     pass
...
>>> print(issubclass(B,A))
True
```

### 4.7 基础类函数object()

Python基础类。

### 4.8 返回属性函数property()

在新式类中返回属性值

```python
class property([fget[, fset[, fdel[, doc]]]])
# fget -- 获取属性值的函数
# fset -- 设置属性值的函数
# fdel -- 删除属性值函数
# doc -- 属性描述信息

class Parrot(object):
    def __init__(self):
        self._voltage = 100000
 
    @property
    def voltage(self):
        """Get the current voltage."""
        return self._voltage
```

### 4.8 可读类输函数repr()

将对象转化为供解释器读取的形式。

```python
# repr(object)
# object -- 对象。
# 返回一个对象的 string 格式。

>>>s = 'RUNOOB'
>>> repr(s)
"'RUNOOB'"
>>> dict = {'runoob': 'runoob.com', 'google': 'google.com'};
>>> repr(dict)
"{'google': 'google.com', 'runoob': 'runoob.com'}"
```

### 4.9 设置属性函数setattr()

对应函数 getattr()，用于设置属性值，该属性不一定是存在的

```python
setattr(object, name, value)
# object -- 对象。
# name -- 字符串，对象属性。
# >>>class A(object):

...     bar = 1
... 
>>> a = A()
>>> getattr(a, 'bar')          # 获取属性 bar 值
1
>>> setattr(a, 'bar', 5)       # 设置属性 bar 值
>>> a.bar
5value -- 属性值。

```

### 4.10 静态方法函数staticmethod()

返回函数的静态方法。

```python
class C(object):
    @staticmethod
    def f(arg1, arg2, ...):
        ...
staticmethod(function)

class C(object):
    @staticmethod
    def f():
        print('runoob');
 
>>> class C(object):
...     @staticmethod
...     def f():
...         print('runoob');
...
>>> C.f();          # 静态方法无需实例化
runoob
>>> cobj = C()
>>> cobj.f()        # 也可以实例化后调用
runoob
```

### 4.11 父类函数super()

用于调用父类(超类)的一个方法。

解决多重继承问题的，直接用类名调用父类方法在使用单继承的时候没问题，但是如果使用多继承，会涉及到查找顺序（MRO）、重复调用（钻石继承）等种种问题。

```python
super(type[, object-or-type])

# type -- 类。
# object-or-type -- 类，一般是 self

>>> class A:
...      def add(self, x):
...          y = x+1
...          print(y)
...
>>> class B(A):
...     def add(self, x):
...         super().add(x)
...
>>> b = B()
>>> b.add(2)  # 3
3
```

### 4.12 返回类型函数type()

如果你只有第一个参数则返回对象的类型，三个参数返回新的类型对象

```python
type(object)
type(name, bases, dict)

# name -- 类的名称。
# bases -- 基类的元组。
# dict -- 字典，类内定义的命名空间变量。

# 一个参数实例
>>> type(1)
<type 'int'>
>>> type('runoob')
<type 'str'>
>>> type([2])
<type 'list'>
>>> type({0:'zero'})
<type 'dict'>
>>> x = 1          
>>> type( x ) == int    # 判断类型是否相等
True
 
# 三个参数
>>> class X(object):
...     a = 1
...
>>> X = type('X', (object,), dict(a=1))  # 产生一个新的类型 X
>>> X
<class '__main__.X'>
```

###  4.13 类字典函数vars()

返回对象object的属性和属性值的字典对象。

```python
vars([object])
# object -- 对象
# 返回对象object的属性和属性值的字典对象，如果没有参数，就打印当前调用位置的属性和属性值 类似 locals()。

>>>print(vars())
{'__builtins__': <module '__builtin__' (built-in)>, '__name__': '__main__', '__doc__': None, '__package__': None}
>>> class Runoob:
...     a = 1
... 
>>> print(vars(Runoob))
{'a': 1, '__module__': '__main__', '__doc__': None}
>>> runoob = Runoob()
>>> print(vars(runoob))
{}
```

## 5. 文件函数

### 5.1 dir()

不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。如果参数包含方法__dir__()，该方法将被调用。如果参数不包含__dir__()，该方法将最大限度地收集参数信息。

```python
dir([object])
# object -- 对象、变量、类型。

>>>dir()   #  获得当前模块的属性列表
['__builtins__', '__doc__', '__name__', '__package__', 'arr', 'myslice']
>>> dir([ ])    # 查看列表的方法
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__delslice__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getslice__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__setslice__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

### 5.2 执行文件函数execfile()

用来执行一个文件

```python
execfile(filename[, globals[, locals]])
# filename -- 文件名。
# globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
# locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。

# hello.py
print('hello world!');

>>>execfile('hello.py')
hello world!
```

### 5.3 文件函数file()

创建一个 file 对象，它有一个别名叫 [open()](https://www.runoob.com/python/pytho-func-open.html)，更形象一些，它们是内置函数。参数是以字符串的形式传递的。

```python
file(name[, mode[, buffering]])

# name -- 文件名
# mode -- 打开模式
# buffering -- 0 表示不缓冲,如果为 1 表示进行行缓冲，大于 1 为缓冲区大小。

>>>f = file('test.txt')
>>> f.read()
'RUNOOB1\nRUNOOB2\n'
```

### 5.4 文件操作函数open()

用于打开一个文件，创建一个 **file** 对象，相关的方法才可以调用它进行读写。

```python
open(name[, mode[, buffering]])

# name : 一个包含了你要访问的文件名称的字符串值。
# mode : mode 决定了打开文件的模式：只读，写入，追加等。所有可取值见如下的完全列表。这个参数是非强制的，默认文件访问模式为只读(r)。
# buffering : 如果 buffering 的值被设为 0，就不会有寄存。如果 buffering 的值取 1，访问文件时会寄存行。如果将 buffering 的值设为大于 1 的整数，表明了这就是的寄存区的缓冲大小。如果取负值，寄存区的缓冲大小则为系统默认。

>>>f = open('test.txt')
>>> f.read()
'RUNOOB1\nRUNOOB2\n'
```

## 6. 输入输出函数

### 6.1 字符串格式输出函数format()

一种格式化字符串的函数，增强了字符串格式化的功能。

```python
 str.format()
 
 >>>"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
'hello world'
>>> "{0} {1}".format("hello", "world")  # 设置指定位置
'hello world'
>>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置
'world hello world'
```

### 6.2 输入函数input()

接受一个标准输入数据，返回为 string 类型。

```python
input([prompt])
# prompt: 提示信息

>>> a = input("intput:")
intput:123
>>> type(a)
<class 'str'>
```

### 6.3 输出函数print()

用于打印输出，最常见的一个函数。

在 Python3.3 版增加了 flush 关键字参数。

*print 在 Python3.x 是一个函数，但在 Python2.x 版本不是一个函数，只是一个关键字。*

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)

# objects -- 复数，表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。
# sep -- 用来间隔多个对象，默认值是一个空格。
# end -- 用来设定以什么结尾。默认值是换行符 \n，我们可以换成其他字符串。
# file -- 要写入的文件对象。
# flush -- 输出是否被缓存通常决定于 file，但如果 flush 关键字参数为 True，流会被强制刷新。

>>> print("www", "runoob", "com", sep=".")  # 设置间隔符
www.runoob.com
```

## 7.与 函数操作相关函数

### 7.1 模块载入函数reload()

重新载入之前载入的模块。

```python
reload(module)
# module -- 模块对象。

>>>import sys
>>> sys.getdefaultencoding()            # 当前默认编码
'ascii'
>>> reload(sys)                         # 使用 reload
<module 'sys' (built-in)>
>>> sys.setdefaultencoding('utf8')      # 设置编码
>>> sys.getdefaultencoding()
'utf8'
```

### 7.2 模块加载函数\_\_import\_\_()

用于动态加载类和函数。

```python
__import__(name[, globals[, locals[, fromlist[, level]]]])
# name -- 模块名


>>> import os
>>> print ('在 a.py 文件中 %s' % id(os))
在 a.py 文件中 1690711523960

>>> import sys  
>>> __import__('a')        # 导入 a.py 模块，没有模块则跑操场异常
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'a'
```

## 参考

- [01-runoob-Python 内置函数-菜鸟教程](https://www.runoob.com/python/python-built-in-functions.html)

