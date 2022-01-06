# N 的乘法分区数

> 原文:[https://www . geesforgeks . org/n 的乘法分区计数/](https://www.geeksforgeeks.org/count-of-multiplicative-partitions-of-n/)

给定一个整数 **N** ，任务是求 N 的乘法分区总数。

> **乘法除法:**所有因子都大于 1 的整数的因式分解的次数。

**示例:**

> **输入:** N = 20
> **输出:** 4
> **说明:**
> 20 的乘法分区为:
> 2 × 2 × 5 = 2 × 10 = 4 × 5 = 20。
> **输入:** N = 30
> **输出:** 5
> **说明:**
> 30 的乘法分区为:
> 2 × 3 × 5 = 2 × 15 = 6 × 5 = 3 × 10 = 30

**逼近**:想法是对 N 的每一个[除数进行尝试，然后递归地打破被除数，得到乘法分区。以下是该方法步骤的图示:](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)

*   将最小因子初始化为 2。因为它是 1 以外的最小因子。
*   从 i =最小值到 N–1 开始循环，检查数字是否除以 N 和 N/i > i，然后将计数器增加 1，并再次调用相同的函数。因为我除以 N，所以这意味着 I 和 N/i 可以再分解几次。

**例如:**

> 如果 N = 30，让 i = min = 2
> 30 % 2 = 0，那么再次用(2，15)
> 15 % 3 = 0 重现，那么再次用(3，5)
> 重现。
> 。
> 等等。

以下是上述方法的实现:

## C++

```
// C++ implementation to find
// the multiplicative partitions of
// the given number N
#include <bits/stdc++.h>
using namespace std;

// Function to return number of ways
// of factoring N with all
// factors greater than 1
static int getDivisors(int min, int n)
{

    // Variable to store number of ways
    // of factoring n with all
    // factors greater than 1
    int total = 0;

    for(int i = min; i < n; ++i)
    {
        if (n % i == 0 && n / i >= i)
        {
            ++total;
            if (n / i > i)
                total += getDivisors(i, n / i);
        }
    }
    return total;
}

// Driver code
int main()
{
    int n = 30;

    // 2 is the minimum factor of
    // number other than 1.
    // So calling recursive
    // function to find
    // number of ways of factoring N
    // with all factors greater than 1
    cout << 1 + getDivisors(2, n);

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the multiplicative partitions of
// the given number N

class MultiPart {

    // Function to return number of ways
    // of factoring N with all
    // factors greater than 1
    static int getDivisors(int min, int n)
    {

        // Variable to store number of ways
        // of factoring n with all
        // factors greater than 1
        int total = 0;

        for (int i = min; i < n; ++i)

            if (n % i == 0 && n / i >= i) {
                ++total;
                if (n / i > i)
                    total
                        += getDivisors(
                            i, n / i);
            }

        return total;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 30;

        // 2 is the minimum factor of
        // number other than 1.
        // So calling recursive
        // function to find
        // number of ways of factoring N
        // with all factors greater than 1
        System.out.println(
            1 + getDivisors(2, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find
# the multiplicative partitions of
# the given number N

# Function to return number of ways
# of factoring N with all
# factors greater than 1
def getDivisors(min, n):

    # Variable to store number of ways
    # of factoring n with all
    # factors greater than 1
    total = 0

    for i in range(min, n):
        if (n % i == 0 and n // i >= i):
            total += 1
            if (n // i > i):
                total += getDivisors(i, n // i)

    return total

# Driver code
if __name__ == '__main__':

    n = 30

    # 2 is the minimum factor of
    # number other than 1.
    # So calling recursive
    # function to find
    # number of ways of factoring N
    # with all factors greater than 1
    print(1 + getDivisors(2, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find
// the multiplicative partitions of
// the given number N
using System;

class GFG{

// Function to return number of ways
// of factoring N with all
// factors greater than 1
static int getDivisors(int min, int n)
{

    // Variable to store number of ways
    // of factoring n with all
    // factors greater than 1
    int total = 0;

    for(int i = min; i < n; ++i)
        if (n % i == 0 && n / i >= i)
        {
            ++total;
            if (n / i > i)
                total+= getDivisors(i, n / i);
        }

    return total;
}

// Driver code
public static void Main()
{
    int n = 30;

    // 2 is the minimum factor of
    // number other than 1.
    // So calling recursive
    // function to find
    // number of ways of factoring N
    // with all factors greater than 1
    Console.Write(1 + getDivisors(2, n));
}
}

// This code is contributed by adityakumar27200
```

## java 描述语言

```
<script>

// Javascript implementation to find
// the multiplicative partitions of
// the given number N

// Function to return number of ways
// of factoring N with all
// factors greater than 1
function getDivisors(min, n)
{

    // Variable to store number of ways
    // of factoring n with all
    // factors greater than 1
    var total = 0;

    for(var i = min; i < n; ++i)
    {
        if (n % i == 0 && n / i >= i)
        {
            ++total;
            if (n / i > i)
                total += getDivisors(i, n / i);
        }
    }
    return total;
}

// Driver code
var n = 30;

// 2 is the minimum factor of
// number other than 1.
// So calling recursive
// function to find
// number of ways of factoring N
// with all factors greater than 1
document.write( 1 + getDivisors(2, n));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*