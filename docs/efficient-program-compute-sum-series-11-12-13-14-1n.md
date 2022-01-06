# 计算级数 1/1 和的高效程序！+ 1/2!+ 1/3!+ 1/4!+..+ 1/n！

> 原文:[https://www . geesforgeks . org/efficient-program-compute-sum-series-11-12-13-14-1n/](https://www.geeksforgeeks.org/efficient-program-compute-sum-series-11-12-13-14-1n/)

给定一个正整数 n，写一个函数计算级数 1/1 的和！+ 1/2!+..+ 1/n！
一个**简单的解决方案**是将和初始化为 0，然后运行一个循环并调用循环内的阶乘函数。
下面是一个简单解决方案的实现。

## C++

```
// A simple C++ program to compute sum of series 1/1! + 1/2! + .. + 1/n!
#include <iostream>
using namespace std;

//  Utility function to find
int factorial(int n)
{
    int res = 1;
    for (int i=2; i<=n; i++)
       res *= i;
    return res;
}

// A Simple Function to return value of 1/1! + 1/2! + .. + 1/n!
double sum(int n)
{
    double sum = 0;
    for (int i = 1; i <= n; i++)
        sum += 1.0/factorial(i);
    return sum;
}

// Driver program to test above functions
int main()
{
    int n = 5;
    cout << sum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to compute
// sum of series 1/1! + 1/2! + .. + 1/n!
import java.io.*;

class GFG {

    // Utility function to find
    static int factorial(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
        res *= i;
        return res;
    }

    // A Simple Function to return value
    // of 1/1! + 1/2! + .. + 1/n!
    static double sum(int n)
    {
        double sum = 0;
        for (int i = 1; i <= n; i++)
            sum += 1.0/factorial(i);
        return sum;
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 5;
        System.out.println(sum(n));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 program to compute sum of series
# 1/1! + 1/2! + .. + 1/n!

# Function to find factorial of a number
def factorial(n):
    res = 1
    for i in range(2, n + 1):
            res *= i
    return res

# A Simple Function to return value
# of 1/1! + 1/2! + .. + 1/n!
def sum(n):
    s = 0.0

    for i in range(1, n + 1):
        s += 1.0 / factorial(i)
    print(s)

# Driver program to test above functions
n = 5
sum(n)

# This code is contributed by Danish Raza
```

## C#

```
// A simple C# program to compute sum
// of series 1/1! + 1/2! + .. + 1/n!
using System;

class GFG {

    // Utility function to find
    static int factorial(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res *= i;

        return res;
    }

    // A Simple Function to return value
    // of 1/1! + 1/2! + .. + 1/n!
    static double sum(int n)
    {
        double sum = 0;
        for (int i = 1; i <= n; i++)
            sum += 1.0/factorial(i);

        return sum;
    }

    // Driver program
    public static void Main ()
    {
        int n = 5;

        Console.WriteLine(sum(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to compute
// sum of series 1/1! + 1/2! + .. + 1/n!

// Utility function to find
function factorial($n)
{
    $res = 1;
    for ($i = 2; $i <= $n; $i++)
        $res *= $i;
    return $res;
}

// A Simple Function to return
// value of 1/1! + 1/2! + .. + 1/n!
function sum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += 1.0 / factorial($i);
    return $sum;
}

// Driver Code
$n = 5;
echo(sum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

//Javascript program to compute
// sum of series 1/1! + 1/2! + .. + 1/n!

// Utility function to find
function factorial(n)
{
    let res = 1;
    for (let i = 2;  i <= n; i++)
        res *= i;
    return res;
}

// A Simple Function to return
// value of 1/1! + 1/2! + .. + 1/n!
function sum(n)
{
    let sum = 0;
    for (let i = 1; i <= n; i++)
        sum += 1.0 / factorial(i);
    return sum;
}

// Driver Code

let n = 5;
document.write(sum(n).toFixed(5));

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
1.71667
```

上述解的时间复杂度为 O(n * n！)这是巨大的。
一个**有效解**可以求出 O(n)时间内的和。其思想是在和相同的循环中计算阶乘。下面是这个想法的实现。

## C++

```
// A simple C++ program to compute sum of series 1/1! + 1/2! + .. + 1/n!
#include <iostream>
using namespace std;

// An Efficient Function to return value of 1/1! + 1/2! + .. + 1/n!
double sum(int n)
{
    double sum = 0;
    int fact = 1;
    for (int i = 1; i <= n; i++)
    {
       fact *= i;         // Update factorial
       sum += 1.0/fact;   // Update series sum
    }
    return sum;
}

// Driver program to test above functions
int main()
{
    int n = 5;
    cout << sum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to compute
// sum of series 1/1! + 1/2! + .. + 1/n!
import java.io.*;

class GFG {

    // An Efficient Function to return
    // value of 1/1! + 1/2! + .. + 1/n!
    static double sum(int n)
    {
        double sum = 0;
        int fact = 1;
        for (int i = 1; i <= n; i++)
        {
            // Update factorial
            fact *= i;

            // Update series sum
            sum += 1.0/fact;
        }
        return sum;
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 5;
        System.out.println(sum(n));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 program to compute sum of series
# 1/1! + 1/2! + .. + 1/n!

# Function to return value of
# 1/1! + 1/2! + .. + 1/n!
def sum(n):
    sum = 0
    fact = 1

    for i in range(1, n + 1):

        # Update factorial
        fact *= i

        # Update series sum
        sum += 1.0/fact

    print(sum)

# Driver program to test above functions
n = 5
sum(n)

# This code is contributed by Danish Raza
```

## C#

```
// A simple C# program to compute sum
// of series 1/1! + 1/2! + .. + 1/n!
using System;

class GFG {

    // An Efficient Function to return
    // value of 1/1! + 1/2! + .. + 1/n!
    static double sum(int n)
    {
        double sum = 0;
        int fact = 1;

        for (int i = 1; i <= n; i++)
        {

            // Update factorial
            fact *= i;

            // Update series sum
            sum += 1.0 / fact;
        }
        return sum;
    }

    // Driver program
    public static void Main ()
    {
        int n = 5;

        Console.WriteLine(sum(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to
// compute sum of series
// 1/1! + 1/2! + .. + 1/n!

// An Efficient Function to
// return value of 1/1! +
// 1/2! + .. + 1/n!
function sum($n)
{
    $sum = 0;
    $fact = 1;
    for ($i = 1; $i <= $n; $i++)
    {
        // Update factorial
        $fact *= $i;   

        // Update series sum
        $sum += 1.0 / $fact;
    }
    return $sum;
}

// Driver Code
$n = 5;
echo sum($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

    // A simple Javascript program to compute sum
    // of series 1/1! + 1/2! + .. + 1/n!

    // An Efficient Function to return
    // value of 1/1! + 1/2! + .. + 1/n!
    function sum(n)
    {
        let sum = 0;
        let fact = 1;

        for (let i = 1; i <= n; i++)
        {

            // Update factorial
            fact *= i;

            // Update series sum
            sum += 1.0 / fact;
        }
        return sum.toFixed(5);
    }

    let n = 5;

      document.write(sum(n));

</script>
```

**输出:**

```
1.71667
```

本文由 **Rahul Gupta** 撰稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写下您的评论。