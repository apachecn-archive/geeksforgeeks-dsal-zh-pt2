# 计数连续零对

> 原文:[https://www . geesforgeks . org/count-对连续零/](https://www.geeksforgeeks.org/count-pairs-of-consecutive-zeros/)

考虑机器上以 1 开头的序列。在每个连续的步骤中，机器同时将每个数字 0 转换为序列 10，将每个数字 1 转换为序列 01。
第一时间步后，得到序列 01；第二个之后是序列 1001，第三个之后是序列 01101001，依此类推。
n 步后序列中会出现多少对连续的零？
**例:**

```
Input : Number of steps = 3
Output: 1
// After 3rd step sequence will be  01101001

Input : Number of steps = 4
Output: 3
// After 4rd step sequence will be 1001011001101001

Input : Number of steps = 5
Output: 5
// After 3rd step sequence will be  01101001100101101001011001101001
```

这是一个简单的推理问题。如果我们非常仔细地看序列，那么我们将能够找到给定序列的模式。如果 n=1 序列将为{01}那么连续零对的数量为 0，如果 n = 2 序列将为{1001}那么连续零对的数量为 1，如果 n=3 序列将为{01101001}那么连续零对的数量为 1，
如果 n=4 序列将为{1001011001101001}那么连续零对的数量为 3。
所以序列的长度永远是 2 的幂。我们可以看到长度为 12 的序列是重复的，长度为 12。在长度为 12 的段中，总共有 2 对连续的 0。因此，我们可以推广给定的模式 q = (2^n/12)，连续零对的总数将是 2*q+1。

## C++

```
// C++ program to find number of consecutive
// 0s in a sequence
#include<bits/stdc++.h>
using namespace std;

// Function to find number of consecutive Zero Pairs
// Here n is number of steps
int consecutiveZeroPairs(int n)
{
    // Base cases
    if (n==1)
        return 0;
    if (n==2 || n==3)
        return 1;

    // Calculating how many times divisible by 12, i.e.,
    // count total number repeating segments of length 12
    int q = (pow(2, n) / 12);

    // number of consecutive Zero Pairs
    return 2 * q + 1;
}

// Driver code
int main()
{
    int n = 5;
    cout << consecutiveZeroPairs(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find number of
// consecutive 0s in a sequence
import java.io.*;
import java.math.*;

class GFG {

    // Function to find number of consecutive
    // Zero Pairs. Here n is number of steps
    static int consecutiveZeroPairs(int n)
    {
        // Base cases
        if (n == 1)
            return 0;
        if (n == 2 || n == 3)
            return 1;

        // Calculating how many times divisible
        // by 12, i.e.,count total number
        // repeating segments of length 12
        int q = ((int)(Math.pow(2, n)) / 12);

        // number of consecutive Zero Pairs
        return (2 * q + 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(consecutiveZeroPairs(n));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to find number of
# consecutive 0s in a sequence
import math

# Function to find number of consecutive
# Zero Pairs. Here n is number of steps
def consecutiveZeroPairs(n) :

    # Base cases
    if (n == 1) :
        return 0
    if (n == 2 or n == 3) :
        return 1

    # Calculating how many times divisible
    # by 12, i.e.,count total number
    # repeating segments of length 12
    q =(int) (pow(2,n) / 12)

    # number of consecutive Zero Pairs
    return 2 * q + 1

# Driver code
n = 5
print consecutiveZeroPairs(n)

#This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find number of
// consecutive 0s in a sequence
using System;

class GFG {

    // Function to find number of
    // consecutive Zero Pairs.
    // Here n is number of steps
    static int consecutiveZeroPairs(int n)
    {
        // Base cases
        if (n == 1)
            return 0;
        if (n == 2 || n == 3)
            return 1;

        // Calculating how many times divisible
        // by 12, i.e.,count total number
        // repeating segments of length 12
        int q = ((int)(Math.Pow(2, n)) / 12);

        // number of consecutive Zero Pairs
        return (2 * q + 1);
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        Console.Write(consecutiveZeroPairs(n));
    }
}

// This code is contributed by Nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of consecutive 0s in a sequence

// Function to find number
// of consecutive Zero Pairs
// Here n is number of steps
function consecutiveZeroPairs($n)
{
    // Base cases
    if ($n == 1)
        return 0;
    if ($n == 2 || $n == 3)
        return 1;

    // Calculating how many times
    // divisible by 12, i.e., count
    // total number repeating segments
    // of length 12
    $q = floor(pow(2, $n) / 12);

    // number of consecutive Zero Pairs
    return 2 * $q + 1;
}

// Driver code
$n = 5;
echo consecutiveZeroPairs($n) ;

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>
//javascript program to find number of
// consecutive 0s in a sequence

    // Function to find number of consecutive
    // Zero Pairs. Here n is number of steps
    function consecutiveZeroPairs(n)
    {
        // Base cases
        if (n == 1)
            return 0;
        if (n == 2 || n == 3)
            return 1;

        // Calculating how many times divisible
        // by 12, i.e.,count total number
        // repeating segments of length 12
        var q =(parseInt((Math.pow(2, n)) / 12));

        // number of consecutive Zero Pairs
        return (2 * q + 1);
    }

    // Driver code

        var n = 5;
        document.write(consecutiveZeroPairs(n));

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
5
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 GeeksForGeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。