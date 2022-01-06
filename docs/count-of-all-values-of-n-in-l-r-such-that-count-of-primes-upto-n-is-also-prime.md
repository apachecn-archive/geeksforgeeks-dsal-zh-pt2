# 对[L，R]中 N 的所有值进行计数，使得直到 N 的素数的计数也是素数

> 原文:[https://www . geeksforgeeks . org/n-in-l-r-this-count-of-prime-up-n-也是 prime/](https://www.geeksforgeeks.org/count-of-all-values-of-n-in-l-r-such-that-count-of-primes-upto-n-is-also-prime/)

给定两个正整数 **L** 和 **R** ，任务是找出范围**【L，R】**之间的值的总数，使得从 **1** 到 **N** 的质数也是质数。
**示例:**

> **输入:** L = 3，R = 10
> **输出:** 4
> **说明:**
> 3、4、5、6、7、8、9、10 的素数分别为 2、2、3、3、4、4、4、4、4。因此，总共有 4 个这样的数字{3，4，5，6}[3，10]。
> **输入:** L = 4，R = 12
> **输出:** 5
> **解释:**
> 4、5、6、7、8、9、10、11 和 12 的素数分别为 2、3、3、4、4、4、5 和 5。因此，总共有 5 个这样的数字{4，5，6，11，12}满足范围[4，12]中的条件。

**天真方法:**
解决问题最简单的方法是遍历[1，L–1]**范围内的所有值，计算**该范围内的素数。一旦计算完毕，检查**计数**是否为质数。现在，开始逐个遍历**【L，R】**范围内的值，检查数字是否为质数，并相应增加计数。对于每次更新的计数，检查它是否是质数，并相应地更新给定范围内所需数字的计数。
***时间复杂度:**O(R<sup>2</sup>)*
**高效途径:**
以上途径可以通过厄拉多塞的[筛进一步优化。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

1.  用筛子找出所有直到 **R** 的质数。
2.  维护一个频率数组，以存储所有值的素数计数，直到 **R** 。
3.  创建另一个计数数组(比如 **freqPrime[]** )，如果到 **i** 的总素数的累计计数本身就是一个素数，则在位置 **i** 处加 1。
4.  现在对于任意范围 **L 到 R** ，那么疯狂素数的个数可以通过**freqPrime[R]–freqPrime[L–1]**来计算。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// crazy primes in the given range [L, R]
int count_crazy_primes(int L, int R)
{
    // Stores all primes
    int prime[R + 1] = { 0 };

    // Stores count of primes
    int countPrime[R + 1] = { 0 };

    // Stores if frequency of
    // primes is a prime or not
    // upto each index
    int freqPrime[R + 1] = { 0 };

    prime[0] = prime[1] = 1;
    // Sieve of Eratosthenes
    for (int p = 2; p * p <= R; p++) {
        if (prime[p] == 0) {
            for (int i = p * p;
                 i <= R; i += p)

                prime[i] = 1;
        }
    }

    // Count primes
    for (int i = 1; i <= R; i++) {
        countPrime[i] = countPrime[i - 1];

        // If i is a prime
        if (!prime[i]) {
            countPrime[i]++;
        }
    }

    // Stores frequency of primes
    for (int i = 1; i <= R; i++) {
        freqPrime[i] = freqPrime[i - 1];

        // If the frequency of primes
        // is a prime
        if (!prime[countPrime[i]]) {

            // Increase count of
            // required numbers
            freqPrime[i]++;
        }
    }

    // Return the required count
    return (freqPrime[R]
            - freqPrime[L - 1]);
}

// Driver Code
int main()
{
    // Given Range
    int L = 4, R = 12;

    // Function Call
    cout << count_crazy_primes(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Function to count the number of
// crazy primes in the given range [L, R]
static int count_crazy_primes(int L, int R)
{

    // Stores all primes
    int prime[] = new int[R + 1];

    // Stores count of primes
    int countPrime[] = new int[R + 1];

    // Stores if frequency of
    // primes is a prime or not
    // upto each index
    int freqPrime[] = new int[R + 1];

    prime[0] = 1;
    prime[1] = 1;

    // Sieve of Eratosthenes
    for(int p = 2; p * p <= R; p++)
    {
       if (prime[p] == 0)
       {
           for(int i = p * p;
                   i <= R; i += p)
              prime[i] = 1;
       }
    }

    // Count primes
    for(int i = 1; i <= R; i++)
    {
       countPrime[i] = countPrime[i - 1];

       // If i is a prime
       if (prime[i] != 0)
       {
           countPrime[i]++;
       }
    }

    // Stores frequency of primes
    for(int i = 1; i <= R; i++)
    {
       freqPrime[i] = freqPrime[i - 1];

       // If the frequency of primes
       // is a prime
       if (prime[countPrime[i]] != 0)
       {

           // Increase count of
           // required numbers
           freqPrime[i]++;
       }
    }

    // Return the required count
    return (freqPrime[R] -
            freqPrime[L - 1]);
}

// Driver code
public static void main (String[] args)
{

    // Given range
    int L = 4, R = 12;

    // Function call
    System.out.println(count_crazy_primes(L, R));
}
}

// This code is contributed by Pratima Pandey    
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# crazy primes in the given range [L, R]
def count_crazy_primes(L, R):

    # Stores all primes
    prime = [0] * (R + 1)

    # Stores count of primes
    countPrime = [0] * (R + 1)

    # Stores if frequency of
    # primes is a prime or not
    # upto each index
    freqPrime = [0] * (R + 1)

    prime[0] = prime[1] = 1

    # Sieve of Eratosthenes
    p = 2
    while p * p <= R:
        if (prime[p] == 0):
            for i in range (p * p,
                            R + 1 , p):
                prime[i] = 1
        p += 1

    # Count primes
    for i in range (1 , R + 1):
        countPrime[i] = countPrime[i - 1]

        # If i is a prime
        if (not prime[i]):
            countPrime[i] += 1

    # Stores frequency of primes
    for i in range (1, R + 1):
        freqPrime[i] = freqPrime[i - 1]

        # If the frequency of primes
        # is a prime
        if (not prime[countPrime[i]]):

            # Increase count of
            # required numbers
            freqPrime[i] += 1

    # Return the required count
    return (freqPrime[R] -
            freqPrime[L - 1])

# Driver Code
if __name__ =="__main__":

    # Given Range
    L = 4
    R = 12

    # Function Call
    print(count_crazy_primes(L, R))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the approach
using System;
class GFG{

// Function to count the number of
// crazy primes in the given range [L, R]
static int count_crazy_primes(int L,
                              int R)
{     
    // Stores all primes
    int []prime = new int[R + 1];

    // Stores count of primes
    int []countPrime = new int[R + 1];

    // Stores if frequency of
    // primes is a prime or not
    // upto each index
    int []freqPrime = new int[R + 1];

    prime[0] = 1;
    prime[1] = 1;

    // Sieve of Eratosthenes
    for(int p = 2; p * p <= R; p++)
    {
       if (prime[p] == 0)
       {
           for(int i = p * p; i <= R;
               i += p)
              prime[i] = 1;
       }
    }

    // Count primes
    for(int i = 1; i <= R; i++)
    {
       countPrime[i] = countPrime[i - 1];

       // If i is a prime
       if (prime[i] != 0)
       {
           countPrime[i]++;
       }
    }

    // Stores frequency of primes
    for(int i = 1; i <= R; i++)
    {
       freqPrime[i] = freqPrime[i - 1];

       // If the frequency of primes
       // is a prime
       if (prime[countPrime[i]] != 0)
       {            
           // Increase count of
           // required numbers
           freqPrime[i]++;
       }
    }

    // Return the required count
    return (freqPrime[R] -
            freqPrime[L - 1]);
}

// Driver code
public static void Main(String[] args)
{      
    // Given range
    int L = 4, R = 12;

    // Function call
    Console.WriteLine(
            count_crazy_primes(L, R));
}
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number of
// crazy primes in the given range [L, R]
function count_crazy_primes(L, R)
{

    // Stores all primes
    let prime = Array.from({length: R+1}, (_, i) => 0);

    // Stores count of primes
    let countPrime = Array.from({length: R+1}, (_, i) => -1);

    // Stores if frequency of
    // primes is a prime or not
    // upto each index
    let freqPrime = Array.from({length: R+1}, (_, i) => 0);

    prime[0] = 1;
    prime[1] = 1;

    // Sieve of Eratosthenes
    for(let p = 2; p * p <= R; p++)
    {
       if (prime[p] == 0)
       {
           for(let i = p * p;
                   i <= R; i += p)
              prime[i] = 1;
       }
    }

    // Count primes
    for(let i = 1; i <= R; i++)
    {
       countPrime[i] = countPrime[i - 1];

       // If i is a prime
       if (prime[i] != 0)
       {
           countPrime[i]++;
       }
    }
    // Stores frequency of primes
    for (let i = 1; i <= R; i++) {
        freqPrime[i] = freqPrime[i - 1];

        // If the frequency of primes
        // is a prime
        if (!prime[countPrime[i]]) {

            // Increase count of
            // required numbers
            freqPrime[i]++;
        }
    }

    // Return the required count
    return (freqPrime[R] -
            freqPrime[L - 1]);
}

    // Driver Code

    // Given range
    let L = 4, R = 12;

    // Function call
    document.write(count_crazy_primes(L, R));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(R * log(log(R)))*
***辅助空间:** O(R)*