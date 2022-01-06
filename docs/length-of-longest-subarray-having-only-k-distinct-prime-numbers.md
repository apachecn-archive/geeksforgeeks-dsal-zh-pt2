# 只有 K 个不同素数的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最长子数组长度-只有-k 个不同的素数/](https://www.geeksforgeeks.org/length-of-longest-subarray-having-only-k-distinct-prime-numbers/)

给定一个由正整数组成的 **N** 数组 **arr[]** 。任务是找到这个数组中最长的子数组的长度，这个子数组包含精确的不同的素数。如果不存在任何子阵列，则打印**-1”**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8，9}，K = 1
> **输出:** 4
> **解释:**
> 子阵{6，7，8，9}包含 4 个元素，只有一个是质数(7)。因此，所需长度为 4。
> 
> **输入:** arr[] = {1，2，3，3，4，5，6，7，8，9}，K = 3
> **输出:** 8
> **解释:**
> 子阵列{3，3，4，5，6，7，8，9}包含 8 个元素，只包含 3 个不同的素数(3，5 和 7)。因此，所需长度为 8。

**天真方法:**想法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并检查任何最大长度的子阵是否包含 **K** 个不同的素数。如果是，则打印子阵列长度，否则打印**-1”**。
***时间复杂度:** O(N <sup>2</sup> ，其中 N 为给定数组的长度。*
***空间复杂度:** O(N)*

**高效方法:**思路是利用厄拉多塞的[筛计算素数，利用](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决上述问题。以下是步骤:

1.  使用厄拉多塞的[筛预先计算给定的数是否为素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2.  遍历给定数组时，保持该数组中出现的素数。
3.  直到 **K** 不为零，我们计算子阵列中出现的不同素数，并将 **K** 减少 1。
4.  As **K** becomes negative, start deleting the elements till the first prime number of the current subarray as there might be a possibility of a longer subarray afterward.
5.  当 **K** 为 **0** 时，我们更新最大长度。
6.  完成上述所有步骤后，打印最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
bool isprime[2000010];

// Function to precalculate all the
// prime up to 10^6
void SieveOfEratosthenes(int n)
{
    // Initialize prime to true
    memset(isprime, true, sizeof(isprime));

    isprime[1] = false;

    // Iterate [2, sqrt(N)]
    for (int p = 2; p * p <= n; p++) {

        // If p is prime
        if (isprime[p] == true) {

            // Mark all multiple of p as true
            for (int i = p * p; i <= n; i += p)
                isprime[i] = false;
        }
    }
}

// Function that finds the length of
// longest subarray K distinct primes
int KDistinctPrime(int arr[], int n,
                   int k)
{
    // Precompute all prime up to 2*10^6
    SieveOfEratosthenes(2000000);

    // Keep track occurrence of prime
    map<int, int> cnt;

    // Initialize result to -1
    int result = -1;

    for (int i = 0, j = -1; i < n; ++i) {

        int x = arr[i];

        // If number is prime then
        // increment its count and
        // decrease k
        if (isprime[x]) {

            if (++cnt[x] == 1) {

                // Decrement K
                --k;
            }
        }

        // Remove required elements
        // till k become non-negative
        while (k < 0) {

            x = arr[++j];
            if (isprime[x]) {

                // Decrease count so
                // that it may appear
                // in another subarray
                // appearing after this
                // present subarray
                if (--cnt[x] == 0) {

                    // Increment K
                    ++k;
                }
            }
        }

        // Take the max value as
        // length of subarray
        if (k == 0)
            result = max(result, i - j);
    }

    // Return the final length
    return result;
}

// Driver Code
int main(void)
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 3, 4,
                  5, 6, 7, 8, 9 };
    int K = 3;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << KDistinctPrime(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

static boolean[] isprime = new boolean[2000010];

// Function to precalculate all the
// prime up to 10^6
static void SieveOfEratosthenes(int n)
{

    // Initialize prime to true
    Arrays.fill(isprime, true);

    isprime[1] = false;

    // Iterate [2, sqrt(N)]
    for(int p = 2; p * p <= n; p++)
    {

        // If p is prime
        if (isprime[p] == true)
        {

            // Mark all multiple of p as true
            for(int i = p * p; i <= n; i += p)
                isprime[i] = false;
        }
    }
}

// Function that finds the length of
// longest subarray K distinct primes
static int KDistinctPrime(int arr[], int n,
                                     int k)
{

    // Precompute all prime up to 2*10^6
    SieveOfEratosthenes(2000000);

    // Keep track occurrence of prime
    Map<Integer, Integer> cnt = new HashMap<>();

    // Initialize result to -1
    int result = -1;

    for(int i = 0, j = -1; i < n; ++i)
    {
        int x = arr[i];

        // If number is prime then
        // increment its count and
        // decrease k
        if (isprime[x])
        {
            cnt.put(x, cnt.getOrDefault(x, 0) + 1);

            if (cnt.get(x) == 1)
            {

                // Decrement K
                --k;
            }
        }

        // Remove required elements
        // till k become non-negative
        while (k < 0)
        {
            x = arr[++j];
            if (isprime[x])
            {

                // Decrease count so
                // that it may appear
                // in another subarray
                // appearing after this
                // present subarray
                cnt.put(x, cnt.getOrDefault(x, 0) - 1);
                if (cnt.get(x) == 0)
                {

                    // Increment K
                    ++k;
                }
            }
        }

        // Take the max value as
        // length of subarray
        if (k == 0)
            result = Math.max(result, i - j);
    }

    // Return the final length
    return result;
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 3, 4,
                  5, 6, 7, 8, 9 };
    int K = 3;

    int N = arr.length;

    // Function call
    System.out.println(KDistinctPrime(arr, N, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import defaultdict

isprime = [True] * 2000010

# Function to precalculate all the
# prime up to 10^6
def SieveOfEratosthenes(n):

    isprime[1] = False

    # Iterate [2, sqrt(N)]
    p = 2
    while(p * p <= n):

        # If p is prime
        if(isprime[p] == True):

            # Mark all multiple of p as true
            for i in range(p * p, n + 1, p):
                isprime[i] = False

        p += 1

# Function that finds the length of
# longest subarray K distinct primes
def KDistinctPrime(arr, n, k):

    # Precompute all prime up to 2*10^6
    SieveOfEratosthenes(2000000)

    # Keep track occurrence of prime
    cnt = defaultdict(lambda : 0)

    # Initialize result to -1
    result = -1

    j = -1

    for i in range(n):
        x = arr[i]

        # If number is prime then
        # increment its count and
        # decrease k
        if(isprime[x]):
            cnt[x] += 1

            if(cnt[x] == 1):

                # Decrement K
                k -= 1

    # Remove required elements
    # till k become non-negative
    while(k < 0):
        j += 1
        x = arr[j]

        if(isprime[x]):

            # Decrease count so
            # that it may appear
            # in another subarray
            # appearing after this
            # present subarray
            cnt[x] -= 1
            if(cnt[x] == 0):

                # Increment K
                k += 1

        # Take the max value as
        # length of subarray
        if(k == 0):
            result = max(result, i - j)

    # Return the final length
    return result

# Driver Code

# Given array arr[]
arr = [ 1, 2, 3, 3, 4,
        5, 6, 7, 8, 9 ]

K = 3

N = len(arr)

# Function call
print(KDistinctPrime(arr, N, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{
static bool[] isprime = new bool[2000010];

// Function to precalculate all the
// prime up to 10^6
static void SieveOfEratosthenes(int n)
{   
    // Initialize prime to true
    for(int i = 0; i < isprime.Length; i++)
        isprime[i] = true;
    isprime[1] = false;

    // Iterate [2, sqrt(N)]
    for(int p = 2; p * p <= n; p++)
    {       
        // If p is prime
        if (isprime[p] == true)
        {           
            // Mark all multiple of p as true
            for(int i = p * p; i <= n; i += p)
                isprime[i] = false;
        }
    }
}

// Function that finds the length of
// longest subarray K distinct primes
static int KDistinctPrime(int []arr,
                          int n, int k)
{   
    // Precompute all prime up to 2*10^6
    SieveOfEratosthenes(2000000);

    // Keep track occurrence of prime
    Dictionary<int,
               int> cnt = new Dictionary<int,
                                         int>();

    // Initialize result to -1
    int result = -1;

    for(int i = 0, j = -1; i < n; ++i)
    {
        int x = arr[i];

        // If number is prime then
        // increment its count and
        // decrease k
        if (isprime[x])
        {
            if(cnt.ContainsKey(x))
                cnt[x] = cnt[x] + 1;
            else
                cnt.Add(x, 1);           
            if (cnt[x] == 1)
            {               
                // Decrement K
                --k;
            }
        }

        // Remove required elements
        // till k become non-negative
        while (k < 0)
        {
            x = arr[++j];
            if (isprime[x])
            {               
                // Decrease count so
                // that it may appear
                // in another subarray
                // appearing after this
                // present subarray
                if(cnt.ContainsKey(x))
                    cnt[x] = cnt[x] - 1;
                else
                    cnt.Add(x, 0);
                if (cnt[x] == 0)
                {                   
                    // Increment K
                    ++k;
                }
            }
        }

        // Take the max value as
        // length of subarray
        if (k == 0)
            result = Math.Max(result, i - j);
    }

    // Return the readonly length
    return result;
}

// Driver Code
public static void Main(String[] args)
{   
    // Given array []arr
    int []arr = {1, 2, 3, 3, 4,
                 5, 6, 7, 8, 9};
    int K = 3;

    int N = arr.Length;

    // Function call
    Console.WriteLine(KDistinctPrime(arr, N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let isprime = new Array(2000010);

    // Function to precalculate all the
    // prime up to 10^6
    function SieveOfEratosthenes(n)
    {

        // Initialize prime to true
        isprime.fill(true);

        isprime[1] = false;

        // Iterate [2, sqrt(N)]
        for(let p = 2; p * p <= n; p++)
        {

            // If p is prime
            if (isprime[p] == true)
            {

                // Mark all multiple of p as true
                for(let i = p * p; i <= n; i += p)
                    isprime[i] = false;
            }
        }
    }

    // Function that finds the length of
    // longest subarray K distinct primes
    function KDistinctPrime(arr, n, k)
    {

        // Precompute all prime up to 2*10^6
        SieveOfEratosthenes(2000000);

        // Keep track occurrence of prime
        let cnt = new Map();

        // Initialize result to -1
        let result = -1;

        for(let i = 0, j = -1; i < n; ++i)
        {
            let x = arr[i];

            // If number is prime then
            // increment its count and
            // decrease k
            if (isprime[x])
            {
                if(cnt.has(x))
                    cnt.set(x, cnt.get(x)+1)
                else
                    cnt.set(x, 1);

                if (cnt.get(x) == 1)
                {

                    // Decrement K
                    --k;
                }
            }

            // Remove required elements
            // till k become non-negative
            while (k < 0)
            {
                x = arr[++j];
                if (isprime[x])
                {

                    // Decrease count so
                    // that it may appear
                    // in another subarray
                    // appearing after this
                    // present subarray
                    if(cnt.has(x))
                        cnt.set(x, cnt.get(x) - 1)
                    else
                        cnt.set(x, -1);
                    if (cnt.get(x) == 0)
                    {

                        // Increment K
                        ++k;
                    }
                }
            }

            // Take the max value as
            // length of subarray
            if (k == 0)
                result = Math.max(result, i - j);
        }

        // Return the final length
        return result;
    }

    // Given array arr[]
    let arr = [ 1, 2, 3, 3, 4, 5, 6, 7, 8, 9 ];
    let K = 3;

    let N = arr.length;

    // Function call
    document.write(KDistinctPrime(arr, N, K));

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N*log(log(N))，其中 N 是给定数组中的最大元素。*
***辅助空间:** O(N)*