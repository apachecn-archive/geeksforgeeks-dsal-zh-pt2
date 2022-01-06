# 可以从 K 开始形成的 N 大小数组的计数，这样每个元素都可以被下一个

整除

> 原文:[https://www . geesforgeks . org/count-of-n-size-数组-可以以-k 开头-这样-每个元素都可以被-next/](https://www.geeksforgeeks.org/count-of-n-size-arrays-that-can-be-formed-starting-with-k-such-that-every-element-is-divisible-by-next/) 整除

给定两个整数 **N** 和 **K** ，任务是找到大小不同的数组 **N** 的数量，这些数组可以由第一个元素作为 **K** 形成，这样除了最后一个元素之外的每个元素都可以被数组中的下一个元素整除。由于计数会很大，所以打印模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** N = 3，K = 5
> **输出:** 3
> **解释:**
> 有 3 个可能的有效数组，从满足给定标准的值 5 开始:
> 
> 1.  {5, 5, 5}
> 2.  {5, 5, 1}
> 3.  {5, 1, 1}.
> 
> 因此总数是 3。
> 
> **输入:** N = 3，K = 6
> T3】输出: 9

**方法:**利用[数论](https://www.geeksforgeeks.org/number-theory-competitive-programming/)和[组合学](https://www.geeksforgeeks.org/mathematics-combinatorics-basics/)可以解决给定的问题。数组的第一个元素是 **K** ，那么下一个数组元素就是 **K** 的[因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)之一。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说 **res** 为 **1** ，它存储形成的数组的结果计数。
*   [找出数字 **K**](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/) 的质因数的所有幂，并对每个[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) **P** 执行以下步骤:
    *   求值 **K** 中 **P** 出现的次数。让那个计数成为**计数**。
    *   保持 **P** 其中一个因子的可能方式数由**<sup>(N–count+1)</sup>C<sub>count</sub>**给出。
    *   将值**<sup>(N–计数+ 1)</sup> C <sub>计数</sub>T5】乘以值 **res** 。**
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
int MOD = 1000000007;

// Find the value of x raised to the
// yth power modulo MOD
long modPow(long x, long y)
{
    // Stores the value of x^y
    long r = 1, a = x;

    // Iterate until y is positive
    while (y > 0) {
        if ((y & 1) == 1) {
            r = (r * a) % MOD;
        }
        a = (a * a) % MOD;
        y /= 2;
    }

    return r;
}
// Function to perform the Modular
// Multiplicative Inverse using the
// Fermat's little theorem
long modInverse(long x)
{
    return modPow(x, MOD - 2);
}

// Modular division x / y, find
// modular multiplicative inverse
// of y and multiply by x
long modDivision(long p, long q)
{
    return (p * modInverse(q)) % MOD;
}

// Function to find Binomial Coefficient
// C(n, k) in O(k) time
long C(long n, int k)
{
    // Base Case
    if (k > n) {
        return 0;
    }
    long p = 1, q = 1;

    for (int i = 1; i <= k; i++) {

        // Update the value of p and q
        q = (q * i) % MOD;
        p = (p * (n - i + 1)) % MOD;
    }

    return modDivision(p, q);
}

// Function to find the count of arrays
// having K as the first element satisfying
// the given criteria
int countArrays(int N, int K)
{
    // Stores the resultant count of arrays
    long res = 1;

    // Find the factorization of K
    for (int p = 2; p <= K / p; p++) {

        int c = 0;

        // Stores the count of the exponent
        // of the currentprime factor
        while (K % p == 0) {
            K /= p;
            c++;
        }
        res = (res * C(N - 1 + c, c))
              % MOD;
    }
    if (N > 1) {

        // N is one last prime factor,
        // for c = 1 -> C(N-1+1, 1) = N
        res = (res * N) % MOD;
    }

    // Return the totol count
    return res;
}

// Driver Code
int main()
{
    int N = 3, K = 5;
    cout << countArrays(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    public static int MOD = 1000000007;

    // Find the value of x raised to the
    // yth power modulo MOD
    public static long modPow(long x, long y)
    {

        // Stores the value of x^y
        long r = 1, a = x;

        // Iterate until y is positive
        while (y > 0) {
            if ((y & 1) == 1) {
                r = (r * a) % MOD;
            }
            a = (a * a) % MOD;
            y /= 2;
        }

        return r;
    }

    // Function to perform the Modular
    // Multiplicative Inverse using the
    // Fermat's little theorem
    public static long modInverse(long x) {
        return modPow(x, MOD - 2);
    }

    // Modular division x / y, find
    // modular multiplicative inverse
    // of y and multiply by x
    public static long modDivision(long p, long q) {
        return (p * modInverse(q)) % MOD;
    }

    // Function to find Binomial Coefficient
    // C(n, k) in O(k) time
    public static long C(long n, int k) {
        // Base Case
        if (k > n) {
            return 0;
        }
        long p = 1, q = 1;

        for (int i = 1; i <= k; i++) {

            // Update the value of p and q
            q = (q * i) % MOD;
            p = (p * (n - i + 1)) % MOD;
        }

        return modDivision(p, q);
    }

    // Function to find the count of arrays
    // having K as the first element satisfying
    // the given criteria
    public static long countArrays(int N, int K) {
        // Stores the resultant count of arrays
        long res = 1;

        // Find the factorization of K
        for (int p = 2; p <= K / p; p++) {

            int c = 0;

            // Stores the count of the exponent
            // of the currentprime factor
            while (K % p == 0) {
                K /= p;
                c++;
            }
            res = (res * C(N - 1 + c, c)) % MOD;
        }
        if (N > 1) {

            // N is one last prime factor,
            // for c = 1 -> C(N-1+1, 1) = N
            res = (res * N) % MOD;
        }

        // Return the totol count
        return res;
    }

    // Driver Code
    public static void main(String args[]) {
        int N = 3, K = 5;
        System.out.println(countArrays(N, K));

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python 3 program for the above approach
MOD = 1000000007

from math import sqrt

# Find the value of x raised to the
# yth power modulo MOD
def modPow(x, y):

    # Stores the value of x^y
    r = 1
    a = x

    # Iterate until y is positive
    while(y > 0):
        if ((y & 1) == 1):
            r = (r * a) % MOD
        a = (a * a) % MOD
        y /= 2

    return r
# Function to perform the Modular
# Multiplicative Inverse using the
# Fermat's little theorem
def modInverse(x):
    return modPow(x, MOD - 2)

# Modular division x / y, find
# modular multiplicative inverse
# of y and multiply by x
def modDivision(p, q):
    return (p * modInverse(q)) % MOD

# Function to find Binomial Coefficient
# C(n, k) in O(k) time
def C(n, k):
    # Base Case
    if (k > n):
        return 0

    p = 1
    q = 1

    for i in range(1,k+1,1):

        # Update the value of p and q
        q = (q * i) % MOD
        p = (p * (n - i + 1)) % MOD

    return modDivision(p, q)

# Function to find the count of arrays
# having K as the first element satisfying
# the given criteria
def countArrays(N, K):
    # Stores the resultant count of arrays
    res = 1

    # Find the factorization of K
    for p in range(2,int(sqrt(K)),1):
        c = 0

        # Stores the count of the exponent
        # of the currentprime factor
        while (K % p == 0):
            K /= p
            c += 1
        res = (res * C(N - 1 + c, c)) % MOD
    if (N > 1):

        # N is one last prime factor,
        # for c = 1 -> C(N-1+1, 1) = N
        res = (res * N) % MOD

    # Return the totol count
    return res

# Driver Code
if __name__ == '__main__':
    N = 3
    K = 5
    print(countArrays(N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{   
      public static int MOD = 1000000007;

    // Find the value of x raised to the
    // yth power modulo MOD
    public static long modPow(long x, long y)
    {

        // Stores the value of x^y
        long r = 1, a = x;

        // Iterate until y is positive
        while (y > 0) {
            if ((y & 1) == 1) {
                r = (r * a) % MOD;
            }
            a = (a * a) % MOD;
            y /= 2;
        }

        return r;
    }

    // Function to perform the Modular
    // Multiplicative Inverse using the
    // Fermat's little theorem
    public static long modInverse(long x) {
        return modPow(x, MOD - 2);
    }

    // Modular division x / y, find
    // modular multiplicative inverse
    // of y and multiply by x
    public static long modDivision(long p, long q) {
        return (p * modInverse(q)) % MOD;
    }

    // Function to find Binomial Coefficient
    // C(n, k) in O(k) time
    public static long C(long n, int k) {
        // Base Case
        if (k > n) {
            return 0;
        }
        long p = 1, q = 1;

        for (int i = 1; i <= k; i++) {

            // Update the value of p and q
            q = (q * i) % MOD;
            p = (p * (n - i + 1)) % MOD;
        }

        return modDivision(p, q);
    }

    // Function to find the count of arrays
    // having K as the first element satisfying
    // the given criteria
    public static long countArrays(int N, int K) {
        // Stores the resultant count of arrays
        long res = 1;

        // Find the factorization of K
        for (int p = 2; p <= K / p; p++) {

            int c = 0;

            // Stores the count of the exponent
            // of the currentprime factor
            while (K % p == 0) {
                K /= p;
                c++;
            }
            res = (res * C(N - 1 + c, c)) % MOD;
        }
        if (N > 1) {

            // N is one last prime factor,
            // for c = 1 -> C(N-1+1, 1) = N
            res = (res * N) % MOD;
        }

        // Return the totol count
        return res;
    }

    // Driver Code
    static public void Main (){

        int N = 3, K = 5;
        Console.WriteLine(countArrays(N, K));
    }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach
       let MOD = 1000000007;

       // Find the value of x raised to the
       // yth power modulo MOD
       function modPow(x, y)
       {

           // Stores the value of x^y
           let r = 1, a = x;

           // Iterate until y is positive
           while (y > 0) {
               if ((y & 1) == 1) {
                   r = (r * a) % MOD;
               }
               a = (a * a) % MOD;
               y /= 2;
           }

           return r;
       }

       // Function to perform the Modular
       // Multiplicative Inverse using the
       // Fermat's little theorem
       function modInverse(x) {
           return modPow(x, MOD - 2);
       }

       // Modular division x / y, find
       // modular multiplicative inverse
       // of y and multiply by x
       function modDivision(p, q) {
           return (p * modInverse(q)) % MOD;
       }

       // Function to find Binomial Coefficient
       // C(n, k) in O(k) time
       function C(n, k)
       {

           // Base Case
           if (k > n) {
               return 0;
           }
           let p = 1, q = 1;

           for (let i = 1; i <= k; i++) {

               // Update the value of p and q
               q = (q * i) % MOD;
               p = (p * (n - i + 1)) % MOD;
           }

           return modDivision(p, q);
       }

       // Function to find the count of arrays
       // having K as the first element satisfying
       // the given criteria
       function countArrays(N, K)
       {

           // Stores the resultant count of arrays
           let res = 1;

           // Find the factorization of K
           for (let p = 2; p <= K / p; p++) {

               let c = 0;

               // Stores the count of the exponent
               // of the currentprime factor
               while (K % p == 0) {
                   K /= p;
                   c++;
               }
               res = (res * C(N - 1 + c, c))
                   % MOD;
           }
           if (N > 1) {

               // N is one last prime factor,
               // for c = 1 -> C(N-1+1, 1) = N
               res = (res * N) % MOD;
           }

           // Return the totol count
           return res;
       }

       // Driver Code
       let N = 3, K = 5;
       document.write(countArrays(N, K));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(1)*