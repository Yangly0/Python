---
@Author: liuyangly1
@Date  : 2021-07-08 15:53:41
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 函数

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

函数是一段具有特点功能的、可重用的语句组，目的是封装一个重复的功能。

## 1. 函数：定义与调用

- 定义

```python
# 函数的说明文档通常位于函数内部、所有代码的最前面。
def 函数名(参数列表):
    '''
    函数文档
    '''
    //实现特定功能的多行代码
    [return [返回值]]
```

- 调用

```python
[返回值] = 函数名([形参值])
```



## 2.  函数：参数

### 2.1 位置参数

实参和形参位置必须一致。问题：抛出 TypeError异常和产生的结果和预期不符。

- 语法

```python
def 函数名(形参名1，形参名2)：
    代码块
#当调用的时候必须有两个参数，否则会提示错误
函数名(实参1, 实参2)
```

- demo：实参与形参位置不等

```python
>>> def f(x, y):
...     return x+y
...
>>> f(1, 2)
3
>>> f(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: f() missing 1 required positional argument: 'y'
```

### 2.2 关键字参数

关键字参数是指使用形式参数的名字来确定输入的参数值。通过此方式指定函数实参时，不再需要与形参的位置完全一致，只要将参数名写正确即可。

- 语法

```python
def 函数名(形参名1，形参名2)：
    代码块
#当调用的时候必须有两个参数，否则会提示错误
函数名(形参名2 = 实参1, 形参名1 = 实参2)
```

- demo：关键字参数调用函数

```python
>>> def f(x, y):
...     return x + 2*y
...
>>> f(y=2, x=1)
5
```

### 2.3 默认参数

当定义一个有默认值参数的函数时，有默认值的参数必须位于所有没默认值参数的后面。

- 语法

```python
def 函数名(形参名1，形参名2=默认值)：
    代码块
函数名(实参1)
```
- demo：默认参数

```python
>>> def f(x, y=2):
...     return x + 2*y
...
>>> f(1)
5
```

### 2.4 可变参数

- 语法

```python
# *args是arguments单词缩写，表示任意多个无名参数，是一个tuple，如 (1,2,3,'a','b','c')

# **kwargs是keyword arguments单词缩写,表示关键字参数，是一个dict，如{'a':1,'b':2,'c':3}
def 函数名(*args,**kwargs)：
    代码块
```

- demo：可变参数

```python
>>> def f(*args,**kwargs):
...     print('args=',args)
...     print('kwargs=', kwargs)
...
>>> f(1,2,3)  # 只传参数*args=(1,2,3)
args= (1, 2, 3)
kwargs= {}
>>> f(a=1,b=2,c=3)  # 只传参数**kwargs=dict(a=1,b=2,c=3)
args= ()
kwargs= {'a': 1, 'b': 2, 'c': 3}
>>> f(1,2,3,a=1,b=2,c=3)  # 传入参数*args=(1,2,3) 和 **kwargs=dict(a=1,b=2,c=3)
args= (1, 2, 3)
kwargs= {'a': 1, 'b': 2, 'c': 3}
```

### 2.5 序列参数

- 语法：*args表示分离序列元素并传递。

```python
def 函数名(形参名1，形参名2)：
    代码块
函数名(*args)
```

- demo：序列化参数

```python
>>> def f(a,b,c):
...     return a + b +c
...
>>> f(*[1, 2, 3])
6
```
### 2.6 值传递和引用传递，以及参数传递机制

1. **值传递**：适用于实参类型为不可变类型（字符串、数字、元组）；
2. **引用（地址）传递**：适用于实参类型为可变类型（列表，字典）；
3. **参数传递机制**：值传递只是拷贝数值副本；引用传递实际上底层是值传递，只是传递的地址。

注意，不管什么类型的参数，在 Python 函数中对参数直接使用“=”符号赋值是没用的，直接使用“=”符号赋值并不能改变参数。

## 3. 返回值

### 3.1  return

Python中，用 def 语句创建函数时，可以用 return 语句指定应该返回的值，该返回值可以是任意类型。需要注意的是，return 语句在同一函数中可以出现多次，但只要有一个得到执行，就会直接结束函数的执行。

注意：返回值参数可以指定，也可以省略不写（将返回空值 None）。

```python
def 函数():
	return [返回值]
```

### 3.2 None

