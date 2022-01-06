# 将偶数‘n’表示为偶数的和的计数方式

> 原文:[https://www . geesforgeks . org/count-way-express-偶数-n-sum-偶数-整数/](https://www.geeksforgeeks.org/count-ways-express-even-number-n-sum-even-integers/)

给定一个偶数正整数“n”。计算将“n”表示为偶数正整数之和的方法总数。以模 **10 <sup>9</sup> + 7**
**输出答案示例:**

```
Input: 6
Output: 4

Explanation
There are only four ways to write 6
as sum of even integers:
1\. 2 + 2 + 2
2\. 2 + 4
3\. 4 + 2
4\. 6
Input: 8
Output: 8
```

**方法**是寻找模式或递归函数，只要有可能。这种方法与已经在“[计数法中讨论过的将‘n’表示为奇数之和](https://www.geeksforgeeks.org/count-ways-express-n-sum-odd-integers/)的方法相同。这里给定的数是偶数，这意味着只有将第(n-2) <sup>个</sup>数相加两次才能得到偶数和。我们可以注意到(举几个例子)给一个数字加 2 会使计数翻倍。让写“n”的方式总数为方式(n)。‘way(n)’的值可以用公式表示如下:

```
ways(n) = ways(n-2) + ways(n-2)
ways(n) = 2 * ways(n-2)

ways(2) = 1 = 20
ways(4) = 2 = 21
ways(6) = 4 = 22
ways(8) = 8 = 23
''
''
''
ways(2 * n) = 2n-1

Replace n by (m / 2)
=> ways(m) = 2<sup>m/2 - 1</sup>
```

## C++

```
// C++ program to count ways to write
// number as sum of even integers
#include<iostream>
using namespace std;

// Initialize mod variable as constant
const int MOD = 1e9 + 7;

/* Iterative Function to calculate (x^y)%p in O(log y) */
int power(int x, unsigned int y, int p)
{
    int res = 1;      // Initialize result

    x = x % p;  // Update x if it is more than or
                // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (1LL * res * x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (1LL * x * x) % p;
    }
    return res;
}

// Return number of ways to write 'n'
// as sum of even integers
int countEvenWays(int n)
{
  return power(2, n/2 - 1, MOD);
}

// Driver code
int main()
{
    int n = 6;
    cout << countEvenWays(n) << "\n";

    n = 8;
    cout << countEvenWays(n);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to count ways to write
// number as sum of even integers

class GFG {

    // Initialize mod variable as constant
    static int MOD = 1000000007;

    /* Iterative Function to calculate
    (x^y)%p in O(log y) */
    static int power(int x, int y, int p)
    {  
        // Initialize result
        int res = 1;     

        // Update x if it is more
        // than or equal to p
        x = x % p; 

        while (y > 0)
        {
            // If y is odd, multiply x
            // with result
            if (y % 2 == 1)
                res = (1 * res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (1 * x * x) % p;
        }
        return res;
    }

    // Return number of ways to write
    // 'n' as sum of even integers
    static int countEvenWays(int n)
    {
      return power(2, n/2 - 1, MOD);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 6;
        System.out.println(countEvenWays(n));
        n = 8;
        System.out.println(countEvenWays(n));
    }
}

/* This code is contributed by Nikita Tiwari. */
```

## 计算机编程语言

```
# PYTHON program to count ways to write
# number as sum of even integers

# Initialize mod variable as constant
MOD = 1e9 + 7

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p) :
    res = 1      # Initialize result

    x = x % p  # Update x if it is more
               # than or equal to p

    while (y > 0) :

        # If y is odd, multiply x
        # with result
        if (y & 1) :
            res = (1 * res * x) % p

        # y must be even now
        y = y >> 1  # y = y/2
        x = (1 * x * x) % p

    return res

# Return number of ways to write 'n'
# as sum of even integers
def countEvenWays(n) :
    return power(2, n/2 - 1, MOD)

# Driver code
n = 6
print (int(countEvenWays(n)))
n = 8
print (int(countEvenWays(n)))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to count ways to write
// number as sum of even integers
using System;

class GFG {

    // Initialize mod variable as constant
    static int MOD = 1000000007;

    /* Iterative Function to calculate
    (x^y)%p in O(log y) */
    static int power(int x, int y, int p)
    {

        // Initialize result
        int res = 1;    

        // Update x if it is more
        // than or equal to p
        x = x % p;

        while (y > 0)
        {

            // If y is odd, multiply x
            // with result
            if (y % 2 == 1)
                res = (1 * res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (1 * x * x) % p;
        }

        return res;
    }

    // Return number of ways to write
    // 'n' as sum of even integers
    static int countEvenWays(int n)
    {
        return power(2, n/2 - 1, MOD);
    }

    // Driver code
    public static void Main()
    {
        int n = 6;
        Console.WriteLine(countEvenWays(n));

        n = 8;
        Console.WriteLine(countEvenWays(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count ways
// to write number as sum of
// even integers

// Initialize mod variable
// as constant
$MOD = 1000000000.0;

/* Iterative Function to
calculate (x^y)%p in O(log y) */
function power($x, $y, $p)
{
    // Initialize result
    $res = 1;

    // Update x if it is more
    // than or equal to p
    $x = $x % $p;

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = (1 * $res *
                        $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = (1 * $x *
                  $x) % $p;
    }
    return $res;
}

// Return number of ways
// to write 'n' as sum of
// even integers
function countEvenWays($n)
{
    global $MOD;
    return power(2, $n /
                 2 - 1, $MOD);
}

// Driver code
$n = 6;
echo countEvenWays($n), "\n";

$n = 8;
echo countEvenWays($n);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count ways to write
// number as sum of even integers

    // Initialize mod variable as constant
    let MOD = 1000000007;

    /* Iterative Function to calculate
    (x^y)%p in O(log y) */
    function power(x, y, p)
    {  
        // Initialize result
        let res = 1;     

        // Update x if it is more
        // than or equal to p
        x = x % p; 

        while (y > 0)
        {
            // If y is odd, multiply x
            // with result
            if (y % 2 == 1)
                res = (1 * res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (1 * x * x) % p;
        }
        return res;
    }

    // Return number of ways to write
    // 'n' as sum of even integers
    function countEvenWays(n)
    {
      return power(2, n/2 - 1, MOD);
    }

// Driver code

        let n = 6;
        document.write(countEvenWays(n) + "<br/>");
        n = 8;
        document.write(countEvenWays(n));

    // This code is contributed by code_hunt.
</script>
```

**输出:**

```
4
8
```

**时间复杂度:** O(Log(n))
**辅助空间:** O(1)
本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。