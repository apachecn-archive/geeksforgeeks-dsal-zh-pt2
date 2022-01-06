# 对可以表示为素数幂的 N 个数字进行计数

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-可以表示为素数的幂/](https://www.geeksforgeeks.org/count-numbers-up-to-n-that-can-be-expressed-as-powers-of-prime-numbers/)

给定一个整数 **N** ，任务是从**【1，N】**范围内数，这是[素数](https://www.geeksforgeeks.org/prime-numbers/)的幂。

**示例:**

> **输入:** N = 6
> **输出:** 3
> **解释:**
> 范围内可以表示为素数幂的数字有:
> 2 = 2<sup>1</sup>
> 3 = 3<sup>1</sup>
> 4 = 2<sup>2</sup>
> 5 = 5<sup>1</sup>
> 
> **输入:** N = 9
> **输出:** 7
> **解释:**
> 范围内可表示为素数幂的数字为:
> 2 = 2<sup>1</sup>
> 3 = 3<sup>1</sup>
> 4 = 2<sup>2</sup>
> 5 = 5<sup>1</sup>T21】7 = 7<sup>1</sup>

**方式:**使用厄拉多塞的[筛可以解决问题。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

1.  使用厄拉多塞的[筛初始化一个长度为 **N+1** 的数组**素数[]** ，其中**素数[i] = 1** 表示 **i** 是素数，**素数[i] = 0** 表示 I 不是素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2.  把所有质数推进一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，说 **v** 。
3.  初始化一个变量，比如 **ans，**来存储素数幂的计数。
4.  对于每个素数，在向量 **v** 中说出 **p** ，执行以下操作:
    *   初始化一个变量，说 **temp，**等于 **p** 。
    *   检查**温度**是否小于 **N.** 如果发现为真，则执行以下操作:
        *   用 **1** 增加**和**。
        *   更新 **temp = temp * p** ，下一个 **p** 的电源。
5.  将最终计数返回为**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of powers of prime numbers upto N
int countPowerOfPrimes(int N)
{

    // Sieve array
    int prime[N + 1];

    // Sieve of Eratosthenes

    // Initialize all numbers as prime
    for (int i = 0; i <= N; i++)
        prime[i] = 1;

    // Mark 0 and 1 as non prime
    prime[0] = 0;
    prime[1] = 0;

    for (int i = 2; i * i <= N; i++) {
        // If a prime number is found
        if (prime[i] == 1) {
            // Mark all multiples
            // of i as non-prime
            for (int j = i * i;
                 j <= N; j += i) {
                prime[j] = 0;
            }
        }
    }

    // Stores all prime
    // numbers upto N
    vector<int> v;

    // Push all the primes into v
    for (int i = 2; i <= N; i++) {
        if (prime[i] == 1) {
            v.push_back(i);
        }
    }

    // Stores the count of
    // powers of primes up to N
    int ans = 0;

    // Iteratre over every
    // prime number up to N
    for (auto p : v) {
        // Store p in temp
        int temp = p;

        // Iterate until temp exceeds n
        while (temp <= N) {
            // Increment ans by 1
            ans = ans + 1;

            // Update temp to
            // next power of p
            temp = temp * p;
        }
    }

    // Return ans as the final answer
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int n = 9;

    // Function call to count
    // the number of power of
    // primes in the range [1, N]
    cout << countPowerOfPrimes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the number
// of powers of prime numbers upto N
static int countPowerOfPrimes(int N)
{

    // Sieve array
    int prime[] = new int[N + 1];

    // Sieve of Eratosthenes

    // Initialize all numbers as prime
    for(int i = 0; i <= N; i++)
        prime[i] = 1;

    // Mark 0 and 1 as non prime
    prime[0] = 0;
    prime[1] = 0;

    for(int i = 2; i * i <= N; i++)
    {

        // If a prime number is found
        if (prime[i] == 1)
        {

            // Mark all multiples
            // of i as non-prime
            for(int j = i * i;
                    j < N + 1;
                    j += i)
            {
                prime[j] = 0;
            }
        }
    }

    // Stores all prime
    // numbers upto N
    int v[] = new int[N + 1];
    int j = 0;

    // Push all the primes into v
    for(int i = 2; i < N + 1; i++)
    {
        if (prime[i] == 1)
        {
            v[j] = i;
            j += 1;
        }
    }

    // Stores the count of
    // powers of primes up to N
    int ans = 0;

    // Iteratre over every
    // prime number up to N
    for(int k = 0; k < j; k++)
    {

        // Store v[k] in temp
        int temp = v[k];

        // Iterate until temp exceeds n
        while (temp <= N)
        {

            // Increment ans by 1
            ans = ans + 1;

            // Update temp to
            // next power of v[k]
            temp = temp * v[k];
        }
    }

    // Return ans as the final answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 9;

    // Function call to count
    // the number of power of
    // primes in the range [1, N]
    System.out.println(countPowerOfPrimes(n));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number
# of powers of prime numbers upto N
def countPowerOfPrimes(N):

    # Sieve array
    prime = [1] * (N + 1)

    # Mark 0 and 1 as non prime
    prime[0] = 0
    prime[1] = 0

    for i in range(2, N + 1):
        if i * i > N:
            break

        # If a prime number is found
        if (prime[i] == 1):

            # Mark all multiples
            # of i as non-prime
            for j in range(i * i, N + 1, i):
                prime[j] = 0

    # Stores all prime
    # numbers upto N
    v = []

    # Push all the primes into v
    for i in range(2, N + 1):
        if (prime[i] == 1):
            v.append(i)

    # Stores the count of
    # powers of primes up to N
    ans = 0

    # Iteratre over every
    # prime number up to N
    for p in v:

        # Store p in temp
        temp = p

        # Iterate until temp exceeds n
        while (temp <= N):

            # Increment ans by 1
            ans = ans + 1

            # Update temp to
            # next power of p
            temp = temp * p

    # Return ans as the final answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 9

    # Function call to count
    # the number of power of
    # primes in the range [1, N]
    print (countPowerOfPrimes(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number
// of powers of prime numbers upto N
static int countPowerOfPrimes(int N)
{

    // Sieve array
    int[] prime = new int[N + 1];
    int j;

    // Sieve of Eratosthenes

    // Initialize all numbers as prime
    for(int i = 0; i <= N; i++)
        prime[i] = 1;

    // Mark 0 and 1 as non prime
    prime[0] = 0;
    prime[1] = 0;

    for(int i = 2; i * i <= N; i++)
    {

        // If a prime number is found
        if (prime[i] == 1)
        {

            // Mark all multiples
            // of i as non-prime
            for(j = i * i;
                j < N + 1;
                j += i)
            {
                prime[j] = 0;
            }
        }
    }

    // Stores all prime
    // numbers upto N
    int[] v = new int[N + 1];
    j = 0;

    // Push all the primes into v
    for(int i = 2; i < N + 1; i++)
    {
        if (prime[i] == 1)
        {
            v[j] = i;
            j += 1;
        }
    }

    // Stores the count of
    // powers of primes up to N
    int ans = 0;

    // Iteratre over every
    // prime number up to N
    for(int k = 0; k < j; k++)
    {

        // Store v[k] in temp
        int temp = v[k];

        // Iterate until temp exceeds n
        while (temp <= N)
        {

            // Increment ans by 1
            ans = ans + 1;

            // Update temp to
            // next power of v[k]
            temp = temp * v[k];
        }
    }

    // Return ans as the final answer
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    int n = 9;

    // Function call to count
    // the number of power of
    // primes in the range [1, N]
    Console.Write(countPowerOfPrimes(n));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number
// of powers of prime numbers upto N
    function countPowerOfPrimes(N) {

        // Sieve array
        var prime = Array(N + 1).fill(0);

        // Sieve of Eratosthenes

        // Initialize all numbers as prime
        for (i = 0; i <= N; i++)
            prime[i] = 1;

        // Mark 0 and 1 as non prime
        prime[0] = 0;
        prime[1] = 0;

        for (i = 2; i * i <= N; i++) {

            // If a prime number is found
            if (prime[i] == 1) {

                // Mark all multiples
                // of i as non-prime
                for (j = i * i; j < N + 1; j += i) {
                    prime[j] = 0;
                }
            }
        }

        // Stores all prime
        // numbers upto N
        var v = Array(N + 1).fill(0);
        var j = 0;

        // Push all the primes into v
        for (i = 2; i < N + 1; i++) {
            if (prime[i] == 1) {
                v[j] = i;
                j += 1;
            }
        }

        // Stores the count of
        // powers of primes up to N
        var ans = 0;

        // Iteratre over every
        // prime number up to N
        for (k = 0; k < j; k++) {

            // Store v[k] in temp
            var temp = v[k];

            // Iterate until temp exceeds n
            while (temp <= N) {

                // Increment ans by 1
                ans = ans + 1;

                // Update temp to
                // next power of v[k]
                temp = temp * v[k];
            }
        }

        // Return ans as the final answer
        return ans;
    }

    // Driver Code

        var n = 9;

        // Function call to count
        // the number of power of
        // primes in the range [1, N]
        document.write(countPowerOfPrimes(n));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N log(log N))*
***辅助空间:** O(N)*