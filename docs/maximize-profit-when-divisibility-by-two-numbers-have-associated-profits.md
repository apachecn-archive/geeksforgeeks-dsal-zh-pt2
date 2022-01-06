# 当两个数可除性有关联利润时利润最大化

> 原文:[https://www . geeksforgeeks . org/利润最大化-当被两个数字分割-有关联-利润/](https://www.geeksforgeeks.org/maximize-profit-when-divisibility-by-two-numbers-have-associated-profits/)

给定五个整数 **N** 、 **A** 、 **B** 、 **X** 和 **Y** 。任务是从**【1，N】**范围内的数字中找到最大利润。如果正数可被 **A** 整除，则利润增加 **X** ，如果正数可被 **B** 整除，则利润增加 **Y** 。
**注:**获利正数最多可以加一次。
**举例:**

> **输入:** N = 3，A = 1，B = 2，X = 3，Y = 4
> T3】输出: 10
> 1， 2 和 3 可以被 A 整除
> 2 是给定范围内唯一可以被 B 整除的数
> 2 可以被 A 和 B 整除
> 1 和 3 可以被 A 整除得到 2 * 3 = 6 的利润
> 2 可以被 B 整除得到 1 *的利润 4 = 4
> 2 可被两者整除，但为了利润最大化，它被 B 而不是 A 整除。
> **输入:** N = 6，A = 6，B = 2，X = 8，Y = 2
> **输出:** 12

**方法:**很容易看出，只有当一个数是 **lcm(A，B)** 的倍数时，我们才能用 **A** 和 **B** 来除这个数。很明显，这个数字应该除以产生更多利润的数字。
所以答案等于**X *(N/A)+Y *(N/B)–min(X，Y) * (N / lcm(A，B))** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum profit
int maxProfit(int n, int a, int b, int x, int y)
{
    int res = x * (n / a);
    res += y * (n / b);

    // min(x, y) * n / lcm(a, b)
    res -= min(x, y) * (n / ((a * b) / __gcd(a, b)));
    return res;
}

// Driver code
int main()
{
    int n = 6, a = 6, b = 2, x = 8, y = 2;
    cout << maxProfit(n, a, b, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to return the maximum profit
static int maxProfit(int n, int a, int b,
                            int x, int y)
{
    int res = x * (n / a);
    res += y * (n / b);

    // min(x, y) * n / lcm(a, b)
    res -= Math.min(x, y) * (n / ((a * b) / __gcd(a, b)));
    return res;
}

// Driver code
public static void main (String[] args)
{
    int n = 6, a = 6, b = 2, x = 8, y = 2;
    System.out.println(maxProfit(n, a, b, x, y));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the maximum profit
def maxProfit(n, a, b, x, y) :

    res = x * (n // a);
    res += y * (n // b);

    # min(x, y) * n / lcm(a, b)
    res -= min(x, y) * (n // ((a * b) //
                           gcd(a, b)));
    return res;

# Driver code
if __name__ == "__main__" :

    n = 6 ;a = 6; b = 2; x = 8; y = 2;

    print(maxProfit(n, a, b, x, y));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to return the maximum profit
static int maxProfit(int n, int a, int b, int x, int y)
{
    int res = x * (n / a);
    res += y * (n / b);

    // min(x, y) * n / lcm(a, b)
    res -= Math.Min(x, y) * (n / ((a * b) / __gcd(a, b)));
    return res;
}

// Driver code
static void Main()
{
    int n = 6, a = 6, b = 2, x = 8, y = 2;
    Console.WriteLine(maxProfit(n, a, b, x, y));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);

}

// Function to return the maximum profit
function maxProfit($n, $a, $b, $x, $y)
{
    $res = $x * ($n / $a);
    $res += $y * ($n / $b);

    // min(x, y) * n / lcm(a, b)
    $res -= min($x, $y) * ($n /
              (($a * $b) / __gcd($a, $b)));
    return $res;
}

// Driver code
$n = 6;
$a = 6;
$b = 2;
$x = 8;
$y = 2;
print(maxProfit($n, $a, $b, $x, $y));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to return the maximum profit

function maxProfit(n, a, b, x, y)
{
    let res = x * Math.floor(n / a);
    res += y * Math.floor(n / b);

    // min(x, y) * n / lcm(a, b)
    res -= Math.min(x, y) * (n / ((a * b) / __gcd(a, b)));
    return res;
}

// Driver code
    let n = 6, a = 6, b = 2, x = 8, y = 2;
    document.write(maxProfit(n, a, b, x, y));

// This article is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
12
```