# 求最大异或的子矩阵

> 原文:[https://www . geesforgeks . org/find-a-sub-matrix-with-maximum-xor/](https://www.geeksforgeeks.org/find-a-sub-matrix-with-maximum-xor/)

**问题**给定 N 边的正方形矩阵，我们必须找到一个子矩阵，这样它的元素的按位异或是最大的，我们必须打印最大的按位异或。
**例:**

```
Input : 
         matrix is
        { {1, 2, 3, 4}
          {5, 6, 7, 8}
          {9, 10, 11, 12}
          {13, 14, 15, 16} } 
Output : 31
We get the value 31 by doing XOR of submatrix [15, 16}
```

**天真方法**蛮力方法是通过运行四个循环来找到数组的所有子矩阵，两个循环用于开始行和列，两个循环用于结束行和列，现在找到子矩阵所有元素的 xor，并找出 xor，检查这个子矩阵的 xor 是否最大。
**时间复杂度:O ( n^6 )**
**高效方法**在该方法中，我们将计算从 1，1 到 I，j 的每个子矩阵的 xor，这可以通过使用以下公式在 O (N*N)中完成:
(子矩阵从 1，1 到 I，j 的 xor)=(子矩阵从 1，1 到 i-1 的 xor，子矩阵从 1，1 到 I，j-1 的 j )^(xor)^(子矩阵从 1，1 到 i-1，j-1 的 xor)
现在为了计算从 I，j 到 i1，j1 的子矩阵的 xor，我们可以使用下面的公式
(子矩阵从 I，j 到 i1，j1 的 xor)=(子矩阵从 1，1 到 i1，j1 的)^(xor 从 1，1 到 i-1，j-1) ^(子矩阵从 1，1 到 i1，j-1 的 xor)^(子矩阵从 1，1 到 i-1，j1 的 xor)。
我们要运行四个循环才能找出数组的所有子矩阵，子矩阵的 xor 可以在 O(1)时间内计算出来。
因此时间复杂度降低到**o(n^4)**t15】

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;
#define N 101

// Compute the xor of elements from (1, 1) to
// (i, j) and store it in prefix_xor[i][j]
void prefix(int arr[N][N], int prefix_xor[N][N], int n)
{
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {

            // xor of submatrix from 1, 1 to i, j is
            // (xor of submatrix from  1, 1 to i-1,
            // j )^(xor of submatrix from 1, 1 to i, j-1)
            // ^(xor of submatrix from 1, 1 to i-1, j-1) ^
            // arr[i][j]
            prefix_xor[i][j] = arr[i][j] ^
                               prefix_xor[i - 1][j] ^
                               prefix_xor[i][j - 1] ^
                               prefix_xor[i - 1][j - 1];
        }
    }
}
// find the submatrix with maximum xor value
void Max_xor(int prefix_xor[N][N], int n)
{
    int max_value = 0;

    // we need four loops to find all the submatrix
    // of a matrix
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            for (int i1 = i; i1 <= n; i1++) {
                for (int j1 = j; j1 <= n; j1++) {

                    // xor of submatrix from i, j to i1, j1 is
                    //  (xor of submatrix from 1, 1 to i1, j1 )
                    // ^(xor of submatrix from 1, 1 to i-1, j-1)
                    // ^(xor of submatrix from 1, 1 to i1, j-1)
                    // ^(xor of submatrix from 1, 1 to i-1, j1)
                    int x = 0;
                    x ^= prefix_xor[i1][j1];
                    x ^= prefix_xor[i - 1][j - 1];
                    x ^= prefix_xor[i1][j - 1];
                    x ^= prefix_xor[i - 1][j1];

                    // if the xor is greater than maximum value
                    // substitute it
                    max_value = max(max_value, x);
                }
            }
        }
    }
    cout << max_value << endl;
}

