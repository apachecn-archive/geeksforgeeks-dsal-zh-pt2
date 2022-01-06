# 求两个给定整数之和的 N 次方与其差

之间的 GCD

> 原文:[https://www . geesforgeks . org/find-gcd-两个给定整数之和-n 的幂及其差/](https://www.geeksforgeeks.org/find-gcd-between-the-sum-of-two-given-integers-raised-to-the-power-of-n-and-their-difference/)

给定三个正整数， **P** 、 **Q** 和 **N** ，任务是在[模 **10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 下找到**(P<sup>N</sup>+Q<sup>N</sup>)**和**(P–Q)**。

**示例:**

> **输入:** p = 10，q = 6，n = 5
> **输出:** 4
> **解释:**p<sup>n</sup>+q<sup>n</sup>= 10<sup>5</sup>+6<sup>5</sup>= 107776，p–q = 4。107776 和 4 的 GCD 是 4。
> 
> **输入:**p =**T3】7，q = 2，n = 5
> T5】输出:**1
> T8】说明:p<sup>n</sup>+q<sup>n</sup>= 7<sup>5</sup>+2<sup>5</sup>=16839，p–q = 5。16839 和 5 的 GCD 为 1。

**方法:**由于数字 **(p <sup>n</sup> + q <sup>n</sup> )** 可以非常大，这样巨大的数字不能存储在任何数据类型中，因此 [GCD](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 不能使用[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)计算。所以可以用[模运算](https://www.geeksforgeeks.org/modular-arithmetic/)来寻找答案。

请按照以下步骤解决此问题:

*   求一个大数和一个小数的 [GCD](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) ，在 **O(√p-q)** 中求较小数的除数。
*   这些数字是潜在的 GCD 候选人。
*   现在，检查这些潜在的 [GCDs](https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/) 中是否有任何一个除以较大的数字。两个数相除的最大数就是最终答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Function to find the value of (a ^ n) % d
long long int power(long long a, long long n,
                    long long int d)
{

    // Stores the value
    // of (a ^ n) % d
    long long int res = 1;

    // Calculate the value
    // of (a ^ n) % d
    while (n) {

        // If n is odd
        if (n % 2) {

            // Update res
            res = ((res % d) * (a % d)) % d;
        }

        // Update a
        a = ((a % d) * (a % d)) % d;

        // Update n
        n /= 2;
    }

    return res;
}

// Function to find the GCD of (p ^ n + q ^ n)
// and p - q mod d
long long int gcd(long long p, long long q,
                  long long n)
{

    // If p and q are equal
    if (p == q) {
        return (power(p, n, mod)
                + power(q, n, mod))
               % mod;
    }

    // Stores GCD of (p ^ n + q ^ n)
    // and (p - q) mod d
    long long int candidate = 1;

    // Stores the value of (p-q)
    long long int num = p - q;

    // Stores square root of num
    long long int sq = sqrt(num);

    // Find the divisors of num.
    for (long long i = 1; i <= sq; ++i) {

        // If i divides num
        if (num % i == 0) {

            // Stores power of (p ^ n) mod i
            long long int X = power(p, n, i);

            // Stores power of (q ^ n) mod i
            long long int Y = power(q, n, i);

            // Stores power of (p ^ n + q ^ n) mod i
            long long int temp = (X + Y) % i;

            // If (p^n + q^n) is divisible by i
            if (temp == 0) {

                // Calculate the largest divisor.
                candidate = max(candidate, i);
            }

            // If i divides num, (num/i) also divides
            // num. Hence, calculate temp.
            temp = (power(p, n, num / i)
                    + power(q, n, num / i))
                   % (num / i);

            // If (p^n + q^n) is divisible
            // by (num/i)
            if (temp == 0) {

                // Calculate the largest divisor.
                candidate = max(candidate, num / i);
            }
        }
    }

    return candidate % mod;
}

// Driver Code
int main()
{

    // Given p, q and n
    long long int p, q, n;
    p = 10;
    q = 6;
    n = 5;

    // Function Call
    cout << gcd(p, q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{
static int mod = 1000000007;

// Function to find the value of (a ^ n) % d
static int power(int a, int n, int d)
{

    // Stores the value
    // of (a ^ n) % d
    int res = 1;

    // Calculate the value
    // of (a ^ n) % d
    while (n != 0) {

        // If n is odd
        if ((n % 2) !=0) {

            // Update res
            res = ((res % d) * (a % d)) % d;
        }

        // Update a
        a = ((a % d) * (a % d)) % d;

        // Update n
        n /= 2;
    }

    return res;
}

// Function to find the GCD of (p ^ n + q ^ n)
// and p - q mod d
static int gcd(int p, int q, int n)
{

    // If p and q are equal
    if (p == q) {
        return (power(p, n, mod)
                + power(q, n, mod))
               % mod;
    }

    // Stores GCD of (p ^ n + q ^ n)
    // and (p - q) mod d
    int candidate = 1;

    // Stores the value of (p-q)
    int num = p - q;

    // Stores square root of num
    int sq = (int)Math.sqrt(num);

    // Find the divisors of num.
    for (int  i = 1; i <= sq; ++i) {

        // If i divides num
        if (num % i == 0) {

            // Stores power of (p ^ n) mod i
            int X = power(p, n, i);

            // Stores power of (q ^ n) mod i
            int Y = power(q, n, i);

            // Stores power of (p ^ n + q ^ n) mod i
            int temp = (X + Y) % i;

            // If (p^n + q^n) is divisible by i
            if (temp == 0) {

                // Calculate the largest divisor.
                candidate = Math.max(candidate, i);
            }

            // If i divides num, (num/i) also divides
            // num. Hence, calculate temp.
            temp = (power(p, n, num / i)
                    + power(q, n, num / i))
                   % (num / i);

            // If (p^n + q^n) is divisible
            // by (num/i)
            if (temp == 0) {

                // Calculate the largest divisor.
                candidate = Math.max(candidate, num / i);
            }
        }
    }
    return candidate % mod;
}

// Driver code
public static void main(String[] args)
{
    // Given p, q and n
    int p, q, n;
    p = 10;
    q = 6;
    n = 5;

    // Function Call
    System.out.println(gcd(p, q, n));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program for the above approach
import math
mod = 1000000007;

# Function to find the value of (a ^ n) % d
def power(a, n, d):

    # Stores the value
    # of (a ^ n) % d
    res = 1;

    # Calculate the value
    # of (a ^ n) % d
    while (n != 0):

        # If n is odd
        if ((n % 2) != 0):

            # Update res
            res = ((res % d) * (a % d)) % d;

        # Update a
        a = ((a % d) * (a % d)) % d;

        # Update n
        n /= 2;
    return res;

# Function to find the GCD of (p ^ n + q ^ n)
# and p - q mod d
def gcd(p, q, n):

    # If p and q are equal
    if (p == q):
        return (power(p, n, mod) + power(q, n, mod)) % mod;

    # Stores GCD of (p ^ n + q ^ n)
    # and (p - q) mod d
    candidate = 1;

    # Stores the value of (p-q)
    num = p - q;

    # Stores square root of num
    sq = (int)(math.sqrt(num));

    # Find the divisors of num.
    for i in range(1, sq):

        # If i divides num
        if (num % i == 0):

            # Stores power of (p ^ n) mod i
            X = power(p, n, i);

            # Stores power of (q ^ n) mod i
            Y = power(q, n, i);

            # Stores power of (p ^ n + q ^ n) mod i
            temp = (X + Y) % i;

            # If (p^n + q^n) is divisible by i
            if (temp == 0):

                # Calculate the largest divisor.
                candidate = max(candidate, i);

            # If i divides num, (num/i) also divides
            # num. Hence, calculate temp.
            temp = (power(p, n, num / i) + power(q, n, num / i)) % (num / i);

            # If (p^n + q^n) is divisible
            # by (num/i)
            if (temp == 0):

                # Calculate the largest divisor.
                candidate = max(candidate, num / i);           
    return candidate % mod;

# Driver code
if __name__ == '__main__':

  # Given p, q and n
    p = 10;
    q = 6;
    n = 5;

    # Function Call
    print((int)(gcd(p, q, n)));

# This code contributed by aashish1995
```

## C#

```
// C# program for the above approach
using System;

class GFG
{
    static int mod = 1000000007;

    // Function to find the value of (a ^ n) % d
    static int power(int a, int n, int d)
    {

        // Stores the value
        // of (a ^ n) % d
        int res = 1;

        // Calculate the value
        // of (a ^ n) % d
        while (n != 0)
        {

            // If n is odd
            if ((n % 2) != 0)
            {

                // Update res
                res = ((res % d) * (a % d)) % d;
            }

            // Update a
            a = ((a % d) * (a % d)) % d;

            // Update n
            n /= 2;
        }

        return res;
    }

    // Function to find the GCD of (p ^ n + q ^ n)
    // and p - q mod d
    static int gcd(int p, int q, int n)
    {

        // If p and q are equal
        if (p == q)
        {
            return (power(p, n, mod) + power(q, n, mod))
                % mod;
        }

        // Stores GCD of (p ^ n + q ^ n)
        // and (p - q) mod d
        int candidate = 1;

        // Stores the value of (p-q)
        int num = p - q;

        // Stores square root of num
        int sq = (int)Math.Sqrt(num);

        // Find the divisors of num.
        for (int i = 1; i <= sq; ++i) {

            // If i divides num
            if (num % i == 0) {

                // Stores power of (p ^ n) mod i
                int X = power(p, n, i);

                // Stores power of (q ^ n) mod i
                int Y = power(q, n, i);

                // Stores power of (p ^ n + q ^ n) mod i
                int temp = (X + Y) % i;

                // If (p^n + q^n) is divisible by i
                if (temp == 0) {

                    // Calculate the largest divisor.
                    candidate = Math.Max(candidate, i);
                }

                // If i divides num, (num/i) also divides
                // num. Hence, calculate temp.
                temp = (power(p, n, num / i)
                        + power(q, n, num / i))
                       % (num / i);

                // If (p^n + q^n) is divisible
                // by (num/i)
                if (temp == 0) {

                    // Calculate the largest divisor.
                    candidate
                        = Math.Max(candidate, num / i);
                }
            }
        }
        return candidate % mod;
    }

    // Driver code
    static public void Main()
    {

        // Given p, q and n
        int p, q, n;
        p = 10;
        q = 6;
        n = 5;

        // Function Call
        Console.WriteLine(gcd(p, q, n));
    }
}

// This is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// javascript program for the above approach
    const mod = 1000000007;

    // Function to find the value of (a ^ n) % d
    function power(a , n , d) {

        // Stores the value
        // of (a ^ n) % d
        var res = 1;

        // Calculate the value
        // of (a ^ n) % d
        while (n != 0) {

            // If n is odd
            if ((n % 2) != 0) {

                // Update res
                res = ((res % d) * (a % d)) % d;
            }

            // Update a
            a = ((a % d) * (a % d)) % d;

            // Update n
            n /= 2;
        }

        return res;
    }

    // Function to find the GCD of (p ^ n + q ^ n)
    // and p - q mod d
    function gcd(p , q , n)
    {

        // If p and q are equal
        if (p == q)
        {
            return (power(p, n, mod) + power(q, n, mod)) % mod;
        }

        // Stores GCD of (p ^ n + q ^ n)
        // and (p - q) mod d
        var candidate = 1;

        // Stores the value of (p-q)
        var num = p - q;

        // Stores square root of num
        var sq = parseInt( Math.sqrt(num));

        // Find the divisors of num.
        for (i = 1; i <= sq; ++i) {

            // If i divides num
            if (num % i == 0) {

                // Stores power of (p ^ n) mod i
                var X = power(p, n, i);

                // Stores power of (q ^ n) mod i
                var Y = power(q, n, i);

                // Stores power of (p ^ n + q ^ n) mod i
                var temp = (X + Y) % i;

                // If (p^n + q^n) is divisible by i
                if (temp == 0) {

                    // Calculate the largest divisor.
                    candidate = Math.max(candidate, i);
                }

                // If i divides num, (num/i) also divides
                // num. Hence, calculate temp.
                temp = (power(p, n, num / i) + power(q, n, num / i)) % (num / i);

                // If (p^n + q^n) is divisible
                // by (num/i)
                if (temp == 0) {

                    // Calculate the largest divisor.
                    candidate = Math.max(candidate, num / i);
                }
            }
        }
        return candidate % mod;
    }

    // Driver code

        // Given p, q and n
        var p, q, n;
        p = 10;
        q = 6;
        n = 5;

        // Function Call
        document.write(gcd(p, q, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(sqrt(p–q))*
***辅助空间:** O(1)*