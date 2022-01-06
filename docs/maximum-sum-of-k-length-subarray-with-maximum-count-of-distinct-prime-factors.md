# 具有不同素因子最大计数的 K 长度子阵列的最大和

> 原文:[https://www . geeksforgeeks . org/最大 k 长度和-具有最大不同素因子计数的子阵列/](https://www.geeksforgeeks.org/maximum-sum-of-k-length-subarray-with-maximum-count-of-distinct-prime-factors/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是在每个 **K** 长度子数组中寻找具有不同[素因子](https://www.geeksforgeeks.org/prime-factor/)最大和的[子数组中数组元素](https://www.geeksforgeeks.org/tag/subarray/)的最大[和。
***注:**如果有多个答案，则打印具有最大和的原始子阵列的和。*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {1，4，2，10，3}，K = 3
> **输出:** 16
> **解释:**
> 长度为 3 的所有可能的子阵列为:
> {1，4，2} →具有 0+1+1= 2 个不同的素因子
> {4，2，10} →具有 1+1+2= 4 个不同的素因子。总和= 16。
> {2，10，3} →具有 1+1+2= 4 个不同的质因数。总和= 15。
> 因此，具有最大相异素因子的 K 长度子阵的最大和为 16。
> 
> **输入:** arr[] = {10，14，12，9，16，11}，K = 2
> **输出:** 26

**天真方法:**最简单的方法是[从给定的数组中生成所有可能的长度为 **K** 的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并[遍历每个子数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[计算其元素的不同素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，并计算它们的和。最后，打印具有不同质因数的最大计数的子阵列中的最大和。
***时间复杂度:** O(N <sup>3</sup> * sqrt(MAX))，其中 **MAX** 是数组中存在的最大数量。*
***辅助空间:** O(N * sqrt(MAX))*

**高效途径:**最优思路是使用厄拉多塞的[筛和](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[的滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决这个问题。按照以下步骤解决问题:

*   初始化一个数组，比如**CountDistinct[]**，通过每次递增 **CountDistinct[]** 的计数，使用**筛**将不同质因数的计数存储到一个极限，同时将质数的倍数标记为 **false** 。
*   大小为 **K** 的子阵列(或窗口)的和可以使用大小为 **K** 的先前子阵列(或窗口)的和，使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)在恒定时间内获得。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，检查哪个子数组具有不同素数的最大和。
*   最后，打印子阵列的总和或具有最大质因数计数的原始阵列的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 100001

// Function to print the sum of
// subarray of length K having
// maximum distinct prime factors
int maxSum(int arr[], int N, int K)
{
    // If K exceeds N
    if (N < K) {
        cout << "Invalid";
        return -1;
    }

    // Stores the count of distinct primes
    int CountDistinct[MAX + 1];

    // True, if index 'i' is a prime
    bool prime[MAX + 1];

    // Initialize the count of factors
    // to 0 and set all indices as prime
    for (int i = 0; i <= MAX; i++) {
        CountDistinct[i] = 0;
        prime[i] = true;
    }

    for (long long int i = 2; i <= MAX; i++) {

        // If i is prime
        if (prime[i] == true) {

            // Number is prime
            CountDistinct[i] = 1;

            // Count of factors of a prime number is 1
            for (long long int j = i * 2; j <= MAX;
                 j += i) {

                // Increment CountDistinct as
                // the factors of i
                CountDistinct[j]++;

                // Mark its multiple non-prime
                prime[j] = false;
            }
        }
    }

    // Compute sum of first K-length subarray
    int Maxarr_sum = 0, DistPrimeSum = 0;
    for (int i = 0; i < K; i++) {

        Maxarr_sum += arr[i];
        DistPrimeSum += CountDistinct[arr[i]];
    }

    // Compute sums of remaining windows
    // by removing first element of the
    // previous window and adding last
    // element of the current window
    int curr_sum = DistPrimeSum;
    int curr_arrSum = Maxarr_sum;

    for (int i = K; i < N; i++) {

        curr_sum += CountDistinct[arr[i]]
                    - CountDistinct[arr[i - K]];

        curr_arrSum += arr[i] - arr[i - K];
        if (curr_sum > DistPrimeSum) {

            DistPrimeSum = curr_sum;
            Maxarr_sum = curr_arrSum;
        }
        else if (curr_sum == DistPrimeSum) {

            Maxarr_sum = max(
              curr_arrSum, Maxarr_sum);
        }
    }

    // Print the maximum sum
    cout << Maxarr_sum;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 4, 2, 10, 3 };

    // Given  size of subarray
    int K = 3;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    maxSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG
{

  static int MAX = 100001;

  // Function to print the sum of
  // subarray of length K having
  // maximum distinct prime factors
  static void maxSum(int arr[], int N, int K)
  {

    // If K exceeds N
    if (N < K) {
      System.out.println("Invalid");
      return;
    }

    // Stores the count of distinct primes
    int CountDistinct[] = new int[MAX + 1];

    // True, if index 'i' is a prime
    boolean prime[] = new boolean[MAX + 1];

    // Initialize the count of factors
    // to 0 and set all indices as prime
    for (int i = 0; i <= MAX; i++) {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    for (int i = 2; i <= MAX; i++) {

      // If i is prime
      if (prime[i] == true) {

        // Number is prime
        CountDistinct[i] = 1;

        // Count of factors of a prime number is 1
        for (int j = i * 2; j <= MAX; j += i) {

          // Increment CountDistinct as
          // the factors of i
          CountDistinct[j]++;

          // Mark its multiple non-prime
          prime[j] = false;
        }
      }
    }

    // Compute sum of first K-length subarray
    int Maxarr_sum = 0, DistPrimeSum = 0;
    for (int i = 0; i < K; i++) {

      Maxarr_sum += arr[i];
      DistPrimeSum += CountDistinct[arr[i]];
    }

    // Compute sums of remaining windows
    // by removing first element of the
    // previous window and adding last
    // element of the current window
    int curr_sum = DistPrimeSum;
    int curr_arrSum = Maxarr_sum;

    for (int i = K; i < N; i++) {

      curr_sum += CountDistinct[arr[i]]
        - CountDistinct[arr[i - K]];

      curr_arrSum += arr[i] - arr[i - K];
      if (curr_sum > DistPrimeSum) {

        DistPrimeSum = curr_sum;
        Maxarr_sum = curr_arrSum;
      }
      else if (curr_sum == DistPrimeSum) {

        Maxarr_sum
          = Math.max(curr_arrSum, Maxarr_sum);
      }
    }

    // Print the maximum sum
    System.out.println(Maxarr_sum);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 1, 4, 2, 10, 3 };

    // Given  size of subarray
    int K = 3;

    // Size of the array
    int N = arr.length;

    maxSum(arr, N, K);
  }
}

// This code is contributed by Kingash.
```

## C#

```
// C# Program to implement
// the above approach
using System;
public class GFG
{

  static int MAX = 100001;

  // Function to print the sum of
  // subarray of length K having
  // maximum distinct prime factors
  static void maxSum(int []arr, int N, int K)
  {

    // If K exceeds N
    if (N < K) {
      Console.WriteLine("Invalid");
      return;
    }

    // Stores the count of distinct primes
    int []CountDistinct = new int[MAX + 1];

    // True, if index 'i' is a prime
    bool []prime = new bool[MAX + 1];

    // Initialize the count of factors
    // to 0 and set all indices as prime
    for (int i = 0; i <= MAX; i++) {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    for (int i = 2; i <= MAX; i++) {

      // If i is prime
      if (prime[i] == true) {

        // Number is prime
        CountDistinct[i] = 1;

        // Count of factors of a prime number is 1
        for (int j = i * 2; j <= MAX; j += i) {

          // Increment CountDistinct as
          // the factors of i
          CountDistinct[j]++;

          // Mark its multiple non-prime
          prime[j] = false;
        }
      }
    }

    // Compute sum of first K-length subarray
    int Maxarr_sum = 0, DistPrimeSum = 0;
    for (int i = 0; i < K; i++) {

      Maxarr_sum += arr[i];
      DistPrimeSum += CountDistinct[arr[i]];
    }

    // Compute sums of remaining windows
    // by removing first element of the
    // previous window and adding last
    // element of the current window
    int curr_sum = DistPrimeSum;
    int curr_arrSum = Maxarr_sum;

    for (int i = K; i < N; i++) {

      curr_sum += CountDistinct[arr[i]]
        - CountDistinct[arr[i - K]];

      curr_arrSum += arr[i] - arr[i - K];
      if (curr_sum > DistPrimeSum) {

        DistPrimeSum = curr_sum;
        Maxarr_sum = curr_arrSum;
      }
      else if (curr_sum == DistPrimeSum) {

        Maxarr_sum
          = Math.Max(curr_arrSum, Maxarr_sum);
      }
    }

    // Print the maximum sum
    Console.WriteLine(Maxarr_sum);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given array
    int []arr = { 1, 4, 2, 10, 3 };

    // Given  size of subarray
    int K = 3;

    // Size of the array
    int N = arr.Length;

    maxSum(arr, N, K);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let MAX = 100001

// Function to print the sum of
// subarray of length K having
// maximum distinct prime factors
function maxSum(arr, N, K)
{
    // If K exceeds N
    if (N < K) {
        document.write("Invalid");
        return -1;
    }

    // Stores the count of distinct primes
    let CountDistinct = new Array(MAX + 1);

    // True, if index 'i' is a prime
    let prime = new Array(MAX + 1);

    // Initialize the count of factors
    // to 0 and set all indices as prime
    for (let i = 0; i <= MAX; i++) {
        CountDistinct[i] = 0;
        prime[i] = true;
    }

    for (let i = 2; i <= MAX; i++) {

        // If i is prime
        if (prime[i] == true) {

            // Number is prime
            CountDistinct[i] = 1;

            // Count of factors of a prime number is 1
            for (let j = i * 2; j <= MAX;
                j += i) {

                // Increment CountDistinct as
                // the factors of i
                CountDistinct[j]++;

                // Mark its multiple non-prime
                prime[j] = false;
            }
        }
    }

    // Compute sum of first K-length subarray
    let Maxarr_sum = 0, DistPrimeSum = 0;
    for (let i = 0; i < K; i++) {

        Maxarr_sum += arr[i];
        DistPrimeSum += CountDistinct[arr[i]];
    }

    // Compute sums of remaining windows
    // by removing first element of the
    // previous window and adding last
    // element of the current window
    let curr_sum = DistPrimeSum;
    let curr_arrSum = Maxarr_sum;

    for (let i = K; i < N; i++) {

        curr_sum += CountDistinct[arr[i]]
                    - CountDistinct[arr[i - K]];

        curr_arrSum += arr[i] - arr[i - K];
        if (curr_sum > DistPrimeSum) {

            DistPrimeSum = curr_sum;
            Maxarr_sum = curr_arrSum;
        }
        else if (curr_sum == DistPrimeSum) {

            Maxarr_sum = Math.max(curr_arrSum, Maxarr_sum);
        }
    }

    // Print the maximum sum
    document.write(Maxarr_sum);
}

// Driver Code

// Given array
let arr = [ 1, 4, 2, 10, 3 ];

// Given size of subarray
let K = 3;

// Size of the array
let N = arr.length
maxSum(arr, N, K);

</script>
```

**Output**

```
16
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*