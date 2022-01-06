# 计算骑士到达目标的所有可能方式

> 原文:[https://www . geeksforgeeks . org/骑士到达目标的所有可能方式的计数/](https://www.geeksforgeeks.org/count-of-all-possible-ways-to-reach-a-target-by-a-knight/)

给定两个整数 **N** ， **M** 表示 **N×M** 棋盘，任务是从 **(0，0)** 开始统计骑士可以到达 **(N，M)** 的次数。由于答案可能会很大，所以以 **10 <sup>9</sup> +7** 为模打印答案。

**示例:**

> **输入:** N =3，M= 3
> **输出:** 2
> **说明:**
> 到达(3，3)形态(0，0)的两种方式如下:
> (0，0) → (1，2) → (3，3)
> (0，0) → (2，1) → (3，3)
> 
> **输入:** N=4，M=3 【T15

**逼近**:这里的思路是观察每一次移动都将 **x 坐标的值+y 坐标**的值增加 **3 的模式。**按照以下步骤解决问题。

1.  如果 **(N + M)** 不能被 **3** 整除，那么就不存在可能的路径。
2.  如果 **(N + M) % 3==0** 则计算 **(+1，+2)** 即 **X** 的招式数，计算 **(+2，+1)** 即 **Y** 的招式数。
3.  求类型 **(+1，+2)** 的方程，即 **X + 2Y = N**
4.  求类型 **(+2，+1)** 的方程，即 **2X + Y = M**
5.  求 **X** 和 **Y** 的计算值，如果 **X < 0** 或 **Y < 0** ，则不存在可能的路径。
6.  否则计算<sup>(</sup>**<sup>X+Y)</sup>C<sub>Y</sub>**。

下面是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

const int Mod = 1e9 + 7;

// Function to return X^Y % Mod
int power(int X, int Y, int Mod)
{

    // Base Case
    if (Y == 0)
        return 1;

    int p = power(X, Y / 2, Mod) % Mod;
    p = (p * p) % Mod;

    if (Y & 1) {
        p = (X * p) % Mod;
    }

    return p;
}

// Function to return the
// inverse of factorial of N
int Inversefactorial(int N)
{

    // Base case
    if (N <= 0)
        return 1;

    int fact = 1;

    for (int i = 1; i <= N; i++) {
        fact = (fact * i) % Mod;
    }

    return power(fact, Mod - 2, Mod);
}

// Function to return factorial
// of n % Mod
int factorial(int N)
{

    // Base case
    if (N <= 0)
        return 1;

    int fact = 1;

    for (int i = 1; i <= N; i++) {
        fact = (fact * i) % Mod;
    }

    return fact;
}

// Function to return  the value
// of n! / (( n- k)! * k!)
int nck(int N, int K)
{
    int factN = factorial(N);
    int inv = Inversefactorial(K);
    int invFact = Inversefactorial(N - K);
    return (((factN * inv) % Mod) * invFact) % Mod;
}

// Function to return the count of
// ways to reach (n, m) from (0, 0)
int TotalWaYs(int N, int M)
{

    // If (N + M) % 3 != 0
    if ((N + M) % 3 != 0)

        // No possible way exists
        return 0;

    // Calculate X and Y from the
    // equations X + 2Y = N
    // and 2X + Y == M
    int X = N - (N + M) / 3;
    int Y = M - (N + M) / 3;

    if (X < 0 || Y < 0)
        return 0;

    return nck(X + Y, Y);
}

// Driver Code
int main()
{

    int N = 3, M = 3;

    cout << TotalWaYs(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

static int Mod = (int) (1e9 + 7);

// Function to return X^Y % Mod
static int power(int X, int Y, int Mod)
{

    // Base Case
    if (Y == 0)
        return 1;

    int p = power(X, Y / 2, Mod) % Mod;
    p = (p * p) % Mod;

    if ((Y & 1) != 0)
    {
        p = (X * p) % Mod;
    }

    return p;
}

// Function to return the
// inverse of factorial of N
static int Inversefactorial(int N)
{

    // Base case
    if (N <= 0)
        return 1;

    int fact = 1;

    for (int i = 1; i <= N; i++)
    {
        fact = (fact * i) % Mod;
    }

    return power(fact, Mod - 2, Mod);
}

// Function to return factorial
// of n % Mod
static int factorial(int N)
{

    // Base case
    if (N <= 0)
        return 1;

    int fact = 1;

    for (int i = 1; i <= N; i++)
    {
        fact = (fact * i) % Mod;
    }

    return fact;
}

// Function to return  the value
// of n! / (( n- k)! * k!)
static int nck(int N, int K)
{
    int factN = factorial(N);
    int inv = Inversefactorial(K);
    int invFact = Inversefactorial(N - K);
    return (((factN * inv) % Mod) * invFact) % Mod;
}

// Function to return the count of
// ways to reach (n, m) from (0, 0)
static int TotalWaYs(int N, int M)
{

    // If (N + M) % 3 != 0
    if (((N + M) % 3 )!= 0)

        // No possible way exists
        return 0;

    // Calculate X and Y from the
    // equations X + 2Y = N
    // and 2X + Y == M
    int X = N - (N + M) / 3;
    int Y = M - (N + M) / 3;

    if (X < 0 || Y < 0)
        return 0;

    return nck(X + Y, Y);
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, M = 3;

    System.out.print(TotalWaYs(N, M));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to implement
# above approach
Mod = int(1e9 + 7)

# Function to return X^Y % Mod
def power(X, Y, Mod):

    # Base case
    if Y == 0:
        return 1

    p = power(X, Y // 2, Mod) % Mod
    p = (p * p) % Mod

    if Y & 1:
        p = (X * p) % Mod

    return p

# Function to return the
# inverse of factorial of N
def Inversefactorial(N):

    # Base case
    if N <= 0:
        return 1

    fact = 1
    for i in range(1, N + 1):
        fact = (fact * i) % Mod

    return power(fact, Mod - 2, Mod)

# Function to return factorial
# of n % Mod
def factorial(N):

    # Base case
    if N <= 0:
        return 1

    fact = 1
    for i in range(1, N + 1):
        fact = (fact * i) % Mod

    return fact

# Function to return the value
# of n! / (( n- k)! * k!)
def nck(N, K):

    factN = factorial(N)
    inv = Inversefactorial(K)
    invFact = Inversefactorial(N - K)

    return (((factN * inv) % Mod) * invFact) % Mod

# Function to return the count of
# ways to reach (n, m) from (0, 0)
def TotalWays(N, M):

    # If (N + M) % 3 != 0
    if (N + M) % 3 != 0:

        # No possible way exists
        return 0

    # Calculate X and Y from the
    # equations X + 2Y = N
    # and 2X + Y == M
    X = N - (N + M) // 3
    Y = M - (N + M) // 3

    if X < 0 or Y < 0:
        return 0

    return nck(X + Y, Y)

# Driver code
N, M = 3, 3

print(TotalWays(N, M))

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static int Mod = (int)(1e9 + 7);

// Function to return X^Y % Mod
static int power(int X, int Y, int Mod)
{

    // Base Case
    if (Y == 0)
        return 1;

    int p = power(X, Y / 2, Mod) % Mod;
    p = (p * p) % Mod;

    if ((Y & 1) != 0)
    {
        p = (X * p) % Mod;
    }
    return p;
}

// Function to return the
// inverse of factorial of N
static int Inversefactorial(int N)
{

    // Base case
    if (N <= 0)
        return 1;

    int fact = 1;

    for(int i = 1; i <= N; i++)
    {
        fact = (fact * i) % Mod;
    }
    return power(fact, Mod - 2, Mod);
}

// Function to return factorial
// of n % Mod
static int factorial(int N)
{

    // Base case
    if (N <= 0)
        return 1;

    int fact = 1;

    for(int i = 1; i <= N; i++)
    {
        fact = (fact * i) % Mod;
    }
    return fact;
}

// Function to return the value
// of n! / (( n- k)! * k!)
static int nck(int N, int K)
{
    int factN = factorial(N);
    int inv = Inversefactorial(K);
    int invFact = Inversefactorial(N - K);
    return (((factN * inv) % Mod) * invFact) % Mod;
}

// Function to return the count of
// ways to reach (n, m) from (0, 0)
static int TotalWaYs(int N, int M)
{

    // If (N + M) % 3 != 0
    if (((N + M) % 3 ) != 0)

        // No possible way exists
        return 0;

    // Calculate X and Y from the
    // equations X + 2Y = N
    // and 2X + Y == M
    int X = N - (N + M) / 3;
    int Y = M - (N + M) / 3;

    if (X < 0 || Y < 0)
        return 0;

    return nck(X + Y, Y);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3, M = 3;

    Console.Write(TotalWaYs(N, M));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

var Mod = 1000000007;

// Function to return X^Y % Mod
function power(X, Y, Mod)
{

    // Base Case
    if (Y == 0)
        return 1;

    var p = power(X, Y / 2, Mod) % Mod;
    p = (p * p) % Mod;

    if (Y & 1) {
        p = (X * p) % Mod;
    }

    return p;
}

// Function to return the
// inverse of factorial of N
function Inversefactorial(N)
{

    // Base case
    if (N <= 0)
        return 1;

    var fact = 1;

    for (var i = 1; i <= N; i++) {
        fact = (fact * i) % Mod;
    }

    return power(fact, Mod - 2, Mod);
}

// Function to return factorial
// of n % Mod
function factorial(N)
{

    // Base case
    if (N <= 0)
        return 1;

    var fact = 1;

    for (var i = 1; i <= N; i++) {
        fact = (fact * i) % Mod;
    }

    return fact;
}

// Function to return  the value
// of n! / (( n- k)! * k!)
function nck( N, K)
{
    var factN = factorial(N);
    var inv = Inversefactorial(K);
    var invFact = Inversefactorial(N - K);
    return (((factN * inv) % Mod) * invFact) % Mod;
}

// Function to return the count of
// ways to reach (n, m) from (0, 0)
function TotalWaYs(N, M)
{

    // If (N + M) % 3 != 0
    if ((N + M) % 3 != 0)

        // No possible way exists
        return 0;

    // Calculate X and Y from the
    // equations X + 2Y = N
    // and 2X + Y == M
    var X = N - (N + M) / 3;
    var Y = M - (N + M) / 3;

    if (X < 0 || Y < 0)
        return 0;

    return nck(X + Y, Y);
}

// Driver Code
var N = 3, M = 3;
document.write( TotalWaYs(N, M));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(X + Y + log(mod))。*
***辅助空间:** O(1)*