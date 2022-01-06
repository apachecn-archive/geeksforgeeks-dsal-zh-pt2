# Lobb 号

> 原文:[https://www.geeksforgeeks.org/lobb-number/](https://www.geeksforgeeks.org/lobb-number/)

在组合数学中， [Lobb 数](https://en.wikipedia.org/wiki/Lobb_number) **L <sub>m，n</sub>** 计算 n + m 个开括号可以排列成一个有效的平衡括号序列的开始的次数。
Lobb 数由两个非负整数 m 和 n 参数化，n > = m > = 0。它可以通过:
![L_{m,n} = \frac{2\times m + 1}{m + n + 1}\binom{2\times n}{m + n}   ](img/b6f0fed6e88b7724532efae6ee50e9a5.png "Rendered by QuickLaTeX.com")
Lobb Number 也用于计数 n + m 个值+1 的副本和 n–m 个值-1 的副本排列成序列的方式的数量，使得该序列的所有部分和都是非负的。
**举例:**

```
Input : n = 3, m = 2
Output : 5

Input : n =5, m =3
Output :35
```

想法很简单，我们使用一个函数来计算给定值的二项式系数。利用这个函数和上面的公式，我们可以计算 Lobb 数。

## C++

```
// CPP Program to find Ln, m Lobb Number.
#include <bits/stdc++.h>
#define MAXN 109
using namespace std;

// Returns value of Binomial Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int C[n + 1][k + 1];

    // Calculate value of Binomial Coefficient in
    // bottom up manner
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= min(i, k); j++) {
            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously stored values
            else
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }

    return C[n][k];
}

// Return the Lm, n Lobb Number.
int lobb(int n, int m)
{
    return ((2 * m + 1) * binomialCoeff(2 * n, m + n)) / (m + n + 1);
}

// Driven Program
int main()
{
    int n = 5, m = 3;
    cout << lobb(n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code For Lobb Number
import java.util.*;

class GFG {

    // Returns value of Binomial
    // Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {
        int C[][] = new int[n + 1][k + 1];

        // Calculate value of Binomial
        // Coefficient in bottom up manner
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= Math.min(i, k);
                                        j++) {
                // Base Cases
                if (j == 0 || j == i)
                    C[i][j] = 1;

                // Calculate value using
                // previously stored values
                else
                    C[i][j] = C[i - 1][j - 1] +
                              C[i - 1][j];
            }
        }

        return C[n][k];
    }

    // Return the Lm, n Lobb Number.
    static int lobb(int n, int m)
    {
        return ((2 * m + 1) * binomialCoeff(2 * n, m + n)) /
                                             (m + n + 1);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 5, m = 3;
        System.out.println(lobb(n, m));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 Program to find Ln,
# m Lobb Number.

# Returns value of Binomial
# Coefficient C(n, k)
def binomialCoeff(n, k):

    C = [[0 for j in range(k + 1)]
             for i in range(n + 1)]

    # Calculate value of Binomial
    # Coefficient in bottom up manner
    for i in range(0, n + 1):
        for j in range(0, min(i, k) + 1):
            # Base Cases
            if (j == 0 or j == i):
                C[i][j] = 1

            # Calculate value using
            # previously stored values
            else:
                C[i][j] = (C[i - 1][j - 1]
                            + C[i - 1][j])

    return C[n][k]

# Return the Lm, n Lobb Number.
def lobb(n, m):

    return (((2 * m + 1) *
        binomialCoeff(2 * n, m + n))
                      / (m + n + 1))

# Driven Program
n = 5
m = 3
print(int(lobb(n, m)))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Code For Lobb Number
using System;

class GFG {

    // Returns value of Binomial
    // Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {

        int[, ] C = new int[n + 1, k + 1];

        // Calculate value of Binomial
        // Coefficient in bottom up manner
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= Math.Min(i, k);
                j++) {

                // Base Cases
                if (j == 0 || j == i)
                    C[i, j] = 1;

                // Calculate value using
                // previously stored values
                else
                    C[i, j] = C[i - 1, j - 1]
                                + C[i - 1, j];
            }
        }

        return C[n, k];
    }

    // Return the Lm, n Lobb Number.
    static int lobb(int n, int m)
    {
        return ((2 * m + 1) * binomialCoeff(
                 2 * n, m + n)) / (m + n + 1);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int n = 5, m = 3;

        Console.WriteLine(lobb(n, m));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Ln,
// m Lobb Number.

$MAXN =109;

// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff($n, $k)
{
    $C= array(array());

    // Calculate value of Binomial
    // Coefficient in bottom up manner
    for ($i = 0; $i <= $n; $i++)
    {
        for ($j = 0; $j <= min($i, $k); $j++)
        {
            // Base Cases
            if ($j == 0 || $j == $i)
                $C[$i][$j] = 1;

            // Calculate value using p
            // reviously stored values
            else
                $C[$i][$j] = $C[$i - 1][$j - 1] +
                             $C[$i - 1][$j];
        }
    }

    return $C[$n][$k];
}

// Return the Lm, n Lobb Number.
function lobb($n, int $m)
{
    return ((2 * $m + 1) *
             binomialCoeff(2 * $n, $m + $n)) /
                          ($m + $n + 1);
}

// Driven Code
$n = 5;$m = 3;
echo lobb($n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript code for Lobb Number

    // Returns value of Binomial
    // Coefficient C(n, k)
    function binomialCoeff(n, k)
    {
        let C = new Array(n + 1);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < C.length; i++) {
            C[i] = new Array(2);
        }

        // Calculate value of Binomial
        // Coefficient in bottom up manner
        for (let i = 0; i <= n; i++) {
            for (let j = 0; j <= Math.min(i, k);
                                        j++) {
                // Base Cases
                if (j == 0 || j == i)
                    C[i][j] = 1;

                // Calculate value using
                // previously stored values
                else
                    C[i][j] = C[i - 1][j - 1] +
                              C[i - 1][j];
            }
        }

        return C[n][k];
    }

    // Return the Lm, n Lobb Number.
    function lobb(n, m)
    {
        return ((2 * m + 1) * binomialCoeff(2 * n, m + n)) /
                                             (m + n + 1);
    }

// Driver code

    let n = 5, m = 3;
    document.write(lobb(n, m));

    // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
35
```