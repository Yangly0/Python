---
@Author: liuyangly1
@Date  : 2021-07-07 22:09:27
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]


# Title

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

# 集合类型Set, Frozenset

## 1. set

### 1.1 初始化

```python
# {} 
>>> a = {} 
# set 
>>> x = set('runoob') 
>>> x {'n', 'b', 'o', 'u', 'r'} 
```

### 1.2 索引与切片：无法操作 

```python

x = set('runoob') 
>>> x[3] 

Traceback (most recent call last): File "", line 1, in TypeError: 'set' object is not subscriptable
```

### 1.3 遍历与格式化输出 

```python
x = set('runoob') 
>>> for i in x: 
    ... print(i) ... 
    n b o u r 
```

### 1.4 增, 删, 改, 查, 排序 

- 增add, update

```python
>>> x = {1, 2, 3} 
>>> x.add(4) 
>>> x {1, 2, 3, 4} 
>>> x.update({5, 6}) 
>>> x {1, 2, 3, 4, 5, 6} 
```

- 删 remove, pop, discard, clear 

```python
>>> x = {1, 2, 3} # 如果元素不存在，则会发生错误 
>>> x.remove(3) 
>>> x.remove(3) Traceback (most recent call last): File "", line 1, in KeyError: 3 

# 随机删除集合中的一个元素 
>>> x.pop() 
1 
>>> x {2} # 如果元素不存在，不会发生错误 
>>> x.discard(2)
>>> x set() 
>>> x.discard(2) 
>>> x set() 
>>> x = {1, 2, 3} 
>>> x {1, 2, 3} 
>>> x.clear() 
>>> x set() 
```

- 改: 无 

- 查 in 

```python
>>> x = {1, 2, 3} 
>>> 2 in x True 
```

- 排序 

```python
>>> x = {2, 1, 3} 
>>> sorted(x) [1, 2, 3] 
```

### 1.5 最大，最小，求和，长度，枚举，组合, 比较

- 最大 max

```python
>>> x = {2, 1, 3} 
>>> max(x)
3
```

- 最小 min

```python
>>> x = {2, 1, 3} 
>>> sum(x)
6
```

- 求和 sum

```python
>>> x = {2, 1, 3} 
>>> sum(x)
6
```

- 长度 len

```python
>>> x = {2, 1, 3} 
>>> len(x)
3
```

- 枚举 enumerate

```python
>>> x = {2, 1, 3} 
>>> list(enumerate(x))
[(0, 1), (1, 2), (2, 3)] 
```

- 组合 zip

```python
>>> x = {2, 1, 3} 
>>> list(zip(x,[1, 1, 1])) 
[(1, 1), (2, 1), (3, 1)]
```

- 比较 operator和== 

```python
>>> x = {1, 2, 3} 
>>> y = {2, 3, 1} 
>>> z = {1, 2, 4} 
>>> x.__eq__(y) True 
>>> x.__eq__(z) False 
>>> x == y 
True 
>>> x == z 
False 
>>> import operator 
>>> operator.eq(x, y) 
True 
>>> operator.eq(x, z) 
False 
```

### 1.6 交，并，差及关系判断（相交，子集和异或） 

- 交，并和差 

```python
>>> x = {1, 2, 3} 
>>> y = {2, 3, 4} # 交集 
>>> x & y {2, 3} 
>>> x.intersection(y) 
{2, 3} 
>>> x.intersection_update(y) 
>>> x 
{2, 3} # 并 
>>> x = {1, 2, 3} 
>>> y = {2, 3, 4} 
>>> x | y 
{1, 2, 3, 4} 
>>> x.union(y) 
{1, 2, 3, 4} # 差 

>>> x = {1, 2, 3} 
>>> y = {2, 3, 4} 
>>> x - y {1} 
>>> x.difference(y) 
{1} # 移除差集 
>>> x.difference_update(y) 
>>> x 
{1} 

```

- 相交，子集和异或 

