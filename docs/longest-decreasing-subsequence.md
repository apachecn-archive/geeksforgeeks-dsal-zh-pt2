# 最长递减子序列

> 原文:[https://www . geesforgeks . org/最长递减子序列/](https://www.geeksforgeeks.org/longest-decreasing-subsequence/)

给定一个 N 个整数的数组，求给定序列中最长子序列的长度，使得子序列的所有元素都以严格递减的顺序排序。

**示例:**

> **输入:**arr[]=【15，27，14，38，63，55，46，65，85】
> **输出:** 3
> **解释:**最长递减子序列为{63，55，46}
> **输入:** arr[] = {50，3，10，7，40，80}
> **输出:** 3 【T14

这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)
**最优子结构:**
让 arr[0…n-1]为输入数组，lds[i]为以索引 I 结束的 lds 的长度，这样 arr[i]就是 LDS 的最后一个元素。
然后，lds[i]可以递归地写成:

> lds[i] = 1 + max(lds[j])，其中 i > j > 0 且 arr[j] > arr[i]或
> lds[i] = 1，如果不存在这样的 j。

为了找到给定数组的 LDS，我们需要返回 **max(lds[i])** ，其中 n > i > 0。

## C++

```
// CPP program to find the length of the
// longest decreasing subsequence
#include <bits/stdc++.h>
using namespace std;

// Function that returns the length
// of the longest decreasing subsequence
int lds(int arr[], int n)
{
    int lds[n];
    int i, j, max = 0;

    // Initialize LDS with 1 for all index
    // The minimum LDS starting with any
    // element is always 1
    for (i = 0; i < n; i++)
        lds[i] = 1;

    // Compute LDS from every index
    // in bottom up manner
    for (i = 1; i < n; i++)
        for (j = 0; j < i; j++)
            if (arr[i] < arr[j] && lds[i] < lds[j] + 1)
                lds[i] = lds[j] + 1;

    // Select the maximum
    // of all the LDS values
    for (i = 0; i < n; i++)
        if (max < lds[i])
            max = lds[i];

    // returns the length of the LDS
    return max;
}
// Driver Code
int main()
{
    int arr[] = { 15, 27, 14, 38, 63, 55, 46, 65, 85 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Length of LDS is " << lds(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// length of the longest
// decreasing subsequence
import java.io.*;

class GFG
{

// Function that returns the
// length of the longest
// decreasing subsequence
static int lds(int arr[], int n)
{
    int lds[] = new int[n];
    int i, j, max = 0;

    // Initialize LDS with 1
    // for all index. The minimum
    // LDS starting with any
    // element is always 1
    for (i = 0; i < n; i++)
        lds[i] = 1;

    // Compute LDS from every
    // index in bottom up manner
    for (i = 1; i < n; i++)
        for (j = 0; j < i; j++)
            if (arr[i] < arr[j] &&
                         lds[i] < lds[j] + 1)
                lds[i] = lds[j] + 1;

    // Select the maximum
    // of all the LDS values
    for (i = 0; i < n; i++)
        if (max < lds[i])
            max = lds[i];

    // returns the length
    // of the LDS
    return max;
}
// Driver Code
public static void main (String[] args)
{
    int arr[] = { 15, 27, 14, 38,
                  63, 55, 46, 65, 85 };
    int n = arr.length;
    System.out.print("Length of LDS is " +
                             lds(arr, n));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find the length of
# the longest decreasing subsequence

# Function that returns the length
# of the longest decreasing subsequence
def lds(arr, n):

    lds = [0] * n
    max = 0

    # Initialize LDS with 1 for all index
    # The minimum LDS starting with any
    # element is always 1
    for i in range(n):
        lds[i] = 1

    # Compute LDS from every index
    # in bottom up manner
    for i in range(1, n):
        for j in range(i):
            if (arr[i] < arr[j] and
                lds[i] < lds[j] + 1):
                lds[i] = lds[j] + 1

    # Select the maximum
    # of all the LDS values
    for i in range(n):
        if (max < lds[i]):
            max = lds[i]

    # returns the length of the LDS
    return max

# Driver Code
if __name__ == "__main__":

    arr = [ 15, 27, 14, 38,
            63, 55, 46, 65, 85 ]
    n = len(arr)
    print("Length of LDS is", lds(arr, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the
// length of the longest
// decreasing subsequence
using System;

class GFG
{

// Function that returns the
// length of the longest
// decreasing subsequence
static int lds(int []arr, int n)
{
    int []lds = new int[n];
    int i, j, max = 0;

    // Initialize LDS with 1
    // for all index. The minimum
    // LDS starting with any
    // element is always 1
    for (i = 0; i < n; i++)
        lds[i] = 1;

    // Compute LDS from every
    // index in bottom up manner
    for (i = 1; i < n; i++)
        for (j = 0; j < i; j++)
            if (arr[i] < arr[j] &&
                        lds[i] < lds[j] + 1)
                lds[i] = lds[j] + 1;

    // Select the maximum
    // of all the LDS values
    for (i = 0; i < n; i++)
        if (max < lds[i])
            max = lds[i];

    // returns the length
    // of the LDS
    return max;
}
// Driver Code
public static void Main ()
{
    int []arr = { 15, 27, 14, 38,
                63, 55, 46, 65, 85 };
    int n = arr.Length;
    Console.Write("Length of LDS is " +
                          lds(arr, n));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// length of the longest
// decreasing subsequence

// Function that returns the
// length of the longest
// decreasing subsequence
function lds($arr, $n)
{
    $lds = array();
    $i; $j; $max = 0;

    // Initialize LDS with 1
    // for all index The minimum
    // LDS starting with any
    // element is always 1
    for ($i = 0; $i < $n; $i++)
        $lds[$i] = 1;

    // Compute LDS from every
    // index in bottom up manner
    for ($i = 1; $i < $n; $i++)
        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] < $arr[$j] and
                $lds[$i] < $lds[$j] + 1)
                {
                    $lds[$i] = $lds[$j] + 1;
                }

    // Select the maximum
    // of all the LDS values
    for ($i = 0; $i < $n; $i++)
        if ($max < $lds[$i])
            $max = $lds[$i];

    // returns the length
    // of the LDS
    return $max;
}

// Driver Code
$arr = array(15, 27, 14, 38, 63,
             55, 46, 65, 85);
$n = count($arr);
echo "Length of LDS is " ,
            lds($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find the
// length of the longest
// decreasing subsequence

    // Function that returns the
// length of the longest
// decreasing subsequence
    function lds(arr,n)
    {
        let lds = new Array(n);
    let i, j, max = 0;

    // Initialize LDS with 1
    // for all index. The minimum
    // LDS starting with any
    // element is always 1
    for (i = 0; i < n; i++)
        lds[i] = 1;

    // Compute LDS from every
    // index in bottom up manner
    for (i = 1; i < n; i++)
        for (j = 0; j < i; j++)
            if (arr[i] < arr[j] &&
                         lds[i] < lds[j] + 1)
                lds[i] = lds[j] + 1;

    // Select the maximum
    // of all the LDS values
    for (i = 0; i < n; i++)
        if (max < lds[i])
            max = lds[i];

    // returns the length
    // of the LDS
    return max;
    }

    // Driver Code
    let arr=[15, 27, 14, 38,
                  63, 55, 46, 65, 85 ];

    let n = arr.length;
    document.write("Length of LDS is " +
                             lds(arr, n));

    // This code is contributed by rag2127
</script>
```

**Output :** 

```
Length of LDS is 3
```

**时间复杂度**:O(n)<sup>2</sup>)
**辅助空间** : O(n)
**相关文章**:[https://www . geekesforgeks . org/最长递增子序列/](https://www.geeksforgeeks.org/longest-increasing-subsequence/)