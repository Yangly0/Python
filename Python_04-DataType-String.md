---
@Author: liuyangly1
@Date  : 2021-07-07 22:13:03
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 文本类型String

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 初始化

- 单引号（推荐）和双引号
```python
>>> x = '123'
>>> x
'123'
>>> x = "1234"
>>> x
'1234'
```
- str()
```python
>>> x = str(12345)
>>> x
'12345'
```
## 2. 驻留机制

- 驻留是一种在内存中仅保存一份相同且不可变字符串的方法。
- 相同的字符串只保留一份拷贝，后续创建相同字符串时，不会开辟新空间，而是把该字符串的地址赋给新创建的变量。
- 实现过程：系统维护interned字典，记录已被驻留的字符串对象。当字符串对象a需要驻留时，先在interned检测是否存在，若存在则指向存在的字符串对象，a的引用计数减1；若不存在，则记录a到interned中。
    - 字符串只在编译时进行驻留，而非运行时。
    - 用乘法得到的字符串，如果结果长度 <=20且字符串只包含数字、字母大小写、下划线，支持驻留。长度>20，不支持驻留。这样的设计目的是为了保护.pcy文件不会被错误代码搞的过大。
    - 对于[-5,256]之间的整数数字，Python默认驻留。
    - Pyhton提供intern方法强制2个字符串指向同一个对象。
```python
# 字符串长度为0或1时，默认采用驻留机制
>>> x = 'a'
>>> y = 'a'
>>> x is y
True

# 字符串长度大于1时，且字符串中只包含大小写字母、数字、下划线时，采用驻留机制。
>>> x = 'abcdefghlmd_ADSAFSDG'
>>> y  = 'abcdefghlmd_ADSAFSDG'
>>> x is y
True

# 字符串只在编译时进行驻留，而非运行时。
>>> x = 'abc'
>>> y = 'ab' + 'c'
>>> z = ''.join(['ab', 'c'])
>>> x is y
True
>>> x is z
False

# 用乘法得到的字符串，如果结果长度<=20且字符串只包含数字、字母大小写、下划线，支持驻留。长度>20，不支持驻留。这样的设计目的是为了保护.pcy文件不会被错误代码搞的过大。
>>> x = 'abc'*7
>>> y = 'abc'*7
>>> x is y
True

# 对于[-5,256]之间的整数数字，Python默认驻留
>>> x = -5
>>> y = -5
>>> x is y
True
>>> x = 257
>>> y = 257
>>> x is y
False

# Pyhton提供intern方法强制2个字符串指向同一个对象。
>>> x = 'a%'
>>> y = 'a%'
>>> x is y
False
>>> import sys
>>> y = sys.intern(x)
>>> x is y
True
```

## 3. 索引与切片

```python
>>> x='abc'
>>> x[1]
'b'
>>> x[1:3]
'bc'
```

## 4. 遍历与格式化输出

- 遍历
```python
>>> x='abc'
>>> for i in x:
...     print(i)
...
a
b
c
```
- 格式化输出
```python
>>> a = '1'
>>> b = '2'
>>> c = '3'
>>> print('%s = %s + %s'%(c, a, b))
3 = 1 + 2

>>> print('{0} = {1} + {2}'.format(c, a, b))
3 = 1 + 2

# 前置0
>>> '%05d' % 1
00001'
```

## 5. 增, 删, 改, 查, 排序

- 增：不支持增加，只能重新定义+, %, format和f-string
```python
>>> x = 'a'
>>> y = 'b'
>>> x+y
'ab'
>>> '%s%s'%(x, y)
'ab'
>>> '{}{}'.format(x, y)
'ab'
>>> f'{x}{y}'
'ab'
```
- 删 strip
```python
>>> x=r'abc\n'
>>> x.strip(r'\n')
'abc'
>>> x.lstrip(r'\n')
'abc\\n'
>>> x.rstrip(r'\n')
'abc'
```

- 改：不支持删除，只能重新定义
```python
>>> x = 'abc'
>>> x = 'ab'
>>> x
'ab'
```

- 查 index, count, find
```python
>>> x = 'abc'
>>> x.count('a')
1
>>> x.index('c')
2
>>> x = 'abc'
>>> x.find('c')
2
```

- 排序 sorted
```python
>>> x = 'aebdc'
>>> sorted(x)
['a', 'b', 'c', 'd', 'e']

# 按单词的长度排序
>>> x = 'I love you'
>>> ' '.join(sorted(x.lower().split(' '), key=len)).capitalize()
'I you love'
```

## 6. 最大，最小，长度，组合, 比较

- 最大 max

```python
>>> x = 'a b c'
>>> max(x)
'c'

```

- 最小 min

```python
>>> x = 'a b c'
>>> min(x)
' '
```

- 长度  len

```python
>>> x = 'a b c'
>>> len(x)
5
```

- 组合 zip

```python
>>> list(zip(x, ['1', '2', '3']))
[('a', '1'), (' ', '2'), ('b', '3')]
```

- 比较 ==，operator

```python
>>> x = 'abc'
>>> y = 'bbc'
>>> z = 'abc'
>>> x == y
False
>>> x == z
True
>>> operator.eq(x, y)
False
>>> operator.eq(x, z)
True
```

## 7. 大小写，分割，对齐，替换和合并，编码与解码

- 大小写lower和upper, 首字母大写capitalize和标题大写title
```python
>>> x.lower()
'a b a b'
>>> x.upper()
'A B A B'
>>> x.capitalize()
'A b a b'
>>> x = 'I love you!'
>>> x.title()
'I Love You!'
```
- 分割 split，rsplit
```python
>>> x = 'a b A B'
>>> x.split(' ')
['a', 'b', 'A', 'B']
>>> x.rsplit(' ')
['a', 'b', 'A', 'B']
```
- 对齐 ljust, rjust, center
```python
>>> x = 'abc'
>>> x.ljust(5)
'abc  '
>>> x.rjust(5)
'  abc'
>>> x.center(5, #)
'#abc#'
```
- 替换 replace
```python
# replace(old, new[, max])
>>> x = 'abcabcabc'
>>> x.replace('a','#',2)
'#bc#bcabc'
```
- 合并 join
```python
>>> x = 'a b c'
>>> ','.join(x.split(' '))
'a,b,c'
```

- 编码encode与解码decode
```python
>>> x = 'i love 中国!'
>>> x.encode('gbk')
b'i love \xd6\xd0\xb9\xfa!'
>>> x.encode('utf-8')
b'i love \xe4\xb8\xad\xe5\x9b\xbd!'
>>> x
'i love 中国!'

>>> y = b'i love \xe4\xb8\xad\xe5\x9b\xbd!'
>>> y.decode('utf-8')
'i love 中国!'
```
## 8. 判断: 字母和数字，子串，开头和结尾

- 字母和数字：通过asicc码来判断
```python
str.isalnum() 所有字符都是数字或者字母
str.isalpha() 所有字符都是字母
str.isdigit() 所有字符都是数字，如果带小数点，则会返回False
str.isspace() 所有字符都是空白字符、t、n、r
```
- 字符串中是否包含数字search
```python
bool(re.search(r'\d', str))
```
- 子串 in, count,index,find,rfind
```python
>>> 'ab' in 'abc'
True

>>> x = 'abc'
>>> x.count('a')
1
>>> x.index('c')
2
>>> x = 'abcabc'
>>> x.find('c')
2
# 最大字串
>>> x.rfind('c')
5
```
- 开头startswith和结尾endswith
```python
>>> x = r'abc\n'
>>> x.startswith('bb')
False
>>> x.endswith(r'\n')
True
```

