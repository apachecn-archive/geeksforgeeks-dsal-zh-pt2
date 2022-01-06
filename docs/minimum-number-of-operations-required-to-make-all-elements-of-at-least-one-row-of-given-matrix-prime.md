# 使至少一行给定矩阵的所有元素成为素数所需的最小运算次数

> 原文:[https://www . geeksforgeeks . org/最小操作数-生成给定矩阵素数的至少一行的所有元素所需的操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-make-all-elements-of-at-least-one-row-of-given-matrix-prime/)

给定一个大小为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)、 **mat[][]** ，任务是找到使给定矩阵的至少一行的所有元素成为素数所需的最小运算数。在每个操作中，根据以下条件合并矩阵的任意两行:

*   如果矩阵两行的 **k <sup>第</sup>** 个元素，即**mat【I】【k】**和**mat【j】【k】**是[质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)或[复合数](https://www.geeksforgeeks.org/composite-number/)，则合并行的 **k <sup>第</sup>** 个元素包含**min(mat【I】【k】，mat【j】【k】)**。
*   否则，合并行的第 **k <sup>个</sup>** 元素包含质数元素。

如果无法将一行的所有元素都作为[质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)获得，则打印 **-1** 。

**示例:**

> **输入:** mat[][] = { { 4，6，5 }，{ 2，9，12 }，{ 32，7，18 }，{ 12，4，35 } }
> **输出:** 2
> **解释:**
> 合并 mat[0]和 mat[1]将 mat[[]修改为{ { 2，6，5 }，{ 32，7，18 }，{ 12，4，35 } }
> 合并 mat[1]
> 
> **输入:** mat[][] = { {4，6}，{8，3} }
> **输出:** -1
> **解释:**
> 合并 mat[0]和 mat[1]将 mat[][]修改为{ {4，3 } }
> 由于行中的元素都不是质数，因此所需的输出为-1。

**方法:**使用带有位掩码的[动态编程](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如说**位掩码**，其中**位掩码**的 **i <sup>第</sup>位存储一行的 **i <sup>第</sup>列是否为[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。****
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-java/)，比如说 **dp[]** ，其中 **dp[X]** 存储获得一行素数的 **X** 计数所需的最小操作数。
*   遍历矩阵的每一行，并为每一行更新**位掩码**的值。使用变量 **j** 迭代范围**[(1<<(M–1))、0]** ，并将 **dp[j |位掩码]** 的值更新为 **min(dp[j |位掩码]，dp[j] + 1)** 。
*   最后，检查获得一行 **M** 素数所需的最小操作数是否大于 **N** ，即检查**DP【(1<<(M–1))】**是否大于 **N** 。如果发现属实，则打印 **-1** 。
*   否则，打印**(DP【(1<】T3】(M–1))】–1)**的值。

下面是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to generate all prime
    // numbers using Sieve of Eratosthenes
    private static boolean[] prime;

    // Function to check if a number
    // is prime or not
    private static void sieve(int n)
    {
        // prime[i]: Check if i is a
        // prime number or not
        prime = new boolean[n + 1];

        // Initialize prime[]
        // array to true
        Arrays.fill(prime, true);

        // Iterate over the range
        // [2, sqrt(n)]
        for (int p = 2; p * p <= n;
             p++) {

            // If p is a prime number
            if (prime[p] == true) {

                // Mark all multiples
                // of i to false
                for (int i = p * p;
                     i <= n; i += p)

                    // Update i
                    prime[i] = false;
            }
        }
    }

    // Function to find minimum operations
    // to make all elements of at least one
    // row of the matrix as prime numbers
    private static int MinWays(int[][] a,
                               int n, int m)
    {
        // dp[i]: Stores minimum operations
        // to get i prime numbers in a row
        int[] dp = new int[1 << m];

        // Initialize dp[] array
        // to (n + 1)
        Arrays.fill(dp, n + 1);

        // Traverse the array
        for (int i = 0; i < a.length;
             i++) {

            // Stores count of prime
            // numbers in a i-th row
            int bitmask = BitMask(a[i]);

            // Iterate over the range
            // [(1 << m) - 1, 0]
            for (int j = (1 << m) - 1;
                 j >= 0; j--) {

                // If a row exist which
                // contains j prime numbers
                if (dp[j] != n + 1) {

                    // Update dp[j | bitmask]
                    dp[j | bitmask]
                        = Math.min(dp[j | bitmask],
                                   dp[j] + 1);
                }
            }

            // Update dp[bitmask]
            dp[bitmask] = 1;
        }

        // Return minimum operations to get a row
        // of the matrix with all prime numbers
        return (dp[(1 << m) - 1] - 1) == (n + 1)
            ? -1
            : (dp[(1 << m) - 1] - 1);
    }

    // Function to count prime
    // numbers in a row
    private static int BitMask(int[] a)
    {
        // i-th bit of bitmask check if
        // i-th column is a prime or not
        int bitmask = 0;

        // Traverse the array
        for (int i = 0; i < a.length;
             i++) {

            // if a[i] is a prime number
            if (prime[a[i]]) {

                // Update bitmask
                bitmask |= (1 << i);
            }
        }
        return bitmask;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] mat = { { 4, 6, 5, 8 },
                        { 2, 9, 12, 14 },
                        { 32, 7, 18, 16 },
                        { 12, 4, 35, 17 } };

        // Stores count of columns
        // in the matrix
        int m = mat[0].length;

        // Stores length
        int n = mat.length;

        // Calculate all prime numbers in
        // range [1, max] using sieve
        int max = 10000;
        sieve(max);

        // Function Call
        System.out.println(
            MinWays(mat, n, m));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
from math import sqrt

# Function to generate all prime
# numbers using Sieve of Eratosthenes
prime = [True for i in range(10001)]

# Function to check if a number
# is prime or not
def sieve(n):

    # prime[i]: Check if i is a
    # prime number or not
    global prime

    # Iterate over the range
    # [2, sqrt(n)]
    for p in range(2,int(sqrt(10000)) + 1, 1):

        # If p is a prime number
        if (prime[p] == True):

            # Mark all multiples
            # of i to false
            for i in range(p * p, 10001, p):

                # Update i
                prime[i] = False

# Function to find minimum operations
# to make all elements of at least one
# row of the matrix as prime numbers
def MinWays(a, n, m):

    # dp[i]: Stores minimum operations
    # to get i prime numbers in a row
    dp = [n + 1 for i in range(1 << m)]

    # Traverse the array
    for i in range(len(a)):

        # Stores count of prime
        # numbers in a i-th row
        bitmask = BitMask(a[i])

        # Iterate over the range
        # [(1 << m) - 1, 0]
        j = (1 << m) - 1
        while(j >= 0):

            # If a row exist which
            # contains j prime numbers
            if (dp[j] != n + 1):

                # Update dp[j | bitmask]
                dp[j | bitmask] = min(dp[j | bitmask],dp[j] + 1)
            j -= 1

        # Update dp[bitmask]
        dp[bitmask] = 1

    # Return minimum operations to get a row
    # of the matrix with all prime numbers
    if (dp[(1 << m) - 1] - 1) == (n + 1):
        return -1
    else:
        return (dp[(1 << m) - 1] - 1)

# Function to count prime
# numbers in a row
def BitMask(a):
    global prime

    # i-th bit of bitmask check if
    # i-th column is a prime or not
    bitmask = 0

    # Traverse the array
    for i in range(len(a)):

        # if a[i] is a prime number
        if (prime[a[i]]):

            # Update bitmask
            bitmask |= (1 << i)
    return bitmask

# Driver Code
if __name__ == '__main__':
    mat = [[4, 6, 5, 8],
           [2, 9, 12, 14],
           [32, 7, 18, 16],
           [12, 4, 35, 17]]

    # Stores count of columns
    # in the matrix
    m = len(mat[0])

    # Stores length
    n = len(mat)

    # Calculate all prime numbers in
    # range [1, max] using sieve
    max = 10000
    sieve(max)

    # Function Call
    print(MinWays(mat, n, m))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;

public class GFG
{

  // Function to generate all prime
  // numbers using Sieve of Eratosthenes
  private static bool[] prime;

  // Function to check if a number
  // is prime or not
  private static void sieve(int n)
  {
    // prime[i]: Check if i is a
    // prime number or not
    prime = new bool[n + 1];

    // Initialize prime[]
    // array to true
    for (int i = 0; i < prime.Length; i++)
      prime[i] = true;

    // Iterate over the range
    // [2, sqrt(n)]
    for (int p = 2; p * p <= n;
         p++) {

      // If p is a prime number
      if (prime[p] == true)
      {

        // Mark all multiples
        // of i to false
        for (int i = p * p;
             i <= n; i += p)

          // Update i
          prime[i] = false;
      }
    }
  }

  // Function to find minimum operations
  // to make all elements of at least one
  // row of the matrix as prime numbers
  private static int MinWays(int[,] a,
                             int n, int m)
  {
    // dp[i]: Stores minimum operations
    // to get i prime numbers in a row
    int[] dp = new int[1 << m];

    // Initialize []dp array
    // to (n + 1)
    for (int i = 0; i < dp.Length;i++)
    {
      dp[i] = n + 1;
    }

    // Traverse the array
    for (int i = 0; i < a.GetLength(0);
         i++)
    {

      // Stores count of prime
      // numbers in a i-th row
      int bitmask = BitMask(GetRow(a,i));

      // Iterate over the range
      // [(1 << m) - 1, 0]
      for (int j = (1 << m) - 1;
           j >= 0; j--)
      {

        // If a row exist which
        // contains j prime numbers
        if (dp[j] != n + 1)
        {

          // Update dp[j | bitmask]
          dp[j | bitmask]
            = Math.Min(dp[j | bitmask],
                       dp[j] + 1);
        }
      }

      // Update dp[bitmask]
      dp[bitmask] = 1;
    }

    // Return minimum operations to get a row
    // of the matrix with all prime numbers
    return (dp[(1 << m) - 1] - 1) == (n + 1)
      ? -1
      : (dp[(1 << m) - 1] - 1);
  }

  // Function to count prime
  // numbers in a row
  private static int BitMask(int[] a)
  {
    // i-th bit of bitmask check if
    // i-th column is a prime or not
    int bitmask = 0;

    // Traverse the array
    for (int i = 0; i < a.Length;
         i++) {

      // if a[i] is a prime number
      if (prime[a[i]])
      {

        // Update bitmask
        bitmask |= (1 << i);
      }
    }
    return bitmask;
  }
  public static int[] GetRow(int[,] matrix, int row)
  {
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for (var i = 0; i < rowLength; i++)
      rowVector[i] = matrix[row, i];

    return rowVector;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[,] mat = { { 4, 6, 5, 8 },
                  { 2, 9, 12, 14 },
                  { 32, 7, 18, 16 },
                  { 12, 4, 35, 17 } };

    // Stores count of columns
    // in the matrix
    int m = mat.GetLength(0);

    // Stores length
    int n = mat.GetLength(1);

    // Calculate all prime numbers in
    // range [1, max] using sieve
    int max = 10000;
    sieve(max);

    // Function Call
    Console.WriteLine(
      MinWays(mat, n, m));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // Function to generate all prime
    // numbers using Sieve of Eratosthenes
    let prime = [];

    // Function to check if a number
    // is prime or not
    function sieve(n)
    {
        // prime[i]: Check if i is a
        // prime number or not
        prime = new Array(n + 1);

        // Initialize prime[]
        // array to true
        for (let i = 0; i < prime.length; i++)
              prime[i] = true;

        // Iterate over the range
        // [2, sqrt(n)]
        for (let p = 2; p * p <= n;
             p++) {

            // If p is a prime number
            if (prime[p] == true) {

                // Mark all multiples
                // of i to false
                for (let i = p * p;
                     i <= n; i += p)

                    // Update i
                    prime[i] = false;
            }
        }
    }

    // Function to find minimum operations
    // to make all elements of at least one
    // row of the matrix as prime numbers
     function MinWays(a, n, m)
    {
        // dp[i]: Stores minimum operations
        // to get i prime numbers in a row
        let dp = new Array(1 << m);

        // Initialize dp[] array
        // to (n + 1)
        for (let i = 0; i < dp.length;i++)
        {
              dp[i] = n + 1;
        }

        // Traverse the array
        for (let i = 0; i < a.length;
             i++) {

            // Stores count of prime
            // numbers in a i-th row
            let bitmask = BitMask(a[i]);

            // Iterate over the range
            // [(1 << m) - 1, 0]
            for (let j = (1 << m) - 1;
                 j >= 0; j--) {

                // If a row exist which
                // contains j prime numbers
                if (dp[j] != n + 1) {

                    // Update dp[j | bitmask]
                    dp[j | bitmask]
                        = Math.min(dp[j | bitmask],
                                   dp[j] + 1);
                }
            }

            // Update dp[bitmask]
            dp[bitmask] = 1;
        }

        // Return minimum operations to get a row
        // of the matrix with all prime numbers
        return (dp[(1 << m) - 1] - 1) == (n + 1)
            ? -1
            : (dp[(1 << m) - 1] - 1);
    }

    // Function to count prime
    // numbers in a row
    function BitMask(a)
    {
        // i-th bit of bitmask check if
        // i-th column is a prime or not
        let bitmask = 0;

        // Traverse the array
        for (let i = 0; i < a.length;
             i++) {

            // if a[i] is a prime number
            if (prime[a[i]]) {

                // Update bitmask
                bitmask |= (1 << i);
            }
        }
        return bitmask;
    }

// Driver Code
        let mat = [[ 4, 6, 5, 8 ],
                        [ 2, 9, 12, 14 ],
                        [ 32, 7, 18, 16 ],
                        [ 12, 4, 35, 17 ]];

        // Stores count of columns
        // in the matrix
        let m = mat[0].length;

        // Stores length
        let n = mat.length;

        // Calculate all prime numbers in
        // range [1, max] using sieve
        let max = 10000;
        sieve(max);

        // Function Call
        document.write(
            MinWays(mat, n, m));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(X * log(log(X))+N * M * 2<sup>M</sup>，其中 **X** 是矩阵的最大元素*
***辅助空间:** O(X + 2 <sup>M</sup> )*