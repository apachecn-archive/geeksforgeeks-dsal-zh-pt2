# 具有单位 GCD 的子序列的最小长度

> 原文:[https://www . geesforgeks . org/最小长度子序列-having-unit-gcd/](https://www.geeksforgeeks.org/minimum-length-of-subsequence-having-unit-gcd/)

给定一个 **N** 正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到最短子序列的长度，使得子序列的 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 为 1。如果子序列都没有 GCD 1，则打印 **"-1** "。

**示例:**

> **输入:** arr[] = {2，6，12，3}
> **输出:** 2
> **解释:**
> 2，3 的 GCD = 1，这是像 2 一样的子序列的最小长度。
> 
> **输入:** arr[] = {2，4}
> **输出:** -1
> **说明:**
> GCD 为 2，4 = 2

**天真方法:**想法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，并打印 GCD 为 1 且长度最小的子序列的长度。如果子序列都没有 GCD 1，则打印 **"-1** "。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**解决这个问题有两个关键观察点:

1.  只有当两个数的质因数不同时，它们的 GCD 才会等于 1。
2.  任何小于**10<sup>9</sup>T3 的正数最多可以有 9 个质因数。
    **例如** 2×3×5×7×11×13×17×19×23 = 22、30、92、870。如果我们把这个数乘以下一个质数，也就是 29，它会比 10^9.大**

按照以下步骤解决问题:

1.  [将数字表示为其质因数的乘积](https://www.geeksforgeeks.org/product-unique-prime-factors-number/)。由于我们最多有 9 个[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，我们可以使用[位掩码](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)的概念来存储数字的状态。
    **例如**，12 的质因数是 2 和 3。这可以用二进制表示为 11(忽略前面的零)，这意味着这个数字有两个质因数。
2.  对于输入数组中的每个数字，检查是否有其他数字设置了相应的位。这可以通过[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)运算来实现。这个操作的结果是我们的解空间的另一种状态。
3.  现在用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)的概念来记忆状态。这个想法是用一个数组来存储解空间的状态。这是可行的，因为一次只能设置 9 位，大小为 1024 的数组可以捕获解空间的所有状态。
4.  每个状态都使用动态编程来存储到达该状态的最短路径。
5.  如果任意两个状态的按位“与”等于 **0** ，则 GCD 等于**1**，即如果有可能从当前状态到达状态 **0** ，则它将具有最小长度子序列并打印该长度，否则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the prime
// factors of a number
vector<int> findPrimeFactors(int n)
{
    // To store the prime factor
    vector<int> primeFactors(9, 0);

    int j = 0;

    // 2s that divide n
    if (n % 2 == 0) {
        primeFactors[j++] = 2;
        while (n % 2 == 0)
            n >>= 1;
    }

    // N must be odd at this point
    // Skip one element
    for (int i = 3;
         i * i <= n; i += 2) {

        if (n % i == 0) {

            // Update the prime factor
            primeFactors[j++] = i;
            while (n % i == 0)
                n /= i;
        }
    }

    // If n is a prime number
    // greater than 2
    if (n > 2)
        primeFactors[j++] = n;

    vector<int> PrimeFactors(j);

    for(int i = 0; i < j; i++)
    {
        PrimeFactors[i] = primeFactors[i];
    }

    return PrimeFactors;
}

// Function that finds the shortest
// subsequence
void findShortestSubsequence(vector<int> &dp, vector<int> a,
                        int index, vector<int> primeFactors)
{
    int n = a.size();

    for (int j = index; j < n; j++) {
        int bitmask = 0;

        for (int p = 0;
             p < primeFactors.size(); p++) {

            // Check if the prime factor
            // of first number, is also
            // the prime factor of the
            // rest numbers in array
            if ((a[j] % primeFactors[p]) == 0) {

                // Set corresponding bit
                // of prime factor to 1,
                // it means both these
                // numbers have the
                // same prime factor
                bitmask ^= (1 << p);
            }
        }

        for (int i = 0; i < dp.size(); i++) {

            // If no states encountered
            // so far continue for this
            // combination of bits
            if (dp[i] == n + 1)
                continue;

            // Update this state with
            // minimum ways to reach
            // this state
            dp[bitmask & i]
                = min(dp[bitmask & i],
                           dp[i] + 1);
        }
    }
}

// Function that print the minimum
// length of subsequence
void printMinimumLength(vector<int> a)
{
    int Min = a.size() + 1;

    for (int i = 0; i < a.size() - 1; i++) {

        // Find the prime factors of
        // the first number
        vector<int> primeFactors
            = findPrimeFactors(a[i]);

        int n = primeFactors.size();

        // Initialize the array with
        // maximum steps, size of the
        // array + 1 for instance
        vector<int> dp(1 << n, a.size() + 1);

        // Express the prime factors
        // in bit representation

        // Total number of set bits is
        // equal to the total number
        // of prime factors
        int setBits = (1 << n) - 1;

        // Indicates there is one
        // way to reach the number
        // under consideration
        dp[setBits] = 1;
        findShortestSubsequence(dp, a, i + 1,
                                primeFactors);

        // State 0 corresponds
        // to gcd of 1
        Min = min(dp[0], Min);
    }

    // If not found such subsequence
    // then print "-1"
    if (Min == (a.size() + 1))
        cout << -1 << endl;

    // Else print the length
    else
        cout << Min << endl;
}

// Driver code
int main()
{
    // Given array arr[]
    vector<int> arr = { 2, 6, 12, 3 };

    // Function Call
    printMinimumLength(arr);
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function that finds the prime
    // factors of a number
    private static int[] findPrimeFactors(int n)
    {
        // To store the prime factor
        int[] primeFactors = new int[9];

        int j = 0;

        // 2s that divide n
        if (n % 2 == 0) {
            primeFactors[j++] = 2;
            while (n % 2 == 0)
                n >>= 1;
        }

        // N must be odd at this point
        // Skip one element
        for (int i = 3;
             i * i <= n; i += 2) {

            if (n % i == 0) {

                // Update the prime factor
                primeFactors[j++] = i;
                while (n % i == 0)
                    n /= i;
            }
        }

        // If n is a prime number
        // greater than 2
        if (n > 2)
            primeFactors[j++] = n;

        return Arrays.copyOfRange(primeFactors, 0, j);
    }

    // Function that finds the shortest
    // subsequence
    private static void
    findShortestSubsequence(int[] dp, int[] a,
                            int index,
                            int[] primeFactors)
    {
        int n = a.length;

        for (int j = index; j < n; j++) {
            int bitmask = 0;

            for (int p = 0;
                 p < primeFactors.length; p++) {

                // Check if the prime factor
                // of first number, is also
                // the prime factor of the
                // rest numbers in array
                if (a[j] % primeFactors[p] == 0) {

                    // Set corresponding bit
                    // of prime factor to 1,
                    // it means both these
                    // numbers have the
                    // same prime factor
                    bitmask ^= (1 << p);
                }
            }

            for (int i = 0;
                 i < dp.length; i++) {

                // If no states encountered
                // so far continue for this
                // combination of bits
                if (dp[i] == n + 1)
                    continue;

                // Update this state with
                // minimum ways to reach
                // this state
                dp[bitmask & i]
                    = Math.min(dp[bitmask & i],
                               dp[i] + 1);
            }
        }
    }

    // Function that print the minimum
    // length of subsequence
    private static void
    printMinimumLength(int[] a)
    {
        int min = a.length + 1;

        for (int i = 0;
             i < a.length - 1; i++) {

            // Find the prime factors of
            // the first number
            int[] primeFactors
                = findPrimeFactors(a[i]);

            int n = primeFactors.length;

            int[] dp = new int[1 << n];

            // Initialize the array with
            // maximum steps, size of the
            // array + 1 for instance
            Arrays.fill(dp, a.length + 1);

            // Express the prime factors
            // in bit representation

            // Total number of set bits is
            // equal to the total number
            // of prime factors
            int setBits = (1 << n) - 1;

            // Indicates there is one
            // way to reach the number
            // under consideration
            dp[setBits] = 1;
            findShortestSubsequence(dp, a, i + 1,
                                    primeFactors);

            // State 0 corresponds
            // to gcd of 1
            min = Math.min(dp[0], min);
        }

        // If not found such subsequence
        // then print "-1"
        if (min == a.length + 1)
            System.out.println(-1);

        // Else print the length
        else
            System.out.println(min);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 2, 6, 12, 3 };

        // Function Call
        printMinimumLength(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the prime
# factors of a number
def findPrimeFactors(n):

    # To store the prime factor
    primeFactors = [0 for i in range(9)]

    j = 0

    # 2s that divide n
    if (n % 2 == 0):
        primeFactors[j] = 2
        j += 1

        while (n % 2 == 0):
            n >>= 1

    # N must be odd at this point
    # Skip one element
    i = 3
    while (i * i <= n):
        if (n % i == 0):

            # Update the prime factor
            primeFactors[j] = i
            j += 1

            while(n % i == 0):
                n //= i

        i += 2

    # If n is a prime number
    # greater than 2
    if (n > 2):
        primeFactors[j] = n
        j += 1

    for i in range(0, j + 1):
        primeFactors[i] = 0

    return primeFactors

# Function that finds the shortest
# subsequence
def findShortestSubsequence(dp, a, index,
                            primeFactors):
    n = len(a)

    for j in range(index, n):
        bitmask = 0

        for p in range(len(primeFactors)):

            # Check if the prime factor
            # of first number, is also
            # the prime factor of the
            # rest numbers in array
            if (primeFactors[p] != 0 and
                a[j] % primeFactors[p] == 0):

                # Set corresponding bit
                # of prime factor to 1,
                # it means both these
                # numbers have the
                # same prime factor
                bitmask ^= (1 << p)

        for i in range(len(dp)):

            # If no states encountered
            # so far continue for this
            # combination of bits
            if (dp[i] == n + 1):
                continue

            # Update this state with
            # minimum ways to reach
            # this state
            dp[bitmask & i] = min(dp[bitmask & i],
                                  dp[i] + 1)

# Function that print the minimum
# length of subsequence
def printMinimumLength(a):

    mn = len(a) + 1

    for i in range(len(a) - 1):

        # Find the prime factors of
        # the first number
        primeFactors = findPrimeFactors(a[i])

        n = len(primeFactors)

        dp = [0 for i in range(1 << n)]

        # Initialize the array with
        # maximum steps, size of the
        # array + 1 for instance
        dp = [len(a) + 1 for i in range(len(dp))]

        # Express the prime factors
        # in bit representation

        # Total number of set bits is
        # equal to the total number
        # of prime factors
        setBits = (1 << n) - 1

        # Indicates there is one
        # way to reach the number
        # under consideration
        dp[setBits] = 1

        findShortestSubsequence(dp, a, i + 1,
                                primeFactors)

        # State 0 corresponds
        # to gcd of 1
        mn = min(dp[0], mn)

    # If not found such subsequence
    # then print "-1"
    if (mn == len(a) + 1):
        print(-1)

    # Else print the length
    else:
        print(mn)

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, 6, 12, 3 ]

    # Function Call
    printMinimumLength(arr)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that finds the prime
// factors of a number
private static int[] findPrimeFactors(int n)
{
  // To store the prime factor
  int[] primeFactors = new int[9];

  int j = 0;

  // 2s that divide n
  if (n % 2 == 0)
  {
    primeFactors[j++] = 2;
    while (n % 2 == 0)
      n >>= 1;
  }

  // N must be odd at this point
  // Skip one element
  for (int i = 3;
           i * i <= n; i += 2)
  {
    if (n % i == 0)
    {
      // Update the prime factor
      primeFactors[j++] = i;
      while (n % i == 0)
        n /= i;
    }
  }

  // If n is a prime number
  // greater than 2
  if (n > 2)
    primeFactors[j++] = n;

  int []temp = new int[j];
  Array.Copy(primeFactors, temp, j);
  return temp;
}

// Function that finds the shortest
// subsequence
private static void findShortestSubsequence(int[] dp, int[] a,
                                            int index,
                                            int[] primeFactors)
{
  int n = a.Length;

  for (int j = index; j < n; j++)
  {
    int bitmask = 0;

    for (int p = 0;
             p < primeFactors.Length; p++)
    {
      // Check if the prime factor
      // of first number, is also
      // the prime factor of the
      // rest numbers in array
      if (a[j] % primeFactors[p] == 0)
      {
        // Set corresponding bit
        // of prime factor to 1,
        // it means both these
        // numbers have the
        // same prime factor
        bitmask ^= (1 << p);
      }
    }

    for (int i = 0;
             i < dp.Length; i++)
    {
      // If no states encountered
      // so far continue for this
      // combination of bits
      if (dp[i] == n + 1)
        continue;

      // Update this state with
      // minimum ways to reach
      // this state
      dp[bitmask & i] = Math.Min(dp[bitmask & i],
                                 dp[i] + 1);
    }
  }
}

// Function that print the minimum
// length of subsequence
private static void printMinimumLength(int[] a)
{
  int min = a.Length + 1;

  for (int i = 0;
           i < a.Length - 1; i++)
  {
    // Find the prime factors of
    // the first number
    int[] primeFactors = findPrimeFactors(a[i]);

    int n = primeFactors.Length;

    int[] dp = new int[1 << n];

    // Initialize the array with
    // maximum steps, size of the
    // array + 1 for instance
    for(i = 0; i < dp.Length; i++)
      dp[i] = a.Length + 1;

    // Express the prime factors
    // in bit representation

    // Total number of set bits is
    // equal to the total number
    // of prime factors
    int setBits = (1 << n) - 1;

    // Indicates there is one
    // way to reach the number
    // under consideration
    dp[setBits] = 1;
    findShortestSubsequence(dp, a, i + 1,
                            primeFactors);

    // State 0 corresponds
    // to gcd of 1
    min = Math.Min(dp[0], min);
  }

  // If not found such subsequence
  // then print "-1"
  if (min == a.Length + 1)
    Console.WriteLine(-1);

  // Else print the length
  else
    Console.WriteLine(min);
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int[] arr = {2, 6, 12, 3};

  // Function Call
  printMinimumLength(arr);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function that finds the prime
// factors of a number
function findPrimeFactors(n)
{
    // To store the prime factor
    let primeFactors = new Array(9).fill(0);

    let j = 0;

    // 2s that divide n
    if (n % 2 == 0) {
        primeFactors[j++] = 2;
        while (n % 2 == 0)
            n >>= 1;
    }

    // N must be odd at this point
    // Skip one element
    for (let i = 3;
        i * i <= n; i += 2) {

        if (n % i == 0) {

            // Update the prime factor
            primeFactors[j++] = i;
            while (n % i == 0)
                n /= i;
        }
    }

    // If n is a prime number
    // greater than 2
    if (n > 2)
        primeFactors[j++] = n;

    let PrimeFactors = new Array(j);

    for(let i = 0; i < j; i++)
    {
        PrimeFactors[i] = primeFactors[i];
    }

    return PrimeFactors;
}

// Function that finds the shortest
// subsequence
function findShortestSubsequence(dp, a, index, primeFactors)
{
    let n = a.length;

    for (let j = index; j < n; j++) {
        let bitmask = 0;

        for (let p = 0;
            p < primeFactors.length; p++) {

            // Check if the prime factor
            // of first number, is also
            // the prime factor of the
            // rest numbers in array
            if ((a[j] % primeFactors[p]) == 0) {

                // Set corresponding bit
                // of prime factor to 1,
                // it means both these
                // numbers have the
                // same prime factor
                bitmask ^= (1 << p);
            }
        }

        for (let i = 0; i < dp.length; i++) {

            // If no states encountered
            // so far continue for this
            // combination of bits
            if (dp[i] == n + 1)
                continue;

            // Update this state with
            // minimum ways to reach
            // this state
            dp[bitmask & i]
                = Math.min(dp[bitmask & i], dp[i] + 1);
        }
    }
}

// Function that print the minimum
// length of subsequence
function prletMinimumLength(a)
{
    let Min = a.length + 1;

    for (let i = 0; i < a.length - 1; i++) {

        // Find the prime factors of
        // the first number
        let primeFactors = findPrimeFactors(a[i]);

        let n = primeFactors.length;

        // Initialize the array with
        // maximum steps, size of the
        // array + 1 for instance
        let dp = new Array(1 << n);

        for(let i = 0; i < dp.length; i++){
            dp[i] = a.length + 1
        }

        // Express the prime factors
        // in bit representation

        // Total number of set bits is
        // equal to the total number
        // of prime factors
        let setBits = (1 << n) - 1;

        // Indicates there is one
        // way to reach the number
        // under consideration
        dp[setBits] = 1;
        findShortestSubsequence(dp, a, i + 1,
                                primeFactors);

        // State 0 corresponds
        // to gcd of 1
        Min = Math.min(dp[0], Min);
    }

    // If not found such subsequence
    // then print "-1"
    if (Min == (a.length + 1))
        document.write(-1 + "<br>");

    // Else print the length
    else
        document.write(Min + "<br>");
}

// Driver code

    // Given array arr[]
    let arr = [ 2, 6, 12, 3 ];

    // Function Call
    prletMinimumLength(arr);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output**

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*