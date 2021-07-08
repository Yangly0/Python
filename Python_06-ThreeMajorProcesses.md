---
@Author: liuyangly1
@Date  : 2021-07-08 13:38:01
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 三大流程(顺序，分支，循环)

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

## 1. 顺序结构
语句从上到下，从左到右的顺序执行。

```python
# 程序必须先从把2赋值给x，然后对x进行加2，再幂操作。
>>> x = 2
>>> x = x + 2
>>> x = x ** 2
>>> x
16
```

## 2. 分支结构

Python 中的选择结构就是判断真假。

### 2.1 if …… elif …… else

```python
>>> x= 5
>>> if x <1:
...     print('%d < 1'%x)
... elif x < 3:
...     print('1 <= %d < 3'%x)
... else:
...     print('3 <= %d < 10'%x)
...
3<5<10
```
### 2.2 类switch：没有switch结构，以dict实现switch功能
- 代码的可读性更高，执行效率也比if多分支语句要高。
- 结合lambda匿名函数，更简洁。
```python
>>> plus = lambda x,y: x+y
>>> minus = lambda x,y: x-y
>>> times = lambda x,y: x*y
>>> divide = lambda x,y: x/y
>>> operator = {'+':plus,'-':minus,'*':times,'/':divide}
# {key1:case1,key2:case2}.get(key)()
>>> operator.get('-')(5, 2)
3

# {key1:case1,key2:case2}.get(x,lambda *args,**keys: [args,keys])()
>>> func = lambda x,o,y:operator.get(o,lambda *args,**keys: [o,arg,key])(x,y)
>>> func(3, '/', 2)
1.5
>>> func(3, '+', 2)
5
```

### 2.3 demo：闰年判断

```python
>>> year = int(input("请输入年份："))
请输入年份：2000
>>> if year % 4 == 0:
...     if year % 100 == 0:
...             if year % 400 == 0:
...                     print("%d是世纪闰年"%year)
...             else:
...                     print("%d不是闰年"%year)
...     else:
...             print("%d是闰年"%year)
... else:
...     print("%d不是闰年"%year)
...
2000是世纪闰年
```

## 2. 循环结构
### 2.1 while...else 判断结构：条件循环
while 循环结构比较重视对循环条件的判断语句进行执行循环的动作。

```python
>>> n = 0
>>> while n < 10:
...     print(n)
...     n += 3
...
0
3
6
9

# 扩展模式
>>> n = 0
>>> while n < 10:
...     print(n)
...     n += 3
... else:
...     print('end')
0
3
6
9
end

# 无限循环
while True:
    print('1')
```
### 2.2  for...else 判断结构：遍历循环
```python
>>> for i in range(3):
...     print(i**2)
...
0
1
4
9

# 扩展模式
>>> for i in range(3):
...     print(i**2)
... else:
...     print('end')
...
0
1
4
9
end
```
### 2.3 循环控制: break和continue
```python
>>> while True:
...     number = int(input("请输入一个数(输入0退出)："))
...     if number == 0:
...             break
...     if number < 0:
...             print('输入数为负，请重新输入')
...             continue
...     print('输入的数是:%d'%number)
...
请输入一个数(输入0退出)：5
输入的数是:5
请输入一个数(输入0退出)：-5
输入数为负，请重新输入
请输入一个数(输入0退出)：0
```
### 2.4 demo：猜数字

```python
>>> import random
>>> number = random.randint(1, 1000)
>>> while True:
...     num = eval(input('请猜一个数字: '))
...     if num > number:
...             print('猜大了')
...     elif num < number:
...             print('猜小了')
...     else:
...             print('恭喜你，猜对了！')
...             break
...
请猜一个数字: 425
猜小了
请猜一个数字: 475
猜大了
请猜一个数字: 445
猜小了
请猜一个数字: 448
猜大了
请猜一个数字: 447
恭喜你，猜对了！
```

