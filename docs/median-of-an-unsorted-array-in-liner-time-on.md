# 使用快速选择算法的未排序数组的中值

> 原文:[https://www . geeksforgeeks . org/中值未排序的线性阵列开启时间/](https://www.geeksforgeeks.org/median-of-an-unsorted-array-in-liner-time-on/)

给定一个长度为 **N** 的未排序数组 **arr[]** ，任务是找到这个数组的中值。
[**大小为 N 的排序数组的中值**](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/) 定义为 N 为奇数时的中间元素和 N 为偶数时中间两个元素的平均值。

**示例:**

> **输入:** arr[] = {12，3，5，7，4，19，26}
> **输出:** 7
> 给定数组 arr[] = {3，4，5，7，12，19，26}
> 排序序列由于元素个数为奇数，因此中位数为给定数组 arr[]排序序列中的第 4 个元素，即 7
> 
> **输入:** arr[] = {12，3，5，7，4，26}
> **输出:** 6
> 由于元素个数是偶数，所以中值是给定数组 arr[](即(5 + 7)/2 = 6)排序序列中第 3 个和第 4 个元素的平均值

**天真方法:**

*   [按递增顺序对数组](https://www.geeksforgeeks.org/sorting-algorithms/) arr[]进行排序。
*   如果 **arr[]** 中的元素个数是奇数，那么中间值就是 **arr[n/2]** 。
*   如果**arr【】**中的元素个数为偶数，则中位数为 arr【n/2】和 arr【n/2+1】的**平均值。**

上述方法的实施请参考[本文](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。

**高效方法:使用** [**随机快速选择**](https://www.geeksforgeeks.org/quickselect-algorithm/)

*   从**arr【】**中随机选取枢轴元素，并使用[快速排序](https://www.geeksforgeeks.org/quick-sort/)算法中的**分割步骤**将所有小于枢轴的元素排列在其左侧，大于枢轴的元素排列在其右侧。
*   如果在上一步之后，所选轴的位置是数组的中间，则它是给定数组的所需中值。
*   如果位置在中间元素之前，则从上一个起始索引开始为子阵列重复该步骤，并选择枢轴作为结束索引。
*   如果位置在中间元素之后，则从所选的轴开始，重复子阵列的步骤，并在前一个结束索引处结束。
*   请注意，在偶数个元素的情况下，必须找到中间的两个元素，它们的平均值将是数组的中值。

下面是上述方法的实现:

## C++

```
// CPP program to find median of
// an array

#include "bits/stdc++.h"
using namespace std;

// Utility function to swapping of element
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Returns the correct position of
// pivot element
int Partition(int arr[], int l, int r)
{
    int lst = arr[r], i = l, j = l;
    while (j < r) {
        if (arr[j] < lst) {
            swap(&arr[i], &arr[j]);
            i++;
        }
        j++;
    }
    swap(&arr[i], &arr[r]);
    return i;
}

// Picks a random pivot element between
// l and r and partitions arr[l..r]
// around the randomly picked element
// using partition()
int randomPartition(int arr[], int l,
                    int r)
{
    int n = r - l + 1;
    int pivot = rand() % n;
    swap(&arr[l + pivot], &arr[r]);
    return Partition(arr, l, r);
}

// Utility function to find median
void MedianUtil(int arr[], int l, int r,
                int k, int& a, int& b)
{

    // if l < r
    if (l <= r) {

        // Find the partition index
        int partitionIndex
            = randomPartition(arr, l, r);

        // If partition index = k, then
        // we found the median of odd
        // number element in arr[]
        if (partitionIndex == k) {
            b = arr[partitionIndex];
            if (a != -1)
                return;
        }

        // If index = k - 1, then we get
        // a & b as middle element of
        // arr[]
        else if (partitionIndex == k - 1) {
            a = arr[partitionIndex];
            if (b != -1)
                return;
        }

        // If partitionIndex >= k then
        // find the index in first half
        // of the arr[]
        if (partitionIndex >= k)
            return MedianUtil(arr, l,
                              partitionIndex - 1,
                              k, a, b);

        // If partitionIndex <= k then
        // find the index in second half
        // of the arr[]
        else
            return MedianUtil(arr,
                              partitionIndex + 1,
                              r, k, a, b);
    }

    return;
}

// Function to find Median
void findMedian(int arr[], int n)
{
    int ans, a = -1, b = -1;

    // If n is odd
    if (n % 2 == 1) {
        MedianUtil(arr, 0, n - 1,
                   n / 2, a, b);
        ans = b;
    }

    // If n is even
    else {
        MedianUtil(arr, 0, n - 1,
                   n / 2, a, b);
        ans = (a + b) / 2;
    }

    // Print the Median of arr[]
    cout << "Median = " << ans;
}

// Driver program to test above methods
int main()
{
    int arr[] = { 12, 3, 5, 7, 4, 19, 26 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findMedian(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find median of
// an array
class GFG
{
    static int a, b;

    // Utility function to swapping of element
    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Returns the correct position of
    // pivot element
    static int Partition(int arr[], int l, int r)
    {
        int lst = arr[r], i = l, j = l;
        while (j < r)
        {
            if (arr[j] < lst)
            {
                arr = swap(arr, i, j);
                i++;
            }
            j++;
        }
        arr = swap(arr, i, r);
        return i;
    }

    // Picks a random pivot element between
    // l and r and partitions arr[l..r]
    // around the randomly picked element
    // using partition()
    static int randomPartition(int arr[], int l, int r)
    {
        int n = r - l + 1;
        int pivot = (int) (Math.random() % n);
        arr = swap(arr, l + pivot, r);
        return Partition(arr, l, r);
    }

    // Utility function to find median
    static int MedianUtil(int arr[], int l, int r, int k)
    {

        // if l < r
        if (l <= r)
        {

            // Find the partition index
            int partitionIndex = randomPartition(arr, l, r);

            // If partition index = k, then
            // we found the median of odd
            // number element in arr[]
            if (partitionIndex == k)
            {
                b = arr[partitionIndex];
                if (a != -1)
                    return Integer.MIN_VALUE;
            }

            // If index = k - 1, then we get
            // a & b as middle element of
            // arr[]
            else if (partitionIndex == k - 1)
            {
                a = arr[partitionIndex];
                if (b != -1)
                    return Integer.MIN_VALUE;
            }

            // If partitionIndex >= k then
            // find the index in first half
            // of the arr[]
            if (partitionIndex >= k)
                return MedianUtil(arr, l, partitionIndex - 1, k);

            // If partitionIndex <= k then
            // find the index in second half
            // of the arr[]
            else
                return MedianUtil(arr, partitionIndex + 1, r, k);
        }

        return Integer.MIN_VALUE;
    }

    // Function to find Median
    static void findMedian(int arr[], int n)
    {
        int ans;
        a = -1;
        b = -1;

        // If n is odd
        if (n % 2 == 1)
        {
            MedianUtil(arr, 0, n - 1, n / 2);
            ans = b;
        }

        // If n is even
        else
        {
            MedianUtil(arr, 0, n - 1, n / 2);
            ans = (a + b) / 2;
        }

        // Print the Median of arr[]
        System.out.print("Median = " + ans);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 12, 3, 5, 7, 4, 19, 26 };
        int n = arr.length;
        findMedian(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find median of
# an array
import random

a, b = None, None;

# Returns the correct position of
# pivot element
def Partition(arr, l, r) :

    lst = arr[r]; i = l; j = l;
    while (j < r) :
        if (arr[j] < lst) :
            arr[i], arr[j] = arr[j],arr[i];
            i += 1;

        j += 1;

    arr[i], arr[r] = arr[r],arr[i];
    return i;

# Picks a random pivot element between
# l and r and partitions arr[l..r]
# around the randomly picked element
# using partition()
def randomPartition(arr, l, r) :
    n = r - l + 1;
    pivot = random.randrange(1, 100) % n;
    arr[l + pivot], arr[r] = arr[r], arr[l + pivot];
    return Partition(arr, l, r);

# Utility function to find median
def MedianUtil(arr, l, r,
                k, a1, b1) :

    global a, b;

    # if l < r
    if (l <= r) :

        # Find the partition index
        partitionIndex = randomPartition(arr, l, r);

        # If partition index = k, then
        # we found the median of odd
        # number element in arr[]
        if (partitionIndex == k) :
            b = arr[partitionIndex];
            if (a1 != -1) :
                return;

        # If index = k - 1, then we get
        # a & b as middle element of
        # arr[]
        elif (partitionIndex == k - 1) :
            a = arr[partitionIndex];
            if (b1 != -1) :
                return;

        # If partitionIndex >= k then
        # find the index in first half
        # of the arr[]
        if (partitionIndex >= k) :
            return MedianUtil(arr, l, partitionIndex - 1, k, a, b);

        # If partitionIndex <= k then
        # find the index in second half
        # of the arr[]
        else :
            return MedianUtil(arr, partitionIndex + 1, r, k, a, b);

    return;

# Function to find Median
def findMedian(arr, n) :
    global a;
    global b;
    a = -1;
    b = -1;

    # If n is odd
    if (n % 2 == 1) :
        MedianUtil(arr, 0, n - 1, n // 2, a, b);
        ans = b;

    # If n is even
    else :
        MedianUtil(arr, 0, n - 1, n // 2, a, b);
        ans = (a + b) // 2;

    # Print the Median of arr[]
    print("Median = " ,ans);

# Driver code
arr = [ 12, 3, 5, 7, 4, 19, 26 ];
n = len(arr);
findMedian(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find median of
// an array
using System;

class GFG
{
    static int a, b;

    // Utility function to swapping of element
    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Returns the correct position of
    // pivot element
    static int Partition(int []arr, int l, int r)
    {
        int lst = arr[r], i = l, j = l;
        while (j < r)
        {
            if (arr[j] < lst)
            {
                arr = swap(arr, i, j);
                i++;
            }
            j++;
        }
        arr = swap(arr, i, r);
        return i;
    }

    // Picks a random pivot element between
    // l and r and partitions arr[l..r]
    // around the randomly picked element
    // using partition()
    static int randomPartition(int []arr, int l, int r)
    {
        int n = r - l + 1;
        int pivot = (int) (new Random().Next() % n);
        arr = swap(arr, l + pivot, r);
        return Partition(arr, l, r);
    }

    // Utility function to find median
    static int MedianUtil(int []arr, int l, int r, int k)
    {

        // if l < r
        if (l <= r)
        {

            // Find the partition index
            int partitionIndex = randomPartition(arr, l, r);

            // If partition index = k, then
            // we found the median of odd
            // number element in []arr
            if (partitionIndex == k)
            {
                b = arr[partitionIndex];
                if (a != -1)
                    return int.MinValue;
            }

            // If index = k - 1, then we get
            // a & b as middle element of
            // []arr
            else if (partitionIndex == k - 1)
            {
                a = arr[partitionIndex];
                if (b != -1)
                    return int.MinValue;
            }

            // If partitionIndex >= k then
            // find the index in first half
            // of the []arr
            if (partitionIndex >= k)
                return MedianUtil(arr, l, partitionIndex - 1, k);

            // If partitionIndex <= k then
            // find the index in second half
            // of the []arr
            else
                return MedianUtil(arr, partitionIndex + 1, r, k);
        }

        return int.MinValue;
    }

    // Function to find Median
    static void findMedian(int []arr, int n)
    {
        int ans;
        a = -1;
        b = -1;

        // If n is odd
        if (n % 2 == 1)
        {
            MedianUtil(arr, 0, n - 1, n / 2);
            ans = b;
        }

        // If n is even
        else
        {
            MedianUtil(arr, 0, n - 1, n / 2);
            ans = (a + b) / 2;
        }

        // Print the Median of []arr
        Console.Write("Median = " + ans);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 12, 3, 5, 7, 4, 19, 26 };
        int n = arr.Length;
        findMedian(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
Median = 7
```

**时间复杂度:**

1.  最佳案例分析:O(1)
2.  平均案例分析:O(N)
3.  最坏情况分析:O(N <sup>2</sup> )

**辅助空间:** O(N)
想知道怎么做？
参考:[by 斯坦福大学](https://web.stanford.edu/class/archive/cs/cs161/cs161.1138/lectures/09/Small09.pdf)