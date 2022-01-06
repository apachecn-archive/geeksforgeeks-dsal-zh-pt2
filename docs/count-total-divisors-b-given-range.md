# 计算给定范围内 A 或 B 的总除数

> 原文:[https://www . geesforgeks . org/count-total-dividers-b-给定-range/](https://www.geeksforgeeks.org/count-total-divisors-b-given-range/)

给定四个整数 m，n，a，b .找出 m 到 n 范围内有多少整数可以被 a **或** b.
**举例:**

```
Input: 3 11 2 3
Output: 6
Explanation:
m = 3, n = 11, a = 2, b = 3
There are total 6 numbers from 3 to 
11 which are divisible by 2 or 3 i.e, 
3, 4, 6, 8, 9, 10 

Input: arr[] = {11, 1000000, 6, 35}
Output: 190475
```

A **天真的方法**是运行一个从 m 到 n 的循环，并计算所有可被 a 或 b 整除的数字。这种方法的时间复杂度将是 O(m–n)，对于 m 的大值，这肯定会超时。
一种**有效的方法**是使用简单的 LCM 和除法。

1.  将 **n** 除以 a，得到可被“a”整除的所有数字(1 到 n)的总数。

2.  将 **m-1** 除以 a，得到可被“a”整除的所有数字(1 到 m-1)的总数。

3.  减去步骤 1 和 2 的计数，得到 m 到 n 范围内的总除数

现在我们有了给定范围内 a 的除数。重复上面的步骤来计算“b”的除数。
将这些相加，得到除数‘a’和‘b’的总数。
但同时被 a 和 b 整除的数要数两次。因此，为了消除这种歧义，我们可以使用 a 和 b 的 LCM 来计算可被“a”和“b”整除的总数。

1.  查找“a”和“b”的 LCM。

2.  将 **n** 除以 LCM，得到可被‘a’和‘b’整除的数字(1 到 n)的个数。

3.  将 **m-1** 除以 LCM，得到可被‘a’和‘b’整除的数的个数(1 到 m-1)。

4.  减去步骤 2 和 3 的计数，得到“a”和“b”的总除数。

现在从之前的计算结果中减去这个结果，得到所有唯一除数“a”或“b”的总数。

## C++

```
// C++ program to count total divisors of 'a'
// or 'b' in a given range
#include <bits/stdc++.h>
using namespace std;

// Utility function to find LCM of two numbers
int FindLCM(int a, int b)
{
    return (a * b) / __gcd(a, b);
}

// Function to calculate all divisors in given range
int rangeDivisor(int m, int n, int a, int b)
{
    // Find LCM of a and b
    int lcm = FindLCM(a, b);

    int a_divisor = n / a - (m - 1) / a;
    int b_divisor = n / b - (m - 1) / b;

    // Find common divisor by using LCM
    int common_divisor = n / lcm - (m - 1) / lcm;

    int ans = a_divisor + b_divisor - common_divisor;
    return ans;
}

// Driver code
int main()
{
    int m = 3, n = 11, a = 2, b = 3;
    cout << rangeDivisor(m, n, a, b) << endl;

    m = 11, n = 1000000, a = 6, b = 35;
    cout << rangeDivisor(m, n, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total divisors of 'a'
// or 'b' in a given range

import java.math.BigInteger;

class Test
{
    // Utility method to find LCM of two numbers
    static int FindLCM(int a, int b)
    {
        return (a * b) / new BigInteger(a+"").gcd(new BigInteger(b+"")).intValue();
    }

    // method to calculate all divisors in given range
    static int rangeDivisor(int m, int n, int a, int b)
    {
        // Find LCM of a and b
        int lcm = FindLCM(a, b);

        int a_divisor = n / a - (m - 1) / a;
        int b_divisor = n / b - (m - 1) / b;

        // Find common divisor by using LCM
        int common_divisor = n / lcm - (m - 1) / lcm;

        int ans = a_divisor + b_divisor - common_divisor;
        return ans;
    }

    // Driver method
    public static void main(String args[])
    {
        int m = 3, n = 11, a = 2, b = 3;
        System.out.println(rangeDivisor(m, n, a, b));

        m = 11; n = 1000000 ; a = 6; b = 35;
        System.out.println(rangeDivisor(m, n, a, b));
    }
}
```

## 蟒蛇 3

```
# python program to count total divisors
# of 'a' or 'b' in a given range

def __gcd(x, y):

    if x > y:
        small = y
    else:
        small = x
    for i in range(1, small+1):
        if((x % i == 0) and (y % i == 0)):
            gcd = i

    return gcd

# Utility function to find LCM of two
# numbers
def FindLCM(a, b):
    return (a * b) / __gcd(a, b);

# Function to calculate all divisors in
# given range
def rangeDivisor(m, n, a, b):

    # Find LCM of a and b
    lcm = FindLCM(a, b)

    a_divisor = int( n / a - (m - 1) / a)
    b_divisor = int(n / b - (m - 1) / b)

    # Find common divisor by using LCM
    common_divisor =int( n / lcm - (m - 1) / lcm)

    ans = a_divisor + b_divisor - common_divisor
    return ans

# Driver code
m = 3
n = 11
a = 2
b = 3;
print(rangeDivisor(m, n, a, b))
m = 11
n = 1000000
a = 6
b = 35
print(rangeDivisor(m, n, a, b))

# This code is contributed by Sam007
```

## C#

```
// C# program to count total divisors
// of 'a' or 'b' in a given range
using System;

class GFG {

    static int GCD(int num1, int num2)
    {
        int Remainder;

        while (num2 != 0)
        {
            Remainder = num1 % num2;
            num1 = num2;
            num2 = Remainder;
        }

        return num1;
    }

    // Utility function to find LCM of
    // two numbers
    static int FindLCM(int a, int b)
    {
        return (a * b) / GCD(a, b);
    }

    // Function to calculate all divisors in given range
    static int rangeDivisor(int m, int n, int a, int b)
    {
        // Find LCM of a and b
        int lcm = FindLCM(a, b);

        int a_divisor = n / a - (m - 1) / a;
        int b_divisor = n / b - (m - 1) / b;

        // Find common divisor by using LCM
        int common_divisor = n / lcm - (m - 1) / lcm;

        int ans = a_divisor + b_divisor - common_divisor;
        return ans;
    }

    public static void Main ()
    {
        int m = 3, n = 11, a = 2, b = 3;
        Console.WriteLine(rangeDivisor(m, n, a, b));

        m = 11;    n = 1000000;
        a = 6; b = 35;
        Console.WriteLine(rangeDivisor(m, n, a, b));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count total
// divisors of 'a' or 'b' in
// a given range

function gcd($a, $b)
{
    return ($a % $b) ?
    gcd($b, $a % $b) :
                   $b;
}

// Utility function to
// find LCM of two numbers
function FindLCM($a, $b)
{
    return ($a * $b) / gcd($a, $b);
}

// Function to calculate
// all divisors in given range
function rangeDivisor($m, $n, $a, $b)
{
    // Find LCM of a and b
    $lcm = FindLCM($a, $b);

    $a_divisor = $n / $a - ($m - 1) / $a;
    $b_divisor = $n / $b - ($m - 1) / $b;

    // Find common divisor by using LCM
    $common_divisor = $n / $lcm -
                          ($m - 1) / $lcm;

    $ans = $a_divisor + $b_divisor -
                        $common_divisor;
    return $ans;
}

// Driver Code
$m = 3;
$n = 11;
$a = 2;
$b = 3;
print(ceil(rangeDivisor($m, $n, $a, $b)));
echo "\n";

$m = 11;
$n = 1000000;
$a = 6;
$b = 35;
print(ceil(rangeDivisor($m, $n,$a,$b)));

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

    // JavaScript program to count total divisors
    // of 'a' or 'b' in a given range

    function GCD(num1, num2)
    {
        let Remainder;

        while (num2 != 0)
        {
            Remainder = num1 % num2;
            num1 = num2;
            num2 = Remainder;
        }

        return num1;
    }

    // Utility function to find LCM of
    // two numbers
    function FindLCM(a, b)
    {
        return parseInt((a * b) / GCD(a, b), 10);
    }

    // Function to calculate all divisors in given range
    function rangeDivisor(m, n, a, b)
    {
        // Find LCM of a and b
        let lcm = FindLCM(a, b);

        let a_divisor = parseInt(n / a, 10) -
                        parseInt((m - 1) / a, 10);

        let b_divisor = parseInt(n / b, 10) -
                        parseInt((m - 1) / b, 10);

        // Find common divisor by using LCM
        let common_divisor = parseInt(n / lcm, 10) -
                             parseInt((m - 1) / lcm, 10);

        let ans = a_divisor + b_divisor - common_divisor;
        return ans;
    }

    let m = 3, n = 11, a = 2, b = 3;
    document.write(rangeDivisor(m, n, a, b) + "</br>");

    m = 11;    n = 1000000;
    a = 6; b = 35;
    document.write(rangeDivisor(m, n, a, b));

</script>
```

**输出:**

```
6
190475
```

**时间复杂度:** O(log(MAX(a，b))
**辅助空间:** O(1)
本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。