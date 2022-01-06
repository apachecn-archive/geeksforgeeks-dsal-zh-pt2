# 计数最多 N 个的数字，其与 N 的 GCD 小于该数字

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-what-gcd-with-n-小于该数字/](https://www.geeksforgeeks.org/count-numbers-up-to-n-whose-gcd-with-n-is-less-than-that-number/)

给定一个整数 **N** ，任务是统计 **K** ( *其中 **1 ≤ K≤ N*** )的值，使得**1<**[**GCD**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)**(K，N) < K** 。

**示例:**

> **输入:** N = 10
> **输出:** 3
> **说明:**满足给定条件的 K 值为:
> 
> *   K = 4，gcd(4，10) = 2
> *   K = 6，gcd(6，10) = 2
> *   K = 8，gcd(8，10) = 2
> 
> **输入:** N = 15
> **输出:** 4
> **说明:**满足给定条件的 K 值为:
> 
> *   K = 6，gcd(6，15) = 3
> *   K = 9，gcd(9，15) = 3
> *   K = 10，gcd(10，15) = 5
> *   K = 12，gcd(12，15) = 3

**天真法:**最简单的方法是迭代范围**【1，N】**，检查每个数字是否满足给定条件。最后，打印此类数字的计数。

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*

**高效途径:**思路是找出**【1，N】**范围内的所有数字，其中 **gcd(K，N) = 1** 和 **gcd(K，N) = K** 然后最后从 **N** 中去掉所有这些数字得到最终答案。按照以下步骤解决问题:

*   使用厄拉多塞 [**筛子储存 **N** 的所有质因数。**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   将**【1，N】**范围内所有数字的计数存储在变量**计数 1** 中，其中 **gcd(N，K) = K** 。
*   使用[**欧拉全图函数**](https://www.geeksforgeeks.org/eulers-totient-function/#:~:text=Euler's%20Totient%20function%20%CE%A6%20(n, 2%2C%202)%20is%202.) 将 **gcd(N，K) = 1 的范围内的所有数字的计数存储在变量 **count2** 中。**
*   通过将**和**更新为**N –(计数 1 +计数 2)** ，将这些数字从 **N** 中删除。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Store the all prime numbers
// using Sieve of Eratosthenes
const int MAXN = 100001;
vector<int> spf;

// Function to fill the prime numbers
// using Sieve of Erastosthenes
void sieve()
{
    // Create a boolean array and
    // initialize all entries it as 0
    int p[MAXN + 1] = { 0 };

    p[2] = 1;
    for (long long int i = 3; i < MAXN; i += 2) {
        p[i] = 1;
    }

    // Push the first prime number
    spf.push_back(2);

    for (long long i = 3; i < MAXN; i += 2) {

        // If the current number is prime
        if (p[i]) {

            // Store the prime numbers
            // in spf which is prime
            spf.push_back(i);

            // Mark all its multiples as false
            for (long long int j = i * i; j < MAXN;
                 j += 2 * i)
                p[j] = 0;
        }
    }
}

// Function to count the values of K where
// 1≤K≤N such that 1< gcd(K, N) < K
void countK(int N)
{
    // Precalculate prime numbers
    sieve();
    int N1 = N;

    // Store the smallest prime number
    int div = spf[0];

    int index = 1, C = 0;

    // Store the count of those numbers in the
    // range [1, N] for which gcd(N, K) = K
    int count1 = 1;

    // Store the count of those numbers from
    // the range [1, N] such that gcd(N, K) = 1
    float count2 = N;

    // Iterate through all prime factors of N
    while (div * div <= N) {
        if (N % div == 0) {
            C = 0;
            while (N % div == 0) {
                N /= div;
                C++;
            }

            count1 = count1 * (C + 1);

            // count2 is determined by
            // Euler's Totient Function
            count2 *= (1.0 - (1.0 / (float)div));
        }

        div = spf[index];

        index++;
    }
    if (N != 1) {

        count1 *= 2;
        count2 = count2 * (1.0 - (1.0 / (float)N));
    }

    int ans = N1 - count1 - count2;

    // Add 1 to result as 1 is contributed
    // twice due to count1 and count2
    ans = ans + 1;

    // Print the result
    cout << ans;

    return;
}

// Driver Code
int main()
{
    // Given Input
    int N = 10;

    // Function Call
    countK(N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Store the all prime numbers
# using Sieve of Eratosthenes
MAXN = 100001
spf = []

# Function to fill the prime numbers
# using Sieve of Erastosthenes
def sieve():

    global MAXN

    # Create a boolean array and
    # initialize all entries it as 0
    p = [0] * (MAXN + 1)
    p[2] = 1

    for i in range(3, MAXN, 2):
        p[i] = 1

    # Push the first prime number
    spf.append(2)

    for i in range(3, MAXN, 2):

        # If the current number is prime
        if (p[i]):

            # Store the prime numbers
            # in spf which is prime
            spf.append(i)

            # Mark all its multiples as false
            for j in range(i * i, MAXN, 2 * i):
                p[j] = 0

# Function to count the values of K where
# 1≤K≤N such that 1< gcd(K, N) < K
def countK(N):

    # Precalculate prime numbers
    sieve()
    N1 = N

    # Store the smallest prime number
    div = spf[0]

    index, C = 1, 0

    # Store the count of those numbers in the
    # range [1, N] for which gcd(N, K) = K
    count1 = 1

    # Store the count of those numbers from
    # the range [1, N] such that gcd(N, K) = 1
    count2 = N

    # Iterate through all prime factors of N
    while (div * div <= N):
        if (N % div == 0):
            C = 0

            while (N % div == 0):
                N //= div
                C += 1

            count1 = count1 * (C + 1)

            # count2 is determined by
            # Euler's Totient Function
            count2 *= (1.0 - (1.0 / div))

        div = spf[index]

        index += 1

    if (N != 1):
        count1 *= 2
        count2 = count2 * (1.0 - (1.0 / N))

    ans = N1 - count1 - count2

    # Add 1 to result as 1 is contributed
    # twice due to count1 and count2
    ans = ans + 1

    # Print the result
    print(int(ans))

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 10

    # Function Call
    countK(N)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Store the all prime numbers
// using Sieve of Eratosthenes
var MAXN = 100001;
var spf = [];

// Function to fill the prime numbers
// using Sieve of Erastosthenes
function sieve()
{

// Create a boolean array and
    // initialize all entries it as 0
    var p = Array(MAXN + 1).fill(0);

    p[2] = 1;
    for (var i = 3; i < MAXN; i += 2) {
        p[i] = 1;
    }

    // Push the first prime number
    spf.push(2);

    for (var i = 3; i < MAXN; i += 2) {

        // If the current number is prime
        if (p[i]) {

            // Store the prime numbers
            // in spf which is prime
            spf.push(i);

            // Mark all its multiples as false
            for (var j = i * i; j < MAXN;
                 j += 2 * i)
                p[j] = 0;
        }
    }
}

// Function to count the values of K where
// 1≤K≤N such that 1< gcd(K, N) < K
function countK(N)
{
    // Precalculate prime numbers
    sieve();
    var N1 = N;

    // Store the smallest prime number
    var div = spf[0];

    var index = 1, C = 0;

    // Store the count of those numbers in the
    // range [1, N] for which gcd(N, K) = K
    var count1 = 1;

    // Store the count of those numbers from
    // the range [1, N] such that gcd(N, K) = 1
    var count2 = N;

    // Iterate through all prime factors of N
    while (div * div <= N) {
        if (N % div == 0) {
            C = 0;
            while (N % div == 0) {
                N /= div;
                C++;
            }

            count1 = count1 * (C + 1);

            // count2 is determined by
            // Euler's Totient Function
            count2 *= (1.0 - (1.0 / div));
        }

        div = spf[index];

        index++;
    }
    if (N != 1) {

        count1 *= 2;
        count2 = count2 * (1.0 - (1.0 / N));
    }

    var ans = N1 - count1 - count2;

    // Add 1 to result as 1 is contributed
    // twice due to count1 and count2
    ans = ans + 1;

    // Print the result
    document.write(ans);

    return;
}

// Driver Code
// Given Input
var N = 10;

// Function Call
countK(N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*