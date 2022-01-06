# 大小为 K 的 M 个非重叠子阵列的最大和

> 原文:[https://www . geeksforgeeks . org/max-m 之和-不重叠-大小为 k 的子阵列/](https://www.geeksforgeeks.org/max-sum-of-m-non-overlapping-subarrays-of-size-k/)

给定一个数组和两个数字 M 和 K，我们需要找到数组中大小为 K(非重叠)的最大 M 个子数组的**和。(数组的顺序保持不变)。k 是子阵的大小，M 是子阵的个数。可以假设数组的大小大于 m*k，如果数组总大小不是 k 的倍数，那么我们可以取部分最后一个数组。
**例:**** 

```
Input: N = 7, M = 3, K = 1 
       arr[] = {2, 10, 7, 18, 5, 33, 0}; 
Output: 61 
Explanation: subsets are: 33, 18, 10 (3 subsets of size 1) 

Input: N = 4, M = 2, K = 2 
       arr[] = {3, 2, 100, 1}; 
Output:  106 
Explanation: subsets are: (3, 2), (100, 1) 2 subsets of size 2
```

这里我们可以看到，我们需要找到 M 个子阵列，每个子阵列的大小为 K，所以，
1。我们创建一个假定数组，在每个索引中包含给定数组中从“**索引**”到**“索引+K”**的所有元素的总和。和数组的大小为 **n+1-k** 。
2。现在，如果我们包括大小为 k 的子阵列，那么我们不能在任何其他子阵列中再次包括该子阵列的任何元素，因为它将创建重叠的子阵列。所以我们通过排除包含子阵的 k 个元素进行递归调用。
3。如果我们排除一个子阵列，那么我们可以在其他子阵列中使用该子阵列的下一个 k-1 元素，因此我们将通过排除该子阵列的第一个元素来进行递归调用。
4。最后返回最大值(包括和，不包括和)。

## C++

```
// C++ program to find Max sum of M non-overlapping
// subarray of size K in an Array
#include <bits/stdc++.h>
using namespace std;

// calculating presum of array. presum[i]
// is going to store prefix sum of subarray
// of size k beginning with arr[i]
void calculatePresumArray(int presum[],
                int arr[], int n, int k)
{   
    for (int i=0; i<k; i++)
       presum[0] += arr[i];

    // store sum of array index i to i+k
    // in presum array at index i of it.
    for (int i = 1; i <= n - k; i++)
       presum[i] += presum[i-1] + arr[i+k-1] -
                                  arr[i-1];
}

// calculating maximum sum of m non overlapping array
int maxSumMnonOverlappingSubarray(int presum[],
              int m, int size, int k, int start)
{
    // if m is zero then no need any array
    // of any size so return 0.
    if (m == 0)
        return 0;

    // if start is greater then the size
    // of presum array return 0.
    if (start > size - 1)
        return 0;

    int mx = 0;

    // if including subarray of size k
    int includeMax = presum[start] +
            maxSumMnonOverlappingSubarray(presum,
                        m - 1, size, k, start + k);

    // if excluding element and searching
    // in all next possible subarrays
    int excludeMax =
            maxSumMnonOverlappingSubarray(presum,
                            m, size, k, start + 1);

    // return max
    return max(includeMax, excludeMax);
}

// Driver code
int main()
{
    int arr[] = { 2, 10, 7, 18, 5, 33, 0 };
    int n = sizeof(arr)/sizeof(arr[0]);

     int m = 3, k = 1;

    int presum[n + 1 - k] = { 0 };
    calculatePresumArray(presum, arr, n, k);

    // resulting presum array will have a size = n+1-k
    cout << maxSumMnonOverlappingSubarray(presum,
                               m, n + 1 - k, k, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Max sum
// of M non-overlapping subarray
// of size K in an Array

import java.io.*;

class GFG
{
// calculating presum of array.
// presum[i] is going to store
// prefix sum of subarray of
// size k beginning with arr[i]
static void calculatePresumArray(int presum[],
                                 int arr[],
                                 int n, int k)
{
    for (int i = 0; i < k; i++)
    presum[0] += arr[i];

    // store sum of array index i to i+k
    // in presum array at index i of it.
    for (int i = 1; i <= n - k; i++)
    presum[i] += presum[i - 1] + arr[i + k - 1] -
                                 arr[i - 1];
}

// calculating maximum sum of
// m non overlapping array
static int maxSumMnonOverlappingSubarray(int presum[],
                                         int m, int size,
                                         int k, int start)
{
    // if m is zero then no need
    // any array of any size so
    // return 0.
    if (m == 0)
        return 0;

    // if start is greater then the
    // size of presum array return 0.
    if (start > size - 1)
        return 0;

    int mx = 0;

    // if including subarray of size k
    int includeMax = presum[start] +
            maxSumMnonOverlappingSubarray(presum,
                      m - 1, size, k, start + k);

    // if excluding element and searching
    // in all next possible subarrays
    int excludeMax =
            maxSumMnonOverlappingSubarray(presum,
                          m, size, k, start + 1);

    // return max
    return Math.max(includeMax, excludeMax);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 2, 10, 7, 18, 5, 33, 0 };
    int n = arr.length;
    int m = 3, k = 1;
    int presum[] = new int[n + 1 - k] ;
    calculatePresumArray(presum, arr, n, k);

    // resulting presum array
    // will have a size = n+1-k
    System.out.println(maxSumMnonOverlappingSubarray(presum,
                                        m, n + 1 - k, k, 0));
}
}

// This code is contributed by anuj_67.
```

## 计算机编程语言

```
# Python3 program to find Max sum of M non-overlapping
# subarray of size K in an Array

# calculating presum of array. presum[i]
# is going to store prefix sum of subarray
# of size k beginning with arr[i]
def calculatePresumArray(presum,arr, n, k):

    for i in range(k):
        presum[0] += arr[i]

    # store sum of array index i to i+k
    # in presum array at index i of it.
    for i in range(1,n - k + 1):
        presum[i] += presum[i - 1] + arr[i + k - 1] - arr[i - 1]

# calculating maximum sum of m non overlapping array
def maxSumMnonOverlappingSubarray(presum, m, size, k, start):

    # if m is zero then no need any array
    # of any size so return 0.
    if (m == 0):
        return 0

    # if start is greater then the size
    # of presum array return 0.
    if (start > size - 1):
        return 0

    mx = 0

    # if including subarray of size k
    includeMax = presum[start] + maxSumMnonOverlappingSubarray(presum,m - 1, size, k, start + k)

    # if excluding element and searching
    # in all next possible subarrays
    excludeMax = maxSumMnonOverlappingSubarray(presum,m, size, k, start + 1)

    # return max
    return max(includeMax, excludeMax)

# Driver code
arr = [2, 10, 7, 18, 5, 33, 0]
n = len(arr)

m, k = 3, 1

presum = [0 for i in range(n + 1 - k)]
calculatePresumArray(presum, arr, n, k)

# resulting presum array will have a size = n+1-k
print(maxSumMnonOverlappingSubarray(presum, m, n + 1 - k, k, 0))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find Max sum of M
// non-overlapping subarray of size
// K in an Array
using System;

class GFG {

    // calculating presum of array.
    // presum[i] is going to store
    // prefix sum of subarray of
    // size k beginning with arr[i]
    static void calculatePresumArray(int []presum,
                          int []arr, int n, int k)
    {
        for (int i = 0; i < k; i++)
        presum[0] += arr[i];

        // store sum of array index i to i+k
        // in presum array at index i of it.
        for (int i = 1; i <= n - k; i++)
        presum[i] += presum[i - 1] + arr[i + k - 1]
                                      - arr[i - 1];
    }

    // calculating maximum sum of
    // m non overlapping array
    static int maxSumMnonOverlappingSubarray(
                     int []presum, int m, int size,
                                  int k, int start)
    {

        // if m is zero then no need
        // any array of any size so
        // return 0.
        if (m == 0)
            return 0;

        // if start is greater then the
        // size of presum array return 0.
        if (start > size - 1)
            return 0;

        //int mx = 0;

        // if including subarray of size k
        int includeMax = presum[start] +
                maxSumMnonOverlappingSubarray(presum,
                          m - 1, size, k, start + k);

        // if excluding element and searching
        // in all next possible subarrays
        int excludeMax =
                maxSumMnonOverlappingSubarray(presum,
                              m, size, k, start + 1);

        // return max
        return Math.Max(includeMax, excludeMax);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 2, 10, 7, 18, 5, 33, 0 };
        int n = arr.Length;
        int m = 3, k = 1;
        int []presum = new int[n + 1 - k] ;
        calculatePresumArray(presum, arr, n, k);

        // resulting presum array
        // will have a size = n+1-k
        Console.WriteLine(
              maxSumMnonOverlappingSubarray(presum,
                              m, n + 1 - k, k, 0));
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>
// Javascript program to find Max sum
// of M non-overlapping subarray
// of size K in an Array

// calculating presum of array.
// presum[i] is going to store
// prefix sum of subarray of
// size k beginning with arr[i]
function calculatePresumArray(presum,arr,n,k)
{
    for (let i = 0; i < k; i++)
        presum[0] += arr[i];

    // store sum of array index i to i+k
    // in presum array at index i of it.
    for (let i = 1; i <= n - k; i++)
        presum[i] += presum[i - 1] + arr[i + k - 1] -
                                 arr[i - 1];           
}

// calculating maximum sum of
// m non overlapping array
function maxSumMnonOverlappingSubarray(presum,m,size,k,start)
{
    // if m is zero then no need
    // any array of any size so
    // return 0.
    if (m == 0)
        return 0;

    // if start is greater then the
    // size of presum array return 0.
    if (start > size - 1)
        return 0;

    let mx = 0;

    // if including subarray of size k
    let includeMax = presum[start] +
            maxSumMnonOverlappingSubarray(presum,
                      m - 1, size, k, start + k);

    // if excluding element and searching
    // in all next possible subarrays
    let excludeMax =
            maxSumMnonOverlappingSubarray(presum,
                          m, size, k, start + 1);

    // return max
    return Math.max(includeMax, excludeMax);
}

// Driver code
let arr=[2, 10, 7, 18, 5, 33, 0];
let n = arr.length;
let m = 3, k = 1;
let presum = new Array(n + 1 - k) ;
for(let i = 0; i < presum.length; i++)
{
    presum[i] = 0;
}
calculatePresumArray(presum, arr, n, k);

// resulting presum array
// will have a size = n+1-k
document.write(maxSumMnonOverlappingSubarray(presum,
                                                 m, n + 1 - k, k, 0));

// This code is contributed by patel2127
</script>
```

**Output :** 

```
61
```