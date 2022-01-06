# 要相加的最小元素，以便两个矩阵可以相乘

> 原文:[https://www . geeksforgeeks . org/待添加元素最少以便两个矩阵可以相乘/](https://www.geeksforgeeks.org/minimum-elements-to-be-added-so-that-two-matrices-can-be-multiplied/)

给定 p×q(或 q×p)和 r×s(或 s×r)阶的两个矩阵 A 和 B。任务是找到要添加到两个矩阵中任何一个矩阵的最小元素数，使它们相乘。
如果一个矩阵的列数等于另一个矩阵的行数，则两个矩阵是乘法的。
**例:**

> **输入:** p = 2，q = 3，r = 5，s = 6
> **输出:** 4
> 可加两列使 q = 5。
> 增加两列，元素个数会增加 2 *行数即 2 * 2 = 4
> **输入:** p = 11，q = 5，r = 10，s = 11
> **输出:** 0

**进场:**

*   如果一个矩阵中的列数等于另一个矩阵中的行数，则不需要添加额外的元素。
*   如果它们不相等，我们必须在一个矩阵中增加一些额外的列，或者在另一个矩阵中增加一些额外的行。

因此，计算两个条件中的额外元素的数量，并打印最小的一个。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of extra elements is to add
int minExtraElements(int p, int q, int r, int s)
{
    // num1 will store minimum number of
    // extra elements required
    // to make A x B possible

    // num2 will store minimum number of
    // extra elements required
    // to make B x A possible
    int num1, num2;

    // if either A x B or B x A is possible,
    // it will return 0
    if (q == r || p == s)
        return 0;

    else {
        // it will calculate minimum number of
        // extra elements required
        // to make A x B possible
        if (q < r)
            num1 = (r - q) * p;
        else
            num1 = (q - r) * s;

        // it will calculate minimum number of
        // extra elements required
        // to make B x A possible
        if (p < s)
            num2 = (s - p) * r;
        else
            num2 = (p - s) * q;
    }

    // return minimum of both
    return min(num1, num2);
}

// Driver code
int main()
{

    int p = 2, q = 3, r = 5, s = 6;
    cout << minExtraElements(p, q, r, s) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    // Function to calculate the minimum
    // number of extra elements is to add
    static int minExtraElements(int p, int q, int r, int s)
    {
        // num1 will store minimum number of
        // extra elements required
        // to make A x B possible

        // num2 will store minimum number of
        // extra elements required
        // to make B x A possible
        int num1, num2;

        // if either A x B or B x A is possible,
        // it will return 0
        if (q == r || p == s)
            return 0;

        else {
            // it will calculate minimum number of
            // extra elements required
            // to make A x B possible
            if (q < r)
                num1 = (r - q) * p;
            else
                num1 = (q - r) * s;

            // it will calculate minimum number of
            // extra elements required
            // to make B x A possible
            if (p < s)
                num2 = (s - p) * r;
            else
                num2 = (p - s) * q;
        }

        // return minimum of both
        return Math.min(num1, num2);
    }

    // Driver code
    public static void main(String []rags)
    {

        int p = 2, q = 3, r = 5, s = 6;
        System.out.println(minExtraElements(p, q, r, s));

    }
}

// This code is contributed by ihritik
```

## 计算机编程语言

```
# Python implementation of the above approach

# Function to calculate the minimum
# number of extra elements is to add
def minExtraElements(p,  q, r, s):

    # num1 will store minimum number of
    # extra elements required
    # to make A x B possible

    # num2 will store minimum number of
    # extra elements required
    # to make B x A possible

    # if either A x B or B x A is possible,
    # it will return 0
    if (q == r or p == s):
        return 0

    else :
        # it will calculate minimum number of
        # extra elements required
        # to make A x B possible
        if (q < r):
            num1 = (r - q) * p
        else:
            num1 = (q - r) * s

        # it will calculate minimum number of
        # extra elements required
        # to make B x A possible
        if (p < s):
            num2 = (s - p) * r
        else:
            num2 = (p - s) * q

    # return minimum of both
    return min(num1, num2)

# Driver code

p = 2
q = 3
r = 5
s = 6
print(minExtraElements(p, q, r, s))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{
    // Function to calculate the minimum
    // number of extra elements is to add
    static int minExtraElements(int p, int q, int r, int s)
    {
        // num1 will store minimum number of
        // extra elements required
        // to make A x B possible

        // num2 will store minimum number of
        // extra elements required
        // to make B x A possible
        int num1, num2;

        // if either A x B or B x A is possible,
        // it will return 0
        if (q == r || p == s)
            return 0;

        else {
            // it will calculate minimum number of
            // extra elements required
            // to make A x B possible
            if (q < r)
                num1 = (r - q) * p;
            else
                num1 = (q - r) * s;

            // it will calculate minimum number of
            // extra elements required
            // to make B x A possible
            if (p < s)
                num2 = (s - p) * r;
            else
                num2 = (p - s) * q;
        }

        // return minimum of both
        return Math.Min(num1, num2);
    }

    // Driver code
    public static void Main()
    {

        int p = 2, q = 3, r = 5, s = 6;
        Console.WriteLine(minExtraElements(p, q, r, s));

    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Python3 implementation of the above approach

// Function to calculate the minimum
// number of extra elements is to add
function minExtraElements($p, $q, $r, $s)
{
    // num1 will store minimum number of
    // extra elements required to make
    // A x B possible

    // num2 will store minimum number of
    // extra elements required to make
    // B x A possible

    // if either A x B or B x A is possible,
    // it will return 0
    if ($q == $r || $p == $s)
        return 0;

    else
    {
        // it will calculate minimum number
        // of extra elements required to
        // make A x B possible
        if ($q < $r)
            $num1 = ($r - $q) * $p;
        else
            $num1 = ($q - $r) * $s;

        // it will calculate minimum number
        // of extra elements required to
        // make B x A possible
        if ($p < $s)
            $num2 = ($s - $p) * $r;
        else
            $num2 = ($p - $s) * $q;
    }

    // return minimum of both
    return min($num1, $num2);
}

// Driver code
$p = 2; $q = 3; $r = 5; $s = 6;
echo minExtraElements($p, $q, $r, $s);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to calculate the minimum
// number of extra elements is to add
function minExtraElements( p, q, r, s)
{
    // num1 will store minimum number of
    // extra elements required
    // to make A x B possible

    // num2 will store minimum number of
    // extra elements required
    // to make B x A possible
    let num1, num2;

    // if either A x B or B x A is possible,
    // it will return 0
    if (q == r || p == s)
        return 0;

    else {
        // it will calculate minimum number of
        // extra elements required
        // to make A x B possible
        if (q < r)
            num1 = (r - q) * p;
        else
            num1 = (q - r) * s;

        // it will calculate minimum number of
        // extra elements required
        // to make B x A possible
        if (p < s)
            num2 = (s - p) * r;
        else
            num2 = (p - s) * q;
    }

    // return minimum of both
    return Math.min(num1, num2);
}

    // Driver Code

    let p = 2, q = 3, r = 5, s = 6;
    document.write(minExtraElements(p, q, r, s) + "</br>");

</script>
```

**Output:** 

```
4
```