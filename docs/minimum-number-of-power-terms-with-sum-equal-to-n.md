# 和等于 n 的最小幂项数

> 原文:[https://www . geesforgeks . org/最小幂项数等于 n/](https://www.geeksforgeeks.org/minimum-number-of-power-terms-with-sum-equal-to-n/)

给定两个正整数 **n** 和 **x** 。任务是将 n 表示为 x (x <sup>a1</sup> + x <sup>a2</sup> +…..+ x <sup>a3</sup> )使得 x (x <sup>a1</sup> 、x <sup>a2</sup> 、…..，x <sup>a3</sup> 应最小。打印用于使总和等于 n 的 x 的最小幂次数
示例:

```
Input : n = 5, x = 3
Output : 3
5 = 30 + 30 + 31.
We use only 3 power terms of x { 30, 30, 31} 

Input : n = 13, x = 4
Output : 4
13 = 40 + 41 + 41 + 41.
We use only four power terms of x.

Input : n = 6, x = 1
Output : 6
```

如果 x = 1，那么答案将只有 n(n = 1+1+…。n 次)。
思路是用[霍纳的方法](https://en.wikipedia.org/wiki/Horner's_method)。任何数字 n 都可以表示为，n = x * a + b 其中 0 < = b < = x-1。既然 b 在 0 到 x–1 之间，那么 b 应该表示为 x <sup>0</sup> b 次的和。
进一步 a 可以用类似的方式分解等等。
解决这个问题的算法:

```
1\. Initialize a variable ans to 0.
2\. While n > 0
   a) ans = ans + n % x
   b) n = n/x
3\. Return ans. 
```

以下是上述思路的实现:

## C++

```
// C++ program to calculate minimum number
// of powers of x to make sum equal to n.
#include <bits/stdc++.h>
using namespace std;

// Return minimum power terms of x required
int minPower(int n, int x)
{
    // if x is 1, return n since any power
    // of 1 is 1 only.
    if (x==1)
        return n;

    // Consider n = a * x  + b where a = n/x
    // and b = n % x.
    int ans = 0;
    while (n > 0)
    {
        // Update count of powers for 1's added
        ans += (n%x);

        // Repeat the process for reduced n
        n /= x;
    }

    return ans;
}

// Driven Program
int main()
{
    int n = 5, x = 3;
    cout << minPower(n, x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// minimum numberof powers of
// x to make sum equal to n.

class GFG
{
    // Return minimum power
    // terms of x required
    static int minPower(int n, int x)
    {
        // if x is 1, return n since
        // any power of 1 is 1 only.
        if (x==1)
            return n;

        // Consider n = a * x + b where
        // a = n/x and b = n % x.
        int ans = 0;
        while (n > 0)
        {
            // Update count of powers
            // for 1's added
            ans += (n % x);

            // Repeat the process for reduced n
            n /= x;
        }

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5, x = 3;
        System.out.println(minPower(n, x));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to
# calculate minimum number
# of powers of x to make
# sum equal to n.

# Return minimum power
# terms of x required
def minPower(n,x):

    # if x is 1, return
    # n since any power
    # of 1 is 1 only.
    if (x==1):
        return n

    # Consider n = a * x  + b where a = n/x
    # and b = n % x.
    ans = 0
    while (n > 0):

        # Update count of powers for 1's added
        ans += (n%x)

        # Repeat the process for reduced n
        n //= x

    return ans

# Driver code
n = 5
x = 3
print(minPower(n, x))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to calculate
// minimum numberof powers
// of x to make sum equal
// to n.
using System;

class GFG
{

    // Return minimum power
    // terms of x required
    static int minPower(int n, int x)
    {
        // if x is 1, return n since
        // any power of 1 is 1 only.
        if (x == 1)
            return n;

        // Consider n = a * x + b where
        // a = n / x and b = n % x.
        int ans = 0;
        while (n > 0)
        {
            // Update count of
            // powers for 1's
            // added
            ans += (n % x);

            // Repeat the process
            // for reduced n
            n /= x;
        }

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int n = 5, x = 3;
        Console.WriteLine(minPower(n, x));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate minimum number
// of powers of x to make sum equal to n.

// Return minimum power
// terms of x required
function minPower($n, $x)
{

    // if x is 1, return n since
    // any power of 1 is 1 only.
    if ($x == 1)
        return $n;

    // Consider n = a * x + b
    // where a = n/x and b = n % x.
    $ans = 0;
    while ($n > 0)
    {
        // Update count of powers
        // for 1's added
        $ans += ($n % $x);

        // Repeat the process
        // for reduced n
        $n /= $x;
    }

    return $ans;
}

// Driver Code
$n = 5; $x = 3;
echo(minPower($n, $x));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to calculate minimum number
// of powers of x to make sum equal to n.

// Return minimum power terms of x required
function minPower(n, x)
{
    // if x is 1, return n since any power
    // of 1 is 1 only.
    if (x==1)
        return n;

    // Consider n = a * x + b where a = n/x
    // and b = n % x.
    let ans = 0;
    while (n > 0)
    {
        // Update count of powers for 1's added
        ans += (n%x);

        // Repeat the process for reduced n
        n = Math.floor(n / x);
    }

    return ans;
}

// Driven Program

    let n = 5, x = 3;
    document.write(minPower(n, x) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
3
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。