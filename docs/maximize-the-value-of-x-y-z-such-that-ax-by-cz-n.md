# 最大化 x + y + z 的值，使得 ax + by + cz = n

> 原文:[https://www . geesforgeks . org/x-y-z-so-ax by-cz-n 最大化价值/](https://www.geeksforgeeks.org/maximize-the-value-of-x-y-z-such-that-ax-by-cz-n/)

给定整数 **n** 、 **a** 、 **b** 和 **c** ，任务是找到 **x + y + z** 的最大值，使得 **ax + by + cz = n** 。

**示例:**

> **输入:**
> n = 10
> a = 5
> b = 3
> c = 4
> **输出:**
> 3
> **解释:**
> x = 0，y = 2，z = 1
> 
> **输入:**
> n = 50
> a = 8
> b = 10
> c = 2
> **输出:**
> 25
> **说明:**
> x = 0，y = 0，z = 25

**逼近:**固定 **x** 和 **y** 的值，则 **z** 的值可以计算为**z =(n –( ax+by))/c**。如果 **z** 的当前值是整数，那么更新到目前为止找到的 **x + y + z** 的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum value of (x + y + z)
// such that (ax + by + cz = n)
int maxResult(int n, int a, int b, int c)
{
    int maxVal = 0;

    // i represents possible values of a * x
    for (int i = 0; i <= n; i += a)
    {
        // j represents possible values of b * y
        for (int j = 0; j <= n - i; j += b)
        {
            float z = (float)(n - (i + j)) / (float)(c);

            // If z is an integer
            if (floor(z) == ceil(z))
            {
                int x = i / a;
                int y = j / b;
                maxVal = max(maxVal, x + y + (int)z);
            }
        }
    }

    return maxVal;
}

// Driver code
int main()
{
    int n = 10, a = 5, b = 3, c = 4;

      // Function Call
    cout << maxResult(n, a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the maximum value of (x + y + z)
    // such that (ax + by + cz = n)
    static int maxResult(int n, int a, int b, int c)
    {
        int maxVal = 0;

        // i represents possible values of a * x
        for (int i = 0; i <= n; i += a)

            // j represents possible values of b * y
            for (int j = 0; j <= n - i; j += b) {
                float z = (float)(n - (i + j)) / (float)c;

                // If z is an integer
                if (Math.floor(z) == Math.ceil(z)) {
                    int x = i / a;
                    int y = j / b;
                    maxVal
                        = Math.max(maxVal, x + y + (int)z);
                }
            }

        return maxVal;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10, a = 5, b = 3, c = 4;

          // Function Call
        System.out.println(maxResult(n, a, b, c));
    }
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import *

# Function to return the maximum value
# of (x + y + z) such that (ax + by + cz = n)

def maxResult(n, a, b, c):
    maxVal = 0

    # i represents possible values of a * x
    for i in range(0, n + 1, a):

        # j represents possible values of b * y
        for j in range(0, n - i + 1, b):
            z = (n - (i + j)) / c

            # If z is an integer
            if (floor(z) == ceil(z)):
                x = i // a
                y = j // b
                maxVal = max(maxVal, x + y + int(z))

    return maxVal

# Driver code
if __name__ == "__main__":

    n = 10
    a = 5
    b = 3
    c = 4

    # Function Call
    print(maxResult(n, a, b, c))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the maximum value of (x + y + z)
    // such that (ax + by + cz = n)
    static int maxResult(int n, int a, int b, int c)
    {
        int maxVal = 0;

        // i represents possible values of a * x
        for (int i = 0; i <= n; i += a)

            // j represents possible values of b * y
            for (int j = 0; j <= n - i; j += b) {
                float z = (float)(n - (i + j)) / (float)c;

                // If z is an integer
                if (Math.Floor(z) == Math.Ceiling(z)) {
                    int x = i / a;
                    int y = j / b;
                    maxVal
                        = Math.Max(maxVal, x + y + (int)z);
                }
            }
        return maxVal;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 10, a = 5, b = 3, c = 4;

          // Function Call
        Console.WriteLine(maxResult(n, a, b, c));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum value of
// (x + y + z) such that (ax + by + cz = n)
function maxResult($n, $a, $b, $c)
{
    $maxVal = 0;

    // i represents possible values of a * x
    for ($i = 0; $i <= $n; $i += $a)

        // j represents possible values of b * y
        for ($j = 0; $j <= $n - $i; $j += $b)
        {
            $z = ($n - ($i + $j)) / $c;

            // If z is an integer
            if (floor($z) == ceil($z))
            {
                $x = (int)($i / $a);
                $y = (int)($j / $b);
                $maxVal = max($maxVal, $x + $y + (int)$z);
            }
        }

    return $maxVal;
}

// Driver code
$n = 10;
$a = 5;
$b = 3;
$c = 4;
echo maxResult($n, $a, $b, $c);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    // Function to return the maximum value of (x + y + z)
    // such that (ax + by + cz = n)
    function maxResult(n, a, b, c)
    {
        let maxVal = 0;

        // i represents possible values of a * x
        for (let i = 0; i <= n; i += a)

            // j represents possible values of b * y
            for (let j = 0; j <= n - i; j += b) {
                let z = (n - (i + j)) / c;

                // If z is an integer
                if (Math.floor(z) == Math.ceil(z)) {
                    let x = i / a;
                    let y = j / b;
                    maxVal
                        = Math.max(maxVal, x + y + z);
                }
            }

        return maxVal;
    }

// driver program

    let n = 10, a = 5, b = 3, c = 4;

    // Function Call
    document.write(maxResult(n, a, b, c));

</script>
```

**Output**

```
3
```

**时间复杂度:** O(N <sup>2</sup> )