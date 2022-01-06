# 用{2，3，7}使两个数相等的最小乘法

> 原文:[https://www . geesforgeks . org/minimum-乘-2-3-7 使两个数相等/](https://www.geeksforgeeks.org/minimum-multiplications-with-2-3-7-to-make-two-numbers-equal/)

给定两个数字 **A** 和 **B** ，任务是找到使 **A** 和 **B** 相等所需的最小操作数。在每次操作中，任何数字都可以除以 **2** 、 **3** 或 **7** 。如果不可能，则打印 **-1** 。

**示例:**

> **输入:** A = 14，B = 28
> T3】输出: 1
> 运算 1: A * 2 = 14 * 2 = 28 等于 B
> 
> **输入:** A = 3，B = 5
> **输出:** -1
> 无论操作多少次，A 和 B 永远不会相等。

**进场:**T2 A 和 **B** 可写成**A = x * 2<sup>a1</sup>* 3<sup>a2</sup>* 7<sup>a3</sup>T13】和**B = y * 2<sup>B1</sup>* 3<sup>B2</sup>* 7<sup>B3</sup>T21】其中 **x** 和 **y 现在，******

*   如果 **x！= y** 则 **A** 和 **B** 不能与给定的操作相等。
*   如果 **x = y** ，那么所需的最小运算量将是**| a1–B1 |+| a2–B2 |+| a3–B3 |**，因为这两个数字需要具有相等的 **2** 、 **3** 和 **7** 的幂。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find powers of 2, 3 and 7 in x
vector<int> Divisors(int x)
{
    // To keep count of each divisor
    int c = 0;

    // To store the result
    vector<int> v;

    // Count powers of 2 in x
    while (x % 2 == 0) {
        c++;
        x /= 2;
    }
    v.push_back(c);

    c = 0;

    // Count powers of 3 in x
    while (x % 3 == 0) {
        c++;
        x /= 3;
    }
    v.push_back(c);

    c = 0;

    // Count powers of 7 in x
    while (x % 7 == 0) {
        c++;
        x /= 7;
    }
    v.push_back(c);

    // Remaining number which is not
    // divisible by 2, 3 or 7
    v.push_back(x);

    return v;
}

// Function to return the minimum number of
// given operations required to make a and b equal
int MinOperations(int a, int b)
{
    // a = x * 2^a1 * 3^a2 * 7^a3
    // va[0] = a1
    // va[1] = a2
    // va[2] = a3
    // va[3] = x
    vector<int> va = Divisors(a);

    // Similarly for b
    vector<int> vb = Divisors(b);

    // If a and b cannot be made equal
    // with the given operation. Note
    // that va[3] and vb[3] contain
    // remaining numbers after repeated
    // divisions with 2, 3 and 7.
    // If remaining numbers are not same
    // then we cannot make them equal.
    if (va[3] != vb[3])
        return -1;

    // Minimum number of operations required
    int minOperations = abs(va[0] - vb[0])
                        + abs(va[1] - vb[1])
                        + abs(va[2] - vb[2]);

    return minOperations;
}

// Driver code
int main()
{
    int a = 14, b = 28;
    cout << MinOperations(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.Vector;

class GFG
{

    // Function to find powers of 2, 3 and 7 in x
    static Vector<Integer> Divisors(int x)
    {
        // To keep count of each divisor
        int c = 0;

        // To store the result
        Vector<Integer> v = new Vector<Integer>();

        // Count powers of 2 in x
        while (x % 2 == 0)
        {
            c++;
            x /= 2;
        }
        v.add(c);

        c = 0;

        // Count powers of 3 in x
        while (x % 3 == 0)
        {
            c++;
            x /= 3;
        }
        v.add(c);

        c = 0;

        // Count powers of 7 in x
        while (x % 7 == 0)
        {
            c++;
            x /= 7;
        }
        v.add(c);

        // Remaining number which is not
        // divisible by 2, 3 or 7
        v.add(x);

        return v;
    }

    // Function to return the minimum number of
    // given operations required to make a and b equal
    static int MinOperations(int a, int b)
    {
        // a = x * 2^a1 * 3^a2 * 7^a3
        // va[0] = a1
        // va[1] = a2
        // va[2] = a3
        // va[3] = x
        Vector<Integer> va = Divisors(a);

        // Similarly for b
        Vector<Integer> vb = Divisors(b);

        // If a and b cannot be made equal
        // with the given operation. Note
        // that va[3] and vb[3] contain
        // remaining numbers after repeated
        // divisions with 2, 3 and 7.
        // If remaining numbers are not same
        // then we cannot make them equal.
        if (va.get(3) != vb.get(3))
        {
            return -1;
        }

        // Minimum number of operations required
        int minOperations = Math.abs(va.get(0) - vb.get(0))
                + Math.abs(va.get(1) - vb.get(1))
                + Math.abs(va.get(2) - vb.get(2));

        return minOperations;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 14, b = 28;
        System.out.println(MinOperations(a, b));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# python 3 implementation of the approach

# Function to find powers of 2, 3 and 7 in x
def Divisors(x):
    # To keep count of each divisor
    c = 0

    # To store the result
    v = []

    # Count powers of 2 in x
    while (x % 2 == 0):
        c += 1
        x /= 2

    v.append(c)

    c = 0

    # Count powers of 3 in x
    while (x % 3 == 0):
        c += 1
        x /= 3

    v.append(c)

    c = 0

    # Count powers of 7 in x
    while (x % 7 == 0):
        c += 1
        x /= 7

    v.append(c)

    # Remaining number which is not
    # divisible by 2, 3 or 7
    v.append(x)

    return v

# Function to return the minimum number of
# given operations required to make a and b equal
def MinOperations(a, b):
    # a = x * 2^a1 * 3^a2 * 7^a3
    # va[0] = a1
    # va[1] = a2
    # va[2] = a3
    # va[3] = x
    va = Divisors(a)

    # Similarly for b
    vb = Divisors(b)

    # If a and b cannot be made equal
    # with the given operation. Note
    # that va[3] and vb[3] contain
    # remaining numbers after repeated
    # divisions with 2, 3 and 7.
    # If remaining numbers are not same
    # then we cannot make them equal.
    if (va[3] != vb[3]):
        return -1

    # Minimum number of operations required
    minOperations = abs(va[0] - vb[0]) + abs(va[1] - vb[1]) + abs(va[2] - vb[2])

    return minOperations

# Driver code
if __name__ == '__main__':
    a = 14
    b = 28
    print(MinOperations(a, b))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find powers
    // of 2, 3 and 7 in x
    static List<int> Divisors(int x)
    {
        // To keep count of each divisor
        int c = 0;

        // To store the result
        List<int> v = new List<int>();

        // Count powers of 2 in x
        while (x % 2 == 0)
        {
            c++;
            x /= 2;
        }
        v.Add(c);

        c = 0;

        // Count powers of 3 in x
        while (x % 3 == 0)
        {
            c++;
            x /= 3;
        }
        v.Add(c);

        c = 0;

        // Count powers of 7 in x
        while (x % 7 == 0)
        {
            c++;
            x /= 7;
        }
        v.Add(c);

        // Remaining number which is not
        // divisible by 2, 3 or 7
        v.Add(x);

        return v;
    }

    // Function to return the minimum
    // number of given operations required
    // to make a and b equal
    static int MinOperations(int a, int b)
    {
        // a = x * 2^a1 * 3^a2 * 7^a3
        // va[0] = a1
        // va[1] = a2
        // va[2] = a3
        // va[3] = x
        List<int> va = Divisors(a);

        // Similarly for b
        List<int> vb = Divisors(b);

        // If a and b cannot be made equal
        // with the given operation. Note
        // that va[3] and vb[3] contain
        // remaining numbers after repeated
        // divisions with 2, 3 and 7.
        // If remaining numbers are not same
        // then we cannot make them equal.
        if (va[3] != vb[3])
        {
            return -1;
        }

        // Minimum number of operations required
        int minOperations = Math.Abs(va[0] - vb[0]) +
                            Math.Abs(va[1] - vb[1]) +
                            Math.Abs(va[2] - vb[2]);

        return minOperations;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int a = 14, b = 28;
        Console.WriteLine(MinOperations(a, b));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find powers of 2, 3 and 7 in x
function Divisors($x)
{
    // To keep count of each divisor
    $c = 0;

    // To store the result
    $v = array();

    // Count powers of 2 in x
    while ($x % 2 == 0)
    {
        $c++;
        $x = floor($x / 2);
    }
    array_push($v, $c);

    $c = 0;

    // Count powers of 3 in x
    while ($x % 3 == 0)
    {
        $c++;
        $x = floor($x / 3);
    }
    array_push($v, $c) ;

    $c = 0;

    // Count powers of 7 in x
    while ($x % 7 == 0)
    {
        $c++;
        $x = floor($x / 7);
    }
    array_push($v, $c);

    // Remaining number which is not
    // divisible by 2, 3 or 7
    array_push($v, $x);

    return $v;
}

// Function to return the minimum number
// of given operations required to make
// a and b equal
function MinOperations($a, $b)
{

    // a = x * 2^a1 * 3^a2 * 7^a3
    // va[0] = a1
    // va[1] = a2
    // va[2] = a3
    // va[3] = x
    $va = Divisors($a);

    // Similarly for b
    $vb = Divisors($b);

    // If a and b cannot be made equal
    // with the given operation. Note
    // that va[3] and vb[3] contain
    // remaining numbers after repeated
    // divisions with 2, 3 and 7.
    // If remaining numbers are not same
    // then we cannot make them equal.
    if ($va[3] != $vb[3])
        return -1;

    // Minimum number of operations required
    $minOperations = abs($va[0] - $vb[0]) +
                     abs($va[1] - $vb[1]) +
                     abs($va[2] - $vb[2]);

    return $minOperations;
}

// Driver code
$a = 14 ;
$b = 28 ;
echo MinOperations($a, $b);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of above approach

    // Function to find powers of 2, 3 and 7 in x
    function Divisors(x)
    {

        // To keep count of each divisor
        var c = 0;

        // To store the result
        var v = [];

        // Count powers of 2 in x
        while (x % 2 == 0) {
            c++;
            x /= 2;
        }
        v.push(c);

        c = 0;

        // Count powers of 3 in x
        while (x % 3 == 0) {
            c++;
            x /= 3;
        }
        v.push(c);

        c = 0;

        // Count powers of 7 in x
        while (x % 7 == 0) {
            c++;
            x /= 7;
        }
        v.push(c);

        // Remaining number which is not
        // divisible by 2, 3 or 7
        v.push(x);

        return v;
    }

    // Function to return the minimum number of
    // given operations required to make a and b equal
    function MinOperations(a , b) {
        // a = x * 2^a1 * 3^a2 * 7^a3
        // va[0] = a1
        // va[1] = a2
        // va[2] = a3
        // va[3] = x
        var va = Divisors(a);

        // Similarly for b
        var vb = Divisors(b);

        // If a and b cannot be made equal
        // with the given operation. Note
        // that va[3] and vb[3] contain
        // remaining numbers after repeated
        // divisions with 2, 3 and 7.
        // If remaining numbers are not same
        // then we cannot make them equal.
        if (va[3] != vb[3]) {
            return -1;
        }

        // Minimum number of operations required
        var minOperations = Math.abs(va[0] - vb[0]) + Math.abs(va[1] - vb[1])
                + Math.abs(va[2] - vb[2]);

        return minOperations;
    }

    // Driver code
        var a = 14, b = 28;
        document.write(MinOperations(a, b));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
1
```