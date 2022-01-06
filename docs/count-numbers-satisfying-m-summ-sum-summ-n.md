# 满足 m +和(m) +和(和(m)) = N 的数的计数

> 原文:[https://www . geeksforgeeks . org/count-numbers-coming-m-sum-sum-sum-n/](https://www.geeksforgeeks.org/count-numbers-satisfying-m-summ-sum-summ-n/)

给定一个整数 N，求满足条件 **m + sum(m) + sum (sum(m)) = N，**的数(m)的个数，其中 sum(m)表示 m 中的位数之和，给定 N < = 10e9。
示例:

```
Input: 9
Output: 1
Explanation: Only 1 positive integer satisfies 
             the condition that is 3, 
            3 + sum(3) + sum(sum(3)) = 3 + 3 + 3 
                                     = 9 

Input: 9939
Output: 4
Explanation: m can be 9898, 9907, 9910 and 9913\. 
             9898 + sum(9898) + sum(sum(9898))  
              = 9898 + 34 + 7 = 9939.
             9907 + sum(9907) + sum(sum(9907)) 
              = 9907 + 25 + 7 = 9939.
             9910 + sum(9910) + sum(sum(9910)) 
              = 9910 + 19 + 10 = 9939.
             9913 + sum(9913) + sum(sum(9913))  
              = 9913 + 22 + 4 = 9939\.  
```

**方法:**首先要注意的是，我们被赋予了约束 N < =10e9。这意味着总和(x)对于任何数字最多可以是 81，这是因为 10e9 以下的最大数字是 999999999，其数字加起来是 81。sum(sum(x))的最大值为 16(数字为 79 < =81)，因此最大值为 81 + 16，即 97 需要检查。我们只需要从 N–97 迭代到 N，检查哪些整数满足方程，因为小于 N-97 的整数不能满足方程，大于 N 的整数也不能满足方程。
以下是上述办法的实施情况。

## C++

```
// CPP program to count numbers
// satisfying equation.
#include <bits/stdc++.h>
using namespace std;

// function that returns sum of
// digits in a number
int sum(int n)
{
    int rem = 0;

    // initially sum of digits is 0
    int sum_of_digits = 0;

    // loop runs till all digits
    // have been extracted
    while (n > 0) {

        // last digit from backside
        rem = n % 10;

        // sums up the digits
        sum_of_digits += rem;

        // the number is reduced to the
        // number removing the last digit
        n = n / 10;
    }

    // returns the sum of digits in a number
    return sum_of_digits;
}

// function to calculate the count of
// such occurrences
int count(int n)
{
    // counter to calculate the occurrences
    int c = 0;

    // loop to traverse from n-97 to n
    for (int i = n - 97; i <= n; i++) {

        // calls the function to calculate
        // the sum of digits of i
        int a = sum(i);

        // calls the function to calculate
        // the sum of digits of a
        int b = sum(a);

        // if the summation is equal to n
        // then increase counter by 1
        if ((i + a + b) == n) {
            c += 1;
        }
    }

    // returns the count
    return c;
}

// driver program to test the above function
int main()
{
    int n = 9939;

    // calls the function to get the answer
    cout << count(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers
// satisfying equation.
import java.io.*;

class GFG {

    // function that returns sum of
    // digits in a number
    static int sum(int n)
    {
        int rem = 0;

        // initially sum of digits is 0
        int sum_of_digits = 0;

        // loop runs till all digits
        // have been extracted
        while (n > 0)
        {

            // last digit from backside
            rem = n % 10;

            // sums up the digits
            sum_of_digits += rem;

            // the number is reduced to the
            // number removing the last digit
            n = n / 10;
        }

        // returns the sum of digits in a number
        return sum_of_digits;
    }

    // function to calculate the count of
    // such occurrences
    static int count(int n)
    {
        // counter to calculate the occurrences
        int c = 0;

        // loop to traverse from n-97 to n
        for (int i = n - 97; i <= n; i++)
        {

            // calls the function to calculate
            // the sum of digits of i
            int a = sum(i);

            // calls the function to calculate
            // the sum of digits of a
            int b = sum(a);

            // if the summation is equal to n
            // then increase counter by 1
            if ((i + a + b) == n)
            {
                c += 1;
            }
        }

        // returns the count
        return c;
    }

    // driver program to test the above function
    public static void main (String[] args)
    {
        int n = 9939;
        // calls the function to get the answer
        System.out.println ( count(n) );

    }
}

// This article is contributed by vt_m
```

## 蟒蛇 3

```
# Python program
# to count numbers
# satisfying equation.

# function that returns sum of
# digits in a number
def sum(n):

    rem = 0

    #initially sum of digits is 0
    sum_of_digits = 0

    # loop runs till all digits
    # have been extracted
    while (n > 0):

        # last digit from backside
        rem = n % 10

        # sums up the digits
        sum_of_digits += rem

        # the number is reduced to the
        # number removing the last digit
        n = n // 10

    # returns the sum
    # of digits in a number
    return sum_of_digits

# function to calculate
# the count of
# such occurrences
def count(n):

    # counter to calculate the occurrences
    c = 0

    # loop to traverse from n - 97 to n
    for i in range(n - 97,n+1):

        # calls the function to calculate
        # the sum of digits of i
        a = sum(i)

        # calls the function to calculate
        # the sum of digits of a
        b = sum(a)

        # if the summation is equal to n
        # then increase counter by 1
        if ((i + a + b) == n):
            c += 1

    # returns the count
    return c

# driver program to test
# the above function

n = 9939

# calls the function
# to get the answer
print(count(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count numbers
// satisfying equation.
using System;

class GFG {

    // function that returns sum 
    // of digits in a number
    static int sum(int n)
    {
        int rem = 0;

        // initially sum of
        // digits is 0
        int sum_of_digits = 0;

        // loop runs till all digits
        // have been extracted
        while (n > 0)
        {
            // last digit from
            // backside
            rem = n % 10;

            // sums up the digits
            sum_of_digits += rem;

            // the number is reduced
            // to the number removing
            // the last digit
            n = n / 10;
        }

        // returns the sum of
        // digits in a number
        return sum_of_digits;
    }

    // function to calculate the
    // count of such occurrences
    static int count(int n)
    {

        // counter to calculate
        // the occurrences
        int c = 0;

        // loop to traverse from n-97 to n
        for (int i = n - 97; i <= n; i++)
        {

            // calls the function to calculate
            // the sum of digits of i
            int a = sum(i);

            // calls the function to calculate
            // the sum of digits of a
            int b = sum(a);

            // if the summation is equal to n
            // then increase counter by 1
            if ((i + a + b) == n)
            {
                c += 1;
            }
        }

        // returns the count
        return c;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 9939;

        // calling the function
        Console.Write ( count(n) );

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers
// satisfying equation.

// function that returns sum of
// digits in a number
function sum($n)
{
    $rem = 0;

    // initially sum of
    // digits is 0
    $sum_of_digits = 0;

    // loop runs till all digits
    // have been extracted
    while ($n > 0)
    {

        // last digit from backside
        $rem = $n % 10;

        // sums up the digits
        $sum_of_digits += $rem;

        // the number is reduced to the
        // number removing the last digit
        $n = $n / 10;
    }

    // returns the sum of
    // digits in a number
    return $sum_of_digits;
}

// function to calculate the
// count of such occurrences
function countt($n)
{

    // counter to calculate
    // the occurrences
    $c = 0;

    // loop to traverse
    // from n-97 to n
    for ($i = $n - 97; $i <= $n; $i++)
    {

        // calls the function to calculate
        // the sum of digits of i
        $a = sum($i);

        // calls the function to calculate
        // the sum of digits of a
        $b = sum($a);

        // if the summation is equal to n
        // then increase counter by 1
        if (($i + $a + $b) == $n)
        {
            $c += 1;
        }
    }

    // returns the count
    return $c;
}

    // Driver Code
    $n = 9939;

    // calls the function
    // to get the answer
    echo countt($n) ;

//This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript program to count numbers
// satisfying equation.

    // function that returns sum of
    // digits in a number
    function sum(n)
    {
        var rem = 0;

        // initially sum of digits is 0
        var sum_of_digits = 0;

        // loop runs till all digits
        // have been extracted
        while (n > 0)
        {

            // last digit from backside
            rem = n % 10;

            // sums up the digits
            sum_of_digits += rem;

            // the number is reduced to the
            // number removing the last digit
            n = parseInt(n / 10);
        }

        // returns the sum of digits in a number
        return sum_of_digits;
    }

    // function to calculate the count of
    // such occurrences
    function count(n)
    {

        // counter to calculate the occurrences
        var c = 0;

        // loop to traverse from n-97 to n
        for (i = n - 97; i <= n; i++)
        {

            // calls the function to calculate
            // the sum of digits of i
            var a = sum(i);

            // calls the function to calculate
            // the sum of digits of a
            var b = sum(a);

            // if the summation is equal to n
            // then increase counter by 1
            if ((i + a + b) == n) {
                c += 1;
            }
        }

        // returns the count
        return c;
    }

    // driver program to test the above function   
        var n = 9939;

        // calls the function to get the answer
        document.write(count(n));

// This code is contributed by Rajput-Ji
</script>
```

输出:

```
4
```

本文由 [**拉贾·维克拉玛迪特亚**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。