# 找出 AP 中给定素数倍数的第一个元素

> 原文:[https://www . geesforgeks . org/find-first-element-in-AP-哪个是给定素数的倍数/](https://www.geeksforgeeks.org/find-first-element-in-ap-which-is-multiple-of-given-prime/)

给定算术级数的第一项(A)和公共差(D)以及一个素数(P)。任务是找到给定 AP 中第一个元素的位置，它是给定素数 p 的倍数
**示例** :

> **输入** : A = 4，D = 9，P = 11
> **输出** : 2
> **解释** :
> 给定 AP 的第三项是
> 质数 11 的倍数。
> 第一项= 4
> 第二项= 4+9 = 13
> 第三项= 4+2*9 = 22
> **输入** : A = 5，D = 6，P = 7
> **输出** : 5
> **解释** :
> 给定 AP 的第六项是
> 素数 7 的倍数。
> 第一学期= 5
> 第二学期= 5+6 = 11
> 第三学期= 5+2*6 = 17
> 第四学期= 5+3*6 = 23
> 第五学期= 5+4*6 = 29
> 第六学期= 5+5*5 = 35

**方法:**
让术语为 A <sub>N</sub> 。因此，

```
AN = (A + (N-1)*D)
```

现在，假设 A <sub>N</sub> 是 p 的倍数，那么，

```
A + (N-1)*D = k*P

Where, k is a constant.
```

现在设 A 为(A % P)，D 为(D % P)。所以，我们有(N-1)* D =(k * P–A)。
在 RHS 上加减 P，得到:

```
(N-1)*D = P(k-1) + (P-A), 

Where P-A is a non-negative number 
(since A is replaced by A%P which is less than P)
```

最后两边取 mod:

```
     ((N-1)*D)%P = (P-A)%P
 or, ((N-1)D)%P = P-A
```

让我们找一个 X < P, such that (D*X)%P = 1\. This X is known as the inverse modulo of D with respect to P.
这样答案 N 就是:

```
((X*(P-A)) % P) + 1\. 
```

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Iterative Function to calculate
// (x^y)%p in O(log y) */
int power(int x, int y, int p)
{
    // Initialize result
    int res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to find nearest element in common
int NearestElement(int A, int D, int P)
{
    // base conditions
    if (A == 0)
        return 0;

    else if (D == 0)
        return -1;

    else {
        int X = power(D, P - 2, P);
        return (X * (P - A)) % P;
    }
}

// Driver code
int main()
{
    int A = 4, D = 9, P = 11;

    // module both A and D
    A %= P;
    D %= P;

    // function call
    cout << NearestElement(A, D, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Find First
// element in AP which is
// multiple of given prime
class GFG
{
// Iterative Function to
// calculate (x^y)%p in
// O(log y) */
static int power(int x,
                 int y, int p)
{
    // Initialize result
    int res = 1;

    // Update x if it is
    // more than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to find nearest
// element in common
static int NearestElement(int A,
                          int D, int P)
{
    // base conditions
    if (A == 0)
        return 0;

    else if (D == 0)
        return -1;

    else
    {
        int X = power(D, P - 2, P);
        return (X * (P - A)) % P;
    }
}

// Driver code
public static void main(String args[])
{
    int A = 4, D = 9, P = 11;

    // module both A and D
    A %= P;
    D %= P;

    // function call
    System.out.println(NearestElement(A, D, P));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 Program to Find First
# element in AP which is 
# multiple of given prime

# Iterative Function to calculate 
# (x^y)%p in O(log y)
def power(x, y, p) :

    # Initialize result
    res = 1

    # Update x if it is more than or
    # equal to p
    x = x % p

    while y > 0 :

        # If y is odd, multiply x with result
        if y & 1 :
            res = (res * x) % p

        # y must be even now
        #  y = y/2
        y = y >> 1
        x = (x * x) % p

    return res

# function to find nearest element in common
def NearestElement(A, D, P) :

    # base conditions
    if A == 0 :
        return 0

    elif D == 0 :
        return -1

    else :
        X = power(D, P - 2, P)
        return (X * (P - A)) % P

# Driver Code
if __name__ == "__main__" :

    A, D, P = 4, 9, 11

    # module both A and D
    A %= P
    D %= P

    # function call
    print(NearestElement(A, D, P))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to Find First
// element in AP which is
// multiple of given prime
using System;

class GFG
{
// Iterative Function to
// calculate (x^y)%p in
// O(log y) */
static int power(int x,
                 int y, int p)
{
    // Initialize result
    int res = 1;

    // Update x if it is
    // more than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to find nearest
// element in common
static int NearestElement(int A,
                          int D, int P)
{
    // base conditions
    if (A == 0)
        return 0;

    else if (D == 0)
        return -1;

    else
    {
        int X = power(D, P - 2, P);
        return (X * (P - A)) % P;
    }
}

// Driver code
public static void Main()
{
    int A = 4, D = 9, P = 11;

    // module both A and D
    A %= P;
    D %= P;

    // function call
    Console.WriteLine(NearestElement(A, D, P));
}
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative Function to calculate
// (x^y)%p in O(log y) */
function power($x, $y, $p)
{
    // Initialize result
    $res = 1;

    // Update x if it is more
    // than or equal to p
    $x = $x % $p;

    while ($y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) %$p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) %$p;
    }

    return $res;
}

// function to find nearest
// element in common
function NearestElement($A, $D, $P)
{
    // base conditions
    if ($A == 0)
        return 0;

    else if ($D == 0)
        return -1;

    else
    {
        $X = power($D, $P - 2, $P);
        return ($X * ($P - $A)) %$P;
    }
}

// Driver code
$A = 4; $D = 9; $P = 11;

// module both A and D
$A %= $P;
$D %= $P;

// function call
echo NearestElement($A, $D, $P);

// This code is contributed
// by chandan_jnu.
?>
```

## java 描述语言

```
<script>

// Javascript Program to Find First
// element in AP which is
// multiple of given prime

// Iterative Function to
// calculate (x^y)%p in
// O(log y) */
function power(x, y, p)
{
    // Initialize result
    let res = 1;

    // Update x if it is
    // more than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to find nearest
// element in common
function NearestElement(A, D, P)
{
    // base conditions
    if (A == 0)
        return 0;

    else if (D == 0)
        return -1;

    else
    {
        let X = power(D, P - 2, P);
        return (X * (P - A)) % P;
    }
}

// driver program

    let A = 4, D = 9, P = 11;

    // module both A and D
    A %= P;
    D %= P;

    // function call
    document.write(NearestElement(A, D, P));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(log y)

**辅助空间:** O(1)