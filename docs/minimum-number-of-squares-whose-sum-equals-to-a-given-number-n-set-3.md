# 平方和等于给定数 N 的最小平方数|集合-3

> 原文:[https://www . geesforgeks . org/最小平方数-其和等于给定数-n-set-3/](https://www.geeksforgeeks.org/minimum-number-of-squares-whose-sum-equals-to-a-given-number-n-set-3/)

一个数总是可以表示为其他数的平方和。请注意，1 是一个正方形，我们总是可以将一个数字分解为(1*1 + 1*1 + 1*1 + …)。给定一个数 N，求平方和的最小数 **N** 。

**示例:**

> **输入:** N = 13
> **输出:** 2
> **说明:**
> 13 可以表示为，13 = 3 <sup>2</sup> + 2 <sup>2</sup> 。因此，输出为 2。
> 
> **输入:** N = 100
> **输出:** 1
> **说明:**
> 100 可以表示为 100 = 10 <sup>2</sup> 。因此，输出为 1。

**天真进场:**关于**【O(N * sqrt(N))】进场，请参考本文** [**第二集**](https://www.geeksforgeeks.org/minimum-number-of-squares-whose-sum-equals-to-given-number-n-set-2/) **。**

**高效方法:**优化天真方法的思路是使用 [*拉格朗日四方形定理*](https://www.geeksforgeeks.org/lagranges-four-square-theorem/) 和*勒让德三方形定理*。下面讨论这两个定理:

> [拉格朗日四平方定理](https://en.wikipedia.org/wiki/Lagrange%27s_four-square_theorem)，也称为巴赫猜想，指出每个**自然数**可以表示为四个整数平方的**和，**其中每个整数都是非负的。

> [勒让德三平方定理](https://en.wikipedia.org/wiki/Legendre%27s_three-square_theorem)规定:a **自然数**可以表示为整数的三个平方的**和，当且仅当 n 为**而非**形式为:**n = 4<sup>a</sup>(8b+7)**为**非负整数 a 和 b** 。**

因此，证明了表示任意数 **N** 的最小平方数只能在集合 *{1，2，3，4}* 内。因此，只有检查这些 *4* 可能的值，才能找到代表任何数字 **N** 的最小方块数。请遵循以下步骤:

*   如果 **N** 是一个完美的正方形，那么结果就是 *1* 。
*   如果 **N** 可以表示为两个平方之和，那么结果就是 *2* 。
*   如果 **N** 不能用**N = 4<sup>a</sup>(8b+7)**的形式表示，其中 **a** 和 **b** 都是非负整数，那么通过勒让德三平方定理得到的结果就是 *3。*
*   如果以上条件都不满足，那么由 [*拉格朗日四方形定理*](https://en.wikipedia.org/wiki/Lagrange%27s_four-square_theorem)*得出的结果是 *4* 。*

*下面是上述方法的实现:*

## *C++*

```
*// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if N
// is a perfect square
bool isPerfectSquare(int N)
{
    int floorSqrt = sqrt(N);

    return (N == floorSqrt * floorSqrt);
}

// Function that returns true check if
// N is sum of three squares
bool legendreFunction(int N)
{
    // Factor out the powers of 4
    while (N % 4 == 0)
        N /= 4;

    // N is NOT of the
    // form 4^a * (8b + 7)
    if (N % 8 != 7)
        return true;
    else
        return false;
}

// Function that finds the minimum
// number of square whose sum is N
int minSquares(int N)
{

    // If N is perfect square
    if (isPerfectSquare(N))
        return 1;

    // If N is sum of 2 perfect squares
    for (int i = 1; i * i < N; i++) {
        if (isPerfectSquare(N - i * i))
            return 2;
    }

    // If N is sum of 3 perfect squares
    if (legendreFunction(N))
        return 3;

    // Otherwise, N is the
    // sum of 4 perfect squares
    return 4;
}

// Driver code
int main()
{
    // Given number
    int N = 123;

    // Function call
    cout << minSquares(N);
    return 0;
}*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java program for the above approach
import java.util.*;

class GFG{

// Function that returns true if N
// is a perfect square
static boolean isPerfectSquare(int N)
{
    int floorSqrt = (int)Math.sqrt(N);

    return (N == floorSqrt * floorSqrt);
}

// Function that returns true check if
// N is sum of three squares
static boolean legendreFunction(int N)
{

    // Factor out the powers of 4
    while (N % 4 == 0)
        N /= 4;

    // N is NOT of the
    // form 4^a * (8b + 7)
    if (N % 8 != 7)
        return true;
    else
        return false;
}

// Function that finds the minimum
// number of square whose sum is N
static int minSquares(int N)
{

    // If N is perfect square
    if (isPerfectSquare(N))
        return 1;

    // If N is sum of 2 perfect squares
    for(int i = 1; i * i < N; i++)
    {
        if (isPerfectSquare(N - i * i))
            return 2;
    }

    // If N is sum of 3 perfect squares
    if (legendreFunction(N))
        return 3;

    // Otherwise, N is the
    // sum of 4 perfect squares
    return 4;
}

// Driver code
public static void main(String[] args)
{

    // Given number
    int N = 123;

    // Function call
    System.out.print(minSquares(N));
}
}

// This code is contributed by 29AjayKumar*
```

## *蟒蛇 3*

```
*# Python3 program for the above approach
from math import sqrt, floor, ceil

# Function that returns True if N
# is a perfect square
def isPerfectSquare(N):

    floorSqrt = floor(sqrt(N))
    return (N == floorSqrt * floorSqrt)

# Function that returns True check if
# N is sum of three squares
def legendreFunction(N):

    # Factor out the powers of 4
    while (N % 4 == 0):
        N //= 4

    # N is NOT of the
    # form 4^a * (8b + 7)
    if (N % 8 != 7):
        return True
    else:
        return False

# Function that finds the minimum
# number of square whose sum is N
def minSquares(N):

    # If N is perfect square
    if (isPerfectSquare(N)):
        return 1

    # If N is sum of 2 perfect squares
    for i in range(N):
        if i * i < N:
            break
        if (isPerfectSquare(N - i * i)):
            return 2

    # If N is sum of 3 perfect squares
    if (legendreFunction(N)):
        return 3

    # Otherwise, N is the
    # sum of 4 perfect squares
    return 4

# Driver code
if __name__ == '__main__':

    # Given number
    N = 123

    # Function call
    print(minSquares(N))

# This code is contributed by mohit kumar 29*
```

## *C#*

```
*// C# program for the above approach
using System;

class GFG{

// Function that returns true if N
// is a perfect square
static bool isPerfectSquare(int N)
{
    int floorSqrt = (int)Math.Sqrt(N);

    return (N == floorSqrt * floorSqrt);
}

// Function that returns true check
// if N is sum of three squares
static bool legendreFunction(int N)
{

    // Factor out the powers of 4
    while (N % 4 == 0)
        N /= 4;

    // N is NOT of the
    // form 4^a * (8b + 7)
    if (N % 8 != 7)
        return true;
    else
        return false;
}

// Function that finds the minimum
// number of square whose sum is N
static int minSquares(int N)
{

    // If N is perfect square
    if (isPerfectSquare(N))
        return 1;

    // If N is sum of 2 perfect squares
    for(int i = 1; i * i < N; i++)
    {
        if (isPerfectSquare(N - i * i))
            return 2;
    }

    // If N is sum of 3 perfect squares
    if (legendreFunction(N))
        return 3;

    // Otherwise, N is the
    // sum of 4 perfect squares
    return 4;
}

// Driver code
public static void Main(String[] args)
{

    // Given number
    int N = 123;

    // Function call
    Console.Write(minSquares(N));
}
}

// This code is contributed by Rajput-Ji*
```

## *java 描述语言*

```
*<script>

// Javascript program for the above approach

// Function that returns true if N
// is a perfect square
function isPerfectSquare(N)
{
    let floorSqrt = Math.floor(Math.sqrt(N));

    return (N == floorSqrt * floorSqrt);
}

// Function that returns true check if
// N is sum of three squares
function legendreFunction(N)
{

    // Factor out the powers of 4
    while (N % 4 == 0)
        N = Math.floor(N / 4);

    // N is NOT of the
    // form 4^a * (8b + 7)
    if (N % 8 != 7)
        return true;
    else
        return false;
}

// Function that finds the minimum
// number of square whose sum is N
function minSquares(N)
{

    // If N is perfect square
    if (isPerfectSquare(N))
        return 1;

    // If N is sum of 2 perfect squares
    for(let i = 1; i * i < N; i++)
    {
        if (isPerfectSquare(N - i * i))
            return 2;
    }

    // If N is sum of 3 perfect squares
    if (legendreFunction(N))
        return 3;

    // Otherwise, N is the
    // sum of 4 perfect squares
    return 4;
}

// Driver Code

    // Given number
    let N = 123;

    // Function call
    document.write(minSquares(N));

</script>*
```

***Output:** 

```
3
```* 

***时间复杂度:***O(sqrt(N))*
T5】辅助空间: *O(1)**