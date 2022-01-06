# 将一个数字分成两部分，使位数之和最大

> 原文:[https://www . geesforgeks . org/将一个数字分成两部分，这样数字的总和就是最大值/](https://www.geeksforgeeks.org/divide-a-number-into-two-parts-such-that-sum-of-digits-is-maximum/)

给定一个数字 n，任务是找到 sumofdigts(A)+sumofdigts(B)的最大可能值，使得 A + B = n (0<=A，B<=n)。

**示例:**

```
Input: N = 35
Output: 17
35 = 9 + 26
SumOfDigits(26) = 8, SumOfDigits(9) = 9
So, 17 is the answer.

Input: N = 7
Output: 7
```

**方法:**想法是将数字分成 A 和 B 两部分，这样 A 就等于 9，即最接近 N 的数字，B = N-A。例如，N = 35，最接近 35 的最小数字是 29。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Returns sum of digits of x
int sumOfDigitsSingle(int x)
{
    int ans = 0;
    while (x) {
        ans += x % 10;
        x /= 10;
    }
    return ans;
}

// Returns closest number to x in terms of 9's.
int closest(int x)
{
    int ans = 0;
    while (ans * 10 + 9 <= x)
        ans = ans * 10 + 9;

    return ans;
}

int sumOfDigitsTwoParts(int N)
{
    int A = closest(N);
    return sumOfDigitsSingle(A) + sumOfDigitsSingle(N - A);
}

// Driver code
int main()
{
    int N = 35;
    cout << sumOfDigitsTwoParts(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
// Returns sum of digits of x
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
static int sumOfDigitsSingle(int x)
{
    int ans = 0;
    while (x != 0)
    {
        ans += x % 10;
        x /= 10;
    }
    return ans;
}

// Returns closest number to x
// in terms of 9's.
static int closest(int x)
{
    int ans = 0;
    while (ans * 10 + 9 <= x)
        ans = ans * 10 + 9;

    return ans;
}

static int sumOfDigitsTwoParts(int N)
{
    int A = closest(N);
    return sumOfDigitsSingle(A) +
           sumOfDigitsSingle(N - A);
}

// Driver code
public static void main(String args[])
{
    int N = 35;
    System.out.print(sumOfDigitsTwoParts(N));
}
}

// This code is contributed by
// Subhadeep Gupta
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

#  Returns sum of digits of x
def sumOfDigitsSingle(x) :
    ans = 0
    while x :
        ans += x % 10
        x //= 10

    return ans

# Returns closest number to x in terms of 9's
def closest(x) :
    ans = 0
    while (ans * 10 + 9 <= x) :
        ans = ans * 10 + 9

    return ans

def sumOfDigitsTwoParts(N) :
    A = closest(N)

    return sumOfDigitsSingle(A) + sumOfDigitsSingle(N - A)

# Driver Code
if __name__ == "__main__" :

    N = 35
    print(sumOfDigitsTwoParts(N))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
// Returns sum of digits of x

using System;
class GFG
{
static int sumOfDigitsSingle(int x)
{
    int ans = 0;
    while (x != 0)
    {
        ans += x % 10;
        x /= 10;
    }
    return ans;
}

// Returns closest number to x
// in terms of 9's.
static int closest(int x)
{
    int ans = 0;
    while (ans * 10 + 9 <= x)
        ans = ans * 10 + 9;

    return ans;
}

static int sumOfDigitsTwoParts(int N)
{
    int A = closest(N);
    return sumOfDigitsSingle(A) +
           sumOfDigitsSingle(N - A);
}

// Driver code
public static void Main()
{
    int N = 35;
    Console.Write(sumOfDigitsTwoParts(N));
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Returns sum of digits of x
function sumOfDigitsSingle($x)
{
    $ans = 0;
    while ($x)
    {
        $ans += $x % 10;
        $x /= 10;
    }
    return $ans;
}

// Returns closest number
// to x in terms of 9's.
function closest($x)
{
    $ans = 0;
    while ($ans * 10 + 9 <= $x)
        $ans = $ans * 10 + 9;

    return $ans;
}

function sumOfDigitsTwoParts($N)
{
    $A = closest($N);
    return sumOfDigitsSingle($A) +
           sumOfDigitsSingle($N - $A);
}

// Driver code
$N = 35;
echo sumOfDigitsTwoParts($N);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Returns sum of digits of x
function sumOfDigitsSingle(x)
{
    let ans = 0;
    while (x)
    {
        ans += x % 10;
        x = Math.floor(x / 10);
    }
    return ans;
}

// Returns closest number to x
// in terms of 9's.
function closest(x)
{
    let ans = 0;

    while(ans * 10 + 9 <= x)
        ans = ans * 10 + 9;

    return ans;
}

function sumOfDigitsTwoParts(N)
{
    let A = closest(N);
    return sumOfDigitsSingle(A) +
           sumOfDigitsSingle(N - A);
}

// Driver code
let N = 35;

document.write(sumOfDigitsTwoParts(N));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
17
```