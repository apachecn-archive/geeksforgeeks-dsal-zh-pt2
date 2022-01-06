# 计算多达 N 个正好有 5 个除数的数

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-having-just-5-dividers/](https://www.geeksforgeeks.org/count-numbers-up-to-n-having-exactly-5-divisors/)

给定一个正整数 **N** ，任务是从正好有 5 个[因子](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)的范围**【1，N】**中计算整数的个数。

**示例:**

> **输入:** N = 18
> **输出:** 1
> **解释:**
> 在[1，18]范围内的所有整数中，16 是唯一正好有 5 个除数的整数，即 1，2，8，4 和 16。
> 因此，此类整数的计数为 1。
> 
> **输入:**N = 100
> T3】输出: 2

**天真方法:**解决给定问题的最简单方法是迭代范围**【1，N】**并计算此范围内除数为的那些整数[计数为 **5** 。
***时间复杂度:**O(N<sup>4/3</sup>)*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/count-divisors-n-on13/)

**高效法:**上述方法也可以通过观察一个事实进行优化，即精确具有 **5 个除数的数**可以用**p<sup>4</sup>T7】的形式表示，其中 **p** 是一个[质数](https://www.geeksforgeeks.org/prime-numbers/)作为除数的计数精确为 **5** 。按照以下步骤解决问题:**

*   [使用厄拉多塞](https://www.geeksforgeeks.org/print-all-prime-numbers-less-than-or-equal-to-n/)的[筛生成所有素数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)使其四次方小于**10<sup>18</sup>T5，并存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，比如 **A[]** 。**
*   初始化两个变量，说**低**为 **0** 和**高**为**a . size()–1**。
*   为了执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)迭代直到**低**小于**高**并执行以下步骤:
    *   求**中间**的值为**(低+高)/2** 。
    *   在指数**中间** **(中间–1)**找到元素的四次幂的值，并将其存储在变量中，分别表示**当前**和**先前**。
    *   如果**当前**的值为 **N** ，则打印 **A【中】**的值作为结果。
    *   如果**当前**的值大于**N****先前**最多为**N**，则打印 **A【中】**的值作为结果。
    *   如果**电流**的值大于 **N** ，则将**高**的值更新为**(中间–1)**。否则，将**低位**的值更新为**(中+ 1)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define ll long long int
const int MAX = 1e5;
using namespace std;

// Function to calculate the value of
// (x^y) using binary exponentiation
ll power(ll x, unsigned ll y)
{
    // Stores the value of x^y
    ll res = 1;

    // Base Case
    if (x == 0)
        return 0;

    while (y > 0) {

        // If y is odd multiply
        // x with result
        if (y & 1)
            res = (res * x);

        // Otherwise, divide y by 2
        y = y >> 1;

        x = (x * x);
    }
    return res;
}

// Function to perform the Sieve Of
// Eratosthenes to find the prime
// number over the range [1, 10^5]
void SieveOfEratosthenes(
    vector<pair<ll, ll> >& v)
{
    bool prime[MAX + 1];

    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed
        // then it is a prime
        if (prime[p] == true) {

            // Set all the multiples of
            // p to non-prime
            for (int i = p * 2;
                 i <= MAX; i += p)
                prime[i] = false;
        }
    }

    int num = 1;

    // Iterate over the range [1, MAX]
    for (int i = 1; i <= MAX; i++) {

        // Store all the prime number
        if (prime[i]) {
            v.push_back({ i, num });
            num++;
        }
    }
}

// Function to find the primes having
// only 5 divisors
int countIntegers(ll n)
{
    // Base Case
    if (n < 16) {
        return 0;
    }

    // First value of the pair has the
    // prime number and the second value
    // has the count of primes till that
    // prime numbers
    vector<pair<ll, ll> > v;

    // Precomputing all the primes
    SieveOfEratosthenes(v);

    int low = 0;
    int high = v.size() - 1;

    // Perform the Binary search
    while (low <= high) {

        int mid = (low + high) / 2;

        // Calculate the fourth power of
        // the curr and prev
        ll curr = power(v[mid].first, 4);
        ll prev = power(v[mid - 1].first, 4);

        if (curr == n) {

            // Return value of mid
            return v[mid].second;
        }

        else if (curr > n and prev <= n) {

            // Return value of mid-1
            return v[mid - 1].second;
        }
        else if (curr > n) {

            // Update the value of high
            high = mid - 1;
        }

        else {

            // Update the value of low
            low = mid + 1;
        }
    }
    return 0;
}

// Driver Code
int main()
{
    ll N = 100;
    cout << countIntegers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Vector;

public class GFG {
    static int MAX = (int)1e5;

    public static class pair {
        long first;
        long second;
        pair(long first, long second)
        {
            this.first = first;
            this.second = second;
        }
    }
    // Function to calculate the value of
    // (x^y) using binary exponentiation
    static long power(long x, long y)
    {

        // Stores the value of x^y
        long res = 1;

        // Base Case
        if (x == 0)
            return 0;

        while (y > 0)
        {

            // If y is odd multiply
            // x with result
            if ((y & 1) == 1)
                res = (res * x);

            // Otherwise, divide y by 2
            y = y >> 1;

            x = (x * x);
        }
        return res;
    }

    // Function to perform the Sieve Of
    // Eratosthenes to find the prime
    // number over the range [1, 10^5]
    static void SieveOfEratosthenes(Vector<pair> v)
    {
        boolean prime[] = new boolean[MAX + 1];

        for (int i = 0; i < prime.length; i++) {
            prime[i] = true;
        }

        prime[1] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed
            // then it is a prime
            if (prime[p] == true) {

                // Set all the multiples of
                // p to non-prime
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }

        int num = 1;

        // Iterate over the range [1, MAX]
        for (int i = 1; i <= MAX; i++) {

            // Store all the prime number
            if (prime[i]) {
                v.add(new pair(i, num));
                num++;
            }
        }
    }

    // Function to find the primes having
    // only 5 divisors
    static long countIntegers(long n)
    {
        // Base Case
        if (n < 16) {
            return 0;
        }

        // First value of the pair has the
        // prime number and the second value
        // has the count of primes till that
        // prime numbers
        Vector<pair> v = new Vector<>();

        // Precomputing all the primes
        SieveOfEratosthenes(v);

        int low = 0;
        int high = v.size() - 1;

        // Perform the Binary search
        while (low <= high) {

            int mid = (low + high) / 2;

            // Calculate the fourth power of
            // the curr and prev
            long curr = power(v.get(mid).first, 4);
            long prev = power(v.get(mid - 1).first, 4);

            if (curr == n) {

                // Return value of mid
                return v.get(mid).second;
            }

            else if (curr > n && prev <= n) {

                // Return value of mid-1
                return v.get(mid - 1).second;
            }
            else if (curr > n) {

                // Update the value of high
                high = mid - 1;
            }

            else {

                // Update the value of low
                low = mid + 1;
            }
        }
        return 0;
    }

    // Driver code
    public static void main(String[] args)
    {
        long N = 100;
        System.out.println(countIntegers(N));
    }
}

// This code is contributed by abhinavjain194
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*