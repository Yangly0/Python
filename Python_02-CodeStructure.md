---
@Author: liuyangly1
@Date  : 2021-07-07 19:16:25
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 代码结构

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 交互式编程和脚本式编程
- 交互式编程不需要创建脚本文件，是通过 Python 解释器的交互模式进来编写代码。
- 通过脚本参数调用解释器开始执行脚本，直到脚本执行完毕。当脚本执行完成后，解释器不再有效。

## 2. 代码结构

```python
#!/usr/bin/env/python
# -*- encoding: utf-8 -*-
"""
#############################################################################
@File              :   code_structure.py
@Time              :   2021/04/25 14:18:23
@Author            :   liuyangly1
@Email             :   522927317@qq.com
@Desc              :   代码结构
#############################################################################
"""


# Built-in modules
import os
import sys
import argparse

# Third-party modules
# import numpy as np

# Customized Modules
# import tooltik 


def Function(variable1, variable):
    r"""Overview

    Description

    Args:
        variable (type): introduction

    Returns:
        variable (type): introduction

    .. warning::
        context

    .. note::
        context

    Example::
        >>> model = class()
    """
    pass


def parse_args():
    parser = argparse.ArgumentParser(description="Demo")
    parser.add_argument("--path", type=str, default=".", help="Project Path")
    return parser.parse_args()


def main():
    args = parse_args()
    pass


if __name__ == "__main__":
    main()

```



## 2. 标识符
- 标识符由字母、数字、下划线组成。
- 所有标识符可以包括英文、数字以及下划线(_)，但不能以数字开头。
- 以下划线开头的标识符是有特殊意义的。以单下划线开头 _foo 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 from xxx import * 而导入。
- 以双下划线开头的 __foo 代表类的私有成员，以双下划线开头和结尾的 __foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数。

- Python 可以同一行显示多条语句，方法是用分号 ; 分开。

## 3. 保留字符

- Python 的关键字只包含小写字母。

| and      | exec    | not    |
| -------- | ------- | ------ |
| assert   | finally | or     |
| break    | for     | pass   |
| class    | from    | print  |
| continue | global  | raise  |
| def      | if      | return |
| del      | import  | try    |
| elif     | in      | while  |
| else     | is      | with   |
| except   | lambda  | yield  |

## 4. 行和缩进

- Python 的代码块不使用大括号 {} 来控制类，函数以及其他逻辑判断。python 最具特色的就是用缩进来写模块。

- 缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量，这个必须严格执行。

## 5. 多行语句
- 一般以新行作为语句的结束符。
- 使用斜杠（ \）将一行的语句分为多行显示。

## 6. 引号
- 使用引号( ' )、双引号( " )、三引号( ''' 或 """ ) 来表示字符串，引号的开始与结束必须是相同类型的。
- 三引号可以由多行组成，编写多行文本的快捷语法，常用于文档字符串，在文件的特定地点，被当做注释。

## 7. 注释
- 单行注释采用 # 开头。
- 多行注释使用三个单引号(''')或三个双引号(""")。

## 8. 空行
- 函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。

- 空行与代码缩进不同，空行并不是Python语法的一部分。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

- 记住：空行也是程序代码的一部分。
## 9. 用户输入

```python
>>> input("按下 enter 键退出，其他任意键显示...\n")
按下 enter 键退出，其他任意键显示...
Hello, world!
'Hello, world!'
```

## 10. 同一行显示多条语句
- Python可以在同一行中使用多条语句，语句之间使用分号(;)分割。

## 11. print 输出

- print 默认输出是换行的，如果要实现不换行需要在变量末尾加上逗号 ,。

## 12. 多个语句构成代码组
- 缩进相同的一组语句构成一个代码块，我们称之代码组。
- 像if、while、def和class这样的复合语句，首行以关键字开始，以冒号( : )结束，该行之后的一行或多行代码构成代码组。

## 13. 命令行参数
- Python 可以使用 -h 参数查看各参数帮助信息。
```bash
$ python -h 
usage: python [option] ... [-c cmd | -m mod | file | -] [arg] ... 
Options and arguments (and corresponding environment variables): 
-c cmd : program passed in as string (terminates option list) 
-d     : debug output from parser (also PYTHONDEBUG=x) 
-E     : ignore environment variables (such as PYTHONPATH) 
-h     : print this help message and exit 
 
[ etc. ] 
```

## 参考

- [1] [runoob-Python 基础语法-菜鸟教程](https://www.runoob.com/python/python-basic-syntax.html)

