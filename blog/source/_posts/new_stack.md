---
title: 《数据结构与算法之美 栈篇笔记》
tags:
    - 算法
---
## 如何理解“栈”
后进者先出，先进者后出，这就是典型的“栈”结构。

![](https://static001.geekbang.org/resource/image/3e/0b/3e20cca032c25168d3cc605fa7a53a0b.jpg)

栈是一种“操作受限”的线性表，只允许一端插入和删除数据。
<!--more-->

## 如何实现一个“栈”
栈也可以用数组和链表来实现，用数组实现的栈叫做**顺序栈**，用链表实现的栈叫做**链式栈**

```java
public class ArrayStack {
	private String[] items;
	private int count;
	private int n;
	
	public ArrayStack(int n) {
		this.items = new String[n];
		this.n = n;
		this.count = 0;
	}
	
	public  boolean push(String item) {
		if (count == n) return false;
		items[count] = item;
		++count;
		return true;
	}
	
	public String pop() {
		if (count == 0) return false;
		String tmp = items[count-1];
		--count;
		return tmp;
	}
}
```

### 复杂度

入栈和出栈过程中，只需要一两个临时存储空间，所以空间复杂度为 O(1)。

入栈和出栈只涉及栈顶的数据操作，所以时间复杂度为 O(1)。

## 支持动态扩容的顺序栈
上面那个栈是一个固定大小的栈，也就是说初始化栈的时候就要指定栈的大小。当栈满的时候无法再添加数据。

链式栈的大小虽然不受限，但要存储 next 指针，内存消耗相对较多。

与动态扩容数组的想法一样：

![](https://static001.geekbang.org/resource/image/b1/da/b193adf5db4356d8ab35a1d32142b3da.jpg)

## 栈在函数调用中的应用
栈作为一种比较基础的数据结构，应用场景很多，其中较为经典的是**函数调用栈**

操作系统给每个线程分配了一块独立的内存空间，这块内存被组织成“栈”这种结构，用来存储函数调用时的临时变量。没进入一个函数，就会将临时变量作为一个栈帧入栈，当被调用函数执行完成，返回之后，将这个函数对应的栈帧出栈。

```c
int main() {
	int a = 1;
	int ret = 0;
	int res = 0;
	ret = add(3, 5);
	res = a + ret;
	printf("%d", res);
	return 0;
}

int add(int x, int y) {
	int sum = 0;
	sum = x + y;
	return sum;
}
```

main() 函数调用了 add() 函数，获取计算结果，并且与临时变量 a 相加，最后打印 res 的值。

![](https://static001.geekbang.org/resource/image/17/1c/17b6c6711e8d60b61d65fb0df5559a1c.jpg)

## 栈在表达式求值中的应用
编译器通过两个栈来实现，其中一个保存操作数，另一个保存运算符。我们从左向右遍历表达式，当遇到数字，我们就直接压入操作数栈；当遇到运算符，就与运算符栈的栈顶元素进行比较。

如果比运算符栈顶元素的优先级高，就将当前运算符压入栈；如果比运算符栈顶元素的优先级低或者相同，从运算符栈中取栈顶运算符，从操作数栈的栈顶取两个操作数，然后进行计算，再把计算完的结果压入操作数栈中。

举个栗子

![](https://static001.geekbang.org/resource/image/bc/00/bc77c8d33375750f1700eb7778551600.jpg)

## 栈在括号匹配中的应用
用栈来保存未匹配的左括号，从左到右依次扫描。当扫描到左括号压栈，当扫描到右括号，从栈顶取出一个左括号，如果能匹配，则继续扫描，如果不能匹配或者栈中没有数据，则说明为非法个事。

## 如何实现浏览器的前进后退
用栈
