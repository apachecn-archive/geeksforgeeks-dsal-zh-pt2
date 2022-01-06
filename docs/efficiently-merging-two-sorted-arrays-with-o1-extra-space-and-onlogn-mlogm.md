# 利用 O(1)个额外空间和 O(NlogN + MlogM)有效合并两个排序数组

> 原文:[https://www . geesforgeks . org/efficient-merging-two-sorted-array-with-O1-extra-space-and-onlogn-mlogm/](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space-and-onlogn-mlogm/)

给定两个排序数组 **arr1[]** 和 **arr2[]** ，任务是将它们在 **O(Nlog(N) + Mlog(M))** 时间内与 **O(1)** 额外空间合并成排序数组，其中 **N** 是第一个数组 **arr1[]** 的大小， **M** 是第二个数组**arr 2[**的大小。

**示例:**

> **输入:** arr1[] = {1，5，9，10，15，20}，arr2[] = {2，3，8，13}
> **输出:** 1 2 3 5 8 9 10 13 15 20
> 
> **输入:** arr1[] = {4，9，15，20}，arr2[] = {2，6，7，13 }
> T3】输出: 2 4 6 7 9 13 15 20

**方法:**在[这篇](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)文章中已经讨论了一种方法。在本文中，将讨论一种更有效的方法。

*   通过将一个数组的最高元素与第二个数组的最低元素进行比较，形成两个[双音素数组](https://www.geeksforgeeks.org/find-element-bitonic-array/)，这样两个数组都只包含在两个数组排序后将要出现的元素。
*   现在，分别对两个数组进行排序。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <iostream>
using namespace std;

// Reducing the gap by a factor of 2
int nextGap(int gap)
{
    if (gap <= 1)
        return 0;
    return (gap / 2) + (gap % 2);
}

// Function to merge two sorted
// arrays with O(1) extra space
int mergeTwoSortedArray(int* arr1,
                        int* arr2,
                        int n, int m)
{
    int x = min(n, m);

    // Form both arrays to be bitonic
    for (int i = 0; i < x; i++) {
        if (arr1[n - i - 1] > arr2[i])
            swap(arr1[n - i - 1], arr2[i]);
    }

    // Now both the arrays contain the numbers
    // which should be there in the result
    // Sort the array individually by inplace algo
    for (int gap = nextGap(n); gap > 0;
         gap = nextGap(gap)) {

        // Comparing elements in the first array
        for (int i = 0; i + gap < n; i++)
            if (arr1[i] > arr1[i + gap])
                swap(arr1[i], arr1[i + gap]);
    }

    // Sort the second array
    for (int gap = nextGap(m); gap > 0;
         gap = nextGap(gap)) {

        // Comparing elements in the second array
        for (int i = 0; i + gap < m; i++)
            if (arr2[i] > arr2[i + gap])
                swap(arr2[i], arr2[i + gap]);
    }
    for (int i = 0; i < n; i++)
        cout << arr1[i] << " ";
    for (int j = 0; j < m; j++)
        cout << arr2[j] << " ";
}

// Driver code
int main()
{
    int arr1[] = { 1, 5, 9, 10, 15, 20 };
    int n = sizeof(arr1) / sizeof(int);
    int arr2[] = { 2, 3, 8, 13 };
    int m = sizeof(arr2) / sizeof(int);

    mergeTwoSortedArray(arr1, arr2, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Reducing the gap by a factor of 2
    static int nextGap(int gap)
    {
        if (gap <= 1)
            return 0;
        return (int)((gap / 2) + (gap % 2));
    }

    // Function to merge two sorted
    // arrays with O(1) extra space
    static void mergeTwoSortedArray(int []arr1,
                                    int []arr2,
                                    int n, int m)
    {
        int x = Math.min(n, m);

        // Form both arrays to be bitonic
        for (int i = 0; i < x; i++)
        {
            if (arr1[n - i - 1] > arr2[i])
            {
                // swap(arr1[n - i - 1], arr2[i]);
                int temp = arr1[n - i - 1];
                arr1[n - i - 1] = arr2[i];
                arr2[i] = temp;
            }
        }

        // Now both the arrays contain the numbers
        // which should be there in the result
        // Sort the array individually by inplace algo
        for (int gap = nextGap(n); gap > 0;
            gap = nextGap(gap))
        {

            // Comparing elements in the first array
            for (int i = 0; i + gap < n; i++)
                if (arr1[i] > arr1[i + gap])
                {
                    // swap(arr1[i], arr1[i + gap]);
                    int temp = arr1[i];
                    arr1[i] = arr1[i + gap];
                    arr1[i + gap] = temp;
                }
        }

        // Sort the second array
        for (int gap = nextGap(m); gap > 0;
            gap = nextGap(gap))
        {

            // Comparing elements in the second array
            for (int i = 0; i + gap < m; i++)
                if (arr2[i] > arr2[i + gap])
                {
                    // swap(arr2[i], arr2[i + gap]);
                    int temp = arr2[i];
                    arr2[i] = arr2[i + gap];
                    arr2[i + gap] = temp;
                }
        }
        for (int i = 0; i < n; i++)
            System.out.print(arr1[i] + " ");
        for (int j = 0; j < m; j++)
            System.out.print(arr2[j] + " ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr1[] = { 1, 5, 9, 10, 15, 20 };
        int n = arr1.length;
        int arr2[] = { 2, 3, 8, 13 };
        int m = arr2.length;

        mergeTwoSortedArray(arr1, arr2, n, m);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Reducing the gap by a factor of 2
def nextGap(gap) :
    if (gap <= 1) :
        return 0;
    res = (gap // 2) + (gap % 2);
    return res;

# Function to merge two sorted
# arrays with O(1) extra space
def mergeTwoSortedArray(arr1, arr2, n, m) :

    x = min(n, m);

    # Form both arrays to be bitonic
    for i in range(x) :
        if (arr1[n - i - 1] > arr2[i]) :
            arr1[n - i - 1],arr2[i] = arr2[i], arr1[n- i - 1];

    # Now both the arrays contain the numbers
    # which should be there in the result
    # Sort the array individually by inplace algo
    gap = nextGap(n);
    while gap > 0 :

        # Comparing elements in the first array
        i = 0;

        while i + gap < n :

            if (arr1[i] > arr1[i + gap]) :
                arr1[i], arr1[i + gap] = arr1[i + gap],arr1[i];

            i += 1;

        gap = nextGap(gap)

    # Sort the second array
    gap = nextGap(m);

    while gap > 0 :

        # Comparing elements in the second array
        i = 0
        while i + gap < m :
            if (arr2[i] > arr2[i + gap]) :
                arr2[i], arr2[i + gap] = arr2[i + gap], arr2[i];

            i += 1;

        gap = nextGap(gap)

    for i in range(n) :
        print(arr1[i], end = " ");

    for j in range(m) :
        print(arr2[j], end = " ");

# Driver code
if __name__ == "__main__" :

    arr1 = [ 1, 5, 9, 10, 15, 20 ];
    n = len(arr1);
    arr2 = [ 2, 3, 8, 13 ];
    m = len(arr2);

    mergeTwoSortedArray(arr1, arr2, n, m);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Reducing the gap by a factor of 2
    static int nextGap(int gap)
    {
        if (gap <= 1)
            return 0;
        return (int)((gap / 2) + (gap % 2));
    }

    // Function to merge two sorted
    // arrays with O(1) extra space
    static void mergeTwoSortedArray(int []arr1,
                                    int []arr2,
                                    int n, int m)
    {
        int x = Math.Min(n, m);

        // Form both arrays to be bitonic
        for (int i = 0; i < x; i++)
        {
            if (arr1[n - i - 1] > arr2[i])
            {
                int temp = arr1[n - i - 1];
                arr1[n - i - 1] = arr2[i];
                arr2[i] = temp;
            }
        }

        // Now both the arrays contain the numbers
        // which should be there in the result
        // Sort the array individually by inplace algo
        for (int gap = nextGap(n); gap > 0;
            gap = nextGap(gap))
        {

            // Comparing elements in the first array
            for (int i = 0; i + gap < n; i++)
                if (arr1[i] > arr1[i + gap])
                {
                    int temp = arr1[i];
                    arr1[i] = arr1[i + gap];
                    arr1[i + gap] = temp;
                }
        }

        // Sort the second array
        for (int gap = nextGap(m); gap > 0;
            gap = nextGap(gap))
        {

            // Comparing elements in the second array
            for (int i = 0; i + gap < m; i++)
                if (arr2[i] > arr2[i + gap])
                {
                    int temp = arr2[i];
                    arr2[i] = arr2[i + gap];
                    arr2[i + gap] = temp;
                }
        }
        for (int i = 0; i < n; i++)
            Console.Write(arr1[i] + " ");
        for (int j = 0; j < m; j++)
            Console.Write(arr2[j] + " ");
    }

    // Driver code
    public static void Main()
    {
        int []arr1 = { 1, 5, 9, 10, 15, 20 };
        int n = arr1.Length;
        int []arr2 = { 2, 3, 8, 13 };
        int m = arr2.Length;

        mergeTwoSortedArray(arr1, arr2, n, m);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Reducing the gap by a factor of 2
    function nextGap(gap)
    {
        if (gap <= 1)
            return 0;
        return (parseInt(gap / 2, 10) + (gap % 2));
    }

    // Function to merge two sorted
    // arrays with O(1) extra space
    function mergeTwoSortedArray(arr1, arr2, n, m)
    {
        let x = Math.min(n, m);

        // Form both arrays to be bitonic
        for (let i = 0; i < x; i++)
        {
            if (arr1[n - i - 1] > arr2[i])
            {
                let temp = arr1[n - i - 1];
                arr1[n - i - 1] = arr2[i];
                arr2[i] = temp;
            }
        }

        // Now both the arrays contain the numbers
        // which should be there in the result
        // Sort the array individually by inplace algo
        for (let gap = nextGap(n); gap > 0;
            gap = nextGap(gap))
        {

            // Comparing elements in the first array
            for (let i = 0; i + gap < n; i++)
                if (arr1[i] > arr1[i + gap])
                {
                    let temp = arr1[i];
                    arr1[i] = arr1[i + gap];
                    arr1[i + gap] = temp;
                }
        }

        // Sort the second array
        for (let gap = nextGap(m); gap > 0;
            gap = nextGap(gap))
        {

            // Comparing elements in the second array
            for (let i = 0; i + gap < m; i++)
                if (arr2[i] > arr2[i + gap])
                {
                    let temp = arr2[i];
                    arr2[i] = arr2[i + gap];
                    arr2[i + gap] = temp;
                }
        }
        for (let i = 0; i < n; i++)
            document.write(arr1[i] + " ");
        for (let j = 0; j < m; j++)
            document.write(arr2[j] + " ");
    }

    let arr1 = [ 1, 5, 9, 10, 15, 20 ];
    let n = arr1.length;
    let arr2 = [ 2, 3, 8, 13 ];
    let m = arr2.length;

    mergeTwoSortedArray(arr1, arr2, n, m);

</script>
```

**Output:** 

```
1 2 3 5 8 9 10 13 15 20
```

**时间复杂度:** O(Nlog(N) + Mlog(M))