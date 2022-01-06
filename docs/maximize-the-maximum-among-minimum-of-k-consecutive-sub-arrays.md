# 最大化 K 个连续子阵列中的最小值

> 原文:[https://www . geeksforgeeks . org/k 个连续子阵列中最大化最小化最大值/](https://www.geeksforgeeks.org/maximize-the-maximum-among-minimum-of-k-consecutive-sub-arrays/)

给定一个整数 **K** 和一个数组 **arr[]** ，任务是将数组 arr[]拆分成 K 个连续的子数组，在 **K 个**连续子数组的最小值中找到*最大值的**最大可能值**。*

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 5
> 将数组拆分为[1，2，3，4]和[5]。两个连续子阵列的最小值是 1 和 5。
> 最大值(1，5) = 5。这种分割确保了最大可能的价值。
> 
> **输入:** arr[] = {-4，-5，-3，-2，-1}，K = 1
> T3】输出: -5
> 只能有一个子阵列。因此，最小(-4，-5，-3，-2，-1) = -5

**方法:**解决方案可以分为 3 种可能的情况:

1.  **当 K = 1 时:**在这种情况下，答案总是等于数组的**最小值**，因为数组只分成一个子数组，即数组本身。
2.  **当 K ≥ 3:** 在这种情况下，答案总是等于阵的**最大值**。当数组必须被分成 3 个或更多的段时，那么总是保持一个段只包含数组中的一个元素，即最大元素。
3.  **K = 2 时:**这是最棘手的情况。只有一个前缀和一个后缀，因为只能有两个子数组。维护前缀最小值和后缀最小值的数组。然后对于每个元素**arr【I】**，更新 **ans = max(ans，max(前缀最小值在 I，后缀最小值在 i + 1))** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return maximum possible value
// of maximum of minimum of K sub-arrays
int maximizeMinimumOfKSubarrays(const int* arr, int n, int k)
{
    int m = INT_MAX;
    int M = INT_MIN;

    // Compute maximum and minimum
    // of the array
    for (int i = 0; i < n; i++) {
        m = min(m, arr[i]);
        M = max(M, arr[i]);
    }

    // If k = 1 then return the
    // minimum of the array
    if (k == 1) {
        return m;
    }
    // If k >= 3 then return the
    // maximum of the array
    else if (k >= 3) {
        return M;
    }

    // If k = 2 then maintain prefix
    // and suffix minimums
    else {

        // Arrays to store prefix
        // and suffix minimums
        int L[n], R[n];

        L[0] = arr[0];
        R[n - 1] = arr[n - 1];

        // Prefix minimum
        for (int i = 1; i < n; i++)
            L[i] = min(L[i - 1], arr[i]);

        // Suffix minimum
        for (int i = n - 2; i >= 0; i--)
            R[i] = min(R[i + 1], arr[i]);

        int maxVal = INT_MIN;

        // Get the maximum possible value
        for (int i = 0; i < n - 1; i++)
            maxVal = max(maxVal, max(L[i], R[i + 1]));

        return maxVal;
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << maximizeMinimumOfKSubarrays(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // Function to return maximum possible value
    // of maximum of minimum of K sub-arrays
    static int maximizeMinimumOfKSubarrays(int arr[], int n, int k)
    {
        int m = Integer.MAX_VALUE;
        int M = Integer.MIN_VALUE;

        // Compute maximum and minimum
        // of the array
        for (int i = 0; i < n; i++) {
            m = Math.min(m, arr[i]);
            M = Math.max(M, arr[i]);
        }

        // If k = 1 then return the
        // minimum of the array
        if (k == 1) {
            return m;
        }

        // If k >= 3 then return the
        // maximum of the array
        else if (k >= 3) {
            return M;
        }

        // If k = 2 then maintain prefix
        // and suffix minimums
        else {

            // Arrays to store prefix
            // and suffix minimums
            int L[] = new int[n], R[] = new int[n];

            L[0] = arr[0];
            R[n - 1] = arr[n - 1];

            // Prefix minimum
            for (int i = 1; i < n; i++)
                L[i] = Math.min(L[i - 1], arr[i]);

            // Suffix minimum
            for (int i = n - 2; i >= 0; i--)
                R[i] = Math.min(R[i + 1], arr[i]);

            int maxVal = Integer.MIN_VALUE;

            // Get the maximum possible value
            for (int i = 0; i < n - 1; i++)
                maxVal = Math.max(maxVal, Math.max(L[i], R[i + 1]));

            return maxVal;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        int k = 2;

        System.out.println(maximizeMinimumOfKSubarrays(arr, n, k));
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys

# Function to return maximum possible value
# of maximum of minimum of K sub-arrays
def maximizeMinimumOfKSubarrays(arr, n, k) :

    m = sys.maxsize;
    M = -(sys.maxsize - 1);

    # Compute maximum and minimum
    # of the array
    for i in range(n) :
        m = min(m, arr[i]);
        M = max(M, arr[i]);

    # If k = 1 then return the
    # minimum of the array
    if (k == 1) :
        return m;

    # If k >= 3 then return the
    # maximum of the array
    elif (k >= 3) :
        return M;

    # If k = 2 then maintain prefix
    # and suffix minimums
    else :

        # Arrays to store prefix
        # and suffix minimums
        L = [0] * n;
        R = [0] * n;

        L[0] = arr[0];
        R[n - 1] = arr[n - 1];

        # Prefix minimum
        for i in range(1, n) :
            L[i] = min(L[i - 1], arr[i]);

        # Suffix minimum
        for i in range(n - 2, -1, -1) :
            R[i] = min(R[i + 1], arr[i]);

        maxVal = -(sys.maxsize - 1);

        # Get the maximum possible value
        for i in range(n - 1) :
            maxVal = max(maxVal, max(L[i],
                                 R[i + 1]));

        return maxVal;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];
    n = len(arr);
    k = 2;

    print(maximizeMinimumOfKSubarrays(arr, n, k));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;

public class GFG {

    // Function to return maximum possible value
    // of maximum of minimum of K sub-arrays
    static int maximizeMinimumOfKSubarrays(int[] arr, int n, int k)
    {
        int m = int.MaxValue;
        int M = int.MinValue;

        // Compute maximum and minimum
        // of the array
        for (int i = 0; i < n; i++) {
            m = Math.Min(m, arr[i]);
            M = Math.Max(M, arr[i]);
        }

        // If k = 1 then return the
        // minimum of the array
        if (k == 1) {
            return m;
        }

        // If k >= 3 then return the
        // maximum of the array
        else if (k >= 3) {
            return M;
        }

        // If k = 2 then maintain prefix
        // and suffix minimums
        else {

            // Arrays to store prefix
            // and suffix minimums
            int[] L = new int[n];
            int[] R = new int[n];

            L[0] = arr[0];
            R[n - 1] = arr[n - 1];

            // Prefix minimum
            for (int i = 1; i < n; i++)
                L[i] = Math.Min(L[i - 1], arr[i]);

            // Suffix minimum
            for (int i = n - 2; i >= 0; i--)
                R[i] = Math.Min(R[i + 1], arr[i]);

            int maxVal = int.MinValue;

            // Get the maximum possible value
            for (int i = 0; i < n - 1; i++)
                maxVal = Math.Max(maxVal, Math.Max(L[i], R[i + 1]));

            return maxVal;
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(maximizeMinimumOfKSubarrays(arr, n, k));
    }
}
/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return maximum possible value
// of maximum of minimum of K sub-arrays
function maximizeMinimumOfKSubarrays($arr, $n, $k)
{
    $m = PHP_INT_MAX;
    $M = PHP_INT_MIN;

    // Compute maximum and minimum
    // of the array
    for ($i = 0; $i < $n; $i++)
    {
        $m = min($m, $arr[$i]);
        $M = max($M, $arr[$i]);
    }

    // If k = 1 then return the
    // minimum of the array
    if ($k == 1)
    {
        return $m;
    }

    // If k >= 3 then return the
    // maximum of the array
    else if ($k >= 3)
    {
        return $M;
    }

    // If k = 2 then maintain prefix
    // and suffix minimums
    else
    {

        // Arrays to store prefix
        // and suffix minimums
        $L[0] = $arr[0];
        $R[$n - 1] = $arr[$n - 1];

        // Prefix minimum
        for ($i = 1; $i < $n; $i++)
            $L[$i] = min($L[$i - 1], $arr[$i]);

        // Suffix minimum
        for ($i = $n - 2; $i >= 0; $i--)
            $R[$i] = min($R[$i + 1], $arr[$i]);

        $maxVal = PHP_INT_MIN;

        // Get the maximum possible value
        for ($i = 0; $i < $n - 1; $i++)
            $maxVal = max($maxVal,
                      max($L[$i], $R[$i + 1]));

        return $maxVal;
    }
}

// Driver code
$arr = array( 1, 2, 3, 4, 5 );
$n = sizeof($arr);
$k = 2;

echo maximizeMinimumOfKSubarrays($arr, $n, $k);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of above approach

    // Function to return maximum possible value
    // of maximum of minimum of K sub-arrays
    function maximizeMinimumOfKSubarrays(arr, n, k)
    {
        let m = Number.MAX_VALUE;
        let M = Number.MIN_VALUE;

        // Compute maximum and minimum
        // of the array
        for (let i = 0; i < n; i++) {
            m = Math.min(m, arr[i]);
            M = Math.max(M, arr[i]);
        }

        // If k = 1 then return the
        // minimum of the array
        if (k == 1) {
            return m;
        }

        // If k >= 3 then return the
        // maximum of the array
        else if (k >= 3) {
            return M;
        }

        // If k = 2 then maintain prefix
        // and suffix minimums
        else {

            // Arrays to store prefix
            // and suffix minimums
            let L = new Array(n);
            L.fill(0);
            let R = new Array(n);
            R.fill(0);

            L[0] = arr[0];
            R[n - 1] = arr[n - 1];

            // Prefix minimum
            for (let i = 1; i < n; i++)
                L[i] = Math.min(L[i - 1], arr[i]);

            // Suffix minimum
            for (let i = n - 2; i >= 0; i--)
                R[i] = Math.min(R[i + 1], arr[i]);

            let maxVal = Number.MIN_VALUE;

            // Get the maximum possible value
            for (let i = 0; i < n - 1; i++)
                maxVal = Math.max(maxVal, Math.max(L[i], R[i + 1]));

            return maxVal;
        }
    }

    let arr = [ 1, 2, 3, 4, 5 ];
    let n = arr.length;
    let k = 2;

    document.write(maximizeMinimumOfKSubarrays(arr, n, k));

</script>
```

**Output:** 

```
5
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)