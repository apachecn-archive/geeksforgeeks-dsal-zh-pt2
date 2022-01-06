# 用连续的 1 计数字符串

> 原文:[https://www . geesforgeks . org/count-strings-with-continuous-1s/](https://www.geeksforgeeks.org/count-strings-with-consecutive-1s/)

给定一个数字 n，计算其中有连续 1 的 n 个长度字符串的数量。

**示例:**

```
Input  : n = 2
Output : 1
There are 4 strings of length 2, the
strings are 00, 01, 10 and 11\. Only the 
string 11 has consecutive 1's.

Input  : n = 3
Output : 3
There are 8 strings of length 3, the
strings are 000, 001, 010, 011, 100, 
101, 110 and 111\.  The strings with
consecutive 1's are 011, 110 and 111.

Input : n = 5
Output : 19
```

没有连续 1 的串计数的反问题可以用动态规划解决(见此处的解决方案)。我们可以使用该解决方案，并通过以下步骤找到所需的计数。

1.  使用这里[讨论的方法](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/)计算没有连续 1 的二进制字符串的数量**。让这个数成为 **c** 。**
2.  具有连续 1 的所有可能的二进制字符串的计数是 2^n，其中 n 是输入长度。
3.  连续 1 的二进制字符串总数是 2^n–c。

下面是上述步骤的实现。

## C++

```
// C++ program to count all distinct
// binary strings with two consecutive 1's
#include <iostream>
using namespace std;

// Returns count of n length binary
// strings with consecutive 1's
int countStrings(int n)
{
    // Count binary strings without consecutive 1's.
    // See the approach discussed on be
    // ( http://goo.gl/p8A3sW )
    int a[n], b[n];
    a[0] = b[0] = 1;
    for (int i = 1; i < n; i++)
    {
        a[i] = a[i - 1] + b[i - 1];
        b[i] = a[i - 1];
    }

    // Subtract a[n-1]+b[n-1] from 2^n
    return (1 << n) - a[n - 1] - b[n - 1];
}

// Driver code
int main()
{
    cout << countStrings(5) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all distinct
// binary strings with two consecutive 1's

class GFG {

    // Returns count of n length binary
    // strings with consecutive 1's
    static int countStrings(int n)
    {
        // Count binary strings without consecutive 1's.
        // See the approach discussed on be
        // ( http://goo.gl/p8A3sW )
        int a[] = new int[n], b[] = new int[n];
        a[0] = b[0] = 1;

        for (int i = 1; i < n; i++) {
            a[i] = a[i - 1] + b[i - 1];
            b[i] = a[i - 1];
        }

        // Subtract a[n-1]+b[n-1]
        from 2 ^ n return (1 << n) - a[n - 1] - b[n - 1];
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.println(countStrings(5));
    }
}

// This code is contributed by Nikita tiwari.
```

## 蟒蛇 3

```
# Python 3 program to count all
# distinct binary strings with
# two consecutive 1's

# Returns count of n length
# binary strings with
# consecutive 1's
def countStrings(n):

    # Count binary strings without
    # consecutive 1's.
    # See the approach discussed on be
    # ( http://goo.gl/p8A3sW )
    a = [0] * n
    b = [0] * n
    a[0] = b[0] = 1
    for i in range(1, n):
        a[i] = a[i - 1] + b[i - 1]
        b[i] = a[i - 1]

    # Subtract a[n-1]+b[n-1] from 2^n
    return (1 << n) - a[n - 1] - b[n - 1]

# Driver code
print(countStrings(5))

# This code is contributed
# by Nikita tiwari.
```

## C#

```
// program to count all distinct
// binary strings with two
// consecutive 1's
using System;

class GFG {

    // Returns count of n length
    // binary strings with
    // consecutive 1's
    static int countStrings(int n)
    {
        // Count binary strings without
        // consecutive 1's.
        // See the approach discussed on
        // ( http://goo.gl/p8A3sW )
        int[] a = new int[n];
        int[] b = new int[n];
        a[0] = b[0] = 1;

        for (int i = 1; i < n; i++)
        {
            a[i] = a[i - 1] + b[i - 1];
            b[i] = a[i - 1];
        }

        // Subtract a[n-1]+b[n-1]
        // from 2^n
        return (1 << n) - a[n - 1] - b[n - 1];
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(countStrings(5));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all
// distinct binary strings
// with two consecutive 1's
// Returns count of n length binary
// strings with consecutive 1's

function countStrings($n)
{

    // Count binary strings without consecutive 1's.
    // See the approach discussed on be
    // ( http://goo.gl/p8A3sW )
    $a[$n] = 0;
    $b[$n] = 0;
    $a[0] = $b[0] = 1;
    for ($i = 1; $i < $n; $i++)
    {
        $a[$i] = $a[$i - 1] + $b[$i - 1];
        $b[$i] = $a[$i - 1];
    }

    // Subtract a[n-1]+b[n-1] from 2^n
    return (1 << $n) - $a[$n - 1] -
                       $b[$n - 1];
}

    // Driver Code
    echo countStrings(5), "\n";

// This Code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to count all distinct
// binary strings with two
// consecutive 1's

    // Returns count of n length binary
    // strings with consecutive 1's
    function countStrings(n)
    {
        // Count binary strings without consecutive 1's.
        // See the approach discussed on be
        // ( http://goo.gl/p8A3sW )
        let a = [], b = [];
        a[0] = b[0] = 1;

        for (let i = 1; i < n; i++) {
            a[i] = a[i - 1] + b[i - 1];
            b[i] = a[i - 1];
        }

        // Subtract a[n-1]+b[n-1]
        // from 2 ^ n
        return (1 << n) - a[n - 1] - b[n - 1];
    }

// Driver Code

       document.write(countStrings(5));

</script>
```

**Output**

```
19
```

***时间复杂度:** O(n)*

***辅助空间:** O(n)*

**优化:**
上述解的时间复杂度为 O(n)。我们可以优化上述解决方案，使其在 O(Logn)中工作。
如果我们仔细观察没有连续 1 的计数字符串的模式，我们可以观察到计数实际上是(n+2) <sup>第</sup>个斐波那契数为 n > = 1。斐波那契数列是 0，1，1，2，3，5，8，13，21，34，55，89，141，…

```
n = 1, count = 0  = 21 - fib(3) 
n = 2, count = 1  = 22 - fib(4)
n = 3, count = 3  = 23 - fib(5)
n = 4, count = 8  = 24 - fib(6)
n = 5, count = 19 = 25 - fib(7)
................
```

我们可以在 O(Log n)时间内找到第 n 个斐波那契数(见这里的方法 4)。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息