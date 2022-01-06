# 使用给定数量的设定位的最小数量

> 原文:[https://www . geesforgeks . org/最小使用位数-给定位数/](https://www.geeksforgeeks.org/minimum-number-using-set-bits-given-number/)

给定一个无符号数，用给定的无符号数的位数找出可以构成的最小数。
**例:**

> 输入:6
> 输出:3
> 6 的二进制表示为 0000…0110。具有相同设置位数的最小数字 0000…0011。
> 
> 输入:11
> 输出:7

**简单方法:**
1。使用简单的十进制到二进制表示技术找到数字的二进制表示。
2。计数二进制表示中等于“n”的设置位数。
3。创建一个二进制表示，其“n”个最低有效位设置为 1。
4。将二进制表示转换回数字。
**高效途径:**
1。只需测量数字的位表示中存在的 1 的个数。
2。(设置位数增加到 2 的幂)–1 代表最小化数。

## C++

```
// An efficient C++ program to find
// minimum number formed by bits of a given number.
#include <bits/stdc++.h>
#define ll unsigned int
using namespace std;

// Returns minimum number formed by
// bits of a given number.
ll minimize(ll a)
{
    // _popcnt32(a) gives number of 1's
    // present in binary representation
    // of a.
    ll n = _popcnt32(a);

    return (pow(2, n) - 1);
}

// Driver function.
int main()
{
    ll a = 11;
    cout << minimize(a) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to
// find minimum number formed
// by bits of a given number.
import java.io.*;

class GFG
{
    public static int _popcnt32(long number)
    {
        int count = 0;
        while (number > 0)
        {
            count += number & 1L;
            number >>= 1L;
        }
        return count;
    }

    // Returns minimum number formed
    // by bits of a given number.
    static long minimize(long a)
    {
        // _popcnt32(a) gives number
        // of 1's present in binary
        // representation of a.
        int n = _popcnt32(a);

        return ((long)Math.pow(2, n) - 1);
    }

    // Driver Code.
    public static void main(String args[])
    {
        long a = 11;
        System.out.print(minimize(a));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# An efficient Python3 program
# to find minimum number formed
# by bits of a given number.

# Returns minimum number formed by
# bits of a given number.
def minimize(a):

    # _popcnt32(a) gives number of 1's
    # present in binary representation
    # of a.
    n = bin(a).count("1")

    return (pow(2, n) - 1)

# Driver Code
a = 11
print(minimize(a))

# This code is contributed by Mohit Kumar
```

## C#

```
// An efficient C# program to
// find minimum number formed
// by bits of a given number.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{
    // Returns minimum number formed
    // by bits of a given number.
    static long minimize(long a)
    {
        // _popcnt32(a) gives number
        // of 1's present in binary 
        // representation of a.
        string binaryString = Convert.ToString(a, 2);
        int n = binaryString.Split(new [] {'0'},
                StringSplitOptions.RemoveEmptyEntries).Length + 1;

        return ((long)Math.Pow(2, n) - 1);
    }

    // Driver Code.
    static void Main()
    {
        long a = 11;
        Console.Write(minimize(a));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>
// An efficient Javascript program to
// find minimum number formed
// by bits of a given number.

    function _popcnt32(number)
    {
        let count = 0;
        while (number > 0)
        {
            count += number & 1;
            number >>= 1;
        }
        return count;
    }

    // Returns minimum number formed
    // by bits of a given number.
    function minimize(a)
    {

        // _popcnt32(a) gives number
        // of 1's present in binary
        // representation of a.
        let n = _popcnt32(a);

        return (Math.pow(2, n) - 1);
    }

    // Driver Code.
    let a = 11;
    document.write(minimize(a));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
7
```

**注意:**以上代码使用了 GCC 特有的功能。如果我们希望为其他编译器编写代码，我们可以使用整数中的计数集位。