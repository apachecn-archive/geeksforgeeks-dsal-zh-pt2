# 位数总和和乘积的最大值，直到数字减少到一位数

> 原文:[https://www . geeksforgeeks . org/最大位数和最大位数乘积直到数字减少到一位数/](https://www.geeksforgeeks.org/maximum-of-sum-and-product-of-digits-until-number-is-reduced-to-a-single-digit/)

给定一个数字 N，任务是打印给定数字的位数的和与乘之间的最大值，直到该数字减少到一个位数。
**注意:**要做的数字的和与乘，直到数字减少到一位数。

**举个例子，N = 19，**

> 19 分成 1+9=10，然后 10 分成 1+0=1。1 是个位数的总和。
> 同样，19 分解成 1*9 = 9。9 是个位数的乘法。
> 所以，输出是 9，即 9 和 1 的最大值。

```
Input: N = 631
Output: 8

Input: 110
Output: 2
```

**进场:**

1.  检查一个数字是否小于 10，那么总和和乘积将是相同的。所以，返回那个数字。
2.  否则，
    *   重复使用[的**方法 2** 求数字的和，直到和变成一位数](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)。
    *   并且，反复使用[的**方法 1** 求一个数的位数之和，直到和变成一位数](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)为止。
3.  返回两者的最大值。

下面是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include<bits/stdc++.h>
using namespace std;
    // Function to sum the digits until it
    // becomes a single digit
    long repeatedSum(long n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Function to product the digits until it
    // becomes a single digit
    long repeatedProduct(long n)
    {
        long prod = 1;

        // Loop to do sum while
        // sum is not less than
        // or equal to 9
        while (n > 0 || prod > 9) {
            if (n == 0) {
                n = prod;
                prod = 1;
            }
            prod *= n % 10;
            n /= 10;
        }
        return prod;
    }

    // Function to find the maximum among
    // repeated sum and repeated product
    long maxSumProduct(long N)
    {

        if (N < 10)
            return N;

        return max(repeatedSum(N), repeatedProduct(N));
    }

    // Driver code
    int main()
    {

        long n = 631;
        cout << maxSumProduct(n)<<endl;
        return 0;
    }
// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // Function to sum the digits until it
    // becomes a single digit
    public static long repeatedSum(long n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Function to product the digits until it
    // becomes a single digit
    public static long repeatedProduct(long n)
    {
        long prod = 1;

        // Loop to do sum while
        // sum is not less than
        // or equal to 9
        while (n > 0 || prod > 9) {
            if (n == 0) {
                n = prod;
                prod = 1;
            }
            prod *= n % 10;
            n /= 10;
        }
        return prod;
    }

    // Function to find the maximum among
    // repeated sum and repeated product
    public static long maxSumProduct(long N)
    {

        if (N < 10)
            return N;

        return Math.max(repeatedSum(N), repeatedProduct(N));
    }

    // Driver code
    public static void main(String[] args)
    {

        long n = 631;
        System.out.println(maxSumProduct(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to sum the digits until
# it becomes a single digit
def repeatedSum(n):
    if (n == 0):
        return 0
    return 9 if(n % 9 == 0) else (n % 9)

# Function to product the digits
# until it becomes a single digit
def repeatedProduct(n):
    prod = 1

    # Loop to do sum while
    # sum is not less than
    # or equal to 9
    while (n > 0 or prod > 9) :
        if (n == 0) :
            n = prod
            prod = 1

        prod *= n % 10
        n //= 10

    return prod

# Function to find the maximum among
# repeated sum and repeated product
def maxSumProduct(N):

    if (N < 10):
        return N

    return max(repeatedSum(N),
               repeatedProduct(N))

# Driver code
if __name__ == "__main__":

    n = 631
    print(maxSumProduct(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of
// above approach
using System;
class GFG
{

// Function to sum the digits
// until it becomes a single digit
public static long repeatedSum(long n)
{
    if (n == 0)
        return 0;
    return (n % 9 == 0) ?
                      9 : (n % 9);
}

// Function to product the digits
// until it becomes a single digit
public static long repeatedProduct(long n)
{
    long prod = 1;

    // Loop to do sum while
    // sum is not less than
    // or equal to 9
    while (n > 0 || prod > 9)
    {
        if (n == 0)
        {
            n = prod;
            prod = 1;
        }
        prod *= n % 10;
        n /= 10;
    }
    return prod;
}

// Function to find the maximum among
// repeated sum and repeated product
public static long maxSumProduct(long N)
{

    if (N < 10)
        return N;

    return Math.Max(repeatedSum(N),
                    repeatedProduct(N));
}

// Driver code
public static void Main()
{
    long n = 631;
    Console.WriteLine(maxSumProduct(n));
}
}

// This code is contributed
// by inder_verma
```

## java 描述语言

```
<script>
// javascript implementation of above approach
    // Function to sum the digits until it
    // becomes a single digit
    function repeatedSum(n) {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Function to product the digits until it
    // becomes a single digit
    function repeatedProduct(n) {
        var prod = 1;

        // Loop to do sum while
        // sum is not less than
        // or equal to 9
        while (n > 0 || prod > 9) {
            if (n == 0) {
                n = prod;
                prod = 1;
            }
            prod *= n % 10;
            n = parseInt(n/10);
        }
        return prod;
    }

    // Function to find the maximum among
    // repeated sum and repeated product
    function maxSumProduct(N) {

        if (N < 10)
            return N;

        return Math.max(repeatedSum(N), repeatedProduct(N));
    }

    // Driver code

        var n = 631;
        document.write(maxSumProduct(n));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
8
```