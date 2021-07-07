---
@Author: liuyangly1
@Date  : 2021-07-07 21:59:18
@Blog  : https://blog.csdn.net/liuyang_1106
@Github: https://github.com/liuyangly1
@Email : 522927317@qq.com
---

[toc]

# 堆类型heapq

[<img src="https://img.shields.io/badge/Github-%E8%AF%B7%E7%82%B9%E4%B8%AAStar%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-red" />](https://github.com/liuyangly1/Python) [<img src="https://img.shields.io/badge/CSDN-%E8%AF%B7%E7%82%B9%E4%B8%80%E4%B8%AA%E5%85%B3%E6%B3%A8%EF%BC%8C%E6%84%9F%E8%B0%A2%EF%BC%81-brightgreen" />](https://blog.csdn.net/liuyang_1106)

- 默认是最小堆。
- 最小堆，树种各个父节点的值总是小于或等于任何一个子节点的值。
- 一般使用二叉堆来实现优先级队列,它的内部调整算法复杂度为logN。

## 1. 初始化 heapq.heapify(list)

- 将列表转换为堆。
```python
>>> import heapq
>>> x = [1,2,3,5,1,5,8,9,6]
>>> heapq.heapify(x)
>>> x
[1, 1, 3, 5, 2, 5, 8, 9, 6]
```

## 2. 添加 heapq.heappush(heap, item)

- heap为定义堆，item增加的元素。
```python
>>> import heapq
>>> x = []
>>> heapq.heappush(x, 2)
>>> x
[2]
```

## 3. 弹出 heapq.heappop(heap)

- 删除并返回最小值，因为堆的特征是heap[0]永远是最小的元素，所以一般都是删除第一个元素。
```python
>>> x = [1, 1, 3, 5, 2, 5, 8, 9, 6]
heapq.heapify(x)
>>> heapq.heappop(x)
1
>>> x
[1, 2, 3, 5, 6, 5, 8, 9]
```

