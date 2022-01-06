# 求给定数组元素阶乘的 GCD

> 原文:[https://www . geeksforgeeks . org/find-gcd-of-factorial-of-of-elements-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of-of](https://www.geeksforgeeks.org/find-gcd-of-factorial-of-elements-of-given-array/)

给定一个有 N 个正整数的数组。求数组所有元素阶乘的 GCD。
**例:**

```
Input : arr[] = {3, 4, 8, 6}
Output : 6

Input : arr[] = {13, 24, 8, 5}
Output : 120
```

**方法:**求所有元素的[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 首先计算所有元素的阶乘，然后求出它们的 GCD。但这似乎是一个非常漫长的过程。两个数的 GCD 是两个数相除的最大数。因此，两个数的阶乘的 GCD 是最小数本身的阶乘的值。
*比如*:GCD 3！(6)和 5！(120)是 3！(即 6)本身。
因此要找到给定数组所有元素的阶乘的 GCD，找到最小的元素，然后打印它的阶乘，这将是我们需要的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Implementation of factorial function
int factorial(int n)
{
    return (n == 1 || n == 0) ? 1 : factorial(n - 1) * n;
}

// Function to find GCD of factorial of
// elements from array
int gcdOfFactorial(int arr[], int n)
{
    // find the minimum element of array
    int minm = arr[0];
    for (int i = 1; i < n; i++)
        minm = minm > arr[i] ? arr[i] : minm;

    // return the factorial of minimum element
    return factorial(minm);
}

// Driver Code
int main()
{
    int arr[] = { 9, 12, 122, 34, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << gcdOfFactorial(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Implementation of factorial function
static int factorial(int n)
{
    return (n == 1 || n == 0) ? 1 : factorial(n - 1) * n;
}

// Function to find GCD of factorial of
// elements from array
static int gcdOfFactorial(int []arr, int n)
{
    // find the minimum element of array
    int minm = arr[0];
    for (int i = 1; i < n; i++)
        minm = minm > arr[i] ? arr[i] : minm;

    // return the factorial of minimum element
    return factorial(minm);
}

// Driver Code
public static void main (String[] args)
{
    int []arr = { 9, 12, 122, 34, 15 };
    int n = arr.length;
    System.out.println(gcdOfFactorial(arr, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Implementation of factorial function
def factorial(n):
    if n == 1 or n == 0:
        return 1
    else:
        return factorial(n - 1) * n

# Function to find GCD of factorial
# of elements from array
def gcdOfFactorial(arr, n):

    # find the minimum element
    # of array
    minm = arr[0]
    for i in range(1, n):
        if minm > arr[i]:
            minm = arr[i]
        else:
            arr[i] = minm

    # return the factorial of
    # minimum element
    return factorial(minm)

# Driver Code
arr = [9, 12, 122, 34, 15 ]
n = len(arr)
print(gcdOfFactorial(arr, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Implementation of factorial function
static int factorial(int n)
{
    return (n == 1 || n == 0) ? 1 : factorial(n - 1) * n;
}

// Function to find GCD of factorial of
// elements from array
static int gcdOfFactorial(int []arr, int n)
{
    // find the minimum element of array
    int minm = arr[0];
    for (int i = 1; i < n; i++)
        minm = minm > arr[i] ? arr[i] : minm;

    // return the factorial of minimum element
    return factorial(minm);
}

// Driver Code
static void Main()
{
    int []arr = { 9, 12, 122, 34, 15 };
    int n = arr.Length;
    Console.WriteLine(gcdOfFactorial(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Implementation of factorial function
function factorial($n)
{
    return ($n == 1 || $n == 0) ? 1 :
              factorial($n - 1) * $n;
}

// Function to find GCD of factorial of
// elements from array
function gcdOfFactorial($arr, $n)
{
    // find the minimum element of array
    $minm = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $minm = $minm > $arr[$i] ?
                        $arr[$i] : $minm;

    // return the factorial of minimum element
    return factorial($minm);
}

// Driver Code
$arr = array( 9, 12, 122, 34, 15 );
$n = count($arr);
echo gcdOfFactorial($arr, $n);

// This code is contributed by Srathore
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach   

// Implementation of factorial function
    function factorial(n) {
        return (n == 1 || n == 0) ? 1 : factorial(n - 1) * n;
    }

    // Function to find GCD of factorial of
    // elements from array
    function gcdOfFactorial(arr , n) {
        // find the minimum element of array
        var minm = arr[0];
        for (i = 1; i < n; i++)
            minm = minm > arr[i] ? arr[i] : minm;

        // return the factorial of minimum element
        return factorial(minm);
    }

    // Driver Code

        var arr = [ 9, 12, 122, 34, 15 ];
        var n = arr.length;
        document.write(gcdOfFactorial(arr, n));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
362880
```