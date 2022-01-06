# 找到每一行每一列异或相等的 N×N 网格

> 原文:[https://www . geesforgeks . org/find-an-n-x-n-grid-其每行每列的异或等于/](https://www.geeksforgeeks.org/find-an-n-x-n-grid-whose-xor-of-every-row-and-column-is-equal/)

给定一个整数 **N** ，它是 **4** 的倍数，任务是找到一个 **N x N** 网格，每行和每列的**按位异或**是相同的。
**举例:**

> **输入:** N = 4
> **输出:**
> 0 1 2 3
> 4 5 6 7
> 8 9 10 11
> 12 13 14 15
> **输入:** N = 8
> **输出:**
> 0 2 3 16 17 18 19
> 4 5 6 7 20 21 22 23
> 8 9 10 11 22 35 48 49 50 51
> 36 37 38 39 52 53 54 55
> 40 41 42 43 56 57 58 59
> 44 45 46 47 60 61 62 63

**方法:**为了解决这个问题，让我们将每行每列的**异或**固定为 0，因为从 0 开始的 4 个连续数字的异或为 0。这里有一个 4 x 4 矩阵的例子:

> 0 ^ 1 ^ 2 ^ 3 = 0
> 4 ^ 5 ^ 6 ^ 7 = 0
> 8 ^ 9 ^ 10 11 = 0
> 12 13 14 15 = 0
> 以此类推。

如果您在上面的例子中注意到，每行和每列的 xor 都是 0。现在，我们需要以这样的方式放置数字，即每行和每列的 xor 为 0。因此，我们可以将**N×N**矩阵划分为更小的 4×4 矩阵，具有 **N / 4** 行和列，并以每行和列的异或为 0 的方式填充单元格。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the n x n matrix
// that satisfies the given condition
void findGrid(int n)
{
    int arr[n][n];

    // Initialize x to 0
    int x = 0;

    // Divide the n x n matrix into n / 4 matrices
    // for each of the n / 4 rows where
    // each matrix is of size 4 x 4
    for (int i = 0; i < n / 4; i++) {
        for (int j = 0; j < n / 4; j++) {
            for (int k = 0; k < 4; k++) {
                for (int l = 0; l < 4; l++) {
                    arr[i * 4 + k][j * 4 + l] = x;
                    x++;
                }
            }
        }
    }

    // Print the generated matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << arr[i][j] << " ";
        }
        cout << "\n";
    }
}

// Driver code
int main()
{
    int n = 4;

    findGrid(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to find the n x n matrix
// that satisfies the given condition
static void findGrid(int n)
{
    int [][]arr = new int[n][n];

    // Initialize x to 0
    int x = 0;

    // Divide the n x n matrix into n / 4 matrices
    // for each of the n / 4 rows where
    // each matrix is of size 4 x 4
    for (int i = 0; i < n / 4; i++)
    {
        for (int j = 0; j < n / 4; j++)
        {
            for (int k = 0; k < 4; k++)
            {
                for (int l = 0; l < 4; l++)
                {
                    arr[i * 4 + k][j * 4 + l] = x;
                    x++;
                }
            }
        }
    }

    // Print the generated matrix
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            System.out.print(arr[i][j] + " ");
        }
        System.out.println(" ");
    }
}

// Driver code
public static void main (String[] args)
{
    int n = 4;

    findGrid(n);
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the n x n matrix
# that satisfies the given condition
def findGrid(n):

    arr = [[0 for k in range(n)]
              for l in range(n)]

    # Initialize x to 0
    x = 0

    # Divide the n x n matrix into n / 4 matrices
    # for each of the n / 4 rows where
    # each matrix is of size 4 x 4
    for i in range(n // 4):
        for j in range(n // 4):
            for k in range(4):
                for l in range(4):
                    arr[i * 4 + k][j * 4 + l] = x
                    x += 1

    # Print the generated matrix
    for i in range(n):
        for j in range(n):
            print(arr[i][j], end = " ")
        print()

# Driver code
n = 4
findGrid(n)

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the n x n matrix
// that satisfies the given condition
static void findGrid(int n)
{
    int [,]arr = new int[n, n];

    // Initialize x to 0
    int x = 0;

    // Divide the n x n matrix into n / 4 matrices
    // for each of the n / 4 rows where
    // each matrix is of size 4 x 4
    for (int i = 0; i < n / 4; i++)
    {
        for (int j = 0; j < n / 4; j++)
        {
            for (int k = 0; k < 4; k++)
            {
                for (int l = 0; l < 4; l++)
                {
                    arr[i * 4 + k, j * 4 + l] = x;
                    x++;
                }
            }
        }
    }

    // Print the generated matrix
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            Console.Write(arr[i, j] + " ");
        }
        Console.WriteLine(" ");
    }
}

// Driver code
public static void Main (String[] args)
{
    int n = 4;

    findGrid(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the n x n matrix
// that satisfies the given condition
function findGrid(n)
{
    let arr = new Array(n);
    for (let i = 0; i < n; i++)
        arr[i] = new Array(n);

    // Initialize x to 0
    let x = 0;

    // Divide the n x n matrix into n / 4 matrices
    // for each of the n / 4 rows where
    // each matrix is of size 4 x 4
    for (let i = 0; i < parseInt(n / 4); i++) {
        for (let j = 0; j < parseInt(n / 4); j++) {
            for (let k = 0; k < 4; k++) {
                for (let l = 0; l < 4; l++) {
                    arr[i * 4 + k][j * 4 + l] = x;
                    x++;
                }
            }
        }
    }

    // Print the generated matrix
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            document.write(arr[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver code
    let n = 4;

    findGrid(n);

</script>
```

**Output:** 

```
0 1 2 3 
4 5 6 7 
8 9 10 11 
12 13 14 15
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(N <sup>2</sup> )