# 非负整数的最长子阵列

> 原文:[https://www . geesforgeks . org/long-subarray-非负整数/](https://www.geeksforgeeks.org/longest-subarray-non-negative-integers/)

给定一个数组，返回非负整数最长子数组的长度
**示例:**

```
Input : {2, 3, 4, -1, -2, 1, 5, 6, 3}
Output : 4

The subarray [ 1, 5, 6, 3] has length 4 and 
contains no negative integers

Input : {1, 0, 0, 1, -1, -1, 0, 0, 1, 0}
Output : 4

Subarrays [1, 0, 0, 1] and [0, 0, 1, 0] have 
equal lengths but sum of first one is greater
so that will be the output.
```

我们遵循简单的双指针窗口方法。最初 si 指向 curr 子阵列的起点，即使用非负整数 ei 遍历阵列。每当出现一个负元素时，我们将与迄今为止最大子阵列的长度进行比较，如果当前长度更大，则更新开始和大小。最后，我们从长度尺寸的开始返回子阵列，第一个元素作为子阵列的尺寸。

## C++

```
// C++ program to find length of the longest
// subarray with non-negative numbers.
#include<iostream>
using namespace std;

// Function that returns the longest
// subarray of non-negative integers
int longestSubarry(int *arr, int n)
{
    // Initialize result
    int res = 0;

    // Traverse array
    for (int i = 0; i < n; i++)
    {
        // Count of current
        // non-negative integers
        int curr_count = 0;

        while (i < n && arr[i] >= 0)
        {
            curr_count++;
            i++;
        }

        // Update result if required.
        res = max(res, curr_count);
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = {1, 0, 4, 0, 1, -1, -1,
                           0, 0, 1, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << longestSubarry(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the longest
// subarray with non-negative numbers.

class GFG
{

    // Function that returns the longest
    // subarray of non-negative integers
    static int longestSubarry(int arr[], int n)
    {
        // Initialize result
        int res = 0;

        // Traverse array
        for (int i = 0; i < n; i++)
        {
            // Count of current non-
            // negative integers
            int curr_count = 0;
            while (i < n && arr[i] >= 0)
            {
                curr_count++;
                i++;
            }

            // Update result if required.
            res = Math.max(res, curr_count);
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 0, 4, 0, 1, -1,
                        -1, 0, 0, 1, 0};
        int n = arr.length;
        System.out.println(longestSubarry(arr, n));
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python program to find
# length of the longest
# subarray with
# non-negative numbers.

# Function that returns
# the longest subarray
# of non-negative integers
def longestSubarry(arr,n):

    # Initialize result
    res = 0

    # Traverse array
    for i in range(n):

        # Count of current
        # non-negative integers
        curr_count = 0
        while (i < n and arr[i] >= 0):

            curr_count+=1
            i+=1

        # Update result if required.
        res = max(res, curr_count)

    return res

# Driver code

arr= [1, 0, 4, 0, 1, -1, -1, 0, 0, 1, 0]
n = len(arr)
print(longestSubarry(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find length of the longest
// subarray with non-negative numbers.
using System;

class GFG
{

    // Function that returns the longest
    // subarray of non-negative integers
    static int longestSubarry(int []arr, int n)
    {
        // Initialize result
        int res = 0;

        // Traverse array
        for (int i = 0; i < n; i++)
        {
            // Count of current non-
            // negative integers
            int curr_count = 0;
            while (i < n && arr[i] >= 0)
            {
                curr_count++;
                i++;
            }

            // Update result if required.
            res = Math.Max(res, curr_count);
        }

        return res;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 0, 4, 0, 1, -1,
                        -1, 0, 0, 1, 0};
        int n = arr.Length;
        Console.Write(longestSubarry(arr, n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length
// of the longest subarray with
// non-negative numbers.

// Function that returns the longest
// subarray of non-negative integers
function longestSubarry($arr, $n)
{
    // Initialize result
    $res = 0;

    // Traverse array
    for ($i = 0; $i < $n; $i++)
    {
        // Count of current
        // non-negative integers
        $curr_count = 0;

        while ($i < $n && $arr[$i] >= 0)
        {
            $curr_count++;
            $i++;
        }

        // Update result if required.
        $res = max($res, $curr_count);
    }

    return $res;
}

// Driver code
$arr = array(1, 0, 4, 0, 1, -1,
            -1, 0, 0, 1, 0);
$n = sizeof($arr) / sizeof($arr[0]);
echo longestSubarry($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
 // JavaScript program for the above approach

// Function that returns the longest
// subarray of non-negative integers
function longestSubarry(arr, n)
{
    // Initialize result
    let res = 0;

    // Traverse array
    for (let i = 0; i < n; i++)
    {
        // Count of current
        // non-negative integers
        let curr_count = 0;

        while (i < n && arr[i] >= 0)
        {
            curr_count++;
            i++;
        }

        // Update result if required.
        res = Math.max(res, curr_count);
    }

    return res;
}

// Driver code

    var arr = [1, 0, 4, 0, 1, -1, -1,
                           0, 0, 1, 0];
    let n = arr.length;
    document.write(longestSubarry(arr, n));

// This code is contributed by Potta Lokesh
    </script>
```

**输出:**

```
5
```

**时间复杂度:** O(n)
**练习:**
修改以上解打印结果子阵。另外，如果两个子阵列具有相同的计数，则打印总和较大的子阵列。
本文由**阿迪提·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。