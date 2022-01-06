# 最大和双主音子序列

> 原文:[https://www . geesforgeks . org/maximum-sum-bi-tonic-sub sequence/](https://www.geeksforgeeks.org/maximum-sum-bi-tonic-sub-sequence/)

给定一个整数数组。arr[]的[子序列](http://en.wikipedia.org/wiki/Subsequence)如果是先增后减的，则称为 Bitonic。
**例:**

```
Input : arr[] = {1, 15, 51, 45, 33, 
                   100, 12, 18, 9}
Output : 194
Explanation : Bi-tonic Sub-sequence are :
             {1, 51, 9} or {1, 51, 100, 18, 9} or
             {1, 15, 51, 100, 18, 9}  or 
             {1, 15, 45, 100, 12, 9}  or 
             {1, 15, 45, 100, 18, 9} .. so on            
Maximum sum Bi-tonic sub-sequence is 1 + 15 +
51 + 100 + 18 + 9 = 194   

Input : arr[] = {80, 60, 30, 40, 20, 10} 
Output : 210  
```

这个问题是标准[最长递增子序列(LIS)问题](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)和[最长双音素子序列](https://www.geeksforgeeks.org/dynamic-programming-set-15-longest-bitonic-subsequence/)的变种。
我们构造了两个数组 MSIBS[]和 MSDBS[]。存储以 arr[i]结尾的递增子序列的和。MSDBS[i]存储从 arr[i]开始的递减子序列的和。最后，我们需要返回 MSIBS[I]+MSDB[I]–Arr[I]的最大和。
以下是以上思路的实现

## C++

```
// C++ program to find maximum sum of bi-tonic sub-sequence
#include <bits/stdc++.h>
using namespace std;

// Function return maximum sum of Bi-tonic sub-sequence
int MaxSumBS(int arr[], int n)
{
    int max_sum = INT_MIN;

    // MSIBS[i] ==> Maximum sum Increasing Bi-tonic
    // subsequence ending with arr[i]
    // MSDBS[i] ==> Maximum sum Decreasing Bi-tonic
    // subsequence starting with arr[i]
    // Initialize MSDBS and MSIBS values as arr[i] for
    // all indexes
    int MSIBS[n], MSDBS[n];
    for (int i = 0; i < n; i++) {
        MSDBS[i] = arr[i];
        MSIBS[i] = arr[i];
    }

    // Compute MSIBS values from left to right */
    for (int i = 1; i < n; i++)
        for (int j = 0; j < i; j++)
            if (arr[i] > arr[j] && MSIBS[i] < MSIBS[j] + arr[i])
                MSIBS[i] = MSIBS[j] + arr[i];

    // Compute MSDBS values from right to left
    for (int i = n - 2; i >= 0; i--)
        for (int j = n - 1; j > i; j--)
            if (arr[i] > arr[j] && MSDBS[i] < MSDBS[j] + arr[i])
                MSDBS[i] = MSDBS[j] + arr[i];

    // Find the maximum value of MSIBS[i] + MSDBS[i] - arr[i]
    for (int i = 0; i < n; i++)
        max_sum = max(max_sum, (MSDBS[i] + MSIBS[i] - arr[i]));

    // return max sum of bi-tonic sub-sequence
    return max_sum;
}

// Driver program
int main()
{
    int arr[] = { 1, 15, 51, 45, 33, 100, 12, 18, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Sum : " << MaxSumBS(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find maximum
// sum of bi-tonic sub-sequence
import java.io.*;

class GFG {

    // Function return maximum sum
    // of Bi-tonic sub-sequence
    static int MaxSumBS(int arr[], int n)
    {
        int max_sum = Integer.MIN_VALUE;

        // MSIBS[i] ==> Maximum sum Increasing Bi-tonic
        // subsequence ending with arr[i]
        // MSDBS[i] ==> Maximum sum Decreasing Bi-tonic
        // subsequence starting with arr[i]
        // Initialize MSDBS and MSIBS values as arr[i] for
        // all indexes
        int MSIBS[] = new int[n];
        int MSDBS[] = new int[n];
        for (int i = 0; i < n; i++) {
            MSDBS[i] = arr[i];
            MSIBS[i] = arr[i];
        }

        // Compute MSIBS values from left to right */
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j] && MSIBS[i] < MSIBS[j] + arr[i])
                    MSIBS[i] = MSIBS[j] + arr[i];

        // Compute MSDBS values from right to left
        for (int i = n - 2; i >= 0; i--)
            for (int j = n - 1; j > i; j--)
                if (arr[i] > arr[j] && MSDBS[i] < MSDBS[j] + arr[i])
                    MSDBS[i] = MSDBS[j] + arr[i];

        // Find the maximum value of MSIBS[i] +
        // MSDBS[i] - arr[i]
        for (int i = 0; i < n; i++)
            max_sum = Math.max(max_sum, (MSDBS[i] + MSIBS[i] - arr[i]));

        // return max sum of bi-tonic
        // sub-sequence
        return max_sum;
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = { 1, 15, 51, 45, 33, 100, 12, 18, 9 };
        int n = arr.length;
        System.out.println("Maximum Sum : " + MaxSumBS(arr, n));
    }
}

// This code is contributed by vt_m
```

## 计算机编程语言

```
# Dynamic Programming implementation of maximum sum of bitonic subsequence

# Function return maximum sum of Bi-tonic sub-sequence
def max_sum(arr, n):

    # MSIBS[i] ==> Maximum sum Increasing Bi-tonic
    # subsequence ending with arr[i]
    # MSDBS[i] ==> Maximum sum Decreasing Bi-tonic
    # subsequence starting with arr[i]

    # allocate memory for MSIBS and initialize it to arr[i] for
    # all indexes
    MSIBS = arr[:]

    # Compute MSIBS values from left to right
    for i in range(n):

        for j in range(0, i):

            if arr[i] > arr[j] and MSIBS[i] < MSIBS[j] + arr[i]:

                MSIBS[i] = MSIBS[j] + arr[i]

    # allocate memory for MSDBS and initialize it to arr[i] for
    # all indexes
    MSDBS = arr[:]

    # Compute MSDBS values from right to left
    for i in range(1, n + 1):

        for j in range(1, i):

            if arr[-i] > arr[-j] and MSDBS[-i] < MSDBS[-j] + arr[-i]:

                MSDBS[-i] = MSDBS[-j] + arr[-i]

    max_sum = float("-Inf")

    # Find the maximum value of MSIBS[i] + MSDBS[i] - arr[i]
    for i, j, k in zip(MSIBS, MSDBS, arr):

        max_sum = max(max_sum, i + j - k)

    # return max sum of bi-tonic sub-sequence
    return max_sum

# Driver program to test the above function
def main():

    arr = [1, 15, 51, 45, 33, 100, 12, 18, 9]

    n = len(arr)

    print max_sum(arr, n)

if __name__ == '__main__':
    main()
# This code is contributed by Neelam Yadav
```

## C#

```
// C# program to find maximum
// sun of bi-tonic sub-sequence
using System;

class GFG {

    // Function return maximum sum
    // of Bi-tonic sub-sequence
    static int MaxSumBS(int[] arr, int n)
    {
        int max_sum = int.MinValue;

        // MSIBS[i] ==> Maximum sum Increasing Bi-tonic
        // subsequence ending with arr[i]
        // MSDBS[i] ==> Maximum sum Decreasing Bi-tonic
        // subsequence starting with arr[i]
        // Initialize MSDBS and MSIBS values as arr[i] for
        // all indexes
        int[] MSIBS = new int[n];
        int[] MSDBS = new int[n];
        for (int i = 0; i < n; i++) {
            MSDBS[i] = arr[i];
            MSIBS[i] = arr[i];
        }

        // Compute MSIBS values from left to right */
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j] && MSIBS[i] < MSIBS[j] + arr[i])
                    MSIBS[i] = MSIBS[j] + arr[i];

        // Compute MSDBS values from right to left
        for (int i = n - 2; i >= 0; i--)
            for (int j = n - 1; j > i; j--)
                if (arr[i] > arr[j] && MSDBS[i] < MSDBS[j] + arr[i])
                    MSDBS[i] = MSDBS[j] + arr[i];

        // Find the maximum value of MSIBS[i] +
        // MSDBS[i] - arr[i]
        for (int i = 0; i < n; i++)
            max_sum = Math.Max(max_sum, (MSDBS[i] + MSIBS[i] - arr[i]));

        // return max sum of bi-tonic
        // sub-sequence
        return max_sum;
    }

    // Driver program
    public static void Main()
    {
        int[] arr = { 1, 15, 51, 45, 33, 100, 12, 18, 9 };
        int n = arr.Length;
        Console.WriteLine("Maximum Sum : " + MaxSumBS(arr, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// sun of bi-tonic sub-sequence
function MaxSumBS($arr, $n)
{
    $max_sum = PHP_INT_MIN;

    // MSIBS[i] ==> Maximum sum Increasing
    // Bi-tonic subsequence ending with arr[i]
    // MSDBS[i] ==> Maximum sum Decreasing
    // Bi-tonic subsequence starting with arr[i]
    // Initialize MSDBS and MSIBS values
    // as arr[i] for all indexes
    $MSIBS = array();
    $MSDBS = array();
    for ($i = 0; $i < $n; $i++)
    {
        $MSDBS[$i] = $arr[$i];
        $MSIBS[$i] = $arr[$i];
    }

    // Compute MSIBS values
    // from left to right */
    for ($i = 1; $i < $n; $i++)
        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] > $arr[$j] &&
                $MSIBS[$i] < $MSIBS[$j] +
                             $arr[$i])
                $MSIBS[$i] = $MSIBS[$j] +
                             $arr[$i];

    // Compute MSDBS values
    // from right to left
    for ($i = $n - 2; $i >= 0; $i--)
        for ($j = $n - 1; $j > $i; $j--)
            if ($arr[$i] > $arr[$j] &&
                $MSDBS[$i] < $MSDBS[$j] +
                             $arr[$i])
                $MSDBS[$i] = $MSDBS[$j] +
                             $arr[$i];

    // Find the maximum value of
    // MSIBS[i] + MSDBS[i] - arr[i]
    for ($i = 0; $i < $n; $i++)
        $max_sum = max($max_sum, ($MSDBS[$i] +
                                  $MSIBS[$i] -
                                  $arr[$i]));

    // return max sum of
    // bi-tonic sub-sequence
    return $max_sum;
}

// Driver Code
$arr = array(1, 15, 51, 45, 33,
             100, 12, 18, 9);
$n = count($arr);
echo "Maximum Sum : " ,
      MaxSumBS($arr, $n);

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find maximum
    // sun of bi-tonic sub-sequence

    // Function return maximum sum
    // of Bi-tonic sub-sequence
    function MaxSumBS(arr, n)
    {
        let max_sum = Number.MIN_VALUE;

        // MSIBS[i] ==> Maximum sum Increasing Bi-tonic
        // subsequence ending with arr[i]
        // MSDBS[i] ==> Maximum sum Decreasing Bi-tonic
        // subsequence starting with arr[i]
        // Initialize MSDBS and MSIBS values as arr[i] for
        // all indexes
        let MSIBS = new Array(n);
        let MSDBS = new Array(n);
        for (let i = 0; i < n; i++) {
            MSDBS[i] = arr[i];
            MSIBS[i] = arr[i];
        }

        // Compute MSIBS values from left to right */
        for (let i = 1; i < n; i++)
            for (let j = 0; j < i; j++)
                if (arr[i] > arr[j] &&
                MSIBS[i] < MSIBS[j] + arr[i])
                    MSIBS[i] = MSIBS[j] + arr[i];

        // Compute MSDBS values from right to left
        for (let i = n - 2; i >= 0; i--)
            for (let j = n - 1; j > i; j--)
                if (arr[i] > arr[j] &&
                MSDBS[i] < MSDBS[j] + arr[i])
                MSDBS[i] = MSDBS[j] + arr[i];

        // Find the maximum value of MSIBS[i] +
        // MSDBS[i] - arr[i]
        for (let i = 0; i < n; i++)
            max_sum =
            Math.max(max_sum, (MSDBS[i] + MSIBS[i] - arr[i]));

        // return max sum of bi-tonic
        // sub-sequence
        return max_sum;
    }

    let arr = [ 1, 15, 51, 45, 33, 100, 12, 18, 9 ];
    let n = arr.length;
    document.write("Maximum Sum : " + MaxSumBS(arr, n));

</script>
```

**输出:**

```
Maximum Sum : 194
```

时间复杂度:O(n <sup>2</sup> )
本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。