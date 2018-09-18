---
title: 162. Find Peak Element 
tags: 
	- 算法
	- 二分查找 
	- Leetcode
---
# 162. Find Peak Element
## Description
峰值元素是指其值大于左右相邻的元素。找到峰值元素并返回其索引。

示例1
```
输入：nums = [1, 2, 3, 1]
输出：2
```
示例2
```
输入：nums = [1, 2, 1, 3, 5, 6, 4]
输出：1 或 5
```

## Solution
### Approach 1: 线性扫描
**case1**：所有元素降序，第一个元素为峰值元素
![case1](https://leetcode.com/problems/find-peak-element/Figures/162/Find_Peak_Case1.PNG)
**case2**：所有元素升序，最后一个元素为峰值元素
![-w570](https://leetcode.com/problems/find-peak-element/Figures/162/Find_Peak_Case2.PNG)
**case3**：峰值出现在中间某个位置
![-w576](https://leetcode.com/problems/find-peak-element/Figures/162/Find_Peak_Case3.PNG)
<!-- more -->
这种情况，从左到右首先为递增的情况，到达峰值后下降，因此在这种情况下，从左到右遍历，一旦出现`nums[i] > nums[i+1]`这种情况即返回`i`


```java
public class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] > nums[i + 1])
                return i;
        }
        return nums.length - 1;
    }
}
```
#### Complexity Analysis
- Time complexity: O(n)
- Space complexity: O(1)

### Approach 2: 二分查找
如果中间元素位于一个上升序列，说明峰值在这个元素的右边，于是就可以将搜索空间缩小到中间右边，然后在右子数组中重复同样的操作。

**迭代**
```java
public class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0; r = nums.length - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (nums[mid] > nums[mid + 1]) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }
}
```
### Complexity Analysis
- Time complexity: O(log2(n))
- Space complexity： O(1)
**递归**
```java
public class Solution {
    public int findPeakElement(int[] nums) {
        return search(nums, 0, nums.length - 1);
    }
    
    public int search(int[] nums, int l, int r) {
        if (l == r)
            return l;
        int mid = (l + r) / 2;
        if (nums[mid] > nums[mid + 1]) 
            return search(nums, l, mid);
        return search(nums, mid + 1; r);
    }
}
```

### Complexity Analysis
- Time complexity: O(log2(n))
- Space complexity： O(log2(n))
