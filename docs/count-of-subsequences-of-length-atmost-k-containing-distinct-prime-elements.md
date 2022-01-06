# 包含不同素元素的长度为 K 的子序列的计数

> 原文:[https://www . geesforgeks . org/长度子序列计数-atmat-k-包含不同的素元素/](https://www.geeksforgeeks.org/count-of-subsequences-of-length-atmost-k-containing-distinct-prime-elements/)

给定一个长度为 **N** 的数组**和一个整数 **K** ，任务是计算长度最多为 **K** 的可能子序列的数量，这些子序列包含数组中不同的素元素。
**示例:****

> **输入:** arr[] = {1，2，2，3，3，4，5}，N = 7，K = 3
> **输出:** 18
> **解释:** {}、{2}、{2}、{3}、{3}、{5}、{2，3}、{2，3}、{2，3}、{2，3}、{2，3}、{2，5}、{2，5}、{3，5}、{3，5}
> **输入** arr[] = {2，4，6，7，3，9，11，5}，N = 8，K = 3
> **输出:** 26

**进场:**
使用厄拉多塞的[筛，预计算并存储所有质数。计算并存储给定数组中每个素数的频率。使用动态编程方法，计算长度为 2 至 **K** 的子序列的数量。通过为每个**DP【I】**添加长度 2 到 **K** 的可能不同组合，继续更新**和**。一旦计算出来，将所有素数+ 1 的频率相加，作为长度为 1 和 0 的子序列。**和**的最终值给出了所需的结果。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ Program to find the
// count of distinct prime
// subsequences at most of
// of length K from a given array

#include <bits/stdc++.h>
using namespace std;

bool prime[100001];

void SieveOfEratosthenes()
{
    // Initialize all indices as true
    memset(prime, true, sizeof(prime));

    prime[0] = prime[1] = false;

    // A value in prime[i] will finally be
    // false if i is not a prime, else true
    for (int p = 2; p * p <= 100000; p++) {

        // If prime[p] is true,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // as false, i.e. non-prime
            for (int i = p * p;
                 i <= 100000;
                 i += p)

                prime[i] = false;
        }
    }
}

// Returns number of subsequences
// of maximum length k and
// contains distinct primes
int distinctPrimeSubSeq(
    int a[],
    int n, int k)
{
    SieveOfEratosthenes();

    // Store the primes in
    // the given array
    vector<int> primes;

    for (int i = 0; i < n; i++) {
        if (prime[a[i]])
            primes.push_back(a[i]);
    }

    int l = primes.size();
    // Sort the primes
    sort(primes.begin(),
         primes.end());

    // Store the frequencies
    // of all the
    // distinct primes
    vector<int> b;
    vector<int> dp;
    int sum = 0;

    for (int i = 0; i < l;) {
        int count = 1, x = a[i];
        i++;
        while (i < l && a[i] == x) {
            count++;
            i++;
        }

        // Store the frequency
        // of primes
        b.push_back(count);
        dp.push_back(count);

        // Store the sum of all
        // frequencies
        sum += count;
    }

    // Store the length of
    // subsequence at every
    // instant
    int of_length = 2;
    int len = dp.size();
    int ans = 0;

    while (of_length <= k) {

        // Store the frequency
        int freq = 0;

        // Store the previous
        // count of updated DP
        int prev = 0;

        for (int i = 0; i < (len - 1); i++) {
            freq += dp[i];

            int j = sum - freq;

            // Calculate total subsequences
            // of current of_length
            int subseq = b[i] * j;

            // Add the number of
            // subsequences to the answer
            ans += subseq;

            // Update the value in dp[i]
            dp[i] = subseq;

            // Store the updated dp[i]
            prev += dp[i];
        }

        len--;
        sum = prev;
        of_length++;
    }

    ans += (l + 1);

    return ans;
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 2, 3, 3, 4, 5 };
    int n = sizeof(a) / sizeof(int);
    int k = 3;

    cout << distinctPrimeSubSeq(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// count of distinct prime
// subsequences at most of
// of length K from a given array
import java.util.*;
class GFG{

static boolean []prime =
       new boolean[100001];

static void SieveOfEratosthenes()
{
  // Initialize all indices as true
  for (int i = 0; i < prime.length; i++)
    prime[i] = true;

  prime[0] = prime[1] = false;

  // A value in prime[i] will finally
  // be false if i is not a prime,
  // else true
  for (int p = 2; p * p < 100000; p++)
  {
    // If prime[p] is true,
    // then it is a prime
    if (prime[p] == true)
    {
      // Update all multiples of p
      // as false, i.e. non-prime
      for (int i = p * p;
               i <= 100000; i += p)
        prime[i] = false;
    }
  }
}

// Returns number of subsequences
// of maximum length k and
// contains distinct primes
static int distinctPrimeSubSeq(int a[],
                               int n,
                               int k)
{
  SieveOfEratosthenes();

  // Store the primes in
  // the given array
  Vector<Integer> primes =
         new Vector<>();

  for (int i = 0; i < n; i++)
  {
    if (prime[a[i]])
      primes.add(a[i]);
  }

  int l = primes.size();

  // Sort the primes
  Collections.sort(primes);

  // Store the frequencies
  // of all the
  // distinct primes
  Vector<Integer> b =
         new Vector<>();
  Vector<Integer> dp =
         new Vector<>();
  int sum = 0;

  for (int i = 0; i < l;)
  {
    int count = 1, x = a[i];
    i++;
    while (i < l && a[i] == x)
    {
      count++;
      i++;
    }

    // Store the frequency
    // of primes
    b.add(count);
    dp.add(count);

    // Store the sum of all
    // frequencies
    sum += count;
  }

  // Store the length of
  // subsequence at every
  // instant
  int of_length = 2;
  int len = dp.size();
  int ans = 0;

  while (of_length < k)
  {
    // Store the frequency
    int freq = 0;

    // Store the previous
    // count of updated DP
    int prev = 0;

    for (int i = 0;
             i < (len - 1); i++)
    {
      freq += dp.elementAt(i);

      int j = sum - freq;

      // Calculate total subsequences
      // of current of_length
      int subseq = b.elementAt(i) * j;

      // Add the number of
      // subsequences to the answer
      ans += subseq;

      // Update the value in dp[i]
      dp.add(i, subseq);

      // Store the updated dp[i]
      prev += dp.elementAt(i);
    }

    len--;
    sum = prev;
    of_length++;
  }
  ans += (l + 3);
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  int a[] = {1, 2, 2, 3, 3, 4, 5};
  int n = a.length;
  int k = 3;
  System.out.print(distinctPrimeSubSeq(a, n, k));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 Program to find the
# count of distinct prime
# subsequences at most of
# of length K from a given array

prime = [True] * 1000000

def SieveOfEratosthenes():

    global prime

    prime[0] = prime[1] = False

    # A value in prime[i] will
    # finally be false if i is
    # not a prime, else true
    p = 2

    while p * p <= 100000:

        # If prime[p] is true,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # as false, i.e. non-prime
            for i in range(p * p,
                           100001, p):
                prime[i] = False

        p += 1

# Returns number of subsequences
# of maximum length k and
# contains distinct primes
def distinctPrimeSubSeq(a,
                        n, k):

    SieveOfEratosthenes()

    # Store the primes in
    # the given array
    primes = []

    for i in range(n):
        if (prime[a[i]]):
            primes.append(a[i])

    l = len(primes)

    # Sort the primes
    primes.sort()

    # Store the frequencies
    # of all the
    # distinct primes
    b = []
    dp = []
    sum = 0

    i = 0
    while i < l:
        count = 1
        x = a[i]
        i += 1
        while (i < l and
               a[i] == x):
            count += 1
            i += 1

        # Store the frequency
        # of primes
        b.append(count)
        dp.append(count)

        # Store the sum of all
        # frequencies
        sum += count

    # Store the length of
    # subsequence at every
    # instant
    of_length = 2
    leng = len(dp)
    ans = 0

    while (of_length <= k):

        # Store the frequency
        freq = 0

        # Store the previous
        # count of updated DP
        prev = 0

        for i in range(leng - 1):
            freq += dp[i]

            j = sum - freq

            # Calculate total subsequences
            # of current of_length
            subseq = b[i] * j

            # Add the number of
            # subsequences to the answer
            ans += subseq

            # Update the value in dp[i]
            dp[i] = subseq

            # Store the updated dp[i]
            prev += dp[i]

        leng -= 1
        sum = prev
        of_length += 1

    ans += (l + 1)
    return ans

# Driver Code
if __name__ == "__main__":

    a = [1, 2, 2,
         3, 3, 4, 5]
    n = len(a)
    k = 3
    print(distinctPrimeSubSeq(a, n, k))

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to find the
// count of distinct prime
// subsequences at most of
// of length K from a given array
using System;
using System.Collections.Generic;
class GFG{

static bool []prime =
       new bool[100001];

static void SieveOfEratosthenes()
{
  // Initialize all indices as true
  for (int i = 0; i < prime.Length; i++)
    prime[i] = true;

  prime[0] = prime[1] = false;

  // A value in prime[i] will finally
  // be false if i is not a prime,
  // else true
  for (int p = 2; p * p < 100000; p++)
  {
    // If prime[p] is true,
    // then it is a prime
    if (prime[p] == true)
    {
      // Update all multiples of p
      // as false, i.e. non-prime
      for (int i = p * p;
               i <= 100000; i += p)
        prime[i] = false;
    }
  }
}

// Returns number of subsequences
// of maximum length k and
// contains distinct primes
static int distinctPrimeSubSeq(int []a,
                               int n,
                               int k)
{
  SieveOfEratosthenes();

  // Store the primes in
  // the given array
  List<int> primes = new List<int>();

  for (int i = 0; i < n; i++)
  {
    if (prime[a[i]])
      primes.Add(a[i]);
  }

  int l = primes.Count;

  // Sort the primes
  primes.Sort();

  // Store the frequencies
  // of all the
  // distinct primes
  List<int> b = new List<int>();
  List<int> dp = new List<int>();
  int sum = 0;

  for (int i = 0; i < l;)
  {
    int count = 1, x = a[i];
    i++;

    while (i < l && a[i] == x)
    {
      count++;
      i++;
    }

    // Store the frequency
    // of primes
    b.Add(count);
    dp.Add(count);

    // Store the sum of all
    // frequencies
    sum += count;
  }

  // Store the length of
  // subsequence at every
  // instant
  int of_length = 2;
  int len = dp.Count;
  int ans = 0;

  while (of_length <= k)
  {
    // Store the frequency
    int freq = 0;

    // Store the previous
    // count of updated DP
    int prev = 0;

    for (int i = 0;
             i < (len ); i++)
    {
      freq += dp[i];
      int j = sum - freq;

      // Calculate total subsequences
      // of current of_length
      int subseq = b[i] * j;

      // Add the number of
      // subsequences to the answer
      ans += subseq;

      // Update the value in dp[i]
      dp[i] = subseq;

      // Store the updated dp[i]
      prev += dp[i];
    }

    len--;
    sum = prev;
    of_length++;
  }

  ans += (l + 1);
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int []a = {1, 2, 2, 3, 3, 4, 5};
  int n = a.Length;
  int k = 3;
  Console.Write(distinctPrimeSubSeq(a, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript Program to find the
// count of distinct prime
// subsequences at most of
// of length K from a given array

let prime = new Array(100001);

function SieveOfEratosthenes()
{
    // Initialize all indices as true
    prime.fill(true)

    prime[0] = prime[1] = false;

    // A value in prime[i] will finally be
    // false if i is not a prime, else true
    for (let p = 2; p * p <= 100000; p++) {

        // If prime[p] is true,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // as false, i.e. non-prime
            for (let i = p * p;
                i <= 100000;
                i += p)

                prime[i] = false;
        }
    }
}

// Returns number of subsequences
// of maximum length k and
// contains distinct primes
function distinctPrimeSubSeq(a, n, k)
{
    SieveOfEratosthenes();

    // Store the primes in
    // the given array
    let primes = new Array();

    for (let i = 0; i < n; i++) {
        if (prime[a[i]])
            primes.push(a[i]);
    }

    let l = primes.length;
    // Sort the primes
    primes.sort((a, b) => a - b)

    // Store the frequencies
    // of all the
    // distinct primes
    let b = new Array();
    let dp = new Array();
    let sum = 0;

    for (let i = 0; i < l;) {
        let count = 1, x = a[i];
        i++;
        while (i < l && a[i] == x) {
            count++;
            i++;
        }

        // Store the frequency
        // of primes
        b.push(count);
        dp.push(count);

        // Store the sum of all
        // frequencies
        sum += count;
    }

    // Store the length of
    // subsequence at every
    // instant
    let of_length = 2;
    let len = dp.length;
    let ans = 0;

    while (of_length <= k) {

        // Store the frequency
        let freq = 0;

        // Store the previous
        // count of updated DP
        let prev = 0;

        for (let i = 0; i < (len - 1); i++) {
            freq += dp[i];

            let j = sum - freq;

            // Calculate total subsequences
            // of current of_length
            let subseq = b[i] * j;

            // Add the number of
            // subsequences to the answer
            ans += subseq;

            // Update the value in dp[i]
            dp[i] = subseq;

            // Store the updated dp[i]
            prev += dp[i];
        }

        len--;
        sum = prev;
        of_length++;
    }

    ans += (l + 1);

    return ans;
}

// Driver Code

let a = [ 1, 2, 2, 3, 3, 4, 5 ];
let n = a.length;
let k = 3;

document.write(distinctPrimeSubSeq(a, n, k));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
18
```

**时间复杂度:** *O(K*(不同的素数))*