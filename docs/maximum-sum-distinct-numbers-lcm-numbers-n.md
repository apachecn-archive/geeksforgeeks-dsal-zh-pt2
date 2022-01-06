# 不同数字的最大和，使得这些数字的 LCM 为 N

> 原文:[https://www . geesforgeks . org/maximum-sum-distinct-numbers-LCM-numbers-n/](https://www.geeksforgeeks.org/maximum-sum-distinct-numbers-lcm-numbers-n/)

给定一个正数 n .任务是找出不同数字的最大和，使得所有这些数字的 [LCM](https://en.wikipedia.org/wiki/Least_common_multiple) 等于 N.
**示例:**

```
Input  : 2
Output : 3
The distinct numbers you can have are 
just 1 and 2 and their sum is equal to 3.

Input  : 5
Output : 6
```

由于所有数字的 LCM 都是 N，所以所有的数字都必须是 N 的除数，所有的数字都是不同的，所以答案必须是 N 的所有除数之和。要有效地找到所有的除数，请参考文章 https://www . geeksforgeeks . org/find-自然数集的所有除数-2/

## C++

```
// C++ program to find the max sum of
// numbers whose lcm is n
#include<bits/stdc++.h>
using namespace std;

// Returns maximum sum of numbers with
// LCM as N
int maxSumLCM(int n)
{
    int max_sum = 0;  // Initialize result

    // Finding a divisor of n and adding
    // it to max_sum
    for (int i=1; i*i<=n; i++)
    {
        if (n%i == 0)
        {
            max_sum += i;
            if (n/i != i)
                max_sum += (n/i);
        }
    }

    return max_sum;
}

// Driver code
int main()
{
    int n = 2;
    cout << MaxSumLCM(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the max sum of
// numbers whose lcm is n

class MaxSum
{
    // Returns maximum sum of numbers with
    // LCM as N
    static int maxSumLCM(int n)
    {
        int max_sum = 0;  // Initialize result

        // Finding a divisor of n and adding
        // it to max_sum
        for (int i=1; i*i<=n; i++)
        {
            if (n%i == 0)
            {
                max_sum += i;
                if (n/i != i)
                    max_sum += (n/i);
            }
        }

        return max_sum;
    }

    // main function
    public static void main (String[] args)
    {
        int n = 2;
        System.out.println(maxSumLCM(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the max sum of
# numbers whose lcm is n

# Returns maximum sum of numbers with
# LCM as N
def maxSumLCM(n) :

    # Initialize result
    max_sum = 0

    # Finding a divisor of n and adding
    # it to max_sum
    i = 1
    while(i * i<= n ):
        if (n % i == 0) :
            max_sum = max_sum + i
            if (n // i != i) :
                max_sum = max_sum + (n // i)
        i = i + 1

    return max_sum

# Driver code
n = 2
print(maxSumLCM(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find the max sum
// of numbers whose lcm is n
using System;

class MaxSum
{

    // Returns maximum sum of 
    // numbers with LCM as N
    static int maxSumLCM(int n)
    {

         // Initialize result
         int max_sum = 0;

        // Finding a divisor of n and
        // adding it to max_sum
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                max_sum += i;
                if (n / i != i)
                    max_sum += (n / i);
            }
        }

        return max_sum;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int n = 2;
        Console.Write(maxSumLCM(n));
    }
}

// This code is contributed by parashar..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the max sum of numbers
// whose lcm is n

// Returns maximum sum
// of numbers with
// LCM as N
function maxSumLCM($n)
{
    // Initialize result
    $max_sum = 0;

    // Finding a divisor
    // of n and adding
    // it to max_sum
    for ($i = 1;
         $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            $max_sum += $i;
            if ($n / $i != $i)
                $max_sum += ($n / $i);
        }
    }

    return $max_sum;
}

// Driver code
$n = 2;
echo MaxSumLCM($n);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the max sum of
// numbers whose lcm is n

// Returns maximum sum of numbers with
// LCM as N
function maxSumLCM(n)
{
    let max_sum = 0; // Initialize result

    // Finding a divisor of n and adding
    // it to max_sum
    for (let i=1; i*i<=n; i++)
    {
        if (n%i == 0)
        {
            max_sum += i;
            if (n/i != i)
                max_sum += (n/i);
        }
    }

    return max_sum;
}

// Driver code

    let n = 2;
    document.write(maxSumLCM(n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
3
```

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。