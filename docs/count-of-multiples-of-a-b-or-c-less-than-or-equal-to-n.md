# 小于或等于 N 的 A、B 或 C 的倍数的计数

> 原文:[https://www . geesforgeks . org/a-B-或-c-小于或等于 n 的倍数计数/](https://www.geeksforgeeks.org/count-of-multiples-of-a-b-or-c-less-than-or-equal-to-n/)

给定四个整数 **N** 、 **A** 、 **B** 和 **C** 。任务是从范围**【1，N】**中找出可被 **A** 、 **B** 或 **C** 整除的整数个数。

**示例:**

> **输入:** A = 2，B = 3，C = 5，N = 10
> **输出:** 8
> 2，3，4，5，6，8，9 和 10 是
> 范围【1，10】中唯一可被 2，3 或 5 整除的数字。
> 
> **输入:** A = 7，B = 3，C = 5，N = 100
> T3】输出: 55

**方法:**一种有效的方法是使用集合论的概念。因为我们必须找到能被 a 或 b 或 c 整除的数。

*   设 n(a):可被 a 整除的数的个数。
*   设 n(b):可被 b 整除的数的个数。
*   设 n(c):可被 c 整除的数的个数。
*   n(a∪b):可被 a 和 b 整除的数的计数。
*   n(a∪c):可被 a 和 c 整除的数的计数。
*   n(b∪c):可被 b 和 c 整除的数的计数。
*   n(a∪b∪c):可被 a 和 b 以及 c 整除的数的计数。

根据集合论，

n(a∪b∪c)= n(a)+n(b)+n(c)——n(a∪b)——n(b∪c)——n(a∪c)+n(a∪b∪c)

所以。可被 A、B 或 C 整除的数的计数为**(num/A)+(num/B)+(num/C)–(num/LCM(A，B))–(num/LCM(A，B))–(num/LCM(A，C))+–(num/LCM(A，B，C))**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// gcd of a and b
long gcd(long a, long b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the count of integers
// from the range [1, num] which are
// divisible by either a, b or c
long divTermCount(long a, long b, long c, long num)
{
    // Calculate the number of terms divisible by a, b
    // and c then remove the terms which are divisible
    // by both (a, b) or (b, c) or (c, a) and then
    // add the numbers which are divisible by a, b and c
    return ((num / a) + (num / b) + (num / c)
            - (num / ((a * b) / gcd(a, b)))
            - (num / ((c * b) / gcd(c, b)))
            - (num / ((a * c) / gcd(a, c)))
            + (num / ((a * b * c) / gcd(gcd(a, b), c))));
}

// Driver code
int main()
{
    long a = 7, b = 3, c = 5, n = 100;

    cout << divTermCount(a, b, c, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the
// gcd of a and b
static long gcd(long a, long b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the count of integers
// from the range [1, num] which are
// divisible by either a, b or c
static long divTermCount(long a, long b,
                         long c, long num)
{
    // Calculate the number of terms divisible by a, b
    // and c then remove the terms which are divisible
    // by both (a, b) or (b, c) or (c, a) and then
    // add the numbers which are divisible by a, b and c
    return ((num / a) + (num / b) + (num / c) -
                (num / ((a * b) / gcd(a, b))) -
                (num / ((c * b) / gcd(c, b))) -
                (num / ((a * c) / gcd(a, c))) +
                (num / ((a * b * c) / gcd(gcd(a, b), c))));
}

// Driver code
static public void main (String []arr)
{
    long a = 7, b = 3, c = 5, n = 100;

    System.out.println(divTermCount(a, b, c, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# gcd of a and b
def gcd(a, b) :

    if (a == 0) :
        return b;

    return gcd(b % a, a);

def lcm (x, y):
    return (x * y) // gcd (x, y)

# Function to return the count of integers
# from the range [1, num] which are
# divisible by either a, b or c
def divTermCount(a, b, c, num) :

    # Calculate the number of terms divisible by a, b
    # and c then remove the terms which are divisible
    # by both (a, b) or (b, c) or (c, a) and then
    # add the numbers which are divisible by a, b and c
    return (num // a + num // b + num // c -
                 num // lcm(a, b) -
                 num // lcm(c, b) -
                 num // lcm(a, c) +
                 num // (lcm(lcm(a, b), c)))

# Driver code
if __name__ == "__main__" :

    a = 7; b = 3; c = 5; n = 100;

    print(divTermCount(a, b, c, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation for above approach
using System;

class GFG
{

// Function to return the
// gcd of a and b
static long gcd(long a, long b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the count of integers
// from the range [1, num] which are
// divisible by either a, b or c
static long divTermCount(long a, long b,
                         long c, long num)
{
    // Calculate the number of terms divisible by a, b
    // and c then remove the terms which are divisible
    // by both (a, b) or (b, c) or (c, a) and then
    // add the numbers which are divisible by a, b and c
    return ((num / a) + (num / b) + (num / c) -
            (num / ((a * b) / gcd(a, b))) -
            (num / ((c * b) / gcd(c, b))) -
            (num / ((a * c) / gcd(a, c))) +
            (num / ((a * b * c) / gcd(gcd(a, b), c))));
}

// Driver code
static public void Main (String []arr)
{
    long a = 7, b = 3, c = 5, n = 100;

    Console.WriteLine(divTermCount(a, b, c, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// gcd of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the count of integers
// from the range [1, num] which are
// divisible by either a, b or c
function divTermCount(a, b, c, num)
{

    // Calculate the number of terms divisible by a, b
    // and c then remove the terms which are divisible
    // by both (a, b) or (b, c) or (c, a) and then
    // add the numbers which are divisible by a, b and c
    return Math.ceil(((num / a) + (num / b) + (num / c) -
                      (num / ((a * b) / gcd(a, b))) -
                      (num / ((c * b) / gcd(c, b))) -
                      (num / ((a * c) / gcd(a, c))) +
                      (num / ((a * b * c) / gcd(gcd(a, b), c)))));
}

// Driver code
n = 13;
var a = 7, b = 3, c = 5, n = 100;

document.write(divTermCount(a, b, c, n));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
55
```