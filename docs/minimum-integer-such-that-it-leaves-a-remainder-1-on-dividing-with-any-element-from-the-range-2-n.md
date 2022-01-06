# 最小整数，在与范围[2，N]

中的任何元素相除时，余数为 1

> 原文:[https://www . geesforgeks . org/minimum-integer-so-it-leave-a-余数-1-on-division-from-2-n 中的任意元素/](https://www.geeksforgeeks.org/minimum-integer-such-that-it-leaves-a-remainder-1-on-dividing-with-any-element-from-the-range-2-n/)

给定一个整数 **N** ，任务是从范围**【2，N】**
**中找到所有 **M** 的最小可能整数 **X** 使得 **X % M = 1** 示例:**

> **输入:** N = 5
> **输出:**61
> 61% 2 = 1
> 61% 3 = 1
> 61% 4 = 1
> 61% 5 = 1
> **输入:** N = 2
> **输出:** 3

**方法:**从范围**【2，N】**中找到所有整数的 lcm，并将其存储在变量 **lcm** 中。现在我们知道 **lcm** 是可以被**【2，N】**范围内的所有元素整除的最小数，要让它在每次除法时都留下 **1** 的余数，只需加上 **1** 即可，即 **lcm + 1** 就是所需答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest number
// which on dividing with any element from
// the range [2, N] leaves a remainder of 1
long getMinNum(int N)
{
    // Find the LCM of the elements
    // from the range [2, N]
    int lcm = 1;
    for (int i = 2; i <= N; i++)
        lcm = ((i * lcm) / (__gcd(i, lcm)));

    // Return the required number
    return (lcm + 1);
}

// Driver code
int main()
{
    int N = 5;

    cout << getMinNum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the smallest number
    // which on dividing with any element from
    // the range [2, N] leaves a remainder of 1
    static long getMinNum(int N)
    {
        // Find the LCM of the elements
        // from the range [2, N]
        int lcm = 1;
        for (int i = 2; i <= N; i++)
            lcm = ((i * lcm) / (__gcd(i, lcm)));

        // Return the required number
        return (lcm + 1);
    }

    static int __gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 5;
        System.out.println(getMinNum(N));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the smallest number
# which on dividing with any element from
# the range [2, N] leaves a remainder of 1
def getMinNum(N) :

    # Find the LCM of the elements
    # from the range [2, N]
    lcm = 1;
    for i in range(2, N + 1) :
        lcm = ((i * lcm) // (gcd(i, lcm)));

    # Return the required number
    return (lcm + 1);

# Driver code
if __name__ == "__main__" :

    N = 5;

    print(getMinNum(N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the smallest number
    // which on dividing with any element from
    // the range [2, N] leaves a remainder of 1
    static long getMinNum(int N)
    {
        // Find the LCM of the elements
        // from the range [2, N]
        int lcm = 1;
        for (int i = 2; i <= N; i++)
            lcm = ((i * lcm) / (__gcd(i, lcm)));

        // Return the required number
        return (lcm + 1);
    }

    static int __gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Driver code
    public static void Main()
    {
        int N = 5;
        Console.WriteLine(getMinNum(N));
    }
}

// This code has been contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the smallest number
// which on dividing with any element from
// the range [2, N] leaves a remainder of 1
function getMinNum($N)
{
    // Find the LCM of the elements
    // from the range [2, N]
    $lcm = 1;
    for ($i = 2; $i <= $N; $i++)
        $lcm = (($i * $lcm) / (__gcd($i, $lcm)));

    // Return the required number
    return ($lcm + 1);
}

function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);
}

// Driver code

$N = 5;
echo (getMinNum($N));

// This code has been contributed by ajit....
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest number
// which on dividing with any element from
// the range [2, N] leaves a remainder of 1
function getMinNum(N)
{
    // Find the LCM of the elements
    // from the range [2, N]
    var lcm = 1;
    for (var i = 2; i <= N; i++)
        lcm = ((i * lcm) / (__gcd(i, lcm)));

    // Return the required number
    return (lcm + 1);
}

function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver code
var N = 5;
document.write( getMinNum(N));

</script>
```

**Output:** 

```
61
```

**时间复杂度:** O(N * log(N))

**辅助空间:** O(1)