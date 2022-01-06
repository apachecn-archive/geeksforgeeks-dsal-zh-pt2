# 数组的最大乘积子集

> 原文:[https://www.geeksforgeeks.org/maximum-product-subset-array/](https://www.geeksforgeeks.org/maximum-product-subset-array/)

给定一个数组 a，我们必须找到数组中元素子集的最大乘积。最大乘积也可以是单元素。
**例:**

```
Input: a[] = { -1, -1, -2, 4, 3 }
Output: 24
Explanation : Maximum product will be ( -2 * -1 * 4 * 3 ) = 24

Input: a[] = { -1, 0 }
Output: 0
Explanation: 0(single element) is maximum product possible

Input: a[] = { 0, 0, 0 }
Output: 0
```

一个**简单的解决方案**就是[生成所有子集](https://www.geeksforgeeks.org/power-set/)，找到每个子集的乘积，返回最大乘积。
A **更好的解决方案**就是用下面的事实。

1.  如果有偶数个负数，没有零，结果就是所有的乘积
2.  如果有奇数个负数且没有零，则结果是除了绝对值最小的负整数之外的所有整数的乘积。
3.  如果有零，结果是除这些零以外的所有零与一个例外情况的乘积。例外情况是有一个负数，而所有其他元素都是 0。在这种情况下，结果为 0。

以下是上述方法的实现:

## C++

```
// CPP program to find maximum product of
// a subset.
#include <bits/stdc++.h>
using namespace std;

int maxProductSubset(int a[], int n)
{
    if (n == 1)
        return a[0];

    // Find count of negative numbers, count
    // of zeros, negative number
    // with least absolute value
    // and product of non-zero numbers
    int max_neg = INT_MIN;
    int count_neg = 0, count_zero = 0;
    int prod = 1;
    for (int i = 0; i < n; i++) {

        // If number is 0, we don't
        // multiply it with product.
        if (a[i] == 0) {
            count_zero++;
            continue;
        }

        // Count negatives and keep
        // track of negative number
        // with least absolute value
        if (a[i] < 0) {
            count_neg++;
            max_neg = max(max_neg, a[i]);
        }

        prod = prod * a[i];
    }

    // If there are all zeros
    if (count_zero == n)
        return 0;

    // If there are odd number of
    // negative numbers
    if (count_neg & 1) {

        // Exceptional case: There is only
        // negative and all other are zeros
        if (count_neg == 1 &&
            count_zero > 0 &&
            count_zero + count_neg == n)
            return 0;

        // Otherwise result is product of
        // all non-zeros divided by
        //negative number with
        // least absolute value
        prod = prod / max_neg;
    }

    return prod;
}

// Driver Code
int main()
{
    int a[] = {  -1, -1, -2, 4, 3  };
    int n = sizeof(a) / sizeof(a[0]);
    cout << maxProductSubset(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum product of
// a subset.

class GFG {

    static int maxProductSubset(int a[], int n) {
        if (n == 1) {
            return a[0];
        }

        // Find count of negative numbers, count
        // of zeros, negative number
        // with least absolute value
        // and product of non-zero numbers
        int max_neg = Integer.MIN_VALUE;
        int count_neg = 0, count_zero = 0;
        int prod = 1;
        for (int i = 0; i < n; i++) {

            // If number is 0, we don't
            // multiply it with product.
            if (a[i] == 0) {
                count_zero++;
                continue;
            }

            // Count negatives and keep
            // track of negative number
            // with least absolute value.
            if (a[i] < 0) {
                count_neg++;
                max_neg = Math.max(max_neg, a[i]);
            }

            prod = prod * a[i];
        }

        // If there are all zeros
        if (count_zero == n) {
            return 0;
        }

        // If there are odd number of
        // negative numbers
        if (count_neg % 2 == 1) {

            // Exceptional case: There is only
            // negative and all other are zeros
            if (count_neg == 1
                    && count_zero > 0
                    && count_zero + count_neg == n) {
                return 0;
            }

            // Otherwise result is product of
            // all non-zeros divided by
            //negative number with
            // least absolute value.
            prod = prod / max_neg;
        }

        return prod;
    }

    // Driver Code
    public static void main(String[] args) {
        int a[] = {-1, -1, -2, 4, 3};
        int n = a.length;
        System.out.println(maxProductSubset(a, n));

    }
}
/* This JAVA code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python3 program to find maximum product
# of a subset.

def maxProductSubset(a, n):
    if n == 1:
        return a[0]

    # Find count of negative numbers, count
    # of zeros, negative number
    # with least absolute value
    # and product of non-zero numbers
    max_neg = -999999999999
    count_neg = 0
    count_zero = 0
    prod = 1
    for i in range(n):

        # If number is 0, we don't
        # multiply it with product.
        if a[i] == 0:
            count_zero += 1
            continue

        # Count negatives and keep
        # track of negative number
        # with least absolute value.
        if a[i] < 0:
            count_neg += 1
            max_neg = max(max_neg, a[i])

        prod = prod * a[i]

    # If there are all zeros
    if count_zero == n:
        return 0

    # If there are odd number of
    # negative numbers
    if count_neg & 1:

        # Exceptional case: There is only
        # negative and all other are zeros
        if (count_neg == 1 and count_zero > 0 and
            count_zero + count_neg == n):
            return 0

        # Otherwise result is product of
        # all non-zeros divided
        # by negative number
        # with least absolute value
        prod = int(prod / max_neg)

    return prod

# Driver Code
if __name__ == '__main__':
    a = [ -1, -1, -2, 4, 3 ]
    n = len(a)
    print(maxProductSubset(a, n))

# This code is contributed by PranchalK
```

## C#

```
// C# Java program to find maximum
// product of a subset.
using System;

class GFG
{

static int maxProductSubset(int []a,
                            int n)
{
    if (n == 1)
    {
        return a[0];
    }

    // Find count of negative numbers,
    // count of zeros, negative number with
    // least absolute value and product of
    // non-zero numbers
    int max_neg = int.MinValue;
    int count_neg = 0, count_zero = 0;
    int prod = 1;
    for (int i = 0; i < n; i++)
    {

        // If number is 0, we don't
        // multiply it with product.
        if (a[i] == 0)
        {
            count_zero++;
            continue;
        }

        // Count negatives and keep
        // track of negative number with
        // least absolute value.
        if (a[i] < 0)
        {
            count_neg++;
            max_neg = Math.Max(max_neg, a[i]);
        }

        prod = prod * a[i];
    }

    // If there are all zeros
    if (count_zero == n)
    {
        return 0;
    }

    // If there are odd number of
    // negative numbers
    if (count_neg % 2 == 1)
    {

        // Exceptional case: There is only
        // negative and all other are zeros
        if (count_neg == 1 && count_zero > 0 &&
            count_zero + count_neg == n)
        {
            return 0;
        }

        // Otherwise result is product of
        // all non-zeros divided by negative
        // number with least absolute value.
        prod = prod / max_neg;
    }

    return prod;
}

// Driver code
public static void Main()
{
    int []a = {-1, -1, -2, 4, 3};
    int n = a.Length;
    Console.Write(maxProductSubset(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// product of a subset.

function maxProductSubset($a, $n)
{
    if ($n == 1)
        return $a[0];

    // Find count of negative numbers,
    // count of zeros, negative number
    // with least absolute value and product of
    // non-zero numbers
    $max_neg = PHP_INT_MIN;
    $count_neg = 0; $count_zero = 0;
    $prod = 1;
    for ($i = 0; $i < $n; $i++)
    {

        // If number is 0, we don't
        // multiply it with product.
        if ($a[$i] == 0)
        {
            $count_zero++;
            continue;
        }

        // Count negatives and keep
        // track of negative number
        // with least absolute value.
        if ($a[$i] < 0)
        {
            $count_neg++;
            $max_neg = max($max_neg, $a[$i]);
        }

        $prod = $prod * $a[$i];
    }

    // If there are all zeros
    if ($count_zero == $n)
        return 0;

    // If there are odd number of
    // negative numbers
    if ($count_neg & 1)
    {

        // Exceptional case: There is only
        // negative and all other are zeros
        if ($count_neg == 1 &&
            $count_zero > 0 &&
            $count_zero + $count_neg == $n)
            return 0;

        // Otherwise result is product of
        // all non-zeros divided by negative
        // number with least absolute value.
        $prod = $prod / $max_neg;
    }

    return $prod;
}

// Driver Code
$a = array(-1, -1, -2, 4, 3 );
$n = sizeof($a);
echo maxProductSubset($a, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum
// product of a subset.

function maxProductSubset(a, n)
{
    if (n == 1)
        return a[0];

    // Find count of negative numbers,
    // count of zeros, negative number
    // with least absolute value and product of
    // non-zero numbers
    let max_neg = Number.MIN_SAFE_INTEGER;
    let count_neg = 0; count_zero = 0;
    let prod = 1;
    for (let i = 0; i < n; i++)
    {

        // If number is 0, we don't
        // multiply it with product.
        if (a[i] == 0)
        {
            count_zero++;
            continue;
        }

        // Count negatives and keep
        // track of negative number
        // with least absolute value.
        if (a[i] < 0)
        {
            count_neg++;
            max_neg = Math.max(max_neg, a[i]);
        }

        prod = prod * a[i];
    }

    // If there are all zeros
    if (count_zero == n)
        return 0;

    // If there are odd number of
    // negative numbers
    if (count_neg & 1)
    {

        // Exceptional case: There is only
        // negative and all other are zeros
        if (count_neg == 1 &&
            count_zero > 0 &&
            count_zero + count_neg == n)
            return 0;

        // Otherwise result is product of
        // all non-zeros divided by negative
        // number with least absolute value.
        prod = prod / max_neg;
    }

    return prod;
}

// Driver Code
let a = [-1, -1, -2, 4, 3 ];
let n = a.length;
document.write(maxProductSubset(a, n));

// This code is contributed
// by _saurabh_jaiswal

</script>
```

**Output**

```
24
```

***时间复杂度:**O(n)*
T5**辅助空间:** O(1)