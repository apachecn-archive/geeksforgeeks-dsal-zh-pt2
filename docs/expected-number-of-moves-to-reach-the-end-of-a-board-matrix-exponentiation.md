# 到达棋盘末端的预期移动次数|矩阵幂运算

> 原文:[https://www . geeksforgeeks . org/预计到达板端的移动次数-矩阵求幂/](https://www.geeksforgeeks.org/expected-number-of-moves-to-reach-the-end-of-a-board-matrix-exponentiation/)

给定一个从 **1** 到 **N** 的长度为 **N** 的线性棋盘，任务是找到到达棋盘的第 **N <sup>第</sup>T9】单元所需的预期移动次数，如果我们从编号为 **1** 的单元开始，在每一步我们掷出一个立方体骰子来决定下一个移动。此外，我们不能超越董事会的界限。**注意**预期的移动次数可以是小数。**

**示例:**

> **输入:** N = 8
> **输出:** 7
> p1 = (1 / 6) | 1 步- > 6 步预计到达终点
> p2 = (1 / 6) | 2 步- > 6 步预计到达终点
> p3 = (1 / 6) | 3 步- > 6 步预计到达终点
> p4 = (1 / 6) | 4 步- > 6 步预计到达终点
> p5 = (1 / 6) | 5 步- > 6 步预计到达终点
> p6 = (1 / 6) | 6 步- > 6 步预计到达终点
> 如果我们相距 7 步，那么我们可以以相等的概率(即 1 / 6)在 1、2、3、4、5、6 步
> 处结束。
> 看上面的模拟更好理解。
> DP[N–1]= DP[7]
> = 1+(DP[1]+DP[2]+DP[3]+DP[4]+DP[5]+DP[6])/6
> = 1+6 = 7
> 
> **输入:**N = 10
> T3】输出: 7.36111

**方法:**基于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的方法已经在之前的帖子中讨论过了。本文将讨论一种更优化的方法来解决这个问题。这个想法是使用一种叫做[矩阵求幂](https://www.geeksforgeeks.org/matrix-exponentiation/)的技术。
我们将 A <sub>n</sub> 定义为到达长度为 **N + 1** 的棋盘末端的预期移动次数。

重复关系将是:

> A<sub>n</sub>= 1+(A<sub>n-1</sub>+A<sub>n-2</sub>+A<sub>n-3</sub>+A<sub>n-4</sub>+A<sub>n-5</sub>+A<sub>n-6</sub>)/6

现在，循环关系需要转换成合适的格式。

> A<sub>n</sub>= 1+(A<sub>n-1</sub>+A<sub>n-2</sub>+A<sub>n-3</sub>+A<sub>n-4</sub>+A<sub>n-5</sub>+A<sub>n-6</sub>)/6(方程式 1)
> A<sub>n-1</sub>= 1+(A<sub>n-2</sub>+A
> 6(公式 2)
> 1 减 2，得到 A<sub>n</sub>= 7 *(A<sub>n-1</sub>)/6 –( A<sub>n-7</sub>)/6

矩阵求幂技术可以应用于上述递归关系。
基数为 **{6，6，6，6，6，6，6，0}** 对应 **{A6，A5，A4…，A0}** 乘数为

> {
> {7/6，1，0，0，0，0，0}，
> {0，0，1，0，0，0}，
> {0，0，0，1，0，0，0}，
> {0，0，0，0，0，1，0，0}，
> {0，0，0，0，0，1，0}，
> {0，0，0，0，0，0，0，0，1}，
> {-1/6

要找到该值:

*   找到我 <sup>（N – 7）</sup>
*   找到基数* mul<sup>(N–7)</sup>。
*   1 * 7 矩阵的第一个值将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define maxSize 50
using namespace std;

// Function to multiply two 7 * 7 matrix
vector<vector<double> > matrix_product(
    vector<vector<double> > a,
    vector<vector<double> > b)
{
    vector<vector<double> > c(7);
    for (int i = 0; i < 7; i++)
        c[i].resize(7, 0);

    for (int i = 0; i < 7; i++)
        for (int j = 0; j < 7; j++)
            for (int k = 0; k < 7; k++)
                c[i][j] += a[i][k] * b[k][j];
    return c;
}

// Function to perform matrix exponentiation
vector<vector<double> > mul_expo(vector<vector<double> > mul, int p)
{

    // 7 * 7 identity matrix
    vector<vector<double> > s = { { 1, 0, 0, 0, 0, 0, 0 },
                                  { 0, 1, 0, 0, 0, 0, 0 },
                                  { 0, 0, 1, 0, 0, 0, 0 },
                                  { 0, 0, 0, 1, 0, 0, 0 },
                                  { 0, 0, 0, 0, 1, 0, 0 },
                                  { 0, 0, 0, 0, 0, 1, 0 },
                                  { 0, 0, 0, 0, 0, 0, 1 } };

    // Loop to find the power
    while (p != 1) {
        if (p % 2 == 1)
            s = matrix_product(s, mul);
        mul = matrix_product(mul, mul);
        p /= 2;
    }

    return matrix_product(mul, s);
}

// Function to return the required count
double expectedSteps(int x)
{

    // Base cases
    if (x == 0)
        return 0;
    if (x <= 6)
        return 6;

    // Multiplier matrix
    vector<vector<double> > mul = { { (double)7 / 6, 1, 0, 0, 0, 0, 0 },
                                    { 0, 0, 1, 0, 0, 0, 0 },
                                    { 0, 0, 0, 1, 0, 0, 0 },
                                    { 0, 0, 0, 0, 1, 0, 0 },
                                    { 0, 0, 0, 0, 0, 1, 0 },
                                    { 0, 0, 0, 0, 0, 0, 1 },
                                    { (double)-1 / 6, 0, 0, 0, 0, 0, 0 } };

    // Finding the required multiplier
    // i.e mul^(X-6)
    mul = mul_expo(mul, x - 6);

    // Final answer
    return (mul[0][0]
            + mul[1][0]
            + mul[2][0]
            + mul[3][0]
            + mul[4][0]
            + mul[5][0])
           * 6;
}

// Driver code
int main()
{
    int n = 10;

    cout << expectedSteps(n - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static final int maxSize = 50;

// Function to multiply two 7 * 7 matrix
static double [][] matrix_product(double [][] a,
                                  double [][] b)
{
    double [][] c = new double[7][7];

    for (int i = 0; i < 7; i++)
        for (int j = 0; j < 7; j++)
            for (int k = 0; k < 7; k++)
                c[i][j] += a[i][k] * b[k][j];
    return c;
}

// Function to perform matrix exponentiation
static double [][] mul_expo(double [][] mul, int p)
{

    // 7 * 7 identity matrix
    double [][] s = {{ 1, 0, 0, 0, 0, 0, 0 },
                     { 0, 1, 0, 0, 0, 0, 0 },
                     { 0, 0, 1, 0, 0, 0, 0 },
                     { 0, 0, 0, 1, 0, 0, 0 },
                     { 0, 0, 0, 0, 1, 0, 0 },
                     { 0, 0, 0, 0, 0, 1, 0 },
                     { 0, 0, 0, 0, 0, 0, 1 }};

    // Loop to find the power
    while (p != 1)
    {
        if (p % 2 == 1)
            s = matrix_product(s, mul);
        mul = matrix_product(mul, mul);
        p /= 2;
    }
    return matrix_product(mul, s);
}

// Function to return the required count
static double expectedSteps(int x)
{

    // Base cases
    if (x == 0)
        return 0;
    if (x <= 6)
        return 6;

    // Multiplier matrix
    double [][]mul = { { (double)7 / 6, 1, 0, 0, 0, 0, 0 },
                                   { 0, 0, 1, 0, 0, 0, 0 },
                                   { 0, 0, 0, 1, 0, 0, 0 },
                                   { 0, 0, 0, 0, 1, 0, 0 },
                                   { 0, 0, 0, 0, 0, 1, 0 },
                                   { 0, 0, 0, 0, 0, 0, 1 },
                                   {(double) - 1 / 6, 0, 0,
                                                0, 0, 0, 0 }};

    // Finding the required multiplier
    // i.e mul^(X-6)
    mul = mul_expo(mul, x - 6);

    // Final answer
    return (mul[0][0] + mul[1][0] + mul[2][0] +
            mul[3][0] + mul[4][0] + mul[5][0]) * 6;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    System.out.printf("%.5f",expectedSteps(n - 1));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

maxSize = 50

# Function to multiply two 7 * 7 matrix
def matrix_product(a, b) :
    c = np.zeros((7, 7));

    for i in range(7) :
        for j in range(7) :
            for k in range(7) :
                c[i][j] += a[i][k] * b[k][j];
    return c

# Function to perform matrix exponentiation
def mul_expo(mul, p) :

    # 7 * 7 identity matrix
    s = [ [ 1, 0, 0, 0, 0, 0, 0 ],
          [ 0, 1, 0, 0, 0, 0, 0 ],
          [ 0, 0, 1, 0, 0, 0, 0 ],
          [ 0, 0, 0, 1, 0, 0, 0 ],
          [ 0, 0, 0, 0, 1, 0, 0 ],
          [ 0, 0, 0, 0, 0, 1, 0 ],
          [ 0, 0, 0, 0, 0, 0, 1 ] ];

    # Loop to find the power
    while (p != 1) :
        if (p % 2 == 1) :
            s = matrix_product(s, mul);

        mul = matrix_product(mul, mul);
        p //= 2;

    return matrix_product(mul, s);

# Function to return the required count
def expectedSteps(x) :

    # Base cases
    if (x == 0) :
        return 0;

    if (x <= 6) :
        return 6;

    # Multiplier matrix
    mul = [ [ 7 / 6, 1, 0, 0, 0, 0, 0 ],
            [ 0, 0, 1, 0, 0, 0, 0 ],
            [ 0, 0, 0, 1, 0, 0, 0 ],
            [ 0, 0, 0, 0, 1, 0, 0 ],
            [ 0, 0, 0, 0, 0, 1, 0 ],
            [ 0, 0, 0, 0, 0, 0, 1 ],
            [ -1 / 6, 0, 0, 0, 0, 0, 0 ] ];

    # Finding the required multiplier
    # i.e mul^(X-6)
    mul = mul_expo(mul, x - 6);

    # Final answer
    return (mul[0][0] + mul[1][0] + mul[2][0] +
            mul[3][0] + mul[4][0] + mul[5][0]) * 6;

# Driver code
if __name__ == "__main__" :

    n = 10;

    print(expectedSteps(n - 1));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static readonly int maxSize = 50;

// Function to multiply two 7 * 7 matrix
static double [,] matrix_product(double [,] a,
                                 double [,] b)
{
    double [,] c = new double[7, 7];

    for (int i = 0; i < 7; i++)
        for (int j = 0; j < 7; j++)
            for (int k = 0; k < 7; k++)
                c[i, j] += a[i, k] * b[k, j];
    return c;
}

// Function to perform matrix exponentiation
static double [,] mul_expo(double [,] mul, int p)
{

    // 7 * 7 identity matrix
    double [,] s = {{ 1, 0, 0, 0, 0, 0, 0 },
                    { 0, 1, 0, 0, 0, 0, 0 },
                    { 0, 0, 1, 0, 0, 0, 0 },
                    { 0, 0, 0, 1, 0, 0, 0 },
                    { 0, 0, 0, 0, 1, 0, 0 },
                    { 0, 0, 0, 0, 0, 1, 0 },
                    { 0, 0, 0, 0, 0, 0, 1 }};

    // Loop to find the power
    while (p != 1)
    {
        if (p % 2 == 1)
            s = matrix_product(s, mul);
        mul = matrix_product(mul, mul);
        p /= 2;
    }
    return matrix_product(mul, s);
}

// Function to return the required count
static double expectedSteps(int x)
{

    // Base cases
    if (x == 0)
        return 0;
    if (x <= 6)
        return 6;

    // Multiplier matrix
    double [,]mul = {{(double)7 / 6, 1, 0, 0, 0, 0, 0 },
                                { 0, 0, 1, 0, 0, 0, 0 },
                                { 0, 0, 0, 1, 0, 0, 0 },
                                { 0, 0, 0, 0, 1, 0, 0 },
                                { 0, 0, 0, 0, 0, 1, 0 },
                                { 0, 0, 0, 0, 0, 0, 1 },
                                {(double) - 1 / 6, 0, 0,
                                                0, 0, 0, 0 }};

    // Finding the required multiplier
    // i.e mul^(X-6)
    mul = mul_expo(mul, x - 6);

    // Final answer
    return (mul[0, 0] + mul[1, 0] + mul[2, 0] +
            mul[3, 0] + mul[4, 0] + mul[5, 0]) * 6;
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;

    Console.Write("{0:f5}", expectedSteps(n - 1));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxSize = 50;

// Function to multiply two 7 * 7 matrix
function matrix_product(a, b)
{
    var c = Array.from(Array(7),
                 () => Array(7).fill(0));

    for(var i = 0; i < 7; i++)
        for(var j = 0; j < 7; j++)
            for(var k = 0; k < 7; k++)
                c[i][j] += a[i][k] * b[k][j];

    return c;
}

// Function to perform matrix exponentiation
function mul_expo( mul, p)
{

    // 7 * 7 identity matrix
    var s = [ [ 1, 0, 0, 0, 0, 0, 0 ],
              [ 0, 1, 0, 0, 0, 0, 0 ],
              [ 0, 0, 1, 0, 0, 0, 0 ],
              [ 0, 0, 0, 1, 0, 0, 0 ],
              [ 0, 0, 0, 0, 1, 0, 0 ],
              [ 0, 0, 0, 0, 0, 1, 0 ],
              [ 0, 0, 0, 0, 0, 0, 1 ] ];

    // Loop to find the power
    while (p != 1)
    {
        if (p % 2 == 1)
            s = matrix_product(s, mul);

        mul = matrix_product(mul, mul);
        p = parseInt(p / 2);
    }
    return matrix_product(mul, s);
}

// Function to return the required count
function expectedSteps(x)
{

    // Base cases
    if (x == 0)
        return 0;
    if (x <= 6)
        return 6;

    // Multiplier matrix
    var mul = [ [ 7 / 6, 1, 0, 0, 0, 0, 0 ],
                [ 0, 0, 1, 0, 0, 0, 0 ],
                [ 0, 0, 0, 1, 0, 0, 0 ],
                [ 0, 0, 0, 0, 1, 0, 0 ],
                [ 0, 0, 0, 0, 0, 1, 0 ],
                [ 0, 0, 0, 0, 0, 0, 1 ],
                [ -1 / 6, 0, 0, 0, 0, 0, 0 ] ];

    // Finding the required multiplier
    // i.e mul^(X-6)
    mul = mul_expo(mul, x - 6);

    // Final answer
    return (mul[0][0] + mul[1][0] +
            mul[2][0] + mul[3][0] +
            mul[4][0] + mul[5][0]) * 6;
}

// Driver code
var n = 10;

document.write(expectedSteps(n - 1));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
7.36111
```

**上述方法的时间复杂度**将为 O(343 * log(N))或简单的 **O(log(N))** 。