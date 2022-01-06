# 矩阵链乘法| DP-8

> 原文:[https://www . geesforgeks . org/matrix-chain-乘法-dp-8/](https://www.geeksforgeeks.org/matrix-chain-multiplication-dp-8/)

给定一系列矩阵，找到将这些矩阵相乘的最有效方法。问题不在于实际执行乘法，而仅仅在于决定以何种顺序执行乘法。
我们有很多选择来乘法矩阵链，因为矩阵乘法是关联的。换句话说，无论我们如何给产品加上括号，结果都是一样的。例如，如果我们有四个矩阵 A、B、C 和 D，我们会有:

```
(ABC)D = (AB)(CD) = A(BCD) = ....
```

然而，我们给乘积加括号的顺序会影响计算乘积所需的简单算术运算的次数，或者效率。例如，假设 A 是 10 × 30 矩阵，B 是 30 × 5 矩阵，C 是 5 × 60 矩阵。然后，

```
(AB)C = (10×30×5) + (10×5×60) = 1500 + 3000 = 4500 operations
A(BC) = (30×5×60) + (10×30×60) = 9000 + 18000 = 27000 operations.
```

显然，第一个括号需要较少的操作次数。
*给定一个表示矩阵链的数组 p[]，使得矩阵 Ai 的维数为 p[i-1] x p[i]。我们需要编写一个 MatrixChainOrder()函数，该函数应该返回乘法链所需的最小乘法次数。*

```
Input: p[] = {40, 20, 30, 10, 30}   
Output: 26000 
There are 4 matrices of dimensions 40x20, 20x30, 30x10 and 10x30.
Let the input 4 matrices be A, B, C and D.  The minimum number of 
multiplications are obtained by putting parenthesis in following way
(A(BC))D --> 20*30*10 + 40*20*10 + 40*10*30

Input: p[] = {10, 20, 30, 40, 30} 
Output: 30000 
There are 4 matrices of dimensions 10x20, 20x30, 30x40 and 40x30\. 
Let the input 4 matrices be A, B, C and D.  The minimum number of 
multiplications are obtained by putting parenthesis in following way
((AB)C)D --> 10*20*30 + 10*30*40 + 10*40*30

Input: p[] = {10, 20, 30} 
Output: 6000  
There are only two matrices of dimensions 10x20 and 20x30\. So there 
is only one way to multiply the matrices, cost of which is 10*20*30
```

**1)最优子结构:**
一个简单的解决方案是在所有可能的地方放置括号，计算每个放置的成本并返回最小值。在 n 大小的矩阵链中，我们可以以 n-1 种方式放置第一组括号。例如，如果给定的链是 4 个矩阵。设链为 ABCD，则有 3 种方式放置第一组括号外侧:(A)(BCD)、(AB)(CD)和(ABC)(D)。所以当我们放置一组括号时，我们把问题分成更小的子问题。因此，该问题具有最优子结构性质，易于用递归方法求解。
乘法一个大小为 n 的链所需的最小乘法次数=所有 n-1 个布局中的最小值(这些布局产生较小大小的子问题)

**2)重叠子问题**
跟随是一个递归实现，它简单地跟随上面的最优子结构属性。

下面是上述想法的实现:

## C++

```
/* A naive recursive implementation that simply
follows the above optimal substructure property */
#include <bits/stdc++.h>
using namespace std;

// Matrix Ai has dimension p[i-1] x p[i]
// for i = 1..n
int MatrixChainOrder(int p[], int i, int j)
{
    if (i == j)
        return 0;
    int k;
    int min = INT_MAX;
    int count;

    // place parenthesis at different places
    // between first and last matrix, recursively
    // calculate count of multiplications for
    // each parenthesis placement and return the
    // minimum count
    for (k = i; k < j; k++)
    {
        count = MatrixChainOrder(p, i, k)
                + MatrixChainOrder(p, k + 1, j)
                + p[i - 1] * p[k] * p[j];

        if (count < min)
            min = count;
    }

    // Return minimum count
    return min;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Minimum number of multiplications is "
         << MatrixChainOrder(arr, 1, n - 1);
}

// This code is contributed by Shivi_Aggarwal
```

