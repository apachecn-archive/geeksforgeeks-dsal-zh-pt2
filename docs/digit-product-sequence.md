# 数字-产品-序列

> 原文:[https://www.geeksforgeeks.org/digit-product-sequence/](https://www.geeksforgeeks.org/digit-product-sequence/)

给定一个数字 N，任务是将序列打印到 N。序列是:1，2，4，8，16，22，26，38，62，74，102，104，108，116，122，126，138，162 等等……这个序列被称为数字-乘积-序列。在本系列中，我们取数字的每个非零数字，乘以它们，然后将乘积加到数字本身上。

**示例:**

```
Input : N = 10
Output :1 2 4 8 16 22 26 38 62 74

Input : N = 7
Output :1 2 4 8 16 22 26
```

**说明:**

```
1 + (1 * 1)  = 1 + 1  = 2
2 + (2 * 1)  = 2 + 2  = 4
4 + (4 * 1)  = 4 + 4  = 8
8 + (8 * 1)  = 8 + 8  = 16
16 + (1 * 6) = 16 + 6 = 22
22 + (2 * 2) = 22 + 4 = 26
26 + (2 * 6) = 26 + 12 = 38
38 + (3 * 8) = 38 + 24 = 62
62 + (6 * 2) = 62 + 12 = 74
and so on...
```

## C++

```
// CPP program for Digit Product Sequence
#include <bits/stdc++.h>
using namespace std;

// function to produce and print Digit
// Product Sequence
void digit_product_Sum(int N)
{
    // Array which store sequence
    int a[N];

    // Temporary variable to store product
    int product = 1;

    // Initialize first element of the
    // array with 1
    a[0] = 1;

    // Run a loop from 1 to N. Check if
    // previous number is single digit or
    // not. If yes then product = 1 else
    // take modulus. Then again check if
    // previous number is single digit or
    // not if yes then store previous number,
    // else store its first value Then for
    // every i store value in the array.
    for (int i = 1; i <= N; i++) {
        product = a[i - 1] / 10;

        if (product == 0)
            product = 1;
        else
            product = a[i - 1] % 10;

        int val = a[i - 1] / 10;

        if (val == 0)
            val = a[i - 1];

        a[i] = a[i - 1] + (val * product);
    }

    // Print sequence
    for (int i = 0; i < N; i++)
        cout << a[i] << " ";
}

// Driver Code
int main()
{
    // Value of N
    int N = 10;

    // Calling function
    digit_product_Sum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Digit Product Sequence

// function to produce and print Digit
// Product Sequence
import java.lang.*;
import java.io.*;

class GFG
{
    public static void digit_product_Sum(int N)
    {
        // Array which store sequence
        int a[] = new int[N+1] ;

        // Temporary variable to store product
        int product = 1;

        // Initialize first element of the
        // array with 1
        a[0] = 1;

        // Run a loop from 1 to N. Check if
        // previous number is single digit or
        // not. If yes then product = 1 else
        // take modulus. Then again check if
        // previous number is single digit or
        // not if yes then store previous number,
        // else store its first value Then for
        // every i store value in the array.
        for (int i = 1; i <= N; i++)
        {
            product = a[i - 1] / 10;

            if (product == 0)
                product = 1;
            else
                product = a[i - 1] % 10;

            int val = a[i - 1] / 10;

            if (val == 0)
                val = a[i - 1];

            a[i] = a[i - 1] + (val * product);
        }

        // Print sequence
        for (int i = 0; i < N; i++)
            System.out.print(a[i] + " ");
    }

// Driver Code
    public static void main(String[] args)
    {
        // Value of N
        int N = 10;

        // Calling function
        digit_product_Sum(N);

    }
}
// Code contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Python3 program for
# Digit Product Sequence

# function to produce and
# print Digit Product Sequence

def digit_product_Sum(N):

    # Array which store sequence
    a = [0] * (N + 1);

    # Temporary variable
    # to store product
    product = 1;

    # Initialize first element
    # of the array with 1
    a[0] = 1;

    # Run a loop from 1 to N.
    # Check if previous number
    # is single digit or not.
    # If yes then product = 1
    # else take modulus. Then
    # again check if previous
    # number is single digit or
    # not if yes then store
    # previous number, else store
    # its first value Then for
    # every i store value in
    # the array.
    for i in range(1, N + 1):
        product = int(a[i - 1] / 10);
        if (product == 0):
            product = 1;
        else:
            product = a[i - 1] % 10;

        val = int(a[i - 1] / 10);
        if (val == 0):
            val = a[i - 1];
        a[i] = a[i - 1] + (val * product);

    # Print sequence
    for i in range(N):
        print(a[i], end = " ");

# Driver Code

# Value of N
N = 10;

# Calling function
digit_product_Sum(N);

# This Code is contributed
# by mits.
```

## C#

```
// C# program for Digit Product Sequence
// function to produce and print Digit
// Product Sequence
using System;

class GFG
{
    public static void digit_product_Sum(int N)
    {
        // Array which store sequence
        int []a = new int[N + 1] ;

        // Temporary variable to store product
        int product = 1;

        // Initialize first element of the
        // array with 1
        a[0] = 1;

        // Run a loop from 1 to N. Check if
        // previous number is single digit or
        // not. If yes then product = 1 else
        // take modulus. Then again check if
        // previous number is single digit or
        // not if yes then store previous number,
        // else store its first value Then for
        // every i store value in the array.
        for (int i = 1; i <= N; i++)
        {
            product = a[i - 1] / 10;

            if (product == 0)
                product = 1;
            else
                product = a[i - 1] % 10;

            int val = a[i - 1] / 10;

            if (val == 0)
                val = a[i - 1];

            a[i] = a[i - 1] + (val * product);
        }

        // Print sequence
        for (int i = 0; i < N; i++)
        Console.Write(a[i] + " ");
    }

    // Driver Code
    public static void Main()
    {
        // Value of N
        int N = 10;

        // Calling function
        digit_product_Sum(N);

    }
}
// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Digit
// Product Sequence

// function to produce
// and print Digit
// Product Sequence
function digit_product_Sum($N)
{
    // Array which
    // store sequence
    $a = array_fill(0, $N, 0);

    // Temporary variable
    // to store product
    $product = 1;

    // Initialize first
    // element of the
    // array with 1
    $a[0] = 1;

    // Run a loop from 1 to
    // N. Check if previous
    // number is single digit
    // or not. If yes then
    // product = 1 else take
    // modulus. Then again check
    // if previous number is single
    // digit or not if yes then
    // store previous number,
    // else store its first value
    // Then for every i store value
    // in the array.
    for ($i = 1; $i <= $N; $i++)
    {
        $product = (int)($a[$i - 1] / 10);

        if ($product == 0)
            $product = 1;
        else
            $product = $a[$i - 1] % 10;

        $val = (int)($a[$i - 1] / 10);

        if ($val == 0)
            $val = $a[$i - 1];

        $a[$i] = $a[$i - 1] +
                ($val * $product);
    }

    // Print sequence
    for ($i = 0; $i < $N; $i++)
        echo $a[$i]." ";
}

// Driver Code

// Value of N
$N = 10;

// Calling function
digit_product_Sum($N);

// This Code is contributed
// by mits.

?>
```

## java 描述语言

```
<script>
      // JavaScript program for Digit
      // Product Sequence

      // function to produce and print Digit
      // Product Sequence
      function digit_product_Sum(N) {
        // Array which store sequence
        var a = [...Array(N)];

        // Temporary variable to store product
        var product = 1;

        // Initialize first element of the
        // array with 1
        a[0] = 1;

        // Run a loop from 1 to N. Check if
        // previous number is single digit or
        // not. If yes then product = 1 else
        // take modulus. Then again check if
        // previous number is single digit or
        // not if yes then store previous number,
        // else store its first value Then for
        // every i store value in the array.
        for (var i = 1; i <= N; i++)
        {
          product = parseInt(a[i - 1] / 10);

          if (product == 0) product = 1;
          else product = a[i - 1] % 10;

          var val = parseInt(a[i - 1] / 10);

          if (val == 0) val = a[i - 1];

          a[i] = a[i - 1] + val * product;
        }

        // Print sequence
        for (var i = 0; i < N; i++)
        document.write(a[i] + " ");
      }

      // Driver Code
      // Value of N
      var N = 10;

      // Calling function
      digit_product_Sum(N);

</script>
```

**输出:**

```
1 2 4 8 16 22 26 38 62 74
```

本文由 **Ayush Saxena** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。