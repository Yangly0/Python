---
@Author: liuyangly1
@Date  : 2021-07-07 22:00:58
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 序列类型 list, tuple

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. list

### 1.1 初始化

```python
# []
>>> x = []
>>> x
[]

# 推导式创建列表
>>> x = [i**2 for i in range(5)]
>>> x
[0, 1, 4, 9, 16]

# 构造函数
>>> x = list()
>>> x
[]
>>> x = list((3.14, False, 'x', None))
>>> x
[3.14, False, 'x', None]
>>> x = list({'x':1,'y':2,'z':3})
>>> x
['x', 'y', 'z']
```

### 1.2 索引与切片

```python
# 左闭右开
>>> x = [1, 2, 3]
>>> x[1:2]
[2]

# 最后一个元素
>>> x[-1]
3
```
### 1.3 遍历与格式化输出

```python
# 遍历
>>> x= [1, 2, 3]
>>> for i in x:
...     print(i)
...
1
2
3
# 格式化输出
>>> x = [1, 2, 3]
>>> print('a:%d, b:%d, c:%d'%(*x))
  File "<stdin>", line 1
SyntaxError: can't use starred expression here
>>> print('%s, a:%d, b:%d, c:%d'%('dict',*x))
dict, a:1, b:2, c:3
```

### 1.4 增, 删, 改, 查, 排序

- 增 append()，insert()，extend()，+, *
```python
## 不修改地址
# append(value) 用于向列表尾部追加一个元素
# insert(index,value) 用于向列表任意指定位置插入一个元素
# extend(list) 用于将另一个列表中的所有元素追加至当前列表的尾部
>>> x = [1, 2, 3]
>>> x
[1, 2, 3]
>>> id(x)
2403937045832
>>> x.append(4)
>>> x
[1, 2, 3, 4]
>>> id(x)
2403937045832
>>> x.insert(0, 0)
>>> x
[0, 1, 2, 3, 4]
>>> id(x)
2403937045832
>>> x.extend([5, 6, 7])
>>> x
[0, 1, 2, 3, 4, 5, 6, 7]
>>> id(x)
2403937045832

## 修改地址
# list + list 列表合并
>>> x = [1, 2, 3]
>>> x
[1, 2, 3]
>>> id(x)
2403937045832
>>> x = x + x
>>> x
[1, 2, 3, 1, 2, 3]
>>> id(x)
2403937009864

# list * 2 列表重复
>>> x = [1, 2, 3]
>>> x
[1, 2, 3]
>>> id(x)
2403937045832
>>> x = x * 3
>>> x
[1, 2, 3, 1, 2, 3, 1, 2, 3]
>>> id(x)
2403937009864
```
- 删 pop(), remove(), clear(), del
```python
## 地址不改变
# pop(index) 用于删除并返回指定位置（默认是最后一个）上的元素
# remove(value) 用于删除列表中第一个值与指定值相等的元素
# clear() 用于清空列表
# del list[index]  删除列表中指定位置的元素

>>> x = [1, 2, 3, 4]
>>> x
[1, 2, 3, 4]
>>> x.pop()
4
>>> x.remove(2)
>>> x
[1, 3]
>>> del x[0]
>>> x
[3]
>>> x.clear()
>>> x
[]
```
- 改 list[index] = new_value
```python
>>> x = [1, 2, 3]
>>> x
[1, 2, 3]
>>> x[1] = 10
>>> x
[1, 10, 3]
>>> x[x.index(3)] = 5
>>> x
[1, 10, 5]
>>> x[1:3] = 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only assign an iterable
>>> x[1:3] = [1, 1]
>>> x
[1, 1, 1]
```

- 查 count(), index(), in
```python
# count() 用于返回列表中指定元素出现的次数
# index() 用于返回指定元素在列表中首次出现的位置，如果不存在则抛出异常
# in 测试列表中是否存在某个元素
>>> x = [1, 1, 2, 3]
>>> x.count(1)
2
>>> x.index(2)
2
>>> 4 in x
False
```
- 排序 sort(), reverse(), sorted(), reversed()
```python
## 不改变地址
# sort() 用于按照指定的规则对所有元素进行排序，默认规则是直接比较元素大小
# reverse() 用于将列表所有元素逆序排列
>>> x = [1, 3, 2, 0]
>>> x.sort()
>>> x
[0, 1, 2, 3]
>>> x.reverse()
>>> x
[3, 2, 1, 0]

## 改变地址
# sorted() 用于按照指定的规则对所有元素进行排序，默认规则是直接比较元素大小
>>> x = [1, 3, 2, 0]
>>> id(x)
2403937045832
>>> y = sorted(x)
>>> y
[0, 1, 2, 3]
>>> id(y)
2403937046024
>>> x
[1, 3, 2, 0]
# reversed() 用于将列表所有元素逆序排列
>>> y = list(reversed(x))
>>> id(y)
2403937055176
>>> id(x)
2403937045832
>>> y
[0, 2, 3, 1]
>>> x
[1, 3, 2, 0]
```

### 1.5 最大，最小，求和，长度，枚举，组合, 比较

- 最大 max

```python
>>> x = [1, 2, 3]
>>> max(x)
3
```

- 最小 min

```python
>>> x = [1, 2, 3]
>>> sum(x)
6
```

