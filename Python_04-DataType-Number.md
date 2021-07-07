---
@Author: liuyangly1
@Date  : 2021-07-07 22:08:41
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 数值类型Number

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. int

- 不同的类型，有不同的存储大小和取值范围，超出这个范围就会溢出报错。
- Python明显简化了这一类型，所有的整数类型，不论正负不论大小，全都归一为int类型。
- Python2还保留了long类型，python3把long类型也去掉了。
- 进制：0b开头表示二进制(bin)、0o开头表示八进制(oct)、0x开头表示十六进制(hex)。

```python
# 10进制
>>> value = 16    # 默认显示格式
# 十进制转二进制
>>> bin(value)    # 默认运算格式
>>> bin(-1 & 0xffffffff)  # 负数补码
>>> int('10100111110',2) 
# 十进制转八进制
>>> oct(value)
>>> int('17',8)  
# 十进制转十六进制
>>> hex(value)
>>> int('0xf',16) 
```
## 2. float
- 浮点型由整数部分与小数部分组成，浮点型也可以使用科学计数法表示（2.5e2 = 2.5 x 10^2 = 250）.
```python
>>> x = 1.5
>>> x
1.5
>>> x = 1e5
>>> x
100000.0
```
## 3. complex
```python
>>> x = 1-7j
>>> x
(1-7j)
>>> x = complex(3, 2)
>>> x
(3+2j)
```

