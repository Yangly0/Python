---
@Author: liuyangly1
@Date  : 2021-07-07 21:06:01
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 代码规范

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 程序

### 1.1 编码

- 程序一律使用 UTF-8 编码，在代码开头加入编码声明。
```python
# -*- encoding: utf-8 -*-
```

### 1.2 代码格式

#### 1.2.1 缩进
- 统一使用 4 个空格进行缩进。
- 默认设置tab为4个空格。
```python
for i in range(5):
	print(i)
```

#### 1.2.2 行宽
- 每行代码尽量不超过 80 个字符(在特殊情况下可以略微超过 80 ，但最长不得超过 120)。
- 理由：
    - 这在查看 side-by-side 的 diff 时很有帮助。
    - 方便在控制台下查看代码。
    - 太长可能是设计有缺陷。
 - 实现：
 	- \，反斜杠后不能用空格或者其他符号。
```python
>>> a = 111111 + \
...       2222
>>> a
113333
```

#### 1.2.3 引号
- 自然语言使用双引号，机器标示使用单引号，因此代码里多数应该使用单引号。
- 自然语言使用双引号 "..."，例如错误信息；很多情况还是 unicode，使用u"你好世界"。
- 机器标识 使用单引号 '...'， 例如 dict 里的 key。
- 正则表达式使用原生的双引号 r"..."。
- 文档字符串 (docstring) 使用三个双引号 """......"""。

```python
"""文档说明"""      # 文档注释
print("你好！")     # 自然语言
x = {'x':1, 'y':2}  # 机器标识 
```

#### 1.2.4 空行
- 模块级函数和类定义之间空两行。
- 类成员函数之间空一行。
```python
class A:

    def __init__(self):
        pass

    def method(self):
        pass


def main():
    pass   
```

### 1.3 模块
- 分行书写。
- import 绝对路径。
- 放在文件头部，置于模块说明及docstring之后，于全局变量之前。
- 按照顺序排列，每组之间用一个空行分隔。
- 导入其他模块的类定义时，可以使用相对导入。
- 如果发生命名冲突，则可使用命名空间。
```python
# 内置模块
import os
import sys
# 三方模块
import numpy as np
# 自定义模块
import tooltik 
```
### 1.4 空格
- 在二元运算符两边各空一格[=,-,+=,==,>,in,is not, and]。
- 函数的参数列表中，之后要有空格。
- 函数的参数列表中，默认值等号两边不要添加空格。
- 左括号之后，右括号之前不要加多余的空格。
- 字典对象的左括号之前不要多余的空格。
- 不要为对齐赋值语句而使用的额外空格。
```python
x = 1 + 2
def function(arg1, arg2=1):
	return arg1 + arg2
y = (1 + 2)
z = {'x':1, 'y':2}
```

### 1.5 换行
- 第二行缩进到括号的起始处。
```python
fun = function(arg1, arg2,
               arg3, arg4)
```
- 第二行缩进 4 个空格，适用于起始括号就换行的情形。
```python
def function(
        arg1, arg2, 
        arg3, arg4):
    pass
```
- 使用反斜杠\换行，二元运算符+,-等应出现在行末；长字符串也可以用此法换行。
```python
x = 111111 + \
	222222
	
print('Hello, '\
      '%s %s!' %\
      ('L', 'Y'))
```
- 禁止复合语句，即一行中包含多个语句。
```python
# fun1();fun2();fun3()
fun1()
fun2()
fun3()
```
- if/for/while 一定要换行。
```python
# if flag == '1': pass
if flag == '1':
    pass
```

## 2. 注释

### 2.1 代码注释
#### 2.1.1 块注释
- “#”号后空一格，段落间用空行分开（同样需要“#”号）。
```python
# 块注释
# 块注释
# (注释段落，同样需要“#”)
# 块注释
# 块注释
```
#### 2.1.2 行注释
- 至少使用两个空格和语句分开，注意不要使用无意义的注释。
```python
# x = x + 1  # x加1
x = x + 1  # 向右移动1
```
#### 2.1.3 建议
- 在代码的关键部分(或比较复杂的地方), 能写注释的要尽量写注释。
- 比较重要的注释段, 使用多个等号隔开, 可以更加醒目, 突出重要性。
```python
def main():
	pass
# =====================================
# 建议内容
# =====================================

if __name__ == '__main__':
    main()
```

