# 将两个给定的数除以它们的公约数

> 原文:[https://www . geeksforgeeks . org/将两个给定的数字除以它们的公约数/](https://www.geeksforgeeks.org/divide-the-two-given-numbers-by-their-common-divisors/)

给定两个数 A 和 B，任务是用它们的公约数除这两个数 A 和 B。数字 a 和 b 小于 10^8.
**例:**

```
Input: A = 10, B = 15
Output: A = 2, B = 3
The common factors are 1, 5

Input: A = 100, B = 150
Output: A = 2, B = 3
```

**天真法:**从 i = 1 迭代到 A 和 B 的最小值，检查 **i** 是否是 A 和 B 的因子，如果 **i** 是 **A** 和 **B** 的因子，那么将 A 和 B 两个数除以 I
以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// print the numbers after dividing
// them by their common factors
void divide(int a, int b)
{
    // iterate from 1 to minimum of a and b
    for (int i = 2; i <= min(a, b); i++) {

        // if i is the common factor
        // of both the numbers
        while (a % i == 0 && b % i == 0) {
            a = a / i;
            b = b / i;
        }
    }

    cout << "A = " << a << ", B = " << b << endl;
}

// Driver code
int main()
{
    int A = 10, B = 15;

    // divide A and B by their common factors
    divide(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class solution
{

// print the numbers after dividing
// them by their common factors
static void divide(int a, int b)
{
    // iterate from 1 to minimum of a and b
    for (int i = 2; i <= Math.min(a, b); i++) {

        // if i is the common factor
        // of both the numbers
        while (a % i == 0 && b % i == 0) {
            a = a / i;
            b = b / i;
        }
    }

    System.out.println("A = "+a+", B = "+b);
}

// Driver code
public static void main(String args[])
{
    int A = 10, B = 15;

    // divide A and B by their common factors
    divide(A, B);

}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# print the numbers after dividing
# them by their common factors
def divide(a, b) :

    # iterate from 1 to minimum of a and b
    for i in range(2, min(a, b) + 1) :

        # if i is the common factor
        # of both the numbers
        while (a % i == 0 and b % i == 0) :
            a = a // i
            b = b // i

    print("A =", a, ", B =", b)

# Driver code
if __name__ == "__main__" :

    A, B = 10, 15

    # divide A and B by their
    # common factors
    divide(A, B)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// print the numbers after dividing
// them by their common factors
static void divide(int a, int b)
{
    // iterate from 1 to minimum of a and b
    for (int i = 2; i <= Math.Min(a, b); i++)
    {

        // if i is the common factor
        // of both the numbers
        while (a % i == 0 && b % i == 0)
        {
            a = a / i;
            b = b / i;
        }
    }
    Console.WriteLine("A = "+a+", B = "+b);
}

// Driver code
static public void Main ()
{
    int A = 10, B = 15;

    // divide A and B by their common factors
    divide(A, B);
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
// print the numbers after dividing
// them by their common factors

function divide($a, $b)
{
    // iterate from 1 to minimum of a and b
    for ($i = 2; $i <= min($a, $b); $i++)
    {

        // if i is the common factor
        // of both the numbers
        while ($a % $i == 0 &&
                $b % $i == 0)
        {
            $a = $a / $i;
            $b = $b / $i;
        }
    }
    echo "A = ", $a, ", B = ", $b, "\n";
}

// Driver code
$A = 10;
$B = 15;

// divide A and B by their common factors
divide($A, $B);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// print the numbers after dividing
// them by their common factors
function divide(a, b)
{
    // iterate from 1 to minimum of a and b
    for (let i = 2; i <= Math.min(a, b); i++) {

        // if i is the common factor
        // of both the numbers
        while (a % i == 0 && b % i == 0) {
            a = a / i;
            b = b / i;
        }
    }

    document.write("A = " + a + ", B = " + b + "<br>");
}

// Driver code

    let A = 10, B = 15;

    // divide A and B by their common factors
    divide(A, B);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
A = 2, B = 3
```