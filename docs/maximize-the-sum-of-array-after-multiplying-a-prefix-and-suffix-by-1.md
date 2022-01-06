# 将前缀和后缀乘以-1 后最大化数组的和

> 原文:[https://www . geesforgeks . org/将前缀和后缀乘以 1 后的数组总和最大化/](https://www.geeksforgeeks.org/maximize-the-sum-of-array-after-multiplying-a-prefix-and-suffix-by-1/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是通过最多执行一次以下操作来最大化数组所有元素的总和。

*   选择数组的前缀，并将所有元素乘以-1。
*   选择数组的后缀，并将所有元素乘以-1。

**示例:**

> **输入:** arr[] = {-1，-2，-3}
> **输出:** 6
> **说明:**
> **运算 1:** 数组的前缀–{-1，-2，-3}
> 可以乘以-1 得到最大和。
> 运算后的数组:{1，2，3}
> 总和= 1 + 2 + 3 = 6
> 
> **输入:** arr[] = {-4，2，0，5，0}
> **输出:** 11
> **解释:**
> **运算 1:** 数组的前缀–{-4 }
> 可以乘以-1 得到最大和。
> 运算后的数组:{4，2，0，5，0}
> Sum = 4 + 2 + 0 + 5 + 0 = 11

**方法:**问题中的关键观察是如果前缀和后缀的选择范围相交，那么相交部分的元素具有相同的符号。因此，选择前缀和后缀数组的非交叉范围总是更好。下面是步骤的图示:

*   很容易观察到，阵列中会有一部分/子阵列的和与原始的相同，而其他元素的和是相反的。所以数组的新总和将是:

```
// X - Sum of subarray which is not in
//     the range of the prefix and suffix
// S - Sum of the original array

New Sum = X + -1*(S - X) = 2*X - S 
```

*   因此，想法是最大化 X 的值，以获得最大和，因为 S 是不可改变的常数值。这可以在[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)的帮助下实现。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum sum of the array by
// multiplying the prefix and suffix
// of the array by -1

#include <bits/stdc++.h>

using namespace std;

// Kadane's algorithm to find
// the maximum subarray sum
int maxSubArraySum(int a[], int size)
{
    int max_so_far = INT_MIN,
         max_ending_here = 0;

    // Loop to find the maximum subarray
    // array sum in the given array
    for (int i = 0; i < size; i++) {
        max_ending_here =
             max_ending_here + a[i];
        if (max_ending_here < 0)
            max_ending_here = 0;
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

// Function to find the maximum
// sum of the array by multiplying
// the prefix and suffix by -1
int maxSum(int a[], int n)
{

    // Total intital sum
    int S = 0;

    // Loop to find the maximum
    // sum of the array
    for (int i = 0; i < n; i++)
        S += a[i];
    int X = maxSubArraySum(a, n);

    // Maximum value
    return 2 * X - S;
}

// Driver Code
int main()
{
    int a[] = { -1, -2, -3 };
    int n = sizeof(a) / sizeof(a[0]);
    int max_sum = maxSum(a, n);
    cout << max_sum;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum of the array by
// multiplying the prefix and suffix
// of the array by -1
class GFG
{

    // Kadane's algorithm to find
    // the maximum subarray sum
    static int maxSubArraySum(int a[], int size)
    {
        int max_so_far = Integer.MIN_VALUE,
             max_ending_here = 0;

        // Loop to find the maximum subarray
        // array sum in the given array
        for (int i = 0; i < size; i++) {
            max_ending_here =
                 max_ending_here + a[i];
            if (max_ending_here < 0)
                max_ending_here = 0;
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;
        }
        return max_so_far;
    }

    // Function to find the maximum
    // sum of the array by multiplying
    // the prefix and suffix by -1
    static int maxSum(int a[], int n)
    {

        // Total intital sum
        int S = 0;
        int i;

        // Loop to find the maximum
        // sum of the array
        for (i = 0; i < n; i++)
            S += a[i];
        int X = maxSubArraySum(a, n);

        // Maximum value
        return 2 * X - S;
    }

    // Driver Code
    public static void main(String []args)
    {
        int a[] = { -1, -2, -3 };
        int n = a.length;
        int max_sum = maxSum(a, n);
        System.out.print(max_sum);
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum sum of the array by
# multiplying the prefix and suffix
# of the array by -1

# Kadane's algorithm to find
# the maximum subarray sum
def maxSubArraySum(a, size):
    max_so_far = -10**9
    max_ending_here = 0

    # Loop to find the maximum subarray
    # array sum in the given array
    for i in range(size):
        max_ending_here = max_ending_here + a[i]
        if (max_ending_here < 0):
            max_ending_here = 0
        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here
    return max_so_far

# Function to find the maximum
# sum of the array by multiplying
# the prefix and suffix by -1
def maxSum(a, n):

    # Total intital sum
    S = 0

    # Loop to find the maximum
    # sum of the array
    for i in range(n):
        S += a[i]
    X = maxSubArraySum(a, n)

    # Maximum value
    return 2 * X - S

# Driver Code
if __name__ == '__main__':
    a=[-1, -2, -3]
    n= len(a)
    max_sum = maxSum(a, n)
    print(max_sum)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// maximum sum of the array by
// multiplying the prefix and suffix
// of the array by -1
using System;

class GFG
{

    // Kadane's algorithm to find
    // the maximum subarray sum
    static int maxSubArraySum(int []a, int size)
    {
        int max_so_far = int.MinValue,
             max_ending_here = 0;

        // Loop to find the maximum subarray
        // array sum in the given array
        for (int i = 0; i < size; i++) {
            max_ending_here =
                 max_ending_here + a[i];
            if (max_ending_here < 0)
                max_ending_here = 0;
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;
        }
        return max_so_far;
    }

    // Function to find the maximum
    // sum of the array by multiplying
    // the prefix and suffix by -1
    static int maxSum(int []a, int n)
    {

        // Total intital sum
        int S = 0;
        int i;

        // Loop to find the maximum
        // sum of the array
        for (i = 0; i < n; i++)
            S += a[i];
        int X = maxSubArraySum(a, n);

        // Maximum value
        return 2 * X - S;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []a = { -1, -2, -3 };
        int n = a.Length;
        int max_sum = maxSum(a, n);
        Console.Write(max_sum);
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// maximum sum of the array by
// multiplying the prefix and suffix
// of the array by -1   

// Kadane's algorithm to find
// the maximum subarray sum
function maxSubArraySum(a, size)
{
    var max_so_far = Number.MIN_VALUE,
        max_ending_here = 0;

    // Loop to find the maximum subarray
    // array sum in the given array
    for(i = 0; i < size; i++)
    {
        max_ending_here = max_ending_here + a[i];

        if (max_ending_here < 0)
            max_ending_here = 0;

        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

// Function to find the maximum
// sum of the array by multiplying
// the prefix and suffix by -1
function maxSum(a, n)
{

    // Total intital sum
    var S = 0;
    var i;

    // Loop to find the maximum
    // sum of the array
    for(i = 0; i < n; i++)
        S += a[i];

    var X = maxSubArraySum(a, n);

    // Maximum value
    return 2 * X - S;
}

// Driver Code
var a = [ -1, -2, -3 ];
var n = a.length;
var max_sum = maxSum(a, n);

document.write(max_sum);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N)