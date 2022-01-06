# 从每个索引开始的最长交替(正和负)子阵列

> 原文:[https://www . geesforgeks . org/最长-交替-正-负-子数组-开始-每-索引/](https://www.geeksforgeeks.org/longest-alternating-positive-negative-subarray-starting-every-index/)

如果子阵列中的任意两个连续数字符号相反(即其中一个应该是负数，而另一个应该是正数)，则称之为交替。
给定一个 n 个整数的数组。对于每个索引 I，我们需要找到从 I 开始的最长交替子阵列的长度
示例:

```
Input : a[] = {1, -5, 1, -5}
Output : For index 0, {1, -5, 1, -5} = 4
             index 1, {-5, 1, -5} = 3
             index 2, {1, -5} = 2
             index 3, {-5} = 1.

Input :a[] = {-5, -1, -1, 2, -2, -3}
Output : index 0 = 1,
         index 1 = 1,
         index 2 = 3,
         index 3 = 2,
         index 4 = 1,
         index 5 = 1,
```

一种**天真的方法**是使用两个循环，其中我们从每个索引 i (0 到 n-1)开始遍历整个阵列，并计算交替子阵列的长度。
时间复杂度:O(n <sup>2</sup> )。
**高效进场:**
观察当*a【I】*和*a【I+1】*符号相反时，*计数【I】*将比*计数【I+1】*多 1。否则当它们有相同的符号时*计数【I】*将为 1。
这里我们使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。

## C++

```
// CPP program to find longest alternating
// subarray starting from every index.
#include <bits/stdc++.h>
using namespace std;

void longestAlternating(int arr[], int n)
{
    int count[n];

    // Fill count[] from end.
    count[n - 1] = 1;
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] * arr[i + 1] < 0)
            count[i] = count[i + 1] + 1;
        else
            count[i] = 1;
    }

    // Print result
    for (int i = 0; i < n; i++)
        cout << count[i] << " ";
}

// Driver code
int main()
{
    int a[] = { -5, -1, -1, 2, -2, -3 };
    int n = sizeof(a) / sizeof(a[0]);
    longestAlternating(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest alternating
// subarray starting from every index.
import java.util.*;

class Longest{

    public static void longestAlternating(int arr[],
                                             int n)
    {
        int[] count = new int[n];

        // Fill count[] from end.
        count[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--) {
            if (arr[i] * arr[i + 1] < 0)
                count[i] = count[i + 1] + 1;
            else
                count[i] = 1;
        }

        // Print result
        for (int i = 0; i < n; i++)
            System.out.print(count[i] + " ");
    }

    // driver program
    public static void main(String[] args)
    {
        int a[] = { -5, -1, -1, 2, -2, -3 };
        int n = 6;
        longestAlternating(a, n);
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program to find longest alternating
# subarray starting from every index.

def longestAlternating(arr, n) :
    count = [None] * n

    # Fill count[] from end.
    count[n - 1] = 1
    i = n - 2

    while i >= 0 :
        if (arr[i] * arr[i + 1] < 0) :
            count[i] = count[i + 1] + 1
        else :
            count[i] = 1;
        i = i - 1

    i = 0

    # Print result
    while i < n :
        print (count[i], end = " ")
        i = i + 1

# Driver Code
a = [ -5, -1, -1, 2, -2, -3 ]
n = len(a)
longestAlternating(a, n);

# This code is contributed by rishabh_jain
```

## C#

```
//C# program to find longest alternating
// subarray starting from every index.
using System;

class Longest
{

    public static void longestAlternating(int []arr,
                                            int n)
    {
        int[] count = new int[n];

        // Fill count[] from end.
        count[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--)
        {
            if (arr[i] * arr[i + 1] < 0)
                count[i] = count[i + 1] + 1;
            else
                count[i] = 1;
        }

        // Print result
        for (int i = 0; i < n; i++)
            Console.Write(count[i] + " ");
    }

    // Driver program
    public static void Main()
    {
        int []a = { -5, -1, -1, 2, -2, -3 };
        int n = 6;
        longestAlternating(a, n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find longest alternating
// subarray starting from every index.

function longestAlternating( $arr, $n)
{
    $count = array();

    // Fill count[] from end.
    $count[$n - 1] = 1;
    for ( $i = $n - 2; $i >= 0; $i--)
    {
        if ($arr[$i] * $arr[$i + 1] < 0)
            $count[$i] = $count[$i + 1] + 1;
        else
            $count[$i] = 1;
    }

    // Print result
    for ( $i = 0; $i < $n; $i++)
        echo $count[$i] , " ";
}

    // Driver code
    $a = array( -5, -1, -1, 2, -2, -3 );
    $n =count($a);
    longestAlternating($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find longest alternating
// subarray starting from every index.
function longestAlternating(arr, n)
{
    let count = new Array(n);

    // Fill count[] from end.
    count[n - 1] = 1;
    for (let i = n - 2; i >= 0; i--) {
        if (arr[i] * arr[i + 1] < 0)
            count[i] = count[i + 1] + 1;
        else
            count[i] = 1;
    }

    // Prlet result
    for (let i = 0; i < n; i++)
        document.write(count[i] + " ");
}

// Driver code
    let a = [ -5, -1, -1, 2, -2, -3 ];
    let n = a.length;
    longestAlternating(a, n);

// This code is contributed by Surbhi Tyagi.
</script>
```

输出:

```
1 1 3 2 1 1
```