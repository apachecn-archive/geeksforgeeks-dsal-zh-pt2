# 检查第 n 个斐波那契数是否为 10 的倍数的有效方法

> 原文:[https://www . geesforgeks . org/efficient-way-check-what-n-th-Fibonacci-number-multiple-10/](https://www.geeksforgeeks.org/efficient-way-check-whether-n-th-fibonacci-number-multiple-10/)

给我们一个变量 n，我们需要找出[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是否会是 10 的倍数。
**例:**

```
Input : 15
Output : Yes

Input : 17
Output : No
```

一个**简单的方法**就是找到第 n 个斐波那契数，检查它是否能被 10 整除。

## C++

```
// A simple C++ program to check if
// n-th Fibonacci number is multiple
// of 10.
#include<bits/stdc++.h>

int fibonacci(int n)
{
    int a = 0, b = 1, c;
    if (n <= 1)
        return n;
    for (int i = 2; i<= n; i++)
    {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Returns true if n-th Fibonacci number
// is multiple of 10.
bool isMultipleOf10(int n)
{
    int f = fibonacci(30);
    return  (f % 10 == 0);
}

// Driver code
int main()
{
    int n = 30;
    if (isMultipleOf10(n))
        printf("Yes\n");
    else
        printf("No\n");
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to check if
// n-th Fibonacci number is multiple
// of 10.
class Fibonacci
{
    static int fibonacci(int n)
    {
        int a = 0;
        int b=1;
        int c=0;
        if (n <= 1)
            return n;

        for (int i = 2; i<= n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }

        return c;
    }

    // Returns true if n-th Fibonacci number
    // is multiple of 10.
    static boolean isMultipleOf10(int n)
    {
        int f = fibonacci(30);
        return  (f % 10 == 0);
    }

    // main function
    public static void main (String[] args)
    {
        int n = 30;
        if (isMultipleOf10(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# A simple Python 3 program to check if
# n-th Fibonacci number is multiple
# of 10.

def fibonacci(n):

    a = 0
    b = 1
    if (n <= 1):
        return n
    for i in range(2, n + 1):

        c = a + b
        a = b
        b = c

    return c

# Returns true if n-th Fibonacci
# number is multiple of 10.
def isMultipleOf10(n):
    f = fibonacci(30)
    return (f % 10 == 0)

# Driver code
if __name__ =="__main__":

    n = 30
    if (isMultipleOf10(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ita_c
```

## C#

```
// A simple C# program to check if
// n-th Fibonacci number is multiple
// of 10.
using System;

class GFG {

    static int fibonacci(int n)
    {
        int a = 0;
        int b = 1;
        int c = 0;
        if (n <= 1)
            return n;

        for (int i = 2; i<= n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }

        return c;
    }

    // Returns true if n-th Fibonacci
    // number is multiple of 10.
    static bool isMultipleOf10(int n)
    {
        int f = fibonacci(30);
        return (f % 10 == 0);
    }

    // main function
    public static void Main ()
    {
        int n = 30;

        if (isMultipleOf10(n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code contribute by parshar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// A simple PHP program to
// check if n-th Fibonacci
// number is multiple of 10.

function fibonacci($n)
{
    $a = 0; $b = 1; $c;
    if ($n <= 1)
        return $n;
    for ($i = 2; $i<= $n; $i++)
    {
        $c = $a + $b;
        $a = $b;
        $b = $c;
    }
    return $c;
}

// Returns true if n-th Fibonacci
// number is multiple of 10.
function isMultipleOf10($n)
{
    $f = fibonacci(30);
    return ($f % 10 == 0);
}

// Driver code
    $n = 30;

    if (isMultipleOf10($n))
        echo "Yes\n";
    else
        echo "No\n";

// This ocde is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to
// check if n-th Fibonacci
// number is multiple of 10.
function fibonacci(n)
{
    let a = 0;
    let b = 1;
    let c;
    if (n <= 1)
        return n;
    for (let i = 2; i<= n; i++)
    {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Returns true if n-th Fibonacci
// number is multiple of 10.
function isMultipleOf10(n)
{
    let f = fibonacci(30);
    return (f % 10 == 0);
}

// Driver code
    let n = 30;    
    if (isMultipleOf10(n))
        document.write("Yes<br>");
    else
        document.write("No\n");

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
Yes
```

**高效法:**
如果 n 很大，那么上面的解法可能行不通，那么就不可能找到斐波那契数。此外，我们可以通过查看模式来检查而不找到斐波那契数。让我们看看如何！
如果一个数能被 10 整除，那么它必须能被 5 整除，也能被 2 整除。
**斐波那契数列中 2 的倍数:**
**0**1 1**2**3 5**8**13 21**34**55 89**144**233 377**610**987 1597**2584**…。
粗体显示的数字可被 2 整除。仔细观察，我们发现每三分之一的数都可以被 2 整除。
**斐波那契数列中 5 的倍数:**
**0**1 1 2 3**5**8 13 21 34**55**89 144 233 377**610**987 1597 2584……
粗体显示的数字可被 5 整除。仔细观察，我们发现每 5 个数字都可以被 5 整除。
现在 3 和 5 的 LCM 是 15。所以，每 15 个斐波那契数都可以被 10 整除。所以，我们不需要求斐波那契数，只需要检查 n 是否能被 15 整除。下面是实现。

## C++

```
// A simple C++ program to check if
// n-th Fibonacci number is multiple
// of 10.
#include<bits/stdc++.h>

// Returns true if n-th Fibonacci number
// is multiple of 10.
bool isMultipleOf10(int n)
{
    return  (n % 15 == 0);
}

int main()
{
    int n = 30;
    if (isMultipleOf10(n))
        printf("Yes\n");
    else
        printf("No\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to check if
// n-th Fibonacci number is multiple
// of 10.
class Fibonacci
{
    // Returns true if n-th Fibonacci number
    // is multiple of 10.
    static boolean isMultipleOf10(int n)
    {
        if(n%15 == 0)
            return  true;

        return false;   
    }

    // main function
    public static void main (String[] args)
    {
        int n = 30;
        if (isMultipleOf10(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# A simple Python 3 program to check if
# n-th Fibonacci number is multiple
# of 10.

# Returns true if n-th Fibonacci number
# is multiple of 10.
def isMultipleOf10(n):

    return (n % 15 == 0)

# Driver Code
n = 30

if (isMultipleOf10(n)):
    print("Yes");
else:
    print("No");

# This code is contributed
# by Akanksha Rai
```

## C#

```
// A simple C# program to check if
// n-th Fibonacci number is multiple
// of 10.
using System;

class GFG {

    // Returns true if n-th Fibonacci number
    // is multiple of 10.
    static bool isMultipleOf10(int n)
    {
        if(n % 15 == 0)
            return  true;

        return false;   
    }

    // main function
    public static void Main ()
    {
        int n = 30;
        if (isMultipleOf10(n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to
// check if n-th Fibonacci
// number is multiple of 10.

// Returns true if n-th
// Fibonacci number is
// multiple of 10.
function isMultipleOf10($n)
{
    return ($n % 15 == 0);
}

// Driver Code
$n = 30;
if (isMultipleOf10($n))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
// A simple Javascript program to
// check if n-th Fibonacci
// number is multiple of 10.

// Returns true if n-th
// Fibonacci number is
// multiple of 10.
function isMultipleOf10(n)
{
    return (n % 15 == 0);
}

// Driver Code
let n = 30;
if (isMultipleOf10(n))
    document.write("Yes<br>");
else
    document.write("No<br>");

// This code is contributed by _saurabh_jaiswal
```

**输出:**

```
Yes
```

这段代码在 0(1)时间内运行。
本文由[阿迪蒂亚·库马尔](https://www.linkedin.com/in/aditya-kumar-837315100/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。