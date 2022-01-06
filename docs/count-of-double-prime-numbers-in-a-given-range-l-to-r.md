# 给定范围 L 到 R 内双素数的计数

> 原文:[https://www . geesforgeks . org/给定范围内的双素数计数-l 到-r/](https://www.geeksforgeeks.org/count-of-double-prime-numbers-in-a-given-range-l-to-r/)

给定**两个整数 L 和 R** ，任务是找出范围内双素数的个数。

> 当 1 到 N **(不含 1，含 N)** 范围内的素数个数也是素数时，一个数 N 称为**双素数**。

**例:**

> **输入:** L = 3，R = 10
> **输出:** 4
> **解释:**
> 对于 3，我们有范围 1，2，3，素数计数为 2(也是素数)
> 对于 4，我们有范围 1，2，3，4，素数计数为 2(也是素数)
> 对于 5，我们有范围 1，2，3，4，5， 而素数的计数是 3(也是素数)
> 对于 6，我们有 1，2，3，4，5，6 的范围，素数的计数是 3(也是素数)
> 对于 7，我们有 1，2，3，4，5，6，7 的范围，素数的计数是 4，这是非素数。
> 类似于 R = 10 之前的其他数，素数的计数是非素数。因此双素数的计数是 4。
> **输入:** L = 4，R = 12
> **输出:** 5
> **说明:**
> 给定范围内共有 5 个双素数。

**方法:**
为了解决上面提到的问题，我们将使用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的概念来生成素数。

*   生成 0 到 10 <sup>6</sup> 的所有素数，并存储在数组中。
*   初始化一个变量*计数*来跟踪从 1 到某个位置的素数。
*   然后，对于每个素数，我们将增加计数，并设置 dp[count] = 1(其中 dp 是存储双素数的数组)，指示从 1 到某个第 I 个位置的素数。
*   最后求 dp 数组的累计和，这样答案就是**DP[R]–DP[L–1]**。

以下是上述方法的实现:

## C++

```
// C++ program to find the count
// of Double Prime numbers
// in the range L to R

#include <bits/stdc++.h>
using namespace std;

// Array to make Sieve
// where arr[i]=0 indicates
// non prime and arr[i] = 1
// indicates prime
int arr[1000001];

// Array to find double prime
int dp[1000001];

// Function to find the number
// double prime numbers in range
void count()
{
    int maxN = 1000000, i, j;

    // Assume all numbers as prime
    for (i = 0; i < maxN; i++)
        arr[i] = 1;

    arr[0] = 0;
    arr[1] = 0;

    for (i = 2; i * i <= maxN; i++) {

        // Check if the number is prime
        if (arr[i] == 1) {

            // check for multiples of i
            for (j = 2 * i; j <= maxN; j += i) {

                // Make all multiples of
                // ith prime as non-prime
                arr[j] = 0;
            }
        }
    }

    int cnt = 0;

    for (i = 0; i <= maxN; i++) {
        // Check if number at ith position
        // is prime then increment count
        if (arr[i] == 1)
            cnt++;

        if (arr[cnt] == 1)

            // Indicates count of numbers
            // from 1 to i that are
            // also prime and
            // hence double prime
            dp[i] = 1;

        else
            // If number is not a double prime
            dp[i] = 0;
    }
    for (i = 1; i <= maxN; i++)
        // finding cumulative sum
        dp[i] += dp[i - 1];
}

// Driver code
int main()
{
    int L = 4, R = 12;
    count();
    cout << dp[R] - dp[L - 1];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of Double Prime numbers
// in the range L to R
import java.util.*;
import java.lang.*;
class GFG{

// Array to make Sieve
// where arr[i]=0 indicates
// non prime and arr[i] = 1
// indicates prime
static int[] arr = new int[1000001];

// Array to find double prime
static int[] dp = new int[1000001];

// Function to find the number
// double prime numbers in range
static void count()
{
    int maxN = 1000000, i, j;

    // Assume all numbers as prime
    for (i = 0; i < maxN; i++)
        arr[i] = 1;

    arr[0] = 0;
    arr[1] = 0;

    for (i = 2; i * i <= maxN; i++)
    {

        // Check if the number is prime
        if (arr[i] == 1)
        {

            // check for multiples of i
            for (j = 2 * i; j <= maxN; j += i)
            {

                // Make all multiples of
                // ith prime as non-prime
                arr[j] = 0;
            }
        }
    }

    int cnt = 0;

    for (i = 0; i <= maxN; i++)
    {
        // Check if number at ith position
        // is prime then increment count
        if (arr[i] == 1)
            cnt++;

        if (arr[cnt] == 1)

            // Indicates count of numbers
            // from 1 to i that are
            // also prime and
            // hence double prime
            dp[i] = 1;

        else
            // If number is not a double prime
            dp[i] = 0;
    }

    for (i = 1; i <= maxN; i++)

        // finding cumulative sum
        dp[i] += dp[i - 1];
}

// Driver code
public static void main(String[] args)
{
    int L = 4, R = 12;
    count();
    System.out.println(dp[R] - dp[L - 1]);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the count
# of Double Prime numbers
# in the range L to R

# Array to make Sieve
# where arr[i]=0 indicates
# non prime and arr[i] = 1
# indicates prime
arr = [0] * 1000001

# Array to find double prime
dp = [0] * 1000001

# Function to find the number
# double prime numbers in range
def count():

    maxN = 1000000

    # Assume all numbers as prime
    for i in range(0, maxN):
        arr[i] = 1

    arr[0] = 0
    arr[1] = 0

    i = 2
    while(i * i <= maxN):

        # Check if the number is prime
        if (arr[i] == 1):

            # Check for multiples of i
            for j in range(2 * i, maxN + 1, i):

                # Make all multiples of
                # ith prime as non-prime
                arr[j] = 0

        i += 1

    cnt = 0

    for i in range(0, maxN + 1):

        # Check if number at ith position
        # is prime then increment count
        if (arr[i] == 1):
            cnt += 1

        if (arr[cnt] == 1):

            # Indicates count of numbers
            # from 1 to i that are
            # also prime and
            # hence double prime
            dp[i] = 1

        else:

            # If number is not a double prime
            dp[i] = 0

    for i in range(0, maxN + 1):

        # Finding cumulative sum
        dp[i] += dp[i - 1]

# Driver code
L = 4
R = 12

count()

print(dp[R] - dp[L - 1])

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to find the count
// of Double Prime numbers
// in the range L to R
using System;
class GFG{

// Array to make Sieve
// where arr[i]=0 indicates
// non prime and arr[i] = 1
// indicates prime
static int[] arr = new int[1000001];

// Array to find double prime
static int[] dp = new int[1000001];

// Function to find the number
// double prime numbers in range
static void count()
{
    int maxN = 1000000, i, j;

    // Assume all numbers as prime
    for (i = 0; i < maxN; i++)
        arr[i] = 1;

    arr[0] = 0;
    arr[1] = 0;

    for (i = 2; i * i <= maxN; i++)
    {

        // Check if the number is prime
        if (arr[i] == 1)
        {

            // check for multiples of i
            for (j = 2 * i; j <= maxN; j += i)
            {

                // Make all multiples of
                // ith prime as non-prime
                arr[j] = 0;
            }
        }
    }

    int cnt = 0;

    for (i = 0; i <= maxN; i++)
    {
        // Check if number at ith position
        // is prime then increment count
        if (arr[i] == 1)
            cnt++;

        if (arr[cnt] == 1)

            // Indicates count of numbers
            // from 1 to i that are
            // also prime and
            // hence double prime
            dp[i] = 1;

        else
            // If number is not a double prime
            dp[i] = 0;
    }

    for (i = 1; i <= maxN; i++)

        // finding cumulative sum
        dp[i] += dp[i - 1];
}

// Driver code
public static void Main()
{
    int L = 4, R = 12;
    count();
    Console.Write(dp[R] - dp[L - 1]);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find the count
// of Double Prime numbers
// in the range L to R

// Array to make Sieve
// where arr[i]=0 indicates
// non prime and arr[i] = 1
// indicates prime
let arr = [];

// Array to find double prime
let dp = [];

// Function to find the number
// double prime numbers in range
function count()
{
    let maxN = 1000000, i, j;

    // Assume all numbers as prime
    for (i = 0; i < maxN; i++)
        arr[i] = 1;

    arr[0] = 0;
    arr[1] = 0;

    for (i = 2; i * i <= maxN; i++)
    {

        // Check if the number is prime
        if (arr[i] == 1)
        {

            // check for multiples of i
            for (j = 2 * i; j <= maxN; j += i)
            {

                // Make all multiples of
                // ith prime as non-prime
                arr[j] = 0;
            }
        }
    }

    let cnt = 0;

    for (i = 0; i <= maxN; i++)
    {
        // Check if number at ith position
        // is prime then increment count
        if (arr[i] == 1)
            cnt++;

        if (arr[cnt] == 1)

            // Indicates count of numbers
            // from 1 to i that are
            // also prime and
            // hence double prime
            dp[i] = 1;

        else
            // If number is not a double prime
            dp[i] = 0;
    }

    for (i = 1; i <= maxN; i++)

        // finding cumulative sum
        dp[i] += dp[i - 1];
}

// Driver code

    let L = 4, R = 12;
    count();
    document.write(dp[R] - dp[L - 1]);

   // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
5
```