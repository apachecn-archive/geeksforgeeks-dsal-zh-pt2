# 在恒定时间内找到给定斐波那契数的指数

> 原文:[https://www . geesforgeks . org/find-index-given-Fibonacci-number-constant-time/](https://www.geeksforgeeks.org/find-index-given-fibonacci-number-constant-time/)

给我们一个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。前几个斐波那契数是 0，1，1，2，3，5，8，13，21，34，55，89，144，…..
我们必须找到给定斐波那契数的指数，即像斐波那契数 8 在指数 6。

**示例:**

```
Input : 13
Output : 7

Input : 34
Output : 9
```

**方法 1(简单)**
一个简单的方法是找到给定斐波那契数之前的斐波那契数，并计算执行的迭代次数。

## C++

```
// A simple C++ program to find index of given
// Fibonacci number.
#include<bits/stdc++.h>

int findIndex(int n)
{
    // if Fibonacci number is less than 2,
    // its index will be same as number
    if (n <= 1)
        return n;

    int a = 0, b = 1, c = 1;
    int res = 1;

    // iterate until generated fibonacci number
    // is less than given fibonacci number
    while (c < n)
    {
        c = a + b;

        // res keeps track of number of generated
        // fibonacci number

        res++;
        a = b;
        b = c;
    }
    return res;
}

// Driver program to test above function
int main()
{
    int result = findIndex(21);
    printf("%d\n", result);
}

// This code is contributed by Saket Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to find index of
// given Fibonacci number.
import java.io.*;

class GFG {

    static int findIndex(int n)
    {

        // if Fibonacci number is less
        // than 2, its index will be
        // same as number
        if (n <= 1)
            return n;

        int a = 0, b = 1, c = 1;
        int res = 1;

        // iterate until generated fibonacci
        // number is less than given
        // fibonacci number
        while (c < n)
        {
            c = a + b;

            // res keeps track of number of
            // generated fibonacci number
            res++;
            a = b;
            b = c;
        }

        return res;
    }

    // Driver program to test above function
    public static void main (String[] args)
    {
        int result = findIndex(21);
        System.out.println( result);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# A simple Python 3 program to find
# index of given Fibonacci number.

def findIndex(n) :

    # if Fibonacci number is less than 2,
    # its index will be same as number
    if (n <= 1) :
        return n

    a = 0
    b = 1
    c = 1
    res = 1

    # iterate until generated fibonacci number
    # is less than given fibonacci number
    while (c < n) :
        c = a + b

        # res keeps track of number of 
        # generated fibonacci number
        res = res + 1
        a = b
        b = c

    return res

# Driver program to test above function
result = findIndex(21)
print(result)

# this code is contributed by Nikita Tiwari
```

## C#

```
// A simple C# program to
// find index of given
// Fibonacci number.
using System;
class GFG
{
    static int findIndex(int n)
    {

        // if Fibonacci number
        // is less than 2, its
        // index will be same
        // as number
        if (n <= 1)
            return n;

        int a = 0, b = 1, c = 1;
        int res = 1;

        // iterate until generated
        // fibonacci number is less
        // than given fibonacci number
        while (c < n)
        {
            c = a + b;

            // res keeps track of
            // number of generated
            // fibonacci number
            res++;
            a = b;
            b = c;
        }

        return res;
    }

    // Driver Code
    public static void Main ()
    {
        int result = findIndex(21);
        Console.WriteLine(result);
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to
// find index of given
// Fibonacci number.

function findIndex($n)
{

    // if Fibonacci number
    // is less than 2,
    // its index will be
    // same as number
    if ($n <= 1)
        return $n;

    $a = 0; $b = 1; $c = 1;
    $res = 1;

    // iterate until generated
    // fibonacci number
    // is less than given
    // fibonacci number
    while ($c < $n)
    {
        $c = $a + $b;

        // res keeps track of
        // number of generated
        // fibonacci number

        $res++;
        $a = $b;
        $b = $c;
    }
    return $res;
}

// Driver Code
$result = findIndex(21);
echo($result);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to
// find index of given
// Fibonacci number.
function findIndex(n)
{

    // If Fibonacci number
    // is less than 2, its
    // index will be same
    // as number
    if (n <= 1)
        return n;

    let a = 0, b = 1, c = 1;
    let res = 1;

    // Iterate until generated
    // fibonacci number is less
    // than given fibonacci number
    while (c < n)
    {
        c = a + b;

        // res keeps track of
        // number of generated
        // fibonacci number
        res++;
        a = b;
        b = c;
    }
    return res;
}

// Driver code
let result = findIndex(21);
document.write(result);

// This code is contributed by decode2207

</script>
```

**输出:**

```
 8
```

**方法 2(基于公式)**
但是在这里，我们需要生成所有斐波那契数，直到提供一个斐波那契数。但是，这个问题有一个快速的解决方案。让我们看看如何！请注意，在大多数平台上，计算一个数字的日志是一个 O(1)操作。

斐波纳契数描述为，
**F** n = 1 / sqrt(5)(幂(a，n)–幂(b，n))，其中
a = 1 / 2 ( 1 + sqrt(5))和 b = 1/2(1–sqrt(5))

在忽略因 n 值大而非常小的幂(b，n)时，我们得到
**n = round { 2.078087 * log(Fn)+1.672276 }**
，其中 **round** 表示四舍五入到最接近的整数。

以下是上述想法的实现。

## C++

```
// C++ program to find index of given Fibonacci
// number
#include<bits/stdc++.h>

int findIndex(int n)
{
    float fibo = 2.078087 * log(n) + 1.672276;

    // returning rounded off value of index
    return round(fibo);
}

// Driver program to test above function
int main()
{
    int n = 55;
    printf("%d\n", findIndex(n));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to find index of given
// Fibonacci number
public class Fibonacci
{

  static int findIndex(int n)
  {
    float fibo = 2.078087F * (float) Math.log(n) + 1.672276F;

    // returning rounded off value of index
    return Math.round(fibo);
  }

  public static void main(String[] args)
  {
    int result = findIndex(55);
    System.out.println(result);
  }
}
```

## 蟒蛇 3

```
# Python 3 program to find index of given Fibonacci
# number

import math
def findIndex(n) :
    fibo = 2.078087 * math.log(n) + 1.672276

    # returning rounded off value of index
    return round(fibo)

# Driver program to test above function
n = 21
print(findIndex(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A simple C# program to find
// index of given Fibonacci number
using System;

class Fibonacci {

static int findIndex(int n)
{
    float fibo = 2.078087F * (float) Math.Log(n) +
                                        1.672276F;

    // returning rounded off value of index
    return (int)(Math.Round(fibo));
}

  // Driver code
  public static void Main()
  {
    int result = findIndex(55);
    Console.Write(result);
  }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find index
// of given Fibonacci Number

function findIndex($n)
{
    $fibo = 2.078087 * log($n) + 1.672276;

    // returning rounded off
    // value of index
    return round($fibo);
}

// Driver code
$n = 55;
echo(findIndex($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to find
// index of given Fibonacci number

function findIndex(n)
{
    var fibo = 2.078087 * parseFloat(Math.log(n)) + 1.672276;

    // Returning rounded off value of index
    return Math.round(fibo);
}

// Driver code
var result = findIndex(55);
document.write(result);

// This code is contributed by Ankita saini

</script>
```

**输出:**

```
 10
```

本文由[阿迪蒂亚·库马尔](https://www.linkedin.com/in/aditya-kumar-837315100/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。