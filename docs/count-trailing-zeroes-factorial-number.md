# 计算一个数的阶乘中的尾随零

> 原文:[https://www . geesforgeks . org/count-training-zero-factorial-number/](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)

给定一个整数 n，写一个函数，返回 n！。
**例:**

```
Input: n = 5
Output: 1 
Factorial of 5 is 120 which has one trailing 0.

Input: n = 20
Output: 4
Factorial of 20 is 2432902008176640000 which has
4 trailing zeroes.

Input: n = 100
Output: 24
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/trailing-zeroes-in-factorial5134/1)

1.  **方法:**
    一个简单的方法是首先计算 n 的阶乘，然后计算结果中尾随的 0(我们可以通过重复将阶乘除以 10 直到余数为 0 来计算尾随的 0)。

2.  由于一个数的阶乘是一个大数，上述方法可能会导致稍大的数溢出(参见上面例子中给出的 20 的阶乘)。其思想是考虑阶乘 n 的[素因子](http://en.wikipedia.org/wiki/Prime_factor)，尾随零总是由素因子 2 和 5 产生。如果我们能数出 5s 和 2s 的数量，我们的任务就完成了。考虑下面的例子。
    **n = 5:**5 的质因数中有 1 个 5 和 3 个 2s！(2 * 2 * 2 * 3 * 5).所以尾随 0 的计数是 1。
    **n = 11:**11 的质因数有 2 个 5s 和 8 个 2s！(2<sup>8</sup>* 3<sup>4</sup>* 5<sup>2</sup>* 7)。所以尾随 0 的计数是 2。

3.  我们很容易观察到质因数中 2s 的个数总是大于或等于 5s 的个数。所以如果我们把 5s 算在主要因素中，我们就完了。*如何数**n 的质因数中 5s 的总数！？*一个简单的方法是计算楼层(n/5)。比如 7！有一个 5，10！有两个 5。这事还没完，还有一件事要考虑。像 25、125 等数字有不止一个 5。比如，如果我们考虑 28！我们得到一个额外的 5，0 的数量变成 6。处理这个很简单，首先 n 除以 5 去掉所有单个 5s，然后除以 25 去掉多余的 5s，以此类推。以下是计数尾随 0 的汇总公式。

```
Trailing 0s in n! = Count of 5s in prime factors of n!
                  = floor(n/5) + floor(n/25) + floor(n/125) + ....
```

以下是基于上述公式的程序:

## C++

```
// C++ program to count
// trailing 0s in n!
#include <iostream>
using namespace std;

// Function to return trailing
// 0s in factorial of n
int findTrailingZeros(int n)
{
    if (n < 0) // Negative Number Edge Case
        return -1;

    // Initialize result
    int count = 0;

    // Keep dividing n by powers of
    // 5 and update count
    for (int i = 5; n / i >= 1; i *= 5)
        count += n / i;

    return count;
}

// Driver Code
int main()
{
    int n = 100;
    cout << "Count of trailing 0s in " << 100 << "! is "
         << findTrailingZeros(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// trailing 0s in n!
import java.io.*;

class GFG {
    // Function to return trailing
    // 0s in factorial of n
    static int findTrailingZeros(int n)
    {
        if (n < 0) // Negative Number Edge Case
            return -1;

        // Initialize result
        int count = 0;

        // Keep dividing n by powers
        // of 5 and update count
        for (int i = 5; n / i >= 1; i *= 5)
            count += n / i;

        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 100;
        System.out.println("Count of trailing 0s in " + n
                           + "! is "
                           + findTrailingZeros(n));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to
# count trailing 0s
# in n!

# Function to return
# trailing 0s in
# factorial of n

def findTrailingZeros(n):
    # Negative Number Edge Case
    if(n < 0):
        return -1

    # Initialize result
    count = 0

    # Keep dividing n by
    # 5 & update Count
    while(n >= 5):
        n //= 5
        count += n

    return count

# Driver program
n = 100
print("Count of trailing 0s " +
      "in 100! is", findTrailingZeros(n))

# This code is contributed by Uttam Singh
```

## C#

```
// C# program to count
// trailing 0s in n!
using System;

class GFG
{

    // Function to return trailing
    // 0s in factorial of n
    static int findTrailingZeros(int n)
    {

          if(n < 0) //Negative Number Edge Case
              return -1;       

        // Initialize result
        int count = 0;

        // Keep dividing n by powers
        // of 5 and update count
        for (int i = 5; n / i >= 1; i *= 5)
            count += n / i;

        return count;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 100;
        Console.WriteLine("Count of trailing 0s in " +
                                           n +"! is "+
                                findTrailingZeros(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// trailing 0s in n!

// Function to return trailing
// 0s in factorial of n
function findTrailingZeros( $n)
{

      if($n < 0) //Negative Number Edge Case
      return -1;   

    // Initialize result
    $count = 0;

    // Keep dividing n by powers
    // of 5 and update count
    for ($i = 5; $n / $i >= 1; $i *= 5)
        $count += $n / $i;

    return $count;
}

// Driver Code

$n = 100;
echo "Count of trailing 0s in " , 100,
     "! is " , findTrailingZeros($n);

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>

// JavaScript program to count
// trailing 0s in n!

// Function to return trailing
// 0s in factorial of n
function findTrailingZeros(n)
{

    if(n < 0) //Negative Number Edge Case
      return -1;

    // Initialize result
    let count = 0;

    // Keep dividing n by powers of
    // 5 and update count
    for (let i = 5; Math.floor(n / i) >= 1; i *= 5)
        count += Math.floor(n / i);

    return count;
}

// Driver Code
    let n = 100;
    document.write("Count of trailing 0s in " + 100
        + "! is " + findTrailingZeros(n));

// This code is contributed by Surbhi Tyagi

</script>
```

**输出:**

```
Count of trailing 0s in 100! is 24 
```

***时间复杂度:** O(log <sub>5</sub> n)*

***辅助空间:** O(1)*

本文由**拉胡尔·贾恩**供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论