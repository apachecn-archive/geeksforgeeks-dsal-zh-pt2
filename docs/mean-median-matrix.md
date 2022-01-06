# 矩阵的平均值和中值

> 原文:[https://www.geeksforgeeks.org/mean-median-matrix/](https://www.geeksforgeeks.org/mean-median-matrix/)

给定大小为 **n*n** 的排序矩阵。计算矩阵的**平均值**和**中值**。
示例:

```
Input : 1 2 3
        4 5 6
        7 8 9
Output :Mean: 5
        Median: 5

Input : 1 1 1
        2 2 2
        4 4 4
Output :Mean: 2
        Median: 2
```

```
Mean of matrix is = 
   (sum of all elements of matrix)/
   (total elements of matrix)
Note that this definition doesn't require
matrix to be sorted and works for all
matrices.

Median of a sorted matrix is calculated as:
1\. When n is odd
    median is mat[n/2][n/2]
2\. When n is even, median is average
   of middle two elements.
   Middle two elements can be found at indexes
   a[(n-2)/2][n-1] and a[n/2][0]    
```

如果给定的矩阵没有排序，我们可以通过首先[排序矩阵](https://www.geeksforgeeks.org/sort-matrix-way-increasing-order/)来找到它的中值。

## C++

```
// CPP program to find mean and median
// of sorted square matrix.
#include <bits/stdc++.h>
using namespace std;

const int N = 4;

// Returns mean of a given matrix of
// size n x n.
double findMean(int a[][N])
{
    int sum = 0;

    // total sum calculation of matrix
    for (int i=0; i<N; i++)
       for (int j=0; j<N; j++)
          sum += a[i][j];

    return (double)sum/(N*N);
}

// Function for calculating median
double findMedian(int a[][N])
{
    if (N % 2 != 0)
       return a[N/2][N/2];

    if (N%2 == 0)
       return (a[(N-2)/2][N-1] +
                       a[N/2][0])/2.0;
}

// Driver program
int main()
{
    int a[N][N]= {{1, 2, 3, 4},
                   {5, 6, 7, 8},
                   {9, 10, 11, 12},
                   {13, 14, 15, 16}};
    cout << "Mean : " << findMean(a) << endl
         << "Median : "<< findMedian(a) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find mean and median
// of sorted square matrix.
import java.io.*;

class GFG
{

// Returns mean of a given
// matrix of size n x n.
static double findMean(int a[][],
                    int n)
{
    int sum = 0;
    int N=n;

    // total sum calculation of matrix
    for (int i = 0; i < N; i++)
    for (int j = 0; j < N; j++)
        sum += a[i][j];

    return (double)sum / (N * N);
}

// Function for calculating median
static double findMedian(int a[][], int n)
{
    int N = n;

    if (N % 2 != 0)
    return a[N / 2][N / 2];

    if (N % 2 == 0)
    return (a[(N - 2) / 2][ N - 1] +
            a[ N / 2][0]) / (2.0);
    return 0;
}

    // Driver Code
    public static void main (String[] args)
    {
        int a[][]= {{1, 2, 3, 4},
                    {5, 6, 7, 8},
                    {9, 10, 11, 12},
                    {13, 14, 15, 16}};

        int n = a.length;
        System.out.println("Mean   : " +
                            findMean(a, n));
        System.out.println("Median : " +
                            findMedian(a, n));
    }

}

// This code is contributed by KRV.
```

## 蟒蛇 3

```
# Python3 program to find mean and median
# of sorted square matrix.
N = 4

# Returns mean of a given matrix of
# size n x n.
def findMean(a):

    summ = 0

    # total sum calculation of matrix
    for i in range(N):
        for j in range(N):
            summ += a[i][j]

    return summ/(N*N)

# Function for calculating median
def findMedian(a):
    if (N % 2 != 0):
        return a[N//2][N//2]
    if (N % 2 == 0):
        return (a[(N - 2)//2][N - 1] + a[N//2][0])/2

# Driver program
a = [[1, 2, 3, 4],[5, 6, 7, 8],
    [9, 10, 11, 12],[13, 14, 15, 16]]
print("Mean :", findMean(a))
print("Median :",findMedian(a))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find mean and median
// of sorted square matrix.
using System;

class GFG {

    // Returns mean of a given
    // matrix of size n x n.
    static double findMean(int [,]a, int n)
    {
        int sum = 0;
        int N = n;

        // total sum calculation of matrix
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                sum += a[i,j];

        return (double)sum / (N * N);
    }

    // Function for calculating median
    static double findMedian(int [,]a, int n)
    {
        int N = n;

        if (N % 2 != 0)
        return a[N / 2,N / 2];

        if (N % 2 == 0)
        return ( a[(N - 2) / 2, (N - 1)] +
                     a[ N / 2, 0] ) / (2.0);

        return 0;
    }

    // Driver Code
    public static void Main ()
    {
        int [,]a= { { 1,  2,  3,  4},
                    { 5,  6,  7,  8},
                    { 9, 10, 11, 12},
                    {13, 14, 15, 16} };

        int n = a.GetLength(0);

        Console.WriteLine("Mean : " +
                            findMean(a, n));

        Console.WriteLine("Median : " +
                            findMedian(a, n));
    }

}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// mean and median
// of sorted square
// matrix.

$N = 4;

// Returns mean of
// a given matrix of
// size n x n.
function findMean($a)
{
    global $N;
    $sum = 0;

    // total sum calculation
    // of matrix
    for ($i = 0; $i < $N; $i++)
    for ($j = 0; $j < $N; $j++)
        $sum += $a[$i][$j];

    return (double)$sum / ($N * $N);
}

// Function for calculating median
function findMedian($a)
{
    global $N;
    if ($N % 2 != 0)
    return $a[$N / 2][$N / 2];

    if ($N % 2 == 0)
    return ($a[($N - 2) / 2][$N - 1] +
                 $a[$N / 2][0]) / 2.0;
}

    // Driver Code
    $a= array(array(1, 2, 3, 4),
              array(5, 6, 7, 8),
              array(9, 10, 11, 12),
              array(13, 14, 15, 16));
        echo "Mean : " , findMean($a),"\n",
             "Median : ", findMedian($a);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascriptprogram to find mean and median
// of sorted square matrix.

// Returns mean of a given
// matrix of size n x n.
function findMean(a, n)
{
    var sum = 0;
    var N = n;

    // Total sum calculation of matrix
    for(var i = 0; i < N; i++)
        for(var j = 0; j < N; j++)
            sum += a[i][j];

    return sum / (N * N);
}

// Function for calculating median
function findMedian(a, n)
{
    var N = n;

    if (N % 2 != 0)
        return a[N / 2][N / 2];

    if (N % 2 == 0)
        return (a[(N - 2) / 2][ N - 1] +
                a[N / 2][0]) / (2.0);
    return 0;
}

// Driver Code
var a = [ [ 1, 2, 3, 4 ],
          [ 5, 6, 7, 8 ],
          [ 9, 10, 11, 12 ],
          [ 13, 14, 15, 16 ] ];

var n = a.length;
document.write("Mean   : " +
               findMean(a, n) + "<br>");
document.write("Median : " +
               findMedian(a, n) + "<br>");

// This code is contributed by Kirti

</script>
```

**输出:**

```
Mean : 8.5
Median : 8.5
```

本文由 [**喜马拉雅冉冉**](https://auth.geeksforgeeks.org/profile.php?user=himanshu_300) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。