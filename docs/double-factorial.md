# 双因子

> 原文:[https://www.geeksforgeeks.org/double-factorial/](https://www.geeksforgeeks.org/double-factorial/)

**非负整数 n 的双阶乘**，是从 1 到 n 的所有与 n 具有相同奇偶性(奇数或偶数)的整数的乘积，也称为一个数的**半阶乘**，用**表示！！**。例如，9 的双阶乘是 9*7*5*3*1，即 945。注意，这个定义的一个结果是 0！！= 1.
**举例:**

```
Input: 6
Output: 48
Note that 6*4*2 = 48

Input: 7
Output: 105
Note that 7*5*3 = 105
```

对于偶数 n，双阶乘为:
![n!!=\prod_{k=1}^{n/2}(2k)=n(n-2)(n-4).....4*2    ](img/fdb911a61414c152134599912edabfee.png "Rendered by QuickLaTeX.com")
对于奇数 n，双阶乘为:
![n!!=\prod_{k=1}^{{n+1}/2}(2k-1)=n(n-2)(n-4).....3*1    ](img/44932ead5b6d9f17578824a99297cbf0.png "Rendered by QuickLaTeX.com")

**递归解:**
双阶乘可以用以下递归公式计算。

```
  n!! = n * (n-2)!!
  n!! = 1 if n = 0 or n = 1 
```

下面是双阶乘的实现。

## C++

```
#include<stdio.h>

// function to find double factorial of given number
unsigned int doublefactorial(unsigned int n)
{
    if (n == 0 || n==1)
      return 1;
    return n*doublefactorial(n-2);
}

int main()
{
    printf("Double factorial is %d", doublefactorial(5));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {

    // function to find double factorial
    // of given number
    static long doublefactorial(long n)
    {
        if (n == 0 || n==1)
            return 1;

        return n * doublefactorial(n - 2);
    }

    // Driver code
    static public void main (String[] args)
    {
        System.out.println("Double factorial"
            + " is " + doublefactorial(5));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# function to find double
# factorial of given number
def doublefactorial(n):

    if (n == 0 or n == 1):
        return 1;
    return n * doublefactorial(n - 2);

# Driver Code
print("Double factorial is",
       doublefactorial(5));

# This code is contributed
# by Smitha
```

## C#

```
using System;

class GFG {

    // function to find double factorial
    // of given number
    static uint doublefactorial(uint n)
    {
        if (n == 0 || n==1)
            return 1;

        return n * doublefactorial(n - 2);
    }

    // Driver code
    static public void Main ()
    {
        Console.WriteLine("Double factorial"
             + " is " + doublefactorial(5));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for
// Double factorial

// function return
// double factorial
function doublefactorial($n)
{
    if ($n == 0 || $n==1)
    return 1;
    return $n * doublefactorial($n - 2);
}

    // Driver Code
    echo "Double factorial is ",
            doublefactorial(5);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find double factorial of given number

    // function to find double factorial
    // of given number
    function doublefactorial(n)
    {
        if (n == 0 || n==1)
            return 1;   
        return n * doublefactorial(n - 2);
    }

// Driver code   

    document.write("Double factorial"
            + " is " + doublefactorial(5));

// This code is contributed by susmitakundugoaldanga.         
</script>
```

**输出:**

```
Double factorial is 15
```

**迭代解:**
双阶乘也可以迭代计算，因为递归对于大数来说成本很高。

## C++

```
#include<stdio.h>

// function to find double factorial of given number
unsigned int doublefactorial(unsigned int n)
{
    int res = 1;
    for (int i=n; i>=0; i=i-2)
    {
        if (i==0 || i==1)
            return res;
        else
            res *= i;
    }
}

int main()
{
    printf("Double factorial is %d", doublefactorial(5));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find double factorial
// of given number
import java .io.*;

class GFG {

    // function to find double factorial
    // of given number
    static int doublefactorial(int n)
    {
        int res = 1;
        for (int i = n; i >= 0; i = i-2)
        {
            if (i == 0 || i == 1)
                return res;
            else
                res *= i;
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println("Double factorial"
             + " is " + doublefactorial(5));
    }
}

// This code is Contributed by Anuj_67
```

## 蟒蛇 3

```
# Python3 Program to find double
# factorial of given number

# Function to find double
# factorial of given number
def doublefactorial(n):
    res = 1;
    for i in range(n, -1, -2):
        if(i == 0 or i == 1):
            return res;
        else:
            res *= i;

# Driver Code
print("Double factorial is",
        doublefactorial(5));

# This code is contributed by mits
```

## C#

```
// C# Program to find double factorial
// of given number
using System;

class GFG {

    // function to find double factorial
    // of given number
    static int doublefactorial(int n)
    {
        int res = 1;
        for (int i = n; i >= 0; i = i-2)
        {
            if (i == 0 || i == 1)
                return res;
            else
                res *= i;
        }

        return res;
    }

    // Driver code   
    static void Main()
    {
        Console.Write("Double factorial"
          + " is " + doublefactorial(5));
    }
}

// This code is Contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// function to find double
// factorial of given number
function doublefactorial( $n)
{
    $res = 1;
    for ($i = $n; $i >= 0; $i = $i - 2)
    {
        if ($i == 0 or $i == 1)
            return $res;
        else
            $res *= $i;
    }
}  

    // Driver Code
    echo "Double factorial is ", doublefactorial(5);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find
    // double factorial of given number

    // function to find double factorial
    // of given number
    function doublefactorial(n)
    {
        let res = 1;
        for (let i = n; i >= 0; i = i-2)
        {
            if (i == 0 || i == 1)
                return res;
            else
                res *= i;
        }

        return res;
    }

    document.write("Double factorial" + " is "
    + doublefactorial(5));

</script>
```

**输出:**

```
Double factorial is 15
```

上述解的时间复杂度为 O(n)。
**要点:**

1.  双阶乘和阶乘用下面的公式联系起来。

```
Note : n!! means double factorial.
If n is even, i.e., n = 2k
   n!! = 2kk!
Else (n = 2k + 1)
   n!! = (2k)! / 2kk! 

```

2.双阶乘常用于组合学。应用列表参见[维基](https://en.wikipedia.org/wiki/Double_factorial#Applications_in_enumerative_combinatorics)。一个示例应用是奇数编号的完整图 K <sub>n+1</sub> 的完美匹配计数

**参考文献:**
https://en.wikipedia.org/wiki/Double_factorial
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。