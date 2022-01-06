# 距离二维矩阵中心 0 的最远距离

> 原文:[https://www . geeksforgeeks . org/距离二维矩阵中心 0 的最远距离/](https://www.geeksforgeeks.org/farthest-distance-of-a-0-from-the-center-of-a-2-d-matrix/)

给定一个奇数阶的矩阵 *mat* ，任务是找到一个 *0* 到矩阵中心的最远距离。位于矩阵位置 *(i1，j1)和(i2，j2)* 的两个元素之间的距离计算为|i1- i2| + |j1-j2|。如果矩阵中没有出现 *0* ，则打印 *0* 作为结果。
**举例:**

> **输入:** mat[][] = {{2，3，0}，{0，2，0}，{0，1，1 } }
> T3】输出:2
> T6】输入: mat[][] = {{2，3，4，{0，2，0}，{6，1，1}}
> **输出:** 1

**方法:**任何奇数阶矩阵的中心都在索引处 *i = j = floor(n/2)* 。现在为了找到任何一个 *0* 到中心的最远距离，计算每个 *0* 到矩阵中心的距离为 *|i-n/2| + |j-n/2|* 并更新最大距离。最后打印结果，或者如果矩阵不包含任何 *0* ，则打印 *0* 。
以下是上述方法的实施:

## C++

```
// C++ program to find the farthest distance
// of a 0 from the center of the matrix
#include <bits/stdc++.h>
#define n 3
using namespace std;

// function to return farthest distance
// of zero from center of the matrix
int farthestDistance(int matrix[][n])
{

    int result = 0;

    // traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0)
                result = max(result
                           , abs(i - n/2) + abs(j - n/2));
        }
    }

    // return result
    return result;
}

// driver program
int main()
{
    int matrix[n][n] = { { 1, 2, 3 }
                       , { 0, 1, 1 }
                       , { 0, 0, 0 } };

    cout << farthestDistance(matrix);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java program to find the farthest distance
// of a 0 from the center of the matrix

import java.io.*;

class GFG {

static int n = 3;

// function to return farthest distance
// of zero from center of the matrix
static int farthestDistance(int matrix[][])
{

    int result = 0;

    // traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0)
                result = Math.max(result
                        , Math.abs(i - n/2) + Math.abs(j - n/2));
        }
    }

    // return result
    return result;
}

// driver program

    public static void main (String[] args) {
            int matrix[][] = { { 1, 2, 3 }
                    , { 0, 1, 1 }
                    , { 0, 0, 0 } };

    System.out.print(farthestDistance(matrix));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find the farthest distance
# of a 0 from the center of the matrix

n = 3

# function to return farthest distance
# of zero from center of the matrix
def farthestDistance(matrix):
    result = 0

    # traverse the matrix
    for i in range (0, n):
        for j in range (0, n):
            if (matrix[i][j] == 0):
                result = max(result, abs(i - n // 2) +
                                     abs(j - n//2))

    # return result
    return result

# Driver Code
matrix = [[1, 2, 3],
          [0, 1, 1],
          [0, 0, 0]]

print(farthestDistance(matrix))

# This code is contributed by
# Archana_kumari
```

## C#

```
// C# program to find the farthest distance
// of a 0 from the center of the matrix
using System;

class GFG
{

static int n = 3;

// function to return farthest distance
// of zero from center of the matrix
static int farthestDistance(int [,]matrix)
{

    int result = 0;

    // traverse the matrix
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (matrix[i,j] == 0)
                result = Math.Max(result ,
                         Math.Abs(i - n / 2) +
                         Math.Abs(j - n / 2));
        }
    }

    // return result
    return result;
}

// Driver Code
static public void Main ()
{
    int [,]matrix = {{ 1, 2, 3 },
                     { 0, 1, 1 },
                     { 0, 0, 0 }};

    Console.WriteLine(farthestDistance(matrix));
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the farthest distance
// of a 0 from the center of the matrix
$n = 3;

// function to return farthest distance
// of zero from center of the matrix
function farthestDistance($matrix)
{
    global $n;
    $result = 0;

    // traverse the matrix
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            if (($matrix[$i][$j] == 0) > 0)
                $result = max($result,
                          abs($i - $n / 2) +
                          abs($j - $n / 2));
        }
    }

    // return result
    return $result;
}

// Driver Code
$matrix = array(array( 1, 2, 3 ),
                array( 0, 1, 1 ),
                array( 0, 0, 0 ));

echo farthestDistance($matrix);

// This code is contributed by Sach_code
?>
```

## java 描述语言

```
<script>

// Javascript program to find the farthest distance
// of a 0 from the center of the matrix
var n = 3;

// function to return farthest distance
// of zero from center of the matrix
function farthestDistance(matrix)
{

    var result = 0;

    // traverse the matrix
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < n; j++) {
            if (matrix[i][j] == 0)
                result = Math.max(result
                           , Math.abs(i - n/2) + Math.abs(j - n/2));
        }
    }

    // return result
    return result;
}

// driver program
var matrix = [ [ 1, 2, 3 ]
                   , [ 0, 1, 1 ]
                   , [ 0, 0, 0 ] ];
document.write( farthestDistance(matrix));

</script>
```

**Output:** 

```
2
```