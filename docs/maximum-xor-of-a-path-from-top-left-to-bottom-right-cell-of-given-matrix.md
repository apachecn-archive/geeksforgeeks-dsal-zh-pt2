# 从给定矩阵的左上角到右下角单元的路径的最大异或

> 原文:[https://www . geeksforgeeks . org/给定矩阵从左上方到右下方的最大路径异或/](https://www.geeksforgeeks.org/maximum-xor-of-a-path-from-top-left-to-bottom-right-cell-of-given-matrix/)

给定尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)、 **mat[][]** ，任务是打印从给定矩阵的左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的路径的最大[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值。任何单元格 **(i，j)** 唯一可能的移动是 **(i + 1，j)** 和 **(i，j + 1)** 。
**注:** [路径的按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值定义为该路径上所有可能元素的按位异或。

**示例:**

> **输入:** mat[][] = {{3，2，1}，{6，5，4}，{7，8，9}}
> **输出:** 13
> **解释:**
> 从(0，0)到(N–1，M–1)的可能路径及其按位异或值为:
> (0，0) - > (0，1) - > (0，2) - > (1，2)-(T20)
> (0，0) - > (0，1) - > (1，1) - > (1，2) - > (2，2)异或值为 9。
> (0，0) - > (1，0) - > (1，1) - > (1，2) - > (2，2)异或值为 13。
> (0，0) - > (0，1) - > (1，1) - > (2，1) - > (2，2)异或值为 5。
> (0，0) - > (1，0) - > (1，1) - > (2，1) - > (2，2)异或值为 1。
> (0，0) - > (1，0) - > (2，0) - > (2，1) - > (2，2)具有异或值 3
> 因此，所有可能路径的最大按位异或值为 13。
> 
> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9 } }
> T3】输出: 15

