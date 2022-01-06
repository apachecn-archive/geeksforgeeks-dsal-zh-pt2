# 计数不超过 N 的整数，这些整数是非除数且与 N 非互质

> 原文:[https://www . geesforgeks . org/整数计数-最多 n 个非除数-和-非互素-带-n/](https://www.geeksforgeeks.org/count-of-integers-up-to-n-which-are-non-divisors-and-non-coprime-with-n/)

给定一个整数 **N** ，任务是找出满足以下性质的小于 **N** 的所有可能整数的计数:

*   这个数与 **N** 不是互质的，即它们的 [**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 大于 1。
*   这个数不是 **N** 的除数。

**示例:**

> **输入:** N = 10
> **输出:** 3
> **解释:**
> 所有小于 10 且既不是除数也不是与 10 互素的可能整数都是{4，6，8}。
> 因此，所需计数为 3。
> **输入:** N = 42
> **输出:** 23

**方法:**
按照以下步骤解决问题:

*   设置**计数= N** 。
*   计算[欧拉全能性函数到 **N**](https://www.geeksforgeeks.org/eulers-totient-function-for-all-numbers-smaller-than-or-equal-to-n/) 的所有值，找出与 **N** 互素的**【1，N】**范围内的数的计数，即 [GCD(最大公约数)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)与 N 为 1 的数。
*   由于这些与 **N** 是互质的，所以从**计数**中减去它们。
*   使用厄拉多塞的**筛计算**N**T3[除数。从**计数**中减去它们。](https://www.geeksforgeeks.org/total-number-divisors-given-number/)**
*   打印**计数**的最终值，等于:

> **总计数= N–欧拉全数(N)–除数计数(N)**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of integers less than N
// satisfying given conditions
int count(int n)
{
    // Stores Euler counts
    int phi[n + 1] = { 0 };

    // Store Divisor counts
    int divs[n + 1] = { 0 };

    // Based on Sieve of Eratosthenes
    for (int i = 1; i <= n; i++) {

        phi[i] += i;

        // Update phi values of all
        // multiples of i
        for (int j = i * 2; j <= n; j += i)
            phi[j] -= phi[i];

        // Update count of divisors
        for (int j = i; j <= n; j += i)
            divs[j]++;
    }

    // Return the final count
    return (n - phi[n] - divs[n] + 1);
}

// Driver Code
int main()
{

    int N = 42;

    cout << count(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;

class GFG{

// Function to return the count
// of integers less than N
// satisfying given conditions
public static int count(int n)
{

    // Stores Euler counts
    int []phi = new int[n + 1];
    Arrays.fill(phi, 0);

    // Store Divisor counts
    int []divs = new int[n + 1];
    Arrays.fill(divs, 0);

    // Based on Sieve of Eratosthenes
    for(int i = 1; i <= n; i++)
    {
        phi[i] += i;

        // Update phi values of all
        // multiples of i
        for(int j = i * 2; j <= n; j += i)
            phi[j] -= phi[i];

        // Update count of divisors
        for(int j = i; j <= n; j += i)
            divs[j]++;
    }

    // Return the final count
    return (n - phi[n] - divs[n] + 1);
}

// Driver Code
public static void main(String []args)
{
    int N = 42;

    System.out.println(count(N));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return the count
# of integers less than N
# satisfying given conditions
def count(n):

    # Stores Euler counts
    phi = [0] * (n + 1)

    # Store Divisor counts
    divs = [0] * (n + 1)

    # Based on Sieve of Eratosthenes
    for i in range(1, n + 1):
        phi[i] += i

        # Update phi values of all
        # multiples of i
        for j in range(i * 2, n + 1, i):
            phi[j] -= phi[i];

        # Update count of divisors
        for j in range(i, n + 1, i):
            divs[j] += 1

    # Return the final count
    return (n - phi[n] - divs[n] + 1);

# Driver code
if __name__ == '__main__':

    N = 42

    print(count(N))

# This code is contributed by jana_sayantan
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return the count
// of integers less than N
// satisfying given conditions
public static int count(int n)
{

    // Stores Euler counts
    int []phi = new int[n + 1];

    // Store Divisor counts
    int []divs = new int[n + 1];

    // Based on Sieve of Eratosthenes
    for(int i = 1; i <= n; i++)
    {
        phi[i] += i;

        // Update phi values of all
        // multiples of i
        for(int j = i * 2; j <= n; j += i)
            phi[j] -= phi[i];

        // Update count of divisors
        for(int j = i; j <= n; j += i)
            divs[j]++;
    }

    // Return the final count
    return (n - phi[n] - divs[n] + 1);
}

// Driver Code
public static void Main(String []args)
{
    int N = 42;

    Console.WriteLine(count(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to return the count
// of integers less than N
// satisfying given conditions
function count(n)
{

    // Stores Euler counts
    let phi = [];

    // Store Divisor counts
    let divs = [];
    for(let i = 1; i <= n; i++)
    {
        phi[i] = 0;
        divs[i] = 0;
    }

    // Based on Sieve of Eratosthenes
    for(let i = 1; i <= n; i++)
    {
        phi[i] += i;

        // Update phi values of all
        // multiples of i
        for(let j = i * 2; j <= n; j += i)
            phi[j] -= phi[i];

        // Update count of divisors
        for(let j = i; j <= n; j += i)
            divs[j]++;
    }

    // Return the final count
    return (n - phi[n] - divs[n] + 1);
}

// Driver code

        let N = 42;
   document.write(count(N));

    // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
23
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*