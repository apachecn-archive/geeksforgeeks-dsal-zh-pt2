# 数组中每个元素右侧较大元素的计数

> 原文:[https://www . geesforgeks . org/数组中每个元素右侧的较大元素计数/](https://www.geeksforgeeks.org/count-of-larger-elements-on-right-side-of-each-element-in-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算每个数组元素**右侧**的**个较大元素**的数量。

**示例:**

> **输入:** arr[] = {3，7，1，5，9，2}
> **输出:** {3，1，3，1，0，0}
> **解释:**
> 对于 arr[0]，右边大于它的元素是{7，5，9}。
> 对于 arr[1]，右边唯一比它大的元素是{9}。
> 对于 arr[2]，右边大于它的元素是{5，9，2}。
> 对于 arr[3]，右边唯一大于它的元素是{9}。
> 对于 arr[4]和 arr[5]，右侧不存在更大的元素。
> 
> **输入:** arr[] = {5，4，3，2}
> **输出:** {0，0，0，0}

**天真方法:**最简单的方法是[使用两个循环迭代所有数组元素](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个数组元素，计算其右侧大于它的元素数量，然后打印出来。
***时间复杂度:** O(N <sup>2</sup> )
**辅助空间:** O(1)*

**高效途径:**使用[合并排序](https://www.geeksforgeeks.org/merge-sort/)的概念，按照降序排列，可以解决问题。按照下面给出的步骤解决问题:

*   初始化一个数组 **count[]** ，其中 **count[i]** 为每个 **arr[i]** 存储右侧更大元素的相应计数
*   取索引 **i** 和 **j** ，比较数组中的元素。
*   如果较高的索引元素大于较低的索引元素，则所有较高的索引元素都将大于该较低索引之后的所有元素。
*   由于左边部分已经排序，将较低索引元素后的元素计数添加到较低索引的**计数[]** 数组中。
*   重复以上步骤，直到整个数组被排序。
*   最后打印**计数[]** 数组的值。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

public class GFG {

    // Stores the index & value pairs
    static class Item {

        int val;
        int index;

        public Item(int val, int index)
        {
            this.val = val;
            this.index = index;
        }
    }

    // Function to count the number of
    // greater elements on the right
    // of every array element
    public static ArrayList<Integer>
    countLarge(int[] a)
    {
        // Length of the array
        int len = a.length;

        // Stores the index-value pairs
        Item[] items = new Item[len];

        for (int i = 0; i < len; i++) {
            items[i] = new Item(a[i], i);
        }

        // Stores the count of greater
        // elements on right
        int[] count = new int[len];

        // Perform MergeSort operation
        mergeSort(items, 0, len - 1,
                  count);

        ArrayList<Integer> res
            = new ArrayList<>();

        for (int i : count) {
            res.add(i);
        }

        return res;
    }

    // Function to sort the array
    // using Merge Sort
    public static void mergeSort(
        Item[] items, int low int high,
        int[] count)
    {

        // Base Case
        if (low >= high) {
            return;
        }

        // Find Mid
        int mid = low + (high - low) / 2;

        mergeSort(items, low, mid,
                  count);
        mergeSort(items, mid + 1,
                  high, count);

        // Merging step
        merge(items, low, mid,
              mid + 1, high, count);
    }

    // Utility function to merge sorted
    // subarrays and find the count of
    // greater elements on the right
    public static void merge(
        Item[] items, int low, int lowEnd,
        int high, int highEnd, int[] count)
    {
        int m = highEnd - low + 1; // mid

        Item[] sorted = new Item[m];

        int rightCounter = 0;
        int lowInd = low, highInd = high;
        int index = 0;

        // Loop to store the count of
        // larger elements on right side
        // when both array have elements
        while (lowInd <= lowEnd
               && highInd <= highEnd) {

            if (items[lowInd].val
                < items[highInd].val) {
                rightCounter++;
                sorted[index++]
                    = items[highInd++];
            }
            else {
                count[items[lowInd].index] += rightCounter;
                sorted[index++] = items[lowInd++];
            }
        }

        // Loop to store the count of
        // larger elements in right side
        // when only left array have
        // some element
        while (lowInd <= lowEnd) {

            count[items[lowInd].index] += rightCounter;
            sorted[index++] = items[lowInd++];
        }

        // Loop to store the count of
        // larger elements in right side
        // when only right array have
        // some element
        while (highInd <= highEnd) {

            sorted[index++] = items[highInd++];
        }

        System.arraycopy(sorted, 0, items,
                         low, m);
    }

    // Utility function that prints
    // the count of greater elements
    // on the right
    public static void
    printArray(ArrayList<Integer> countList)
    {

        for (Integer i : countList)
            System.out.print(i + " ");

        System.out.println();
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int arr[] = { 3, 7, 1, 5, 9, 2 };
        int n = arr.length;

        // Function Call
        ArrayList<Integer> countList
            = countLarge(arr);

        printArray(countList);
    }
}
```

**Output:**

```
3 1 3 1 0 0

```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*