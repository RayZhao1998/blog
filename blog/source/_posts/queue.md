---
title: Queue 队列
tags: 
	- 算法
	- 队列 
---

### Queue 队列

Queue 是一个 FIFO(先进先出) 的数据结构,并发中使用较多,可以安全地将对象从一个任务传给另一个任务

#### Python 实现

Queue 和 Stack 在 Python 中都有`list[]`实现的.在 Python 中 list 是一个 dynamic array,可以通过 `append`在 list 的尾部添加元素,通过`pop()`在 list 尾部弹出元素实现 `stack`的 `FILO`,如果是`pop(0)`则弹出头部元素实现`Queue`的`FIFO`

```python
queue = []
size = len(queue)
queue.append(1)
queue.append(2)
queue.pop(0)
queue[0] # return 2
```
<!-- more -->

##### Methods

|    \    |     Methods     |
| :-----: | :-------------: |
| Insert  | queue.append(e) |
| Remove  |  queue.pop(0)   |
| Examine |    queue[0]     |

#### 优先队列

应用程序常常需要处理带有优先级的业务,优先级最高的业务首先得到服务.因此优先队列这种数据结构应运而生.优先队列中的每个元素都有各自的优先级,优先级最高的元素最先得到服务;优先级相同的元素按照其在优先队列中的顺序得到服务.

优先队列可以使用数组或链表实现,从时间复杂度和空间复杂度来说,往往用二叉堆来实现.

|    \    |       methods        | time complexity |
| :-----: | :------------------: | :-------------: |
| enqueue | heapq.push(queue, e) |     O(logn)     |
| dequeue |   Heaps.pop(queue)   |     O(logn)     |
|  init   | Heaps.heapify(queue) |    O(nlogn)     |
|  peek   |       queue[0]       |      O(1)       |

#### Deque 双端队列

双端队列(double-ended queue) 可以让你在任何一端添加或删除元素,因此它是一种具有队列和栈性质的数据结构.

Python 的 list 就可以执行类似 deque 的操作,但是效率会过于慢.为了提升数据的处理效率,一些高效的数据结构放在了 collections 中. 在 collections 中提供了 deque 的类, 如果需要多次对 list 执行头尾元素的操作,请使用 deque

```python
dq = collections.deque()
```

|       \       |      methods      | time complexity |
| :-----------: | :---------------: | :-------------: |
| enqueue left  | dq.appendleft(e)  |      O(1)       |
| enqueue right | dq.appendright(e) |      O(1)       |
| dequeue left  |   dq.popleft()    |      O(1)       |
| dequeue right |     dq.pop()      |      O(1)       |
|   peek left   |       dq[0]       |      O(1)       |
|  peek right   |      dq[-1]       |      O(1)       |




