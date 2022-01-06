# 计算最多 N 个质数，可以表示为两个质数之和

> 原文:[https://www . geesforgeks . org/count-质数-最多 n 个可以表示为两个质数之和的数/](https://www.geeksforgeeks.org/count-prime-numbers-up-to-n-that-can-be-represented-as-a-sum-of-two-prime-numbers/)

给定一个正整数 **N** ，任务是找出小于或等于 **N** 的[素数](https://www.geeksforgeeks.org/tag/prime-number/)的个数，可以表示为两个素数的[和。](https://www.geeksforgeeks.org/check-if-a-prime-number-can-be-expressed-as-sum-of-two-prime-numbers/)

**示例:**

> **输入:** N = 6
> **输出:** 1
> **说明:**
> 5 是**【1，6】**范围内唯一可以表示为 2 个素数之和的素数，即 5 = 2 + 3，其中 2，3，5 都是素数。
> 因此，计数为 2。
> 
> **输入:**N = 14
> T3】输出: 3

**天真方法:**解决给定问题最简单的方法是[考虑范围内所有可能的对(I，j)**【1，N】**](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)和[如果 **i** 和 **j** 是素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)和 **(i + j)** 位于范围内**【1，N】**则增加素数的计数。检查所有可能的配对后，打印获得的总计数值。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   除了 **2** 外，所有的[质数](https://www.geeksforgeeks.org/tag/prime-number/)都是奇数
*   [表示一个质数](https://www.geeksforgeeks.org/count-of-ways-to-represent-n-as-sum-of-a-prime-number-and-twice-of-a-square/)(也就是**奇数**)不可能表示为两个奇数质数之和，所以两个质数之一应该是 **2** 。
*   所以对于一个[质数](https://www.geeksforgeeks.org/tag/prime-number/) **X** 是两个质数的和，**X–2**也必须是质数。

按照以下步骤解决问题:

*   初始化一个数组，说出大小为**10<sup>5</sup>T5【的**素数[]** ，用厄拉多塞的[筛填充所有素数直到**10<sup>5</sup>T9】。**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**
*   初始化一个大小为 **(N + 1)** 的辅助[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **dp[]** ，其中 **dp[i]** 是小于或等于 **i** 的素数的计数，可以表示为 2 个素数[之和](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N】**，并执行以下步骤:
    *   将**DP[I–1]**的值更新为**DP[I–1]**和 **dp[i]** 之和。
    *   检查 **prime[i]** 和**prime[I–2]**是否为 **true** ，然后将 **dp[i]** 的值增加 **1** 。
*   完成上述步骤后，打印**DP【N】**的值作为结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to store all prime numbers
// up to N using Sieve of Eratosthenes
void SieveOfEratosthenes(
    int n, bool prime[])
{
    // Set 0 and 1 as non-prime
    prime[0] = 0;
    prime[1] = 0;

    for (int p = 2; p * p <= n; p++) {

        // If p is prime
        if (prime[p] == true) {

            // Set all multiples
            // of p as non-prime
            for (int i = p * p;
                 i <= n; i += p) {
                prime[i] = false;
            }
        }
    }
}

// Function to count prime numbers
// up to N that can be represented
// as the sum of two prime numbers
void countPrime(int n)
{
    // Stores all the prime numbers
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    // Update the prime array
    SieveOfEratosthenes(n, prime);

    // Create a dp array of size n + 1
    int dp[n + 1];

    memset(dp, 0, sizeof(dp));

    // Update dp[1] = 0
    dp[1] = 0;

    // Iterate over the range [2, N]
    for (int i = 2; i <= n; i++) {

        // Add the previous count value
        dp[i] += dp[i - 1];

        // Increment dp[i] by 1 if i
        // and (i - 2) are both prime
        if (prime[i] == 1
            && prime[i - 2] == 1) {
            dp[i]++;
        }
    }

    // Print the result
    cout << dp[n];
}

// Driver Code
int main()
{
    int N = 6;
    countPrime(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java approach for the above approach
class GFG{

// Function to store all prime numbers
// up to N using Sieve of Eratosthenes
static void SieveOfEratosthenes(int n, boolean prime[])
{

    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= n; p++)
    {

        // If p is prime
        if (prime[p] == true)
        {

            // Set all multiples
            // of p as non-prime
            for(int i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to count prime numbers
// up to N that can be represented
// as the sum of two prime numbers
static void countPrime(int n)
{

    // Stores all the prime numbers
    boolean prime[] = new boolean[n + 1];

    for(int i = 0; i < prime.length; i++)
    {
        prime[i] = true;
    }

    // Update the prime array
    SieveOfEratosthenes(n, prime);

    // Create a dp array of size n + 1
    int dp[] = new int[n + 1];
    for(int i = 0; i < dp.length; i++)
    {
        dp[i] = 0;
    }

    // Update dp[1] = 0
    dp[1] = 0;

    // Iterate over the range [2, N]
    for(int i = 2; i <= n; i++)
    {

        // Add the previous count value
        dp[i] += dp[i - 1];

        // Increment dp[i] by 1 if i
        // and (i - 2) are both prime
        if (prime[i] == true &&
            prime[i - 2] == true)
        {
            dp[i]++;
        }
    }

    // Print the result
    System.out.print(dp[n]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;

    countPrime(N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to store all prime numbers
# up to N using Sieve of Eratosthenes
def SieveOfEratosthenes(n, prime):

    # Set 0 and 1 as non-prime
    prime[0] = 0
    prime[1] = 0

    p = 2

    while p * p <= n:

        # If p is prime
        if (prime[p] == True):

            # Set all multiples
            # of p as non-prime
            for i in range(p * p, n + 1, p):
                prime[i] = False

        p += 1

# Function to count prime numbers
# up to N that can be represented
# as the sum of two prime numbers
def countPrime(n):

    # Stores all the prime numbers
    prime = [True] * (n + 1)

    # Update the prime array
    SieveOfEratosthenes(n, prime)

    # Create a dp array of size n + 1
    dp = [0] * (n + 1)

    # Update dp[1] = 0
    dp[1] = 0

    # Iterate over the range [2, N]
    for i in range(2, n + 1):

        # Add the previous count value
        dp[i] += dp[i - 1]

        # Increment dp[i] by 1 if i
        # and (i - 2) are both prime
        if (prime[i] == 1 and prime[i - 2] == 1):
            dp[i] += 1

    # Print the result
    print(dp[n])

# Driver Code
if __name__ == "__main__":

    N = 6

    countPrime(N)

# This code is contributed by mohit ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to store all prime numbers
// up to N using Sieve of Eratosthenes
static void SieveOfEratosthenes(int n, bool[] prime)
{

    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= n; p++)
    {

        // If p is prime
        if (prime[p] == true)
        {

            // Set all multiples
            // of p as non-prime
            for(int i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to count prime numbers
// up to N that can be represented
// as the sum of two prime numbers
static void countPrime(int n)
{

    // Stores all the prime numbers
    bool[] prime = new bool[n + 1];

    for(int i = 0; i < prime.Length; i++)
    {
        prime[i] = true;
    }

    // Update the prime array
    SieveOfEratosthenes(n, prime);

    // Create a dp array of size n + 1
    int[] dp = new int[n + 1];
    for(int i = 0; i < dp.Length; i++)
    {
        dp[i] = 0;
    }

    // Update dp[1] = 0
    dp[1] = 0;

    // Iterate over the range [2, N]
    for(int i = 2; i <= n; i++)
    {

        // Add the previous count value
        dp[i] += dp[i - 1];

        // Increment dp[i] by 1 if i
        // and (i - 2) are both prime
        if (prime[i] == true &&
            prime[i - 2] == true)
        {
            dp[i]++;
        }
    }

    // Print the result
    Console.Write(dp[n]);
}

// Driver code
static void Main()
{
    int N = 6;

    countPrime(N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to store all prime numbers
// up to N using Sieve of Eratosthenes
function SieveOfEratosthenes(n, prime)
{

    // Set 0 and 1 as non-prime
    prime[0] = 0;
    prime[1] = 0;

    for(var p = 2; p * p <= n; p++)
    {

        // If p is prime
        if (prime[p] == Boolean(true))
        {

            // Set all multiples
            // of p as non-prime
            for(var i = p * p;i <= n; i += p)
            {
                prime[i] = Boolean(false);
            }
        }
    }
}

// Function to count prime numbers
// up to N that can be represented
// as the sum of two prime numbers
function countPrime(n)
{

    // Stores all the prime numbers
    var prime = new Array(n + 1);
    var x = new Boolean(true);
    prime.fill(x);

    // Update the prime array
    SieveOfEratosthenes(n, prime);

    // Create a dp array of size n + 1
    var dp = new Array(n + 1);
    dp.fill(0);

    // Update dp[1] = 0
    dp[1] = 0;

    // Iterate over the range [2, N]
    for(var i = 2; i <= n; i++)
    {

        // Add the previous count value
        dp[i] += dp[i - 1];

        // Increment dp[i] by 1 if i
        // and (i - 2) are both prime
        if (prime[i] == Boolean(true) &&
            prime[i - 2] == Boolean(true))
        {
            dp[i]++;

        }
    }

    // Print the result
    document.write(dp[n]);
}

// Driver code
var n = 6;

countPrime(n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*