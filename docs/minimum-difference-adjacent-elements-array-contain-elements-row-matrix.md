# 包含矩阵每行元素的数组相邻元素之间的最小差异

> 原文:[https://www . geesforgeks . org/最小差-相邻元素-数组-包含元素-行-矩阵/](https://www.geeksforgeeks.org/minimum-difference-adjacent-elements-array-contain-elements-row-matrix/)

给定一个由 **N** 行和 **M** 列组成的矩阵，任务是找到大小为 **N** 的数组中任意两个相邻元素之间的最小绝对差，这是通过从矩阵的每一行中选取一个元素来创建的。请注意，从第 1 行选取的元素将变成 arr[0]，从第 2 行选取的元素将变成 arr[1]等等。

**示例:**

```
Input :  N = 2, M = 2
m[2][2] = { 8, 2,
            6, 8 }
Output : 0.
Picking 8 from row 1 and picking 8 from row 2, we create an array { 8, 8 } and minimum
difference between any of adjacent element is 0.

Input :  N = 3, M = 3
m[3][3] = { 1, 2, 3
            4, 5, 6 
            7, 8, 9 }
Output : 1.
```

其思想是对所有行单独排序，然后进行二分搜索法运算，为每个元素找到下一行中最接近的元素。
要以高效的方式做到这一点，请对矩阵的每一行进行排序。从矩阵的第 1 行到第 N–1 行，对于矩阵中当前行的每个元素 m[i][j]，找到下一行中大于或等于当前元素的最小元素，比如 p，以及小于当前元素的最大元素，比如 q。这可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来完成。最后，从 p 和 q 中找出当前元素差值的最小值，并更新变量。

下面是这种方法的实现:

## C++

```
// C++ program to find the minimum absolute difference
// between any of the adjacent elements of an array
// which is created by picking one element from each
// row of the matrix.
#include<bits/stdc++.h>
using namespace std;
#define R 2
#define C 2

// Return smallest element greater than or equal
// to the current element.
int bsearch(int low, int high, int n, int arr[])
{
    int mid = (low + high)/2;

    if(low <= high)
    {
        if(arr[mid] < n)
            return bsearch(mid +1, high, n, arr);
        return bsearch(low, mid - 1, n, arr);
    }

    return low;
}

// Return the minimum absolute difference adjacent
// elements of array
int mindiff(int arr[R][C], int n, int m)
{
    // Sort each row of the matrix.
    for (int i = 0; i < n; i++)
        sort(arr[i], arr[i] + m);

    int ans = INT_MAX;

    // For each matrix element
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < m; j++)
        {
            // Search smallest element in the next row which
            // is greater than or equal to the current element
            int p = bsearch(0, m-1, arr[i][j], arr[i + 1]);
            ans = min(ans, abs(arr[i + 1][p] - arr[i][j]));

            // largest element which is smaller than the current
            // element in the next row must be just before
            // smallest element which is greater than or equal
            // to the current element because rows are sorted.
            if (p-1 >= 0)
                ans = min(ans, abs(arr[i + 1][p - 1] - arr[i][j]));
        }
    }
    return ans;
}

// Driven Program
int main()
{
    int m[R][C] =
    {
        8, 5,
        6, 8,
    };

    cout << mindiff(m, R, C) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// absolute difference between any
// of the adjacent elements of an
// array which is created by picking
// one element from each row of the matrix
import java.util.Arrays;
class GFG
{
static final int R=2;
static final int C=2;

// Return smallest element greater than
// or equal to the current element.
static int bsearch(int low, int high, int n, int arr[])
{
    int mid = (low + high)/2;

    if(low <= high)
    {
        if(arr[mid] < n)
            return bsearch(mid +1, high, n, arr);
        return bsearch(low, mid - 1, n, arr);
    }

    return low;
}

// Return the minimum absolute difference adjacent
// elements of array
static int mindiff(int arr[][], int n, int m)
{

    // Sort each row of the matrix.
    for (int i = 0; i < n; i++)
        Arrays.sort(arr[i]);

    int ans = +2147483647;

    // For each matrix element
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < m; j++)
        {

        // Search smallest element in the
        // next row which is greater than
        // or equal to the current element
        int p = bsearch(0, m-1, arr[i][j], arr[i + 1]);
        ans = Math.min(ans, Math.abs(arr[i + 1][p] - arr[i][j]));

        // largest element which is smaller than the current
        // element in the next row must be just before
        // smallest element which is greater than or equal
        // to the current element because rows are sorted.
        if (p-1 >= 0)
            ans = Math.min(ans,
                        Math.abs(arr[i + 1][p - 1] - arr[i][j]));
        }
    }
    return ans;
}

    //Driver code
public static void main (String[] args)
{
    int m[][] ={{8, 5},
                {6, 8}};

    System.out.println(mindiff(m, R, C));
}
}
//This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to find the minimum absolute difference
# between any of the adjacent elements of an array
# which is created by picking one element from each
# row of the matrix.
# R 2
# C 2

# Return smallest element greater than or equal
# to the current element.
def bsearch(low, high, n, arr):
    mid = (low + high)/2

    if(low <= high):
        if(arr[mid] < n):
            return bsearch(mid +1, high, n, arr);
        return bsearch(low, mid - 1, n, arr);

    return low;

# Return the minimum absolute difference adjacent
# elements of array
def mindiff(arr, n, m):

    # arr = [0 for i in range(R)][for j in range(C)]
    # Sort each row of the matrix.
    for i in range(n):
        sorted(arr)

    ans = 2147483647

    # For each matrix element
    for i in range(n-1):
        for j in range(m):
            # Search smallest element in the next row which
            # is greater than or equal to the current element
            p = bsearch(0, m-1, arr[i][j], arr[i + 1])
            ans = min(ans, abs(arr[i + 1][p] - arr[i][j]))

            # largest element which is smaller than the current
            # element in the next row must be just before
            # smallest element which is greater than or equal
            # to the current element because rows are sorted.
            if (p-1 >= 0):
                ans = min(ans, abs(arr[i + 1][p - 1] - arr[i][j]))
    return ans;

# Driver Program
m =[8, 5], [6, 8]
print mindiff(m, 2, 2)

# This code is contributed by Afzal
```

## C#

```
// C# program to find the minimum
// absolute difference between any
// of the adjacent elements of an
// array which is created by picking
// one element from each row of the matrix
using System;

class GFG
{

static public int R=2;
static public int C=2;

// Return smallest element greater than
// or equal to the current element.
static int bsearch(int low, int high, int n, int []arr)
{
    int mid = (low + high)/2;

    if(low <= high)
    {
        if(arr[mid] < n)
            return bsearch(mid +1, high, n, arr);
        return bsearch(low, mid - 1, n, arr);
    }

    return low;
}
public static int[] GetRow(int[,] matrix, int row)
{
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for (var i = 0; i < rowLength; i++)
    rowVector[i] = matrix[row, i];

    return rowVector;
}
// Return the minimum absolute difference adjacent
// elements of array
static int mindiff(int [,]arr, int n, int m)
{

    // Sort each row of the matrix.
    for (int i = 0; i < n; i++)
        Array.Sort(GetRow(arr,i));

    int ans = +2147483647;

    // For each matrix element
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < m; j++)
        {

        // Search smallest element in the
        // next row which is greater than
        // or equal to the current element
        int p = bsearch(0, m-1, arr[i,j], GetRow(arr,i+1));
        ans = Math.Min(ans, Math.Abs(arr[i + 1,p] - arr[i,j]));

        // largest element which is smaller than the current
        // element in the next row must be just before
        // smallest element which is greater than or equal
        // to the current element because rows are sorted.
        if (p-1 >= 0)
            ans = Math.Min(ans,
                        Math.Abs(arr[i + 1,p - 1] - arr[i,j]));
        }
    }
    return ans;
}

// Driver code
public static void Main (String[] args)
{
    int [,]m ={{8, 5},
                {6, 8}};

    Console.WriteLine(mindiff(m, R, C));
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// absolute difference between any
// of the adjacent elements of an
// array which is created by picking
// one element from each row of the matrix.
$R = 2;
$C = 2;

// Return smallest element greater
// than or equal to the current element.
function bsearch($low, $high, $n, $arr)
{
    $mid = ($low + $high) / 2;

    if($low <= $high)
    {
        if($arr[$mid] < $n)
            return bsearch($mid + 1, $high,
                                 $n, $arr);
        return bsearch($low, $mid - 1,
                            $n, $arr);
    }
    return $low;
}

// Return the minimum absolute difference
// adjacent elements of array
function mindiff($arr, $n, $m)
{
    // Sort each row of the matrix.
    for ($i = 0; $i < $n; $i++)
        sort($arr);

    $ans = PHP_INT_MAX;

    // For each matrix element
    for ($i = 0; $i < $n - 1; $i++)
    {
        for ( $j = 0; $j < $m; $j++)
        {
            // Search smallest element in the
            // next row which is greater than
            // or equal to the current element
            $p = bsearch(0, $m - 1, $arr[$i][$j],
                                    $arr[$i + 1]);
            $ans = min($ans, abs($arr[$i + 1][$p] -
                                 $arr[$i][$j]));

            // largest element which is smaller than
            // the current element in the next row
            // must be just before smallest element
            // which is greater than or equal to the
            // current element because rows are sorted.
            if ($p - 1 >= 0)
                $ans = min($ans, abs($arr[$i + 1][$p - 1] -
                                     $arr[$i][$j]));
        }
    }
    return $ans;
}

// Driver Code
$m = array(8, 5, 6, 8);

echo mindiff($m, $R, $C), "\n";

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the minimum
// absolute difference between any
// of the adjacent elements of an
// array which is created by picking
// one element from each row of the matrix.
let R = 2;
let C = 2;

// Return smallest element greater than
// or equal to the current element.
function bsearch(low, high, n, arr)
{
    let mid = (low + high) / 2;

    if (low <= high)
    {
        if (arr[mid] < n)
            return bsearch(mid + 1,
                           high, n, arr);

        return bsearch(low, mid - 1,
                       n, arr);
    }
    return low;
}

// Return the minimum absolute difference
// adjacent elements of array
function mindiff(arr, n, m)
{

    // Sort each row of the matrix.
    for(let i = 0; i < n; i++)
        arr.sort();

    let ans = +2147483647;

    // For each matrix element
    for(let i = 0; i < n - 1; i++)
    {
        for(let j = 0; j < m; j++)
        {

            // Search smallest element in the
            // next row which is greater than
            // or equal to the current element
            let p = bsearch(0, m - 1, arr[i][j],
                                      arr[i + 1]);
            ans = Math.min(ans,
                  Math.abs(arr[i + 1][p] -
                           arr[i][j]));

            // largest element which is smaller
            // than the current element in the
            // next row must be just before smallest
            // element which is greater than or equal
            // to the current element because
            // rows are sorted.
            if (p - 1 >= 0)
                ans = Math.min(ans,
                      Math.abs(arr[i + 1][p - 1] -
                               arr[i][j]));
        }
    }
    return ans;
}

// Driver Code
let m = [ [ 8, 5 ],
          [ 6, 8 ] ];

document.write(mindiff(m, R, C));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
0
```

**时间复杂度:** O(N*M*logM)。

本文由 [**Anuj Chauhan**](https://web.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。