```python 
set.isdisjoint(s) # 判断两个集合是不是不相交 
set.issuperset(s) # 子集，判断集合是不是包含其他集合，等同于a>=b 
set.issubset(s) # 子集，判断集合是不是被其他集合包含，等同于a<=b 
set.symmetric_difference(s) # 异或，返回不同项 
set.symmetric_difference_update(s) # 异或，合并不同项，并更新自己 
```

### 1.7 集合推导式 = { key for循环 + 序列 + if条件} 

```python
>>> x = {i**2 for i in range(10) if i%2==0} 
>>> x 
{0, 64, 4, 36, 16} 
```

## 2. frozense 

### 2.1 初始化 

``` python
x = frozenset("hello") 
>>> type(x) 
>>> x 
frozenset({'h', 'o', 'l', 'e'}) 
```

### 2.2 索引与切片：无法操作

``` python
>>> x = frozenset("hello") 
>>> x[2] Traceback (most recent call last): File "", line 1, in TypeError: 'frozenset' object is not subscriptable
```

### 2.3 遍历与格式化输出

``` python
>>> x = frozenset("hello") 
>>> for i in x: 
    ... print(i) ... 
```

### 2.4 增, 删, 改, 查, 排序

- 增，删，改：无法操作

- 查

``` python
>>> x = frozenset([1, 2, 3]) 
>>> 3 in x True 
```

- 排序 

``` python
>>> x = frozenset([3, 2, 1]) 
>>> sorted(x) 
[1, 2, 3] 
```

### 2.5 最大，最小，求和，长度，枚举，组合, 比较

- 最大 max

```python
>>> x = frozenset([3, 2, 1]) 
>>> max(x)
3
```

- 最小 min

```python
>>> x = frozenset([3, 2, 1]) 
>>> sum(x)
6
```

- 求和 sum

```python
>>> x = frozenset([3, 2, 1]) 
>>> sum(x)
6
```

- 长度 len

```python
>>> x = frozenset([3, 2, 1]) 
>>> len(x)
3
```

- 枚举 enumerate

```python
>>> x = frozenset([3, 2, 1]) 
>>> list(enumerate(x))
[(0, 1), (1, 2), (2, 3)] 
```

- 组合 zip

```python
>>> x = frozenset([3, 2, 1]) 
>>> list(zip(x,[1, 1, 1])) 
[(1, 1), (2, 1), (3, 1)]
```

- 比较 operator和== 

``` python
>>> x = frozenset([3, 2, 1]) 
>>> y = frozenset([3, 2, 1]) 
>>> z = frozenset([3, 2, 0]) 

>>> x == y 
True 
>>> x == z 
False 
>>> import operator 
>>> operator.eq(x, y) 
True 
>>> operator.eq(x, z) 
False 
```

### 2.6 交，并，差及关系判断（相交，子集和异或） 

- 交，并和差

```python
# 交 
>>> x = frozenset({1, 2, 3}) 
>>> y = frozenset({2, 3, 4}) 
>>> x & y 
frozenset({2, 3}) 
>>> x.intersection(y) 
frozenset({2, 3}) 
>>> x.intersection_update(y) 
Traceback (most recent call last): File "", line 1, in AttributeError: 'frozenset' object has no attribute 'intersection_update' # 并 
>>> x = frozenset({1, 2, 3}) 
>>> y = frozenset({2, 3, 4}) 
>>> x | y 
frozenset({1, 2, 3, 4}) 
>>> x.union(y) 
frozenset({1, 2, 3, 4}) # 差 

>>> x = frozenset({1, 2, 3}) 
>>> y = frozenset({2, 3, 4}) 
>>> x - y 
frozenset({1}) 
>>> x.difference(y) 
frozenset({1}) 
>>> x.difference_update(y) 
Traceback (most recent call last): File "", line 1, in AttributeError: 'frozenset' object has no attribute 'difference_update' 
```

- 相交，子集和异或 

``` python
set.isdisjoint(s) # 判断两个集合是不是不相交 
set.issuperset(s) # 子集。判断集合是不是包含其他集合，等同于a>=b 
set.issubset(s) # 子集，判断集合是不是被其他集合包含，等同于a<=b 
set.symmetric_difference(s) # 异或，返回不同项 
```

