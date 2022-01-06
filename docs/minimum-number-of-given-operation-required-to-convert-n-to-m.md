# 将 n 转换为 m 所需的最小给定操作次数

> 原文:[https://www . geeksforgeeks . org/最小给定操作数-需要将 n 转换为 m/](https://www.geeksforgeeks.org/minimum-number-of-given-operation-required-to-convert-n-to-m/)

给定两个整数 **n** 和 **m** ，在一次操作中 **n** 可以乘以 **2** 或 **3** 。任务是以最少的给定操作次数将 **n** 转换为 **m** 。如果给定操作无法将 **n** 转换为 **m** ，则打印 **-1** 。
**例:**

> **输入:** n = 120，m = 51840
> **输出:**7
> 120 * 2 * 2 * 2 * 2 * 3 * 3 * 3 = 51840
> **输入:** n = 42，m = 42
> **输出:** 0
> 无需操作。
> **输入:** n = 48，m = 72
> **输出:** -1

**方法:**如果 **m** 不能被 **n** 整除，那么打印 **-1** 作为 **n** 不能用给定的操作转换为 **m** 。否则我们可以检查在除法运算中，商是否只有 **2** 和 **3** 作为质因数。如果是，那么结果将是 **2** 和 **3** 的幂之和，否则打印 **-1**
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// operations required
int minOperations(int n, int m)
{
    if (m % n != 0)
        return -1;

    int minOperations = 0;
    int q = m / n;

    // Counting all 2s
    while (q % 2 == 0) {
        q = q / 2;
        minOperations++;
    }

    // Counting all 3s
    while (q % 3 == 0) {
        q = q / 3;
        minOperations++;
    }

    // If q contained only 2 and 3
    // as the only prime factors
    // then it must be 1 now
    if (q == 1)
        return minOperations;

    return -1;
}

// Driver code
int main()
{
    int n = 120, m = 51840;
    cout << minOperations(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG {

    // Function to return the minimum
    // operations required
    static int minOperations(int n, int m)
    {
        if (m % n != 0)
            return -1;

        int minOperations = 0;
        int q = m / n;

        // Counting all 2s
        while (q % 2 == 0) {
            q = q / 2;
            minOperations++;
        }

        // Counting all 3s
        while (q % 3 == 0) {
            q = q / 3;
            minOperations++;
        }

        // If q contained only 2 and 3
        // as the only prime factors
        // then it must be 1 now
        if (q == 1)
            return minOperations;

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 120, m = 51840;
        System.out.println(minOperations(n, m));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum
# operations required
def minOperations(n, m):
    if (m % n != 0):
        return -1

    minOperations = 0
    q = int(m / n)

    # Counting all 2s
    while (q % 2 == 0):
        q = int(q / 2)
        minOperations += 1

    # Counting all 3s
    while (q % 3 == 0):
        q = int(q / 3)
        minOperations += 1

    # If q contained only 2 and 3
    # as the only prime factors
    # then it must be 1 now
    if (q == 1):
        return minOperations

    return -1

# Driver code
if __name__ == '__main__':
    n = 120
    m = 51840
    print(minOperations(n, m))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// operations required
static int minOperations(int n, int m)
{
    if (m % n != 0)
        return -1;

    int minOperations = 0;
    int q = m / n;

    // Counting all 2s
    while (q % 2 == 0)
    {
        q = q / 2;
        minOperations++;
    }

    // Counting all 3s
    while (q % 3 == 0)
    {
        q = q / 3;
        minOperations++;
    }

    // If q contained only 2 and 3
    // as the only prime factors
    // then it must be 1 now
    if (q == 1)
        return minOperations;

    return -1;
}

// Driver code
public static void Main()
{
    int n = 120, m = 51840;
    Console.WriteLine(minOperations(n, m));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// operations required
function minOperations($n, $m)
{
    if ($m % $n != 0)
        return -1;

    $minOperations = 0;
    $q = $m / $n;

    // Counting all 2s
    while ($q % 2 == 0)
    {
        $q = $q / 2;
        $minOperations++;
    }

    // Counting all 3s
    while ($q % 3 == 0)
    {
        $q = $q / 3;
        $minOperations++;
    }

    // If q contained only 2 and 3
    // as the only prime factors
    // then it must be 1 now
    if ($q == 1)
        return $minOperations;

    return -1;
}

// Driver code
$n = 120; $m = 51840;
echo(minOperations($n, $m));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the minimum
    // operations required
    function minOperations(n , m) {
        if (m % n != 0)
            return -1;

        var minOperations = 0;
        var q = m / n;

        // Counting all 2s
        while (q % 2 == 0) {
            q = q / 2;
            minOperations++;
        }

        // Counting all 3s
        while (q % 3 == 0) {
            q = q / 3;
            minOperations++;
        }

        // If q contained only 2 and 3
        // as the only prime factors
        // then it must be 1 now
        if (q == 1)
            return minOperations;

        return -1;
    }

    // Driver code

        var n = 120, m = 51840;
        document.write(minOperations(n, m));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
7
```