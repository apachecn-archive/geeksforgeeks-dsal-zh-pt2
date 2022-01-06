# 找出 L 到 R 范围内的所有数字，使数字和数字平方之和为质数

> 原文:[https://www . geeksforgeeks . org/find-所有数字-范围-l 到-r-这样-数字的总和和数字的平方的总和是质数/](https://www.geeksforgeeks.org/find-all-numbers-between-range-l-to-r-such-that-sum-of-digit-and-sum-of-square-of-digit-is-prime/)

给定范围 **L** 和 **R，**计算 **L** 到 **R** 之间的所有数字，使得每个数字的**位数之和**和每个数字的**位数之和**为**质数**。
**注:**10<=【L，R】<= 10<sup>8</sup>

**示例:**

> **输入:** L = 10，R = 20
> T3】输出: 4
> 这样的数字类型有:11 12 14 16
> 
> **输入:** L = 100，R = 130
> **输出:** 9
> 这样的数字类型有:101 102 104 106 110 111 113 119 120

**天真的做法:**
只需要得到每个数的位数之和，每个数的位数的平方之和，检查两者是否都是质数。

**有效方法:**

*   现在，如果你仔细观察这个范围，数字是**10<sup>8</sup>T3】ie。，小于这个的最大数字将是 **99999999** ，可以形成的最大数字是 **8 * ( 9 * 9 ) = 648** (由于数字的平方和是 9<sup>2</sup>+9<sup>2</sup>+…8 倍)，所以，我们只需要 648 以内的素数，这只能用厄拉多塞的[筛来完成。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**
*   现在迭代范围内的每个数字，检查它是否满足上述条件。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Sieve of prime numbers
void primesieve(vector<bool>& prime)
{
    // Sieve to store whether a
    // number is prime or not in
    // O(nlog(log(n)))
    prime[1] = false;

    for (int p = 2; p * p <= 650; p++) {
        if (prime[p] == true) {
            for (int i = p * 2; i <= 650; i += p)
                prime[i] = false;
        }
    }
}

// Function to return sum of digit
// and sum of square of digit
pair<int, int> sum_sqsum(int n)
{

    int sum = 0;
    int sqsum = 0;
    int x;

    // Until number is not
    // zero
    while (n) {
        x = n % 10;
        sum += x;
        sqsum += x * x;
        n /= 10;
    }

    return (make_pair(sum, sqsum));
}

// Function to return the count
// of number form L to R
// whose sum of digits and
// sum of square of digits
// are prime
int countnumber(int L, int R)
{

    vector<bool> prime(651, true);

    primesieve(prime);

    int cnt = 0;

    // Iterate for each value
    // in the range of L to R
    for (int i = L; i <= R; i++) {

        // digit.first stores sum of digits
        // digit.second stores sum of
        // square of digit
        pair<int, int> digit = sum_sqsum(i);

        // If sum of digits and sum of
        // square of digit both are
        // prime then increment the count
        if (prime[digit.first]
            && prime[digit.second]) {
            cnt += 1;
        }
    }

    return cnt;
}

// Driver Code
int main()
{

    int L = 10;
    int R = 20;

    cout << countnumber(L, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Sieve of prime numbers
static void primesieve(boolean []prime)
{
    // Sieve to store whether a
    // number is prime or not in
    // O(nlog(log(n)))
    prime[1] = false;

    for (int p = 2; p * p <= 650; p++)
    {
        if (prime[p] == true)
        {
            for (int i = p * 2; i <= 650; i += p)
                prime[i] = false;
        }
    }
}

// Function to return sum of digit
// and sum of square of digit
static pair sum_sqsum(int n)
{
    int sum = 0;
    int sqsum = 0;
    int x;

    // Until number is not
    // zero
    while (n > 0)
    {
        x = n % 10;
        sum += x;
        sqsum += x * x;
        n /= 10;
    }
    return (new pair(sum, sqsum));
}

// Function to return the count
// of number form L to R
// whose sum of digits and
// sum of square of digits
// are prime
static int countnumber(int L, int R)
{
    boolean []prime = new boolean[651];

    Arrays.fill(prime, true);
    primesieve(prime);

    int cnt = 0;

    // Iterate for each value
    // in the range of L to R
    for (int i = L; i <= R; i++)
    {

        // digit.first stores sum of digits
        // digit.second stores sum of
        // square of digit
        pair digit = sum_sqsum(i);

        // If sum of digits and sum of
        // square of digit both are
        // prime then increment the count
        if (prime[digit.first] &&
            prime[digit.second])
        {
            cnt += 1;
        }
    }
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int L = 10;
    int R = 20;

    System.out.println(countnumber(L, R));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Sieve of prime numbers
def primesieve(prime) :

    # Sieve to store whether a
    # number is prime or not in
    # O(nlog(log(n)))
    prime[1] = False;

    for p in range(2, int(sqrt(650)) + 1) :
        if (prime[p] == True) :
            for i in range(p * 2, 651, p) :
                prime[i] = False;

# Function to return sum of digit
# and sum of square of digit
def sum_sqsum(n) :

    sum = 0;
    sqsum = 0;

    # Until number is not
    # zero
    while (n) :
        x = n % 10;
        sum += x;
        sqsum += x * x;
        n //= 10;

    return (sum, sqsum);

# Function to return the count
# of number form L to R
# whose sum of digits and
# sum of square of digits
# are prime
def countnumber(L, R):

    prime = [True] * 651;

    primesieve(prime);

    cnt = 0;

    # Iterate for each value
    # in the range of L to R
    for i in range(L, R + 1) :

        # digit.first stores sum of digits
        # digit.second stores sum of
        # square of digit
        digit = sum_sqsum(i);

        # If sum of digits and sum of
        # square of digit both are
        # prime then increment the count
        if (prime[digit[0]] and prime[digit[1]]) :
            cnt += 1;

    return cnt;

# Driver Code
if __name__ == "__main__" :

    L = 10;
    R = 20;

    print(countnumber(L, R));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Sieve of prime numbers
static void primesieve(bool []prime)
{
    // Sieve to store whether a
    // number is prime or not in
    // O(nlog(log(n)))
    prime[1] = false;

    for (int p = 2; p * p <= 650; p++)
    {
        if (prime[p] == true)
        {
            for (int i = p * 2;
                     i <= 650; i += p)
                prime[i] = false;
        }
    }
}

// Function to return sum of digit
// and sum of square of digit
static pair sum_sqsum(int n)
{
    int sum = 0;
    int sqsum = 0;
    int x;

    // Until number is not
    // zero
    while (n > 0)
    {
        x = n % 10;
        sum += x;
        sqsum += x * x;
        n /= 10;
    }
    return (new pair(sum, sqsum));
}

// Function to return the count
// of number form L to R
// whose sum of digits and
// sum of square of digits
// are prime
static int countnumber(int L, int R)
{
    bool []prime = new bool[651];
    for (int i = 0; i < 651; i++)
        prime[i] = true;
    primesieve(prime);

    int cnt = 0;

    // Iterate for each value
    // in the range of L to R
    for (int i = L; i <= R; i++)
    {

        // digit.first stores sum of digits
        // digit.second stores sum of
        // square of digit
        pair digit = sum_sqsum(i);

        // If sum of digits and sum of
        // square of digit both are
        // prime then increment the count
        if (prime[digit.first] &&
            prime[digit.second])
        {
            cnt += 1;
        }
    }
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{
    int L = 10;
    int R = 20;

    Console.WriteLine(countnumber(L, R));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Sieve of prime numbers
function primesieve(prime) {

    // Sieve to store whether a
    // number is prime or not in
    // O(nlog(log(n)))
    prime[1] = false;

    for (let p = 2; p < Math.floor(Math.sqrt(650)) + 1; p++) {
        if (prime[p] == true) {
            for (let i = p * 2; i < 651; i += p) {
                prime[i] = false;
            }
        }
    }
}

// Function to return sum of digit
// and sum of square of digit
function sum_sqsum(n) {

    let sum = 0;
    let sqsum = 0;
    let x;
    // Until number is not
    // zero
    while (n) {
        x = n % 10;
        sum += x;
        sqsum += x * x;
        n = Math.floor(n / 10);
    }
    return [sum, sqsum];
}
// Function to return the count
// of number form L to R
// whose sum of digits and
// sum of square of digits
// are prime
function countnumber(L, R) {

    let prime = new Array(651).fill(true);

    primesieve(prime);

    let cnt = 0;

    // Iterate for each value
    // in the range of L to R
    for (let i = L; i <= R; i++) {

        // digit.first stores sum of digits
        // digit.second stores sum of
        // square of digit
        let digit = sum_sqsum(i);

        // If sum of digits and sum of
        // square of digit both are
        // prime then increment the count
        if (prime[digit[0]] && prime[digit[1]]) {
            cnt += 1;
        }
    }
    return cnt;
}

// Driver Code

let L = 10;
let R = 20;

document.write(countnumber(L, R));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4
```

**注:**

1.  将所有满足上述条件的数字存储在另一个数组中，用二分搜索法查找数组中有多少元素小于 **R** ，称 **cnt1** ，数组中有多少元素小于 **L** ，称 **cnt2** 。每次查询返回**CNT 1–CNT 2**
    **时间复杂度:** O(log(N)) 。
2.  我们可以使用前缀数组或 DP 方法，这样它就已经存储了从索引 0 到 I 的上述类型的好数量，并通过每个查询给出**DP[R]–DP[L-1]**
    **时间复杂度:** O(1) 来返回总计数。