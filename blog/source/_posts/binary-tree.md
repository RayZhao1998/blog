---
title: Binary Tree 二叉树
tags: 
	- 算法
	- 二叉树 
---

### Binary Tree 二叉树

```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
```

#### 树的遍历

- 深度优先
  - 前序(pre-order): 先根后左再右
  - 中序(in-order): 先左后根再右
  - 后序(post-order): 先左后右再根
- 广度优先: 先访问根节点,沿着树的宽度遍历子节点,直到所有节点均被访问为止.
<!-- more -->

```python
class TreeNode:
    def __init__(self, val):
		self.val = val
        self.left, self.right = None, None
        
class Traversal(object):
    def __init__(self):
        self.traverse_path = list()
        
    def preorder(self, root):
        self.traverse_path.append(root.val)
        self.preorder(root.left)
        self.preorder(root.right)
        
    def inorder(self, root):
        self.inorder(root.left)
        self.traverse_path.append(root.val)
        self.inorder(root.right)
        
    def postorder(self, root):
        self.postorder(root.left)
        self.postorder(root.right)
        self.traverse_path.append(root.val)
```



#### Binary Search Tree 二叉查找树

每个节点的键都大于等于左子树中任意节点的键,小于右子树中任意节点的键.

使用中序遍历可以得到有序数列
