# 使用数字 1 到 N^2

从矩阵的层中找到最小值的最大值

> 原文:[https://www . geeksforgeeks . org/find-从矩阵的最大值到最小值-使用数字-1 到-n2/](https://www.geeksforgeeks.org/find-maximum-of-minimums-from-layers-of-matrix-using-numbers-1-to-n2/)

给定大小为 **N*N** 的正方形**矩阵**,使用数字 **1 到 N^2** ,任务是找到矩阵每一层的最小值的最大值。

> 矩阵的**层**是从(I，I)开始到(N–I+1，N–I+1)结束的子矩阵的边界元素，其中 1 < = i < = ceil(N/2)。

**示例:**

> **输入:**下面是给定的矩阵:
> 1 2 3 4
> 5 6 7 8
> 9 10 11 1 2
> 13 14 15 16
> T7】输出: 6
> **说明:**层数为{1，2，3，4，8，12，16，15，14，13，9，5}最少为 1，{6，7，10，11}最少为 6。1 和 6 的最大值是 6。
> 
> **输入:**下面是给定的矩阵:
> 1 2 3
> 4 30 5
> 1 2 3
> **输出:** 30
> **说明:**图层是最小 1 的{1，2，3，5，3，2，1，4，1}和最小 30 的{30}。1 和 30 的最大值是 30。

**方法:**思路是仔细观察，对于第 i <sup>层</sup>层，上、左、右、下边界的元素在索引处:

*   顶部边界在索引(I，j)处
*   左边界在索引(j，I)处
*   右边界在索引处(j，n–I+1)
*   底部边界在索引处(n–I+1，j)，其中 I < = j < = n–I+1

因此，找到每层的最小值，并存储这些最小值的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the minimum
// of the boundary elements
int getBoundaryMin(int a[][4], int n,
                   int index)
{
    int min1 = INT_MAX;

    for(int i = index; i < n - index; i++)
    {

        // Top boundary
        min1 = min(min1,
                   a[index][i]);

        // Left boundary
        min1 = min(min1,
                   a[i][index]);

        // Right boundary
        min1 = min(min1,
                    a[i][n - index - 1]);

        // Bottom boundary
        min1 = min(min1,
                   a[n - index - 1][i]);
    }
    return min1;
}

// Function to find the maximum of
// minimums of all layers
void MaximumOfMinimum(int a[][4], int n)
{

    // Calculate the layers
    int layers = n / 2 + n % 2;
    int max1 = INT_MIN;

    // Iterate for all the layers
    for(int i = 0; i < layers; i++)
    {

        // Find maximum
        max1 = max(max1,
                   getBoundaryMin(a, n, i));
    }

    // Print the answer
    cout << (max1);
}

// Driver Code
int main()
{

    // Initialize the matrix
    int a[][4] = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 },
                   { 13, 14, 15, 16 } };

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    MaximumOfMinimum(a, n);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach

class GFG {

    // Function to return the minimum
    // of the boundary elements
    static int
    getBoundaryMin(int a[][], int n,
                   int index)
    {
        int min = Integer.MAX_VALUE;

        for (int i = index; i < n - index; i++) {

            // Top boundary
            min = Math.min(
                min,
                a[index][i]);

            // Left boundary
            min = Math.min(
                min,
                a[i][index]);

            // Right boundary
            min = Math.min(
                min,
                a[i][n - index - 1]);

            // Bottom boundary
            min = Math.min(
                min,
                a[n - index - 1][i]);
        }

        return min;
    }

