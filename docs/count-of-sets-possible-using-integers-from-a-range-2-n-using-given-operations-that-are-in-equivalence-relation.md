# 使用等价关系

中的给定运算，使用范围[2，N]中的整数对可能的集合进行计数

> 原文:[https://www . geesforgeks . org/集合计数-可能使用范围内的整数-2-n-使用等价关系中的给定运算/](https://www.geeksforgeeks.org/count-of-sets-possible-using-integers-from-a-range-2-n-using-given-operations-that-are-in-equivalence-relation/)

给定一个整数 **N** ，从范围 **2** 到 **N** 中反复选择两个不同的整数，如果发现它们的 GCD 大于 1，尽可能长地将它们插入同一个集合中。在[等价关系](https://www.geeksforgeeks.org/number-possible-equivalence-relations-finite-set/)中形成的集合。因此，如果整数 **a** 和 **b** 在同一个集合中，整数 **b** 和 **c** 在同一个集合中，那么整数 **a** 和 **c** 也称在同一个组中。任务是找到可以形成的这种集合的总数。

**示例:**

> **输入:** N = 3
> **输出:** 2
> **说明:**形成的集合有:{2}、{3}。它们不能放在同一个集合中，因为 GCD 为 1。
> 
> **输入:** N = 9
> **输出:** 3
> 形成的集合为:{2，3，4，6，8，9}，{5}，{7}
> 因为{2，4，6，8}位于同一个集合中，{3，6，9}也位于同一个集合中。因此，所有这些都在一个集合中，因为 6 是这两个集合中的公共元素。

**方法:**解决问题的思路是基于以下观察:所有小于或等于 **N/2** 的数字都属于同一个集合，因为如果其中乘以 2，它们将是偶数，并且 GCD 大于 **1** 和 **2** 。所以剩下的集合是由大于 N/2 的数组成的，并且是素数，因为如果它们不是素数，那么有一个小于或等于 N/2 的数是这个数的除数。使用厄拉多塞的[筛可以找到从 2 到 N 的质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
bool prime[100001];

// Sieve of Eratosthenes to find
// primes less than or equal to N
void SieveOfEratosthenes(int n)
{

    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        if (prime[p] == true) {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find number of Sets
void NumberofSets(int N)
{
    SieveOfEratosthenes(N);

    // Handle Base Case
    if (N == 2) {
        cout << 1 << endl;
    }
    else if (N == 3) {
        cout << 2 << endl;
    }
    else {

        // Set which contains less
        // than or equal to N/2
        int ans = 1;

        // Number greater than N/2 and
        // are prime increment it by 1
        for (int i = N / 2 + 1; i <= N; i++) {

            // If the number is prime
            // Increment answer by 1
            if (prime[i]) {
                ans += 1;
            }
        }

        cout << ans << endl;
    }
}
// Driver Code
int main()
{
    // Input
    int N = 9;

    // Function Call
    NumberofSets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static boolean prime[] = new boolean[100001];

// Sieve of Eratosthenes to find
// primes less than or equal to N
static void SieveOfEratosthenes(int n)
{
    Arrays.fill(prime, true);

    for(int p = 2; p * p <= n; p++)
    {
        if (prime[p] == true)
        {
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find number of Sets
static void NumberofSets(int N)
{
    SieveOfEratosthenes(N);

    // Handle Base Case
    if (N == 2)
    {
        System.out.print(1);
    }
    else if (N == 3)
    {
        System.out.print(2);
    }
    else
    {

        // Set which contains less
        // than or equal to N/2
        int ans = 1;

        // Number greater than N/2 and
        // are prime increment it by 1
        for(int i = N / 2 + 1; i <= N; i++)
        {

            // If the number is prime
            // Increment answer by 1
            if (prime[i])
            {
                ans += 1;
            }
        }
        System.out.print(ans);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 9;

    // Function Call
    NumberofSets(N);
}   
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach
prime = [True] * 100001

# Sieve of Eratosthenes to find
# primes less than or equal to N
def SieveOfEratosthenes(n):

    global prime

    for p in range(2, n + 1):
        if p * p > n:
            break

        if (prime[p] == True):
            for i in range(p * p, n + 1, p):
                prime[i] = False

# Function to find number of Sets
def NumberofSets(N):

    SieveOfEratosthenes(N)

    # Handle Base Case
    if (N == 2):
        print(1)
    elif (N == 3):
        print(2)
    else:

        # Set which contains less
        # than or equal to N/2
        ans = 1

        # Number greater than N/2 and
        # are prime increment it by 1
        for i in range(N // 2, N + 1):

            # If the number is prime
            # Increment answer by 1
            if (prime[i]):
                ans += 1

        print(ans)

# Driver Code
if __name__ == '__main__':

    # Input
    N = 9

    # Function Call
    NumberofSets(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{
static bool []prime = new bool[100001];

// Sieve of Eratosthenes to find
// primes less than or equal to N
static void SieveOfEratosthenes(int n)
{

    for(int i=0;i<100001;i++)
        prime[i] = true;

    for (int p = 2; p * p <= n; p++) {

        if (prime[p] == true) {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find number of Sets
static void NumberofSets(int N)
{
    SieveOfEratosthenes(N);

    // Handle Base Case
    if (N == 2) {
        Console.Write(1);
    }
    else if (N == 3) {
        Console.Write(2);
    }
    else {

        // Set which contains less
        // than or equal to N/2
        int ans = 1;

        // Number greater than N/2 and
        // are prime increment it by 1
        for (int i = N / 2 + 1; i <= N; i++) {

            // If the number is prime
            // Increment answer by 1
            if (prime[i]) {
                ans += 1;
            }
        }

        Console.Write(ans);
    }
}

// Driver Code
public static void Main()
{
    // Input
    int N = 9;

    // Function Call
    NumberofSets(N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let prime = new Array(100001);

// Sieve of Eratosthenes to find
// primes less than or equal to N
function SieveOfEratosthenes(n)
{
    for(let i=0;i<prime.length;i++)
    {
        prime[i]=true;
    }

    for(let p = 2; p * p <= n; p++)
    {
        if (prime[p] == true)
        {
            for(let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find number of Sets
function NumberofSets(N)
{
    SieveOfEratosthenes(N);

    // Handle Base Case
    if (N == 2)
    {
        document.write(1);
    }
    else if (N == 3)
    {
        document.write(2);
    }
    else
    {

        // Set which contains less
        // than or equal to N/2
        let ans = 1;

        // Number greater than N/2 and
        // are prime increment it by 1
        for(let i = Math.floor(N / 2) + 1; i <= N; i++)
        {

            // If the number is prime
            // Increment answer by 1
            if (prime[i])
            {
                ans += 1;
            }
        }
        document.write(ans);
    }
}

// Driver Code
// Input
let N = 9;

// Function Call
NumberofSets(N);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(K)