---
title: Stack 栈 & Set 集合 & Map 哈希表
tags: 
	- 算法
	- 栈 
	- 集合
	- 哈希表
---

### Stack 栈

栈是一种 LIFO (Last In First Out) 的数据结构,常用方法有添加元素,取栈顶元素,弹出栈顶元素,判断栈是否为空.

#### Python

```python
stack = []
len(stack) # size of stack

import collections
stack = collections.deque()
```

list 作为最基本的python数据结构之一,可以轻松地实现 stack. 如果需要更高效的 stack, 建议使用 deque.

#### Methods

- len(stack) != 0 判断 stack 是否为空
- stack[-1] 取栈顶元素,不移除
- pop() 移除栈顶元素并返回该元素
- append(item) 向栈顶添加元素
<!-- more -->

### Set 集合

Set 是一种用于保存不重复元素的数据结构,常被用作测试归属性,故其查找的性能十分重要

#### Python

Set 是 python 自带的基本数据结构,有多种初始化方式. Python 的 set 跟 dict 的 实现方式类似,可以认为 set 是只有 key 的 dict

```pyton
s = set()
s1 = {1, 2, 3}
s.add('rayzhao')
'ray' in s # return true
s.remove('rayzhao')
```

### Map 哈希表

Map 是一种关联数组的数据结构,也常被称为字典或键值对.

#### Python

在 python 中 dict(Map) 是一种基本的数据结构

```python
# map 在 python 中是一个 keyword
hash_map = {}
hash_map['ray'] = 98
hash_map['zhao'] = 99
exist = 'zhao' in hash_map # check existence
point = hash_map['ray']
point = hash_map.pop('ray')
keys = hash_map.keys()

for key, value in hash_map.items():
    # do something with k, v
    pass
```

### Graph 图

图的表示通常使用**邻接矩阵**和**邻接表**,前者易实现但是对于稀疏矩阵会浪费较多空间,后者使用链表的方式存储信息但是对图搜索时间复杂度较高

#### 邻接矩阵

设顶点个数为 V, 那么邻接矩阵可以使用 V x V 的二维数组来表示. `g[i][j]`表示顶点 i 和顶点 j 的关系,对于无向图可以使用 0/1 表示是否有连接,对于带权图则需要使用 INF 来区分,有重边时保存边数或者权值最大/小的边即可

##### python

```python
g = [[0 for _ in range(V)] for _ in range(V)]
```

##### 邻接表

###### 有向图

```python
class DirectedGraphNode:
    def __init__(self, x):
        self.label = x
        self.neighbors = []
```

###### 无向图同上,只不过在建图时双向同时加

```python
class UndirectedGraphNode:
	def __init__(self, x):
		self.label = x
        self.neighbors = []
```