    // Function to find the maximum of
    // minimums of all layers
    static void MaximumOfMinimum(
        int a[][], int n)
    {
        // Calculate the layers
        int layers = n / 2 + n % 2;
        int max = Integer.MIN_VALUE;

        // Iterate for all the layers
        for (int i = 0; i < layers; i++) {

            // Find maximum
            max
                = Math.max(
                    max,
                    getBoundaryMin(a, n, i));
        }

        // Print the answer
        System.out.print(max);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Initialize the matrix
        int a[][] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

        int n = a.length;

        // Function call
        MaximumOfMinimum(a, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to return the minimum
# of the boundary elements
def getBoundaryMin(a, n, index):

    min1 = sys.maxsize

    for i in range(index, n - index):

        # Top boundary
        min1 = min(min1, a[index][i])

        # Left boundary
        min1 = min(min1, a[i][index])

        # Right boundary
        min1 = min(min1, a[i][n - index - 1])

        # Bottom boundary
        min1 = min(min1, a[n - index - 1][i])

    return min1

# Function to find the maximum of
# minimums of all layers
def MaximumOfMinimum(a, n):

    # Calculate the layers
    layers = n // 2 + n % 2
    max1 = -sys.maxsize - 1

    # Iterate for all the layers
    for i in range(0, layers):

        # Find maximum
        max1 = max(max1, getBoundaryMin(a, n, i))

    # Print the answer
    print(max1)

# Driver Code

# Initialize the matrix
a = [ [ 1, 2, 3, 4 ],
      [ 5, 6, 7, 8 ],
      [ 9, 10, 11, 12 ] ,
      [ 13, 14, 15, 16 ] ]

n = len(a)

# Function call
MaximumOfMinimum(a, n)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the minimum
// of the boundary elements
static int getBoundaryMin(int[,]a, int n,
                          int index)
{
    int min = int.MaxValue;

    for(int i = index; i < n - index; i++)
    {

        // Top boundary
        min = Math.Min(min, a[index, i]);

        // Left boundary
        min = Math.Min(min, a[i, index]);

        // Right boundary
        min = Math.Min(min, a[i, n - index - 1]);

        // Bottom boundary
        min = Math.Min(min, a[n - index - 1, i]);
    }
    return min;
}

// Function to find the maximum of
// minimums of all layers
static void MaximumOfMinimum(int[,]a, int n)
{

    // Calculate the layers
    int layers = n / 2 + n % 2;
    int max = int.MinValue;

    // Iterate for all the layers
    for(int i = 0; i < layers; i++)
    {

        // Find maximum
        max = Math.Max(max,
                       getBoundaryMin(a, n, i));
    }

    // Print the answer
    Console.Write(max);
}

// Driver Code
public static void Main(String[] args)
{

    // Initialize the matrix
    int[,]a = { { 1, 2, 3, 4 },
                { 5, 6, 7, 8 },
                { 9, 10, 11, 12 },
                { 13, 14, 15, 16 } };

    int n = a.GetLength(0);

    // Function call
    MaximumOfMinimum(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the minimum
// of the boundary elements
function getBoundaryMin(a, n, index)
{
    min1 = 1000000000;

    for(var i = index; i < n - index; i++)
    {

        // Top boundary
        min1 = Math.min(min1,
        a[index][i]);

        // Left boundary
        min1 = Math.min(min1,
        a[i][index]);

        // Right boundary
        min1 = Math.min(min1,
        a[i][n - index - 1]);

        // Bottom boundary
        min1 = Math.min(min1,
        a[n - index - 1][i]);
    }
    return min1;
}

// Function to find the maximum of
// minimums of all layers
function MaximumOfMinimum(a, n)
{

    // Calculate the layers
    var layers = parseInt(n / 2) + n % 2;
    var max1 = -1000000000;

    // Iterate for all the layers
    for(var i = 0; i < layers; i++)
    {

        // Find maximum
        max1 = Math.max(max1,
        getBoundaryMin(a, n, i));
    }

    // Print the answer
    document.write(max1);
}

// Driver Code

// Initialize the matrix
var a = [ [ 1, 2, 3, 4 ],
          [ 5, 6, 7, 8 ],
          [ 9, 10, 11, 12 ],
          [ 13, 14, 15, 16 ] ];
var n = a.length;

// Function call
MaximumOfMinimum(a, n);

// This code is contributed by itsok

</script>
```

**Output:** 

```
6
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*