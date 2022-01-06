# 最长的子序列，子序列中的每个元素都是通过将前一个元素乘以一个素数

而形成的

> 原文:[https://www . geeksforgeeks . org/最长子序列这样子序列中的每个元素都是通过将前一个元素乘以一个素数而形成的/](https://www.geeksforgeeks.org/longest-subsequence-such-that-every-element-in-the-subsequence-is-formed-by-multiplying-previous-element-with-a-prime/)

给定一个排序的 **N** 整数数组。任务是找到最长的子序列，这样子序列中的每个元素都可以通过将任意[质数](https://www.geeksforgeeks.org/prime-numbers/)乘以子序列中的前一个元素来获得。
**注**:A【I】<= 10<sup>5</sup>

**示例:**

> **输入** : a[] = {3，5，6，12，15，36}
> 输出 4
> 最长的子序列是{3，6，12，36 }
> 6 = 3 * 2
> 12 = 6 * 2
> 36 = 12 * 3
> 2 和 3 是素数
> 
> **输入:** a[] = {1，2，5，6，12，35，60，385}
> **输出:** 5

**逼近**:使用预存储素数直到数组中的最大数，使用基本的[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决这个问题。可以遵循以下步骤来解决上述问题:

*   最初，它们将所有素数存储在任何数据结构中。
*   散列散列图中数字的索引。
*   创建一个大小为 N 的 dp[]，并在每个地方用 1 初始化它，因为最长的子序列可能只有 1。dp[i]表示最长子序列的长度，该子序列可以以[i]作为起始元素。
*   从 n-2 开始迭代，对每个数乘以所有素数，直到它超过一个[n-1]，并执行下面的操作。
*   将数字 a[i]乘以质数得到 x。如果 x 存在于哈希映射中，则循环将是 **dp[i] = max(dp[i]，1+DP[哈希[x]])** 。
*   最后，在 dp[]数组中迭代，找到最大值，这就是我们的答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to pre-store primes
void SieveOfEratosthenes(int MAX, vector<int>& primes)
{
    bool prime[MAX + 1];
    memset(prime, true, sizeof(prime));

    // Sieve method to check if prime or not
    for (long long p = 2; p * p <= MAX; p++) {
        if (prime[p] == true) {
            // Multiples
            for (long long i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // Pre-store all the primes
    for (long long i = 2; i <= MAX; i++) {
        if (prime[i])
            primes.push_back(i);
    }
}

// Function to find the longest subsequence
int findLongest(int A[], int n)
{
    // Hash map
    unordered_map<int, int> mpp;
    vector<int> primes;

    // Call the function to pre-store the primes
    SieveOfEratosthenes(A[n - 1], primes);

    int dp[n];
    memset(dp, 0, sizeof dp);

    // Initialize last element with 1
    // as that is the longest possible
    dp[n - 1] = 1;
    mpp[A[n - 1]] = n - 1;

    // Iterate from the back and find the longest
    for (int i = n - 2; i >= 0; i--) {

        // Get the number
        int num = A[i];

        // Initialize dp[i] as 1
        // as the element will only me in
        // the subsequence .
        dp[i] = 1;
        int maxi = 0;

        // Iterate in all the primes and
        // multiply to get the next element
        for (auto it : primes) {

            // Next element if multiplied with it
            int xx = num * it;

            // If exceeds the last element
            // then break
            if (xx > A[n - 1])
                break;

            // If the number is there in the array
            else if (mpp[xx] != 0) {
                // Get the maximum most element
                dp[i] = max(dp[i], 1 + dp[mpp[xx]]);
            }
        }
        // Hash the element
        mpp[A[i]] = i;
    }
    int ans = 1;

    // Find the longest
    for (int i = 0; i < n; i++) {
        ans = max(ans, dp[i]);
    }

    return ans;
}
// Driver Code
int main()
{
    int a[] = { 1, 2, 5, 6, 12, 35, 60, 385 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << findLongest(a, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.HashMap;
import java.util.Vector;

class GFG
{

    // Function to pre-store primes
    public static void SieveOfEratosthenes(int MAX,
                            Vector<Integer> primes)
    {
        boolean[] prime = new boolean[MAX + 1];
        for (int i = 0; i < MAX + 1; i++)
            prime[i] = true;

        // Sieve method to check if prime or not
        for (int p = 2; p * p <= MAX; p++)
        {
            if (prime[p] == true)
            {
                // Multiples
                for (int i = p * p; i <= MAX; i += p)
                    prime[i] = false;
            }
        }

        // Pre-store all the primes
        for (int i = 2; i <= MAX; i++)
        {
            if (prime[i])
                primes.add(i);
        }
    }

    // Function to find the intest subsequence
    public static int findLongest(int[] A, int n)
    {

        // Hash map
        HashMap<Integer, Integer> mpp = new HashMap<>();
        Vector<Integer> primes = new Vector<>();

        // Call the function to pre-store the primes
        SieveOfEratosthenes(A[n - 1], primes);

        int[] dp = new int[n];

        // Initialize last element with 1
        // as that is the intest possible
        dp[n - 1] = 1;
        mpp.put(A[n - 1], n - 1);

        // Iterate from the back and find the intest
        for (int i = n - 2; i >= 0; i--)
        {

            // Get the number
            int num = A[i];

            // Initialize dp[i] as 1
            // as the element will only me in
            // the subsequence .
            dp[i] = 1;
            int maxi = 0;

            // Iterate in all the primes and
            // multiply to get the next element
            for (int it : primes)
            {

                // Next element if multiplied with it
                int xx = num * it;

                // If exceeds the last element
                // then break
                if (xx > A[n - 1])
                    break;

                // If the number is there in the array
                else if (mpp.get(xx) != null && mpp.get(xx) != 0)
                {

                        // Get the maximum most element
                        dp[i] = Math.max(dp[i], 1 + dp[mpp.get(xx)]);
                }
            }

            // Hash the element
            mpp.put(A[i], i);
        }
        int ans = 1;

        // Find the intest
        for (int i = 0; i < n; i++)
            ans = Math.max(ans, dp[i]);

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 1, 2, 5, 6, 12, 35, 60, 385 };
        int n = a.length;
        System.out.println(findLongest(a, n));

    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

from math import sqrt

# Function to pre-store primes
def SieveOfEratosthenes(MAX, primes) :

    prime = [True]*(MAX + 1);

    # Sieve method to check if prime or not
    for p in range(2,int(sqrt(MAX)) + 1) :
        if (prime[p] == True) :
            # Multiples
            for i in range(p**2, MAX + 1, p) :
                prime[i] = False;

    # Pre-store all the primes
    for i in range(2, MAX + 1) :
        if (prime[i]) :
            primes.append(i);

# Function to find the longest subsequence
def findLongest(A, n) :

    # Hash map
    mpp = {};
    primes = [];

    # Call the function to pre-store the primes
    SieveOfEratosthenes(A[n - 1], primes);

    dp = [0] * n ;

    # Initialize last element with 1
    # as that is the longest possible
    dp[n - 1] = 1;
    mpp[A[n - 1]] = n - 1;

    # Iterate from the back and find the longest
    for i in range(n-2,-1,-1) :

        # Get the number
        num = A[i];

        # Initialize dp[i] as 1
        # as the element will only me in
        # the subsequence
        dp[i] = 1;
        maxi = 0;

        # Iterate in all the primes and
        # multiply to get the next element
        for it in primes :

            # Next element if multiplied with it
            xx = num * it;

            # If exceeds the last element
            # then break
            if (xx > A[n - 1]) :
                break;

            # If the number is there in the array
            elif xx in mpp :
                # Get the maximum most element
                dp[i] = max(dp[i], 1 + dp[mpp[xx]]);

        # Hash the element
        mpp[A[i]] = i;

    ans = 1;

    # Find the longest
    for i in range(n) :
        ans = max(ans, dp[i]);

    return ans;

# Driver Code
if __name__ == "__main__" :

    a = [ 1, 2, 5, 6, 12, 35, 60, 385 ];
    n = len(a);

    print(findLongest(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to pre-store primes
    public static void SieveOfEratosthenes(int MAX,
                                      List<int> primes)
    {
        Boolean[] prime = new Boolean[MAX + 1];
        for (int i = 0; i < MAX + 1; i++)
            prime[i] = true;

        // Sieve method to check if prime or not
        for (int p = 2; p * p <= MAX; p++)
        {
            if (prime[p] == true)
            {
                // Multiples
                for (int i = p * p; i <= MAX; i += p)
                    prime[i] = false;
            }
        }

        // Pre-store all the primes
        for (int i = 2; i <= MAX; i++)
        {
            if (prime[i])
                primes.Add(i);
        }
    }

    // Function to find the intest subsequence
    public static int findLongest(int[] A, int n)
    {

        // Hash map
        Dictionary<int, int> mpp = new Dictionary<int, int>();
        List<int> primes = new List<int>();

        // Call the function to pre-store the primes
        SieveOfEratosthenes(A[n - 1], primes);

        int[] dp = new int[n];

        // Initialize last element with 1
        // as that is the intest possible
        dp[n - 1] = 1;
        mpp.Add(A[n - 1], n - 1);

        // Iterate from the back and find the intest
        for (int i = n - 2; i >= 0; i--)
        {

            // Get the number
            int num = A[i];

            // Initialize dp[i] as 1
            // as the element will only me in
            // the subsequence .
            dp[i] = 1;

            // Iterate in all the primes and
            // multiply to get the next element
            foreach (int it in primes)
            {

                // Next element if multiplied with it
                int xx = num * it;

                // If exceeds the last element
                // then break
                if (xx > A[n - 1])
                    break;

                // If the number is there in the array
                else if (mpp.ContainsKey(xx) && mpp[xx] != 0)
                {

                    // Get the maximum most element
                    dp[i] = Math.Max(dp[i], 1 + dp[mpp[xx]]);
                }
            }

            // Hash the element
            if(mpp.ContainsKey(A[i]))
                mpp[A[i]] = i;
            else
                mpp.Add(A[i], i);
        }
        int ans = 1;

        // Find the intest
        for (int i = 0; i < n; i++)
            ans = Math.Max(ans, dp[i]);

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 1, 2, 5, 6, 12, 35, 60, 385 };
        int n = a.Length;
        Console.WriteLine(findLongest(a, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to implement the
    // above approach

    // Function to pre-store primes
    function SieveOfEratosthenes(MAX, primes) {
        let prime = new Array(MAX + 1).fill(true);

        // Sieve method to check if prime or not
        for (let p = 2; p * p <= MAX; p++) {
            if (prime[p] == true) {
            // Multiples
                for (let i = p * p; i <= MAX; i += p)
                    prime[i] = false;
            }
        }

        // Pre-store all the primes
        for (let i = 2; i <= MAX; i++) {
            if (prime[i])
                primes.push(i);
        }
    }   

    // Function to find the longest subsequence
    function findLongest(A, n) {
        // Hash map
        let mpp = new Map();
        let primes = new Array();

        // Call the function to pre-store the primes
        SieveOfEratosthenes(A[n - 1], primes);

        let dp = new Array(n);
        dp.fill(0)

        // Initialize last element with 1
        // as that is the longest possible
        dp[n - 1] = 1;
        mpp.set(A[n - 1], n - 1);

        // Iterate from the back and find the longest
        for (let i = n - 2; i >= 0; i--) {

            // Get the number
            let num = A[i];

            // Initialize dp[i] as 1
            // as the element will only me in
            // the subsequence .
            dp[i] = 1;
            let maxi = 0;

            // Iterate in all the primes and
            // multiply to get the next element
            for (let it of primes) {

                // Next element if multiplied with it
                let xx = num * it;

                // If exceeds the last element
                // then break
                if (xx > A[n - 1])
                    break;

                // If the number is there in the array
                else if (mpp.get(xx)) {
                    // Get the maximum most element
                    dp[i] = Math.max(dp[i], 1 + dp[mpp.get(xx)]);
                }
            }
            // Hash the element
            mpp.set(A[i], i);
        }
        let ans = 1;

        // Find the longest
        for (let i = 0; i < n; i++) {
            ans = Math.max(ans, dp[i]);
        }

        return ans;
    }
    // Driver Code

    let a = [1, 2, 5, 6, 12, 35, 60, 385];
    let n = a.length;
    document.write(findLongest(a, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
5
```

**时间复杂度**:O(N log N)
T3】辅助空间 : O(N)