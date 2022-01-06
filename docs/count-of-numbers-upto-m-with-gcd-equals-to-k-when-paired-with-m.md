# 当与 M 配对时，GCD 等于 K 的最多 M 个数字的计数

> 原文:[https://www . geesforgeks . org/count-numbers-up-m-with-gcd-equals-to-k-with-m-pain/](https://www.geeksforgeeks.org/count-of-numbers-upto-m-with-gcd-equals-to-k-when-paired-with-m/)

给定两个整数 **M** 和 **K** ，任务是计算【0，M】之间的整数数量，使得带有 **M** 的那个整数的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 等于 **K** 。

**示例:**

> **输入:** M = 9，K = 1
> **输出:** 6
> **解释:**
> 当与 9 配对时，GCD 为 1 的可能数字是 1、2、4、5、7、8。
> 
> **输入:** M = 10，K = 5
> T3】输出: 1

**进场:**

*   具有带 M 的 GCD K 的整数将是 K，2K，3K，…..以此类推直到 m
*   让我们考虑 K 的系数，即 1，2，3，4…直到(M/K)。
*   现在我们只需要找到 GCD 为(M/K) = 1 的系数的个数。所以现在问题简化为找到 1 到(M/K)之间的整数个数，Gcd 为(m/k) = 1。
*   为了找到这一点，我们将使用(M/K)的[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)。

下面是上述方法的实现:

## C++

```
// C++ program to Count of numbers
// between 0 to M which have GCD
// with M equals to K.

#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD
// using euler totient function
int EulerTotientFunction(int limit)
{
    int copy = limit;

    // Finding the prime factors of
    // limit to calculate it's
    // euler totient function
    vector<int> primes;

    for (int i = 2; i * i <= limit; i++) {
        if (limit % i == 0) {
            while (limit % i == 0) {
                limit /= i;
            }
            primes.push_back(i);
        }
    }
    if (limit >= 2) {
        primes.push_back(limit);
    }

    // Calculating the euler totient
    // function of (m/k)
    int ans = copy;
    for (auto it : primes) {
        ans = (ans / it) * (it - 1);
    }
    return ans;
}

// Function print the count of
// numbers whose GCD with M
// equals to K
void CountGCD(int m, int k)
{

    if (m % k != 0) {
        // GCD of m with any integer
        // cannot  be equal to k
        cout << 0 << endl;
        return;
    }

    if (m == k) {
        // 0 and m itself will be
        // the only valid integers
        cout << 2 << endl;
        return;
    }

    // Finding the number upto which
    // coefficient of k can come
    int limit = m / k;

    int ans = EulerTotientFunction(limit);

    cout << ans << endl;
}
// Driver code
int main()
{

    int M = 9;
    int K = 1;
    CountGCD(M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count of numbers
// between 0 to M which have GCD
// with M equals to K.
import java.util.*;

class GFG{

// Function to calculate GCD
// using euler totient function
static int EulerTotientFunction(int limit)
{
    int copy = limit;

    // Finding the prime factors of
    // limit to calculate it's
    // euler totient function
    Vector<Integer> primes = new Vector<Integer>();

    for (int i = 2; i * i <= limit; i++) {
        if (limit % i == 0) {
            while (limit % i == 0) {
                limit /= i;
            }
            primes.add(i);
        }
    }
    if (limit >= 2) {
        primes.add(limit);
    }

    // Calculating the euler totient
    // function of (m/k)
    int ans = copy;
    for (int it : primes) {
        ans = (ans / it) * (it - 1);
    }
    return ans;
}

// Function print the count of
// numbers whose GCD with M
// equals to K
static void CountGCD(int m, int k)
{

    if (m % k != 0) {
        // GCD of m with any integer
        // cannot  be equal to k
        System.out.print(0 +"\n");
        return;
    }

    if (m == k) {
        // 0 and m itself will be
        // the only valid integers
        System.out.print(2 +"\n");
        return;
    }

    // Finding the number upto which
    // coefficient of k can come
    int limit = m / k;

    int ans = EulerTotientFunction(limit);

    System.out.print(ans +"\n");
}

// Driver code
public static void main(String[] args)
{

    int M = 9;
    int K = 1;
    CountGCD(M, K);

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to Count of numbers
# between 0 to M which have GCD
# with M equals to K.

# Function to calculate GCD
# using euler totient function
def EulerTotientFunction(limit):
    copy = limit

    # Finding the prime factors of
    # limit to calculate it's
    # euler totient function
    primes = []

    for i in range(2, limit + 1):
        if i * i > limit:
            break
        if (limit % i == 0):
            while (limit % i == 0):
                limit //= i
            primes.append(i)

    if (limit >= 2):
        primes.append(limit)

    # Calculating the euler totient
    # function of (m//k)
    ans = copy
    for it in primes:
        ans = (ans // it) * (it - 1)

    return ans

# Function print the count of
# numbers whose GCD with M
# equals to K
def CountGCD(m, k):

    if (m % k != 0):

        # GCD of m with any integer
        # cannot be equal to k
        print(0)
        return

    if (m == k):

        # 0 and m itself will be
        # the only valid integers
        print(2)
        return

    # Finding the number upto which
    # coefficient of k can come
    limit = m // k

    ans = EulerTotientFunction(limit)

    print(ans)

# Driver code
if __name__ == '__main__':

    M = 9
    K = 1
    CountGCD(M, K)

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to Count of numbers
// between 0 to M which have GCD
// with M equals to K.
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate GCD
// using euler totient function
static int EulerTotientFunction(int limit)
{
    int copy = limit;

    // Finding the prime factors of
    // limit to calculate it's
    // euler totient function
    List<int> primes = new List<int>();

    for (int i = 2; i * i <= limit; i++)
    {
        if (limit % i == 0)
        {
            while (limit % i == 0)
            {
                limit /= i;
            }
            primes.Add(i);
        }
    }
    if (limit >= 2)
    {
        primes.Add(limit);
    }

    // Calculating the euler totient
    // function of (m/k)
    int ans = copy;
    foreach (int it in primes)
    {
        ans = (ans / it) * (it - 1);
    }
    return ans;
}

// Function print the count of
// numbers whose GCD with M
// equals to K
static void CountGCD(int m, int k)
{
    if (m % k != 0)
    {
        // GCD of m with any integer
        // cannot be equal to k
        Console.Write(0 + "\n");
        return;
    }

    if (m == k)
    {
        // 0 and m itself will be
        // the only valid integers
        Console.Write(2 + "\n");
        return;
    }

    // Finding the number upto which
    // coefficient of k can come
    int limit = m / k;

    int ans = EulerTotientFunction(limit);

    Console.Write(ans + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int M = 9;
    int K = 1;
    CountGCD(M, K);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to Count of numbers
// between 0 to M which have GCD
// with M equals to K.

// Function to calculate GCD
// using euler totient function
function EulerTotientFunction(limit)
{
    let copy = limit;

    // Finding the prime factors of
    // limit to calculate it's
    // euler totient function
    let primes = [];

    for (let i = 2; i * i <= limit; i++) {
        if (limit % i == 0) {
            while (limit % i == 0) {
                limit /= i;
            }
            primes.push(i);
        }
    }
    if (limit >= 2) {
        primes.push(limit);
    }

    // Calculating the euler totient
    // function of (m/k)
    let ans = copy;
    for (let it in primes) {
        ans = (ans / primes[it]) * (primes[it] - 1);
    }
    return ans;
}

// Function print the count of
// numbers whose GCD with M
// equals to K
function CountGCD(m, k)
{

    if (m % k != 0) {
        // GCD of m with any integer
        // cannot  be equal to k
        document.write(0 +"<br/>");
        return;
    }

    if (m == k) {
        // 0 and m itself will be
        // the only valid integers
        document.write(2 +"<br/>");
        return;
    }

    // Finding the number upto which
    // coefficient of k can come
    let limit = Math.floor(m / k);

    let ans = EulerTotientFunction(limit);

    document.write(ans +"\n");
}

// Driver Code

    let M = 9;
    let K = 1;
    CountGCD(M, K);

</script>
```

**Output:** 

```
6
```

时间复杂度:O((m / k) <sup>1/2</sup> * log(m/k))

辅助空间:O((m / k) <sup>1/2</sup> )