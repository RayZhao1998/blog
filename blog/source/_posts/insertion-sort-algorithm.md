---
title: 必会算法之插入排序
tags: 
	- 算法
	- 必会算法
---

> 翻译自[Top Algorithm/Data Structures/Concepts every computer science student should know](http://www.techiedelight.com/top-algorithms-data-structures-concepts-computer-science/)————Insert Sort Algorithm

### 插入排序

插入排序是一种稳定的内部排序算法,可以一次构建最终排序的数组.它在性能方面并不是最好的,但实际上它比大多数其他简单的O(n2)算法(选择排序和冒泡排序)更有效率.插入排序也用于混合排序,它结合了不同的排序算法来提高性能.

<!-- more -->

它是一个著名的在线算法(online algorithm),因为它可以在接收列表时对其进行排序.在所有其他算法中,我们需要在应用之前向排序算法提供所有元素.但是插入排序允许我们从部分元素集开始,对它进行排序(称为部分排序集),我国我们需要,我们可以插入更多的元素(这些元素是新的元素集,在在排序开始时不在内存中),并对这些元素进行排序.在现实世界中,需要分类的数据通常不是静态的,而是动态的.如果在排序过程中甚至插入一个额外的元素,其他算法就不会很容易地作出反应.但是只有这个算法没有中断,并且可以很好地响应额外的元素.

#### 它是如何工作的?

这个想法是将数组分成两个子集——分类子集和未排序子集.排序子集只包含索引为0的元素.然后对于每个迭代,插入排序从未排序子集中移除下一个元素,找到它应该在的位置,插入到该子集中.然后不断重复,知道没有输入元素保留.

#### 循环实现

```java
import java.util.Arrays;
 
class InsertionSort
{
    // Function to perform insertion sort on arr[]
    public static void insertionSort(int[] arr)
    {
        // Start from the second element
        // (element at index 0 is already sorted)
        for (int i = 1; i < arr.length; i++)
        {
            int value = arr[i];
            int j = i;
 
            // Find the index j within the sorted subset arr[0..i-1]
            // where element arr[i] belongs
            while (j > 0 && arr[j - 1] > value)
            {
                arr[j] = arr[j - 1];
                j--;
            }
 
            // Note that sub-array arr[j..i-1] is shifted to
            // the right by one position i.e. arr[j+1..i]
 
            arr[j] = value;
        }
    }
 
    public static void main(String[] args)
    {
        int[] arr = { 3, 8, 5, 4, 1, 9, -2 };
 
        insertionSort(arr);
 
        // print the sorted array
        System.out.println(Arrays.toString(arr));
    }
}
```



#### 递归实现

```java
import java.util.Arrays;
 
class InsertionSort
{
    // Recursive function to perform insertion sort on sub-array arr[i..n]
    public static void insertionSort(int[] arr, int i, int n)
    {
        int value = arr[i];
        int j = i;
 
        // Find index j within the sorted subset arr[0..i-1]
        // where element arr[i] belongs
        while (j > 0 && arr[j - 1] > value)
        {
            arr[j] = arr[j - 1];
            j--;
        }
 
        arr[j] = value;
 
        // Note that subarray arr[j..i-1] is shifted to
        // the right by one position i.e. arr[j+1..i]
 
        if (i + 1 <= n) {
            insertionSort(arr, i + 1, n);
        }
    }
 
    public static void main(String[] args)
    {
        int[] arr = { 3, 8, 5, 4, 1, 9, -2 };
 
        // Start from second element (element at index 0 
        // is already sorted)
        insertionSort(arr, 1, arr.length - 1);
 
        // print the sorted array
        System.out.println(Arrays.toString(arr));
    }
}
```


