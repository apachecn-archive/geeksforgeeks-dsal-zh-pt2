# 给定未知数乘积的最大 GCD

> 原文:[https://www . geesforgeks . org/maximum-gcd-from-给定未知产品/](https://www.geeksforgeeks.org/maximum-gcd-from-given-product-of-unknowns/)

给定两个整数 **N** 和 **P** ，其中 **P** 是 **N** 个未知整数的乘积，任务是找出这些整数的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。可能有不同的整数组给出相同的乘积，在这种情况下，打印所有可能组中最大的 GCD。
**举例:**

> **输入:** N = 3，P = 24
> **输出:** 2
> {1，1，24}、{1，2，12}、{1，3，8}、{1，4，6}、{2，2，6}和{2，3，4}
> 是乘积= 24
> 唯一可能的整数组，它们分别有 GCDs 1，1，1，1，2 和 1。
> **输入:** N = 5，P = 1
> **输出:**

**进场:**让 **g** 成为 **a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> ，…，a <sub>n</sub>** 的 gcd。因为， **a <sub>i</sub>** 必须是 **g** 的倍数对于每个 **i** 及其产品**P = a<sub>1</sub>* a<sub>2</sub>* a<sub>3</sub>*……* a<sub>n</sub>T31】必须是**g<sup>n</sup>T35】的倍数。答案是最大 **g** 使得 **g <sup>n</sup> % P = 0** 。
让**P = k<sub>1</sub>T46】PT48<sup>1</sup>T51】k<sub>2</sub>T54】PT56<sup>2</sup>T59】k<sub>3</sub>T62】PT64<sup>3</sup>T67】*…* k<sub>n 那么 **g** 必须是**k<sub>1</sub><sup>p</sup><sub><sup>1</sup></sub><sup>'</sup>* k<sub>2</sub>T92】p<sub>T95】2</sub><sup>'</sup>* k<sub>3</sub>T102 为了最大化 **g** 我们必须选择**p<sub>I</sub><sup>'</sup>= p<sub>I</sub>/N**
以下是上述方法的实施:**</sub>****** 

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the required gcd
long max_gcd(long n, long p)
{
    int count = 0;
    long gcd = 1;

    // Count the number of times 2 divides p
    while (p % 2 == 0)
    {

        // Equivalent to p = p / 2;
        p >>= 1;
        count++;
    }

    // If 2 divides p
    if (count > 0)
        gcd *= (long)pow(2, count / n);

    // Check all the possible numbers
    // that can divide p
    for (long i = 3; i <= sqrt(p); i += 2)
    {
        count = 0;
        while (p % i == 0)
        {
            count++;
            p = p / i;
        }
        if (count > 0)
        {
            gcd *= (long)pow(i, count / n);
        }
    }

    // If n in the end is a prime number
    if (p > 2)
        gcd *= (long)pow(p, 1 / n);

    // Return the required gcd
    return gcd;
}

// Driver code
int main()
{
    long n = 3;
    long p = 80;
    cout << max_gcd(n, p);
}

// This code is contributed by Code_Mech
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the required gcd
    static long max_gcd(long n, long p)
    {
        int count = 0;
        long gcd = 1;

        // Count the number of times 2 divides p
        while (p % 2 == 0) {

            // Equivalent to p = p / 2;
            p >>= 1;
            count++;
        }

        // If 2 divides p
        if (count > 0)
            gcd *= (long)Math.pow(2, count / n);

        // Check all the possible numbers
        // that can divide p
        for (long i = 3; i <= Math.sqrt(p); i += 2) {
            count = 0;
            while (p % i == 0) {
                count++;
                p = p / i;
            }
            if (count > 0) {
                gcd *= (long)Math.pow(i, count / n);
            }
        }

        // If n in the end is a prime number
        if (p > 2)
            gcd *= (long)Math.pow(p, 1 / n);

        // Return the required gcd
        return gcd;
    }

    // Driver code
    public static void main(String[] args)
    {
        long n = 3;
        long p = 80;
        System.out.println(max_gcd(n, p));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the required gcd
def max_gcd(n, p):

    count = 0;
    gcd = 1;

    # Count the number of times 2 divides p
    while (p % 2 == 0):

        # Equivalent to p = p / 2;
        p >>= 1;
        count = count + 1;

    # If 2 divides p
    if (count > 0):
        gcd = gcd * pow(2, count // n);

    # Check all the possible numbers
    # that can divide p
    for i in range(3, (int)(math.sqrt(p)), 2):

        count = 0;
        while (p % i == 0):

            count = count + 1;
            p = p // i;

        if (count > 0):

            gcd = gcd * pow(i, count // n);

    # If n in the end is a prime number
    if (p > 2) :
        gcd = gcd * pow(p, 1 // n);

    # Return the required gcd
    return gcd;

# Driver code
n = 3;
p = 80;
print(max_gcd(n, p));

# This code is contributed by Shivi_Aggarwal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required gcd
static long max_gcd(long n, long p)
{
    int count = 0;
    long gcd = 1;

    // Count the number of times 2 divides p
    while (p % 2 == 0)
    {

        // Equivalent to p = p / 2;
        p >>= 1;
        count++;
    }

    // If 2 divides p
    if (count > 0)
        gcd *= (long)Math.Pow(2, count / n);

    // Check all the possible numbers
    // that can divide p
    for (long i = 3; i <= Math.Sqrt(p); i += 2)
    {
        count = 0;
        while (p % i == 0)
        {
            count++;
            p = p / i;
        }
        if (count > 0)
        {
            gcd *= (long)Math.Pow(i, count / n);
        }
    }

    // If n in the end is a prime number
    if (p > 2)
        gcd *= (long)Math.Pow(p, 1 / n);

    // Return the required gcd
    return gcd;
}

// Driver code
public static void Main()
{
    long n = 3;
    long p = 80;
    Console.WriteLine(max_gcd(n, p));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required gcd
function max_gcd($n, $p)
{
    $count = 0;
    $gcd = 1;

    // Count the number of times 2 divides p
    while ($p % 2 == 0)
    {

        // Equivalent to p = p / 2;
        $p >>= 1;
        $count++;
    }

    // If 2 divides p
    if ($count > 0)
        $gcd *= pow(2, (int)($count / $n));

    // Check all the possible numbers
    // that can divide p
    for ($i = 3; $i <= (int)sqrt($p); $i += 2)
    {
        $count = 0;
        while ($p % $i == 0)
        {
            $count++;
            $p = (int)($p / $i);
        }
        if ($count > 0)
        {
            $gcd *= pow($i, (int)($count / $n));
        }
    }

    // If n in the end is a prime number
    if ($p > 2)
        $gcd *= pow($p, (int)(1 / $n));

    // Return the required gcd
    return $gcd;
}

// Driver code
$n = 3;
$p = 80;
echo(max_gcd($n, $p));

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the required gcd
    function max_gcd(n, p)
    {
        let count = 0;
        let gcd = 1;

        // Count the number of times 2 divides p
        while (p % 2 == 0)
        {

            // Equivalent to p = p / 2;
            p >>= 1;
            count++;
        }

        // If 2 divides p
        if (count > 0)
            gcd *= Math.pow(2, parseInt(count / n, 10));

        // Check all the possible numbers
        // that can divide p
        for (let i = 3; i <= parseInt(Math.sqrt(p), 10); i += 2)
        {
            count = 0;
            while (p % i == 0)
            {
                count++;
                p = parseInt(p / i, 10);
            }
            if (count > 0)
            {
                gcd *= Math.pow(i, parseInt(count / n, 10));
            }
        }

        // If n in the end is a prime number
        if (p > 2)
            gcd *= Math.pow(p, parseInt(1 / n, 10));

        // Return the required gcd
        return gcd;
    }

    let n = 3;
    let p = 80;
    document.write(max_gcd(n, p));

</script>
```

**Output:** 

```
2
```