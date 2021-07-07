---
@Author: liuyangly1
@Date  : 2021-07-07 21:15:31
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 类型转换

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 数值型

```python
# int(x [,base]) 将x转换为一个整数
>>> x = 1.0
>>> int(x)
# 注意：对于字符串的不同基数，可以转换为整型
>>> x = '101'  
>>> int(x, 2)
5

# float(x)  将x转换到一个浮点数 
>>> x = 1
>>> float(x)
1.0

# complex(real [,imag]) 创建一个复数
>>> complex(1, -1)
(1-1j)
```

## 2. 进制转换：二进制十进制、八进制、十六进制

```python
# bin(x) 将一个整数转换为一个二进制字符串 
>>> x = 2
>>> bin(x)
'0b10'

# oct(x) 将一个整数转换为一个八进制字符串  
>>> x = 2
>>> oct(x)
'0o2'

# hex(x) 将一个整数转换为一个十六进制字符串  
>>> x = 2
>>> hex(x)
'0x2'

```

## 3. ASCII码

```python
# ord(x) 将一个字符即ASICII码转换为它的整数十进制值  
>>> x = 'a'
>>> ord(x)
97
# chr(x) 将一个整数转换为一个字符 
>>> x = 97
>>> chr(x)
'a'
```

## 4. 字符和字符串

```python
# 字符串
# str(x) 将对象 x 转换为字符串  
>>> x = 1
>>> str(x)
'1'

# repr(x) 将对象 x 转换为表达式字符串  
>>> x = 1
>>> repr(x)
'1'

# eval(str) 用来计算在字符串中的有效Python表达式,并返回一个对象 
>>> x = '1+1'
>>> eval(x)
2
```

## 5. 元组和列表

```python
# tuple(x) 将序列x转换为一个元组 
>>> x = [1, 2, 3]
>>> tuple(x)
(1, 2, 3)


# list(x) 将序列x转换为一个列表  
>>> x = (1, 2, 3)
>>> list(x)
[1, 2, 3]
```

## 6. 集合

```python
# set(s) 将序列 s 转换为一个集合 去重
>>> x = [1, 1, 2, 3]
>>> set(x)
{1, 2, 3}
```

