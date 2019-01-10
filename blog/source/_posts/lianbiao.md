---
title: 《数据结构与算法之美 链表篇笔记》
tag:
	- 算法
---
# 链表
## 缓存淘汰策略
* 先进先出策略 FIFO(First In, First Out)
* 最少使用策略 LFU(Least Frequently Used)
* 最近最少使用 LRU(Least Recently Used)

## 链表与数组的区别
### 从底层的存储结构
数组需要一块连续的内存空间，对内存的要求比较高。

而链表并不需要一块连续的内存空间，它通过“指针”将一组零散的内存块串联起来使用

![](https://static001.geekbang.org/resource/image/d5/cd/d5d5bee4be28326ba3c28373808a62cd.jpg)
<!-- more -->

## 单链表

每个链表的结点除了存储数据外，还需要记录链上的下一个结点的地址，这个记录下个结点地址的指针叫做后继指针 next

![](https://static001.geekbang.org/resource/image/b9/eb/b93e7ade9bb927baad1348d9a806ddeb.jpg)

头结点用来记录链表的基地址；尾结点的指针指向空地址 NULL。

数组的插入删除操作，时间复杂度为 O(n) ，而链表的插入删除，只需要考虑相邻结点的指针改变，所以时间复杂度为 O(1)。

![](https://static001.geekbang.org/resource/image/45/17/452e943788bdeea462d364389bd08a17.jpg)

但是访问元素就没有数组高效了

## 循环链表
循环链表是一个特殊的单链表，唯一的区别在尾结点，尾结点的指针指向了链表的头结点。

![](https://static001.geekbang.org/resource/image/86/55/86cb7dc331ea958b0a108b911f38d155.jpg)

当解决的问题具有环形结构特点时，如约瑟夫问题，使用循环链表就简洁的多。

## 双向链表
单链表只有一个方向，每个结点只有一个后继指针 next 指向后面的结点。而双向链表有两个方向，除了后继指针 next 外，还有一个前驱指针 prev 指向前一个结点。

![](https://static001.geekbang.org/resource/image/cb/0b/cbc8ab20276e2f9312030c313a9ef70b.jpg)

**用空间换时间**

## 如何写好链表 

### 技巧一：理解指针或引用的含义
将某个变量赋值给指针，实际上就是将这个变量的地址赋值给指针，或者反过来说，指针中存储了这个变量的内存地址，指向了这个变量，通过指针就能找到这个变量。

### 技巧二：警惕指针丢失和内存泄漏
如图，希望在结点 a 和 结点 b 之间插入结点 x，假设当前指针 p 指向结点 a。如果代码如下实现，则会发生指针丢失和内存泄漏

```c
p->next = x;
x->next = p->next;
```

所以插入结点时，一定要注意操作的顺序。同理，删除链表结点时，也要记得手动释放内存空间。

### 技巧三：利用哨兵简化实现难度
如果我们在结点 p 之后插入一个新的结点：

```c
new_node->next = p->next;
p->next = new_node;
```

当向一个空链表插入第一个结点，刚刚的逻辑就不能用了

```c
if (head == null) {
	head = new_node;
}
```

如果删除结点 p 的后继节点：

```c
p->next = p->next->next;
```

同样如果是最后一个结点，上述代码也不能奏效：

```c
if (head->next == null) {
	head = null;
}
```

> 综上：链表的插入删除，需要对插入第一个结点和删除最后一个结点进行特殊处理

但上述的方法很繁琐，这时候哨兵就要登场了，如果我们引入哨兵，在任何时候，不管链表是否为空，head 指针都会指向这个哨兵结点。我们把这种有哨兵结点的链表叫**带头链表**。

哨兵结点是不存数据的：

![](https://static001.geekbang.org/resource/image/7d/c7/7d22d9428bdbba96bfe388fe1e3368c7.jpg)

```c
// 在数组 a 中查找 key，返回 key 所在位置
// 其中，n 表示数组 a 的长度
int find(char* a, int n, char key) {
	if (a == null || n <= 0) {
		return -1;
	}
	
	int i = 0;
	while(i < n) {
		if (a[i] == key) {
			return i;
		}
		i++;
	}
	return -1;
}
```

```c
int find(char* a, int n, char key) {
	if (a == null || n <= 0) {
		return -1;
	}

	if (a[n-1] == key) {
		return n-1;
	}

	char tmp = a[n-1];
	a[n-1] = key;
	int i = 0;
	while (a[i] != key) {
		++i;
	}

	a[n-1] = tmp;
	
	if (i == n-1) {
		return -1;
	} else {
		return i;
	}
}
```

比较上述两段代码，第二段代码通过哨兵 a[n-1] = key，成功省掉了一个比较 i < n.

### 技巧四：重点留意边界条件处理

经常用来检查链表代码是否正确的边界有：

* 如果链表为空时
* 如果链表只包含一个结点时
* 如果链表只包含两个结点时
* 代码逻辑在处理头结点和尾结点时

### 技巧五：举例画图，辅助思考

### 技巧六：多写多练，没有捷径

* 单链表反转
* 链表中环的检测
* 两个有序的链表合并
* 删除链表倒数第 n 个节点
* 求链表的中间结点
