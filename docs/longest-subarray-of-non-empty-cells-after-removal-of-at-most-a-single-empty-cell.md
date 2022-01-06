# 去除最多一个空细胞后最长的非空细胞子阵列

> 原文:[https://www . geeksforgeeks . org/移除最多一个空单元后的最长非空单元子阵列/](https://www.geeksforgeeks.org/longest-subarray-of-non-empty-cells-after-removal-of-at-most-a-single-empty-cell/)

给定一个二进制数组 **arr[]** ，任务是在移除最多 **1** 个空单元后，找到最长的非空单元子阵列。

> 用 0 填充的数组索引称为**空单元格**，而用 1 填充的索引称为**非空单元格**。

**例:**

> **输入:** arr[] = {1，1，0，1}
> **输出:** 3
> **解释:**
> 移除 0 会将数组修改为{1，1，1}，从而将子数组的长度最大化为 3。
> **输入:** arr[] = {1，1，1，1，1}
> **输出:** 5

**方法:**
想法是将 1 的频率存储在每个索引的前缀和后缀中，以计算特定索引的两个方向上最长的连续 1 序列。按照以下步骤解决问题:

*   初始化两个数组 **l[]** 和 **r[]** ，分别从数组的左侧和右侧存储数组 **arr[]** 中最长的连续 **1s** 的长度。
*   在索引 **(0，N)** 上迭代输入数组，并为每个 **arr[i] = 1** 将**计数**增加 1。否则，存储**计数**的值，直到**l【I】**中的**(I–1)<sup>第</sup>个**索引将计数重置为零。

*   类似地，通过遍历索引**【N–1，0】**重复上述步骤，从右至右在**r【】**中存储**计数**。
*   对于包含 **0** 的每一个 **i <sup>第</sup>索引**索引，通过移除该 **0** 计算可能的非空子阵列的长度，该长度等于 **l[i] + r[i]** 。
*   计算所有这些长度的最大值并打印结果。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// of a subarray of 1s after removing
// at most one 0
int longestSubarray(int a[], int n)
{
    // Stores the count of consecutive
    // 1's from left
    int l[n];

    // Stores the count of consecutive
    // 1's from right
    int r[n];

    // Traverse left to right
    for (int i = 0, count = 0;
        i < n; i++) {

        // If cell is non-empty
        if (a[i] == 1)

            // Increase count
            count++;

        // If cell is empty
        else {

            // Store the count of
            // consecutive 1's
            // till (i - 1)-th index
            l[i] = count;
            count = 0;
        }
    }

    // Traverse from right to left
    for (int i = n - 1, count = 0;
        i >= 0; i--) {

        if (a[i] == 1)
            count++;

        else {

            // Store the count of
            // consecutive 1s
            // till (i + 1)-th index
            r[i] = count;
            count = 0;
        }
    }

    // Stores the length of
    // longest subarray
    int ans = -1;
    for (int i = 0; i < n; ++i) {

        if (a[i] == 0)

            // Store the maximum
            ans = max(ans, l[i] + r[i]);
    }

    // If array a contains only 1s
    // return n else return ans
    return ans < 0 ? n : ans;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 1, 1, 0, 1,
                0, 1, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestSubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum length
// of a subarray of 1s after removing
// at most one 0
public static int longestSubarray(int[] a,
                                int n)
{

    // Stores the count of consecutive
    // 1's from left
    int[] l = new int[n];

    // Stores the count of consecutive
    // 1's from right
    int[] r = new int[n];

    // Traverse left to right
    for(int i = 0, count = 0;
            i < n; i++)
    {

    // If cell is non-empty
    if (a[i] == 1)

        // Increase count
        count++;

    // If cell is empty
    else
    {

        // Store the count of
        // consecutive 1's
        // till (i - 1)-th index
        l[i] = count;
        count = 0;
    }
    }

    // Traverse from right to left
    for(int i = n - 1, count = 0;
            i >= 0; i--)
    {
    if (a[i] == 1)
        count++;

    else
    {

        // Store the count of
        // consecutive 1s
        // till (i + 1)-th index
        r[i] = count;
        count = 0;
        }
    }

    // Stores the length of
    // longest subarray
    int ans = -1;
    for(int i = 0; i < n; ++i)
    {
    if (a[i] == 0)

        // Store the maximum
        ans = Math.max(ans, l[i] + r[i]);
    }

    // If array a contains only 1s
    // return n else return ans
    return ans < 0 ? n : ans;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 0, 1, 1, 1, 0,
                1, 0, 1, 1 };
    int n = arr.length;

    System.out.println(longestSubarray(arr, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum length
# of a subarray of 1s after removing
# at most one 0
def longestSubarray(a, n):

    # Stores the count of consecutive
    # 1's from left
    l = [0] * (n)

    # Stores the count of consecutive
    # 1's from right
    r = [0] * (n)

    count = 0

    # Traverse left to right
    for i in range(n):

        # If cell is non-empty
        if (a[i] == 1):

            # Increase count
            count += 1

        # If cell is empty
        else:

            # Store the count of
            # consecutive 1's
            # till (i - 1)-th index
            l[i] = count
            count = 0

    count = 0
    # Traverse from right to left
    for i in range(n - 1, -1, -1):
        if (a[i] == 1):
            count += 1

        else:

            # Store the count of
            # consecutive 1s
            # till (i + 1)-th index
            r[i] = count
            count = 0

    # Stores the length of
    # longest subarray
    ans = -1
    for i in range(n):
        if (a[i] == 0):

            # Store the maximum
            ans = max(ans, l[i] + r[i])

    # If array a contains only 1s
    # return n else return ans
    return ans < 0 and n or ans

# Driver code
arr = [ 0, 1, 1, 1, 0, 1, 0, 1, 1 ]

n = len(arr)

print(longestSubarray(arr, n))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum length
// of a subarray of 1s after removing
// at most one 0
public static int longestSubarray(int[] a,
                                  int n)
{

    // Stores the count of consecutive
    // 1's from left
    int[] l = new int[n];

    // Stores the count of consecutive
    // 1's from right
    int[] r = new int[n];

    // Traverse left to right
    for(int i = 0, count = 0; i < n; i++)
    {

        // If cell is non-empty
        if (a[i] == 1)

            // Increase count
            count++;

        // If cell is empty
        else
        {

            // Store the count of
            // consecutive 1's
            // till (i - 1)-th index
            l[i] = count;
            count = 0;
        }
    }

    // Traverse from right to left
    for(int i = n - 1, count = 0;
            i >= 0; i--)
    {
    if (a[i] == 1)
        count++;

    else
    {

        // Store the count of
        // consecutive 1s
        // till (i + 1)-th index
        r[i] = count;
        count = 0;
        }
    }

    // Stores the length of
    // longest subarray
    int ans = -1;
    for(int i = 0; i < n; ++i)
    {
        if (a[i] == 0)

            // Store the maximum
            ans = Math.Max(ans, l[i] + r[i]);
    }

    // If array a contains only 1s
    // return n else return ans
    return ans < 0 ? n : ans;
}

// Driver code
public static void Main()
{
    int[] arr = { 0, 1, 1, 1, 0,
                  1, 0, 1, 1 };
    int n = arr.Length;

    Console.Write(longestSubarray(arr, n));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the above approach    
// Function to find the maximum length
    // of a subarray of 1s after removing
    // at most one 0
    function longestSubarray(a , n)
    {

        // Stores the count of consecutive
        // 1's from left
        var l = Array(n).fill(0);

        // Stores the count of consecutive
        // 1's from right
        var r = Array(n).fill(0);

        // Traverse left to right
        for (i = 0, count = 0; i < n; i++)
        {

            // If cell is non-empty
            if (a[i] == 1)

                // Increase count
                count++;

            // If cell is empty
            else {

                // Store the count of
                // consecutive 1's
                // till (i - 1)-th index
                l[i] = count;
                count = 0;
            }
        }

        // Traverse from right to left
        for (i = n - 1, count = 0; i >= 0; i--) {
            if (a[i] == 1)
                count++;

            else {

                // Store the count of
                // consecutive 1s
                // till (i + 1)-th index
                r[i] = count;
                count = 0;
            }
        }

        // Stores the length of
        // longest subarray
        var ans = -1;
        for (i = 0; i < n; ++i) {
            if (a[i] == 0)

                // Store the maximum
                ans = Math.max(ans, l[i] + r[i]);
        }

        // If array a contains only 1s
        // return n else return ans
        return ans < 0 ? n : ans;
    }

    // Driver code
        var arr = [ 0, 1, 1, 1, 0, 1, 0, 1, 1 ];
        var n = arr.length;
        document.write(longestSubarray(arr, n));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*