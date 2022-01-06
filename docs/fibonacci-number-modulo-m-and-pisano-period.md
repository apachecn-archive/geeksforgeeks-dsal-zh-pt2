# 斐波那契数模 M 和皮萨诺周期

> 原文:[https://www . geesforgeks . org/Fibonacci-number-modal-m-and-pisano-period/](https://www.geeksforgeeks.org/fibonacci-number-modulo-m-and-pisano-period/)

给定两个数字 **N** 和 **M** 。任务是找到**第 N 个** [斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) **mod** **M** 。
一般来说，让 **F <sub>N</sub>** 为**第 N 个**斐波那契数，则输出应为**F<sub>N</sub>**%**M**。

斐波那契数列是一系列数字，其中每个数字都是前面两个数字的和。它由递归关系定义:

```
F0 = 0
F1 = 1
Fn = Fn-1 + Fn-2
```

这些编号的顺序如下:0、1、1、2、3、5、8、13、21、34、55、…
这里 **N** 可以大。

**示例:**

> **输入:** N = 438，M = 900
> T3】输出: 44
> 
> **输入:** N = 1548276540，M = 235
> T3】输出: 185

**方法:**
但是，对于 *N* 这样的值，应该避免使用简单的[递归方法](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)来继续计算时间复杂度为 *O(2 <sup>N</sup> )* 的 *N* 斐波那契数。即使是迭代或[动态编程方法](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的算法循环进行 *N 次*迭代也不会节省时间。
这个问题可以利用 [**比萨诺时期**T21 的性质来解决。
对于给定值 *N* 和 M > = 2，用 *F <sub>i</sub> 模 M* 生成的序列(对于范围(N)中的 I)是周期性的。](https://en.wikipedia.org/wiki/Pisano_period)

**周期总是从 01 开始。**比萨诺周期定义为本系列周期的长度。
为了进一步了解，我们来看看 *M* 小的时候会发生什么:

<figure class="table">

| 我 | Zero | one | Two | three | four | five | six | seven | eight | nine | Ten | Eleven |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| *F<sub>I</sub>T3】* | Zero | one | one | Two | three | five | eight | Thirteen | Twenty-one | Thirty-four | Fifty-five | eighty-nine |
| *和对 2* | Zero | one | one | Zero | one | one | Zero | one | one | Zero | one | one |
| *和对 3* 的影响 | Zero | one | one | Two | Zero | Two | Two | one | Zero | one | one | Two |

对于 *M* = 2，周期为 011，长度为 3，而对于 *M* = 3，序列在 8 次之后重复

**例:**
那么计算一下，比如说 F <sub>2019</sub> mod 5，我们会发现 2019 年的余数除以 20 (Pisano Period of 5 就是 20)。2019 款 mod 20 是 19。所以 F<sub>2019</sub>mod 5 = F<sub>19</sub>mod 5 = 1。一般来说，这个属性是正确的。
我们需要找到 *N* 除以 *M* 的 Pisano 周期时的余数。然后对新计算的 *N* 计算 F <sub>(N)余数</sub> mod *M* 。

下面是 *F <sub>N</sub> 模 M:* 的实现

## C++

```
// C++ program to calculate
// Fibonacci no. modulo m using
// Pisano Period
#include <bits/stdc++.h>
using namespace std;

// Calculate and return Pisano Period
// The length of a Pisano Period for
// a given m ranges from 3 to m * m
long pisano(long m)
{
    long prev = 0;
    long curr = 1;
    long res = 0;

    for(int i = 0; i < m * m; i++)
    {
        long temp = 0;
        temp = curr;
        curr = (prev + curr) % m;
        prev = temp;

        if (prev == 0 && curr == 1)
            res = i + 1;
    }
    return res;
}

// Calculate Fn mod m
long fibonacciModulo(long n, long m)
{

    // Getting the period
    long pisanoPeriod = pisano(m);

    n = n % pisanoPeriod;

    long prev = 0;
    long curr = 1;

    if (n == 0)
        return 0;
    else if (n == 1)
        return 1;

    for(int i = 0; i < n - 1; i++)
    {
        long temp = 0;
        temp = curr;
        curr = (prev + curr) % m;
        prev = temp;
    }
    return curr % m;
}

// Driver Code
int main()
{
    long n = 1548276540;
    long m = 235;

    cout << (fibonacciModulo(n, m));
    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// Fibonacci no. modulo m using
// Pisano Period
import java.io.*;

class GFG{

// Calculate and return Pisano Period
// The length of a Pisano Period for
// a given m ranges from 3 to m * m
public static long pisano(long m)
{
    long prev = 0;
    long curr = 1;
    long res = 0;

    for(int i = 0; i < m * m; i++)
    {
        long temp = 0;
        temp = curr;
        curr = (prev + curr) % m;
        prev = temp;

        if (prev == 0 && curr == 1)
            res= i + 1;
    }
    return res;
}

// Calculate Fn mod m
public static long fibonacciModulo(long n,
                                   long m)
{

    // Getting the period
    long pisanoPeriod = pisano(m);

    n = n % pisanoPeriod;

    long prev = 0;
    long curr = 1;

    if (n == 0)
        return 0;
    else if (n == 1)
        return 1;

    for(int i = 0; i < n - 1; i++)
    {
        long temp = 0;
        temp = curr;
        curr = (prev + curr) % m;
        prev = temp;
    }
    return curr % m;
}

// Driver Code
public static void main(String[] args)
{
    long n = 1548276540;
    long m = 235;

    System.out.println(fibonacciModulo(n, m));
}
}

// This code is contributor by Parag Pallav Singh
```

## 蟒蛇 3

```
# Python3 program to calculate
# Fibonacci no. modulo m using
# Pisano Period

# Calculate and return Pisano Period
# The length of a Pisano Period for
# a given m ranges from 3 to m * m
def pisanoPeriod(m):
    previous, current = 0, 1
    for i in range(0, m * m):
        previous, current \
        = current, (previous + current) % m

        # A Pisano Period starts with 01
        if (previous == 0 and current == 1):
            return i + 1

# Calculate Fn mod m
def fibonacciModulo(n, m):

    # Getting the period
    pisano_period = pisanoPeriod(m)

    # Taking mod of N with
    # period length
    n = n % pisano_period

    previous, current = 0, 1
    if n==0:
        return 0
    elif n==1:
        return 1
    for i in range(n-1):
        previous, current \
        = current, previous + current

    return (current % m)

# Driver Code
if __name__ == '__main__':
    n = 1548276540
    m = 235
    print(fibonacciModulo(n, m))
```

## C#

```
// C# program to calculate
// Fibonacci no. modulo m using
// Pisano Period
using System;

class GFG {

    // Calculate and return Pisano Period
    // The length of a Pisano Period for
    // a given m ranges from 3 to m * m
    public static long pisano(long m)
    {
        long prev = 0;
        long curr = 1;
        long res = 0;

        for (int i = 0; i < m * m; i++) {
            long temp = 0;
            temp = curr;
            curr = (prev + curr) % m;
            prev = temp;

            if (prev == 0 && curr == 1)
                res = i + 1;
        }
        return res;
    }

    // Calculate Fn mod m
    public static long fibonacciModulo(long n, long m)
    {

        // Getting the period
        long pisanoPeriod = pisano(m);

        n = n % pisanoPeriod;

        long prev = 0;
        long curr = 1;

        if (n == 0)
            return 0;
        else if (n == 1)
            return 1;

        for (int i = 0; i < n - 1; i++) {
            long temp = 0;
            temp = curr;
            curr = (prev + curr) % m;
            prev = temp;
        }
        return curr % m;
    }

    // Driver Code
    public static void Main()
    {
        long n = 1548276540;
        long m = 235;

        Console.Write(fibonacciModulo(n, m));
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>

// javascript program to calculate
// Fibonacci no. modulo m using
// Pisano Period
// Calculate and return Pisano Period
// The length of a Pisano Period for
// a given m ranges from 3 to m * m
function pisano(m)
{
    let prev = 0;
    let curr = 1;
    let res = 0;

    for(let i = 0; i < m * m; i++)
    {
        let temp = 0;
        temp = curr;
        curr = (prev + curr) % m;
        prev = temp;

        if (prev == 0 && curr == 1)
            res = i + 1;
    }
    return res;
}

// Calculate Fn mod m
function fibonacciModulo(n,m)
{

    // Getting the period
    let pisanoPeriod = pisano(m);

    n = n % pisanoPeriod;

    let prev = 0;
    let curr = 1;

    if (n == 0)
        return 0;
    else if (n == 1)
        return 1;

    for(let i = 0; i < n - 1; i++)
    {
        let temp = 0;
        temp = curr;
        curr = (prev + curr) % m;
        prev = temp;
    }
    return curr % m;
}

    let n = 1548276540;
    let m = 235;

    document.write(fibonacciModulo(n, m));

    // This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
185
```

235 年的比萨诺时期是 160 年。1548276540 mod 160 是 60。F <sub>60</sub> mod 235 = 185。使用 Pisano Period，我们现在需要为比原始问题中指定的相对较低的 *N* 迭代计算斐波那契数，然后计算 F <sub>N</sub> 模 *M* 。
***时间复杂度:*** O(M <sup>2</sup> )

</figure>