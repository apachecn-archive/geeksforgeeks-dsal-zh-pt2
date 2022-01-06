# 最大化 K 个数组元素不同素因子的计数总和

> 原文:[https://www . geeksforgeeks . org/最大化 k 个数组元素的不同素因子的计数总和/](https://www.geeksforgeeks.org/maximize-sum-of-count-of-distinct-prime-factors-of-k-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到 **K** 数组元素的不同[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的**最大可能和**。

**示例:**

> **输入:** arr[] = {6，9，12}，K = 2
> **输出:** 4
> **解释:**
> 6，9，12 的不同素因子是 2，1，2。
> 不同素因子最大的钾元素分别为 6 和 12。因此，它们的计数之和= 2 + 2 = 4。
> 
> **输入:** arr[] = {4，8，10，6}，K = 3
> **输出:** 5
> **解释:**
> 4，8，10，6 的不同素因子是 1，1，2，2。
> 不同素因子最大的钾元素为 4、6、10。因此，它们的计数之和= 1 + 2 + 2 = 5。

**方法:**按照以下步骤解决问题:

*   通过厄拉多塞技术的[筛，初始化一个大小为**10<sup>6</sup>T5 的布尔数组**质数[**]，以存储该数是否质数。**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   初始化一个数组 **CountDistinct[]** 来存储数字的不同质因数的个数。
*   以倍数增加质因数的计数，同时将数字标记为质数。
*   小于**10<sup>6</sup>T3】的数的不同素数的最大个数为 8，即(2×3×5×7×11×13×17×19 = 9699690>10<sup>6</sup>)。**
*   初始化一个变量，比如说**和**来存储 **K** 数组元素的不同质因数的最大和。
*   初始化一个大小为 **20** 的数组**质因数[]** ，以存储所有不同质因数的计数，并将其初始化为 **0** 。
*   现在[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并增加**prime factor【count distinct[arr[I]]++。**
*   从后向遍历数组**素数[]** ，累加求和 K 次，直到变成 0。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000000

// Function to find the maximum sum of count
// of distinct prime factors of K array elements
int maxSumOfDistinctPrimeFactors(int arr[],
                                 int N, int K)
{
    // Stores the count of distinct primes
    int CountDistinct[MAX + 1];

    // Stores 1 and 0 at prime and
    // non-prime indices respectively
    bool prime[MAX + 1];

    // Initialize the count of factors to 0
    for (int i = 0; i <= MAX; i++) {
        CountDistinct[i] = 0;
        prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (long long int i = 2; i <= MAX; i++) {

        if (prime[i] == true) {

            // Count of factors of a
            // prime number is 1
            CountDistinct[i] = 1;

            for (long long int j = i * 2; j <= MAX;
                 j += i) {

                // Increment CountDistinct
                // of all multiples of i
                CountDistinct[j]++;

                // Mark its multiples non-prime
                prime[j] = false;
            }
        }
    }

    // Stores the maximum sum of distinct
    // prime factors of K array elements
    int sum = 0;

    // Stores the count of all distinct
    // prime factors
    int PrimeFactor[20] = { 0 };

    // Traverse the array to find
    // count of all array elements
    for (int i = 0; i < N; i++) {
        PrimeFactor[CountDistinct[arr[i]]]++;
    }

    // Maximum sum of K prime factors
    // of array elements
    for (int i = 19; i >= 1; i--) {

        // Check for the largest prime factor
        while (PrimeFactor[i] > 0) {

            // Increment sum
            sum += i;

            // Decrement its count and K
            PrimeFactor[i]--;
            K--;
            if (K == 0)
                break;
        }
        if (K == 0)
            break;
    }

    // Print the maximum sum
    cout << sum;
}

// Driver code
int main()
{
    // Given array
    int arr[] = { 6, 9, 12 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 2;

    maxSumOfDistinctPrimeFactors(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  public static int MAX = 1000000;

  // Function to find the maximum sum of count
  // of distinct prime factors of K array elements
  static void maxSumOfDistinctPrimeFactors(int[] arr,
                                           int N, int K)
  {
    // Stores the count of distinct primes
    int[] CountDistinct = new int[MAX + 1];

    // Stores 1 and 0 at prime and
    // non-prime indices respectively
    boolean[] prime = new boolean[MAX + 1];

    // Initialize the count of factors to 0
    for (int i = 0; i <= MAX; i++)
    {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (int i = 2; i <= MAX; i++)
    {

      if (prime[i] == true)
      {

        // Count of factors of a
        // prime number is 1
        CountDistinct[i] = 1;
        for (int j = i * 2; j <= MAX; j += i)
        {

          // Increment CountDistinct
          // of all multiples of i
          CountDistinct[j]++;

          // Mark its multiples non-prime
          prime[j] = false;
        }
      }
    }

    // Stores the maximum sum of distinct
    // prime factors of K array elements
    int sum = 0;

    // Stores the count of all distinct
    // prime factors
    int[] PrimeFactor = new int[20];

    // Traverse the array to find
    // count of all array elements
    for (int i = 0; i < N; i++)
    {
      PrimeFactor[CountDistinct[arr[i]]]++;
    }

    // Maximum sum of K prime factors
    // of array elements
    for (int i = 19; i >= 1; i--)
    {

      // Check for the largest prime factor
      while (PrimeFactor[i] > 0)
      {

        // Increment sum
        sum += i;

        // Decrement its count and K
        PrimeFactor[i]--;
        K--;
        if (K == 0)
          break;
      }
      if (K == 0)
        break;
    }

    // Print the maximum sum
    System.out.print(sum);
  }

  // Driver code
  public static void main(String[] args)
  {
    // Given array
    int[] arr = { 6, 9, 12 };

    // Size of the array
    int N = arr.length;

    // Given value of K
    int K = 2;

    maxSumOfDistinctPrimeFactors(arr, N, K);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

MAX = 1000000

# Function to find the maximum sum of count
# of distinct prime factors of K array elements
def maxSumOfDistinctPrimeFactors(arr, N, K):

    # Stores the count of distinct primes
    CountDistinct = [0]*(MAX + 1)

    # Stores 1 and 0 at prime and
    # non-prime indices respectively
    prime = [False]*(MAX + 1)

    # Initialize the count of factors to 0
    for i in range(MAX + 1):
        CountDistinct[i] = 0
        prime[i] = True

    # Sieve of Eratosthenes
    for i in range(2, MAX + 1):
        if (prime[i] == True):

            # Count of factors of a
            # prime number is 1
            CountDistinct[i] = 1
            for j in range(i * 2,  MAX + 1, i):

                # Increment CountDistinct
                # of all multiples of i
                CountDistinct[j] += 1

                # Mark its multiples non-prime
                prime[j] = False

    # Stores the maximum sum of distinct
    # prime factors of K array elements
    sum = 0

    # Stores the count of all distinct
    # prime factors
    PrimeFactor = [0]*20

    # Traverse the array to find
    # count of all array elements
    for i in range(N):
        PrimeFactor[CountDistinct[arr[i]]] += 1

    # Maximum sum of K prime factors
    # of array elements
    for i in range(19, 0, -1):

        # Check for the largest prime factor
        while (PrimeFactor[i] > 0):

            # Increment sum
            sum += i

            # Decrement its count and K
            PrimeFactor[i] -= 1
            K -= 1
            if (K == 0):
                break
        if (K == 0):
            break

    # Print the maximum sum
    print(sum)

# Driver code
if __name__ == "__main__":

    # Given array
    arr = [6, 9, 12]

    # Size of the array
    N = len(arr)

    # Given value of K
    K = 2

    maxSumOfDistinctPrimeFactors(arr, N, K)

    # This code is contributed by chitranayal.
```

## C#

```
using System;

public class GFG {

  public static int MAX = 1000000;

  // Function to find the maximum sum of count
  // of distinct prime factors of K array elements
  static void maxSumOfDistinctPrimeFactors(int[] arr,
                                           int N, int K)
  {
    // Stores the count of distinct primes
    int[] CountDistinct = new int[MAX + 1];

    // Stores 1 and 0 at prime and
    // non-prime indices respectively
    bool [] prime = new bool[MAX + 1];

    // Initialize the count of factors to 0
    for (int i = 0; i <= MAX; i++) {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (int i = 2; i <= MAX; i++) {

      if (prime[i] == true) {

        // Count of factors of a
        // prime number is 1
        CountDistinct[i] = 1;

        for (int j = i * 2; j <= MAX; j += i) {

          // Increment CountDistinct
          // of all multiples of i
          CountDistinct[j]++;

          // Mark its multiples non-prime
          prime[j] = false;
        }
      }
    }

    // Stores the maximum sum of distinct
    // prime factors of K array elements
    int sum = 0;

    // Stores the count of all distinct
    // prime factors
    int[] PrimeFactor = new int[20];

    // Traverse the array to find
    // count of all array elements
    for (int i = 0; i < N; i++) {
      PrimeFactor[CountDistinct[arr[i]]]++;
    }

    // Maximum sum of K prime factors
    // of array elements
    for (int i = 19; i >= 1; i--) {

      // Check for the largest prime factor
      while (PrimeFactor[i] > 0) {

        // Increment sum
        sum += i;

        // Decrement its count and K
        PrimeFactor[i]--;
        K--;
        if (K == 0)
          break;
      }
      if (K == 0)
        break;
    }

    // Print the maximum sum
    Console.Write(sum);
  }

  // Driver code
  static public void Main()
  {

    // Given array
    int[] arr = { 6, 9, 12 };

    // Size of the array
    int N = arr.Length;

    // Given value of K
    int K = 2;

    maxSumOfDistinctPrimeFactors(arr, N, K);
  }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program of the above approach

let MAX = 1000000;

  // Function to find the maximum sum of count
  // of distinct prime factors of K array elements
  function maxSumOfDistinctPrimeFactors( arr, N, K)
  {
    // Stores the count of distinct primes
    let CountDistinct = [];
    for (let i = 0; i <= MAX ; i++)
    {
        CountDistinct[i] = 0;
    }

    // Stores 1 and 0 at prime and
    // non-prime indices respectively
    let prime = [];
    for (let i = 0; i <= MAX ; i++)
    {
        prime[i] = 0;
    }

    // Initialize the count of factors to 0
    for (let i = 0; i <= MAX; i++)
    {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (let i = 2; i <= MAX; i++)
    {

      if (prime[i] == true)
      {

        // Count of factors of a
        // prime number is 1
        CountDistinct[i] = 1;
        for (let j = i * 2; j <= MAX; j += i)
        {

          // Increment CountDistinct
          // of all multiples of i
          CountDistinct[j]++;

          // Mark its multiples non-prime
          prime[j] = false;
        }
      }
    }

    // Stores the maximum sum of distinct
    // prime factors of K array elements
    let sum = 0;

    // Stores the count of all distinct
    // prime factors
    let PrimeFactor = [];
    for (let i = 0; i <= 20 ; i++)
    {
        PrimeFactor[i] = 0;
    }

    // Traverse the array to find
    // count of all array elements
    for (let i = 0; i < N; i++)
    {
      PrimeFactor[CountDistinct[arr[i]]]++;
    }

    // Maximum sum of K prime factors
    // of array elements
    for (let i = 19; i >= 1; i--)
    {

      // Check for the largest prime factor
      while (PrimeFactor[i] > 0)
      {

        // Increment sum
        sum += i;

        // Decrement its count and K
        PrimeFactor[i]--;
        K--;
        if (K == 0)
          break;
      }
      if (K == 0)
        break;
    }

    // Print the maximum sum
    document.write(sum);
  }

    // Driver Code

     // Given array
    let arr = [ 6, 9, 12 ];

    // Size of the array
    let N = arr.length;

    // Given value of K
    let K = 2;

    maxSumOfDistinctPrimeFactors(arr, N, K);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(MAX)*