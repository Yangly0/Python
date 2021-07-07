---
@Author: liuyangly1
@Date  : 2021-07-07 21:57:44
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 映射类型dict

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 初始化

```python
# {}
>>> x = {}
>>> type(x)
<class 'dict'>
# dict
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x
{'x': 1, 'y': 2, 'z': 3}
>>> x = dict.fromkeys('xyz')
>>> x
{'x': None, 'y': None, 'z': None}
```
## 2. 索引与切片

```python
>>> x['x']
1
```

## 3. 视图keys(),values(),items()，遍历与格式化输出

```python
x = dict({'x':1, 'y':2, 'z':3})
>>> for key in x.keys():
...     print(key)
...
x
y
z
>>> x.values()
dict_values([1, 2, 3])
>>> for key,value in x.items():
...     print(key, value)
...
x 1
y 2
z 3
```

##  4. 增, 删, 改, 查, 排序

- 增 update, setdefault
```python
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x['a'] = 4
>>> x
{'x': 1, 'y': 2, 'z': 3, 'a': 4}

# update不存在则添加，存在则修改
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x.update({'a':4})
>>> x
{'x': 1, 'y': 2, 'z': 3, 'a': 4}

>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x.setdefault('a')
>>> x
{'x': 1, 'y': 2, 'z': 3, 'a': None}

```
- 删 pop, popitem, del
```python
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x.pop('x')
1
>>> x
{'y': 2, 'z': 3}
>>> x.popitem()
('z', 3)
>>> x
{'y': 2}
>>> del x['y']
>>> x
{}
```
- 改 update
```python
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x['x'] = 0
>>> x
{'x': 0, 'y': 2, 'z': 3}

# update不存在则添加，存在则修改
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x.update({'x':0})
>>> x
{'x': 0, 'y': 2, 'z': 3}
```
- 查
```python
>>> x = dict({'x':1, 'y':2, 'z':3})
>>> x.get('x')
1
```
- 排序
```python
>>> x = dict({'x':3, 'y':2, 'z':1})
>>> sorted(x)
['x', 'y', 'z']
>>> sorted(x.values())
[1, 2, 3]
# 按键排序
>>> sorted(x.items())
[('x', 3), ('y', 2), ('z', 1)]
# 按值排序
>>> sorted(x.items(), key=lambda x:x[1])
[('z', 1), ('y', 2), ('x', 3)]
```

## 5. 最大max，最小min，求和sum，长度len，枚举enumerate，组合zip, 比较operator

```python
# 键最大值
>>> x = dict({'x':3, 'y':2, 'z':1})
>>> max(x)
'z'
# 值最大值
>>> max(zip(x.values(),x.keys()))
(3, 'x')
# 值最小值
>>> x[min(x,key=x.get)]
1
>>> sum(x.values())
6
>>> len(x)
3
>>> list(enumerate(x))
[(0, 'x'), (1, 'y'), (2, 'z')]
>>> list(zip(x, [1, 1, 1]))
[('x', 1), ('y', 1), ('z', 1)]
# 比较
>>> x = dict({'x':3, 'y':2, 'z':1})
>>> y = dict({'x':3, 'y':2, 'z':1})
>>> z = dict({'x':3, 'y':2, 'z':0})
>>> x == y
True
>>> x == z
False
>>> import operator
>>> operator.eq(x,y)
True
>>> operator.eq(x,z)
False
```
## 6. 字典推导式 = { key:value for循环 + 序列 + if条件}

```python
>>> x = {i:i**2 for i in range(10) if i%2==0}
>>> x
{0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

