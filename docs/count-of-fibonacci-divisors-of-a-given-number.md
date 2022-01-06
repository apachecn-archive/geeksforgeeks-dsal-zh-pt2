# 给定数目的斐波那契除数

> 原文:[https://www . geeksforgeeks . org/给定数字的斐波那契除数/](https://www.geeksforgeeks.org/count-of-fibonacci-divisors-of-a-given-number/)

给定一个数字 **N** ，任务是[找到属于](https://www.geeksforgeeks.org/total-number-divisors-given-number/)[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的 N 的除数。

**示例:**

> **输入:** N = 12
> **输出:** 3
> **说明:**
> 1、2、3 是斐波那契数列中 12 的 3 除数。
> 因此，答案是 3。
> 
> **输入:** N = 110
> **输出:** 4
> **说明:**
> 1、2、5、55 是斐波那契数列中 110 的 4 除数。

**高效方法**:

1.  创建一个[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)来存储所有的斐波那契数，直到 N，以便在 O(1)时间内登记。
2.  [求 o(∛n n 的所有除数)](https://www.geeksforgeeks.org/count-divisors-n-on13/)
3.  对于每个除数，检查它是否也是斐波那契数。数一数这样的除数并打印出来。

下面是上述方法的实现:

## C++

```
// C++ program to count number of divisors
// of N which are Fibonacci numbers

#include <bits/stdc++.h>
using namespace std;

// Function to create hash table
// to check Fibonacci numbers
void createHash(
    set<int>& hash, int maxElement)
{
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to count number of divisors
// of N which are fibonacci numbers
int countFibonacciDivisors(int n)
{
    set<int> hash;
    createHash(hash, n);

    int cnt = 0;
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {

            // If divisors are equal,
            // check and count only one
            if ((n / i == i)
                && (hash.find(n / i)
                    != hash.end()))
                cnt++;

            // Otherwise check and count both
            else {
                if (hash.find(n / i)
                    != hash.end())
                    cnt++;
                if (hash.find(n / (n / i))
                    != hash.end())
                    cnt++;
            }
        }
    }
    return cnt;
}

// Driver code
int main()
{
    int n = 12;

    cout << countFibonacciDivisors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of divisors
// of N which are Fibonacci numbers
import java.util.*;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(
    HashSet<Integer> hash, int maxElement)
{
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to count number of divisors
// of N which are fibonacci numbers
static int countFibonacciDivisors(int n)
{
    HashSet<Integer> hash = new HashSet<Integer>();
    createHash(hash, n);

    int cnt = 0;
    for (int i = 1; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {

            // If divisors are equal,
            // check and count only one
            if ((n / i == i)
                && (hash.contains(n / i)))
                cnt++;

            // Otherwise check and count both
            else {
                if (hash.contains(n / i))
                    cnt++;
                if (hash.contains(n / (n / i)))
                    cnt++;
            }
        }
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 12;

    System.out.print(countFibonacciDivisors(n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count number of divisors
# of N which are Fibonacci numbers
from math import sqrt,ceil,floor

# Function to create hash table
# to check Fibonacci numbers
def createHash(maxElement):
    prev = 0
    curr = 1
    d = dict()
    d[prev] = 1
    d[curr] = 1

    while (curr <= maxElement):
        temp = curr + prev
        d[temp] = 1
        prev = curr
        curr = temp
    return d

# Function to count number of divisors
# of N which are fibonacci numbers
def countFibonacciDivisors(n):
    hash = createHash(n)

    cnt = 0
    for i in range(1, ceil(sqrt(n))):
        if (n % i == 0):

            # If divisors are equal,
            # check and count only one
            if ((n // i == i)
                and (n // i in hash)):
                cnt += 1

            # Otherwise check and count both
            else:
                if (n // i in hash):
                    cnt += 1
                if (n // (n // i) in hash):
                    cnt += 1
    return cnt

# Driver code
n = 12

print(countFibonacciDivisors(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count number of divisors
// of N which are Fibonacci numbers
using System;
using System.Collections.Generic;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(
    HashSet<int> hash, int maxElement)
{
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to count number of divisors
// of N which are fibonacci numbers
static int countFibonacciDivisors(int n)
{
    HashSet<int> hash = new HashSet<int>();
    createHash(hash, n);

    int cnt = 0;
    for (int i = 1; i <= Math.Sqrt(n); i++) {
        if (n % i == 0) {

            // If divisors are equal,
            // check and count only one
            if ((n / i == i)
                && (hash.Contains(n / i)))
                cnt++;

            // Otherwise check and count both
            else {
                if (hash.Contains(n / i))
                    cnt++;
                if (hash.Contains(n / (n / i)))
                    cnt++;
            }
        }
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int n = 12;

    Console.Write(countFibonacciDivisors(n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to count number of divisors
// of N which are Fibonacci numbers

// Function to create hash table
// to check Fibonacci numbers
function createHash( hash, maxElement)
{
    let prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {
        let temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to count number of divisors
// of N which are fibonacci numbers
function countFibonacciDivisors(n)
{
    let hash = new Set();
    createHash(hash, n);

    let cnt = 0;
    for (let i = 1; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {

            // If divisors are equal,
            // check and count only one
            if ((n / i == i)
                && (hash.has(n / i)))
                cnt++;

            // Otherwise check and count both
            else {
                if (hash.has(n / i))
                    cnt++;
                if (hash.has(n / (n / i)))
                    cnt++;
            }
        }
    }
    return cnt;
}

// Driver Code

    let n = 12;

    document.write(countFibonacciDivisors(n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(∛N)*

***辅助空间:**O(N)*T4】