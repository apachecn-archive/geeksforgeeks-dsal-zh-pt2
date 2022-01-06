# 对两个给定数字中的一个进行最小数量的递增/递减，以使它们成为非互质

> 原文:[https://www . geesforgeks . org/要求在两个给定数字中的一个上执行的最小增量-减量数-使它们成为非互质/](https://www.geeksforgeeks.org/minimum-number-of-increment-decrements-required-to-be-performed-on-one-of-the-two-given-numbers-to-make-them-non-coprime/)

给定两个正整数 **A** 和 **B** ，任务是找到需要在 **A** 或 **B** 上执行的最小增量/减量数，以使两个数**不互质**。

**示例:**

> **输入:** A = 12，B = 3
> **输出:** 0
> **说明:**
> 由于 12 & 3 已经是非共形，所以所需的增量/减量操作的最小计数为 0。
> 
> **输入:** A = 7，B = 17
> T3】输出: 2

**方法:**给定的问题可以基于以下观察来解决:

*   如果 **A** 和 **B** 的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)大于 **1** ，则不执行增量或减量，因为数字已经是非互质的。
*   现在，检查 **A** 和 **B** 两个方向的 **1** 的差异。因此，只需要一步就可以将任何数字转换成偶数。
*   如果以上两种情况都不适用，则需要 **2** 的递增/递减操作来使数字 **A** 和 **B** 成为它们最接近的偶数，从而使[数字成为非同素数](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。

根据以上观察，按照以下步骤解决问题:

*   如果**A****B**的 GCD 不等于 **1** ，则打印 **0** ，因为不需要操作。
*   否则，如果其中一对{ **{A + 1，B}** 、**{ A–1，B}** 、 **{A，B + 1}** 、 **{A，B–1 }**}的 GCD 不等于 **1** ，则打印 **1** ，因为只需要一个操作。
*   否则，打印 **2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// increments/decrements operations required
// to make both the numbers non-coprime
int makeCoprime(int a, int b)
{
    // If a & b are already non-coprimes
    if (__gcd(a, b) != 1)
        return 0;

    // If a & b can become non-coprimes
    // by only incrementing/decrementing
    // a number only once
    if (__gcd(a - 1, b) != 1
        or __gcd(a + 1, b) != 1
        or __gcd(b - 1, a) != 1
        or __gcd(b + 1, a) != 1)
        return 1;

    // Otherwise
    return 2;
}

// Driver Code
int main()
{
    int A = 7, B = 17;
    cout << makeCoprime(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

  // function to calculate gcd
  static int __gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return __gcd(a-b, b);
    return __gcd(a, b-a);
  }

  // Function to find the minimum number of
  // increments/decrements operations required
  // to make both the numbers non-coprime
  static int makeCoprime(int a, int b)
  {

    // If a & b are already non-coprimes
    if (__gcd(a, b) != 1)
      return 0;

    // If a & b can become non-coprimes
    // by only incrementing/decrementing
    // a number only once
    if (__gcd(a - 1, b) != 1 || __gcd(a + 1, b) != 1
        || __gcd(b - 1, a) != 1
        || __gcd(b + 1, a) != 1)
      return 1;

    // Otherwise
    return 2;
  }

  // Driver code
  public static void main(String args[])
  {
    int A = 7, B = 17;
    System.out.println(makeCoprime(A, B));
  }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import gcd

# Function to find the minimum number of
# increments/decrements operations required
# to make both the numbers non-coprime
def makeCoprime(a, b):

    # If a & b are already non-coprimes
    if (gcd(a, b) != 1):
        return 0

    # If a & b can become non-coprimes
    # by only incrementing/decrementing
    # a number only once
    if (gcd(a - 1, b) != 1 or
        gcd(a + 1, b) != 1 or
        gcd(b - 1, a) != 1 or
        gcd(b + 1, a) != 1):
        return 1

    # Otherwise
    return 2

# Driver Code
if __name__ == '__main__':

    A = 7
    B = 17

    print(makeCoprime(A, B))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate gcd
static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Function to find the minimum number of
// increments/decrements operations required
// to make both the numbers non-coprime
static int makeCoprime(int a, int b)
{

    // If a & b are already non-coprimes
    if (__gcd(a, b) != 1)
        return 0;

    // If a & b can become non-coprimes
    // by only incrementing/decrementing
    // a number only once
    if (__gcd(a - 1, b) != 1 ||
        __gcd(a + 1, b) != 1 ||
        __gcd(b - 1, a) != 1 ||
        __gcd(b + 1, a) != 1)
        return 1;

    // Otherwise
    return 2;
}

// Driver Code
public static void Main(String[] args)
{
    int A = 7, B = 17;

    Console.Write(makeCoprime(A, B));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        function __gcd(a, b) {
            if (b == 0)
                return a;
            return __gcd(b, a % b);

        }

        // Function to find the minimum number of
        // increments/decrements operations required
        // to make both the numbers non-coprime
        function makeCoprime(a, b) {
            // If a & b are already non-coprimes
            if (__gcd(a, b) != 1)
                return 0;

            // If a & b can become non-coprimes
            // by only incrementing/decrementing
            // a number only once
            if (__gcd(a - 1, b) != 1
                || __gcd(a + 1, b) != 1
                || __gcd(b - 1, a) != 1
                || __gcd(b + 1, a) != 1)
                return 1;

            // Otherwise
            return 2;
        }

        // Driver Code

        let A = 7, B = 17;
        document.write(makeCoprime(A, B));

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log(A，B))*
***辅助空间:** O(1)*