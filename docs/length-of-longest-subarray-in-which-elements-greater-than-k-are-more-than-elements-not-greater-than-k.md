# 大于 K 的元素多于不大于 K 的元素的最长子阵列长度

> 原文:[https://www . geeksforgeeks . org/最长子阵列长度其中大于 k 的元素是不大于 k 的元素/](https://www.geeksforgeeks.org/length-of-longest-subarray-in-which-elements-greater-than-k-are-more-than-elements-not-greater-than-k/)

给定一个长度为 **N** 的数组 **arr[]** 。任务是找出最长子阵列的长度，其中大于给定数目的元素 **K** 多于不大于 **K** 的元素。
**示例:**

> **输入:** N = 5，K = 2，arr[]={ 1，2，3，4，1 }
> **输出:** 3
> 子阵【2，3，4】或【3，4，1】满足给定条件，没有
> 长度为 4 或 5 的子阵能保持给定条件，所以答案是 3。
> 
> **输入:** N = 4，K = 2，arr[]={ 6，5，3，4 }
> T3】输出: 4

**进场:**

*   想法是用二分搜索法的概念超过部分和。
*   首先，将大于 **K** 的元素替换为 1，将其他元素替换为-1，并计算其前缀和。现在，如果一个子阵列的和大于 0，这意味着它比小于 T4 的元素拥有更多的大于 T2 的元素。
*   要找到答案，请用二分搜索法代替答案。在二分搜索法的每一步中，检查该长度的每个子阵列，然后决定是否进行更大的长度。

以下是上述方法的实施情况:

## C++

```
#include <bits/stdc++.h>
using namespace std;
// C++ implementation of above approach

// Function to find the length of a
// longest subarray in which elements
// greater than K are more than
// elements not greater than K
int LongestSubarray(int a[], int n, int k)
{

    int pre[n] = { 0 };

    // Create a new array in which we store 1
    // if a[i] > k otherwise we store -1.
    for (int i = 0; i < n; i++) {
        if (a[i] > k)
            pre[i] = 1;
        else
            pre[i] = -1;
    }

    // Taking prefix sum over it
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + pre[i];

    // len will store maximum
    // length of subarray
    int len = 0;

    int lo = 1, hi = n;

    while (lo <= hi) {
        int mid = (lo + hi) / 2;

        // This indicate there is at least one
        // subarray of length mid that has sum > 0
        bool ok = false;

        // Check every subarray of length mid if
        // it has sum > 0 or not if sum > 0 then it
        // will satisfy our required condition
        for (int i = mid - 1; i < n; i++) {

            // x will store the sum of
            // subarray of length mid
            int x = pre[i];
            if (i - mid >= 0)
                x -= pre[i - mid];

            // Satisfy our given condition
            if (x > 0) {
                ok = true;
                break;
            }
        }

        // Check for higher length as we
        // get length mid
        if (ok == true) {
            len = mid;
            lo = mid + 1;
        }
        // Check for lower length as we
        // did not get length mid
        else
            hi = mid - 1;
    }

    return len;
}

// Driver code
int main()
{
    int a[] = { 2, 3, 4, 5, 3, 7 };
    int k = 3;
    int n = sizeof(a) / sizeof(a[0]);

    cout << LongestSubarray(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to find the length of a
// longest subarray in which elements
// greater than K are more than
// elements not greater than K
static int LongestSubarray(int a[], int n, int k)
{

    int []pre = new int[n];

    // Create a new array in which we store 1
    // if a[i] > k otherwise we store -1.
    for (int i = 0; i < n; i++)
    {
        if (a[i] > k)
            pre[i] = 1;
        else
            pre[i] = -1;
    }

    // Taking prefix sum over it
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + pre[i];

    // len will store maximum
    // length of subarray
    int len = 0;

    int lo = 1, hi = n;

    while (lo <= hi)
    {
        int mid = (lo + hi) / 2;

        // This indicate there is at least one
        // subarray of length mid that has sum > 0
        boolean ok = false;

        // Check every subarray of length mid if
        // it has sum > 0 or not if sum > 0 then it
        // will satisfy our required condition
        for (int i = mid - 1; i < n; i++)
        {

            // x will store the sum of
            // subarray of length mid
            int x = pre[i];
            if (i - mid >= 0)
                x -= pre[i - mid];

            // Satisfy our given condition
            if (x > 0)
            {
                ok = true;
                break;
            }
        }

        // Check for higher length as we
        // get length mid
        if (ok == true)
        {
            len = mid;
            lo = mid + 1;
        }

        // Check for lower length as we
        // did not get length mid
        else
            hi = mid - 1;
    }

    return len;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 3, 4, 5, 3, 7 };
    int k = 3;
    int n = a.length;

    System.out.println(LongestSubarray(a, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find the Length of a
# longest subarray in which elements
# greater than K are more than
# elements not greater than K
def LongestSubarray(a, n, k):

    pre = [0 for i in range(n)]

    # Create a new array in which we store 1
    # if a[i] > k otherwise we store -1.
    for i in range(n):
        if (a[i] > k):
            pre[i] = 1
        else:
            pre[i] = -1

    # Taking prefix sum over it
    for i in range(1, n):
        pre[i] = pre[i - 1] + pre[i]

    # Len will store maximum
    # Length of subarray
    Len = 0

    lo = 1
    hi = n

    while (lo <= hi):
        mid = (lo + hi) // 2

        # This indicate there is at least one
        # subarray of Length mid that has sum > 0
        ok = False

        # Check every subarray of Length mid if
        # it has sum > 0 or not if sum > 0 then it
        # will satisfy our required condition
        for i in range(mid - 1, n):

            # x will store the sum of
            # subarray of Length mid
            x = pre[i]
            if (i - mid >= 0):
                x -= pre[i - mid]

            # Satisfy our given condition
            if (x > 0):
                ok = True
                break

        # Check for higher Length as we
        # get Length mid
        if (ok == True):
            Len = mid
            lo = mid + 1

        # Check for lower Length as we
        # did not get Length mid
        else:
            hi = mid - 1

    return Len

# Driver code
a = [2, 3, 4, 5, 3, 7]
k = 3
n = len(a)

print(LongestSubarray(a, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the length of a
// longest subarray in which elements
// greater than K are more than
// elements not greater than K
static int LongestSubarray(int[] a, int n, int k)
{
    int []pre = new int[n];

    // Create a new array in which we store 1
    // if a[i] > k otherwise we store -1.
    for (int i = 0; i < n; i++)
    {
        if (a[i] > k)
            pre[i] = 1;
        else
            pre[i] = -1;
    }

    // Taking prefix sum over it
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + pre[i];

    // len will store maximum
    // length of subarray
    int len = 0;

    int lo = 1, hi = n;

    while (lo <= hi)
    {
        int mid = (lo + hi) / 2;

        // This indicate there is at least one
        // subarray of length mid that has sum > 0
        bool ok = false;

        // Check every subarray of length mid if
        // it has sum > 0 or not if sum > 0 then it
        // will satisfy our required condition
        for (int i = mid - 1; i < n; i++)
        {

            // x will store the sum of
            // subarray of length mid
            int x = pre[i];
            if (i - mid >= 0)
                x -= pre[i - mid];

            // Satisfy our given condition
            if (x > 0)
            {
                ok = true;
                break;
            }
        }

        // Check for higher length as we
        // get length mid
        if (ok == true)
        {
            len = mid;
            lo = mid + 1;
        }

        // Check for lower length as we
        // did not get length mid
        else
            hi = mid - 1;
    }
    return len;
}

// Driver code
public static void Main()
{
    int[] a = { 2, 3, 4, 5, 3, 7 };
    int k = 3;
    int n = a.Length;

    Console.WriteLine(LongestSubarray(a, n, k));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript implementation of above approach

// Function to find the length of a
// longest subarray in which elements
// greater than K are more than
// elements not greater than K
function LongestSubarray(a , n , k)
{

    var pre = Array.from({length: n}, (_, i) => 0);

    // Create a new array in which we store 1
    // if a[i] > k otherwise we store -1.
    for (i = 0; i < n; i++)
    {
        if (a[i] > k)
            pre[i] = 1;
        else
            pre[i] = -1;
    }

    // Taking prefix sum over it
    for (i = 1; i < n; i++)
        pre[i] = pre[i - 1] + pre[i];

    // len will store maximum
    // length of subarray
    var len = 0;

    var lo = 1, hi = n;

    while (lo <= hi)
    {
        var mid = parseInt((lo + hi) / 2);

        // This indicate there is at least one
        // subarray of length mid that has sum > 0
        var ok = false;

        // Check every subarray of length mid if
        // it has sum > 0 or not if sum > 0 then it
        // will satisfy our required condition
        for (i = mid - 1; i < n; i++)
        {

            // x will store the sum of
            // subarray of length mid
            var x = pre[i];
            if (i - mid >= 0)
                x -= pre[i - mid];

            // Satisfy our given condition
            if (x > 0)
            {
                ok = true;
                break;
            }
        }

        // Check for higher length as we
        // get length mid
        if (ok == true)
        {
            len = mid;
            lo = mid + 1;
        }

        // Check for lower length as we
        // did not get length mid
        else
            hi = mid - 1;
    }

    return len;
}

// Driver code
var a = [ 2, 3, 4, 5, 3, 7 ];
var k = 3;
var n = a.length;

document.write(LongestSubarray(a, n, k));

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
5
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(N)