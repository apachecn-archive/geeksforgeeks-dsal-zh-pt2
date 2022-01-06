# 将 n 转换为 m 所需的最小运算次数| Set-2

> 原文:[https://www . geesforgeks . org/最小数量-操作-要求-转换-n-m-set-2/](https://www.geeksforgeeks.org/minimum-number-operations-required-to-convert-n-to-m-set-2/)

给定两个整数 **n** 和 **m** 和 **a** 和 **b** ，在一次操作中 **n** 可以乘以 **a** 或 **b** 。任务是以最少的给定操作次数将 **n** 转换为 **m** 。如果无法通过给定的操作将 n 转换为 m，则打印-1。

**示例:**

```
Input: n = 120, m = 51840, a = 2, b = 3
Output: 7
120 * 2 * 2 * 2 * 2 * 3 * 3 * 3 = 51840

Input: n = 10, m = 50, a = 5, b = 7
Output: 1
10 * 5 = 50 
```

在 [**之前的帖子**](https://www.geeksforgeeks.org/minimum-number-of-given-operation-required-to-convert-n-to-m/) 中，我们讨论了一种使用除法的方法。
在这篇文章中，我们将使用一种方法，使用递归找到最小操作数。递归将由两个状态组成，数字乘以 a 或 b，并计算步数。这两个步骤中最少的一步就是答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAXN 10000000

// Function to find the minimum number of steps
int minimumSteps(int n, int m, int a, int b)
{
    // If n exceeds M
    if (n > m)
        return MAXN;

    // If N reaches the target
    if (n == m)
        return 0;

    // The minimum of both the states
    // will be the answer
    return min(1 + minimumSteps(n * a, m, a, b),
               1 + minimumSteps(n * b, m, a, b));
}

// Driver code
int main()
{
    int n = 120, m = 51840;
    int a = 2, b = 3;
    cout << minimumSteps(n, m, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    static int MAXN = 10000000;

    // Function to find the minimum number of steps
    static int minimumSteps(int n, int m, int a, int b)
    {
        // If n exceeds M
        if (n > m)
            return MAXN;

        // If N reaches the target
        if (n == m)
            return 0;

        // The minimum of both the states
        // will be the answer
        return Math.min(1 + minimumSteps(n * a, m, a, b),
                1 + minimumSteps(n * b, m, a, b));
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 120, m = 51840;
        int a = 2, b = 3;
        System.out.println(minimumSteps(n, m, a, b));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
MAXN = 10000000

# Function to find the minimum
# number of steps
def minimumSteps(n, m, a, b):

    # If n exceeds M
    if (n > m):
        return MAXN

    # If N reaches the target
    if (n == m):
        return 0

    # The minimum of both the states
    # will be the answer
    return min(1 + minimumSteps(n * a, m, a, b),
               1 + minimumSteps(n * b, m, a, b))

# Driver code
if __name__ == '__main__':
    n = 120
    m = 51840
    a = 2
    b = 3
    print(minimumSteps(n, m, a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int MAXN = 10000000;

    // Function to find the minimum number of steps
    static int minimumSteps(int n, int m, int a, int b)
    {
        // If n exceeds M
        if (n > m)
            return MAXN;

        // If N reaches the target
        if (n == m)
            return 0;

        // The minimum of both the states
        // will be the answer
        return Math.Min(1 + minimumSteps(n * a, m, a, b),
                1 + minimumSteps(n * b, m, a, b));
    }

    // Driver code
    public static void Main ()
    {
        int n = 120, m = 51840;
        int a = 2, b = 3;
        Console.WriteLine(minimumSteps(n, m, a, b));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$MAXN = 10000000;

// Function to find the minimum number of steps
function minimumSteps($n, $m, $a, $b)
{
    global $MAXN;

    // If n exceeds M
    if ($n > $m)
        return $MAXN;

    // If N reaches the target
    if ($n == $m)
        return 0;

    // The minimum of both the states
    // will be the answer
    return min(1 + minimumSteps($n * $a, $m, $a, $b),
               1 + minimumSteps($n * $b, $m, $a, $b));
}

// Driver code
$n = 120; $m = 51840;
$a = 2; $b = 3;
echo minimumSteps($n, $m, $a, $b);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    var MAXN = 10000000;

    // Function to find the minimum number of steps
    function minimumSteps(n , m , a , b) {
        // If n exceeds M
        if (n > m)
            return MAXN;

        // If N reaches the target
        if (n == m)
            return 0;

        // The minimum of both the states
        // will be the answer
        return Math.min(1 + minimumSteps(n * a, m, a, b),
        1 + minimumSteps(n * b, m, a, b));
    }

    // Driver code

        var n = 120, m = 51840;
        var a = 2, b = 3;
        document.write(minimumSteps(n, m, a, b));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
7
```