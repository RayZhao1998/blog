---
title: 必会算法之合并排序
tags: 
	- 算法
	- 必会算法
---

> 翻译自[Top Algorithm/Data Structures/Concepts every computer science student should know](http://www.techiedelight.com/top-algorithms-data-structures-concepts-computer-science/)————Merge Sort Algorithm

### 合并排序算法

合并排序是一种高效的内部排序算法,它产生一个稳定的排序,这意味着如果两个元素具有相同的值,它们在输出中的相对位置与输入相同.换句话说,具有等值的元素的相对顺序保留在排序的输出中.

<!-- more -->

#### 合并时如何工作的

合并排序时一个分治法.像所有的分割和征服算法(conquer algorithms)一样,合并排序将一个大数组分成两个较小的子数组,然后递归地对子数组进行排序.基本上,整个过程中涉及两个步骤

1. 将未排序的数组分为 n 个子数组,每个子数组的大小为1
2. 重复合并子数组,以生成新的排序子数组,直到只剩下一个子数组,这个子数组就是我们的排序数组.

下图显示了用于对7个整数进行排序的递归合并排序算法的自顶向下视图.

![](https://i2.wp.com/www.techiedelight.com/wp-content/uploads/Merge-Sort-Steps.png?zoom=2&resize=668%2C633&ssl=1)

下面是合并排序算法的 Java 实现

```java
import java.util.Arrays;

class MergeSort
{
	public static void merge(int[] arr, int[] aux, int low, int mid, int high)
	{
		int k = low, i = low, j = mid + 1;
		while(i <= mid && j <= high)
		{
			if (arr[i] < arr[j]) {
				aux[k++] = arr[i++];
			}
			else {
				aux[k++] = arr[j++];
			}
		}
		
		while (i <= mid) {
			aux[k++] = arr[i++];
		}
		
		for (i = low; i <= high; i++)
		{
			arr[i] = aux[i];
		}
	}
	
	public static void mergeSort(int[] arr, int[] aux, int low, int high)
	{
		if (high == low)
		{
			return;
		}
		
		int mid = (low + ((high - low) >> 1));
		
		mergeSort(arr, aux, low, mid);
		mergeSort(arr, aux, mid+ 1 , high);
		
		merge(arr, aux, low, mid, high);
	}
	
	public static boolean isSorted(int[] arr)
	{
		int prev = arr[0];
		for (int i = 1; i < arr.length; i++)
		{
			if (prev > arr[i])
			{
				System.out.println("MergeSort Fails!!");
				return false;
			}
			prev = arr[i];
		}
		
		return true;
	}
	
	public static void main(String[] args)
	{
		int[] arr = {12, 3, 18, 24, 0, 5, -2};
		int[] aux = Arrays.copyOf(arr, arr.length);
		
		mergeSort(arr, aux, 0, arr.length - 1);
		
		if (isSorted(arr)) {
			System.out.println(Arrays.toString(arr));
		}
	}
}
```

#### 合并排序性能

最坏的情况时间复杂度为O(nlog(n)),递推关系式为
$$
T(n) = 2T(n/2) + cn = O(nlog(n)
$$
空间复杂度为O(n)


