---
title: 《数据结构与算法之美 队列篇笔记》 
tags:
    - 算法
---
## 如何理解队列
先进者先出，这就是典型的“队列”

栈有两个基本操作：入栈 `push()` 和出栈`pop()`，队列和栈非常相似，也有两个基本的操作：入队`enqueue()` 和出队`dequeue()`

![](https://static001.geekbang.org/resource/image/9e/3e/9eca53f9b557b1213c5d94b94e9dce3e.jpg)
<!-- more -->

所以队列和栈一样是一种*操作受限的线性表数据结构*

队列的应用非常广，特别是一些具有额外特性的队列，比如循环队列、阻塞队列、并发队列。他们在很多偏底层系统、框架、中间件开发中起着关键性的作用。比如高性能队列 Disruptor 、Linux 环形缓存，都用到了循环并发队列； Java concurrent 并发包利用 ArrayBlockingQueue 来实现公平锁。

## 顺序队列和链式队列
和栈一样，用数组实现的队列叫做*顺序队列*，用链表实现的队列叫做*链式队列*

```java
public class ArrayQueue {
	private String[] items;
	private int n = 0;
	
	private int head = 0;
	private int tail = 0;

	public ArrayQueue(int capacity) {
		items = new String[capacity];
		n = capacity;
	}

	public boolean enqueue(String item) {
		if (tail == n) return false;
		items[tail] = item;
		++tail;
		return true;
	}

	public String dequeue(String item) {
		if (head == tail) return null;
		String ret = items[head];
		++head;
		return ret;
	}
}
```

在顺序队列中，当队列满时，做一次*数据搬运*即可

```java
public boolean enqueue(String item) {
	if (tail == n) {
		if (head == 0) return false;
		for (int i = head; i < tail; ++i) {
			items[i-head] = items[i];
		}
		tail -= head;
		head = 0;
	}
	
	items[tail] = item;
	++tail;
	return true;
}
```

*基于链表的队列实现方式*

入队时，`tail->next = new_node, tail = tail->next`
出对时，`head = head->next`

## 循环队列

通过循环队列可以避免数据搬移操作。需要确定好队空和队满的判定条件。

队空的判断条件是`head == tail`，队满的条件`(tail+1)%n == head`

```java
public class CircularQueue {
	private String[] items;
	private int n = 0;
	
	private int head = 0;
	private int tail = 0;
	
	public CircularQueue(int capacity) {
		items = new String[capacity];
		n = capacity;
	}

	public boolean enqueue(String item) {
		if ((tail + 1) % n == head) return false;
		items[tail] = item;
		tail = (tail + 1) % n;
		return true;
	}

	public String dequeue() {
		if (head == tail) return null;
		String rett = items[head];
		head = (head + 1) % n;
		return ret;
	}
}
```

## 阻塞队列和并发队列
 *阻塞队列*

阻塞队列就是在队列的基础上加上了阻塞操作。在队列为空的时候，从队头取数据会被阻塞。直到队列中有了数据才能返回；如果队列满了，那么插入数据的操作会被阻塞，直到有空位再插入数据。

![](https://static001.geekbang.org/resource/image/5e/eb/5ef3326181907dea0964f612890185eb.jpg)

上述定义就是一个“生产者 - 消费者模型”。

*并发队列*

在多线程情况下，会有多个线程同时操作队列，这个时候就会存在线程安全问题。

线程安全的队列叫做并发队列。最简单的实现方式就是直接在 `enqueue()`、`dequeue()` 方法上加锁，但是锁粒度大并发度会比较低，同一时刻仅允许一个存或者取操作。

## 线程池没有空闲线程时，新任务该如何处理？

一般有两种策略。第一种是非阻塞的方式，直接拒绝任务请求；另一种是阻塞的处理，将请求排队，等到有空闲线程时，取出排队的请求继续处理
