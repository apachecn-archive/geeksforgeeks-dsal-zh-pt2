# 最大和递减子序列

> 原文:[https://www . geesforgeks . org/maximum-sum-reducing-subsequence/](https://www.geeksforgeeks.org/maximum-sum-decreasing-subsequence/)

给定一个 N 个正整数的数组。任务是找到给定数组的最大和递减子序列(MSDS)的和，使得子序列中的整数按递减顺序排序。
**例**:

> **输入:** arr[] = {5，4，100，3，2，101，1}
> **输出:** 106
> 100 + 3 + 2 + 1 = 106
> **输入:** arr[] = {10，5，4，3}
> **输出:** 22
> 10 + 5 + 4 + 3 = 22

这个问题是[最长递减子序列](https://www.geeksforgeeks.org/longest-decreasing-subsequence/)问题的变种。上述问题的**最优子结构**将是:
让 arr[0..n-1]是输入数组， *MSDS[i]是以索引 i* 结束的 MSDS 的最大和，使得 arr[i]是 MSDS 的最后一个元素。
那么，MSDS[我]可以写成:

> MSDS[i] = a[i] + max( MSDS[j])，其中 i > j > 0 且 arr[j] > arr[i]或，
> MSDS[i] = a[i]，如果不存在这样的 j。

为了找到给定数组的 MSDS，我们需要返回 max(MSDS[i])，其中 n > i > 0。
以下是上述方法的实现:

## C++

```
// CPP code to return the maximum sum
// of decreasing subsequence in arr[]
#include <bits/stdc++.h>
using namespace std;

// function to return the maximum
// sum of decreasing subsequence
// in arr[]
int maxSumDS(int arr[], int n)
{
    int i, j, max = 0;
    int MSDS[n];

    // Initialize msds values
    // for all indexes
    for (i = 0; i < n; i++)
        MSDS[i] = arr[i];

    // Compute maximum sum values
    // in bottom up manner
    for (i = 1; i < n; i++)
        for (j = 0; j < i; j++)
            if (arr[i] < arr[j] && MSDS[i] < MSDS[j] + arr[i])
                MSDS[i] = MSDS[j] + arr[i];

    // Pick maximum of all msds values
    for (i = 0; i < n; i++)
        if (max < MSDS[i])
            max = MSDS[i];

    return max;
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 100, 3, 2, 101, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Sum of maximum sum decreasing subsequence is: "
         << maxSumDS(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to return the maximum sum
// of decreasing subsequence in arr[]
import java.io.*;
import java.lang.*;

class GfG {

    // function to return the maximum
    // sum of decreasing subsequence
    // in arr[]
    public static int maxSumDS(int arr[], int n)
    {
        int i, j, max = 0;
        int[] MSDS = new int[n];

        // Initialize msds values
        // for all indexes
        for (i = 0; i < n; i++)
            MSDS[i] = arr[i];

        // Compute maximum sum values
        // in bottom up manner
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] < arr[j] &&
                    MSDS[i] < MSDS[j] + arr[i])
                    MSDS[i] = MSDS[j] + arr[i];

        // Pick maximum of all msds values
        for (i = 0; i < n; i++)
            if (max < MSDS[i])
                max = MSDS[i];

        return max;
    }

    // Driver Code
    public static void main(String argc[])
    {
        int arr[] = { 5, 4, 100, 3, 2, 101, 1 };

        int n = 7;

        System.out.println("Sum of maximum sum"
               + " decreasing subsequence is: "
                           + maxSumDS(arr, n));
    }
}

// This code os contributed by Sagar Shukla.
```

## 蟒蛇 3

```
# Python3 code to return the maximum sum
# of decreasing subsequence in arr[]

# Function to return the maximum
# sum of decreasing subsequence
# in arr[]
def maxSumDS(arr, n):

    i, j, max = (0, 0, 0)

    MSDS=[0 for i in range(n)]

    # Initialize msds values
    # for all indexes
    for i in range(n):
        MSDS[i] = arr[i]

    # Compute maximum sum values
    # in bottom up manner
    for i in range(1, n):
        for j in range(i):
            if (arr[i] < arr[j] and
                MSDS[i] < MSDS[j] + arr[i]):
                MSDS[i] = MSDS[j] + arr[i]

    # Pick maximum of all msds values
    for i in range(n):
        if (max < MSDS[i]):
            max = MSDS[i]

    return max

if __name__ == "__main__":

    arr=[5, 4, 100, 3,
         2, 101, 1]
    n=len(arr)
    print("Sum of maximum sum decreasing subsequence is: ",
           maxSumDS(arr, n))

# This code is contributed by Rutvik_56
```

## C#

```
// C# code to return the
// maximum sum of decreasing
// subsequence in arr[]
using System;

class GFG
{

    // function to return the
    // maximum sum of decreasing
    // subsequence in arr[]
    public static int maxSumDS(int []arr,
                               int n)
    {
        int i, j, max = 0;
        int[] MSDS = new int[n];

        // Initialize msds values
        // for all indexes
        for (i = 0; i < n; i++)
            MSDS[i] = arr[i];

        // Compute maximum sum values
        // in bottom up manner
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] < arr[j] &&
                    MSDS[i] < MSDS[j] + arr[i])
                    MSDS[i] = MSDS[j] + arr[i];

        // Pick maximum of
        // all msds values
        for (i = 0; i < n; i++)
            if (max < MSDS[i])
                max = MSDS[i];

        return max;
    }

    // Driver Code
    static public void Main ()
    {
        int []arr = {5, 4, 100,
                     3, 2, 101, 1};
        int n = 7;
        Console.WriteLine("Sum of maximum sum" +
                " decreasing subsequence is: " +
                              maxSumDS(arr, n));
    }
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to return the maximum sum
// of decreasing subsequence in arr[]

// function to return the maximum
// sum of decreasing subsequence
// in arr[]
function maxSumDS($arr, $n)
{
    $i; $j; $max = 0;
    $MSDS = array();

    // Initialize msds values
    // for all indexes
    for ($i = 0; $i < $n; $i++)
        $MSDS[$i] = $arr[$i];

    // Compute maximum sum values
    // in bottom up manner
    for ($i = 1; $i < $n; $i++)
        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] < $arr[$j] &&
                   $MSDS[$i] < $MSDS[$j] + $arr[$i])
                $MSDS[$i] = $MSDS[$j] + $arr[$i];

    // Pick maximum of
    // all msds values
    for ($i = 0; $i < $n; $i++)
        if ($max < $MSDS[$i])
            $max = $MSDS[$i];

    return $max;
}

// Driver Code
$arr = array (5, 4, 100,
              3, 2, 101, 1 );

$n = sizeof($arr);

echo "Sum of maximum sum decreasing " .
                    "subsequence is: ",
                    maxSumDS($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript code to return the
    // maximum sum of decreasing
    // subsequence in arr[]

    // function to return the
    // maximum sum of decreasing
    // subsequence in arr[]
    function maxSumDS(arr, n)
    {
        let i, j, max = 0;
        let MSDS = new Array(n);

        // Initialize msds values
        // for all indexes
        for (i = 0; i < n; i++)
            MSDS[i] = arr[i];

        // Compute maximum sum values
        // in bottom up manner
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] < arr[j] &&
                    MSDS[i] < MSDS[j] + arr[i])
                    MSDS[i] = MSDS[j] + arr[i];

        // Pick maximum of
        // all msds values
        for (i = 0; i < n; i++)
            if (max < MSDS[i])
                max = MSDS[i];

        return max;
    }

    let arr = [5, 4, 100, 3, 2, 101, 1];
    let n = 7;
    document.write("Sum of maximum sum" +
                      " decreasing subsequence is: " +
                      maxSumDS(arr, n));

// This code is contributed by suresh07.
</script>
```

**输出** :

```
Sum of maximum sum decreasing subsequence is: 106
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)