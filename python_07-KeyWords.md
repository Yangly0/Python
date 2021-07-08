---
@Author: liuyangly1
@Date  : 2021-07-08 13:40:52
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 关键字

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

| 关键字   | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| and      | 用于表达式运算，逻辑与操作                                   |
| as       | 用于类型转换                                                 |
| assert   | 断言，用于判断变量或条件表达式的值是否为真                   |
| break    | 中断循环语句的执行                                           |
| class    | 用于定义类                                                   |
| continue | 继续执行下一次循环                                           |
| def      | 用于定义函数或方法                                           |
| del      | 删除变量或者序列的值                                         |
| elif     | 条件语句 与if else 结合使用                                  |
| else     | 条件语句条件语句，与if,elif结合使用。也可以用于异常和循环使用 |
| except   | 包括捕获异常后的操作代码，与try，finally结合使用             |
| exec     | 用于执行python语句                                           |
| for      | 循环语句                                                     |
| finally  | 用于异常语句，出现异常后，始终要执行finally包含的代码块。与try,except结合使用 |
| from     | 用于导入模块，与import结合使用                               |
| global   | 定义全局变量                                                 |
| if       | 条件语句，与else，elif结合使用                               |
| import   | 用于导入模块，与from 结合使用                                |
| in       | 判断变量是否存在序列中                                       |
| is       | 判断变量是否为某个类的实例                                   |
| lambda   | 定义匿名函数                                                 |
| not      | 用于表达式运算，逻辑非操作                                   |
| or       | 用于表达式运算，逻辑或操作                                   |
| pass     | 空的类，函数，方法的占位符                                   |
| print    | 打印语句                                                     |
| raise    | 异常抛出操作                                                 |
| return   | 用于从函数返回计算结果                                       |
| try      | 包含可能会出现异常的语句，与except，finally结合使用          |
| while    | 循环语句                                                     |
| with     | 简化Python的语句                                             |
| yield    | 用于从函数依次返回值                                         |

## 1. 布尔关键字

False代表假，值为0；True代表真，值为1；


```python
>>> True == 1
True
>>> False == 0
True
>>> isinstance(True, object)
True
>>> isinstance(False, object)
True
>>> isinstance(False, int)
True
>>> isinstance(True, int)
True
```

注意：False、True、None本质都是object对象，False、True属于int对象。

## 2. 控制流关键字

- 语法

```python
if...elif...else...:条件判断；
for...in...:对可迭代对象循环遍历
for...in...else...:遍历正常完成则执行else后的代码；
continue:终止本次循环，继续下一次循环；
break：跳出循环；
while：循环结构；
```
注意：详细使用，可以见python之06三大流程中循环内容。

## 3. 逻辑判断关键字

- 语法


```python
and:表示与
or：表示或；
not：表示非；
in：判断元素是否在容器内；
not in：判断元素是否不再容器内；
is:比较两个变量的内存地址；
```

扩展：is关键字比较两个变量的内存地址，==比较两个变量的值；

```python
>>> x = [123]
>>> y = [123]
>>> x is y
False
>>> x == y
True
```

注意：详细使用，可以见python之05运算符中逻辑运算符内容。

## 4. 异常关键字

- 语法

```python
try:
	代码1，正常执行块
except A:
	代码2，异常A会执行这里
except B:
    代码2，异常B会执行这里
except:
    代码2，其他异常会执行这里
else：
	代码3，无异常则执行
finally：
	代码4，# 注意，无论正常与否都要执行代码4.

raise：主动触发异常；
```

注意：详细使用，可以见python之10异常处理。

- demo：文件打开异常处理

```python
>>> try:
...     f = open('1.txt','r')
...     try:
...         context = f.write('abc')
...         print(context)
...     except:
...         raise("错误，文件写入出现异常")
...     finally:
...         f.close()
...         print('关闭打开的文件')
... except Exception as e:
...     print(e)
...
关闭打开的文件
exceptions must derive from BaseException
```



## 5. 命令空间关键字

```python
global:将模块空间变量引入到局部空间修改；
nonlocal:将本局部空间的外层空间变量引入到本层局部空间修改，用来嵌套函数内；
```

注意：详细使用，可以见python之8函数中变量空间。

## 6. 匿名函数关键字

没有名称的内联函数

- 语法

```python
lambda [arg1 [, agr2,.....argn]] : expression
```

- lambda与map

```python
>>> x = [1, 2, 3]
>>> y = [1, 2, 3]
>>> list(map(lambda x, y : x*y, x, y))
[1, 4, 9]
```

- lambda与filter

```python
>>> x = [1, 2, 3]
>>> list(filter(lambda x:x%2==0, x))
[2]
```

- lambda与sort

