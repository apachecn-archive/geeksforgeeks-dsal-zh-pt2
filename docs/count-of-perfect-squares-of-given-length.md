# 给定长度的完美正方形的计数

> 原文:[https://www . geesforgeks . org/给定长度的完美平方数/](https://www.geeksforgeeks.org/count-of-perfect-squares-of-given-length/)

给定一个整数 **N** ，任务是找到长度为 **N** 的完美正方形的数量。
**例:**

> **输入:** N = 1
> **输出:** 3
> **说明:**一位数的完美方块是 1、4、9。
> **输入:** N = 2
> **输出:** 6
> **说明:**两位数的完美方块是 16、25、36、49、64 和 81。

**天真的做法:**为了解决这个问题，我们可以检查**10<sup>(N–1)</sup>T5】和**10<sup>N</sup>–1**之间的所有数字，每当遇到完美的正方形时，递增**计数器**。
以下是上述方法的实施:**

## C++

```
// C++ Program to count perfect
// squares of given length

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is perfect square
bool isPerfectSquare(long double x)
{
    // Find floating point value of
    // square root of x.
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function to return the count of
// n digit perfect squares
int countSquares(int n)
{
    // Initialize result
    int cnt = 0;

    // Traverse through all numbers
    // of n digits
    for (int i = pow(10, (n - 1));
         i < pow(10, n); i++) {

        // Check if current number
        // 'i' is perfect square
        if (i != 0 && isPerfectSquare(i))
            cnt++;
    }
    return cnt;
}

// Driver code
int main()
{
    int n = 3;
    cout << countSquares(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count perfect
// squares of given length
class GFG{

// Function to check if a
// number is perfect square
static boolean isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to return the count of
// n digit perfect squares
static int countSquares(int n)
{

    // Initialize result
    int cnt = 0;

    // Traverse through all numbers
    // of n digits
    for(int i = (int) Math.pow(10, (n - 1));
                  i < Math.pow(10, n); i++)
    {

        // Check if current number
        // 'i' is perfect square
        if (i != 0 && isPerfectSquare(i))
            cnt++;
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.print(countSquares(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to count perfect
# squares of given length
import math;

# Function to check if a
# number is perfect square
def isPerfectSquare(x):

    # Find floating point value of
    # square root of x.
    sr = math.sqrt(x);

    # If square root is an integer
    return ((sr - math.floor(sr)) == 0);

# Function to return the count of
# n digit perfect squares
def countSquares(n):

    # Initialize result
    cnt = 0;

    # Traverse through all numbers
    # of n digits
    for i in range(int(math.pow(10, (n - 1))),
                   int(math.pow(10, n))):

        # Check if current number
        # 'i' is perfect square
        if (i != 0 and isPerfectSquare(i)):
            cnt += 1;

    return cnt;

# Driver code
n = 3;
print(countSquares(n));

# This code is contributed by Akanksha_Rai
```

## C#

```
// C# program to count perfect
// squares of given length
using System;

class GFG{

// Function to check if a
// number is perfect square
static bool isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function to return the count of
// n digit perfect squares
static int countSquares(int n)
{

    // Initialize result
    int cnt = 0;

    // Traverse through all numbers
    // of n digits
    for(int i = (int) Math.Pow(10, (n - 1));
                  i < Math.Pow(10, n); i++)
    {

       // Check if current number
       // 'i' is perfect square
       if (i != 0 && isPerfectSquare(i))
           cnt++;
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.Write(countSquares(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript Program to count perfect
// squares of given length

// Function to check if a
// number is perfect square
function isPerfectSquare(x)
{
    // Find floating point value of
    // square root of x.
    let sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to return the count of
// n digit perfect squares
function countSquares(n)
{
    // Initialize result
    let cnt = 0;

    // Traverse through all numbers
    // of n digits
    for (let i = Math.pow(10, (n - 1));
         i < Math.pow(10, n); i++) {

        // Check if current number
        // 'i' is perfect square
        if (i != 0 && isPerfectSquare(i))
            cnt++;
    }
    return cnt;
}

// Driver code
let n = 3;
document.write(countSquares(n));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
22
```