## C

```
/* A naive recursive implementation that simply
  follows the above optimal substructure property */
#include <limits.h>
#include <stdio.h>

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
int MatrixChainOrder(int p[], int i, int j)
{
    if (i == j)
        return 0;
    int k;
    int min = INT_MAX;
    int count;

    // place parenthesis at different places between first
    // and last matrix, recursively calculate count of
    // multiplications for each parenthesis placement and
    // return the minimum count
    for (k = i; k < j; k++)
    {
        count = MatrixChainOrder(p, i, k)
                + MatrixChainOrder(p, k + 1, j)
                + p[i - 1] * p[k] * p[j];

        if (count < min)
            min = count;
    }

    // Return minimum count
    return min;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Minimum number of multiplications is %d ",
           MatrixChainOrder(arr, 1, n - 1));

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A naive recursive implementation that simply follows
   the above optimal substructure property */
class MatrixChainMultiplication {
    // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
    static int MatrixChainOrder(int p[], int i, int j)
    {
        if (i == j)
            return 0;

        int min = Integer.MAX_VALUE;

        // place parenthesis at different places between
        // first and last matrix, recursively calculate
        // count of multiplications for each parenthesis
        // placement and return the minimum count
        for (int k = i; k < j; k++)
        {
            int count = MatrixChainOrder(p, i, k)
                        + MatrixChainOrder(p, k + 1, j)
                        + p[i - 1] * p[k] * p[j];

            if (count < min)
                min = count;
        }

        // Return minimum count
        return min;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = new int[] { 1, 2, 3, 4, 3 };
        int n = arr.length;

        System.out.println(
            "Minimum number of multiplications is "
            + MatrixChainOrder(arr, 1, n - 1));
    }
}
/* This code is contributed by Rajat Mishra*/
```

## 蟒蛇 3

```
# A naive recursive implementation that
# simply follows the above optimal
# substructure property
import sys

# Matrix A[i] has dimension p[i-1] x p[i]
# for i = 1..n

def MatrixChainOrder(p, i, j):

    if i == j:
        return 0

    _min = sys.maxsize

    # place parenthesis at different places
    # between first and last matrix,
    # recursively calculate count of
    # multiplications for each parenthesis
    # placement and return the minimum count
    for k in range(i, j):

        count = (MatrixChainOrder(p, i, k)
                 + MatrixChainOrder(p, k + 1, j)
                 + p[i-1] * p[k] * p[j])

        if count < _min:
            _min = count

    # Return minimum count
    return _min

# Driver code
arr = [1, 2, 3, 4, 3]
n = len(arr)

print("Minimum number of multiplications is ",
      MatrixChainOrder(arr, 1, n-1))

# This code is contributed by Aryan Garg
```

## C#

