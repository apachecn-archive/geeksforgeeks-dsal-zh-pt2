# 斐波那契问题(Fib(N)* Fib(N)–Fib(N-1)* Fib(N+1)的值)

> 原文:[https://www . geesforgeks . org/Fibonacci-problem-of-fibn-fibn-fibn 1/](https://www.geeksforgeeks.org/fibonacci-problem-value-of-fibnfibn-fibn-fibn1/)

给定一个正整数 *N* ，任务是找到*Fib(N)<sup>2</sup>–(Fib(N-1)* Fib(N+1))*，其中 *Fib(N)* 返回[第 N 个斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**举例:**

> **输入:** N = 3
> **输出:**1
> Fib(3)* Fib(3)–Fib(2)* Fib(4)= 4–3 = 1
> **输入:** N = 2
> **输出:**-1
> Fib(2)* Fib(2)–Fib(1)* Fib(3)= 1–2 =-1

**方法:**这个问题可以通过先试用几个测试用例来解决。让我们举几个例子:

> 对于 N = 1:Fib(1)* Fib(1)–Fib(0)* Fib(2)= 1–0 = 1
> 对于 N = 2:Fib(2)* Fib(2)–Fib(1)* Fib(3)= 1–2 =-1
> 对于 N = 3:Fib(3)* Fib(3)–Fib(2)* Fib(4)= 4–3 = 1
> 对于 N = 4:Fib(4)* Fib(4)–Fib(3)* Fib(5) = 9–10 =-1
> 我们在这里观察到当 *N* 为偶数时，则答案为 *-1* ，当 *N* 为奇数时，则答案为 *1* 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

int getResult(int n)
{
    if (n & 1)
        return 1;
    return -1;
}

// Driver code
int main()
{
    int n = 3;
    cout << getResult(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach

import java.io.*;

class GFG {

static int getResult(int n)
{
    if ((n & 1)>0)
        return 1;
    return -1;
}

// Driver code
    public static void main (String[] args) {

    int n = 3;
    System.out.println(getResult(n));
    }
//This code is contributed by @Tushil.   
}
```

## 蟒蛇 3

```
# Python 3 implementation of
# the approach
def getResult(n):

    if n & 1:
        return 1
    return -1

# Driver code
n = 3
print(getResult(n))

# This code is contributed
# by Shrikant13
```

## C#

```
//C# implementation of the approach

using System;

class GFG {

static int getResult(int n)
{
    if ((n & 1)>0)
        return 1;
    return -1;
}

// Driver code
    public static void Main () {

    int n = 3;
    Console.WriteLine(getResult(n));
    }
//This code is contributed by anuj_67..
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

function getResult($n)
{
    if ($n & 1)
        return 1;
    return -1;
}

// Driver code
$n = 3;
echo getResult($n);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    function getResult(n)
    {
        if ((n & 1)>0)
            return 1;
        return -1;
    }

    let n = 3;
    document.write(getResult(n));

</script>
```

**Output:** 

```
1
```