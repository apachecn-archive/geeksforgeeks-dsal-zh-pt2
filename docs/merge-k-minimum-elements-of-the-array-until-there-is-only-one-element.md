# 合并数组的 K 个最小元素，直到只有一个元素

> 原文:[https://www . geeksforgeeks . org/merge-k-最少元素数组-直到只有一个元素/](https://www.geeksforgeeks.org/merge-k-minimum-elements-of-the-array-until-there-is-only-one-element/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是合并数组的 K 个最小元素，直到数组中只剩下一个元素。

**注意:**如果不可能只合并成一个元素，那么打印-1。

> **输入:** arr[] = {3，2，4，1}，K = 2
> **输出:** 10
> **解释:**
> 合并数组的 K 个最小元素({3，2，4，1}) = 1 + 2 = 3
> 合并后数组将为{3，3，4}
> 合并数组的 K 个最小元素({3，3，4}) = 3 + 3 = 6
> 合并后数组将
> 
> **输入:** arr[] = {3，2，4，1}，K = 3
> **输出:** -1
> **说明:**
> 合并后会剩下两个元素{6，4}，无法进一步合并。

**方法:**思路是[对数组](https://www.geeksforgeeks.org/merge-sort/)进行排序，然后将数组的前 K 个最小元素合并成一个元素，然后在[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的帮助下，将元素插入到数组中其排序后的位置进入数组。同样，重复此步骤，直到数组中只剩下一个元素。如果最后剩下的元素少于 K 个，那么返回-1。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to merge the
// K minimum elements of the Array
// until there is only one element
// is left in the array

// Imports
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to merge the element
    // of the array until there is
    // only one element left in array
    public static int mergeStones(
        List<Integer> list, final int k) {

        // Sorting the array
        Collections.sort(list);
        int cost = 0;

        // Loop to merge the elements
        // until there is element
        // greater than K elements
        while(list.size() > k) {
            int sum = 0;

            // Merging the K minimum 
            // elements of the array
            for(int i = 0; i < k; i++) {
                sum += list.get(i);
            }

            // Removing the K minimum 
            // elements of the array
            list.subList(0, k).clear();

            // Inserting the merged 
            // element into the array
            insertInSortedList(list, sum); 
            cost += sum;
        }

        // If there is only K element
        // left then return the element
        if(list.size() == k) {
            cost += list.stream().reduce(
                         0, Integer::sum);
            return cost;
        } else {
            return -1;
        }
    }

    // Function insert the element into
    // the sorted position in the array
    public static void insertInSortedList(
        List<Integer> sortedList, int item) {
        int len = sortedList.size();
        insertInSortedList(sortedList, item, 
                                 0, len - 1);
    }

    // Utility function to insert into the
    // array with the help of the position
    public static void insertInSortedList(
        List<Integer> sortedList, int item, 
                       int start, int end) {
        int mid = (int) ((end - start)/ 2.00);
        if(mid == 0 || 
             (mid == sortedList.size() - 1) || 
                sortedList.get(mid) == item) {
            sortedList.add(mid, item);
            return;
        } 
        else if(sortedList.get(mid) < item) {
            insertInSortedList(sortedList, 
                       item, mid + 1, end);
        } else {
            insertInSortedList(sortedList, 
                     item, start, mid - 1);
        }
    }

    // Driver Code
    public static void main(String [] args) {
        List<Integer> stones = new ArrayList<>();
        stones.add(3);
        stones.add(2);
        stones.add(4);
        stones.add(1);
        System.out.println(mergeStones(stones, 3));
        System.out.println(mergeStones(stones, 2));
    }
}
```

**Output:**

```
-1
10

```