### 2.2 文档注释（Docstring）

- 作为文档的Docstring一般出现在模块头部、函数和类的头部，这样在python中可以通过对象的__doc__对象获取文档，
编辑器和IDE也可以根据Docstring给出自动提示。
- 文档注释以"""开头和结尾, 首行不换行, 如有多行, 末行必需换行, 以下是Google的docstring风格示例。

```python
# -*- coding: utf-8 -*-
"""Example docstrings.

This module demonstrates documentation as specified by the `Google Python
Style Guide`_. Docstrings may extend over multiple lines. Sections are created
with a section header and a colon followed by a block of indented text.

Example:
    Examples can be given using either the ``Example`` or ``Examples``
    sections. Sections support any reStructuredText formatting, including
    literal blocks::

        $ python example_google.py

Section breaks are created by resuming unindented text. Section breaks
are also implicitly created anytime a new section starts.
"""
```
- 不要在文档注释复制函数定义原型, 而是具体描述其具体内容, 解释具体参数和返回值等。

```python
def function(a, b):
    # """function(a, b) -> list"""
    """计算并返回a到b范围内数据的平均值"""
    pass
```
- 对函数参数、返回值等的说明采用numpy标准。

```python
def func(arg1, arg2):
    """在这里写函数的一句话总结(如: 计算平均值).

    这里是具体描述.

    参数
    ----------
    arg1 : int
        arg1的具体描述
    arg2 : int
        arg2的具体描述

    返回值
    -------
    int
        返回值的具体描述

    参看
    --------
    otherfunc : 其它关联函数等...

    示例
    --------
    示例使用doctest格式, 在`>>>`后的代码可以被文档测试工具作为测试用例自动运行

    >>> a=[1,2,3]
    >>> print [x + 3 for x in a]
    [4, 5, 6]
    """
```
- 文档注释不限于中英文, 但不要中英文混用。
- 文档注释不是越长越好, 通常一两句话能把情况说清楚即可。
- 模块、公有类、公有方法, 能写文档注释的, 应该尽量写文档注释。



## 3. 命名
### 3.1 模块
1. 模块推荐使用小写命名。
2. 除非有很多字母，尽量不要用下划线。

- 因为很多模块文件存与模块名称一致的类，模块采用小写，类采用首字母大写，这样就能区分开模块和类。
```python
# import Decoder
import decoder
import html_parser
```

### 3.2 类
1. 类名使用驼峰(CamelCase)命名风格，首字母大写。
2. 私有类可用一个下划线开头。
```python
class Class():
    pass

class SubClass(Class):
    pass

class _SubClass(Class):
    pass
```

### 3.3 函数
1. 函数名一律小写，如有多个单词，用下划线隔开。
2. 类内部函数命名，用单下划线(_)开头（该函数可被继承访问）。
3. 类内私有函数命名，用双下划线(__)开头（该函数不可被继承访问）。

```python
def fun():
    pass

def get_value():
    pass

class Class():

    def _private_func():
        pass
```


### 3.4 变量
1. 变量名推荐小写，如有多个单词，用下划线隔开。
2. 类内部变量命名，用单下划线(_)开头（该变量可被继承访问）。
3. 类内私有变量命名，用双下划线(__)开头（该变量不可被继承访问）。
```python
num = 0
name = ''
```

### 3.5 常量
- 使用下划线分割大些字母命名。
```python
MAX_CLIENT = 100
MAX_CONNECTION = 1000
CONNECTION_TIMEOUT = 600
```

## 参考
- [1] [GitHubClub-Python 代码规范-简书](https://www.jianshu.com/p/8b6c425b65a6)

