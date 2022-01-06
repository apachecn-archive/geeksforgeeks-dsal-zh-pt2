# 求数组数乘积的最后 k 位数字

> 原文:[https://www . geesforgeks . org/find-last-k-digits-product-array-numbers/](https://www.geeksforgeeks.org/find-last-k-digits-product-array-numbers/)

给定 n 的数组大小，求数组数乘积的最后 k 个数字(1 <= k < 10)

示例:

```
Input  : a[] = {22, 31, 44, 27, 37, 43}
Output : 56

Input  : a[] = {24, 7, 144, 77, 29, 19}
Output : 84
```

一个**简单的解法**就是把所有数字相乘，然后求乘积的最后 k 位数字。此解决方案可能会导致溢出，因为阵列乘积可能很高。

一个**更好的解决方案**是以 10 <sup>k</sup> 为模乘数组元素

## C++

```
// CPP program to find the last k digits in
// product of array
#include <bits/stdc++.h>
using namespace std;

// Returns last k digits in product of a[]
int lastKDigits(int a[], int n, int k)
{
    int num = (int)pow(10, k);

    // Multiplying array elements under
    // modulo 10^k.
    int mul = a[0] % num;
    for (int i = 1; i < n; i++) {
        a[i] = a[i] % num;
        mul = (a[i] * mul) % num;
    }
    return mul;
}

// Driven program
int main()
{
    int a[] = { 22, 31, 44, 27, 37, 43 };
    int k = 2;
    int n = sizeof(a) / sizeof(a[0]);
    cout << lastKDigits(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the last k digits in
// product of array
import java.io.*;
import java.math.*;

class GFG {

    // Returns last k digits in product of a[]
    static int lastKDigits(int a[], int n, int k)
    {
        int num = (int)(Math.pow(10, k));

        // Multiplying array elements
        // under modulo 10^k.
        int mul = a[0] % num;

        for (int i = 1; i < n; i++) {
            a[i] = a[i] % num;
            mul = (a[i] * mul) % num;
        }
        return mul;
    }

// Driven program
public static void main(String args[])
{
    int a[] = { 22, 31, 44, 27, 37, 43 };
    int k = 2;
    int n = a.length;

    System.out.println(lastKDigits(a, n, k));
}

}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find the last
# k digits inproduct of array
import math

# Returns last k digits
# in product of a[]
def lastKDigits(a, n, k) :

    num = (int)(math.pow(10, k))

    # Multiplying array elements
    # under modulo 10^k.
    mul = a[0] % num

    for i in range(1,n) :
        a[i] = a[i] % num
        mul = (a[i] * mul) % num

    return mul

# Driven program
a = [ 22, 31, 44, 27, 37, 43 ]
k = 2
n = len(a)
print(lastKDigits(a, n, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find
// the last k digits in
// product of array
using System;

class GFG {

    // Returns last k digits in product of a[]
    static int lastKDigits(int []a, int n, int k)
    {
        int num = (int)(Math.Pow(10, k));

        // Multiplying array elements
        // under modulo 10^k.
        int mul = a[0] % num;

        for (int i = 1; i < n; i++) {
            a[i] = a[i] % num;
            mul = (a[i] * mul) % num;
        }
        return mul;
    }

    // Driven program
    public static void Main()
    {
        int []a = { 22, 31, 44, 27, 37, 43 };
        int k = 2;
        int n = a.Length;

        Console.WriteLine(lastKDigits(a, n, k));
    }

}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the last k digits in
// product of array

// Returns last k digits
// in product of a[]
function lastKDigits($a, $n, $k)
{

    $num = (int)pow(10, $k);

    // Multiplying array elements
    // under modulo 10^k.
    $mul = $a[0] % $num;
    for ($i = 1; $i < $n; $i++)
    {
        $a[$i] = $a[$i] % $num;
        $mul = ($a[$i] * $mul) % $num;
    }
    return $mul;
}

// Driver Code
$a = array( 22, 31, 44, 27, 37, 43 );
$k = 2;
$n = sizeof($a);
echo(lastKDigits($a, $n, $k));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the last k digits in
// product of array

// Returns last k digits in product of a[]
function lastKDigits(a, n, k)
{
    let num = (Math.pow(10, k));

    // Multiplying array elements
    // under modulo 10^k.
    let mul = a[0] % num;

    for(let i = 1; i < n; i++)
    {
        a[i] = a[i] % num;
        mul = (a[i] * mul) % num;
    }
    return mul;
}

// Driver code
let a = [ 22, 31, 44, 27, 37, 43 ];
let k = 2;
let n = a.length;

document.write(lastKDigits(a, n, k));

// This code is contributed by suresh07 

</script>
```

输出:

```
 56
```

**时间复杂度:O(n)**