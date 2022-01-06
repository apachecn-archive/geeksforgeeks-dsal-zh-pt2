# 使用从 1 到 n 的 K 个数字的最大异或

> 原文:[https://www . geesforgeks . org/maximum-xor-using-k-numbers-1-n/](https://www.geeksforgeeks.org/maximum-xor-using-k-numbers-1-n/)

给定一个正整数 n 和 k，用最多 k 个数求 1 到 n 的最大异或。1 与 n 的异或和定义为 1 ^ 2 ^ 3 ^ … ^ n.
**例:**

```
Input :  n = 4, k = 3
Output : 7
Explanation
Maximum possible xor sum is 1 ^ 2 ^ 4 = 7.

Input : n = 11, k = 1
Output : 11
Explanation
Maximum Possible xor sum is 11.
```

如果我们有 k = 1，那么最大可能的异或和就是“n”本身。现在，对于 k > 1，我们总是可以设置一个数字的所有位，直到“n”中的最高有效设置位。

## C++

```
// CPP program to find max xor sum
// of 1 to n using atmost k numbers
#include <bits/stdc++.h>
using namespace std;

// To return max xor sum of 1 to n
// using at most k numbers
int maxXorSum(int n, int k)
{
    // If k is 1 then maximum
    // possible sum is n
    if (k == 1)
        return n;

    // Finding number greater than
    // or equal to n with most significant
    // bit same as n. For example, if n is
    // 4, result is 7\. If n is 5 or 6, result
    // is 7
    int res = 1;
    while (res <= n)
        res <<= 1;

    // Return res - 1 which denotes
    // a number with all bits set to 1
    return res - 1;
}

// Driver program
int main()
{
    int n = 4, k = 3;
    cout << maxXorSum(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find max xor sum
// of 1 to n using atmost k numbers
public class Main {

    // To return max xor sum of 1 to n
    // using at most k numbers
    static int maxXorSum(int n, int k)
    {
        // If k is 1 then maximum
        // possible sum is n
        if (k == 1)
            return n;

        // Finding number greater than
        // or equal to n with most significant
        // bit same as n. For example, if n is
        // 4, result is 7\. If n is 5 or 6, result
        // is 7
        int res = 1;
        while (res <= n)
            res <<= 1;

        // Return res - 1 which denotes
        // a number with all bits set to 1
        return res - 1;
    }

    // Driver program to test maxXorSum()
    public static void main(String[] args)
    {
        int n = 4, k = 3;
        System.out.print(maxXorSum(n, k));
    }
}
```

## 计算机编程语言

```
# Python3 code to find max xor sum
# of 1 to n using atmost k numbers

# To return max xor sum of 1 to n
# using at most k numbers
def maxXorSum( n , k ):
    # If k is 1 then maximum
    # possible sum is n
    if k == 1:
        return n

    # Finding number greater than
    # or equal to n with most significant
    # bit same as n. For example, if n is
    # 4, result is 7\. If n is 5 or 6, result
    # is 7
    res = 1
    while res <= n:
        res <<= 1

    # Return res - 1 which denotes
    # a number with all bits set to 1
    return res - 1

# Driver code
n = 4
k = 3
print( maxXorSum(n, k) )

# This code is contributed by Abhishek Sharma44.
```

## C#

```
// C# program to find max xor sum
// of 1 to n using atmost k numbers
using System;

public class main {

    // To return max xor sum of 1 to n
    // using at most k numbers
    static int maxXorSum(int n, int k)
    {
        // If k is 1 then maximum
        // possible sum is n
        if (k == 1)
            return n;

        // Finding number greater than
        // or equal to n with most significant
        // bit same as n. For example, if n is
        // 4, result is 7\. If n is 5 or 6, result
        // is 7
        int res = 1;
        while (res <= n)
            res <<= 1;

        // Return res - 1 which denotes
        // a number with all bits set to 1
        return res - 1;
    }

    // Driver program
    public static void Main()
    {
        int n = 4, k = 3;
        Console.WriteLine(maxXorSum(n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find max xor sum
// of 1 to n using atmost k numbers

// To return max xor sum of 1 to n
// using at most k numbers
function maxXorSum($n, $k)
{
    // If k is 1 then maximum
    // possible sum is n
    if ($k == 1)
        return $n;

    // Finding number greater than
    // or equal to n with most
    // significant bit same as n.
    // For example, if n is 4, result
    // is 7\. If n is 5 or 6, result is 7
    $res = 1;
    while ($res <= $n)
        $res <<= 1;

    // Return res - 1 which denotes
    // a number with all bits set to 1
    return $res - 1;
}

// Driver code
$n = 4;
$k = 3;
echo maxXorSum($n, $k);

// This code is contributed by Mithun Kumar
?>
```

## java 描述语言

```
<script>

// JavaScript program to find max xor sum
// of 1 to n using atmost k numbers

    // To return max xor sum of 1 to n
    // using at most k numbers
    function maxXorSum(n, k)
    {
        // If k is 1 then maximum
        // possible sum is n
        if (k == 1)
            return n;

        // Finding number greater than
        // or equal to n with most significant
        // bit same as n. For example, if n is
        // 4, result is 7\. If n is 5 or 6, result
        // is 7
        let res = 1;
        while (res <= n)
            res <<= 1;

        // Return res - 1 which denotes
        // a number with all bits set to 1
        return res - 1;
    }

// Driver code

        let n = 4, k = 3;
        document.write(maxXorSum(n, k));

</script>
```

**输出:**

```
7
```