# 最大长度 L，使得长度 L 的所有子阵列之和小于 K

> 原文:[https://www . geeksforgeeks . org/最大长度-l-这样长度-l-的所有子阵列的总和小于-k/](https://www.geeksforgeeks.org/maximum-length-l-such-that-the-sum-of-all-subarrays-of-length-l-is-less-than-k/)

给定一组长度 **N** 和一个整数 **K** 。任务是找到最大长度 **L** ，使得长度 **L** 的所有子阵列的元素之和小于 **K** 。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 20
> **输出:** 5
> 长度为 5 的唯一子阵列是完整的
> 阵列和(1 + 2 + 3 + 4 + 5) = 15 < 20。
> **输入:** arr[] = {1，2，3，4，5}，K = 10
> **输出:** 2

**方法:**对于长度为 **K** 的子阵列的最大和，请执行[这篇](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)文章中讨论的方法。现在，可以执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来找到最大长度。由于阵列元素是正的，那么增加子阵列长度将增加该长度的子阵列元素的最大和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum
// in a subarray of size k
int maxSum(int arr[], int n, int k)
{
    // k must be greater
    if (n < k) {
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
    for (int i = k; i < n; i++) {
        curr_sum += arr[i] - arr[i - k];
        res = max(res, curr_sum);
    }

    return res;
}

// Function to return the length of subarray
// Sum of all the subarray of this
// length is less than or equal to K
int solve(int arr[], int n, int k)
{
    int max_len = 0, l = 0, r = n, m;

    // Binary search from l to r as all the
    // array elements are positive so that
    // the maximum subarray sum is monotonically
    // increasing
    while (l <= r) {
        m = (l + r) / 2;

        // Check if the subarray sum is
        // greater than K or not
        if (maxSum(arr, n, m) > k)
            r = m - 1;
        else {
            l = m + 1;

            // Update the maximum length
            max_len = m;
        }
    }
    return max_len;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(int);
    int k = 10;

    cout << solve(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximum sum
    // in a subarray of size k
    static int maxSum(int arr[], int n, int k)
    {
        // k must be greater
        if (n < k)
        {
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
            res = Math.max(res, curr_sum);
        }

        return res;
    }

    // Function to return the length of subarray
    // Sum of all the subarray of this
    // length is less than or equal to K
    static int solve(int arr[], int n, int k)
    {
        int max_len = 0, l = 0, r = n, m;

        // Binary search from l to r as all the
        // array elements are positive so that
        // the maximum subarray sum is monotonically
        // increasing
        while (l <= r)
        {
            m = (l + r) / 2;

            // Check if the subarray sum is
            // greater than K or not
            if (maxSum(arr, n, m) > k)
                r = m - 1;
            else
            {
                l = m + 1;

                // Update the maximum length
                max_len = m;
            }
        }
        return max_len;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;

        int k = 10;

        System.out.println(solve(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum sum
# in a subarray of size k
def maxSum(arr, n, k) :

    # k must be greater
    if (n < k) :
        return -1;

    # Compute sum of first window of size k
    res = 0;

    for i in range(k) :
        res += arr[i];

    # Compute sums of remaining windows by
    # removing first element of previous
    # window and adding last element of
    # current window.
    curr_sum = res;

    for i in range(k, n) :
        curr_sum += arr[i] - arr[i - k];
        res = max(res, curr_sum);

    return res;

# Function to return the length of subarray
# Sum of all the subarray of this
# length is less than or equal to K
def solve(arr, n, k) :

    max_len = 0; l = 0; r = n;

    # Binary search from l to r as all the
    # array elements are positive so that
    # the maximum subarray sum is monotonically
    # increasing
    while (l <= r) :
        m = (l + r) // 2;

        # Check if the subarray sum is
        # greater than K or not
        if (maxSum(arr, n, m) > k) :
            r = m - 1;
        else :
            l = m + 1;

            # Update the maximum length
            max_len = m;

    return max_len;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];
    n = len(arr);
    k = 10;

    print(solve(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum sum
    // in a subarray of size k
    static int maxSum(int []arr, int n, int k)
    {
        // k must be greater
        if (n < k)
        {
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

    // Function to return the length of subarray
    // Sum of all the subarray of this
    // length is less than or equal to K
    static int solve(int []arr, int n, int k)
    {
        int max_len = 0, l = 0, r = n, m;

        // Binary search from l to r as all the
        // array elements are positive so that
        // the maximum subarray sum is monotonically
        // increasing
        while (l <= r)
        {
            m = (l + r) / 2;

            // Check if the subarray sum is
            // greater than K or not
            if (maxSum(arr, n, m) > k)
                r = m - 1;
            else
            {
                l = m + 1;

                // Update the maximum length
                max_len = m;
            }
        }
        return max_len;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;

        int k = 10;

        Console.WriteLine(solve(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the maximum sum
// in a subarray of size k
    function maxSum(arr , n , k) {
        // k must be greater
        if (n < k) {
            return -1;
        }

        // Compute sum of first window of size k
        var res = 0;
        for (i = 0; i < k; i++)
            res += arr[i];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        var curr_sum = res;
        for (i = k; i < n; i++) {
            curr_sum += arr[i] - arr[i - k];
            res = Math.max(res, curr_sum);
        }

        return res;
    }

    // Function to return the length of subarray
    // Sum of all the subarray of this
    // length is less than or equal to K
    function solve(arr , n , k) {
        var max_len = 0, l = 0, r = n, m;

        // Binary search from l to r as all the
        // array elements are positive so that
        // the maximum subarray sum is monotonically
        // increasing
        while (l <= r) {
            m = parseInt((l + r) / 2);

            // Check if the subarray sum is
            // greater than K or not
            if (maxSum(arr, n, m) > k)
                r = m - 1;
            else {
                l = m + 1;

                // Update the maximum length
                max_len = m;
            }
        }
        return max_len;
    }

    // Driver code

        var arr = [ 1, 2, 3, 4, 5 ];
        var n = arr.length;

        var k = 10;

        document.write(solve(arr, n, k));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```