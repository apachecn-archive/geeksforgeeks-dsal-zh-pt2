# 记忆化(1D、2D 和 3D)

> 原文:[https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)

大多数动态规划问题通过两种方式解决:

1.  **制表:**自下而上
2.  **记忆化:**自上而下

解决动态规划中大多数问题的一个更简单的方法是首先编写递归代码，然后编写递归函数的自底向上制表法或自顶向下记忆法。为任何问题编写自上而下的动态规划解决方案的步骤是:

1.  编写递归代码
2.  记住返回值并使用它来减少递归调用。

**一维记忆**
第一步将是编写递归代码。在下面的程序中，显示了一个与递归相关的程序，其中只有一个参数改变了它的值。由于只有一个参数是非常数，这种方法被称为一维记忆。例如，寻找斐波那契数列中第 N 项的斐波那契数列问题。这里已经讨论了递归方法。
下面给出的是寻找第 N 项的递归代码:

## C++

```
// C++ program to find the Nth term
// of Fibonacci series
#include <bits/stdc++.h>
using namespace std;

// Fibonacci Series using Recursion
int fib(int n)
{

    // Base case
    if (n <= 1)
        return n;

    // recursive calls
    return fib(n - 1) + fib(n - 2);
}

// Driver Code
int main()
{
    int n = 6;
    printf("%d", fib(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// Nth term of Fibonacci series
import java.io.*;

class GFG
{

// Fibonacci Series
// using Recursion
static int fib(int n)
{

    // Base case
    if (n <= 1)
        return n;

    // recursive calls
    return fib(n - 1) +
           fib(n - 2);
}

// Driver Code
public static void main (String[] args)
{
    int n = 6;
    System.out.println(fib(n));
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 program to find the Nth term
# of Fibonacci series

# Fibonacci Series using Recursion
def fib(n):

    # Base case
    if (n <= 1):
        return n

    # recursive calls
    return fib(n - 1) + fib(n - 2)

# Driver Code
if __name__=='__main__':
    n = 6
    print (fib(n))

# This code is contributed by
# Shivi_Aggarwal
```

## C#

```
// C# program to find
// the Nth term of
// Fibonacci series
using System;

class GFG
{

// Fibonacci Series
// using Recursion
static int fib(int n)
{
    // Base case
    if (n <= 1)
        return n;

    // recursive calls
    return fib(n - 1) +
           fib(n - 2);
}
// Driver Code
static public void Main ()
{
    int n = 6;
    Console.WriteLine(fib(n));
}
}

// This code is contributed
// by akt_mit
```

## java 描述语言

```
<script>
// Javascript program to find the Nth term
// of Fibonacci series

// Fibonacci Series using Recursion
function fib(n)
{

    // Base case
    if (n <= 1)
        return n;

    // recursive calls
    return fib(n - 1) + fib(n - 2);
}

// Driver Code
let n = 6;
document.write(fib(n));

// This code is contributed by subhammahato348.
</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the Nth term of
// Fibonacci series
// using Recursion

function fib($n)
{

    // Base case
    if ($n <= 1)
        return $n;

    // recursive calls
    return fib($n - 1) +
           fib($n - 2);
}

// Driver Code
$n = 6;
echo fib($n);

// This code is contributed
// by ajit
?>
```

**Output:** 

```
8
```