// Driver code
int main()
{
    int arr[N][N] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    int n = 4;
    int prefix_xor[N][N] = { 0 };

    // Find the prefix_xor
    prefix(arr, prefix_xor, n);

    // Find submatrix with maximum bitwise xor
    Max_xor(prefix_xor, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
public class GFG
{

static int N =101;

// Compute the xor of elements from (1, 1) to
// (i, j) and store it in prefix_xor[i][j]
static void prefix(int arr[][], int prefix_xor[][], int n)
{
    for (int i = 1; i < n; i++)
    {
        for (int j = 1; j < n; j++)
        {

            // xor of submatrix from 1, 1 to i, j is
            // (xor of submatrix from 1, 1 to i-1,
            // j )^(xor of submatrix from 1, 1 to i, j-1)
            // ^(xor of submatrix from 1, 1 to i-1, j-1) ^
            // arr[i][j]
            prefix_xor[i][j] = arr[i][j] ^
                            prefix_xor[i - 1][j] ^
                            prefix_xor[i][j - 1] ^
                            prefix_xor[i - 1][j - 1];
        }
    }
}
// find the submatrix with maximum xor value
static void Max_xor(int prefix_xor[][], int n)
{
    int max_value = 0;

    // we need four loops to find all the submatrix
    // of a matrix
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            for (int i1 = i; i1 <= n; i1++)
            {
                for (int j1 = j; j1 <= n; j1++)
                {

                    // xor of submatrix from i, j to i1, j1 is
                    // (xor of submatrix from 1, 1 to i1, j1 )
                    // ^(xor of submatrix from 1, 1 to i-1, j-1)
                    // ^(xor of submatrix from 1, 1 to i1, j-1)
                    // ^(xor of submatrix from 1, 1 to i-1, j1)
                    int x = 0;
                    x ^= prefix_xor[i1][j1];
                    x ^= prefix_xor[i - 1][j - 1];
                    x ^= prefix_xor[i1][j - 1];
                    x ^= prefix_xor[i - 1][j1];

                    // if the xor is greater than maximum value
                    // substitute it
                    max_value = Math.max(max_value, x);
                }
            }
        }
    }
    System.out.println(max_value);
}

// Driver code
public static void main(String[] args)
{
    int arr[][] = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    int n = 4;
    int prefix_xor[][] = new int[N][N];

    // Find the prefix_xor
    prefix(arr, prefix_xor, n);

    // Find submatrix with maximum bitwise xor
    Max_xor(prefix_xor, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement the above approach
N = 101

# Compute the xor of elements from (1, 1) to
# (i, j) and store it in prefix_xor[i][j]
def prefix(arr, prefix_xor, n):
    for i in range(1, n):
        for j in range(1, n):

            # xor of submatrix from 1, 1 to i, j is
            # (xor of submatrix from 1, 1 to i-1,
            # j )^(xor of submatrix from 1, 1 to i, j-1)
            # ^(xor of submatrix from 1, 1 to i-1, j-1) ^
            # arr[i][j]
            prefix_xor[i][j] = (arr[i][j] ^
                                prefix_xor[i - 1][j] ^
                                prefix_xor[i][j - 1] ^
                                prefix_xor[i - 1][j - 1])

# find the submatrix with maximum xor value
def Max_xor(prefix_xor, n):
    max_value = 0

    # we need four loops to find
    # all the submatrix of a matrix
    for i in range(1, n + 1):
        for j in range(1, n + 1):
            for i1 in range(i, n + 1):
                for j1 in range(j, n + 1):

                    # xor of submatrix from i, j to i1, j1 is
                    # (xor of submatrix from 1, 1 to i1, j1 )
                    # ^(xor of submatrix from 1, 1 to i-1, j-1)
                    # ^(xor of submatrix from 1, 1 to i1, j-1)
                    # ^(xor of submatrix from 1, 1 to i-1, j1)
                    x = 0
                    x ^= prefix_xor[i1][j1]
                    x ^= prefix_xor[i - 1][j - 1]
                    x ^= prefix_xor[i1][j - 1]
                    x ^= prefix_xor[i - 1][j1]

                    # if the xor is greater than maximum value
                    # substitute it
                    max_value = max(max_value, x)

    print(max_value)

# Driver code
arr = [[ 1, 2, 3, 4 ],
       [ 5, 6, 7, 8 ],
       [ 9, 10, 11, 12 ],
       [ 13, 14, 15, 16 ]]

n = 4
prefix_xor = [[ 0 for i in range(N)]
                  for i in range(N)]

# Find the prefix_xor
prefix(arr, prefix_xor, n)

# Find submatrix with maximum bitwise xor
Max_xor(prefix_xor, n)

#  This code is contributed by Mohit Kumar
```

C#

```
 // C# program to implement the above approach
using System;

class GFG 
{

    static int N =101;

    // Compute the xor of elements from (1, 1) to 
    // (i, j) and store it in prefix_xor[i][j]
    static void prefix(int [ , ] arr, int [ , ] prefix_xor, int n)
    {
        for (int i = 1; i < n; i++)
        {
            for (int j = 1; j < n; j++)
            {

                // xor of submatrix from 1, 1 to i, j is 
                // (xor of submatrix from 1, 1 to i-1, 
                // j )^(xor of submatrix from 1, 1 to i, j-1)
                // ^(xor of submatrix from 1, 1 to i-1, j-1) ^
                // arr[i][j]
                prefix_xor[i, j] = arr[i, j] ^ 
                                prefix_xor[i - 1, j] ^ 
                                prefix_xor[i, j - 1] ^
                                prefix_xor[i - 1, j - 1];
            }
        }
    }

    // find the submatrix with maximum xor value
    static void Max_xor(int[ , ] prefix_xor, int n)
    {
        int max_value = 0;

        // we need four loops to find all the submatrix
        // of a matrix
        for (int i = 1; i <= n; i++) 
        {
            for (int j = 1; j <= n; j++) 
            {
                for (int i1 = i; i1 <= n; i1++) 
                {
                    for (int j1 = j; j1 <= n; j1++) 
                    {

                        // xor of submatrix from i, j to i1, j1 is
                        // (xor of submatrix from 1, 1 to i1, j1 )
                        // ^(xor of submatrix from 1, 1 to i-1, j-1)
                        // ^(xor of submatrix from 1, 1 to i1, j-1)
                        // ^(xor of submatrix from 1, 1 to i-1, j1)
                        int x = 0;
                        x ^= prefix_xor[i1, j1];
                        x ^= prefix_xor[i - 1, j - 1];
                        x ^= prefix_xor[i1, j - 1];
                        x ^= prefix_xor[i - 1, j1];

                        // if the xor is greater than maximum value
                        // substitute it
                        max_value = Math.Max(max_value, x);
                    }
                }
            }
        }
        Console.WriteLine(max_value);
    }

    // Driver code
    public static void Main() 
    {
        int [ , ] arr = new int [ , ] { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 9, 10, 11, 12 },
                        { 13, 14, 15, 16 } };

        int n = 4;
        int [ , ] prefix_xor = new int[N, N];

        // Find the prefix_xor
        prefix(arr, prefix_xor, n);

        // Find submatrix with maximum bitwise xor
        Max_xor(prefix_xor, n);
    }
}

// This code is contributed by ihritik 
```

## java 描述语言

```
<script>

// Javascript program to implement the above approach
var N = 101;

// Compute the xor of elements from (1, 1) to
// (i, j) and store it in prefix_xor[i][j]
function prefix(arr, prefix_xor, n)
{
    for (var i = 1; i < n; i++) {
        for (var j = 1; j < n; j++) {

            // xor of submatrix from 1, 1 to i, j is
            // (xor of submatrix from  1, 1 to i-1,
            // j )^(xor of submatrix from 1, 1 to i, j-1)
            // ^(xor of submatrix from 1, 1 to i-1, j-1) ^
            // arr[i][j]
            prefix_xor[i][j] = arr[i][j] ^
                               prefix_xor[i - 1][j] ^
                               prefix_xor[i][j - 1] ^
                               prefix_xor[i - 1][j - 1];
        }
    }
}

// find the submatrix with maximum xor value
function Max_xor(prefix_xor, n)
{
    var max_value = 0;

    // we need four loops to find all the submatrix
    // of a matrix
    for (var i = 1; i <= n; i++)
    {
        for (var j = 1; j <= n; j++)
        {
            for (var i1 = i; i1 <= n; i1++)
            {
                for (var j1 = j; j1 <= n; j1++)
                {

                    // xor of submatrix from i, j to i1, j1 is
                    //  (xor of submatrix from 1, 1 to i1, j1 )
                    // ^(xor of submatrix from 1, 1 to i-1, j-1)
                    // ^(xor of submatrix from 1, 1 to i1, j-1)
                    // ^(xor of submatrix from 1, 1 to i-1, j1)
                    var x = 0;
                    x ^= prefix_xor[i1][j1];
                    x ^= prefix_xor[i - 1][j - 1];
                    x ^= prefix_xor[i1][j - 1];
                    x ^= prefix_xor[i - 1][j1];

                    // if the xor is greater than maximum value
                    // substitute it
                    max_value = Math.max(max_value, x);
                }
            }
        }
    }
    document.write( max_value );
}

// Driver code
var arr = [ [ 1, 2, 3, 4 ],
                  [ 5, 6, 7, 8 ],
                  [ 9, 10, 11, 12 ],
                  [ 13, 14, 15, 16 ] ];
var n = 4;
var prefix_xor = Array.from(Array(N), () => Array(N).fill(0));

// Find the prefix_xor
prefix(arr, prefix_xor, n);

// Find submatrix with maximum bitwise xor
Max_xor(prefix_xor, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
31
```

时间复杂度:O(n <sup>4</sup> )

辅助空间:0(1)