**方法:**思路是[使用](https://www.geeksforgeeks.org/print-all-possible-paths-from-top-left-to-bottom-right-of-a-mxn-matrix/)[递归](https://www.geeksforgeeks.org/recursion/)生成给定矩阵从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的所有可能路径，并打印所有可能路径的最大异或值。以下是递归关系及其基本情况:

> **循环关系:**T2】printmaxx or(I，j，xorg value)= max(printmaxor(I–1，j，xorg value ^ mat[I][j])、printmaxor(I，j–1，xorg value ^ mat[I][j])
> 
> **基本情况:**
> **如果 i = 0 且 j = 0:** 返回 mat[i][j] ^ xorValue
> **如果 i = 0:** 返回 printMaxXOR(i，j–1，mat[i][j] ^ xorValue)
> **如果 j = 0:** 返回 print maxxor(I–1，j，mat[i][j] ^ xorValue)

按照以下步骤解决问题:

*   初始化一个变量，说**异或**存储从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**路径上所有可能元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。
*   利用上述递推关系，求出从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的所有可能路径的最大异或值。
*   最后，打印从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的所有可能路径的最大异或值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print maximum XOR
// value of all possible path
// from (0, 0) to (N - 1, M - 1)
int printMaxXOR(vector<vector<int> >& mat,
                int i, int j,
                int xorValue)
{
    // Base case
    if (i == 0 && j == 0) {
        return mat[i][j] ^ xorValue;
    }

    // Base case
    if (i == 0) {

        // Stores maximum XOR value
        // by selecting path from (i, j)
        // to (i, j - 1)
        return printMaxXOR(mat, i, j - 1,
                           mat[i][j] ^ xorValue);
    }

    if (j == 0) {

        // Stores maximum XOR value
        // by selecting path from (i, j)
        // to (i - 1, j)
        return printMaxXOR(mat, i - 1, j,
                           mat[i][j] ^ xorValue);
    }

    // Stores maximum XOR value
    // by selecting path from (i, j)
    // to (i - 1, j)
    int X
        = printMaxXOR(mat, i - 1,
                      j, mat[i][j] ^ xorValue);

    // Stores maximum XOR value
    // by selecting path from (i, j)
    // to (i, j - 1)
    int Y
        = printMaxXOR(mat, i, j - 1,
                      mat[i][j] ^ xorValue);

    return max(X, Y);
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 3, 2, 1 },
           { 6, 5, 4 },
           { 7, 8, 9 } };
    int N = mat.size();
    int M = mat[0].size();

    // Stores bitwise XOR of
    // all elements on each possible path
    int xorValue = 0;
    cout << printMaxXOR(mat, N - 1,
                        M - 1, xorValue);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
class GFG {
    public static int printMaxXOR(int[][] mat,
                                  int i, int j,
                                  int xorValue)
    {
        // Base case
        if (i == 0 && j == 0)
        {
            return mat[i][j] ^ xorValue;
        }

        // Base case
        if (i == 0) {

            // Stores maximum XOR value
            // by selecting path from (i, j)
            // to (i, j - 1)
            return printMaxXOR(mat, i,
                               j - 1,
                               mat[i][j] ^ xorValue);
        }

        if (j == 0) {

            // Stores maximum XOR value
            // by selecting path from (i, j)
            // to (i - 1, j)
            return printMaxXOR(mat,
                               i - 1, j,
                               mat[i][j] ^ xorValue);
        }

        // Stores maximum XOR value
        // by selecting path from (i, j)
        // to (i - 1, j)
        int X = printMaxXOR(mat,
                            i - 1, j,
                            mat[i][j] ^ xorValue);

        // Stores maximum XOR value
        // by selecting path from (i, j)
        // to (i, j - 1)
        int Y = printMaxXOR(mat,
                            i, j - 1,
                            mat[i][j] ^ xorValue);

        return Math.max(X, Y);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[][] mat
            = { { 3, 2, 1 },
               { 6, 5, 4 },
               { 7, 8, 9 } };
        int N = mat.length;
        int M = mat[0].length;

        // Stores bitwise XOR of
        // all elements on each possible path
        int xorValue = 0;
        System.out.println(
            printMaxXOR(mat, N - 1, M - 1, xorValue));
    }
    // This code is contributed by hemanth gadarla
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to print maximum XOR
# value of all possible path
# from (0, 0) to (N - 1, M - 1)
def printMaxXOR(mat, i, j,
                xorValue):

    # Base case
    if (i == 0 and j == 0):
        return mat[i][j] ^ xorValue

    # Base case
    if (i == 0):

        # Stores maximum XOR value
        # by selecting path from (i, j)
        # to (i, j - 1)
        return printMaxXOR(mat, i, j - 1,
                           mat[i][j] ^
                           xorValue)     
    if (j == 0):

        # Stores maximum XOR value
        # by selecting path from (i, j)
        # to (i - 1, j)
        return printMaxXOR(mat, i - 1, j,
                           mat[i][j] ^
                           xorValue)

    # Stores maximum XOR value
    # by selecting path from (i, j)
    # to (i - 1, j)
    X = printMaxXOR(mat, i - 1,
                    j, mat[i][j] ^
                    xorValue)

    # Stores maximum XOR value
    # by selecting path from (i, j)
    # to (i, j - 1)
    Y = printMaxXOR(mat, i, j - 1,
                    mat[i][j] ^
                    xorValue)

    return max(X, Y)

  # Driver Code
if __name__ == "__main__":

    mat = [[3, 2, 1],
           [6, 5, 4],
           [7, 8, 9]]
    N = len(mat)
    M = len(mat[0])

    # Stores bitwise XOR of
    # all elements on each
    # possible path
    xorValue = 0
    print(printMaxXOR(mat, N - 1,
                      M - 1,
                      xorValue))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement the
// above approach
using System;
class GFG{

public static int printMaxXOR(int[,] mat,
                              int i, int j,
                              int xorValue)
{
  // Base case
  if (i == 0 && j == 0)
  {
    return mat[i,j] ^
           xorValue;
  }

  // Base case
  if (i == 0)
  {
    // Stores maximum XOR value
    // by selecting path from (i, j)
    // to (i, j - 1)
    return printMaxXOR(mat, i,
                       j - 1,
                       mat[i,j] ^
                       xorValue);
  }

  if (j == 0)
  {
    // Stores maximum XOR value
    // by selecting path from (i, j)
    // to (i - 1, j)
    return printMaxXOR(mat,
                       i - 1, j,
                       mat[i,j] ^
                       xorValue);
  }

  // Stores maximum XOR value
  // by selecting path from (i, j)
  // to (i - 1, j)
  int X = printMaxXOR(mat,
                      i - 1, j,
                      mat[i,j] ^
                      xorValue);

  // Stores maximum XOR value
  // by selecting path from (i, j)
  // to (i, j - 1)
  int Y = printMaxXOR(mat,
                      i, j - 1,
                      mat[i,j] ^
                      xorValue);

  return Math.Max(X, Y);
}

// Driver Code
public static void Main(String[] args)
{
  int[,] mat = {{3, 2, 1},
                {6, 5, 4}, 
                {7, 8, 9}};
  int N = mat.GetLength(0);
  int M = mat.GetLength(1);

  // Stores bitwise XOR of
  // all elements on each
  // possible path
  int xorValue = 0;
  Console.WriteLine(printMaxXOR(mat, N - 1,
                                M - 1,
                                xorValue));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

function printMaxXOR(mat, i, j, xorValue)
    {
        // Base case
        if (i == 0 && j == 0)
        {
            return mat[i][j] ^ xorValue;
        }

        // Base case
        if (i == 0) {

            // Stores maximum XOR value
            // by selecting path from (i, j)
            // to (i, j - 1)
            return printMaxXOR(mat, i,
                               j - 1,
                               mat[i][j] ^ xorValue);
        }

        if (j == 0) {

            // Stores maximum XOR value
            // by selecting path from (i, j)
            // to (i - 1, j)
            return printMaxXOR(mat,
                               i - 1, j,
                               mat[i][j] ^ xorValue);
        }

        // Stores maximum XOR value
        // by selecting path from (i, j)
        // to (i - 1, j)
        let X = printMaxXOR(mat,
                            i - 1, j,
                            mat[i][j] ^ xorValue);

        // Stores maximum XOR value
        // by selecting path from (i, j)
        // to (i, j - 1)
        let Y = printMaxXOR(mat,
                            i, j - 1,
                            mat[i][j] ^ xorValue);

        return Math.max(X, Y);
    }

    // Driver Code

       let mat
            = [[ 3, 2, 1 ],
               [ 6, 5, 4 ],
               [ 7, 8, 9 ]];
        let N = mat.length;
        let M = mat[0].length;

        // Stores bitwise XOR of
        // all elements on each possible path
        let xorValue = 0;
        document.write(
            printMaxXOR(mat, N - 1, M - 1, xorValue));

</script>
```

**Output**

```
13
```

**时间复杂度:**O(2<sup>N</sup>)
T5】辅助空间: O(1)

**高效途径**:上述途径可以利用动态规划进行优化。dp 二维数组存储 maxxor 值，我们可以得到该行和该列的值。

*   DP[I][j]= max(DP[I-1][j]^ mat[I][j]，dp[i][j-1]^mat[i][j])
*   最终结果存储在 dp[n-1][m-1]中
*   dp[i][j]=maxxor，直到第 I 行和第 jth 列

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define N 3
#define M 3

int printMaxXOR(int mat[][N],
                int n, int m)
{
  int dp[n + 2][m + 2];

  // Initialise dp 1st row
  // and 1st column
  for (int i = 0; i < n; i++)
    dp[i][0] = ((i - 1 >= 0) ?
                 dp[i - 1][0] : 0) ^
                 mat[i][0];

  for (int j = 0; j < m; j++)
    dp[0][j] = ((j - 1 >= 0) ?
                 dp[0][j - 1] : 0) ^
                 mat[0][j];

  // d[i][j] =maxXOr value you can
  //  get till ith row and jth column
  for (int i = 1; i < n; i++)
  {
    for (int j = 1; j < m; j++)
    {
      // Find the maximum value You
      // can get from the top (i-1,j)
      // and left (i,j-1)
      int X = mat[i][j] ^
              dp[i - 1][j];
      int Y = mat[i][j] ^
              dp[i][j - 1];
      dp[i][j] = max(X, Y);
    }
  }

  // Return the maximum
  // Xorvalue
  return dp[n - 1][m - 1];
}

// Driver Code
int main()
{
  int mat[M][N] = {{3, 2, 1},
                   {6, 5, 4},
                   {7, 8, 9}};

  // Stores bitwise XOR of
  // all elements on each
  // possible path
  int xorValue = 0;
  cout << (printMaxXOR(mat,
                       N, M));
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
class GFG {
    public static int printMaxXOR(int[][] mat,
                                  int n, int m)
    {
        int dp[][] = new int[n + 2][m + 2];

        // Initialise dp 1st row and 1st column
        for (int i = 0; i < n; i++)
            dp[i][0] = ((i - 1 >= 0)
                       ? dp[i - 1][0] : 0)
                       ^ mat[i][0];
        for (int j = 0; j < m; j++)
            dp[0][j] = ((j - 1 >= 0)
                       ? dp[0][j - 1] : 0)
                       ^ mat[0][j];

        // d[i][j] =maxXOr value you can
        //  get till ith row and jth column
        for (int i = 1; i < n; i++)
        {
            for (int j = 1; j < m; j++)
            {
                // Find the maximum value You
                // can get from the top (i-1,j)
                // and left (i,j-1)
                int X = mat[i][j] ^ dp[i - 1][j];
                int Y = mat[i][j] ^ dp[i][j - 1];
                dp[i][j] = Math.max(X, Y);
            }
        }
        // Return the maximum Xorvalue
        return dp[n - 1][m - 1];
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[][] mat
            = { { 3, 2, 1 },
               { 6, 5, 4 },
               { 7, 8, 9 } };
        int N = mat.length;
        int M = mat[0].length;

        // Stores bitwise XOR of
        // all elements on each possible path
        int xorValue = 0;
        System.out.println(printMaxXOR(mat, N, M));
    }
    // This code is contributed by hemanth gadarla
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
def printMaxXOR(mat, n, m):

    dp = [[0 for i in range(m+2)]
             for j in range(n+2)];

    # Initialise dp 1st row and
    # 1st column
    for i in range(n):
        if((i - 1) >= 0):
            dp[i][0] = (dp[i - 1][0] ^
                        mat[i][0]);
        else:
            dp[i][0] =  0 ^ mat[i][0];

    for j in range(m):
        if((j - 1) >= 0):
            dp[0][j] = (dp[0][j - 1] ^
                        mat[0][j]);
        else:
            dp[0][j] = 0 ^ mat[0][j];

    # d[i][j] = maxXOr value you can
    # get till ith row and jth column
    for i in range(1, n):
        for j in range(1, m):

            # Find the maximum value You
            # can get from the top (i-1,j)
            # and left (i,j-1)
            X = (mat[i][j] ^
                 dp[i - 1][j]);
            Y = (mat[i][j] ^
                 dp[i][j - 1]);
            dp[i][j] = max(X, Y);

    # Return the maximum
    # Xorvalue
    return dp[n - 1][m - 1];

# Driver Code
if __name__ == '__main__':

    mat = [[3, 2, 1],
           [6, 5, 4],
           [7, 8, 9]];
    N = len(mat);
    M = len(mat[0]);

    # Stores bitwise XOR of
    # all elements on each
    # possible path
    xorValue = 0;
    print(printMaxXOR(mat, N, M));

# This code is contributed by gauravrajput1
```

## C#

```
// C# Program for the
// above approach
using System;
class GFG{

public static int printMaxXOR(int[,] mat,
                              int n, int m)
{
  int [,]dp = new int[n + 2, m + 2];

  // Initialise dp 1st row and
  // 1st column
  for (int i = 0; i < n; i++)
    dp[i, 0] = ((i - 1 >= 0) ?
                 dp[i - 1, 0] : 0) ^
                 mat[i, 0];

  for (int j = 0; j < m; j++)
    dp[0, j] = ((j - 1 >= 0) ?
                 dp[0, j - 1] : 0) ^
                 mat[0, j];

  // d[i,j] =maxXOr value you can
  //  get till ith row and jth column
  for (int i = 1; i < n; i++)
  {
    for (int j = 1; j < m; j++)
    {
      // Find the maximum value You
      // can get from the top (i-1,j)
      // and left (i,j-1)
      int X = mat[i, j] ^ dp[i - 1, j];
      int Y = mat[i, j] ^ dp[i, j - 1];
      dp[i, j] = Math.Max(X, Y);
    }
  }
  // Return the maximum Xorvalue
  return dp[n - 1, m - 1];
}

// Driver Code
public static void Main(String[] args)
{
  int[,] mat = {{3, 2, 1},
                {6, 5, 4},
                {7, 8, 9}};
  int N = mat.GetLength(0);
  int M = mat.GetLength(1);

  // Stores bitwise XOR of
  // all elements on each
  // possible path
  int xorValue = 0;
  Console.WriteLine(printMaxXOR(mat,
                                N, M));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

N = 3;
M = 3;

function printMaxXOR(mat, n, m)
{
//  var dp[n + 2][m + 2];
  var dp = new Array(n+2).fill(0).map(item =>(new Array(m+2).fill(0)));

  // Initialise dp 1st row
  // and 1st column
  for (var i = 0; i < n; i++)
    dp[i][0] = ((i - 1 >= 0) ? dp[i - 1][0] : 0) ^ mat[i][0];

  for (var j = 0; j < m; j++)
    dp[0][j] = ((j - 1 >= 0) ? dp[0][j - 1] : 0) ^ mat[0][j];

  // d[i][j] =maxXOr value you can
  //  get till ith row and jth column
  for (var i = 1; i < n; i++)
  {
    for (var j = 1; j < m; j++)
    {
      // Find the maximum value You
      // can get from the top (i-1,j)
      // and left (i,j-1)
      var X = mat[i][j] ^ dp[i - 1][j];
      var Y = mat[i][j] ^ dp[i][j - 1];
      dp[i][j] = Math.max(X, Y);
    }
  }

  // Return the maximum
  // Xorvalue
  return dp[n - 1][m - 1];
}

 var mat = [[3, 2, 1],
            [6, 5, 4],
            [7, 8, 9]];

  // Stores bitwise XOR of
  // all elements on each
  // possible path
  var xorValue = 0;
  document.write(printMaxXOR(mat, N, M));

//This code is contributed by SoumikMondal
</script>
```

**Output**

```
13
```

**时间复杂度:**O(N * M)
T3】辅助空间复杂度: O(N*M)