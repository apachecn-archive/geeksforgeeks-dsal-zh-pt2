# 根据给定的条件从两个给定的数组中最大化一对的值

> 原文:[https://www . geesforgeks . org/基于给定条件从两个给定数组中获取最大值/](https://www.geeksforgeeks.org/maximize-value-of-a-pair-from-two-given-arrays-based-on-given-conditions/)

给定由 **N** 个整数和一个整数 **K** 组成的两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和**B【】**，任务是通过选择任意一对 **(i，j)** 找到**B[I]+B[j]+ABS(A[I]–A[j])**的最大值，使得**ABS(A[I]–A[j])≤K**

**示例:**

> **输入:** A[] = {5，6，9，10}，B[] = {3，0，10，-10}，K = 1
> **输出:** 4
> **说明:**
> 只能选择两对，即(0，1)和(2，3)，因为 ABS(A[0]–A[1])≤K 和 ABS(A[2]–A[3])≤K .
> 的值
> 对(2，3)的值为 B[2]+B[3]+ABS(A[2]–A[3])= 10+(-10)+1 = 1。
> 因此，所有可能对的最大值为 4。
> 
> **输入:** A[] = {1，2，3，4}，B[] = {0，8，6，9}，K = 2
> **输出:** 19

**天真方法:**最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并对那些满足给定条件的对进行计数。检查完所有对后，打印所有对的计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方式:**对上述方式进行优化，思路是利用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)、[二分搜索法](https://www.geeksforgeeks.org/binary-search/)、[根据数组**A【】**的值对数组进行排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。请注意，从给定的等式中，很明显**B[I]+B[j]+ABS(A[I]–A[j])**等于以下任何值:

*   **B[I]+B[j]+(A[I]–A[j])**
*   **B[I]+B[j]+(A[j]–A[I])**

> 考虑第二个等式:
> 
> **B[I]+B[j]+A[j]–A[I]**=**B[I]–A[I]+(B[j]+A[j])**
> 
> *   这里，观察到对于阵列**A【】**中的每个 **i** ，找到小于等于**A【I】+K**的最右边的值的索引。让最右边的索引为**右边的**。
> *   现在，计算**B[I]–A[I]+B[j]+A[j]**的最大值，其中 **i + 1 < = j < =右侧**。这将给出所选对的最大值。
> *   为了计算每次在一个范围内的最大值，可以使用分段树。

按照以下步骤解决问题:

*   根据数组 **A[]** 的值对所有值 **B[i]** 和 **B[i] + A[i]** 进行排序。
*   将**最大值**初始化为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 存储最终最大答案，并初始化一个[范围最大查询段树](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)存储所有值， **A[i] + B[i]** 。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**A【】**并执行以下操作:
    *   对于每个元素找到索引，说**右**，这样**腹肌(A[I]–A[右]) < = K** 使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。
    *   然后，求 **(A[j] + B[j])** 的最大值，其中 **i+1 < = j < =右**。
    *   更新**最大值**为**最大值=最大值(最大值，B[I]–A[I]+A[j]+B[j])**。
*   完成上述步骤后，打印**最大值**的值作为结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

// Class to store the values of a[i],
// b[i], a[i] + b[i]
class triplet implements Comparable<triplet> {

    int a, b, c;

    // Constructor
    triplet(int a, int b, int c)
    {
        this.a = a;
        this.b = b;
        this.c = c;
    }

    // Sort values according to array
    public int compareTo(triplet o)
    {
        return this.a - o.a;
    }
}

class GFG {

    // Stores the segment tree
    static int seg[];

    // Function to find the maximum
    // possible value according to the
    // given condition
    public static void maxValue(
        int a[], int b[], int n, int k)
    {
        // Initialize triplet array
        triplet arr[] = new triplet[n];

        // Store the values a[i], b[i],
        // a[i] + b[i]
        for (int i = 0; i < n; i++) {

            arr[i] = new triplet(a[i], b[i],
                                 a[i] + b[i]);
        }

        // Sort the array according
        // to array a[]
        Arrays.sort(arr);

        // Build segment tree
        seg = new int[4 * n];
        build(arr, 0, 0, n - 1);

        // Initialise the maxvalue of
        // the selected pairs
        int maxvalue = Integer.MIN_VALUE;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // For each value find the
            // floor(arr[i] + k)
            int right = search(arr,
                               arr[i].a + k);

            // Find the maximum value of
            // the select pairs i and max
            // from (i + 1, right)
            if (right != -1) {

                maxvalue = Math.max(
                    maxvalue, arr[i].b - arr[i].a
                                  + getMax(arr, 0, 0, n - 1,
                                           i + 1, right));
            }
        }

        // Print the maximum value
        System.out.println(maxvalue);
    }

    // Function to search floor of
    // the current value
    public static int search(
        triplet arr[], int val)
    {
        // Initialise low and high values
        int low = 0, high = arr.length - 1;
        int ans = -1;

        // Perform Binary Search
        while (low <= high) {
            int mid = low + (high - low) / 2;

            // If the current value is
            // <= val then store the
            // candidate answer and
            // find for rightmost one
            if (arr[mid].a <= val) {
                ans = mid;
                low = mid + 1;
            }
            else
                high = mid - 1;
        }
        return ans;
    }

    // Function to build segment tree
    public static void build(
        triplet arr[], int index,
        int s, int e)
    {
        // Base Case
        if (s == e) {
            seg[index] = arr[s].c;
            return;
        }
        int mid = s + (e - s) / 2;

        // Build the left and right
        // segment trees
        build(arr, 2 * index + 1, s, mid);
        build(arr, 2 * index + 2, mid + 1, e);

        // Update current index
        seg[index] = Math.max(seg[2 * index + 1],
                              seg[2 * index + 2]);
    }

    // Function to get maximum value
    // in the range [qs, qe]
    public static int getMax(
        triplet arr[], int index, int s,
        int e, int qs, int qe)
    {
        // If segment is not in range
        if (qe < s || e < qs)
            return Integer.MIN_VALUE / 2;

        // If segment is completely
        // inside the query
        if (s >= qs && e <= qe)
            return seg[index];

        // Calculate the maximum value
        // in left and right half
        int mid = s + (e - s) / 2;
        return Math.max(
            getMax(arr, 2 * index + 1,
                   s, mid, qs, qe),
            getMax(arr, 2 * index + 2,
                   mid + 1, e, qs, qe));
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 4, K = 1;
        int A[] = { 5, 6, 9, 10 };
        int B[] = { 3, 0, 10, -10 };

        // Function call
        maxValue(A, B, N, K);
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// Class to store the values of a[i],
// b[i], a[i] + b[i]
public class triplet : IComparable<triplet> {

    public int a, b, c;

    // Constructor
    public triplet(int a, int b, int c)
    {
        this.a = a;
        this.b = b;
        this.c = c;
    }

    // Sort values according to array
    public int CompareTo(triplet o)
    {
        return this.a - o.a;
    }
}

public class GFG {

    // Stores the segment tree
    static int []seg;

    // Function to find the maximum
    // possible value according to the
    // given condition
    public  void maxValue(
        int []a, int []b, int n, int k)
    {
        // Initialize triplet array
        triplet []arr = new triplet[n];

        // Store the values a[i], b[i],
        // a[i] + b[i]
        for (int i = 0; i < n; i++) {

            arr[i] = new triplet(a[i], b[i],
                                 a[i] + b[i]);
        }

        // Sort the array according
        // to array []a
        Array.Sort(arr);

        // Build segment tree
        seg = new int[4 * n];
        build(arr, 0, 0, n - 1);

        // Initialise the maxvalue of
        // the selected pairs
        int maxvalue = int.MinValue;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // For each value find the
            // floor(arr[i] + k)
            int right = search(arr,
                               arr[i].a + k);

            // Find the maximum value of
            // the select pairs i and max
            // from (i + 1, right)
            if (right != -1) {

                maxvalue = Math.Max(
                    maxvalue, arr[i].b - arr[i].a
                                  + getMax(arr, 0, 0, n - 1,
                                           i + 1, right));
            }
        }

        // Print the maximum value
        Console.WriteLine(maxvalue);
    }

    // Function to search floor of
    // the current value 
    public int search(
        triplet []arr, int val)
    {
        // Initialise low and high values
        int low = 0, high = arr.Length - 1;
        int ans = -1;

        // Perform Binary Search
        while (low <= high) {
            int mid = low + (high - low) / 2;

            // If the current value is
            // <= val then store the
            // candidate answer and
            // find for rightmost one
            if (arr[mid].a <= val) {
                ans = mid;
                low = mid + 1;
            }
            else
                high = mid - 1;
        }
        return ans;
    }

    // Function to build segment tree
    public static void build(
        triplet []arr, int index,
        int s, int e)
    {
        // Base Case
        if (s == e) {
            seg[index] = arr[s].c;
            return;
        }
        int mid = s + (e - s) / 2;

        // Build the left and right
        // segment trees
        build(arr, 2 * index + 1, s, mid);
        build(arr, 2 * index + 2, mid + 1, e);

        // Update current index
        seg[index] = Math.Max(seg[2 * index + 1],
                              seg[2 * index + 2]);
    }

    // Function to get maximum value
    // in the range [qs, qe]
    public static int getMax(
        triplet []arr, int index, int s,
        int e, int qs, int qe)
    {
        // If segment is not in range
        if (qe < s || e < qs)
            return int.MinValue / 2;

        // If segment is completely
        // inside the query
        if (s >= qs && e <= qe)
            return seg[index];

        // Calculate the maximum value
        // in left and right half
        int mid = s + (e - s) / 2;
        return Math.Max(
            getMax(arr, 2 * index + 1,
                   s, mid, qs, qe),
            getMax(arr, 2 * index + 2,
                   mid + 1, e, qs, qe));
    }

    // Driver Code
    public static void Main(String []args)
    {
        int N = 4, K = 1;
        int []A = { 5, 6, 9, 10 };
        int []B = { 3, 0, 10, -10 };

        // Function call
        new GFG().maxValue(A, B, N, K);
    }
}

// This code is contributed by 29AjayKumar
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*