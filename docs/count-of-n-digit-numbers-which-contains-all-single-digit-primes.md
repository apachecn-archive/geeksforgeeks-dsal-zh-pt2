# 包含所有一位数素数的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/n 位数计数-包含所有个位数的素数/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-which-contains-all-single-digit-primes/)

给定一个正整数 **N** ，任务是统计包含**所有**个一位数[素数](https://www.geeksforgeeks.org/prime-numbers/)的 **N** 位数。

**示例:**

> **输入:** N = 4
> **输出:** 24
> **说明:**一位数素数为 4 即{2，3，5，7}。因此，在 4 个地方排列 4 个数字的方法数是 4！= 24.
> 
> **输入:**N = 5
> T3】输出: 936

**天真方法:**解决给定问题的最简单方法是生成所有可能的 **N** 位数，并对包含所有个位数[质数](https://www.geeksforgeeks.org/prime-numbers/)的数字进行计数。检查所有数字后，打印**计数的值**作为数字的总计数。

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构。](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)子问题可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储在 **dp[][]表**中，其中 **dp[index][mask]** 存储从 **index <sup>th</sup>** 位置到结束的答案，其中 **mask** 用于存储到目前为止包含的不同[素数](https://www.geeksforgeeks.org/prime-numbers/)的计数。按照以下步骤解决问题:

*   初始化全局[多维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**DP【100】【1】<<4】**，所有值为 **-1** ，存储每个[递归调用](https://www.geeksforgeeks.org/recursion/)的结果。
*   **使用[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) **以升序索引所有的一位数[质数](https://www.geeksforgeeks.org/prime-numbers/)。****
*   通过执行以下步骤，定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**数(索引，掩码，N)** 。
    *   如果一个指标的值等于**(N+1)**
        *   通过查找掩码中设置位的**计数，计算包含的不同单个数字[素数](https://www.geeksforgeeks.org/prime-numbers/)的数量。**
        *   如果计数等于 **4** ，则返回 **1** 作为已经形成的有效 **N** 位数。
        *   否则返回 **0** 。
    *   如果状态 **dp【索引】【掩码】**的结果已经计算出来，则返回该值 **dp【索引】【掩码】**。
    *   如果当前**索引**为 **1** ，则可以放置来自**【1-9】**的任意数字，如果 **N = 1** ，则也可以放置 **0** 。
    *   对于所有其他索引，可以放置从**【0-9】**开始的任何数字。
    *   如果当前放置的数字是一个[质数](https://www.geeksforgeeks.org/prime-numbers/)，那么在位掩码中将[质数](https://www.geeksforgeeks.org/prime-numbers/)的**索引**设置为 **1** 。
    *   进行有效放置后，**递归调用**(索引+ 1)** 的**计数**函数。**
    *   返回所有可能的有效数字位置的[和](https://www.geeksforgeeks.org/sum-function-python/)作为答案。
*   打印函数**返回的数值作为结果。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the dp-states
int dp[100][1 << 4];

// Stores the index of prime numbers
map<int, int> primeIndex;

int countOfNumbers(int index, int mask, int N)
{
    // If index = N+1
    if (index == N + 1) {

        // Find count of distinct
        // prime numbers by counting
        // number of set bits.
        int countOfPrimes = __builtin_popcount(mask);

        // If count of distinct
        // prime numbers is equal to 4
        // return 1.
        if (countOfPrimes == 4) {
            return 1;
        }
        return 0;
    }

    int& val = dp[index][mask];

    // If the state has
    // already been computed
    if (val != -1) {
        return val;
    }

    val = 0;

    // If current position is 1,
    // then any digit from [1-9] can be placed.
    // If N = 1, 0 can be also placed.
    if (index == 1) {
        for (int digit = (N == 1 ? 0 : 1); digit <= 9;
             ++digit) {

            // If the digit is a prime number,
            // set the index of the
            // digit to 1 in the bitmask.
            if (primeIndex.find(digit)
                != primeIndex.end()) {
                val += countOfNumbers(
                    index + 1,
                    mask | (1 << primeIndex[digit]), N);
            }

            else {
                val += countOfNumbers(index + 1, mask, N);
            }
        }
    }

    // For remaining positions,
    // any digit from [0-9] can be placed
    else {
        for (int digit = 0; digit <= 9; ++digit) {

            // If the digit is a prime number,
            // set the index of the
            // digit to 1 in the bitmask.
            if (primeIndex.find(digit)
                != primeIndex.end()) {
                val += countOfNumbers(
                    index + 1,
                    mask | (1 << primeIndex[digit]), N);
            }

            else {
                val += countOfNumbers(index + 1, mask, N);
            }
        }
    }

    // Return the answer.
    return val;
}

// Driver Code
int main()
{
    // Initializing dp array with -1.
    memset(dp, -1, sizeof dp);

    // Indexing prime numbers in
    // ascending order
    primeIndex[2] = 0;
    primeIndex[3] = 1;
    primeIndex[5] = 2;
    primeIndex[7] = 3;

    // Given Input
    int N = 4;

    // Function call.
    cout << countOfNumbers(1, 0, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

public static int[][] dp = new int[100][(1 << 4)];

// Stores the index of prime numbers
public static HashMap<Integer,
                      Integer> primeIndex = new HashMap<>();

public static int countSetBits(int n)
{
    int count = 0;

    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

public static int countOfNumbers(int index, int mask,
                                 int N)
{

    // If index = N+1
    if (index == N + 1)
    {

        // Find count of distinct
        // prime numbers by counting
        // number of set bits.
        int countOfPrimes = countSetBits(mask);

        // If count of distinct
        // prime numbers is equal to 4
        // return 1.
        if (countOfPrimes == 4)
        {
            return 1;
        }
        return 0;
    }

    int val = dp[index][mask];

    // If the state has
    // already been computed
    if (val != -1)
    {
        return val;
    }

    val = 0;

    // If current position is 1, then any
    // digit from [1-9] can be placed.
    // If N = 1, 0 can be also placed.
    if (index == 1)
    {
        for(int digit = (N == 1 ? 0 : 1);
                digit <= 9; ++digit)
        {

            // If the digit is a prime number,
            // set the index of the digit to 1
            // in the bitmask.
            if (primeIndex.containsKey(digit))
            {
                int newMask = mask | (1 << primeIndex.get(digit));
                val += countOfNumbers(index + 1,
                                      newMask, N);
            }

            else
            {
                val += countOfNumbers(index + 1, mask, N);
            }
        }
    }

    // For remaining positions,
    // any digit from [0-9] can be placed
    else
    {
        for(int digit = 0; digit <= 9; ++digit)
        {

            // If the digit is a prime number,
            // set the index of the digit to 1
            // in the bitmask.
            if (primeIndex.containsKey(digit))
            {
                int newMask = mask | (1 << primeIndex.get(digit));
                val += countOfNumbers(index + 1, newMask, N);
            }
            else
            {
                val += countOfNumbers(index + 1, mask, N);
            }
        }
    }

    // Return the answer.
    return val;
}

// Driver Code
public static void main(String[] args)
{

    // Initializing dp array with -1.
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < (1 << 4); j++)
        {
            dp[i][j] = -1;
        }
    }

    // Indexing prime numbers in
    // ascending order
    primeIndex.put(2, 0);
    primeIndex.put(3, 1);
    primeIndex.put(5, 2);
    primeIndex.put(7, 3);

    // Given Input
    int N = 4;

    // Function call
    System.out.println(countOfNumbers(1, 0, N));
}
}

// This code is contributed by maddler
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the dp-states
dp = [[-1 for i in range(1<<4)] for j in range(100)]

# Stores the index of prime numbers
primeIndex = {}

def  countSetBits(n):
    count = 0
    while (n):
        count += n & 1
        n >>= 1
    return count

def countOfNumbers(index, mask, N):
    # If index = N+1
    if (index == N + 1):

        # Find count of distinct
        # prime numbers by counting
        # number of set bits.
        countOfPrimes = countSetBits(mask);

        # If count of distinct
        # prime numbers is equal to 4
        # return 1.
        if (countOfPrimes == 4):
            return 1
        return 0

    val = dp[index][mask]

    # If the state has
    # already been computed
    if (val != -1):
        return val

    val = 0

    # If current position is 1,
    # then any digit from [1-9] can be placed.
    # If N = 1, 0 can be also placed.
    if (index == 1):
        digit = 0 if N == 1 else 1
        while(digit <= 9):
            # If the digit is a prime number,
            # set the index of the
            # digit to 1 in the bitmask.
            if (digit in primeIndex):
                val += countOfNumbers(index + 1,mask | (1 << primeIndex[digit]), N)

            else:
                val += countOfNumbers(index + 1, mask, N)

            digit += 1

    # For remaining positions,
    # any digit from [0-9] can be placed
    else:
        for digit in range(10):
            # If the digit is a prime number,
            # set the index of the
            # digit to 1 in the bitmask.
            if (digit in primeIndex):
                val += countOfNumbers(index + 1,mask | (1 << primeIndex[digit]), N)

            else:
                val += countOfNumbers(index + 1, mask, N)

    # Return the answer.
    return val

# Driver Code
if __name__ == '__main__':
    # Initializing dp array with -1.
    # Indexing prime numbers in
    # ascending order
    primeIndex[2] = 0
    primeIndex[3] = 1
    primeIndex[5] = 2
    primeIndex[7] = 3

    # Given Input
    N = 4

    # Function call.
    print(countOfNumbers(1, 0, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

public static int[,] dp = new int[100,(1 << 4)];

// Stores the index of prime numbers
public static Dictionary<int,int> primeIndex = new Dictionary<int,int>();

public static int countSetBits(int n)
{
    int count = 0;

    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

public static int countOfNumbers(int index, int mask,
                                 int N)
{

    // If index = N+1
    if (index == N + 1)
    {

        // Find count of distinct
        // prime numbers by counting
        // number of set bits.
        int countOfPrimes = countSetBits(mask);

        // If count of distinct
        // prime numbers is equal to 4
        // return 1.
        if (countOfPrimes == 4)
        {
            return 1;
        }
        return 0;
    }

    int val = dp[index,mask];

    // If the state has
    // already been computed
    if (val != -1)
    {
        return val;
    }

    val = 0;

    // If current position is 1, then any
    // digit from [1-9] can be placed.
    // If N = 1, 0 can be also placed.
    if (index == 1)
    {
        for(int digit = (N == 1 ? 0 : 1);
                digit <= 9; ++digit)
        {

            // If the digit is a prime number,
            // set the index of the digit to 1
            // in the bitmask.
            if (primeIndex.ContainsKey(digit))
            {
                int newMask = mask | (1 << primeIndex[digit]);
                val += countOfNumbers(index + 1,
                                      newMask, N);
            }

            else
            {
                val += countOfNumbers(index + 1, mask, N);
            }
        }
    }

    // For remaining positions,
    // any digit from [0-9] can be placed
    else
    {
        for(int digit = 0; digit <= 9; ++digit)
        {

            // If the digit is a prime number,
            // set the index of the digit to 1
            // in the bitmask.
            if (primeIndex.ContainsKey(digit))
            {
                int newMask = mask | (1 << primeIndex[digit]);
                val += countOfNumbers(index + 1, newMask, N);
            }
            else
            {
                val += countOfNumbers(index + 1, mask, N);
            }
        }
    }

    // Return the answer.
    return val;
}

// Driver Code
public static void Main(String[] args)
{

    // Initializing dp array with -1.
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < (1 << 4); j++)
        {
            dp[i,j] = -1;
        }
    }

    // Indexing prime numbers in
    // ascending order
    primeIndex.Add(2, 0);
    primeIndex.Add(3, 1);
    primeIndex.Add(5, 2);
    primeIndex.Add(7, 3);

    // Given Input
    int N = 4;

    // Function call
    Console.WriteLine(countOfNumbers(1, 0, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let dp = new Array(100).fill(0).map(() => new Array(1 << 4));

// Stores the index of prime numbers
let primeIndex = new Map();

function countSetBits(n) {
  let count = 0;

  while (n > 0) {
    count += n & 1;
    n >>= 1;
  }
  return count;
}

function countOfNumbers(index, mask, N) {
  // If index = N+1
  if (index == N + 1) {
    // Find count of distinct
    // prime numbers by counting
    // number of set bits.
    let countOfPrimes = countSetBits(mask);

    // If count of distinct
    // prime numbers is equal to 4
    // return 1.
    if (countOfPrimes == 4) {
      return 1;
    }
    return 0;
  }

  let val = dp[index][mask];

  // If the state has
  // already been computed
  if (val != -1) {
    return val;
  }

  val = 0;

  // If current position is 1, then any
  // digit from [1-9] can be placed.
  // If N = 1, 0 can be also placed.
  if (index == 1) {
    for (let digit = N == 1 ? 0 : 1; digit <= 9; ++digit) {
      // If the digit is a prime number,
      // set the index of the digit to 1
      // in the bitmask.
      if (primeIndex.has(digit)) {
        let newMask = mask | (1 << primeIndex.get(digit));
        val += countOfNumbers(index + 1, newMask, N);
      } else {
        val += countOfNumbers(index + 1, mask, N);
      }
    }
  }

  // For remaining positions,
  // any digit from [0-9] can be placed
  else {
    for (let digit = 0; digit <= 9; ++digit) {
      // If the digit is a prime number,
      // set the index of the digit to 1
      // in the bitmask.
      if (primeIndex.has(digit)) {
        let newMask = mask | (1 << primeIndex.get(digit));
        val += countOfNumbers(index + 1, newMask, N);
      } else {
        val += countOfNumbers(index + 1, mask, N);
      }
    }
  }

  // Return the answer.
  return val;
}

// Driver Code

// Initializing dp array with -1.
for (let i = 0; i < 100; i++) {
  for (let j = 0; j < 1 << 4; j++) {
    dp[i][j] = -1;
  }
}

// Indexing prime numbers in
// ascending order
primeIndex.set(2, 0);
primeIndex.set(3, 1);
primeIndex.set(5, 2);
primeIndex.set(7, 3);

// Given Input
let N = 4;

// Function call
document.write(countOfNumbers(1, 0, N));

// This code is contributed by gfgking

</script>
```

**Output**

```
24
```

***时间复杂度:**O(N * 10 * 2<sup>4</sup>)*
***辅助空间:** O(N * 2 <sup>4</sup> )*