# 对于大数

找到 a^b 的最后一位数字

> 原文:[https://www . geeksforgeeks . org/find-大数字 ab 的最后一位数字/](https://www.geeksforgeeks.org/find-last-digit-of-ab-for-large-numbers/)

给你两个整数，基数 a(位数 d，如 1 <= d <= 1000) and the index b (0 <= b <= 922*10^15). You have to find the last digit of a^b.
例:

```
Input  : 3 10
Output : 9

Input  : 6 2
Output : 6

Input  : 150 53
Output : 0
```

举几个例子后，我们可以注意到下面的模式。

```
Number  |  Last digits that repeat in cycle
  1     |     1
  2     |  4, 8, 6, 2
  3     |  9, 7, 1, 3
  4     |  6, 4
  5     |  5
  6     |  6
  7     |  9, 3, 1, 7
  8     |  4, 2, 6, 8
  9     |  1, 9
```

在给定的表中，我们可以看到循环重复的最大长度是 4。
**例:**2 * 2 = 4 * 2 = 8 * 2 = 16 * 2 = 32 32 中的最后一位数字是 2，表示乘以 4 次数字后重复自身。所以算法很简单。
来源:[Brilliants.org](https://brilliant.org/wiki/finding-the-last-digit-of-a-power/)
**<u>算法:</u>**

1.  由于数字非常大，我们将它们存储为字符串。
2.  取基数 a 的最后一位数字。
3.  现在计算 b%4。这里 b 很大。
    *   如果 b%4==0，这意味着 b 完全可以被 4 整除，那么我们的指数现在将是 exp = 4，因为通过将数字乘以 4，我们根据上图中的循环表得到了最后一位数字。
    *   如果 b%4！=0 这意味着 b 不能完全被 4 整除，所以我们现在的指数将是 exp=b%4，因为通过指数乘以数，我们根据上图中的循环表得到最后一位数字。
    *   现在计算 ldigit = pow(最后一位数字 in_base，exp)。
    *   a^b 的最后一位是 ldigit%10。

下面是上述算法的实现。

## C++

```
// C++ code to find last digit of a^b
#include <bits/stdc++.h>
using namespace std;

// Function to find b % a
int Modulo(int a, char b[])
{
    // Initialize result
    int mod = 0;

    // calculating mod of b with a to make
    // b like 0 <= b < a
    for (int i = 0; i < strlen(b); i++)
        mod = (mod * 10 + b[i] - '0') % a;

    return mod; // return modulo
}

// function to find last digit of a^b
int LastDigit(char a[], char b[])
{
    int len_a = strlen(a), len_b = strlen(b);

    // if a and b both are 0
    if (len_a == 1 && len_b == 1 && b[0] == '0' && a[0] == '0')
        return 1;

    // if exponent is 0
    if (len_b == 1 && b[0] == '0')
        return 1;

    // if base is 0
    if (len_a == 1 && a[0] == '0')
        return 0;

    // if exponent is divisible by 4 that means last
    // digit will be pow(a, 4) % 10.
    // if exponent is not divisible by 4 that means last
    // digit will be pow(a, b%4) % 10
    int exp = (Modulo(4, b) == 0) ? 4 : Modulo(4, b);

    // Find last digit in 'a' and compute its exponent
    int res = pow(a[len_a - 1] - '0', exp);

    // Return last digit of result
    return res % 10;
}

// Driver program to run test case
int main()
{
    char a[] = "117", b[] = "3";
    cout << LastDigit(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find last digit of a^b
import java.io.*;
import java.math.*;

class GFG {

    // Function to find b % a
    static int Modulo(int a, char b[])
    {
        // Initialize result
        int mod = 0;

        // calculating mod of b with a to make
        // b like 0 <= b < a
        for (int i = 0; i < b.length; i++)
            mod = (mod * 10 + b[i] - '0') % a;

        return mod; // return modulo
    }

    // Function to find last digit of a^b
    static int LastDigit(char a[], char b[])
    {
        int len_a = a.length, len_b = b.length;

        // if a and b both are 0
        if (len_a == 1 && len_b == 1 && b[0] == '0' && a[0] == '0')
            return 1;

        // if exponent is 0
        if (len_b == 1 && b[0] == '0')
            return 1;

        // if base is 0
        if (len_a == 1 && a[0] == '0')
            return 0;

        // if exponent is divisible by 4 that means last
        // digit will be pow(a, 4) % 10.
        // if exponent is not divisible by 4 that means last
        // digit will be pow(a, b%4) % 10
        int exp = (Modulo(4, b) == 0) ? 4 : Modulo(4, b);

        // Find last digit in 'a' and compute its exponent
        int res = (int)(Math.pow(a[len_a - 1] - '0', exp));

        // Return last digit of result
        return res % 10;
    }

    // Driver program to run test case
    public static void main(String args[]) throws IOException
    {
        char a[] = "117".toCharArray(), b[] = { '3' };
        System.out.println(LastDigit(a, b));
    }
}

// This code is contributed by Nikita Tiwari.
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-2">蟒蛇 3</gfg-tab>T2】

```
 # Python 3 code to find last digit of a ^ b

import math

# Function to find b % a
def Modulo(a, b) :
    # Initialize result
    mod = 0

    # calculating mod of b with a to make
    # b like 0 <= b < a
    for i in range(0, len(b)) :
        mod = (mod * 10 + (int)(b[i])) % a

    return mod # return modulo

# function to find last digit of a ^ b
def LastDigit(a, b) :
    len_a = len(a)
    len_b = len(b)

    # if a and b both are 0
    if (len_a == 1 and len_b == 1 and b[0] == '0' and a[0] == '0') :
        return 1

    # if exponent is 0
    if (len_b == 1 and b[0]=='0') :
        return 1

    # if base is 0
    if (len_a == 1 and a[0] == '0') :
        return 0

    # if exponent is divisible by 4 that means last
    # digit will be pow(a, 4) % 10.
    # if exponent is not divisible by 4 that means last
    # digit will be pow(a, b % 4) % 10
    if((Modulo(4, b) == 0)) :
        exp = 4
    else : 
        exp = Modulo(4, b)

    # Find last digit in 'a' and compute its exponent
    res = math.pow((int)(a[len_a - 1]), exp)

    # Return last digit of result
    return res % 10

# Driver program to run test case
a = ['1', '1', '7']
b = ['3']
print(LastDigit(a, b))

# This code is contributed to Nikita Tiwari. 
```

## C#

```
// C# code to find last digit of a^b.
using System;

class GFG {

    // Function to find b % a
    static int Modulo(int a, char[] b)
    {

        // Initialize result
        int mod = 0;

        // calculating mod of b with a
        // to make b like 0 <= b < a
        for (int i = 0; i < b.Length; i++)
            mod = (mod * 10 + b[i] - '0') % a;

        // return modulo
        return mod;
    }

    // Function to find last digit of a^b
    static int LastDigit(char[] a, char[] b)
    {
        int len_a = a.Length, len_b = b.Length;

        // if a and b both are 0
        if (len_a == 1 && len_b == 1 &&
                   b[0] == '0' && a[0] == '0')
            return 1;

        // if exponent is 0
        if (len_b == 1 && b[0] == '0')
            return 1;

        // if base is 0
        if (len_a == 1 && a[0] == '0')
            return 0;

        // if exponent is divisible by 4
        // that means last digit will be
        // pow(a, 4) % 10\. if exponent is
        //not divisible by 4 that means last
        // digit will be pow(a, b%4) % 10
        int exp = (Modulo(4, b) == 0) ? 4
                            : Modulo(4, b);

        // Find last digit in 'a' and
        // compute its exponent
        int res = (int)(Math.Pow(a[len_a - 1]
                                - '0', exp));

        // Return last digit of result
        return res % 10;
    }

    // Driver program to run test case
    public static void Main()
    {

        char[] a = "117".ToCharArray(),
        b = { '3' };

        Console.Write(LastDigit(a, b));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php code to find last digit of a^b

// Function to find b % a
function Modulo($a, $b)
{

    // Initialize result
    $mod = 0;

    // calculating mod of b with a to make
    // b like 0 <= b < a
    for ($i = 0; $i < strlen($b); $i++)
        $mod = ($mod * 10 + $b[$i] - '0') % $a;

    return $mod; // return modulo
}

// function to find last digit of a^b
function LastDigit($a, $b)
{
    $len_a = strlen($a); $len_b = strlen($b);

    // if a and b both are 0
    if ($len_a == 1 && $len_b == 1 &&
                $b[0] == '0' && $a[0] == '0')
        return 1;

    // if exponent is 0
    if ($len_b == 1 && $b[0] == '0')
        return 1;

    // if base is 0
    if ($len_a == 1 && $a[0] == '0')
        return 0;

    // if exponent is divisible by 4 that
    // means last digit will be pow(a, 4)
    // % 10\. if exponent is not divisible
    // by 4 that means last digit will be
    // pow(a, b%4) % 10
    $exp = (Modulo(4, $b) == 0) ? 4 :
                              Modulo(4, $b);

    // Find last digit in 'a' and compute
    // its exponent
    $res = pow($a[$len_a - 1] - '0', $exp);

    // Return last digit of result
    return $res % 10;
}

// Driver program to run test case
$a = "117";
$b = "3";
echo LastDigit($a, $b);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript code to find last digit of a^b

// Function to find b % a
function Modulo(a, b)
{

    // Initialize result
    let mod = 0;

    // calculating mod of b with a to make
    // b like 0 <= b < a
    for (let i = 0; i < b.length; i++)
        mod = (mod * 10 + b[i] - '0') % a;

    return mod; // return modulo
}

// function to find last digit of a^b
function LastDigit(a, b)
{
    let len_a = a.length;
    let len_b = b.length;

    // if a and b both are 0
    if (len_a == 1 && len_b == 1 &&
                b[0] == '0' && a[0] == '0')
        return 1;

    // if exponent is 0
    if (len_b == 1 && b[0] == '0')
        return 1;

    // if base is 0
    if (len_a == 1 && a[0] == '0')
        return 0;

    // if exponent is divisible by 4 that
    // means last digit will be pow(a, 4)
    // % 10\. if exponent is not divisible
    // by 4 that means last digit will be
    // pow(a, b%4) % 10
    exp = (Modulo(4, b) == 0) ? 4 :
                            Modulo(4, b);

    // Find last digit in 'a' and compute
    // its exponent
    res = Math.pow(a[len_a - 1] - '0', exp);

    // Return last digit of result
    return res % 10;
}

// Driver program to run test case
let a = "117";
let b = "3";
document.write(LastDigit(a, b));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
3
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 geeksforgeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。