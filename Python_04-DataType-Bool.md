---
@Author: liuyangly1
@Date  : 2021-07-07 21:48:30
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 布尔类型Bool

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 定义：True和False

```python
>>> flag = True 
>>> flag1 = False
```

## 2. 判断：is和==

```python
>>> flag = True
>>> flag is True
True
>>> flag == True
True
```

## 3. 特殊性质：bool 是int子类；0为False，其余为真。

```python
>>> x = True
>>> x = bool(1)
>>> x
True

# bool 是 int 子类
>>> issubclass(bool, int) 
True
```

