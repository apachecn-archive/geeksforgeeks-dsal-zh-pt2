# 最长递增奇偶子序列

> 原文:[https://www . geesforgeks . org/最长递增奇偶子序列/](https://www.geeksforgeeks.org/longest-increasing-odd-even-subsequence/)

给定大小为 **n** 的数组。问题是在给定的数组中找到子序列的长度，使得子序列的所有元素以递增的顺序排序，并且它们交替是奇数和偶数。
注意，子序列可以从奇数或偶数开始。
**示例:**

```
Input : arr[] = {5, 6, 9, 4, 7, 8}
Output : 6
{5, 6, 9,4,7,8} is the required longest
increasing odd even subsequence which is the array itself in this case

Input : arr[] = {1, 12, 2, 22, 5, 30, 31, 14, 17, 11}
{1,12,5,30,31,14,17} is the required longest
increasing odd even subsequence
Output : 7
```

**朴素方法:**考虑所有子序列，选择奇数和偶数交替的子序列，顺序递增。从中选出最长的一个。这具有指数级的时间复杂度。
**有效方法:**
设 L(i)为结束于索引 I 的 LIOES(最长递增奇偶子序列)的长度，使得 arr[i]是 LIOES 的最后一个元素。
然后，L(i)可以递归写成:
L(i) = 1 + max( L(j))，其中 0 < j < i 和(arr[j] < arr[i])和(arr[i]+arr[j])%2！= 0;或者
L(i) = 1，如果不存在这样的 j。
为了找到给定数组的 LIOES，我们需要返回 max(L(i))，其中 0 < i < n.
下面针对上述递归关系实现了一种动态编程方法。

## C++

```
// C++ implementation to find the longest
// increasing odd even subsequence
#include <bits/stdc++.h>

using namespace std;

// function to find the longest
// increasing odd even subsequence
int longOddEvenIncSeq(int arr[], int n)
{
    // lioes[i] stores longest increasing odd
    // even subsequence ending at arr[i]
    int lioes[n];

    // to store the length of longest increasing
    // odd even subsequence
    int maxLen = 0;

    // Initialize LIOES values for all indexes
    for (int i = 0; i < n; i++)
        lioes[i] = 1;

    // Compute optimized LIOES values
    // in bottom up manner
    for (int i = 1; i < n; i++)
        for (int j = 0; j < i; j++)
            if (arr[i] > arr[j] &&
               (arr[i] + arr[j]) % 2 != 0
                && lioes[i] < lioes[j] + 1)
                lioes[i] = lioes[j] + 1;

    // Pick maximum of all LIOES values
    for (int i = 0; i < n; i++)
        if (maxLen < lioes[i])
            maxLen = lioes[i];

    // required maximum length
    return maxLen;
}

// Driver program to test above
int main()
{
    int arr[] = { 1, 12, 2, 22, 5, 30,
                    31, 14, 17, 11 };
    int n = sizeof(arr) / sizeof(n);
    cout << "Longest Increasing Odd Even "
         << "Subsequence: "
         << longOddEvenIncSeq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the longest
// increasing odd even subsequence
import java.util.*;
import java.lang.*;

public class GfG{

    // function to find the longest
    // increasing odd even subsequence
    public static int longOddEvenIncSeq(int arr[],
                                           int n)
    {
        // lioes[i] stores longest increasing odd
        // even subsequence ending at arr[i]
        int[] lioes = new int[n];

        // to store the length of longest
        // increasing odd even subsequence
        int maxLen = 0;

        // Initialize LIOES values for all indexes
        for (int i = 0; i < n; i++)
            lioes[i] = 1;

        // Compute optimized LIOES values
        // in bottom up manner
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j] &&
                (arr[i] + arr[j]) % 2 != 0
                    && lioes[i] < lioes[j] + 1)
                    lioes[i] = lioes[j] + 1;

        // Pick maximum of all LIOES values
        for (int i = 0; i < n; i++)
            if (maxLen < lioes[i])
                maxLen = lioes[i];

        // required maximum length
        return maxLen;
    }
    // driver function
    public static void main(String argc[]){
        int[] arr = new int[]{ 1, 12, 2, 22,
                     5, 30, 31, 14, 17, 11 };
        int n = 10;
        System.out.println("Longest Increasing Odd"
                          + " Even Subsequence: "
                       + longOddEvenIncSeq(arr, n));
    }
}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python3 implementation to find the longest
# increasing odd even subsequence

# function to find the longest
# increasing odd even subsequence
def longOddEvenIncSeq( arr , n ):

    # lioes[i] stores longest increasing odd
    # even subsequence ending at arr[i]
    lioes = list()

    # to store the length of longest increasing
    # odd even subsequence
    maxLen = 0

    # Initialize LIOES values for all indexes
    for i in range(n):
        lioes.append(1)

    # Compute optimized LIOES values
    # in bottom up manner
    i=1
    for i in range(n):
        for j in range(i):
            if (arr[i] > arr[j] and
                (arr[i] + arr[j]) % 2 != 0 and
                lioes[i] < lioes[j] + 1):
                    lioes[i] = lioes[j] + 1

    # Pick maximum of all LIOES values
    for i in range(n):
        if maxLen < lioes[i]:
            maxLen = lioes[i]

    # required maximum length
    return maxLen

# Driver to test above
arr = [ 1, 12, 2, 22, 5, 30, 31, 14, 17, 11 ]
n = len(arr)
print("Longest Increasing Odd Even " +
      "Subsequence: ",longOddEvenIncSeq(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# implementation to find the longest
// increasing odd even subsequence
using System;

class GFG {

    // function to find the longest
    // increasing odd even subsequence
    public static int longOddEvenIncSeq(int[] arr,
                                            int n)
    {
        // lioes[i] stores longest increasing odd
        // even subsequence ending at arr[i]
        int[] lioes = new int[n];

        // to store the length of longest
        // increasing odd even subsequence
        int maxLen = 0;

        // Initialize LIOES values for all indexes
        for (int i = 0; i < n; i++)
            lioes[i] = 1;

        // Compute optimized LIOES values
        // in bottom up manner
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j] &&
                   (arr[i] + arr[j]) % 2 != 0 &&
                    lioes[i] < lioes[j] + 1)

                    lioes[i] = lioes[j] + 1;

        // Pick maximum of all LIOES values
        for (int i = 0; i < n; i++)
            if (maxLen < lioes[i])
                maxLen = lioes[i];

        // required maximum length
        return maxLen;
    }

    // driver function
    public static void Main()
    {
        int[] arr = new int[]{ 1, 12, 2, 22,
                               5, 30, 31, 14, 17, 11 };
        int n = 10;
        Console.Write("Longest Increasing Odd"
                    + " Even Subsequence: "
                    + longOddEvenIncSeq(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the longest
// increasing odd even subsequence

// function to find the longest
// increasing odd even subsequence
function longOddEvenIncSeq(&$arr, $n)
{
    // lioes[i] stores longest increasing
    // odd even subsequence ending at arr[i]
    $lioes= array_fill(0, $n, NULL);

    // to store the length of longest
    // increasing odd even subsequence
    $maxLen = 0;

    // Initialize LIOES values for
    // all indexes
    for ($i = 0; $i < $n; $i++)
        $lioes[$i] = 1;

    // Compute optimized LIOES values
    // in bottom up manner
    for ($i = 1; $i < $n; $i++)
        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] > $arr[$j] &&
            ($arr[$i] + $arr[$j]) % 2 != 0 &&
                $lioes[$i] < $lioes[$j] + 1)
                $lioes[$i] = $lioes[$j] + 1;

    // Pick maximum of all LIOES values
    for ($i = 0; $i < $n; $i++)
        if ($maxLen < $lioes[$i])
            $maxLen = $lioes[$i];

    // required maximum length
    return $maxLen;
}

// Driver Code
$arr = array( 1, 12, 2, 22, 5, 30,
                    31, 14, 17, 11) ;
$n = sizeof($arr);
echo "Longest Increasing Odd Even ".
        "Subsequence: " . longOddEvenIncSeq($arr, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// javascript program to find the longest
// increasing odd even subsequence

    // function to find the longest
    // increasing odd even subsequence
    function longOddEvenIncSeq(arr, n)
    {

        // lioes[i] stores longest increasing odd
        // even subsequence ending at arr[i]
        let lioes = [];

        // to store the length of longest
        // increasing odd even subsequence
        let maxLen = 0;

        // Initialize LIOES values for all indexes
        for (let i = 0; i < n; i++)
            lioes[i] = 1;

        // Compute optimized LIOES values
        // in bottom up manner
        for (let i = 1; i < n; i++)
            for (let j = 0; j < i; j++)
                if (arr[i] > arr[j] &&
                (arr[i] + arr[j]) % 2 != 0
                    && lioes[i] < lioes[j] + 1)
                    lioes[i] = lioes[j] + 1;

        // Pick maximum of all LIOES values
        for (let i = 0; i < n; i++)
            if (maxLen < lioes[i])
                maxLen = lioes[i];

        // required maximum length
        return maxLen;
    }

// Driver code

    let arr = [ 1, 12, 2, 22,
                     5, 30, 31, 14, 17, 11 ];
        let n = 10;
        document.write("Longest Increasing Odd"
                          + " Even Subsequence: "
                       + longOddEvenIncSeq(arr, n));

    // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
Longest Increasing Odd Even Subsequence: 5
```

**时间复杂度:** O(n <sup>2</sup> )。
**辅助空间:** O(n)。