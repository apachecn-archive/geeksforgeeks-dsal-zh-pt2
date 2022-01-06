# 执行给定操作后数组中相等数字的最大计数

> 原文:[https://www . geeksforgeeks . org/执行给定操作后数组中相等数字的最大计数/](https://www.geeksforgeeks.org/maximum-count-of-equal-numbers-in-an-array-after-performing-given-operations/)

给定一个整数数组。任务是在多次应用给定操作后，找到数组中相等数字的最大计数。
在操作中:

> 1.选择数组的两个元素 a[i]，a[j](这样 I 不等于 j)和，
> 2。将数字 a[i]增加 1，将数字 a[j]减少 1，即 **a[i] = a[i] + 1** 和**a[j]= a[j]–1**。

**示例** :

```
Input: a = { 1, 4, 1 }
Output: 3
after first step { 1, 3, 2}
after second step { 2, 2, 2}

Input: a = { 1, 2 }
Output: 1
```

**进场:**

1.  计算数组元素的总和。
2.  如果和能被 n 整除，其中 n 是数组中元素的个数，那么答案也是 n。
3.  否则，答案将是 n-1。

以下是上述方法的实现:

## C++

```
// CPP program to find the maximum
// number of equal numbers in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// equal numbers in an array
int EqualNumbers(int a[], int n)
{
    // to store sum of elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    // if sum of numbers is not divisible
    // by n
    if (sum % n)
        return n - 1;

    return n;
}

// Driver Code
int main()
{
    int a[] = { 1, 4, 1 };

    // size of an array
    int n = sizeof(a) / sizeof(a[0]);

    cout << EqualNumbers(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// number of equal numbers in an array

public class GFG{

    // Function to find the maximum number of
    // equal numbers in an array
    static int EqualNumbers(int a[], int n)
    {
        // to store sum of elements
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += a[i];

        // if sum of numbers is not divisible
        // by n
        if (sum % n != 0)
            return n - 1;

        return n;
    }

    // Driver code
    public static void main(String args[])
    {
            int a[] = { 1, 4, 1 };

            // size of an array
            int n = a.length;

            System.out.println(EqualNumbers(a, n));
    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# number of equal numbers in an array

# Function to find the maximum
# number of equal numbers in an array
def EqualNumbers(a, n):

    # to store sum of elements
    sum = 0;
    for i in range(n):
        sum += a[i];

    # if sum of numbers is not
    # divisible by n
    if (sum % n):
        return n - 1;

    return n;

# Driver Code
a = [1, 4, 1 ];

# size of an array
n = len(a);

print(EqualNumbers(a, n));

# This code is contributed by mits
```

## C#

```
// C# program to find the maximum
// number of equal numbers in an array
using System;

class GFG
{
// Function to find the maximum
// number of equal numbers in an array
static int EqualNumbers(int []a, int n)
{
    // to store sum of elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    // if sum of numbers is not
    // divisible by n
    if (sum % n != 0)
        return n - 1;

    return n;
}

// Driver code
static public void Main ()
{
    int []a = { 1, 4, 1 };

    // size of an array
    int n = a.Length;

    Console.WriteLine(EqualNumbers(a, n));
}
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// number of equal numbers in an array

// Function to find the maximum
// number of equal numbers in an array
function EqualNumbers($a, $n)
{
    // to store sum of elements
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $a[$i];

    // if sum of numbers is not
    // divisible by n
    if ($sum % $n)
        return $n - 1;

    return $n;
}

// Driver Code
$a = array(1, 4, 1 );

// size of an array
$n = sizeof($a);

echo EqualNumbers($a, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum
// number of equal numbers in an array

// Function to find the maximum number of
// equal numbers in an array
function EqualNumbers(a, n)
{
    // to store sum of elements
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += a[i];

    // if sum of numbers is not divisible
    // by n
    if (sum % n)
        return n - 1;

    return n;
}

// Driver Code

    let a = [ 1, 4, 1 ];

    // size of an array
    let n = a.length;

    document.write(EqualNumbers(a, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```