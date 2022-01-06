# 在小于等于 N 的数字中找出数字的最大乘积

> 原文:[https://www . geesforgeks . org/find-数字中的最大数字乘积-小于或等于 n/](https://www.geeksforgeeks.org/find-maximum-product-of-digits-among-numbers-less-than-or-equal-to-n/)

给定一个整数 **N > 0** ，任务是在小于或等于 **N** 的数字中寻找数字的最大乘积。
**例:**

> **输入:** N = 390
> **输出:** 216
> 最大可能乘积由数字 389
> 3 * 8 * 9 = 216
> **输入:** N = 432
> **输出:** 243

**方法:**这个问题也可以用[这篇](https://www.geeksforgeeks.org/find-the-number-in-a-range-having-maximum-product-of-the-digits/)文章中描述的方法解决，取下限为 **1** ，取上限为 **N** 。解决这个问题的另一个方法是使用递归。递归的条件如下:

*   如果 **N = 0** ，则返回 **1** 。
*   如果 **N < 10** 然后返回 **N** 。
*   否则，返回**最大值(maxProd(N / 10) * (N % 10)，max prod((n/10)–1)* 9**

在递归的每一步，取最后一个数字或 9 来最大化数字的乘积。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the maximum product of
// digits among numbers less than or equal to N
int maxProd(int N)
{
    if (N == 0)
        return 1;
    if (N < 10)
        return N;
    return max(maxProd(N / 10) * (N % 10),
               maxProd(N / 10 - 1) * 9);
}

// Driver code
int main()
{
    int N = 390;
    cout << maxProd(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that returns the maximum product of
// digits among numbers less than or equal to N
static int maxProd(int N)
{
    if (N == 0)
        return 1;
    if (N < 10)
        return N;
    return Math.max(maxProd(N / 10) * (N % 10),
            maxProd(N / 10 - 1) * 9);
}

// Driver code
public static void main (String[] args)
{
    int N = 390;
    System.out.println (maxProd(N));
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the maximum product of
# digits among numbers less than or equal to N
def maxProd(N):

    if (N == 0):
        return 1
    if (N < 10):
        return N
    return max(maxProd(N // 10) * (N % 10),
               maxProd(N // 10 - 1) * 9)

# Driver code
N = 390
print(maxProd(N))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns the maximum product of
// digits among numbers less than or equal to N
static int maxProd(int N)
{
    if (N == 0)
        return 1;
    if (N < 10)
        return N;
    return Math.Max(maxProd(N / 10) * (N % 10),
            maxProd(N / 10 - 1) * 9);
}

// Driver code
static public void Main ()
{
    int N = 390;
    Console.WriteLine(maxProd(N));
}
}

// This code is contributed by Tushil..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns the maximum product of
// digits among numbers less than or equal to N
function maxProd($N)
{
    if ($N == 0)
        return 1;
    if ($N < 10)
        return $N;
    return max(maxProd((int)($N / 10)) * ($N % 10),
               maxProd((int)($N / 10) - 1) * 9);
}

// Driver code
$N = 390;
echo maxProd($N);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns the maximum product of
// digits among numbers less than or equal to N
function maxProd(N)
{
    if (N == 0)
        return 1;
    if (N < 10)
        return N;
    return Math.max(maxProd(parseInt(N / 10)) * (N % 10),
            maxProd(parseInt(N / 10) - 1) * 9);
}

// Driver code
let N = 390;
document.write(maxProd(N));

// This code is contributed
// by bobby

</script>
```

**Output:** 

```
216
```