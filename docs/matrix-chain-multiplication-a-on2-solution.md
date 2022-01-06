# 矩阵链乘法(A O(N^2)解)

> 原文:[https://www . geesforgeks . org/matrix-chain-乘法-a-on2-solution/](https://www.geeksforgeeks.org/matrix-chain-multiplication-a-on2-solution/)

给定一系列矩阵，找到将这些矩阵相乘的最有效方法。问题不在于实际执行乘法，而仅仅在于决定以何种顺序执行乘法。
我们有很多选择来乘法矩阵链，因为矩阵乘法是关联的。换句话说，无论我们如何给产品加上括号，结果都是一样的。例如，如果我们有四个矩阵 A、B、C 和 D，我们就会有:

```
    (ABC)D = (AB)(CD) = A(BCD) = ....
```

然而，我们给乘积加括号的顺序会影响计算乘积所需的简单算术运算的次数或效率。例如，假设 A 是 10 × 30 矩阵，B 是 30 × 5 矩阵，C 是 5 × 60 矩阵。然后，

```
    (AB)C = (10×30×5) + (10×5×60) = 1500 + 3000 = 4500 operations
    A(BC) = (30×5×60) + (10×30×60) = 9000 + 18000 = 27000 operations.
```

显然，第一个括号需要较少的操作次数。
*给定一个表示矩阵链的数组 p[]，使得矩阵 Ai 的维数为 p[i-1] x p[i]。我们需要编写一个 MatrixChainOrder()函数，该函数应该返回乘法链所需的最小乘法次数。*T3】

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

我们已经讨论了矩阵链乘法问题的 O(n^3 解。
**注意:下图解决方案在很多情况下都不起作用。例如:对于输入{2，40，2，40，5}，正确答案是 580 但是这个方法返回 720**
还有另一个类似的方法来解决这个问题。更直观和递归的方法。

> 假设有以下可用方法
> 最小成本(M2 M1)—>返回矩阵 M1 和 M2 相乘的最小成本
> 然后，对于任何矩阵的链式乘积，如，
> M <sub>1</sub> 。M <sub>2</sub> 。M <sub>3</sub> 。M <sub>4</sub> …M <sub>n</sub>
> 链条最小成本= min(minCost(M <sub>1</sub> ，M <sub>2</sub> )。M<sub>3</sub>……M<sub>n</sub>、闵成本(M <sub>1</sub> 。M <sub>2</sub> ..M <sub>n-1</sub> ，M<sub>n</sub>)
> 现在我们有两个子链(子问题):
> M <sub>2</sub> 。M<sub>3</sub>…M<sub>n</sub>T38】M<sub>1</sub>。M <sub>2</sub> ..M <sub>n-1</sub>

## C++

```
// CPP program to implement optimized matrix chain multiplication problem.
#include<iostream>
using namespace std;

// Matrix Mi has dimension p[i-1] x p[i] for i = 1..n
int MatrixChainOrder(int p[], int n)
{

    /* For simplicity of the program, one extra row and one extra column are allocated in
    dp[][]. 0th row and 0th column of dp[][] are not used */
    int dp[n][n];

    /* dp[i, j] = Minimum number of scalar multiplications needed to compute the matrix M[i]M[i+1]...M[j]
                = M[i..j] where dimension of M[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (int i=1; i<n; i++)
        dp[i][i] = 0;

    // Simply following above recursive formula.
    for (int L=1; L<n-1; L++)
    for (int i=1; i<n-L; i++)    
        dp[i][i+L] = min(dp[i+1][i+L] + p[i-1]*p[i]*p[i+L],
                    dp[i][i+L-1] + p[i-1]*p[i+L-1]*p[i+L]);    

    return dp[1][n-1];
}

// Driver code
int main()
{
    int arr[] = {10, 20, 30, 40, 30} ;
    int size = sizeof(arr)/sizeof(arr[0]);

    printf("Minimum number of multiplications is %d ",
                    MatrixChainOrder(arr, size));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement optimized matrix chain multiplication problem.
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{
// Matrix Mi has dimension p[i-1] x p[i] for i = 1..n
static int MatrixChainOrder(int p[], int n)
{

    /* For simplicity of the program, one extra row and one extra column are
     allocated in dp[][]. 0th row and 0th column of dp[][] are not used */
    int [][]dp=new int[n][n];

    /* dp[i, j] = Minimum number of scalar multiplications needed to compute the matrix M[i]M[i+1]...M[j]
                = M[i..j] where dimension of M[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (int i=1; i<n; i++)
        dp[i][i] = 0;

    // Simply following above recursive formula.
    for (int L=1; L<n-1; L++)
    for (int i=1; i<n-L; i++)    
        dp[i][i+L] = Math.min(dp[i+1][i+L] + p[i-1]*p[i]*p[i+L],
                    dp[i][i+L-1] + p[i-1]*p[i+L-1]*p[i+L]);    

    return dp[1][n-1];
}

// Driver code
public static void main(String args[])
{
    int arr[] = {10, 20, 30, 40, 30} ;
    int size = arr.length;

    System.out.print("Minimum number of multiplications is "+
                    MatrixChainOrder(arr, size));

}
}
```

## 蟒蛇 3

```
# Python3 program to implement optimized
# matrix chain multiplication problem.

# Matrix Mi has dimension
# p[i-1] x p[i] for i = 1..n
def MatrixChainOrder(p, n):

    # For simplicity of the program, one
    # extra row and one extra column are
    # allocated in dp[][]. 0th row and
    # 0th column of dp[][] are not used
    dp = [[0 for i in range(n)]
             for i in range(n)]

    # dp[i, j] = Minimum number of scalar
    # multiplications needed to compute
    # the matrix M[i]M[i+1]...M[j] = M[i..j]
    # where dimension of M[i] is p[i-1] x p[i]

    # cost is zero when multiplying one matrix.
    for i in range(1, n):
        dp[i][i] = 0

    # Simply following above recursive formula.
    for L in range(1, n - 1):
        for i in range(n - L):
            dp[i][i + L] = min(dp[i + 1][i + L] +
                                p[i - 1] * p[i] * p[i + L],
                               dp[i][i + L - 1] +
                                p[i - 1] * p[i + L - 1] * p[i + L])

    return dp[1][n - 1]

# Driver code
arr = [10, 20, 30, 40, 30]
size = len(arr)
print("Minimum number of multiplications is",
                 MatrixChainOrder(arr, size))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# program to implement optimized
// matrix chain multiplication problem.
using System;

class GFG
{
// Matrix Mi has dimension
// p[i-1] x p[i] for i = 1..n
static int MatrixChainOrder(int []p, int n)
{

    /* For simplicity of the program,
       one extra row and one extra
       column are allocated in dp[][].
       0th row and 0th column of dp[][]
       are not used */
    int [,]dp = new int[n, n];

    /* dp[i, j] = Minimum number of scalar
       multiplications needed to compute
       the matrix M[i]M[i+1]...M[j] = M[i..j]
       where dimension of M[i] is p[i-1] x p[i] */

    // cost is zero when multiplying
    // one matrix.
    for (int i = 1; i < n; i++)
        dp[i, i] = 0;

    // Simply following above
    // recursive formula.
    for (int L = 1; L < n - 1; L++)
    for (int i = 1; i < n - L; i++)    
        dp[i, i + L] = Math.Min(dp[i + 1, i + L] +
                                 p[i - 1] * p[i] * p[i + L],
                                dp[i, i + L - 1] + p[i - 1] *
                                 p[i + L - 1] * p[i + L]);

    return dp[1, n - 1];
}

// Driver code
public static void Main()
{
    int []arr = {10, 20, 30, 40, 30} ;
    int size = arr.Length;

    Console.WriteLine("Minimum number of multiplications is " +
                                  MatrixChainOrder(arr, size));
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement optimized
// matrix chain multiplication problem.

// Matrix Mi has dimension
// p[i-1] x p[i] for i = 1..n
function MatrixChainOrder($p, $n)
{

    /* For simplicity of the program,
    one extra row and one extra column
    are allocated in dp[][]. 0th row
    and 0th column of dp[][] are not used */
    $dp = array();

    /* dp[i, j] = Minimum number of scalar
                  multiplications needed to
                  compute the matrix M[i]M[i+1]...M[j]
                = M[i..j] where dimension of M[i]
                  is p[i-1] x p[i] */

    // cost is zero when multiplying
    // one matrix.
    for ($i=1; $i<$n; $i++)
        $dp[$i][$i] = 0;

    // Simply following above
    // recursive formula.
    for ($L = 1; $L < $n - 1; $L++)
    for ($i = 1; $i < $n - $L; $i++)
        $dp[$i][$i + $L] = min($dp[$i + 1][$i + $L] + $p[$i - 1] *
                               $p[$i] * $p[$i + $L],
                               $dp[$i][$i + $L - 1] + $p[$i - 1] *
                               $p[$i + $L - 1] * $p[$i + $L]);

    return $dp[1][$n - 1];
}

// Driver code
$arr = array(10, 20, 30, 40, 30) ;
$size = sizeof($arr);

echo "Minimum number of multiplications is ".
               MatrixChainOrder($arr, $size);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to implement optimized
// matrix chain multiplication problem.

// Matrix Mi has dimension p[i-1] x p[i] for i = 1..n
function MatrixChainOrder(p, n)
{

    /* For simplicity of the program, one extra row
    and one extra column are allocated in
    dp[][]. 0th row and 0th column of dp[][] are not used */
    var dp = Array.from(Array(n), ()=> Array(n));

    /* dp[i, j] = Minimum number of scalar multiplications
    needed to compute the matrix M[i]M[i+1]...M[j]
                = M[i..j] where dimension
                of M[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (var i=1; i<n; i++)
        dp[i][i] = 0;

    // Simply following above recursive formula.
    for (var L=1; L<n-1; L++)
    for (var i=1; i<n-L; i++)    
        dp[i][i+L] = Math.min(dp[i+1][i+L] +
        p[i-1]*p[i]*p[i+L],
        dp[i][i+L-1] + p[i-1]*p[i+L-1]*p[i+L]);    

    return dp[1][n-1];
}

// Driver code
var arr = [10, 20, 30, 40, 30];
var size = arr.length;
document.write("Minimum number of multiplications is  "+
                MatrixChainOrder(arr, size));

</script>
```

**Output:** 

```
Minimum number of multiplications is 30000
```

感谢 [Rishi_Lazy](https://auth.geeksforgeeks.org/user/Rishi_Lazy) 提供上述优化解决方案。
**时间复杂度:** O(n <sup>2</sup> )
[**矩阵链乘法中打印括号**](https://www.geeksforgeeks.org/printing-matrix-chain-multiplication-a-space-optimized-solution/)