- 求和 sum

```python
>>> x = [1, 2, 3]
>>> sum(x)
6
```

- 长度 len

```python
>>> x = [1, 2, 3]
>>> len(x)
3
```

- 枚举 enumerate

```python
>>> x = [1, 2, 3]
>>> list(enumerate(x))
[(0, 1), (1, 2), (2, 3)]
```

- 组合 zip

```python
>>> x = [1, 2, 3]
>>> list(zip(x, [1, 1, 1]))
[(1, 1), (2, 1), (3, 1)]
```

- 比较 operator和== 

```python
>>> import operator
>>> y = [1, 2, 4]
>>> z = [1, 2, 3]
>>> operator.eq(x, y)
False
>>> operator.eq(x, z)
True
>>> x == y
False
>>> x == z
True
```

### 1.6 列表推导式 = [表达式 for循环 + 列表 + if条件]

- [表达式 for 变量 in 序列或迭代对象 if 条件]
```python
>>> x = [i**2 for i in range(10) if i%2 == 0]
>>> x
[0, 4, 16, 36, 64]
```

## 2 tuple

### 2.1 初始化

```python
# (value,)
>>> x = (1,)
>>> type(x)
<class 'tuple'>
>>> x = (1)
>>> type(x)
<class 'int'>

# 推导式创建列表
>>> x = [i**2 for i in range(5)]
>>> x
[0, 1, 4, 9, 16]

# 构造函数
>>> x = tuple()
>>> x
()
>>> x = tuple((3.14, False, 'x', None))
>>> x
(3.14, False, 'x', None)
>>> x = tuple({'x':1,'y':2,'z':3})
>>> x
('x', 'y', 'z')
```

### 2.2 索引与切片

```python
# 左闭右开
>>> x = (1, 2, 3, )
>>> x[1:2]
(2,)

# 最后一个元素
>>> x[-1]
3
```
### 2.3 遍历与格式化输出

```python
# 遍历
>>> x = (1, 2, 3, )
>>> for i in x:
...     print(i)
...
1
2
3

# 格式化输出
>>> x = (1, 2, 3, )
>>> x
(1, 2, 3)
>>> print('a:%d, b:%d, c:$d'%(*x))
  File "<stdin>", line 1
SyntaxError: can't use starred expression here
>>> print('%s, a:%d, b:%d, c:%d'%('dict',*x))
dict, a:1, b:2, c:3
```

### 2.4 增, 删, 改, 查, 排序

- 元素无法增，删，改，只能新建元组重新赋值操作。
- 增 +, *
```python
# 组合+和重复*
>>> x = (1, 2, 3,)
>>> id(x)
2143650640016
>>> x = x + x
>>> x
(1, 2, 3, 1, 2, 3)
>>> id(x)
2143649855240
>>> x = x * 2
>>> x
(1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3)
>>> id(x)
2143650010312
```
- 删 del
```python
# del 仅能删除整个元组
>>> x = (1, 2, 3,)
>>> del x[1]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object doesn't support item deletion
>>> del x
>>> x
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'x' is not defined
```

- 改: 无法修改  
```python
>>> x = (1, 2, 3,)
>>> x[1] = 4
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

### 2.5 最大max，最小，求和，长度，枚举，组合, 比较

- 最大 max

```python
>>> x = (1, 2, 3, )
>>> max(x)
3
```

- 最小 min

```python
>>> x = (1, 2, 3, )
>>> sum(x)
6
```

- 求和 sum

```python
>>> x = (1, 2, 3, )
>>> sum(x)
6
```

- 长度 len

```python
>>> x = (1, 2, 3, )
>>> len(x)
3
```

- 枚举 enumerate

```python
>>> x = (1, 2, 3, )
>>> list(enumerate(x))
[(0, 1), (1, 2), (2, 3)]
```

- 组合 zip

```python
>>> x = (1, 2, 3, )
>>> list(zip(x, [1, 1, 1]))
[(1, 1), (2, 1), (3, 1)]
```

- 比较 operator和== 

```python
>>> import operator
>>> y = (1, 2, 4)
>>> z = (1, 2, 3)
>>> operator.eq(x, y)
False
>>> operator.eq(x, z)
True
>>> x == y
False
>>> x == z
True
```



## 3. 注意：元组的特殊性

- 元组是可哈希的，元素具有唯一性，不可变。元组加到集合中，但列表不行，因为列表是不可哈希（unhashable）的。理解这一点并不困难：列表元素可以被动态改变，所以没有一个固定不变的哈希值——这与集合要求的元素唯一性冲突；而元组的元素被禁止更新，其哈希值在整个生命周期都不会变化，因此可以成为集合的元素。
- 元组可以在映射（和集合的成员）中作为键（key）使用，而列表不行。**键一旦修改，会破坏表结果。**
- 元组作为很多内建函数和方法的返回值存在。
- 元组和列表有者完全不同的存储方式。因为不用考虑更新问题，元组的速度性能要远优于列表。优先使用元组，应该成为Python程序员遵循的一条基本原则。
```python
>>> x = (1, 2, 3,)
>>> y = [1, 2, 3]
>>> z = {0}
>>> z.add(x)
>>> z
{0, (1, 2, 3)}
>>> z.add(y)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

