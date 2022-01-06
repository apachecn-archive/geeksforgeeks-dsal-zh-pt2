# 最小化选择两个乘积为 X 的数字的成本

> 原文:[https://www . geeksforgeeks . org/最小化选择两个数字的成本-谁的产品是-x/](https://www.geeksforgeeks.org/minimize-the-cost-of-selecting-two-numbers-whose-product-is-x/)

**先决条件:** [求最大最小素数](https://www.geeksforgeeks.org/sum-of-maximum-and-minimum-prime-factor-of-every-number-in-the-array/)
给定四个整数 **A、B、C 和 X** ，任务是最小化选择两个数 **N** 和 **M** 的成本，使得 N 和 M 的乘积等于 X，即 **N * M = X** 。选择数字 N 和 M 的**成本**决定如下:

1.  对于第一个数字 N:
    *   如果 N 是质数，成本是 A。
    *   如果 N 是一个复合数，成本是 B。
    *   如果 N 为 1，成本为 C。
2.  对于第二个数字 M(！= 1)，成本为 M.

**例:**

> **输入:** A = 7，B = 11，C = 2，X = 20
> **输出:** 11
> **解释:**
> 以下是每对的可能值和成本:
> 设 N = 1 和 M = 20，选择 N 为 1 所用的成本为 C = 2，总成本= 2 + 20 = 22。
> 设 N = 2，M = 10，选择 N 为质数所用成本为 A = 7，总成本为 7 + 10 = 17
> 设 N = 4，M = 5，选择 N 为合成数所用成本为 B = 11，总成本为 11 + 5 = 15
> 设 N = 5，M = 4，选择 N 为质数所用成本为 A = 7， 总成本= 7 + 4 = 11
> 设 N = 10，M = 2，选择 N 作为合成数所用的成本为 B = 11，总成本= 11 + 2 = 13
> 以上所有中最小的为 11。
> **输入:** A = 1，B = 1，C = 1，X = 40
> **输出:** 3
> **说明:**
> 最小成本是当 N = 20 且 M = 2 时，总成本= 1 + 2 = 3。

**天真方法:** [找到数字](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)的所有因子，[检查因子是否为质数](https://www.geeksforgeeks.org/java-program-to-check-if-a-number-is-prime-or-not/)，据此找到成本并从中选择最小值。
**有效途径:**对于 **N** 可能有以下三种情况:

1.  **N 为质数:**那么第一个数字成本是固定的。为了最小化成本，选择可能的最高素数，使得 **N ≠ X** 。
2.  **N 是 Composite:** 类似于上面的情况，需要找到除以该数的最大复合数，而不是该数本身。为了做到这一点，找到除以 **X** 的最小素数，并将其视为 **M** ，然后计算成本。
3.  **N 为 1:** 对于这种情况可以形成任意数(X = 1 时除外)和 **M = X** 。

因此，想法是计算所有三种情况的成本，并找到其中的最小值。为了做到这一点，所有最小质因数和最大质因数的列表使用厄拉多塞的[筛的微小变化来预计算，并存储在数组中。所有三种情况的成本都可以从这些数组中轻松计算出来。
以下是上述办法的实施情况:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;

// max_prime[i] represents maximum prime
// number that divides the number i
int max_prime[MAX];

// min_prime[i] represents minimum prime
// number that divides the number i
int min_prime[MAX];

// Function to store the minimum
// prime factor and the maximum
// prime factor in two arrays
void sieve(int n)
{
    for (int i = 2; i <= n; ++i) {

        // Check for prime number
        // if min_prime[i] > 0,
        // then it is not a prime number
        if (min_prime[i] > 0) {
            continue;
        }

        // If i is a prime number,
        // then both minimum and maximum
        // prime numbers that divide
        // the number is the number itself
        min_prime[i] = i;
        max_prime[i] = i;

        int j = i + i;

        while (j <= n) {
            if (min_prime[j] == 0) {

                // If this number is being visited
                // for first time then this divisor
                // must be the smallest prime number
                // that divides this number
                min_prime[j] = i;
            }

            // Update prime number till the last
            // prime number that divides this number

            // The last prime number that
            // divides this number will be maximum.
            max_prime[j] = i;
            j += i;
        }
    }
}

// Function to minimize the cost of finding
// two numbers for every number such that
// the product of those two is equal to X
int findCost(int A, int B, int C, int X)
{
    // Pre-calculation
    sieve(MAX);

    int N, M;

    // If X == 1, then there is no way to
    // find N and M. Print -1
    if (X == 1) {
        return -1;
    }

    // Case 3 is always valid and cost for that
    // is C + X C for choosing 1 and M = X/1
    int min_cost = C + X;

    // Case 1
    // N is prime, first number cost is fixed
    // N is max_prime number divides this number
    int cost_for_prime = A;
    N = max_prime[X];

    // If X is prime then the maximum prime number
    // is the number itself. For this case,
    // M becomes 1 and this shouldn't be considered.
    if (N != X) {

        // Find M for this case
        M = X / N;

        // Add cost for the second number also
        cost_for_prime += M;

        // Update min_cost, if the
        // cost for prime is minimum
        min_cost = min(min_cost, cost_for_prime);
    }

    // Case 2
    // If N is composite
    // For this find the minimum prime number
    // that divides A[i] and consider this as M
    M = min_prime[X];

    // Find N for that number
    N = X / M;

    // Check if this number is composite or not
    // if N is prime then there is no way
    // to find any composite number that divides X
    // If N = min_prime[N] then N is prime
    if (N != min_prime[N]) {
        int cost_for_comp = B + M;

        // Update min_cost, if the
        // cost for the composite is minimum
        min_cost = min(min_cost, cost_for_comp);
    }

    return min_cost;
}

// Driver code
int main()
{
    int A = 7, B = 11, C = 2, X = 20;

    cout << findCost(A, B, C, X) << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    static final int MAX = 1000;

    // max_prime[i] represents maximum prime
    // number that divides the number i
    static int max_prime[] = new int[MAX];

    // min_prime[i] represents minimum prime
    // number that divides the number i
    static int min_prime[] = new int[MAX];

    // Function to store the minimum
    // prime factor and the maximum
    // prime factor in two arrays
    static void sieve(int n)
    {
        for (int i = 2; i < n; ++i) {

            // Check for prime number
            // if min_prime[i] > 0,
            // then it is not a prime number
            if (min_prime[i] > 0) {
                continue;
            }

            // If i is a prime number,
            // then both minimum and maximum
            // prime numbers that divide
            // the number is the number itself
            min_prime[i] = i;
            max_prime[i] = i;

            int j = i + i;

            while (j < n) {
                if (min_prime[j] == 0) {

                    // If this number is being visited
                    // for first time then this divisor
                    // must be the smallest prime number
                    // that divides this number
                    min_prime[j] = i;
                }

                // Update prime number till the last
                // prime number that divides this number

                // The last prime number that
                // divides this number will be maximum.
                max_prime[j] = i;
                j += i;
            }
        }
    }

    // Function to minimize the cost of finding
    // two numbers for every number such that
    // the product of those two is equal to X
    static int findCost(int A, int B, int C, int X)
    {
        // Pre-calculation
        sieve(MAX);

        int N, M;

        // If X == 1, then there is no way to
        // find N and M. Print -1
        if (X == 1) {
            return -1;
        }

        // Case 3 is always valid and cost for that
        // is C + X C for choosing 1 and M = X/1
        int min_cost = C + X;

        // Case 1
        // N is prime, first number cost is fixed
        // N is max_prime number divides this number
        int cost_for_prime = A;
        N = max_prime[X];

        // If X is prime then the maximum prime number
        // is the number itself. For this case,
        // M becomes 1 and this shouldn't be considered.
        if (N != X) {

            // Find M for this case
            M = X / N;

            // Add cost for the second number also
            cost_for_prime += M;

            // Update min_cost, if the
            // cost for prime is minimum
            min_cost = Math.min(min_cost, cost_for_prime);
        }

        // Case 2
        // If N is composite
        // For this find the minimum prime number
        // that divides A[i] and consider this as M
        M = min_prime[X];

        // Find N for that number
        N = X / M;

        // Check if this number is composite or not
        // if N is prime then there is no way
        // to find any composite number that divides X
        // If N = min_prime[N] then N is prime
        if (N != min_prime[N]) {
            int cost_for_comp = B + M;

            // Update min_cost, if the
            // cost for the composite is minimum
            min_cost = Math.min(min_cost, cost_for_comp);
        }

        return min_cost;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A = 7, B = 11, C = 2, X = 20;

        System.out.println(findCost(A, B, C, X));
    }

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

MAX = 10000;

# max_prime[i] represents maximum prime
# number that divides the number i
max_prime = [0]*MAX;

# min_prime[i] represents minimum prime
# number that divides the number i
min_prime = [0]*MAX;

# Function to store the minimum
# prime factor and the maximum
# prime factor in two arrays
def sieve(n) :

    for i in range(2, n) :

        # Check for prime number
        # if min_prime[i] > 0,
        # then it is not a prime number
        if (min_prime[i] > 0) :
            continue;

        # If i is a prime number,
        # then both minimum and maximum
        # prime numbers that divide
        # the number is the number itself
        min_prime[i] = i;
        max_prime[i] = i;

        j = i + i;

        while (j < n) :
            if (min_prime[j] == 0) :

                # If this number is being visited
                # for first time then this divisor
                # must be the smallest prime number
                # that divides this number
                min_prime[j] = i;

            # Update prime number till the last
            # prime number that divides this number

            # The last prime number that
            # divides this number will be maximum.
            max_prime[j] = i;
            j += i;

# Function to minimize the cost of finding
# two numbers for every number such that
# the product of those two is equal to X
def findCost(A, B, C, X) :

    # Pre-calculation
    sieve(MAX);

    # If X == 1, then there is no way to
    # find N and M. Print -1
    if (X == 1) :
        return -1;

    # Case 3 is always valid and cost for that
    # is C + X C for choosing 1 and M = X/1
    min_cost = C + X;

    # Case 1
    # N is prime, first number cost is fixed
    # N is max_prime number divides this number
    cost_for_prime = A;
    N = max_prime[X];

    # If X is prime then the maximum prime number
    # is the number itself. For this case,
    # M becomes 1 and this shouldn't be considered.
    if (N != X) :

        # Find M for this case
        M = X // N;

        # Add cost for the second number also
        cost_for_prime += M;

        # Update min_cost, if the
        # cost for prime is minimum
        min_cost = min(min_cost, cost_for_prime);

    # Case 2
    # If N is composite
    # For this find the minimum prime number
    # that divides A[i] and consider this as M
    M = min_prime[X];

    # Find N for that number
    N = X // M;

    # Check if this number is composite or not
    # if N is prime then there is no way
    # to find any composite number that divides X
    # If N = min_prime[N] then N is prime
    if (N != min_prime[N]) :
        cost_for_comp = B + M;

        # Update min_cost, if the
        # cost for the composite is minimum
        min_cost = min(min_cost, cost_for_comp);

    return min_cost;

# Driver code
if __name__ == "__main__" :

    A = 7; B = 11; C = 2; X = 20;

    print(findCost(A, B, C, X)) ;

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    static int MAX = 1000;

    // max_prime[i] represents maximum prime
    // number that divides the number i
    static int []max_prime = new int[MAX];

    // min_prime[i] represents minimum prime
    // number that divides the number i
    static int []min_prime = new int[MAX];

    // Function to store the minimum
    // prime factor and the maximum
    // prime factor in two arrays
    static void sieve(int n)
    {
        for (int i = 2; i < n; ++i) {

            // Check for prime number
            // if min_prime[i] > 0,
            // then it is not a prime number
            if (min_prime[i] > 0) {
                continue;
            }

            // If i is a prime number,
            // then both minimum and maximum
            // prime numbers that divide
            // the number is the number itself
            min_prime[i] = i;
            max_prime[i] = i;

            int j = i + i;

            while (j < n) {
                if (min_prime[j] == 0) {

                    // If this number is being visited
                    // for first time then this divisor
                    // must be the smallest prime number
                    // that divides this number
                    min_prime[j] = i;
                }

                // Update prime number till the last
                // prime number that divides this number

                // The last prime number that
                // divides this number will be maximum.
                max_prime[j] = i;
                j += i;
            }
        }
    }

    // Function to minimize the cost of finding
    // two numbers for every number such that
    // the product of those two is equal to X
    static int findCost(int A, int B, int C, int X)
    {
        // Pre-calculation
        sieve(MAX);

        int N, M;

        // If X == 1, then there is no way to
        // find N and M. Print -1
        if (X == 1) {
            return -1;
        }

        // Case 3 is always valid and cost for that
        // is C + X C for choosing 1 and M = X/1
        int min_cost = C + X;

        // Case 1
        // N is prime, first number cost is fixed
        // N is max_prime number divides this number
        int cost_for_prime = A;
        N = max_prime[X];

        // If X is prime then the maximum prime number
        // is the number itself. For this case,
        // M becomes 1 and this shouldn't be considered.
        if (N != X) {

            // Find M for this case
            M = X / N;

            // Add cost for the second number also
            cost_for_prime += M;

            // Update min_cost, if the
            // cost for prime is minimum
            min_cost = Math.Min(min_cost, cost_for_prime);
        }

        // Case 2
        // If N is composite
        // For this find the minimum prime number
        // that divides A[i] and consider this as M
        M = min_prime[X];

        // Find N for that number
        N = X / M;

        // Check if this number is composite or not
        // if N is prime then there is no way
        // to find any composite number that divides X
        // If N = min_prime[N] then N is prime
        if (N != min_prime[N]) {
            int cost_for_comp = B + M;

            // Update min_cost, if the
            // cost for the composite is minimum
            min_cost = Math.Min(min_cost, cost_for_comp);
        }

        return min_cost;
    }

    // Driver code
    public static void Main (string[] args)
    {
        int A = 7, B = 11, C = 2, X = 20;

        Console.WriteLine(findCost(A, B, C, X));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let MAX = 1000;

    // max_prime[i] represents maximum prime
    // number that divides the number i
    let max_prime = Array.from({length: MAX}, (_, i) => 0);

    // min_prime[i] represents minimum prime
    // number that divides the number i
    let min_prime = Array.from({length: MAX}, (_, i) => 0);

    // Function to store the minimum
    // prime factor and the maximum
    // prime factor in two arrays
    function sieve(n)
    {
        for (let i = 2; i < n; ++i) {

            // Check for prime number
            // if min_prime[i] > 0,
            // then it is not a prime number
            if (min_prime[i] > 0) {
                continue;
            }

            // If i is a prime number,
            // then both minimum and maximum
            // prime numbers that divide
            // the number is the number itself
            min_prime[i] = i;
            max_prime[i] = i;

            let j = i + i;

            while (j < n) {
                if (min_prime[j] == 0) {

                    // If this number is being visited
                    // for first time then this divisor
                    // must be the smallest prime number
                    // that divides this number
                    min_prime[j] = i;
                }

                // Update prime number till the last
                // prime number that divides this number

                // The last prime number that
                // divides this number will be maximum.
                max_prime[j] = i;
                j += i;
            }
        }
    }

    // Function to minimize the cost of finding
    // two numbers for every number such that
    // the product of those two is equal to X
    function findCost(A, B, C, X)
    {
        // Pre-calculation
        sieve(MAX);

        let N, M;

        // If X == 1, then there is no way to
        // find N and M. Prlet -1
        if (X == 1) {
            return -1;
        }

        // Case 3 is always valid and cost for that
        // is C + X C for choosing 1 and M = X/1
        let min_cost = C + X;

        // Case 1
        // N is prime, first number cost is fixed
        // N is max_prime number divides this number
        let cost_for_prime = A;
        N = max_prime[X];

        // If X is prime then the maximum prime number
        // is the number itself. For this case,
        // M becomes 1 and this shouldn't be considered.
        if (N != X) {

            // Find M for this case
            M = X / N;

            // Add cost for the second number also
            cost_for_prime += M;

            // Update min_cost, if the
            // cost for prime is minimum
            min_cost = Math.min(min_cost, cost_for_prime);
        }

        // Case 2
        // If N is composite
        // For this find the minimum prime number
        // that divides A[i] and consider this as M
        M = min_prime[X];

        // Find N for that number
        N = X / M;

        // Check if this number is composite or not
        // if N is prime then there is no way
        // to find any composite number that divides X
        // If N = min_prime[N] then N is prime
        if (N != min_prime[N]) {
            let cost_for_comp = B + M;

            // Update min_cost, if the
            // cost for the composite is minimum
            min_cost = Math.min(min_cost, cost_for_comp);
        }

        return min_cost;
    }

// Driver Code

    let A = 7, B = 11, C = 2, X = 20;

    document.write(findCost(A, B, C, X));

</script>
```

**Output:** 

```
11
```

时间复杂度:O(MAX) <sup>2</sup>

辅助空间:0(最大)