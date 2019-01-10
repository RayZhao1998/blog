---
title: C++ vector 学习
tags:
    - C++
---

最近准备刷题了，左想右想还是选择用 C++ 刷一遍，一方面是因为像 Swift 这种语言用来做算法题不是那么的顺手，而 Python 又有很多黑科技，能够真正用来练习数据结构和算法的就属 C++ 和 Java 了。但是 Java 的语法我很不熟练，所以最后还是选择用 C++ 来刷题

之前在做 Leetcode 上的题的时候，看题解里很多人用到了 vector， 但是我们面向对象课上老师并没有介绍 vector 相关的东西，所以我觉得还是有必要花点时间了解和应用一下。

## 什么是 vector
Vector 是一个封装了动态大小数组的顺序容器，可以将它理解成能够存放任意类型的动态数组。

<!-- more -->

## 容器特性
### 1. 顺序序列
按严格的线性顺序排序。可以通过元素在序列中的位置访问对应的元素。
### 2. 动态数组
支持对序列中的任意元素进行快速直接访问。提供了在序列末尾相对快速地添加/ 删除元素的操作。
### 3. 能够感知内存分配器
容器使用一个内存分配器对象来动态地处理它的存储需求。

## 基本用法
```c
#include <vector>
using namespace std;
```

### 实例
#### 1. `pop_back()` & `push_back(elem)`实例在容器最后移除和插入数据
```c
#include <string.h>
#include <vector>
#include <iostream>
using namespace std;

int main() {
	vector<int> obj;
	for (int i = 0; i < 10; i++) {
		obj.push_back(i);
		cout<<obj[i]<<",";
	}
	
	for (int i = 0; i < 5; i++) {
		obj.pop_back();
	}
	
	cout<<"\n"<<endl;
	
	for(int i = 0; i < obj.size(); i++) {
		cout<<obj[i]<<",";
	}
	
	return 0;
}
```

#### 2. `clear()` 清除容器中所有数据

```c
#include <string.h>
#include <vector>
#include <iostream>
using namespace std;

int main() {
	vector<int> obj;
	for (int i = 0; i < 10; i++) {
		obj.push_back(i);
		cout<<obj[i]<<",";
	}
	
	obj.clear();
	
	for (int i = 0; i < obj.size(); i++) {
		obj.pop_back();
	}
	
	return 0;
}
```

#### 3. 排序
```c
#include <string.h>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
	vector<int> obj;
	obj.push_back(1);
	obj.push_back(3);
	obj.push_back(0);
	
	sort(obj.begin(), obj.end());
	for (int i = 0; i < obj.size(); i++) {
		cout<<obj[i]<<",";
	}
	
	reverse(obj.begin(), obj.end());
	for (int i = 0; i < obj.size(); i++) {
		cout<<obj[i]<<",";
	}
}
```

#### 4. 访问（数组访问 & 迭代器）
```c
#include <string.h>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
	vector<int> objl
	for(int i = 0; i < 10; i++) {
		obj.push_back(i);
	}
	
	for(int i = 0; i < 10; i++) {
		cout<<obj[i]<<" ";
	}
	
	vector<int>::iterator it;
	for (it = obj.begin(); it != obj.end(); it++) {
		cout<<*it<<" ";
	}
	
	return 0;
}
```
