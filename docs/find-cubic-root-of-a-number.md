# 求一个数的立方根

> 原文:[https://www.geeksforgeeks.org/find-cubic-root-of-a-number/](https://www.geeksforgeeks.org/find-cubic-root-of-a-number/)

给定一个数 n，求 n 的立方根
例:

```
Input:  n = 3
Output: Cubic Root is 1.442250

Input: n = 8
Output: Cubic Root is 2.000000
```

我们可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。首先我们定义误差 e，假设我们的情况是 0.0000001。我们计算一个数 n 的立方根的算法的主要步骤是:

1.  初始化开始= 0 和结束= n
2.  计算中间=(开始+结束)/2
3.  检查(n–mid * mid * mid)的绝对值是否为< e. If this condition holds true then mid is our answer so return mid. 

4.  如果(中间*中间*中间)> n，则设置 end=mid
5.  If (mid*mid*mid)

以下是上述想法的实现。

## C++

```
// C++ program to find cubic root of a number
// using Binary Search
#include <bits/stdc++.h>
using namespace std;

// Returns the absolute value of n-mid*mid*mid
double diff(double n,double mid)
{
    if (n > (mid*mid*mid))
        return (n-(mid*mid*mid));
    else
        return ((mid*mid*mid) - n);
}

// Returns cube root of a no n
double cubicRoot(double n)
{
    // Set start and end for binary search
    double start = 0, end = n;

    // Set precision
    double e = 0.0000001;

    while (true)
    {
        double mid = (start + end)/2;
        double error = diff(n, mid);

        // If error is less than e then mid is
        // our answer so return mid
        if (error <= e)
            return mid;

        // If mid*mid*mid is greater than n set
        // end = mid
        if ((mid*mid*mid) > n)
            end = mid;

        // If mid*mid*mid is less than n set
        // start = mid
        else
            start = mid;
    }
}

// Driver code
int main()
{
    double n = 3;
    printf("Cubic root of %lf is %lf\n",
           n, cubicRoot(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find cubic root of a number
// using Binary Search
import java.io.*;

class GFG
{
    // Returns the absolute value of n-mid*mid*mid
    static double diff(double n,double mid)
    {
        if (n > (mid*mid*mid))
            return (n-(mid*mid*mid));
        else
            return ((mid*mid*mid) - n);
    }

    // Returns cube root of a no n
    static double cubicRoot(double n)
    {
        // Set start and end for binary search
        double start = 0, end = n;

        // Set precision
        double e = 0.0000001;

        while (true)
        {
            double mid = (start + end)/2;
            double error = diff(n, mid);

            // If error is less than e then mid is
            // our answer so return mid
            if (error <= e)
                return mid;

            // If mid*mid*mid is greater than n set
            // end = mid
            if ((mid*mid*mid) > n)
                end = mid;

            // If mid*mid*mid is less than n set
            // start = mid
            else
                start = mid;
        }
    }

    // Driver program to test above function
    public static void main (String[] args)
    {
        double n = 3;
        System.out.println("Cube root of "+n+" is "+cubicRoot(n));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to find cubic root
# of a number using Binary Search

# Returns the absolute value of
# n-mid*mid*mid
def diff(n, mid) :
    if (n > (mid * mid * mid)) :
        return (n - (mid * mid * mid))
    else :
        return ((mid * mid * mid) - n)

# Returns cube root of a no n
def cubicRoot(n) :

    # Set start and end for binary
    # search
    start = 0
    end = n

    # Set precision
    e = 0.0000001
    while (True) :

        mid = (start + end) / 2
        error = diff(n, mid)

        # If error is less than e
        # then mid is our answer
        # so return mid
        if (error <= e) :
            return mid

        # If mid*mid*mid is greater
        # than n set end = mid
        if ((mid * mid * mid) > n) :
            end = mid

        # If mid*mid*mid is less
        # than n set start = mid
        else :
            start = mid

# Driver code
n = 3
print("Cubic root of", n, "is",
      round(cubicRoot(n),6))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find cubic root
// of a number using Binary Search
using System;

class GFG {

    // Returns the absolute value
    // of n - mid * mid * mid
    static double diff(double n, double mid)
    {
        if (n > (mid * mid * mid))
            return (n-(mid * mid * mid));
        else
            return ((mid * mid * mid) - n);
    }

    // Returns cube root of a no. n
    static double cubicRoot(double n)
    {

        // Set start and end for
        // binary search
        double start = 0, end = n;

        // Set precision
        double e = 0.0000001;

        while (true)
        {
            double mid = (start + end) / 2;
            double error = diff(n, mid);

            // If error is less than e then
            // mid is our answer so return mid
            if (error <= e)
                return mid;

            // If mid * mid * mid is greater
            // than n set end = mid
            if ((mid * mid * mid) > n)
                end = mid;

            // If mid*mid*mid is less than
            // n set start = mid
            else
                start = mid;
        }
    }

    // Driver Code
    public static void Main ()
    {
        double n = 3;
        Console.Write("Cube root of "+ n
                       + " is "+cubicRoot(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find cubic root
// of a number using Binary Search

// Returns the absolute value
// of n - mid * mid * mid
function diff($n,$mid)
{
    if ($n > ($mid * $mid * $mid))
        return ($n - ($mid *
                $mid * $mid));
    else
        return (($mid * $mid *
                 $mid) - $n);
}

// Returns cube root of a no n
function cubicRoot($n)
{

    // Set start and end
    // for binary search
    $start = 0;
    $end = $n;

    // Set precision
    $e = 0.0000001;

    while (true)
    {
        $mid = (($start + $end)/2);
        $error = diff($n, $mid);

        // If error is less
        // than e then mid is
        // our answer so return mid
        if ($error <= $e)
            return $mid;

        // If mid*mid*mid is
        // greater than n set
        // end = mid
        if (($mid * $mid * $mid) > $n)
            $end = $mid;

        // If mid*mid*mid is
        // less than n set
        // start = mid
        else
            $start = $mid;
    }
}

    // Driver Code
    $n = 3;
    echo("Cubic root of $n is ");
    echo(cubicRoot($n));

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find cubic root of a number
// using Binary Search

    // Returns the absolute value of n-mid*mid*mid
    function diff(n, mid)
    {
        if (n > (mid*mid*mid))
            return (n-(mid*mid*mid));
        else
            return ((mid*mid*mid) - n);
    }

    // Returns cube root of a no n
    function cubicRoot(n)
    {
        // Set start and end for binary search
        let start = 0, end = n;

        // Set precision
        let e = 0.0000001;

        while (true)
        {
            let mid = (start + end)/2;
            let error = diff(n, mid);

            // If error is less than e then mid is
            // our answer so return mid
            if (error <= e)
                return mid;

            // If mid*mid*mid is greater than n set
            // end = mid
            if ((mid*mid*mid) > n)
                end = mid;

            // If mid*mid*mid is less than n set
            // start = mid
            else
                start = mid;
        }
    }

// Driver Code

        let n = 3;
        document.write("Cube root of "+n+" is "+cubicRoot(n));

</script>
```

**输出:**

```
Cubic root of 3.000000 is 1.442250
```

时间复杂度:O(Log n)
本文由**马达尔·莫迪**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。