# 沙漠编号

> 原文:[https://www.geeksforgeeks.org/deserium-number/](https://www.geeksforgeeks.org/deserium-number/)

**Deserium Number:** 如果一个数的位数相对于从 1 到位数的幂的和等于该数本身，则称该数为 Deserium Number。

**示例:**

```
Input : 135
Output : Yes
1^1 + 3^2 + 5^3 = 135

Input : 9
Output : Yes
9^1 = 9

Input  : 125
Output : No
1^1+2^2+5^3 != 125
```

想法很简单。
1)计算给定数字的位数。
2)从最右边的数字到最左边的数字遍历，计算幂的和。
3)如果幂的和等于给定的数，返回真。

## C++

```
// C++ program to check whether a number
// is Deserium number or not
#include <iostream>
#include <math.h>

using namespace std;

// Returns count of digits in n.
int countDigits(int n)
{
    int c = 0;

    do {
        c++;
        n = n / 10;
    } while (n != 0);

    return c;
}

// Returns true if x is Diserium
bool isDeserium(int x)
{
    int temp = x;
    int p = countDigits(x);

    // Compute powers of digits
    // from right to left.
    int sum = 0;
    while (x != 0) {
        int digit = x % 10;
        sum += pow(digit, p);
        p--;
        x = x / 10;
    }

    // If sum of powers is same as
    // given number.
    return (sum == temp);
}

// Driver code
int main()
{
    int x = 135;

    if (isDeserium(x))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}

// This code is contributed by vt_m.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number
// is Deserium number or not
import java.util.Scanner;
class Deserium {

    // Returns count of digits in n.
    static int countDigits(int n)
    {
        int c = 0;
        do {
            c++;
            n = n / 10;
        } while (n != 0);
        return c;
    }

    // Returns true if x is Diserium
    static boolean isDeserium(int x)
    {
        int temp = x;
        int p = countDigits(x);

        // Compute powers of digits
        // from right to left.
        int sum = 0;
        while (x != 0) {
            int digit = x % 10;
            sum += Math.pow(digit, p);
            p--;
            x = x / 10;
        }

        // If sum of powers is same as
        // given number.
        return (sum == temp);
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 135;
        if (isDeserium(x))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check whether
# a number is Deserium number or not

# Returns count of digits in n.
def countDigits(n):

    c = 0
    while (n != 0):
        c += 1
        n = int( n / 10)

    return c

# Returns true if x is Diserium
def isDeserium(x):

    temp = x
    p = countDigits(x)

    # Compute powers of digits
    # from right to left.
    sum = 0
    while (x != 0):
        digit = int(x % 10)
        sum += pow(digit, p)
        p -= 1
        x = int(x / 10)

    # If sum of powers is same as
    # given number.
    return (sum == temp)

# Driver code
x = 135
if (isDeserium(x)):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to check whether a number
// is Deserium number or not
using System;

class Deserium {

    // Returns count of digits in n.
    static int countDigits(int n)
    {
        int c = 0;
        do {
            c++;
            n = n / 10;
        } while (n != 0);
        return c;
    }

    // Returns true if x is Diserium
    static bool isDeserium(int x)
    {
        int temp = x;
        int p = countDigits(x);

        // Compute powers of digits
        // from right to left.
        int sum = 0;
        while (x != 0) {
            int digit = x % 10;
            sum += (int)Math.Pow(digit, p);
            p--;
            x = x / 10;
        }

        // If sum of powers is same as
        // given number.
        return (sum == temp);
    }

    // Driver code
    public static void Main()
    {
        int x = 135;

        if (isDeserium(x))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// whether a number is
// Deserium number or not

// Returns count of
// digits in n.
function countDigits($n)
{
    $c = 0;

    do
    {
        $c++;
        $n = $n / 10;
    } while ($n != 0);

    return $c;
}

// Returns true if
// x is Diserium
function isDeserium($x)
{
    $temp = $x;
    $p = countDigits($x);

    // Compute powers of digits
    // from right to left.
    $sum = 0;
    while ($x != 0)
    {
        $digit = $x % 10;
        $sum += pow($digit, $p);
        $p--;
        $x = $x / 10;
    }

    // If sum of powers is
    // same as given number.
    return ($sum == $temp);
}

// Driver Code
$x = 135;

if (isDeserium($x))
    echo "No";
else
    echo "Yes";

// This code is contributed by aj_36.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check whether
// a number is Deserium number or not

// Returns count of digits in n.
function countDigits(n)
{
    let c = 0;
    do
    {
        c++;
        n = Math.floor(n / 10);
    } while (n != 0);
    return c;
}

// Returns true if x is Diserium
function isDeserium(x)
{
    let temp = x;
    let p = countDigits(x);

    // Compute powers of digits
    // from right to left.
    let sum = 0;
    while (x != 0)
    {
        let digit = x % 10;
        sum += Math.floor(Math.pow(digit, p));
        p--;
        x = Math.floor(x / 10);
    }

    // If sum of powers is same as
    // given number.
    return (sum == temp);
}

// Driver Code
let x = 135;

if (isDeserium(x))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by code_hunt

</script>
```

**输出:**

```
Yes
```