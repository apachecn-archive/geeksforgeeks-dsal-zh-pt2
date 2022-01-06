# 从具有不同质因数的偶数乘积的数组中计数对

> 原文:[https://www . geeksforgeeks . org/从具有不同素数因子的偶数乘积的数组中计数对/](https://www.geeksforgeeks.org/count-pairs-from-an-array-with-even-product-of-count-of-distinct-prime-factors/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是对成对的 **(A[i]，B[j])** 进行计数，使得它们的[计数的不同素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的乘积为偶数。

**示例:**

> **输入:** A[] = {1，2，3}，B[] = {4，5，6}，N = 3，M = 3
> T3】输出:2
> T6】解释:
> 
> *   用不同质因数的计数替换所有数组元素会将数组修改为 A[] = {0，1，1}和 B[] = {1，1，2}。
> *   因此，具有偶数乘积的总对是{{2，6}，{3，6}}。
> 
> **输入:** A[] = {1，7}，B[] = {5，6}，N = 2，M = 2
> **输出:** 1
> **解释:**
> 
> *   用不同质因数的计数替换所有数组元素会将数组修改为 A[] = {0，1}和 B[] = {1，2}。
> *   因此，具有偶数乘积的总对是{7，6}。

**天真方法:**最简单的方法是[从两个数组中生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(A[i]，B[j])** ，对于每个对，计算数组元素的不同质数因子[的](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)[计数，并检查它们的乘积是否为偶数。如果发现为真，则增加这种对的计数。](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)

***时间复杂度:**O(N<sup>5/2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过预先计算[从两个数组到](https://www.geeksforgeeks.org/number-of-distinct-prime-factors-of-first-n-natural-numbers/)最大元素的所有数字的不同质因数的计数来优化，并使用两个数字乘积的以下性质:

> *   **Odd * Odd = Odd**
> 
> **偶*奇=偶**
> 
> *   **odd * even = even**
> *   Even * even = even

按照以下步骤解决问题:

*   首先，[计算所有数字](https://www.geeksforgeeks.org/number-of-distinct-prime-factors-of-first-n-natural-numbers/)到 MAX 的相异素因子，并将其存储在[向量< int >](https://www.geeksforgeeks.org/vector-in-cpp-stl/) 表示 **countDistinct。**
*   初始化两个变量，比如 **evenCount** 和 **oddCount，**将数组元素不同素因子的偶数和奇数计数存储在 **B[]** 中。
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【B】。如果， **countDistinct[B[i]] = 0** ，跳过这一步。如果是奇数，将**奇数**增加 1。否则，将**偶数**增加 1。
*   初始化一个变量**将**偶连到 **0** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** ，如果**count distinct【A[I]】**为奇数，则将 **evenPairs** 增加 **evenCount** 。
*   否则，将**偶数对**增加**偶数+奇数。**
*   打印**偶数对的值。**

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000

// Function to calculate count of
// distinct prime factors of a number
void countOfPrimefactors(vector<int>& CountDistinct)
{
    bool prime[MAX + 1];

    for (int i = 0; i <= MAX; i++) {
        CountDistinct[i] = 0;
        prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (long long int i = 2; i <= MAX; i++) {

        if (prime[i] == true) {
            CountDistinct[i] = 1;

            for (long long int j = i * 2; j <= MAX;
                 j += i) {

                CountDistinct[j]++;
                prime[j] = false;
            }
        }
    }
}

// Function to count pairs with even
// product of distinct prime factors
int CountEvenPair(int A[], int B[], int N, int M)
{
    // Stores count of
    // distinct prime factors
    vector<int> countDistinct(MAX + 1);

    countOfPrimefactors(countDistinct);

    // Stores the count of numbers
    // with even prime factors in B[]
    int evenCount = 0;

    // Stores the count of numbers
    // with odd prime factors in B[]
    int oddCount = 0;

    // Even Product Pairs
    int evenPairs = 0;

    // Traverse the array B[]
    for (int i = 0; i < M; i++) {

        // Since, product has to be
        // positive i.e > 0

        if (countDistinct[B[i]] == 0)
            continue;

        // If count of prime factors is odd
        if (countDistinct[B[i]] & 1) {

            // Increment oddCount by 1
            oddCount++;
        }
        else {

            // Increment evenCount by 1
            evenCount++;
        }
    }

    for (int i = 0; i < N; i++) {

        // Since, product has to be
        // positive i.e > 0

        if (countDistinct[A[i]] == 0)
            continue;

        // If count of prime factors is odd
        if (countDistinct[A[i]] & 1) {

            // odd * even = even
            evenPairs += (evenCount);
        }

        // If count of prime factors is even
        else {

            // even * odd = even
            // even * even = even
            evenPairs += evenCount + oddCount;
        }
    }

    return evenPairs;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3 };
    int B[] = { 4, 5, 6 };

    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    cout << CountEvenPair(A, B, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  static int MAX = 1000000;

  // Function to calculate count of
  // distinct prime factors of a number
  static void countOfPrimefactors(int[] CountDistinct)
  {
    boolean[]  prime = new boolean[MAX + 1];

    for (int i = 0; i <= MAX; i++) {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (int i = 2; i <= MAX; i++) {

      if (prime[i] == true) {
        CountDistinct[i] = 1;

        for (int j = i * 2; j <= MAX;
             j += i) {

          CountDistinct[j]++;
          prime[j] = false;
        }
      }
    }
  }

  // Function to count pairs with even
  // product of distinct prime factors
  static int CountEvenPair(int A[], int B[], int N, int M)
  {
    // Stores count of
    // distinct prime factors
    int[] countDistinct = new int[(MAX + 1)];

    countOfPrimefactors(countDistinct);

    // Stores the count of numbers
    // with even prime factors in B[]
    int evenCount = 0;

    // Stores the count of numbers
    // with odd prime factors in B[]
    int oddCount = 0;

    // Even Product Pairs
    int evenPairs = 0;

    // Traverse the array B[]
    for (int i = 0; i < M; i++) {

      // Since, product has to be
      // positive i.e > 0

      if (countDistinct[B[i]] == 0)
        continue;

      // If count of prime factors is odd
      if ((countDistinct[B[i]] & 1) != 0) {

        // Increment oddCount by 1
        oddCount++;
      }
      else {

        // Increment evenCount by 1
        evenCount++;
      }
    }

    for (int i = 0; i < N; i++) {

      // Since, product has to be
      // positive i.e > 0

      if (countDistinct[A[i]] == 0)
        continue;

      // If count of prime factors is odd
      if ((countDistinct[A[i]] & 1) != 0) {

        // odd * even = even
        evenPairs += (evenCount);
      }

      // If count of prime factors is even
      else {

        // even * odd = even
        // even * even = even
        evenPairs += evenCount + oddCount;
      }
    }
    return evenPairs;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int A[] = { 1, 2, 3 };
    int B[] = { 4, 5, 6 };

    int N = A.length;
    int M = B.length;

    System.out.println(CountEvenPair(A, B, N, M));
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach
MAX = 1000000

# Function to calculate count of
# distinct prime factors of a number
def countOfPrimefactors(CountDistinct):
    global MAX
    prime = [0 for i in range(MAX + 1)]

    for i in range(MAX+1):
        CountDistinct[i] = 0
        prime[i] = True

    # Sieve of Eratosthenes
    for i in range(2,MAX+1,1):
        if (prime[i] == True):
            CountDistinct[i] = 1

            for j in range(i * 2,MAX+1,i):
                CountDistinct[j] += 1
                prime[j] = False

# Function to count pairs with even
# product of distinct prime factors
def CountEvenPair(A, B, N, M):
    global MAX

    # Stores count of
    # distinct prime factors
    countDistinct = [0 for i in range(MAX + 1)]
    countOfPrimefactors(countDistinct)

    # Stores the count of numbers
    # with even prime factors in B[]
    evenCount = 0

    # Stores the count of numbers
    # with odd prime factors in B[]
    oddCount = 0

    # Even Product Pairs
    evenPairs = 0

    # Traverse the array B[]
    for i in range(M):

        # Since, product has to be
        # positive i.e > 0
        if (countDistinct[B[i]] == 0):
            continue

        # If count of prime factors is odd
        if (countDistinct[B[i]] & 1):

            # Increment oddCount by 1
            oddCount += 1

        else:
            # Increment evenCount by 1
            evenCount += 1

    for i in range(N):

        # Since, product has to be
        # positive i.e > 0

        if (countDistinct[A[i]] == 0):
            continue

        # If count of prime factors is odd
        if (countDistinct[A[i]] & 1):

            # odd * even = even
            evenPairs += (evenCount)

        # If count of prime factors is even
        else:
            # even * odd = even
            # even * even = even
            evenPairs += evenCount + oddCount

    return evenPairs

# Driver Code
if __name__ == '__main__':
    A =  [1, 2, 3]
    B =  [4, 5, 6]
    N = len(A)
    M = len(B)
    print(CountEvenPair(A, B, N, M))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  static int MAX = 1000000;

  // Function to calculate count of
  // distinct prime factors of a number
  static void countOfPrimefactors(int[] CountDistinct)
  {
    bool[]  prime = new bool[MAX + 1];

    for (int i = 0; i <= MAX; i++) {
      CountDistinct[i] = 0;
      prime[i] = true;
    }

    // Sieve of Eratosthenes
    for (int i = 2; i <= MAX; i++) {

      if (prime[i] == true) {
        CountDistinct[i] = 1;

        for (int j = i * 2; j <= MAX;
             j += i) {

          CountDistinct[j]++;
          prime[j] = false;
        }
      }
    }
  }

  // Function to count pairs with even
  // product of distinct prime factors
  static int CountEvenPair(int []A, int []B, int N, int M)
  {

    // Stores count of
    // distinct prime factors
    int[] countDistinct = new int[(MAX + 1)];
    countOfPrimefactors(countDistinct);

    // Stores the count of numbers
    // with even prime factors in B[]
    int evenCount = 0;

    // Stores the count of numbers
    // with odd prime factors in B[]
    int oddCount = 0;

    // Even Product Pairs
    int evenPairs = 0;

    // Traverse the array B[]
    for (int i = 0; i < M; i++) {

      // Since, product has to be
      // positive i.e > 0
      if (countDistinct[B[i]] == 0)
        continue;

      // If count of prime factors is odd
      if ((countDistinct[B[i]] & 1) != 0) {

        // Increment oddCount by 1
        oddCount++;
      }
      else {

        // Increment evenCount by 1
        evenCount++;
      }
    }

    for (int i = 0; i < N; i++) {

      // Since, product has to be
      // positive i.e > 0

      if (countDistinct[A[i]] == 0)
        continue;

      // If count of prime factors is odd
      if ((countDistinct[A[i]] & 1) != 0) {

        // odd * even = even
        evenPairs += (evenCount);
      }

      // If count of prime factors is even
      else {

        // even * odd = even
        // even * even = even
        evenPairs += evenCount + oddCount;
      }
    }
    return evenPairs;
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int []A = { 1, 2, 3 };
    int []B = { 4, 5, 6 };

    int N = A.Length;
    int M = B.Length;

    Console.WriteLine(CountEvenPair(A, B, N, M));
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// js program for the above approach

  let countDistinct = Array(1000000 + 1);
// Function to calculate count of
// distinct prime factors of a number
function countOfPrimefactors(CountDistinct)
{
  let MAX = 1000000;
  let prime = Array(MAX + 1);

  for (let i = 0; i <= MAX; i++) {
    CountDistinct[i] = 0;
    prime[i] = true;
  }

  // Sieve of Eratosthenes
  for (let i = 2; i <= MAX; i++) {

    if (prime[i] == true) {
      CountDistinct[i] = 1;

      for (let j = i * 2; j <= MAX;
           j += i) {

        CountDistinct[j]++;
        prime[j] = false;
      }
    }
  }

}

// Function to count pairs with even
// product of distinct prime factors
function CountEvenPair(A,B,N,M)
{

  let MAX = 1000000;
  // Stores count of
  // distinct prime factors

  countOfPrimefactors(countDistinct);

  // Stores the count of numbers
  // with even prime factors in B[]
  let evenCount = 0;

  // Stores the count of numbers
  // with odd prime factors in B[]
  let oddCount = 0;

  // Even Product Pairs
  let evenPairs = 0;

  // Traverse the array B[]
  for (let i = 0; i < M; i++) {

    // Since, product has to be
    // positive i.e > 0
    if (countDistinct[B[i]] == 0)
      continue;

    // If count of prime factors is odd
    if ((countDistinct[B[i]] & 1) != 0) {

      // Increment oddCount by 1
      oddCount++;
    }
    else {

      // Increment evenCount by 1
      evenCount++;
    }
  }

  for (let i = 0; i < N; i++) {

    // Since, product has to be
    // positive i.e > 0

    if (countDistinct[A[i]] == 0)
      continue;

    // If count of prime factors is odd
    if ((countDistinct[A[i]] & 1) != 0) {

      // odd * even = even
      evenPairs += (evenCount);
    }

    // If count of prime factors is even
    else {

      // even * odd = even
      // even * even = even
      evenPairs += evenCount + oddCount;
    }
  }
  return evenPairs;
}

// Driver Code
let A = [1, 2, 3];
let B = [4, 5, 6];

let N = A.length;
let M = B.length;

document.write(CountEvenPair(A, B, N, M));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*