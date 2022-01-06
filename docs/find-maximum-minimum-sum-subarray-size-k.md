# 求大小为 k 的子阵列的最大(或最小)和

> 原文:[https://www . geesforgeks . org/find-maximum-minimum-sum-subarray-size-k/](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)

给定一个整数数组和一个数 k，求大小为 k 的子数组的最大和。

**示例:**

```
Input  : arr[] = {100, 200, 300, 400}
         k = 2
Output : 700

Input  : arr[] = {1, 4, 2, 10, 23, 3, 1, 0, 20}
         k = 4 
Output : 39
We get maximum sum by adding subarray {4, 2, 10, 23}
of size 4.

Input  : arr[] = {2, 3}
         k = 3
Output : Invalid
There is no subarray of size 3 as size of whole
array is 2\. 
```

一个**简单的解决方案**是[生成 k 大小的所有子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，计算它们的和，最后返回所有和的最大值。这个解的时间复杂度是 O(n*k)。

一个**有效解**是基于这样一个事实，即大小为 k 的子阵列(或窗口)的和可以在 O(1)时间内使用大小为 k 的前一个子阵列(或窗口)的和获得。除了大小为 k 的第一个子阵列，对于其他子阵列，我们通过移除最后一个窗口的第一个元素并添加当前窗口的最后一个元素来计算和。
下面是上述想法的实现。

## C++

```
// O(n) solution for finding maximum sum of
// a subarray of size k
#include <iostream>
using namespace std;

// Returns maximum sum in a subarray of size k.
int maxSum(int arr[], int n, int k)
{
    // k must be greater
    if (n < k)
    {
       cout << "Invalid";
       return -1;
    }

    // Compute sum of first window of size k
    int res = 0;
    for (int i=0; i<k; i++)
       res += arr[i];

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window.
    int curr_sum = res;
    for (int i=k; i<n; i++)
    {
       curr_sum += arr[i] - arr[i-k];
       res = max(res, curr_sum);
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = {1, 4, 2, 10, 2, 3, 1, 0, 20};
    int k = 4;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << maxSum(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Find maximum (or minimum)
// sum of a subarray of size k
import java.util.*;

class GFG {

    // Returns maximum sum in a subarray of size k.
    public static int maxSum(int arr[], int n, int k)
    {
        // k must be greater
        if (n < k)
        {
           System.out.println("Invalid");
           return -1;
        }

        // Compute sum of first window of size k
        int res = 0;
        for (int i=0; i<k; i++)
           res += arr[i];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        int curr_sum = res;
        for (int i=k; i<n; i++)
        {
           curr_sum += arr[i] - arr[i-k];
           res = Math.max(res, curr_sum);
        }

        return res;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 4, 2, 10, 2, 3, 1, 0, 20};
        int k = 4;
        int n = arr.length;
        System.out.println(maxSum(arr, n, k));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# O(n) solution in Python3 for finding
# maximum sum of a subarray of size k

# Returns maximum sum in
# a subarray of size k.
def maxSum(arr, n, k):

    # k must be greater
    if (n < k):

        print("Invalid")
        return -1

    # Compute sum of first
    # window of size k
    res = 0
    for i in range(k):
        res += arr[i]

    # Compute sums of remaining windows by
    # removing first element of previous
    # window and adding last element of
    # current window.
    curr_sum = res
    for i in range(k, n):

        curr_sum += arr[i] - arr[i-k]
        res = max(res, curr_sum)

    return res

# Driver code
arr = [1, 4, 2, 10, 2, 3, 1, 0, 20]
k = 4
n = len(arr)
print(maxSum(arr, n, k))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code for Find maximum (or minimum)
// sum of a subarray of size k
using System;

class GFG {

    // Returns maximum sum in
    // a subarray of size k.
    public static int maxSum(int []arr,
                             int n,
                             int k)
    {

        // k must be greater
        if (n < k)
        {
            Console.Write("Invalid");
            return -1;
        }

        // Compute sum of first window of size k
        int res = 0;
        for (int i = 0; i < k; i++)
        res += arr[i];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        int curr_sum = res;
        for (int i = k; i < n; i++)
        {
            curr_sum += arr[i] - arr[i - k];
            res = Math.Max(res, curr_sum);
        }

        return res;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 4, 2, 10, 2, 3, 1, 0, 20};
        int k = 4;
        int n = arr.Length;
        Console.Write(maxSum(arr, n, k));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// O(n) solution for finding maximum
// sum of a subarray of size k

// Returns maximum sum in a
// subarray of size k.
function maxSum($arr, $n, $k)
{

    // k must be greater
    if ($n < $k)
    {
        echo "Invalid";
        return -1;
    }

    // Compute sum of first
    // window of size k
    $res = 0;
    for($i = 0; $i < $k; $i++)
    $res += $arr[$i];

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window.
    $curr_sum = $res;
    for($i = $k; $i < $n; $i++)
    {
        $curr_sum += $arr[$i] -
                     $arr[$i - $k];
        $res = max($res, $curr_sum);
    }

    return $res;
}

    // Driver Code
    $arr = array(1, 4, 2, 10, 2, 3, 1, 0, 20);
    $k = 4;
    $n = sizeof($arr);
    echo maxSum($arr, $n, $k);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // JAVA SCRIPT Code for Find maximum (or minimum)
    // sum of a subarray of size k

    // Returns maximum sum in a subarray of size k.
    function maxSum(arr,n,k)
    {
        // k must be greater
        if (n < k)
        {
            document.write("Invalid");
            return -1;
        }

        // Compute sum of first window of size k
        let res = 0;
        for (let i=0; i<k; i++)
        res += arr[i];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        let curr_sum = res;
        for (let i=k; i<n; i++)
        {
            curr_sum += arr[i] - arr[i-k];
            res = Math.max(res, curr_sum);
        }

        return res;
    }

    /* Driver program to test above function */

        let arr = [1, 4, 2, 10, 2, 3, 1, 0, 20];
        let k = 4;
        let n = arr.length;
        document.write(maxSum(arr, n, k));

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**输出:**

```
24
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由**阿布舍克·古普塔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息