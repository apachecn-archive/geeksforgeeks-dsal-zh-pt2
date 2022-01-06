# 计数表示‘n’为奇数之和的方式

> 原文:[https://www . geesforgeks . org/count-way-express-n-sum-奇数-整数/](https://www.geeksforgeeks.org/count-ways-express-n-sum-odd-integers/)

给定一个正整数 n。计算将“n”表示为奇数个正整数之和的方法总数。

```
Input: 4
Output: 3

Explanation
There are only three ways to write 4
as sum of odd integers:
1\. 1 + 3
2\. 3 + 1
3\. 1 + 1 + 1 + 1

Input: 5
Output: 5
```

**简单的方法**就是找到问题的递归性质。数字“n”可以写成(n-1) <sup>第</sup>个数字或(n-2) <sup>第</sup>个数字的奇数之和。让写“n”的方式总数为方式(n)。‘way(n)’的值可以用递归公式写成如下:

```
ways(n) = ways(n-1) + ways(n-2)
```

上面的表达式其实就是[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的表达式。因此问题简化为寻找第 n <sup>个</sup>个实数。

```
ways(1) = fib(1) = 1
ways(2) = fib(2) = 1
ways(3) = fib(2) = 2
ways(4) = fib(4) = 3
```

## C++

```
// C++ program to count ways to write
// number as sum of odd integers
#include<iostream>
using namespace std;

// Function to calculate n'th Fibonacci number
int fib(int n)
{
  /* Declare an array to store Fibonacci numbers. */
  int f[n+1];
  int i;

  /* 0th and 1st number of the series are 0 and 1*/
  f[0] = 0;
  f[1] = 1;

  for (i = 2; i <= n; i++)
  {
      /* Add the previous 2 numbers in the series
         and store it */
      f[i] = f[i-1] + f[i-2];
  }

  return f[n];
}

// Return number of ways to write 'n'
// as sum of odd integers
int countOddWays(int n)
{
    return fib(n);
}

// Driver code
int main()
{
    int n = 4;
    cout << countOddWays(n) << "\n";

    n = 5;
    cout << countOddWays(n);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count ways to write
// number as sum of odd integers
import java.util.*;

class GFG {

// Function to calculate n'th Fibonacci number
static int fib(int n) {

    /* Declare an array to store Fibonacci numbers. */
    int f[] = new int[n + 1];
    int i;

    /* 0th and 1st number of the series are 0 and 1*/
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++) {

    /* Add the previous 2 numbers in the series
        and store it */
    f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Return number of ways to write 'n'
// as sum of odd integers
static int countOddWays(int n)
{
    return fib(n);
}

// Driver code
public static void main(String[] args) {

    int n = 4;
    System.out.print(countOddWays(n) + "\n");

    n = 5;
    System.out.print(countOddWays(n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python code to count ways to write
# number as sum of odd integers

# Function to calculate n'th
# Fibonacci number
def fib( n ):

    # Declare a list to store
    # Fibonacci numbers.
    f=list()

    # 0th and 1st number of the
    # series are 0 and 1
    f.append(0)
    f.append(1)

    i = 2
    while i<n+1:

        # Add the previous 2 numbers
        # in the series and store it
        f.append(f[i-1] + f[i-2])
        i += 1
    return f[n]

# Return number of ways to write 'n'
# as sum of odd integers
def countOddWays( n ):
    return fib(n)

# Driver code
n = 4
print(countOddWays(n))
n = 5
print(countOddWays(n))

# This code is contributed by "Sharad_Bhardwaj"
```

## C#

```
// C# program to count ways to write
// number as sum of odd integers
using System;

class GFG {

    // Function to calculate n'th
    // Fibonacci number
    static int fib(int n) {

        /* Declare an array to store
        Fibonacci numbers. */
        int []f = new int[n + 1];
        int i;

        /* 0th and 1st number of the
        series are 0 and 1*/
        f[0] = 0;
        f[1] = 1;

        for (i = 2; i <= n; i++)
        {

            /* Add the previous 2 numbers
            in the series and store it */
            f[i] = f[i - 1] + f[i - 2];
        }

        return f[n];
    }

    // Return number of ways to write 'n'
    // as sum of odd integers
    static int countOddWays(int n)
    {
        return fib(n);
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(countOddWays(n));

        n = 5;
        Console.WriteLine(countOddWays(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count ways to write
// number as sum of odd integers

// Function to calculate n'th
// Fibonacci number
function fib($n)
{

    // Declare an array to
    // store Fibonacci numbers.
    $f = array();
    $i;

    // 0th and 1st number of the
    // series are 0 and 1
    $f[0] = 0;
    $f[1] = 1;

    for($i = 2; $i <= $n; $i++)
    {

        // Add the previous 2
        // numbers in the series
        // and store it
        $f[$i] = $f[$i - 1] +
                 $f[$i - 2];
    }

    return $f[$n];
}

// Return number of ways to write 'n'
// as sum of odd integers
function countOddWays( $n)
{
    return fib($n);
}

    // Driver Code
    $n = 4;
    echo countOddWays($n) , "\n";
    $n = 5;
    echo countOddWays($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to count ways to write
// number as sum of odd integers

// Function to calculate n'th Fibonacci number
function fib(n) {

    /* Declare an array to store Fibonacci numbers. */
    let f = [];
    let i;

    /* 0th and 1st number of the series are 0 and 1*/
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++) {

    /* Add the previous 2 numbers in the series
        and store it */
    f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Return number of ways to write 'n'
// as sum of odd integers
function countOddWays(n)
{
    return fib(n);
}

// Driver code
        let n = 4;
    document.write(countOddWays(n) + "<br/>");

    n = 5;
    document.write(countOddWays(n));

    // This code is contributed by code_hunt.
</script>
```

输出:

```
3
5
```

**注:** *上述实现的时间复杂度为 O(n)。使用* [*通过矩阵指数*](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) 进行斐波那契函数优化，可以进一步优化到 0(Logn)时间。
本文由[舒巴姆·班萨尔](https://www.quora.com/profile/Shubham-Bansal-209)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。