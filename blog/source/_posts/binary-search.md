---
title: Leetcode 二分查找专题
tags: 
	- 算法
	- 二分查找 
---
# Leetcode 二分查找专题
## 背景
### 最简单的例子
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。
```java
class Solution {
    public int search(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) r = mid - 1;
            else if (nums[mid] < target) l = mid + 1;
        } 
        return -1;
    }
}
```
### 识别和模板介绍
二分查找是一种在每次比较后将查找空间一分为二的算法。每次需要查找集合中的索引或元素时，都应该考虑二分查找。如果集合是无序的，可以在使用二分查找之前先对其进行排序。

**成功的二分查找的 3 个部分**

二分查找一般由三个主要部分组成：
1. 预处理 —— 如果集合未排序，先进行排序
2. 二分查找 —— 使用循环或递归在每次比较将查找空间划分为两半
3. 后处理 —— 在剩余空间中确定可行的候选者

<!-- more -->
## 模板一
### 二分查找模板 1
```java
int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0) return -1;
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

**关键属性**

- 二分查找的最基础和最基本的形式
- 查找条件可以在不与元素的两侧进行比较的情况下确定（或使用它周围的特定元素）
- 不需要后处理，因为每一步中，你都在检查是否找到了元素。如果到达末尾，则知道未找到该元素

**区分语法**

- 初始条件： `left = 0, right = length - 1`
- 终止：`left > right`
- 向左查找：`right = mid - 1`
- 向右查找：`left = mid + 1`

### x 的平方根
实现 int sqrt(int x) 函数。
计算并返回 x 的平方根，其中 x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。
```java
class Solution {
    public int mySqrt(int x) {
        int l = 1, r = x, ans = 0;
        if (x == 0) return 0;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (mid <= x / mid) {
                l = mid + 1;
                ans = mid;
            }
            else {
                r = mid - 1;
            }
        }
        return ans;
    }
}
```

### 猜数字大小
我们正在玩一个猜数字游戏。 游戏规则如下：
我从 1 到 n 选择一个数字。 你需要猜我选择了哪个数字。
每次你猜错了，我会告诉你这个数字是大了还是小了。
你调用一个预先定义好的接口 `guess(int num)`，它会返回 3 个可能的结果（-1，1 或 0）：
> -1 : 我的数字比较小
> 1 : 我的数字比较大
> 0 : 恭喜！你猜对了！

```java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        if (guess(0) == 0) return 0;
        int l = 1, r = n;
        while (l <= r) {
            int mid = (l + r) >>> 1;
            if (guess(mid) == 0) return mid;
            else if (guess(mid) == -1) r = mid - 1;
            else l = mid + 1;
        }
        return 0;
    }
}
```

### 搜索旋转排序数组
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。
搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 `-1` 。
你可以假设数组中不存在重复的元素。
你的算法时间复杂度必须是 `O(log n)` 级别。
```java
class Solution {
    public int search(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[l] <= nums[mid]) {
                if (nums[mid] > target && nums[l] <= target) {
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            } else {
                if (nums[mid] < target && nums[r] >= target) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
        }
        return -1;
    }
}
```
## 模板二
### 二分查找模板 2
```java
int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0) return -1;
    int left = 0, right = nums.length;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid;
    }
    
    if (left != nums.length && nums[left] = target) return left;
    return - 1;
}
```
模板 #2 是二分查找的高级模板。它用于查找需要访问数组中当前索引及其直接右邻居索引的元素或条件。

**关键属性**

- 一种实现二分查找的高级方法
- 查找条件需要访问元素的直接右邻居
- 使用元素的右邻居来确定是否满足条件，并决定是向左还是向右
- 保证查找空间在每一步中至少有 2 个元素
- 需要进行后处理。当你剩下 1 个元素时，循环/递归结束。需要评估剩余元素是否符合条件

**区分语法**

- 初始条件：`left = 0, right = length`
- 终止：`left == right`
- 向左查找：`right = mid`
- 向右查找：`left = mid + 1`
