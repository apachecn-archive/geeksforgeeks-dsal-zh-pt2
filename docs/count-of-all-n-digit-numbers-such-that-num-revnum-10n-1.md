# 对所有 n 位数进行计数，使得 num+rev(num)= 10^n-1

> 原文:[https://www . geesforgeks . org/count-of-all-n-digits-num-revnum-10n-1/](https://www.geeksforgeeks.org/count-of-all-n-digit-numbers-such-that-num-revnum-10n-1/)

给定一个整数 **N** ，任务是找出所有 **N** 位数的个数，使得**数+Rev(num)= 10<sup>N</sup>–1**
**例:**

> **输入:** N = 2
> **输出:** 9
> 所有可能的数字为
> 18+81 = 99
> 27+72 = 99
> 36+45 = 99
> 45+54 = 99
> 54+45 = 99
> 63+54 = 99
> 72+27 = 99
> 81+18 = 99【T14

**趋近**有 2 种情况:
如果 **n 为奇数**则答案为 0。

> 假设 **n = 3** 那么 **num = d1d2d3** 和**rev(num)= d3d2d 1**T6】num+rev(num)应该是 999，因为 n = 3。
> 所以下面的等式必须满足
> D1+D3 = 9……(1)
> D2+D2 = 9……(2)
> D3+D1 = 9……(3)
> 考虑到等式 2:
> D2+D2 = 9
> 2 * D2 = 9
> D2 = 4.5 这是不可能的，因为一个数的数字应该总是一个整数。
> 因此，如果 n 为奇数，则答案为 0。

如果 **n 为偶数**，则答案为**9 * 10<sup>(N/2–1)</sup>**。

> 让 **n = 4** 然后 **num = d1d2d3d4** 和**rev(num)= d4d 3d 1**
> 所以下面的等式应该满足
> D1+D4 = 9…(1)
> D2+D3 = 9…(2)
> D3+D2 = 9…(3)
> D4+D1 = 9…(4)
> 考虑等式 1: **d1 + d4 = 9** 。有 9 种方式可以成立:
> (1 + 8)、(2 + 7)、(3 + 6)、(4 + 5)、(5 + 4)、(6 + 3)、(7 + 2)、(8 + 1)和(9 + 0)
> 类似地，其他方程也会有 9 个解+ 1 个多解，因为剩下的数字不是数字的第一个和最后一个数字，我们可以取形式的和 **(0 + 9)** 。
> 由于等式的一半是相同的
> 因此，如果 N 是偶数，那么答案将是**9 * 10<sup>(N/2–1)</sup>**。

以下是上述方法的实施

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of such numbers
int countNumbers(int n)
{

    // If n is odd
    if (n % 2 == 1)
        return 0;

    return (9 * pow(10, n / 2 - 1));
}

// Driver code
int main()
{
    int n = 2;
    cout << countNumbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the
    // count of such numbers
    static int countNumbers(int n)
    {

        // If n is odd
        if (n % 2 == 1)
            return 0;

        return (9 * (int)Math.pow(10, n / 2 - 1));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 2;
        System.out.print(countNumbers(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# count of such numbers
def countNumbers(n):

    # If n is odd
    if n % 2 == 1:
        return 0

    return (9 * pow(10, n // 2 - 1))

# Driver code
if __name__ == "__main__":

    n = 2
    print(countNumbers(n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the
    // count of such numbers
    static int countNumbers(int n)
    {

        // If n is odd
        if (n % 2 == 1)
            return 0;

        return (9 * (int)Math.Pow(10, n / 2 - 1));
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.WriteLine(countNumbers(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the
// count of such numbers
function countNumbers($n)
{

    // If n is odd
    if ($n % 2 == 1)
        return 0;

    return (9 * (int)pow(10, $n / 2 - 1));
}

// Driver code
$n = 2;
echo(countNumbers($n));

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// count of such numbers
function countNumbers(n)
{

    // If n is odd
    if (n % 2 == 1)
        return 0;

    return (9 * Math.pow(10, parseInt(n / 2) - 1));
}

// Driver code
var n = 2;
document.write(countNumbers(n));

</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(1)