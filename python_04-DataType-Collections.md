---
@Author: liuyangly1
@Date  : 2021-07-07 21:55:20
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 容器类型ollections

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

```python
>>> import collections
>>> collections.__all__
['deque', 'defaultdict', 'namedtuple', 'UserDict', 'UserList', 'UserString', 'Counter', 'OrderedDict', 'ChainMap']
```

## 1. OrderedDict

OrderedDict 可以理解为有序的dict，底层源码是通过双向链表来实现，每一个元素为一个map存储key-value。

### 1.1 初始化
```python
>>> p = collections.OrderedDict()
>>> p["a"]=1
>>> p["b"]=2
>>> p["c"]=3
>>> print(p)
OrderedDict([('a', 1), ('b', 2), ('c', 3)])
```
### 1.2 方法

```python
OrderedDict.clear()        
OrderedDict.fromkeys()   
OrderedDict.items()        
OrderedDict.move_to_end()
OrderedDict.popitem()     
OrderedDict.update()
OrderedDict.copy()        
OrderedDict.get()          
OrderedDict.keys()         
OrderedDict.pop()          
OrderedDict.setdefault()   
OrderedDict.values()
```
- update，pop，move\_to\_end和clear
```python
>>> keys=["apple", "banana", "cat"]
>>> value=[4, 5, 6]
# update
>>> p.update(zip(keys,value))
>>> p
OrderedDict([('a', 1), ('b', 2), ('c', 3), ('apple', 4), ('banana', 5), ('cat', 6)])
# pop
>>> p.pop('a')
1
>>> p
OrderedDict([('b', 2), ('c', 3), ('apple', 4), ('banana', 5), ('cat', 6)])
# move_to_end
>>> p.move_to_end('b')
>>> p
OrderedDict([('c', 3), ('apple', 4), ('banana', 5), ('cat', 6), ('b', 2)])
# del
>>> del(p['c'])
>>> p
OrderedDict([('apple', 4), ('banana', 5), ('cat', 6), ('b', 2)])
# clear
>>> p.clear()
>>> p
OrderedDict()
```
### 1.3 demo:json有序读取
```python
import json  
from collections import OrderedDict  
metadata = json.loads(text, object_pairs_hook=OrderedDict)
```

## 2. deque
- 双向队列,两端快速添加(append)和弹出(pop)。

### 2.1 初始化
```python
d = collections.deque([iterable[, maxlen]])
```

### 2.2 方法
```python
len(d)、reversed(d)、copy.copy(d)、copy.deepcopy(d)
```

```python
deque.append(x)
deque.appendleft(x)
deque.clear()
deque.copy()
deque.count(x)
deque.extend(iterable)
deque.xtendleft(iterable)
deque.index(x[, start[, stop]])
deque.insert(i, x)
deque.pop()
deque.popleft()
deque.remove(value)
deque.reverse()
deque.rotate(n=1) # 向右循环移动 n 步。 如果 n 是负数，就向左循环。
deque.maxlen # 只读属性，Deque的最大尺寸
```
### 2.3 demo

```python
>>> from collections import deque
>>> d = deque('ghi')                 # make a new deque with three items
>>> for elem in d:                   # iterate over the deque's elements
...     print(elem.upper())
G
H
I

>>> d.append('j')                    # add a new entry to the right side
>>> d.appendleft('f')                # add a new entry to the left side
>>> d                                # show the representation of the deque
deque(['f', 'g', 'h', 'i', 'j'])

>>> d.pop()                          # return and remove the rightmost item
'j'
>>> d.popleft()                      # return and remove the leftmost item
'f'
>>> list(d)                          # list the contents of the deque
['g', 'h', 'i']
>>> d[0]                             # peek at leftmost item
'g'
>>> d[-1]                            # peek at rightmost item
'i'

>>> list(reversed(d))                # list the contents of a deque in reverse
['i', 'h', 'g']
>>> 'h' in d                         # search the deque
True
>>> d.extend('jkl')                  # add multiple elements at once
>>> d
deque(['g', 'h', 'i', 'j', 'k', 'l'])
>>> d.rotate(1)                      # right rotation
>>> d
deque(['l', 'g', 'h', 'i', 'j', 'k'])
>>> d.rotate(-1)                     # left rotation
>>> d
deque(['g', 'h', 'i', 'j', 'k', 'l'])

>>> deque(reversed(d))               # make a new deque in reverse order
deque(['l', 'k', 'j', 'i', 'h', 'g'])
>>> d.clear()                        # empty the deque
>>> d.pop()                          # cannot pop from an empty deque
Traceback (most recent call last):
    File "<pyshell#6>", line 1, in -toplevel-
        d.pop()
IndexError: pop from an empty deque

>>> d.extendleft('abc')              # extendleft() reverses the input order
>>> d
deque(['c', 'b', 'a'])
```

## 3. Counter
一个 Counter 是一个 dict 的子类，用于计数可哈希对象。它是一个集合，元素像字典键(key)一样存储，它们的计数存储为值。计数可以是任何整数值，包括0和负数。 Counter 类有点像其他语言中的 bags或multisets。

### 3.1 初始化

```python
collections.Counter([iterable-or-mapping])
```

### 3.2 方法

```python
# 返回一个迭代器，其中每个元素将重复出现计数值所指定次。
Counter.elements()

# 返回一个列表，其中包含 n 个最常见的元素及出现次数，
# 按常见程度由高到低排序。
Counter.most_common([n])

# 从 迭代对象 或 映射对象 减去元素。像 dict.update()
# 但是是减去，而不是替换。
Counter.Counter.subtract([iterable-or-mapping])

# 通常字典方法都可用于 Counter 对象
Counter.fromkeys(iterable)

# 从 迭代对象 计数元素或者 从另一个 映射对象 (或计数器) 添加。
Counter.update([iterable-or-mapping])
```

### 3.3 demo

```python
c = Counter()                           
c = Counter('gallahad')     
c = Counter({'red': 4, 'blue': 2})     
c = Counter(cats=4, dogs=8)      args

c = Counter(['eggs', 'ham'])
c['bacon']     
0

c['sausage'] = 0    
del c['sausage'] 

c = Counter(a=4, b=2, c=0, d=-2)
sorted(c.elements())
['a', 'a', 'a', 'a', 'b', 'b']

Counter('abracadabra').most_common(3)
[('a', 5), ('b', 2), ('r', 2)]

c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
c
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```

## 参考

- [1] [Python-collections---容器数据类型- Python文档](https://docs.python.org/zh-cn/3/library/collections.html#collections.Counter)

