# 最长公共递增子序列(LCS + LIS)

> 原文:[https://www . geesforgeks . org/最长-公共-递增-子序列-lcs-lis/](https://www.geeksforgeeks.org/longest-common-increasing-subsequence-lcs-lis/)

先决条件: [LCS](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/) 、 [LIS](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)
给定两个数组，找到最长的公共递增子序列的长度【LCIS】并打印其中一个序列(可能存在多个序列)
假设我们考虑两个数组–
arr 1[]= {3，4，9，1}和
arr2[] = {5，3，8，9，10，2，1}
我们的答案将是{ 3，9}，因为这是最长的公共递增子序列。

想法是在这里也使用动态编程。我们存储在 arr2[]的每个索引处结束的最长公共递增子序列。我们创建了一个辅助数组表[]使得表[j]存储以 arr2[j]结尾的 LCIS 长度。最后，我们从这个表中返回最大值。为了填充该表中的值，我们遍历 arr1[]的所有元素，对于 arr1[i]的每个元素，我们遍历 arr2[]的所有元素。如果找到匹配，我们用当前 LCIS 的长度更新表[j]。为了保持当前的 LCIS，我们继续检查有效的表[j]值。
下面是寻找 LCIS 长度的程序。

## C++

```
// A C++ Program to find length of the Longest Common
// Increasing Subsequence (LCIS)
#include<bits/stdc++.h>
using namespace std;

// Returns the length and the LCIS of two
// arrays arr1[0..n-1] and arr2[0..m-1]
int LCIS(int arr1[], int n, int arr2[], int m)
{
    // table[j] is going to store length of LCIS
    // ending with arr2[j]. We initialize it as 0,
    int table[m];
    for (int j=0; j<m; j++)
        table[j] = 0;

    // Traverse all elements of arr1[]
    for (int i=0; i<n; i++)
    {
        // Initialize current length of LCIS
        int current = 0;

        // For each element of arr1[], traverse all
        // elements of arr2[].
        for (int j=0; j<m; j++)
        {
            // If both the array have same elements.
            // Note that we don't break the loop here.
            if (arr1[i] == arr2[j])
                if (current + 1 > table[j])
                    table[j] = current + 1;

            /* Now seek for previous smaller common
               element for current element of arr1 */
            if (arr1[i] > arr2[j])
                if (table[j] > current)
                    current = table[j];
        }
    }

    // The maximum value in table[] is out result
    int result = 0;
    for (int i=0; i<m; i++)
        if (table[i] > result)
           result = table[i];

    return result;
}

/* Driver program to test above function */
int main()
{
    int arr1[] = {3, 4, 9, 1};
    int arr2[] = {5, 3, 8, 9, 10, 2, 1};

    int n = sizeof(arr1)/sizeof(arr1[0]);
    int m = sizeof(arr2)/sizeof(arr2[0]);

    cout << "Length of LCIS is "
         << LCIS(arr1, n, arr2, m);
    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java Program to find length of the Longest
// Common Increasing Subsequence (LCIS)
import java.io.*;

class GFG {

    // Returns the length and the LCIS of two
    // arrays arr1[0..n-1] and arr2[0..m-1]
    static int LCIS(int arr1[], int n, int arr2[],
                                         int m)
    {
        // table[j] is going to store length of 
        // LCIS ending with arr2[j]. We initialize
        // it as 0,
        int table[] = new int[m];
        for (int j = 0; j < m; j++)
            table[j] = 0;

        // Traverse all elements of arr1[]
        for (int i = 0; i < n; i++)
        {
            // Initialize current length of LCIS
            int current = 0;

            // For each element of arr1[], traverse 
            // all elements of arr2[].
            for (int j = 0; j < m; j++)
            {
                // If both the array have same 
                // elements. Note that we don't
                // break the loop here.
                if (arr1[i] == arr2[j])
                    if (current + 1 > table[j])
                        table[j] = current + 1;

                /* Now seek for previous smaller
                common element for current 
                element of arr1 */
                if (arr1[i] > arr2[j])
                    if (table[j] > current)
                        current = table[j];
            }
        }

        // The maximum value in table[] is out
        // result
        int result = 0;
        for (int i=0; i<m; i++)
            if (table[i] > result)
            result = table[i];

        return result;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr1[] = {3, 4, 9, 1};
        int arr2[] = {5, 3, 8, 9, 10, 2, 1};

        int n = arr1.length;
        int m = arr2.length;

    System.out.println("Length of LCIS is " +
                       LCIS(arr1, n, arr2, m));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 Program to find length of the 
# Longest Common Increasing Subsequence (LCIS)

# Returns the length and the LCIS of two
# arrays arr1[0..n-1] and arr2[0..m-1]
def LCIS(arr1, n, arr2, m):

    # table[j] is going to store length of LCIS
    # ending with arr2[j]. We initialize it as 0,
    table = [0] * m
    for j in range(m):
        table[j] = 0

    # Traverse all elements of arr1[]
    for i in range(n):

        # Initialize current length of LCIS
        current = 0

        # For each element of arr1[], 
        # traverse all elements of arr2[].
        for j in range(m):

            # If both the array have same elements.
            # Note that we don't break the loop here.
            if (arr1[i] == arr2[j]):
                if (current + 1 > table[j]):
                    table[j] = current + 1

            # Now seek for previous smaller common
            # element for current element of arr1 
            if (arr1[i] > arr2[j]):
                if (table[j] > current):
                    current = table[j]

    # The maximum value in table[] 
    # is out result
    result = 0
    for i in range(m):
        if (table[i] > result):
            result = table[i]

    return result

# Driver Code
if __name__ == "__main__":

    arr1 = [3, 4, 9, 1]
    arr2 = [5, 3, 8, 9, 10, 2, 1]

    n = len(arr1)
    m = len(arr2)

    print("Length of LCIS is", 
           LCIS(arr1, n, arr2, m))

# This code is contributed by ita_c
```

## C#

```
// A C# Program to find length of the Longest
// Common Increasing Subsequence (LCIS)
using System;

class GFG {

    // Returns the length and the LCIS of two
    // arrays arr1[0..n-1] and arr2[0..m-1]
    static int LCIS(int []arr1, int n,
                    int []arr2, int m)
    {
        // table[j] is going to store length of 
        // LCIS ending with arr2[j]. We initialize
        // it as 0,
        int []table = new int[m];
        for (int j = 0; j < m; j++)
            table[j] = 0;

        // Traverse all elements of arr1[]
        for (int i = 0; i < n; i++)
        {
            // Initialize current length of LCIS
            int current = 0;

            // For each element of arr1[], traverse 
            // all elements of arr2[].
            for (int j = 0; j < m; j++)
            {
                // If both the array have same 
                // elements. Note that we don't
                // break the loop here.
                if (arr1[i] == arr2[j])
                    if (current + 1 > table[j])
                        table[j] = current + 1;

                /* Now seek for previous smaller
                   common element for current 
                   element of arr1 */
                if (arr1[i] > arr2[j])
                    if (table[j] > current)
                        current = table[j];
            }
        }

        // The maximum value in 
        // table[] is out result
        int result = 0;
        for (int i = 0; i < m; i++)
            if (table[i] > result)
            result = table[i];

        return result;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int []arr1 = {3, 4, 9, 1};
        int []arr2 = {5, 3, 8, 9, 10, 2, 1};

        int n = arr1.Length;
        int m = arr2.Length;

    Console.Write("Length of LCIS is " +
                   LCIS(arr1, n, arr2, m));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find length of
// the Longest Common Increasing 
// Subsequence (LCIS)

// Returns the length and the LCIS 
// of two arrays arr1[0..n-1] and 
// arr2[0..m-1]
function LCIS($arr1, $n, $arr2, $m)
{
    // table[j] is going to store 
    // length of LCIS ending with 
    // arr2[j]. We initialize it as 0,

    $table = Array();

    //int table[m];
    for ($j = 0; $j < $m; $j++)
        $table[$j] = 0;

    // Traverse all elements of arr1[]
    for ($i = 0; $i < $n; $i++)
    {
        // Initialize current
        // length of LCIS
        $current = 0;

        // For each element of 
        // arr1[], traverse all
        // elements of arr2[].
        for ($j = 0; $j < $m; $j++)
        {
            // If both the array have 
            // same elements. Note that
            // we don't break the loop here.
            if ($arr1[$i] == $arr2[$j])
                if ($current + 1 > $table[$j])
                    $table[$j] = $current + 1;

            /* Now seek for previous smaller 
            common element for current 
            element of arr1 */
            if ($arr1[$i] > $arr2[$j])
                if ($table[$j] > $current)
                    $current = $table[$j];
        }
    }

    // The maximum value in 
    // table[] is out result
    $result = 0;
    for ($i = 0; $i < $m; $i++)
        if ($table[$i] > $result)
        $result = $table[$i];

    return $result;
}

// Driver Code
$arr1 = array (3, 4, 9, 1);
$arr2 = array (5, 3, 8, 9, 10, 2, 1);

$n = sizeof($arr1);
$m = sizeof($arr2);

echo "Length of LCIS is ",
       LCIS($arr1, $n, $arr2, $m);

// This code is contributed by ajit 
?>
```

## java 描述语言

```
<script>

// Javascript Program to find length of the Longest
// Common Increasing Subsequence (LCIS)

    // Returns the length and the LCIS of two
    // arrays arr1[0..n-1] and arr2[0..m-1]
    function LCIS(arr1, n, arr2, m)
    {
        // table[j] is going to store length of 
        // LCIS ending with arr2[j]. We initialize
        // it as 0,
        let table = [];
        for (let j = 0; j < m; j++)
            table[j] = 0;

        // Traverse all elements of arr1[]
        for (let i = 0; i < n; i++)
        {
            // Initialize current length of LCIS
            let current = 0;

            // For each element of arr1[], traverse 
            // all elements of arr2[].
            for (let j = 0; j < m; j++)
            {
                // If both the array have same 
                // elements. Note that we don't
                // break the loop here.
                if (arr1[i] == arr2[j])
                    if (current + 1 > table[j])
                        table[j] = current + 1;

                /* Now seek for previous smaller
                common element for current 
                element of arr1 */
                if (arr1[i] > arr2[j])
                    if (table[j] > current)
                        current = table[j];
            }
        }

        // The maximum value in table[] is out
        // result
        let result = 0;
        for (let i=0; i<m; i++)
            if (table[i] > result)
            result = table[i];

        return result;
    }

// Driver Code

        let arr1 = [3, 4, 9, 1];
        let arr2 = [5, 3, 8, 9, 10, 2, 1];

        let n = arr1.length;
        let m = arr2.length;

    document.write("Length of LCIS is " +
                       LCIS(arr1, n, arr2, m));

</script>
```

**输出:**

```
Length of LCIS is 2
```

本文由**Rachit Belvariar**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息