```
/* C# code for naive recursive implementation
that simply follows the above optimal
substructure property */
using System;

class GFG {

    // Matrix Ai has dimension p[i-1] x p[i]
    // for i = 1..n
    static int MatrixChainOrder(int[] p, int i, int j)
    {

        if (i == j)
            return 0;

        int min = int.MaxValue;

        // place parenthesis at different places
        // between first and last matrix, recursively
        // calculate count of multiplications for each
        // parenthesis placement and return the
        // minimum count
        for (int k = i; k < j; k++)
        {
            int count = MatrixChainOrder(p, i, k)
                        + MatrixChainOrder(p, k + 1, j)
                        + p[i - 1] * p[k] * p[j];

            if (count < min)
                min = count;
        }

        // Return minimum count
        return min;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = new int[] { 1, 2, 3, 4, 3 };
        int n = arr.Length;

        Console.Write(
            "Minimum number of multiplications is "
            + MatrixChainOrder(arr, 1, n - 1));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive recursive implementation
// that simply follows the above
// optimal substructure property

// Matrix Ai has dimension
// p[i-1] x p[i] for i = 1..n
function MatrixChainOrder(&$p, $i, $j)
{
    if($i == $j)
        return 0;
    $min = PHP_INT_MAX;

    // place parenthesis at different places
    // between first and last matrix, recursively
    // calculate count of multiplications for
    // each parenthesis placement and return
    // the minimum count
    for ($k = $i; $k < $j; $k++)
    {
        $count = MatrixChainOrder($p, $i, $k) +
                 MatrixChainOrder($p, $k + 1, $j) +
                                  $p[$i - 1] *
                                  $p[$k] * $p[$j];

        if ($count < $min)
            $min = $count;
    }

    // Return minimum count
    return $min;
}

// Driver Code
$arr = array(1, 2, 3, 4, 3);
$n = sizeof($arr);

echo "Minimum number of multiplications is " .
      MatrixChainOrder($arr, 1, $n - 1);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

/* A naive recursive implementation that simply follows
   the above optimal substructure property */

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
function MatrixChainOrder(p , i , j)
{
    if (i == j)
        return 0;

    var min = Number.MAX_VALUE;

    // place parenthesis at different places between
    // first and last matrix, recursively calculate
    // count of multiplications for each parenthesis
    // placement and return the minimum count
    var k=0;
    for (k = i; k < j; k++)
    {
        var count = MatrixChainOrder(p, i, k)
                    + MatrixChainOrder(p, k + 1, j)
                    + p[i - 1] * p[k] * p[j];

        if (count < min)
            min = count;
    }

    // Return minimum count
    return min;
}

// Driver code
var arr = [ 1, 2, 3, 4, 3 ];
var n = arr.length;

document.write(
    "Minimum number of multiplications is "
    + MatrixChainOrder(arr, 1, n - 1));

// This code contributed by shikhasingrajput

</script>
```

**Output**

```
Minimum number of multiplications is 30
```

上述简单递归方法的时间复杂度是指数级的。需要注意的是，上面的函数一次又一次地计算相同的子问题。大小为 4 的矩阵链见下面的递归树。函数 MatrixChainOrder(p，3，4)被调用两次。我们可以看到有很多子问题被多次调用。

![](img/43369877d26dce811845c2be9f084649.png)

由于相同的子问题被再次调用，这个问题具有重叠子问题的性质。所以矩阵链乘法问题同时具有动态规划问题的两个性质(见[这个](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[这个](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/))。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)一样，相同子问题的重新计算可以通过以自下而上的方式构建临时数组 m[][]来避免。

