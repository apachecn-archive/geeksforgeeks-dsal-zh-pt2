# 统计不包含 3 的数字

> 原文:[https://www . geesforgeks . org/count-numbers-不包含-3/](https://www.geeksforgeeks.org/count-numbers-that-dont-contain-3/)

给定一个数字 n，编写一个函数，返回从 1 到 n 的不包含数字 3 的十进制数。
示例:

```
Input: n = 10
Output: 9 

Input: n = 45
Output: 31 
// Numbers 3, 13, 23, 30, 31, 32, 33, 34, 
// 35, 36, 37, 38, 39, 43 contain digit 3\. 

Input: n = 578
Output: 385
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/count-numbers2004/1)

**求解:**
我们可以递归求解。让 count(n)是计算这些数字的函数。

```
'msd' --> the most significant digit in n 
'd'   --> number of digits in n.

count(n) = n if n < 3

count(n) = n - 1 if 3 <= n  10 and msd is not 3

count(n) = count( msd * (10^(d-1)) - 1) 
           if n > 10 and msd is 3
```

```
Let us understand the solution with n = 578\. 
count(578) = 4*count(99) + 4 + count(78)
The middle term 4 is added to include numbers 
100, 200, 400 and 500.

Let us take n = 35 as another example.  
count(35) = count (3*10 - 1) = count(29)
```

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* returns count of numbers which are
in range from 1 to n and don't contain 3
as a digit */
int count(int n)
{
    // Base cases (Assuming n is not negative)
    if (n < 3)
        return n;
    if (n >= 3 && n < 10)
        return n-1;

    // Calculate 10^(d-1) (10 raise to the power d-1) where d is
    // number of digits in n. po will be 100 for n = 578
    int po = 1;
    while (n/po > 9)
        po = po*10;

    // find the most significant digit (msd is 5 for 578)
    int msd = n/po;

    if (msd != 3)
        // For 578, total will be 4*count(10^2 - 1) + 4 + count(78)
        return count(msd)*count(po - 1) + count(msd) + count(n%po);
    else
        // For 35, total will be equal to count(29)
        return count(msd*po - 1);
}

// Driver code
int main()
{
    cout << count(578) << " ";
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>

/* returns count of numbers which are in range from 1 to n and don't contain 3
   as a digit */
int count(int n)
{
    // Base cases (Assuming n is not negative)
    if (n < 3)
        return n;
    if (n >= 3 && n < 10)
       return n-1;

    // Calculate 10^(d-1) (10 raise to the power d-1) where d is
    // number of digits in n. po will be 100 for n = 578
    int po = 1;
    while (n/po > 9)
        po = po*10;

    // find the most significant digit (msd is 5 for 578)
    int msd = n/po;

    if (msd != 3)
      // For 578, total will be 4*count(10^2 - 1) + 4 + count(78)
      return count(msd)*count(po - 1) + count(msd) + count(n%po);
    else
      // For 35, total will be equal to count(29)
      return count(msd*po - 1);
}

// Driver program to test above function
int main()
{
    printf ("%d ", count(578));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers that not contain 3
import java.io.*;

class GFG
{
    // Function that returns count of numbers which
    // are in range from 1 to n
    // and not contain 3 as a digit
    static int count(int n)
    {
        // Base cases (Assuming n is not negative)
        if (n < 3)
            return n;
        if (n >= 3 && n < 10)
            return n-1;

        // Calculate 10^(d-1) (10 raise to the power d-1) where d is
        // number of digits in n. po will be 100 for n = 578
        int po = 1;
        while (n/po > 9)
            po = po*10;

        // find the most significant digit (msd is 5 for 578)
        int msd = n/po;

        if (msd != 3)
            // For 578, total will be 4*count(10^2 - 1) + 4 + count(78)
            return count(msd)*count(po - 1) + count(msd) + count(n%po);
        else
            // For 35, total will be equal to count(29)
            return count(msd*po - 1);
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 578;
        System.out.println(count(n));
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program to count numbers upto n that don't contain 3

# Returns count of numbers which are in range from 1 to n
# and don't contain 3 as a digit
def count(n):

    # Base Cases ( n is not negative)
    if n < 3:
        return n
    elif n >= 3 and n < 10:
        return n-1

    # Calculate 10^(d-1) ( 10 raise to the power d-1 ) where d
    # is number of digits in n. po will be 100 for n = 578

    po = 1
    while n/po > 9:
        po = po * 10

    # Find the MSD ( msd is 5 for 578 )
    msd = n/po

    if msd != 3:
        # For 578, total will be 4*count(10^2 - 1) + 4 + ccount(78)
        return count(msd) * count(po-1) + count(msd) + count(n%po)
    else:
        # For 35 total will be equal to count(29)
        return count(msd * po - 1)

# Driver Program
n = 578
print count(n)

# Contributed by Harshit Agrawal
```

## C#

```
// C# program to count numbers that not
// contain 3
using System;

class GFG {

    // Function that returns count of
    // numbers which are in range from
    // 1 to n and not contain 3 as a
    // digit
    static int count(int n)
    {

        // Base cases (Assuming n is
        // not negative)
        if (n < 3)
            return n;
        if (n >= 3 && n < 10)
            return n-1;

        // Calculate 10^(d-1) (10 raise
        // to the power d-1) where d is
        // number of digits in n. po will
        // be 100 for n = 578
        int po = 1;

        while (n / po > 9)
            po = po * 10;

        // find the most significant
        // digit (msd is 5 for 578)
        int msd = n / po;

        if (msd != 3)

            // For 578, total will be
            // 4*count(10^2 - 1) + 4 +
            // count(78)
            return count(msd) * count(po - 1)
                + count(msd) + count(n % po);
        else

            // For 35, total will be equal
            // to count(29)
            return count(msd * po - 1);
    }

    // Driver program
    public static void Main ()
    {
        int n = 578;

        Console.Write(count(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* returns count of numbers which are in range
from 1 to n and don't contain 3 as a digit */
function count1($n)
{

    // Base cases (Assuming n is not negative)
    if ($n < 3)
        return $n;
    if ($n >= 3 && $n < 10)
        return $n-1;

    // Calculate 10^(d-1) (10 raise to the
    // power d-1) where d is number of digits
    // in n. po will be 100 for n = 578
    $po = 1;
    for($x = intval($n/$po); $x > 9; $x = intval($n/$po))
        $po = $po*10;

    // find the most significant digit (msd is 5 for 578)
    $msd = intval($n / $po);

    if ($msd != 3)

    // For 578, total will be 4*count(10^2 - 1)
    // + 4 + count(78)
    return count1($msd) * count1($po - 1) +
                count1($msd) + count1($n%$po);
    else

    // For 35, total will be equal to count(29)
    return count1($msd*$po - 1);
}

// Driver program to test above function
    echo count1(578);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// javascript program to count numbers that not contain 3
    // Function that returns count of numbers which
    // are in range from 1 to n
    // and not contain 3 as a digit
    function count(n)
    {

        // Base cases (Assuming n is not negative)
        if (n < 3)
            return n;
        if (n >= 3 && n < 10)
            return n - 1;

        // Calculate 10^(d-1) (10 raise to the power d-1) where d is
        // number of digits in n. po will be 100 for n = 578
        var po = 1;
        while (parseInt(n / po) > 9)
            po = po * 10;

        // find the most significant digit (msd is 5 for 578)
        var msd = parseInt (n / po);

        if (msd != 3)

            // For 578, total will be 4*count(10^2 - 1) + 4 + count(78)
            return count(msd) * count(po - 1) + count(msd) + count(n % po);
        else

            // For 35, total will be equal to count(29)
            return count(msd * po - 1);
    }

    // Driver program
    var n = 578;
    document.write(count(n));

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
385
```

***时间复杂度:** O(log <sub>10</sub> n)*

***辅助空间:** O(1)*

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息