---
@Author: liuyangly1
@Date  : 2021-07-07 21:51:29
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 二进制类型Bytes, Bytearray

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

操作二进制数据的核心内建数据类型是bytes和bytearray。它们由**memoryview**支持，memoryview使用buffer协议访问内存中其它的二进制对象，却不需要拷贝这些对象。array module对像32位整数和IEEE754双精度浮点数这样的基本数据类型有有效的存储支持。

## 1. bytes

bytes对象是由单字节组成的不可修改序列。

### 1.1 初始化

```python
>>> x = b'abc'
>>> x = b"abc"
>>> x = b'''abc'''
>>> type(x)
<class 'bytes'>
>>> x = br'abc\n'
>>> x
b'abc\\n'

# bytes([source[, encoding[, errors]]])
# 整数
>>> x = bytes(1234)
# 字符串，注意encoding必不可少。
>>> x = bytes('1234',encoding='utf-8')
```
当source参数为整数时，返回这个整数所指定长度的空字节数组。

```python
>>> bytes(2)
b'\x00\x00'
>>> bytes(-2) #整数需大于0，用于做数组长度
Traceback (most recent call last):
  File "<pyshell#19>", line 1, in <module>
    bytes(-2)
ValueError: negative count
```

当source参数是一个可迭代对象，那么这个迭代对象的元素都必须符合0 <= x < 256，以便可以初始化到数组里.

```python
>>> bytes([1,2,3])
b'\x01\x02\x03'
>>> bytes([256,2,3])
Traceback (most recent call last):
  File "<pyshell#21>", line 1, in <module>
    bytes([256,2,3])
ValueError: bytes must be in range(0, 256)
```

### 1.2 转换
两位16进制数正好可以表示一个byte，16进制数就成了描述bytes的常用形式。因此，bytes类型就有一个额外的类方法来读取16进制数据。

```python
>>> bytes.fromhex('2Ef0 F1f2  ')
b'.\xf0\xf1\xf2'
>>> b'.\xf0\xf1\xf2'.hex()
'2ef0f1f2'
```

### 1.3 增，删，改，查，排序
- 增：无法增加

- 删 translate, lstrip

```python
bytes.translate(table, /, delete=b'')
# 默认为空格
bytes.lstrip([chars])
```

- 改 replace

```python
>>> x = b'abc'
>>> x.replace('a','#')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: a bytes-like object is required, not 'str'
>>> x.replace(b'a','#')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: a bytes-like object is required, not 'str'
>>> x.replace(b'a',b'#')
b'#bc
```

- 查 count, find，rfind
```python
# bytes.count(sub[, start[, end]])
>>> x = b'abcabcabc'
# 返回匹配数量
>>> x.count(b'abc',4,10)
1
>>> x.count(b'abc',3,10)
2
# 返回匹配的初始位置
>>> x.find(b'abc',3,10)
3
# 最大索引
bytes.rindex(sub[, start[, end]])
```
- 排序

```python

```

### 1.4 开始和末尾判断，子序列判断，拼接，连接，分割序列

- 开始判断startswith末尾判断endswith
```python
>>> x = b'abcabcabc'
>>> x.startswith(b'ab')
True
>>> x.endswith(b'bc')
True
>>> x.endswith(b'bbc')
False
```
- 子序列判断in
```python
>>> b'Py' in b'Python'
True
```
- 拼接join
```python
>>> b''.join([b'a', b'b', b'c'])
b'abc'
```
- 连接maketrans
```python
bytes.maketrans(from, to)
```
- 分割序列partition和rpartition
```python
bytes.partition(sep)
bytes.rpartition(sep)
```

### 1.5 对齐，分割，删除
- 对齐
```python
bytes.ljust(width[, fillbyte])
bytes.center(width[, fillbyte])
bytes.rjust(width[, fillbyte])
```
- 分割

```python
bytes.split(sep=None, maxsplit=-1)
bytes.rsplit(sep=None, maxsplit=-1)
```
- 删除

```python
bytes.strip([chars])
bytes.rstrip([chars])
```

## 2. bytearray

bytearray是bytes的可修改版本。

### 2.1 初始化
```python
# bytearray([source[, encoding[, errors]]])
# 创建一个空的实例：bytearray()
>>> bytearray()
bytearray(b'')
# 创建一个给定长度的0填充的实例：bytearray(10)
>>> bytearray(10)
bytearray(b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')
# 通过一个可迭代的整数序列进行创建：bytearray(range(20))
>>> bytearray(range(20))
bytearray(b'\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f\x10\x11\x12\x13')
# 通过buffer协议拷贝一个已经存在的二进制数据：bytearray(b'Hi!')
>>> bytearray(b'Hi!')
bytearray(b'Hi!')
```
### 2.2 转换
两位16进制数正好可以表示一个byte，16进制数就成了描述bytes的常用形式。因此，bytes类型就有一个额外的类方法来读取16进制数据。

```python
>>> bytearray.fromhex('2Ef0 F1f2  ')
b'.\xf0\xf1\xf2'
>>> b'.\xf0\xf1\xf2'.hex()
'2ef0f1f2'
```

### 2.3 增，删，改，查，排序
- 增：无法增加

- 删 translate, lstrip
```python
bytearray.translate(table, /, delete=b'')
# 默认为空格
bytearray.lstrip([chars])
```


- 改 replace
```python
>>> x = b'abc'
>>> x.replace('a','#')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: a bytes-like object is required, not 'str'
>>> x.replace(b'a','#')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: a bytes-like object is required, not 'str'
>>> x.replace(b'a',b'#')
b'#bc
```

- 查 count, find，rfind
```python
# bytearray.count(sub[, start[, end]])
>>> x = b'abcabcabc'
# 返回匹配数量
>>> x.count(b'abc',4,10)
1
>>> x.count(b'abc',3,10)
2
# 返回匹配的初始位置
>>> x.find(b'abc',3,10)
3
# 最大索引
bytearray.rindex(sub[, start[, end]])
```
- 排序
```

```

### 2.4 开始和末尾判断，子序列判断，拼接，连接，分割序列

- 开始判断startswith末尾判断endswith
```python
>>> x = b'abcabcabc'
>>> x.startswith(b'ab')
True
>>> x.endswith(b'bc')
True
>>> x.endswith(b'bbc')
False
```
- 子序列判断in
```python
>>> b'Py' in b'Python'
True
```
- 拼接join
```python
>>> b''.join([b'a', b'b', b'c'])
b'abc'
```
- 连接maketrans
```python
bytearray.maketrans(from, to)
```
- 分割序列partition和rpartition
```python
bytearray.partition(sep)
bytearray.rpartition(sep)
```

### 2.5 对齐，分割，删除
- 对齐
```python
bytearray.ljust(width[, fillbyte])
bytearray.center(width[, fillbyte])
bytearray.rjust(width[, fillbyte])
```
- 分割
```python
bytearray.split(sep=None, maxsplit=-1)
bytearray.rsplit(sep=None, maxsplit=-1)
```
- 删除
```python
bytearray.strip([chars])
bytearray.rstrip([chars])
```