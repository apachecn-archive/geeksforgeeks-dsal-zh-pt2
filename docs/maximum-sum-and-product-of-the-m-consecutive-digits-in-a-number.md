# 一个数字中 M 个连续数字的最大和与积

> 原文:[https://www . geeksforgeeks . org/数字中 m 个连续数字的最大和与乘积/](https://www.geeksforgeeks.org/maximum-sum-and-product-of-the-m-consecutive-digits-in-a-number/)

给定一个字符串形式的数字。任务是从数字串中找出 m 个连续数字的最大和与乘积。
**例:**

> **输入:** N = 3675356291，m = 5
> **输出:** 3150
> 有 6 个 5 位数的序列 36753、67535、75356、53562、35629、56291
> 6×7×5×3×5 给出最大乘积。
> **输入:** N = 2709360626，m = 5
> **输出:** 0
> 由于连续 5 位数字的每个序列将包含一个 0，因此每次乘积将为零，因此
> 最大乘积为零。

**天真的方法:**

1.  从给定字符串中提取 m 个字符的所有可能的连续序列。
2.  将它们相加，然后通过将字符转换成整数来相乘。
3.  比较每个序列的积和，找出最大的积和。

以下是上述方法的实现:

## C++

```
// Code is Improved by Surya Prakash Sharma

// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum product
void maxProductSum(string str, int m)
{
    int n = str.length();
    int maxProd = INT_MIN, maxSum = INT_MIN;
    for (int i = 0; i <=n - m; i++) {
        int product = 1, sum = 0;

        for (int j = i; j < m + i; j++) {
            product = product * (str[j] - '0');
            sum = sum + (str[j] - '0');
        }

        maxProd = max(maxProd, product);
        maxSum = max(maxSum, sum);
    }
    cout << "Maximum Product = " << maxProd;
    cout << "\nMaximum Sum = " << maxSum;
}

// Driver code
int main()
{
    string str = "3605356297";
    int m = 3;

    maxProductSum(str, m);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Code is Improved by Surya Prakash Sharma

 // Java implementation of the above approach

import java.io.*;

class GFG {

// Function to find the maximum product
 static void maxProductSum(String str, int m)
{
    int n = str.length();
    int maxProd = Integer.MIN_VALUE, maxSum = Integer.MIN_VALUE;
    for (int i = 0; i <=n - m; i++) {
        int product = 1, sum = 0;

        for (int j = i; j < m + i; j++) {
            product = product * (str.charAt(j) - '0');
            sum = sum + (str.charAt(j) - '0');
        }

        maxProd = Math.max(maxProd, product);
        maxSum = Math.max(maxSum, sum);
    }
    System.out.println("Maximum Product = " + maxProd);
    System.out.print( "\nMaximum Sum = " + maxSum);
}

// Driver code

    public static void main (String[] args) {
        String str = "3605356297";
    int m = 3;

    maxProductSum(str, m);
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Code is Improved by Surya Prakash Sharma

# Python implementation of
# above approach
import sys

# Function to find the maximum product
def maxProductSum(string, m) :

    n = len(string)
    maxProd , maxSum = (-(sys.maxsize) - 1,
                        -(sys.maxsize) - 1)

    for i in range(n - m+1) :
        product, sum = 1, 0

        for j in range(i, m + i) :
            product = product * (ord(string[j]) -
                                 ord('0'))
            sum = sum + (ord(string[j]) -
                         ord('0'))

        maxProd = max(maxProd, product)
        maxSum = max(maxSum, sum)

    print("Maximum Product =", maxProd)
    print("Maximum sum =", maxSum)

# Driver code
if __name__ == "__main__" :

    string = "3605356297"
    m = 3
    maxProductSum(string, m)

# This code is contributed by ANKITRAI1
```

## C#

```
// Code is Improved by Surya Prakash Sharma

// C# implementation of the above approach
using System;
class GFG
{

// Function to find the maximum product
static void maxProductSum(string str, int m)
{
    int n = str.Length;
    int maxProd = int.MinValue,
        maxSum = int.MinValue;
    for (int i = 0; i <= n - m; i++)
    {
        int product = 1, sum = 0;

        for (int j = i; j < m + i; j++)
        {
            product = product * (str[j] - '0');
            sum = sum + (str[j] - '0');
        }

        maxProd = Math.Max(maxProd, product);
        maxSum = Math.Max(maxSum, sum);
    }
    Console.WriteLine("Maximum Product = " + maxProd);
    Console.Write( "\nMaximum Sum = " + maxSum);
}

// Driver code
public static void Main ()
{
    string str = "3605356297";
    int m = 3;

    maxProductSum(str, m);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Code is Improved by Surya Prakash Sharma

// PHP implementation of the above approach

// Function to find the maximum product
function maxProductSum($str, $m)
{
    $n = strlen($str);
    $maxProd = PHP_INT_MIN;
    $maxSum = PHP_INT_MIN;
    for ($i = 0; $i <= ($n - $m); $i++)
    {
        $product = 1;
        $sum = 0;

        for ($j = $i; $j < ($m + $i); $j++)
        {
            $product = $product *
                      ($str[$j] - '0');
            $sum = $sum + ($str[$j] - '0');
        }

        $maxProd = max($maxProd, $product);
        $maxSum = max($maxSum, $sum);
    }
    echo "Maximum Product = " ,$maxProd;
    echo "\nMaximum Sum = " , $maxSum;
}

// Driver code
$str = "3605356297";
$m = 3;

maxProductSum($str, $m);

// This code is contributed by @Tushil.
?>
```

## java 描述语言

```
<script>
    // Code is Improved by Surya Prakash Sharma

    // Javascript implementation of the above approach

    // Function to find the maximum product
    function maxProductSum(str, m)
    {
        let n = str.length;
        let maxProd = Number.MIN_VALUE,
            maxSum = Number.MIN_VALUE;
        for (let i = 0; i <= n - m; i++)
        {
            let product = 1, sum = 0;

            for (let j = i; j < m + i; j++)
            {
                product = product * (str[j] - '0');
                sum = sum + (str[j] - '0');
            }

            maxProd = Math.max(maxProd, product);
            maxSum = Math.max(maxSum, sum);
        }
        document.write("Maximum Product = " + maxProd + "</br>");
        document.write( "Maximum Sum = " + maxSum);
    }

    let str = "3605356297";
    let m = 3;

    maxProductSum(str, m);

</script>
```

**Output**

```
Maximum Product = 126
Maximum Sum = 18
```

**高效方法:**想法是使用[滑动窗口概念](https://www.geeksforgeeks.org/window-sliding-technique/)。首先求 M 个连续数字的和与积，更新 maxProd 和 maxSum。
然后从第 M 个索引开始遍历，将当前数字加到和中，从和中减去 str[i-M]，即只考虑 M 个元素/数字。产品也是如此。并不断更新 maxSum 和 maxProd。

## C++

```
// Code Improved By Surya Prakash Sharma

// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum product and sum
void maxProductSum(string str, int m)
{
    int n = str.length();
    int product = 1, sum = 0, ZeroesInWindow=0;

    // find the sum and product of first K digits
    for (int i = 0; i < m; i++) {
        sum += (str[i] - '0');

        if(str[i]!='0')
        product *= (str[i] - '0');
        else
        ZeroesInWindow++;
    }

    // Update maxProd and maxSum
    int maxProd = 0;
    if(ZeroesInWindow==0)
      maxProd = product;
    int maxSum = sum;

    // Start traversing the next element
    for (int i = m; i < n; i++) {

        // Multiply with the current digit and divide by
        // the first digit of previous window
        if(str[i]!='0' && str[i-m]!='0')
        product = product * (str[i] - '0') / ((str[i - m]) - '0');
        else if(str[i]!='0' && str[i-m]=='0')
        { 
           product = product * (str[i] - '0');
           ZeroesInWindow--;
        }
        else if(str[i]=='0' && str[i-m]!='0')
        {
           product = product / (str[i-m] - '0');
           ZeroesInWindow++;
        }

        // Update maxProd
        if(ZeroesInWindow==0)
        maxProd = max(maxProd, product);

        // Add the current digit and subtract
        // the first digit of previous window
        sum = sum + (str[i] - '0') - ((str[i - m]) - '0');

        // Update maxSum
        maxSum = max(maxSum, sum);
    }

    cout << "Maximum Product = " << maxProd;
    cout << "\nMaximum Sum = " << maxSum;
}

// Driver code
int main()
{
    string str = "3601990545";
    int m = 3;

    maxProductSum(str, m);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Code Improved By Surya Prakash Sharma

// Java implementation of the above approach
import java.util.Arrays;
import java.io.*;

class GFG {

// Function to find the maximum product and sum
static void maxProductSum(String str, int m)
{
    int n = str.length();
    int product = 1, sum = 0, ZeroesInWindow=0;

    // find the sum and product of first K digits
    for (int i = 0; i < m; i++)
    {
        sum += (str.charAt(i) - '0');

        if(str.charAt(i)!='0')
        product *= (str.charAt(i) - '0');
        else
        ZeroesInWindow++;

    }

    // Update maxProd and maxSum
    int maxProd = 0;
    if(ZeroesInWindow==0)
      maxProd = product;
    int maxSum = sum;

    // Start traversing the next element
    for (int i = m; i < n; i++)
    {

        // Multiply with the current digit and divide by
        // the first digit of previous window
        if(str.charAt(i)!='0' && str.charAt(i-m)!='0')
        product = product * (str.charAt(i) - '0') / ((str.charAt(i-m)) - '0');
        else if(str.charAt(i)!='0' && str.charAt(i-m)=='0')
        { 
           product = product * (str.charAt(i) - '0');
           ZeroesInWindow--;
        }
        else if(str.charAt(i)=='0' && str.charAt(i-m)!='0')
        {
           product = product / (str.charAt(i-m) - '0');
           ZeroesInWindow++;
        }

        // Update maxProd
        if(ZeroesInWindow==0)
        maxProd = Math.max(maxProd, product);

        // Add the current digit and subtract
        // the first digit of previous window
        sum = sum + (str.charAt(i) - '0') - ((str.charAt(i-m)) - '0');

        // Update maxSum
        maxSum = Math.max(maxSum, sum);
    }

    System.out.println("Maximum Product = " + maxProd);
    System.out.println("\nMaximum Sum = " + maxSum);
}

// Driver code
    public static void main (String[] args) {
        String str = "3601990545";
        int m = 3;
        maxProductSum(str, m);
    }
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to find the maximum product and sum
def maxProductSum(str, m):

    n = len(str)
    product = 1
    sum = 0

    # find the sum and product of first K digits
    for i in range(m):
        sum += (ord(str[i]) - ord('0'))
        product *= (ord(str[i]) - ord('0'))

    # Update maxProd and maxSum
    maxProd = product
    maxSum = sum

    # Start traversing the next element
    for i in range(m, n) :

        # Multiply with the current digit and divide
        # by the first digit of previous window
        product = (product * (ord(str[i]) - ord('0')) //
                            ((ord(str[i - m])) - ord('0')))

        # Add the current digit and subtract
        # the first digit of previous window
        sum = (sum + (ord(str[i]) - ord('0')) -
                    ((ord(str[i - m])) - ord('0')))

        # Update maxProd and maxSum
        maxProd = max(maxProd, product)
        maxSum = max(maxSum, sum)

    print("Maximum Product =", maxProd)
    print("Maximum Sum =", maxSum)

# Driver code
if __name__ == "__main__":

    str = "3675356291"
    m = 5

    maxProductSum(str, m)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to find the maximum product and sum
static void maxProductSum(string str, int m)
{
    int n = str.Length;
    int product = 1, sum = 0;

    // find the sum and product of first K digits
    for (int i = 0; i < m; i++)
    {
        sum += (str[i] - '0');
        product *= (str[i] - '0');
    }

    // Update maxProd and maxSum
    int maxProd = product;
    int maxSum = sum;

    // Start traversing the next element
    for (int i = m; i < n; i++)
    {

        // Multiply with the current digit and divide by
        // the first digit of previous window
        product = product * (str[i] - '0') / ((str[i - m]) - '0');

        // Add the current digit and subtract
        // the first digit of previous window
        sum = sum + (str[i] - '0') - ((str[i - m]) - '0');

        // Update maxProd and maxSum
        maxProd = Math.Max(maxProd, product);
        maxSum = Math.Max(maxSum, sum);
    }

    Console.Write("Maximum Product = " + maxProd);
    Console.Write("\nMaximum Sum = " + maxSum);
}

// Driver code
public static void Main()
{
    string str = "3675356291";
    int m = 5;

    maxProductSum(str, m);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the maximum
// product and sum
function maxProductSum($str, $m)
{
    $n = strlen($str);
    $product = 1;
    $sum = 0;

    // find the sum and product of
    // first K digits
    for ($i = 0; $i < $m; $i++)
    {
        $sum += ($str[$i] - '0');
        $product *= ($str[$i] - '0');
    }

    // Update maxProd and maxSum
    $maxProd = $product;
    $maxSum = $sum;

    // Start traversing the next element
    for ($i = $m; $i < $n; $i++)
    {

        // Multiply with the current digit and divide
        // by the first digit of previous window
        $product = $product * ($str[$i] - '0') /
                             (($str[$i - $m]) - '0');

        // Add the current digit and subtract
        // the first digit of previous window
        $sum = $sum + ($str[$i] - '0') -
                     (($str[$i - $m]) - '0');

        // Update maxProd and maxSum
        $maxProd = max($maxProd, $product);
        $maxSum = max($maxSum, $sum);
    }

    echo "Maximum Product = " , $maxProd;
    echo "\nMaximum Sum = " , $maxSum;
}

// Driver code
$str = "3675356291";
$m = 5;
maxProductSum($str, $m);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>   
    // Javascript implementation of the above approach

    // Function to find the maximum product and sum
    function maxProductSum(str, m)
    {
        let n = str.length;
        let product = 1, sum = 0;

        // find the sum and product of first K digits
        for (let i = 0; i < m; i++)
        {
            sum += (str[i].charCodeAt() - '0'.charCodeAt());
            product *= (str[i].charCodeAt() - '0'.charCodeAt());
        }

        // Update maxProd and maxSum
        let maxProd = product;
        let maxSum = sum;

        // Start traversing the next element
        for (let i = m; i < n; i++)
        {

            // Multiply with the current digit and divide by
            // the first digit of previous window
            product = product * (str[i].charCodeAt() - '0'.charCodeAt()) / ((str[i - m].charCodeAt()) - '0'.charCodeAt());

            // Add the current digit and subtract
            // the first digit of previous window
            sum = sum + (str[i].charCodeAt() - '0'.charCodeAt()) - ((str[i - m].charCodeAt()) - '0'.charCodeAt());

            // Update maxProd and maxSum
            maxProd = Math.max(maxProd, product);
            maxSum = Math.max(maxSum, sum);
        }

        document.write("Maximum Product = " + maxProd + "</br>");
        document.write("Maximum Sum = " + maxSum);
    }

    let str = "3675356291";
    let m = 5;

    maxProductSum(str, m);

</script>
```

**Output**

```
Maximum Product = 100
Maximum Sum = 19
```