在 Python 中，有一个特殊的常量 None（N 必须大写），**和 False 不同，它不表示 0，也不表示空字符串，而表示没有值，也就是空值。**需要注意的是，None 是 NoneType 数据类型的唯一值（其他编程语言可能称这个值为 null、nil 或 undefined），也就是说不能再创建其它 NoneType 类型的变量，但是可以将 None 赋值给任何变量。如果希望变量中存储的东西不与任何其它值混淆，就可以使用 None。

对于所有没有 return 语句的函数定义，Python 都会在末尾加上 return None，使用不带值的 return 语句（也就是只有 return 关键字本身），那么就返回 None。

```python
>>> None is []
False
>>> None is ""
False
>>> type(None)
<class 'NoneType'>
```

### 3.3 返回多个参数

1. 返回一个tuple/list/dict类型，来间接达到返回多个值。
2. 使用Object，类似于C / C ++和Java，可以创建一个类来保存多个值并返回该类的对象。

```python
return (参数1, 参数2, 参数3)
```

## 4. 变量作用域

所谓**作用域（Scope），就是变量的有效范围，就是变量可以在哪个范围以内使用**。有些变量可以在整段代码的任意位置使用，有些变量只能在函数内部使用，有些变量只能在 for 循环内部使用。

变量作用域由变量的定义位置决定，在不同位置定义的变量，它的作用域是不一样的。

1. **在函数内部定义的变量，它的作用域也仅限于函数内部，出了函数就不能使用了，这样的变量称为局部变量（Local Variable）**。当函数被执行时，Python 会为其分配一块临时的存储空间，所有在函数内部定义的变量，都会存储在这块空间中。而在函数执行完毕后，这块**临时存储空间随即会被释放并回收**，该空间中存储的变量自然也就无法再被使用。
2. **在所有函数的外部定义变量，这样的变量称为全局变量（Global Variable）**,和局部变量不同，全局变量的默认作用域是整个程序，即全局变量既可以在各个函数的外部使用，也可以在各函数内部使用。

```python
>>> x = 2 # 全局变量
>>> def f():
...     y = 2  # 局部变量
...     print('x+y:', x+y)
...
>>> f()
x+y: 4
```

**globals() 函数为 Python 的内置函数**，它可以返回一个包含全局范围内所有变量的字典，该字典中的每个键值对，键为变量名，值为该变量的值。

```python
>>> globals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>}
>>> x = 1  # 增加全局变量
>>> globals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'x': 1}
```

**locals() 函数也是 Python 内置函数**，通过调用该函数，我们可以得到一个包含当前作用域内所有变量的字典。这里所谓的“当前作用域”指的是，在函数内部调用 locals() 函数，会获得包含所有局部变量的字典；而在全局范文内调用 locals() 函数，其功能和 globals() 函数相同。

```python
>>> a = 1
>>> b = 2
>>> globals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'a': 1, 'b': 2}
>>> def f():
...     x = 1
...     y = 1
...     print(locals())
>>> f()
{'x': 1, 'y': 1}  # 局部变量
>>> locals()  # 注意定义的函数也是一个全局变量
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'a': 1, 'b': 2, 'f': <function f at 0x000001355CE73F78>}
```

注意：**全局变量与局部变量冲突**，全局变量默认可以在所有函数内被访问，但是，如果当函数中定义了与全局变量同名的变量时，就会发生局部变量遮蔽（hide）全局变量的情形。在函数中声明全局变量。为了避免在函数中对全局变量赋值（不是重新定义局部变量），可使用 global 语句来声明全局变量。

```python
>>> x = 1
>>> y = 1
>>> def f():
...     x = 1
...     y = 2
...     globals()['x'] = 2
...     print(x, y)
...
>>> f()
1 2
```

## 5. 特殊函数

### 5.1 lambda函数

lambda 表达式，又称匿名函数，常用来表示内部仅包含 1 行表达式的函数。如果一个函数的函数体仅有 1 行表达式，则该函数就可以用 lambda 表达式来代替。

对于单行函数，使用 lambda 表达式可以省去定义函数的过程，让代码更加简洁；对于不需要多次复用的函数，使用 lambda 表达式可以在用完之后立即释放，提高程序执行的性能。

```python
# name = lambda [list] : 表达式
>>> func = lambda x:x**2
>>> func(2)
4
```

### 5.2  递归函数

函数在内部调用自己的函数称为递归。