```python
>>> x = [
...     {'name':1, 'date':1999},
...     {'name':2, 'date':2000},
...     {'name':3, 'date':2020},
... ]
>>> x.sort(reverse=True, key=lambda elem: elem["date"])
>>> x
[{'name': 3, 'date': 2020}, {'name': 2, 'date': 2000}, {'name': 1, 'date': 1999}]
```

- lambda与max, min

```python
# max(a, b, c, …[, key=func]) -> value
# min(a, b, c, …[, key=func]) -> value

# 字典按值排序
>>> x = {'a':1, 'b':2, 'c':3}
>>> max(x.items(),key=lambda k:k[1])
('c', 3)

# 注意混合数据：
# 默认情况下，max将通过第一个索引比较项目，如果第一个索引是相同的，那么它会比较第二个索引。
>>> x = ['1','100','111','2', 2, 2.57]
>>> max(x, key=lambda i:int(i))
'111'

# 推荐
# max(x, key=int)
# min(x, key=int)
>>> x = ['1','100','111','2', 2, 2.57]
>>> max(x, key=int)
'111'
>>> min(x, key=int)
'1'
```

- lambda与reduce：reduce函数是python中的一个二元内建函数，它可以通过传给reduce中的函数（必须是二元函数）依次对数据集中的数据进行操作.

```python
>>> from functools import reduce
>>> a = [2,22,222]
>>> reduce(lambda x,y:x+y,a)
246
```

- lambda与深度学习

```python
 net_h1 = BatchNormLayer(net_h1, 
						 act=lambda x: tl.act.lrelu(x, 0.2),
                         is_train=is_train, 
						 name='h1/batchnorm')
```

- lambda与列表表达式：**lambda表达式不会形成对函数体内变量的记忆，只记录最后一个状态。**

```python
>>> y = [lambda :x for x in range(10)]
>>> y  # 9个lambda无参函数lambda :x，每个都会调用x，但是x已经等于9了，所以每次调用都等于9
[<function <listcomp>.<lambda> at 0x000001EDF0D275E8>, <function <listcomp>.<lambda> at 0x000001EDF0D27708>, <function <listcomp>.<lambda> at 0x000001EDF0D274C8>, <function <listcomp>.<lambda> at 0x000001EDF0D04678>, <function <listcomp>.<lambda> at 0x000001EDF0D041F8>, <function <listcomp>.<lambda> at 0x000001EDF0D04168>, <function <listcomp>.<lambda> at 0x000001EDF0D040D8>, <function <listcomp>.<lambda> at 0x000001EDF0D04048>, <function <listcomp>.<lambda> at 0x000001EDF0D04828>, <function <listcomp>.<lambda> at 0x000001EDF0D04318>]
>>> y[0]()  # ()表示调用lambda函数
9
>>> y[1]()
9

>>> y = [lambda x :x for x in range(10)]
>>> y # 9个lambda相同的有参x函数 lambda x:x，输入x，则调用
[<function <listcomp>.<lambda> at 0x000001EDF0D273A8>, <function <listcomp>.<lambda> at 0x000001EDF0D59678>, <function <listcomp>.<lambda> at 0x000001EDF0D59708>, <function <listcomp>.<lambda> at 0x000001EDF0D59798>, <function <listcomp>.<lambda> at 0x000001EDF0D59828>, <function <listcomp>.<lambda> at 0x000001EDF0D598B8>, <function <listcomp>.<lambda> at 0x000001EDF0D59948>, <function <listcomp>.<lambda> at 0x000001EDF0D599D8>, <function <listcomp>.<lambda> at 0x000001EDF0D59A68>, <function <listcomp>.<lambda> at 0x000001EDF0D59AF8>]
>>> y[0](0) 
0 
>>> y[1](0)
0
>>> y[1](5)
5
```

## 7. 断言关键字

用于判断一个表达式，在表达式条件为 false 的时候触发异常。

- 语法

```python
assert expression [, arguments]
```

- demo：判断变量是否相等，文件是否存在

```python
>>> x = 1
>>> assert x == 1
>>> assert x == 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError

>>> import os
>>> assert os.path.exists("1.txt")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError
```

## 8.None关键字

None：代表空，是python解释器的一个内置的关键字变量，本质是一个object()，类似于C++的NULL。

```python
# None关键字
>>> isinstance(None, object)
True
# 注意None 不等于 0
>>> None == 0
False
```

## 9. 函数与模块关键字

```python
from ... import ... #  从模块导入函数
import ...   # 导入模块
import ... as  # 导入模块为什么操作名
return  # 函数返回
pass  # 跳过函数或跳过后续流程，可以用来调试bug等
```

注意，详细使用，可以见python之8函数与模块。

## 10. 其他


```python
yield：生成器关键字； 详细使用，可以见python之生成器
del：从上下文堆栈中删除某个对象。
```

## 参考

- [1] [天宇之游-python基础之常用关键字总结-cnblogs](https://www.cnblogs.com/cwp-bg/p/9830228.html)