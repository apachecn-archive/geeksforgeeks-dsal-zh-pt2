# 通过将 X 乘以给定的同素将 X 转换为 Y 所需的最小运算

> 原文:[https://www . geeksforgeeks . org/minimum-operations-required-convert-x-y-by-x-乘以给定的-co-primes/](https://www.geeksforgeeks.org/minimum-operations-required-to-convert-x-to-y-by-multiplying-x-with-the-given-co-primes/)

给定四个整数 **X** 、 **Y** 、 **P** 和 **Q** ，使得 **X ≤ Y** 和 **gcd(P，Q) = 1** 。任务是找到将 **X** 转换为 **Y** 所需的最小操作。在一次操作中，您可以将 **X** 乘以 **P** 或 **Q** 。如果无法将 **X** 转换为 **Y** ，则打印 **-1** 。
**例:**

> **输入:** X = 12，Y = 2592，P = 2，Q = 3
> **输出:**6
> (12 * 2)—>(24 * 3)—>(72 * 2)—>(144 * 3)—>(432 * 3)—>(1296 * 2)—>2592
> **输入:** X = 7，Y = 0

**逼近:**如果 **Y** 不能被 **X** 整除，那么任何整数与 **X** 的任意次整数乘法都不能得到 **Y** ，结果为 **-1** 。
否则，让 **d = Y / X** 。现在，**P<sup>a</sup>* Q<sup>b</sup>= d**必须成立才能有有效的解，那种情况下的结果就是 **(a + b)** 否则 **-1** 如果 **d** 不能用 **P** 和 **Q** 的幂表示。
为了检查状况，继续用 **P** 和 **Q** 分割 **d** 直到可以分割。现在，如果最终 **d = 1** ，那么解决方案是可能的，否则就不可能。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// operations required
int minOperations(int x, int y, int p, int q)
{

    // Not possible
    if (y % x != 0)
        return -1;

    int d = y / x;

    // To store the greatest power
    // of p that divides d
    int a = 0;

    // While divible by p
    while (d % p == 0) {
        d /= p;
        a++;
    }

    // To store the greatest power
    // of q that divides d
    int b = 0;

    // While divible by q
    while (d % q == 0) {
        d /= q;
        b++;
    }

    // If d > 1
    if (d != 1)
        return -1;

    // Since, d = p^a * q^b
    return (a + b);
}

// Driver code
int main()
{
    int x = 12, y = 2592, p = 2, q = 3;

    cout << minOperations(x, y, p, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimum
    // operations required
    static int minOperations(int x, int y, int p, int q)
    {

        // Not possible
        if (y % x != 0)
            return -1;

        int d = y / x;

        // To store the greatest power
        // of p that divides d
        int a = 0;

        // While divible by p
        while (d % p == 0)
        {
            d /= p;
            a++;
        }

        // To store the greatest power
        // of q that divides d
        int b = 0;

        // While divible by q
        while (d % q == 0)
        {
            d /= q;
            b++;
        }

        // If d > 1
        if (d != 1)
            return -1;

        // Since, d = p^a * q^b
        return (a + b);
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 12, y = 2592, p = 2, q = 3;
        System.out.println(minOperations(x, y, p, q));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# operations required
def minOperations(x, y, p, q):

    # Not possible
    if (y % x != 0):
        return -1

    d = y // x

    # To store the greatest power
    # of p that divides d
    a = 0

    # While divible by p
    while (d % p == 0):
        d //= p
        a+=1

    # To store the greatest power
    # of q that divides d
    b = 0

    # While divible by q
    while (d % q == 0):
        d //= q
        b+=1

    # If d > 1
    if (d != 1):
        return -1

    # Since, d = p^a * q^b
    return (a + b)

# Driver code

x = 12
y = 2592
p = 2
q = 3

print(minOperations(x, y, p, q))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum
    // operations required
    static int minOperations(int x, int y, int p, int q)
    {

        // Not possible
        if (y % x != 0)
            return -1;

        int d = y / x;

        // To store the greatest power
        // of p that divides d
        int a = 0;

        // While divible by p
        while (d % p == 0)
        {
            d /= p;
            a++;
        }

        // To store the greatest power
        // of q that divides d
        int b = 0;

        // While divible by q
        while (d % q == 0)
        {
            d /= q;
            b++;
        }

        // If d > 1
        if (d != 1)
            return -1;

        // Since, d = p^a * q^b
        return (a + b);
    }

    // Driver code
    public static void Main ()
    {
        int x = 12, y = 2592, p = 2, q = 3;
        Console.Write(minOperations(x, y, p, q));
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum
// operations required
function minOperations(x, y, p, q){

    // Not possible
    if (y % x != 0)
        return -1

    var d = Math.floor(y / x)

    // To store the greatest power
    // of p that divides d
    var a = 0

    // While divible by p
    while (d % p == 0){
        d = Math.floor(d / p)
        a+=1
    }

    // To store the greatest power
    // of q that divides d
    var b = 0

    // While divible by q
    while (d % q == 0){
        d = Math.floor(d / q)
        b+=1
    }

    // If d > 1
    if (d != 1)
        return -1

    // Since, d = p^a * q^b
    return (a + b)

}

// Driver code
var x = 12
var y = 2592
var p = 2
var q = 3

document.write(minOperations(x, y, p, q))

// This code is contributed by AnkThon

</script>
```

**Output:** 

```
6
```