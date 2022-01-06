# 用幂的和来表示一个数的计数方式

> 原文:[https://www . geesforgeks . org/count-way-express-number-sum-powers/](https://www.geeksforgeeks.org/count-ways-express-number-sum-powers/)

给定两个整数 x 和 n，我们需要找到许多方法将 x 表示为唯一自然数的 n 次幂之和。给出 1 <= n <= 20.
例:

```
Input  : x = 100
         n = 2
Output : 3
Explanation: There are three ways to 
express 100 as sum of natural numbers
raised to power 2.
100 = 10^2 = 8^2+6^2 = 1^2+3^2+4^2+5^2+7^2

Input  : x = 100
         n = 3
Output : 1
Explanation : The only combination is,
1^3 + 2^3 + 3^3 + 4^3
```

我们用递归来解决这个问题。我们首先逐一检查这个数字是否包含在总和中。

## C++

```
// C++ program to count number of ways
// to express x as sum of n-th power
// of unique natural numbers.
#include <bits/stdc++.h>
using namespace std;

// num is current num.
int countWaysUtil(int x, int n, int num)
{
    // Base cases
    int val = (x - pow(num, n));
    if (val == 0)
        return 1;
    if (val < 0)
        return 0;

    // Consider two possibilities, num is
    // included and num is not included.
    return countWaysUtil(val, n, num + 1) +
           countWaysUtil(x, n, num + 1);
}

// Returns number of ways to express
// x as sum of n-th power of two.
int countWays(int x, int n)
{
    return countWaysUtil(x, n, 1);
}

// Driver code
int main()
{
    int x = 100, n = 2;
    cout << countWays(x, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways
// to express x as sum of n-th power
// of unique natural numbers.
public class GFG {

    // num is current num.
    static int countWaysUtil(int x, int n, int num)
    {
        // Base cases
        int val = (int) (x - Math.pow(num, n));
        if (val == 0)
            return 1;
        if (val < 0)
            return 0;

        // Consider two possibilities, num is
        // included and num is not included.
        return countWaysUtil(val, n, num + 1) +
               countWaysUtil(x, n, num + 1);
    }

    // Returns number of ways to express
    // x as sum of n-th power of two.
    static int countWays(int x, int n)
    {
        return countWaysUtil(x, n, 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int x = 100, n = 2;
        System.out.println(countWays(x, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python program to count number of ways
# to express x as sum of n-th power
# of unique natural numbers.

# num is current num.
def countWaysUtil(x,n,num):

    # Base cases
    val = (x - pow(num, n))
    if (val == 0):
        return 1
    if (val < 0):
        return 0

    # Consider two possibilities, num is
    # included and num is not included.
    return countWaysUtil(val, n, num + 1) +\
           countWaysUtil(x, n, num + 1)

# Returns number of ways to express
# x as sum of n-th power of two.
def countWays(x,n):
    return countWaysUtil(x, n, 1)

# Driver code
x = 100
n = 2

print(countWays(x, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count number of ways
// to express x as sum of n-th power
// of unique natural numbers.
using System;

public class GFG {

    // num is current num.
    static int countWaysUtil(int x,
                          int n, int num)
    {

        // Base cases
        int val = (int) (x - Math.Pow(num, n));
        if (val == 0)
            return 1;
        if (val < 0)
            return 0;

        // Consider two possibilities,
        // num is included and num is
        // not included.
        return countWaysUtil(val, n, num + 1)
              + countWaysUtil(x, n, num + 1);
    }

    // Returns number of ways to express
    // x as sum of n-th power of two.
    static int countWays(int x, int n)
    {
        return countWaysUtil(x, n, 1);
    }

    // Driver code
    public static void Main()
    {
        int x = 100, n = 2;

        Console.WriteLine(countWays(x, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of ways
// to express x as sum of n-th power
// of unique natural numbers.

// num is current num.
function countWaysUtil($x, $n, $num)
{

    // Base cases
    $val = ($x - pow($num, $n));
    if ($val == 0)
        return 1;
    if ($val < 0)
        return 0;

    // Consider two possibilities, num is
    // included and num is not included.
    return (countWaysUtil($val, $n, $num + 1) +
            countWaysUtil($x, $n, $num + 1));
}

// Returns number of ways to express
// x as sum of n-th power of two.
function countWays($x, $n)
{
    return countWaysUtil($x, $n, 1);
}

// Driver code
$x = 100; $n = 2;
echo(countWays($x, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count number of ways
// to express x as sum of n-th power
// of unique natural numbers.

// num is current num.
function countWaysUtil(x, n, num)
{
    // Base cases
    let val = (x - Math.pow(num, n));
    if (val == 0)
        return 1;
    if (val < 0)
        return 0;

    // Consider two possibilities, num is
    // included and num is not included.
    return countWaysUtil(val, n, num + 1) +
        countWaysUtil(x, n, num + 1);
}

// Returns number of ways to express
// x as sum of n-th power of two.
function countWays(x, n)
{
    return countWaysUtil(x, n, 1);
}

// Driver code

    let x = 100, n = 2;
    document.write(countWays(x, n));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
3
```

本文由 **Anjali** 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。