**动态规划解**
下面是使用动态规划[实现矩阵链乘法问题(制表 vs 记忆)](https://www.geeksforgeeks.org/tabulation-vs-memoization/)

**使用记忆化–**

## C++

```
// C++ program using memoization
#include <bits/stdc++.h>
using namespace std;
int dp[100][100];

// Function for matrix chain multiplication
int matrixChainMemoised(int* p, int i, int j)
{
    if (i == j)
    {
        return 0;
    }
    if (dp[i][j] != -1)
    {
        return dp[i][j];
    }
    dp[i][j] = INT_MAX;
    for (int k = i; k < j; k++)
    {
        dp[i][j] = min(
            dp[i][j], matrixChainMemoised(p, i, k)
                     + matrixChainMemoised(p, k + 1, j)
                       + p[i - 1] * p[k] * p[j]);
    }
    return dp[i][j];
}
int MatrixChainOrder(int* p, int n)
{
    int i = 1, j = n - 1;
    return matrixChainMemoised(p, i, j);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    memset(dp, -1, sizeof dp);

    cout << "Minimum number of multiplications is "
         << MatrixChainOrder(arr, n);
}

// This code is contributed by Sumit_Yadav
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program using memoization
import java.io.*;
import java.util.*;
class GFG
{

  static int[][] dp = new int[100][100];

  // Function for matrix chain multiplication
  static int matrixChainMemoised(int[] p, int i, int j)
  {
    if (i == j) 
    {
      return 0;
    }
    if (dp[i][j] != -1) 
    {
      return dp[i][j];
    }
    dp[i][j] = Integer.MAX_VALUE;
    for (int k = i; k < j; k++) 
    {
      dp[i][j] = Math.min(
        dp[i][j], matrixChainMemoised(p, i, k)
        + matrixChainMemoised(p, k + 1, j)
        + p[i - 1] * p[k] * p[j]);
    }
    return dp[i][j];
  }

  static int MatrixChainOrder(int[] p, int n)
  {
    int i = 1, j = n - 1;
    return matrixChainMemoised(p, i, j);
  }

  // Driver Code
  public static void main (String[] args)
  {

    int arr[] = { 1, 2, 3, 4 };
    int n= arr.length;

    for (int[] row : dp)
      Arrays.fill(row, -1);

    System.out.println("Minimum number of multiplications is " + MatrixChainOrder(arr, n));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python program using memoization
import sys
dp = [[-1 for i in range(100)] for j in range(100)]

# Function for matrix chain multiplication
def matrixChainMemoised(p, i, j):
    if(i == j):
        return 0

    if(dp[i][j] != -1):
        return dp[i][j]

    dp[i][j] = sys.maxsize

    for k in range(i,j):
        dp[i][j] = min(dp[i][j], matrixChainMemoised(p, i, k) + matrixChainMemoised(p, k + 1, j)+ p[i - 1] * p[k] * p[j])

    return dp[i][j]

def MatrixChainOrder(p,n):
    i = 1
    j = n - 1   
    return matrixChainMemoised(p, i, j)

# Driver Code
arr = [1, 2, 3, 4]
n = len(arr)
print("Minimum number of multiplications is",MatrixChainOrder(arr, n))

# This code is contributed by rag2127
```

## C#

```
// C# program using memoization
using System;
class GFG
{

    static int[,] dp = new int[100, 100];

  // Function for matrix chain multiplication
  static int matrixChainMemoised(int[] p, int i, int j)
  {
    if (i == j) 
    {
      return 0;
    }
    if (dp[i, j] != -1) 
    {
      return dp[i, j];
    }
    dp[i, j] = Int32.MaxValue;
    for (int k = i; k < j; k++) 
    {
      dp[i, j] = Math.Min(
        dp[i, j], matrixChainMemoised(p, i, k)
        + matrixChainMemoised(p, k + 1, j)
        + p[i - 1] * p[k] * p[j]);
    }
    return dp[i,j];
  }

  static int MatrixChainOrder(int[] p, int n)
  {
    int i = 1, j = n - 1;
    return matrixChainMemoised(p, i, j);
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 2, 3, 4 };
    int n = arr.Length;

    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < 100; j++)
        {
            dp[i, j] = -1;
        }
    }

    Console.WriteLine("Minimum number of multiplications is " +
                      MatrixChainOrder(arr, n));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program using memoization
let dp = new Array(100);
for(var i = 0; i < dp.length; i++)
{
    dp[i] = new Array(2);
}

// Function for matrix chain multiplication
function matrixChainMemoised(p, i, j)
{
    if (i == j) 
    {
        return 0;
    }
    if (dp[i][j] != -1) 
    {
        return dp[i][j];
    }

    dp[i][j] = Number.MAX_VALUE;
    for(let k = i; k < j; k++) 
    {
        dp[i][j] = Math.min(
            dp[i][j], matrixChainMemoised(p, i, k) +
                      matrixChainMemoised(p, k + 1, j) +
                      p[i - 1] * p[k] * p[j]);
    }
    return dp[i][j];
}

function MatrixChainOrder(p, n)
{
    let i = 1, j = n - 1;
    return matrixChainMemoised(p, i, j);
}

// Driver code
let arr = [ 1, 2, 3, 4 ];
let n = arr.length;

for(var i = 0; i < dp.length; i++)
{
    for(var j = 0; j < dp.length; j++)
    {
        dp[i][j] = -1;
    }
}

document.write("Minimum number of multiplications is " +
               MatrixChainOrder(arr, n));

// This code is contributed by target_2

</script>
```

**Output**

```
Minimum number of multiplications is 18
```

**使用列表–**

## C++

```
// See the Cormen book for details of the
// following algorithm
#include <bits/stdc++.h>
using namespace std;

// Matrix Ai has dimension p[i-1] x p[i]
// for i = 1..n
int MatrixChainOrder(int p[], int n)
{

    /* For simplicity of the program, one
    extra row and one extra column are
    allocated in m[][]. 0th row and 0th
    column of m[][] are not used */
    int m[n][n];

    int i, j, k, L, q;

    /* m[i, j] = Minimum number of scalar
    multiplications needed to compute the
    matrix A[i]A[i+1]...A[j] = A[i..j] where
    dimension of A[i] is p[i-1] x p[i] */

    // cost is zero when multiplying
    // one matrix.
    for (i = 1; i < n; i++)
        m[i][i] = 0;

    // L is chain length.
    for (L = 2; L < n; L++)
    {
        for (i = 1; i < n - L + 1; i++)
        {
            j = i + L - 1;
            m[i][j] = INT_MAX;
            for (k = i; k <= j - 1; k++)
            {
                // q = cost/scalar multiplications
                q = m[i][k] + m[k + 1][j]
                    + p[i - 1] * p[k] * p[j];
                if (q < m[i][j])
                    m[i][j] = q;
            }
        }
    }

    return m[1][n - 1];
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << "Minimum number of multiplications is "
         << MatrixChainOrder(arr, size);

    getchar();
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// See the Cormen book for details of the following
// algorithm
#include <limits.h>
#include <stdio.h>

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
int MatrixChainOrder(int p[], int n)
{

    /* For simplicity of the program,
       one extra row and one
       extra column are allocated in m[][]. 
       0th row and 0th
       column of m[][] are not used */
    int m[n][n];

    int i, j, k, L, q;

    /* m[i, j] = Minimum number of
       scalar multiplications
       needed to compute the matrix
       A[i]A[i+1]...A[j] =
       A[i..j] where dimension of A[i]
       is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (i = 1; i < n; i++)
        m[i][i] = 0;

    // L is chain length.
    for (L = 2; L < n; L++) {
        for (i = 1; i < n - L + 1; i++)
        {
            j = i + L - 1;
            m[i][j] = INT_MAX;
            for (k = i; k <= j - 1; k++)
            {
                // q = cost/scalar multiplications
                q = m[i][k] + m[k + 1][j]
                    + p[i - 1] * p[k] * p[j];
                if (q < m[i][j])
                    m[i][j] = q;
            }
        }
    }

    return m[1][n - 1];
}

// Driver  code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int size = sizeof(arr) / sizeof(arr[0]);

    printf("Minimum number of multiplications is %d ",
           MatrixChainOrder(arr, size));

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Dynamic Programming Java implementation of Matrix
// Chain Multiplication.
// See the Cormen book for details of the following
// algorithm
class MatrixChainMultiplication
{

    // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
    static int MatrixChainOrder(int p[], int n)
    {
        /* For simplicity of the
        program, one extra row and
        one extra column are allocated in m[][].  0th row
        and 0th column of m[][] are not used */
        int m[][] = new int[n][n];

        int i, j, k, L, q;

        /* m[i, j] = Minimum number of scalar
        multiplications needed to compute the matrix
        A[i]A[i+1]...A[j] = A[i..j] where
        dimension of A[i] is p[i-1] x p[i] */

        // cost is zero when multiplying one matrix.
        for (i = 1; i < n; i++)
            m[i][i] = 0;

        // L is chain length.
        for (L = 2; L < n; L++)
        {
            for (i = 1; i < n - L + 1; i++)
            {
                j = i + L - 1;
                if (j == n)
                    continue;
                m[i][j] = Integer.MAX_VALUE;
                for (k = i; k <= j - 1; k++)
                {
                    // q = cost/scalar multiplications
                    q = m[i][k] + m[k + 1][j]
                        + p[i - 1] * p[k] * p[j];
                    if (q < m[i][j])
                        m[i][j] = q;
                }
            }
        }

        return m[1][n - 1];
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = new int[] { 1, 2, 3, 4 };
        int size = arr.length;

        System.out.println(
            "Minimum number of multiplications is "
            + MatrixChainOrder(arr, size));
    }
}
/* This code is contributed by Rajat Mishra*/
```

## 计算机编程语言

```
# Dynamic Programming Python implementation of Matrix
# Chain Multiplication. See the Cormen book for details
# of the following algorithm
import sys

# Matrix Ai has dimension p[i-1] x p[i] for i = 1..n

def MatrixChainOrder(p, n):
    # For simplicity of the program,
    # one extra row and one
    # extra column are allocated in m[][]. 
    # 0th row and 0th
    # column of m[][] are not used
    m = [[0 for x in range(n)] for x in range(n)]

    # m[i, j] = Minimum number of scalar
    # multiplications needed
    # to compute the matrix A[i]A[i + 1]...A[j] =
    # A[i..j] where
    # dimension of A[i] is p[i-1] x p[i]

    # cost is zero when multiplying one matrix.
    for i in range(1, n):
        m[i][i] = 0

    # L is chain length.
    for L in range(2, n):
        for i in range(1, n-L + 1):
            j = i + L-1
            m[i][j] = sys.maxint
            for k in range(i, j):

                # q = cost / scalar multiplications
                q = m[i][k] + m[k + 1][j] + p[i-1]*p[k]*p[j]
                if q < m[i][j]:
                    m[i][j] = q

    return m[1][n-1]

# Driver code
arr = [1, 2, 3, 4]
size = len(arr)

print("Minimum number of multiplications is " +
      str(MatrixChainOrder(arr, size)))
# This Code is contributed by Bhavya Jain
```

## C#

```
// Dynamic Programming C# implementation of
// Matrix Chain Multiplication.
// See the Cormen book for details of the
// following algorithm
using System;

class GFG
{

    // Matrix Ai has dimension p[i-1] x p[i]
    // for i = 1..n
    static int MatrixChainOrder(int[] p, int n)
    {

        /* For simplicity of the program, one
        extra row and one extra column are
        allocated in m[][]. 0th row and 0th
        column of m[][] are not used */
        int[, ] m = new int[n, n];

        int i, j, k, L, q;

        /* m[i, j] = Minimum number of scalar
        multiplications needed
        to compute the matrix A[i]A[i+1]...A[j]
        = A[i..j] where dimension of A[i] is
        p[i-1] x p[i] */

        // cost is zero when multiplying
        // one matrix.
        for (i = 1; i < n; i++)
            m[i, i] = 0;

        // L is chain length.
        for (L = 2; L < n; L++)
        {
            for (i = 1; i < n - L + 1; i++)
            {
                j = i + L - 1;
                if (j == n)
                    continue;
                m[i, j] = int.MaxValue;
                for (k = i; k <= j - 1; k++)
                {
                    // q = cost/scalar multiplications
                    q = m[i, k] + m[k + 1, j]
                        + p[i - 1] * p[k] * p[j];
                    if (q < m[i, j])
                        m[i, j] = q;
                }
            }
        }

        return m[1, n - 1];
    }

    // Driver code
    public static void Main()
    {
        int[] arr = new int[] { 1, 2, 3, 4 };
        int size = arr.Length;

        Console.Write("Minimum number of "
                      + "multiplications is "
                      + MatrixChainOrder(arr, size));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Dynamic Programming Python implementation
// of Matrix Chain Multiplication.

// See the Cormen book for details of the
// following algorithm Matrix Ai has
// dimension p[i-1] x p[i] for i = 1..n
function MatrixChainOrder($p, $n)
{
    /* For simplicity of the program, one
    extra row and one extra column are
    allocated in m[][]. 0th row and 0th
    column of m[][] are not used */
    $m[][] = array($n, $n);

    /* m[i, j] = Minimum number of scalar
    multiplications needed to compute the
    matrix A[i]A[i+1]...A[j] = A[i..j] where
    dimension of A[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for ($i = 1; $i < $n; $i++)
        $m[$i][$i] = 0;

    // L is chain length.
    for ($L = 2; $L < $n; $L++)
    {
        for ($i = 1; $i < $n - $L + 1; $i++)
        {
            $j = $i + $L - 1;
            if($j == $n)
                continue;
            $m[$i][$j] = PHP_INT_MAX;
            for ($k = $i; $k <= $j - 1; $k++)
            {
                // q = cost/scalar multiplications
                $q = $m[$i][$k] + $m[$k + 1][$j] +
                     $p[$i - 1] * $p[$k] * $p[$j];
                if ($q < $m[$i][$j])
                    $m[$i][$j] = $q;
            }
        }
    }

    return $m[1][$n-1];
}

// Driver Code
$arr = array(1, 2, 3, 4);
$size = sizeof($arr);

echo"Minimum number of multiplications is ".
              MatrixChainOrder($arr, $size);

// This code is contributed by Mukul Singh
?>
```

## java 描述语言

```
<script>

// Dynamic Programming javascript implementation of Matrix
// Chain Multiplication.
// See the Cormen book for details of the following
// algorithm

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
function MatrixChainOrder(p , n)
{
    /* For simplicity of the
    program, one extra row and
    one extra column are allocated in m.  0th row
    and 0th column of m are not used */
    var m = Array(n).fill(0).map(x => Array(n).fill(0));

    var i, j, k, L, q;

    /* m[i, j] = Minimum number of scalar
    multiplications needed to compute the matrix
    A[i]A[i+1]...A[j] = A[i..j] where
    dimension of A[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (i = 1; i < n; i++)
        m[i][i] = 0;

    // L is chain length.
    for (L = 2; L < n; L++)
    {
        for (i = 1; i < n - L + 1; i++)
        {
            j = i + L - 1;
            if (j == n)
                continue;
            m[i][j] = Number.MAX_VALUE;
            for (k = i; k <= j - 1; k++)
            {
                // q = cost/scalar multiplications
                q = m[i][k] + m[k + 1][j]
                    + p[i - 1] * p[k] * p[j];
                if (q < m[i][j])
                    m[i][j] = q;
            }
        }
    }

    return m[1][n - 1];
}

// Driver code
var arr = [ 1, 2, 3, 4 ];
var size = arr.length;

document.write(
    "Minimum number of multiplications is "
    + MatrixChainOrder(arr, size));

// This code contributed by Princi Singh

</script>
```

**Output**

```
Minimum number of multiplications is 18
```

**时间复杂度:**O(n<sup>3</sup>)
T5】辅助空间: O(n <sup>2</sup>

[矩阵链乘法(一个 O(N^2)解法)](https://www.geeksforgeeks.org/matrix-chain-multiplication-a-on2-solution/)
[**在矩阵链乘法题中打印括号**](https://www.geeksforgeeks.org/printing-brackets-matrix-chain-multiplication-problem/)
如发现有不正确的地方请写评论，或者想分享更多关于以上讨论话题的信息。

**应用程序:**
[带有*和+](https://www.geeksforgeeks.org/minimum-maximum-values-expression/) 的表达式的最小值和最大值

**参考文献:**
[【http://en.wikipedia.org/wiki/Matrix_chain_multiplication】](http://en.wikipedia.org/wiki/Matrix_chain_multiplication)
[http://www . personal . Kent . edu/~ rmuhamma/Algorithms/MyAlgorithms/Dynamic/chainematrixmult . htm](http://www.personal.kent.edu/~rmuhamma/Algorithms/MyAlgorithms/Dynamic/chainMatrixMult.htm)

？list = plqm 7 alhxfysqdk 2 mdfbwedjd 2 svv JH 9p