```python
# n的阶乘
>>> def f(x):
...     if x < 1:
...         return 1
...     return x*f(x-1)
...
>>> f(5)
120
```

注意：递归的次数在python是有限制的，默认递归次数是997次

```python
# 修改默认递归次数的方法
>>> import sys
>>> sys.setrecursionlimit(1000)
```

### 5.3 偏函数partial

new_func = partial(函数名,参数),  生成一个新的函数, 新的函数中参数是partial固定时的参数.

```python
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```

### 5.4 局部函数

Python 支持在函数内部定义函数，此类函数又称为局部函数，嵌套函数。

如果所在函数没有返回局部函数，则局部函数的可用范围仅限于所在函数内部；反之，如果所在函数将局部函数作为返回值，则局部函数的作用域就会扩大，既可以在所在函数内部使用，也可以在所在函数的作用域中使用。

```python
#全局函数
def outdef ():
    #局部函数
    def indef():
        print("调用局部函数")
    #调用局部函数
    return indef
#调用全局函数
new_indef = outdef()
调用全局函数中的局部函数
new_indef()
```

### 5.5 闭包函数

1. 闭包，又称闭包函数或者闭合函数，其实和前面讲的嵌套函数类似，不同之处在于，闭包中外部函数返回的不是一个具体的值，而是一个函数。一般情况下，返回的函数会赋值给一个变量，这个变量可以在后面被继续执行调用。
2. 其次，和缩减嵌套函数的优点类似，函数开头需要做一些额外工作，当需要多次调用该函数时，如果将那些额外工作的代码放在外部函数，就可以减少多次调用导致的不必要开销，提高程序的运行效率。
3. 闭包比普通的函数多了一个 \_\_closure\_\_ 属性，该属性记录着自由变量的地址。当闭包被调用时，系统就会根据该地址找到对应的自由变量，完成整体的函数调用。

### 5.6 执行函数exec和eval

exec函数用于执行存储在字符串中的python语句。问题，污染我命名空间，可以添加命名空间。

```python
>>> abs(-1)
1
>>> exec("abs='xyz'")
>>> abs(-1)
  File "<stdin>", line 1, in <module>
TypeError: "str" object is not callable
>>> scope = {}
>>> exec("abs='xyz'", scope)
>>> abs(-1)
1
>>>scope['abs']
'xyz'
```
eval用于执行存储在字符串中的python表达式，同样可以给eval函数提供命名空间。

```python
>>> eval("1+2+3+4+5")
15
```
**注意：**

1. exec函数执行的是python语句，没有返回值，eval函数执行的是python表达式，有返回值；

2. exec函数和eval函数都可以传入命名空间作为参数，实际上，可以向exec函数和eval函数提供两个命名空间，他们的函数定义为：

```python
exec(source, globals=None, locals=None)
eval(source, globals=None, locals=None)
```

其中globals和locals都是可选参数，globals表示全局命名空间，必须是字典，locals表示局部命名空间，可以是任何映射。

3、需要注意的是，exec函数和eval函数都是将用户提供的字符串作为代码执行，将无法控制代码的行为，会带来严重的安全隐患，使用的时候要慎重。

## 6. 函数式编程

1. 所谓函数式编程，是指代码中每一块都是不可变的，都由纯函数的形式组成。这里的纯函数，是指函数本身相互独立、互不影响，对于相同的输入，总会有相同的输出。
2. 除此之外，函数式编程还具有一个特点，即允许把函数本身作为参数传入另一个函数，还允许返回一个函数。
3. 函数式编程的优点，主要在于其纯函数和不可变的特性使程序更加健壮，易于调试和测试；缺点主要在于限制多，难写。


```python
map(function, iterable)
filter(function, iterable)
reduce(function, iterable)
```

## 7. 函数注解：为函数提供类型提示信息

1. 提供类型信息：包括类型检查、让 IDE 显示函数接受和返回的类型、适配、与其他语言的桥梁、数据库查询映射、RPC参数编组等；
2. 其他信息：函数参数和返回值的文档。
```python
def square(number:"一个数字")->"返回number的平方":
  return number**2
print(square(10))
print(square.__annotations__)
```

## 8. 函数可读性

1. 不写重复性代码。
2. 刻意地减少代码的迭代层数，尽可能让 Python 代码扁平化。
3. 在使用函数时，函数的粒度应该尽可能细，不要让一个函数做太多的事情。

