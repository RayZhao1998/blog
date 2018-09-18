---
title: Linked-list 链表
tags: 
	- 算法
	- 链表 
---

### 链表

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
```

#### 链表的操作

##### 反转链表

1. 单向链表

   ```python
   def reverse(self, head):
       prev = None
       while head:
           // 先用 temp 保存 head 的下一个节点,保证单链表不会因为失去 head 节点的原 next 节点就此断裂
           temp = head.next
           // 让 head 从指向 next 变为指向 pre
           head.next = prev
           // head 指向 pre 后,就继续一次反转下一个节点
           // 让 pre, head, next 依次向后移动一个节点
           prev = head
           head = temp
       return prev
   ```
<!-- more -->

2. 双向链表

   交换 next 和 prev 域

   ```python
   class DListNode:
       def __init__(self, val):
           self.val = val
           self.next = None
       
       def reverse(self, head):
           curt = None
           while head:
               curt = head
               head = cur.next
               curt.next = curt.prev
               curt.prev = head
   ```

   

##### 删除链表中节点

复制一个和要删除节点值一样的节点,然后删除,然后只需要把`prev->next = prev->next->next`

**链表指针的鲁棒性**

- 当访问链表中某个节点`curt.next`时,一定要先判断 curt 是否为 null
- 全部操作结束后,判断是否有环;若有环,则置其中一端为null

**Dummy Node**

Dummy Node 就是在链表表头 head 前加一个节点指向 head.

Dummy Node 的使用多针对单链表没有前向指针的问题,保证链表的 head 不会在删除操作中丢失.

还有一种就是用 Dummy Node 进行 head 的删除操作,比如 Remove Duplicates From Sorted List II, 一般的方法 current = current.next 是无法删除 head 元素的,这时需要在 head 之前放一个 Dummy Node

##### 快慢指针

一个快指针、一个慢指针,快指针每次移动2,慢指针每次移动1

- 快速找出中间节点,`*fast`到末尾时,`*slow`正好在中间
- 判断是否有环,若有环,最终`*fast`将追上`*slow`,否则最后`*fast=NULL`

```python
class NodeCircle:
    def __init__(self, val):
        self.val = val
        self.next = None
        
	    def has_circle(self, head):
            slow = head
            fast = head
            while (slow and fast):
                fast = fast.next
                slow = slow.next
                if fast:
                    fast = fast.next
                if fast == slow:
                    break
            if fast and slow and (fast == slow):
                return true
            else:
                return false
```


