# 计算每个数组元素右边较小的素数

> 原文:[https://www . geesforgeks . org/count-每个数组元素右侧的较小素数/](https://www.geeksforgeeks.org/count-smaller-primes-on-the-right-of-each-array-element/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，每个阵列元素的任务是[计算其右侧小于](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)且为[质数](https://www.geeksforgeeks.org/prime-numbers/)的阵列元素。

**示例:**

> **输入:** N = 10，A[] = {5，5，17，9，12，15，11，7，39，3}
> **输出:**2 1 3 2 3 2 1 0
> **解释:**
> 对于 i = 1，j =【2，10】处的元素均为有效答案。
> 对于 i = 2，j = [10]处的元素是有效答案。
> 对于 i = 3，j = [7，8，10]处的元素为有效答案。
> 对于 i = 4，j = [8，10]处的元素为有效答案。
> 对于 i = 5，j = [7，8，10]处的元素为有效答案。
> 对于 i = 6，j = [7，8，10]处的元素为有效答案。
> 对于 i = 7，j = [8，10]处的元素为有效答案。
> 对于 i = 8，j = [10]处的元素为有效答案。
> 对于 i = 9，j = [10]处的元素为有效答案。
> 对于 i = 5，其右侧没有元素。
> 
> **输入:** N = 6，A[] = {43，3，5，7，2，41}
> **输出:** 5 1 1 1 0 0
> **解释:**
> 对于 i = 1，j = [2，3，4，5，6]处的元素为有效答案。
> 对于 i = 2，j = [5]处的元素是有效答案。
> 对于 i = 3，j = [5]处的元素是有效答案。
> 对于 i = 4，j = [5]处的元素是有效答案。
> 对于 i = 5，无有效答案。
> 对于 i = 6，无有效答案。

**天真法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素， **A[i]** ，迭代其右边的所有元素，[计算小于 A[i]](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/) 的元素个数，为[素数](https://www.geeksforgeeks.org/prime-numbers/)。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to check if a
// number is prime or not
bool is_prime(int n)
{
    if (n <= 1)
        return 0;

    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return 0;
    }
    return 1;
}

// Function to find the count of
// smaller primes on the right
// of each array element
void countSmallerPrimes(int ar[], int N)
{
    for (int i = 0; i < N; i++) {

        // Stores the count of
        // smaller primes
        int count = 0;
        for (int j = i + 1; j < N; j++) {

            // If A[j] <= A[i] and A[j] is prime
            if (ar[j] <= ar[i] && is_prime(ar[j])) {

                // Increase count
                count++;
            }
        }

        // Print the count for
        // the current element
        cout << count << " ";
    }
}

// Driver Code
int main()
{
    int ar[] = { 43, 3, 5, 7, 2, 41 };
    int N = sizeof ar / sizeof ar[0];

    // Function call
    countSmallerPrimes(ar, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if a
// number is prime or not
static boolean is_prime(int n)
{
    if (n <= 1)
        return false;

    for(int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to find the count of
// smaller primes on the right
// of each array element
static void countSmallerPrimes(int ar[], int N)
{
    for(int i = 0; i < N; i++)
    {

        // Stores the count of
        // smaller primes
        int count = 0;
        for(int j = i + 1; j < N; j++)
        {

            // If A[j] <= A[i] and A[j] is prime
            if (ar[j] <= ar[i] && is_prime(ar[j]))
            {

                // Increase count
                count++;
            }
        }

        // Print the count for
        // the current element
        System.out.print(count + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int ar[] = { 43, 3, 5, 7, 2, 41 };
    int N = ar.length;

    // Function call
    countSmallerPrimes(ar, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a
# number is prime or not
def is_prime(n):

    if (n <= 1):
        return 0

    for i in range(2, n + 1):
        if i * i > n:
            break

        if (n % i == 0):
            return 0

    return 1

# Function to find the count of
# smaller primes on the right
# of each array element
def countSmallerPrimes(ar, N):

    for i in range(N):

        # Stores the count of
        # smaller primes
        count = 0
        for j in range(i + 1, N):

            # If A[j] <= A[i] and A[j] is prime
            if (ar[j] <= ar[i] and is_prime(ar[j])):

                # Increase count
                count += 1

        # Print the count for
        # the current element
        print(count, end = " ")

# Driver Code
if __name__ == '__main__':

    ar = [ 43, 3, 5, 7, 2, 41 ]
    N = len(ar)

    # Function call
    countSmallerPrimes(ar, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to check if a
// number is prime or not
static bool is_prime(int n)
{
  if (n <= 1)
    return false;

  for (int i = 2;
           i * i <= n; i++)
  {
    if (n % i == 0)
      return false;
  }

  return true;
}

// Function to find the count of
// smaller primes on the right
// of each array element
static void countSmallerPrimes(int[] ar,
                               int N)
{
  for (int i = 0; i < N; i++)
  {
    // Stores the count of
    // smaller primes
    int count = 0;

    for (int j = i + 1; j < N; j++)
    {
      // If A[j] <= A[i]
      // and A[j] is prime
      if (ar[j] <= ar[i] &&
          is_prime(ar[j]))
      {
        // Increase count
        count++;
      }
    }

    // Print the count for
    // the current element
    Console.Write(count + " ");
  }
}

// Driver Code
public static void Main()
{
  int[] ar = {43, 3, 5,
              7, 2, 41};
  int N = ar.Length;

  // Function call
  countSmallerPrimes(ar, N);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if a
// number is prime or not
function is_prime(n)
{
    if (n <= 1)
        return false;

    for(let i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to find the count of
// smaller primes on the right
// of each array element
function countSmallerPrimes(ar, N)
{
    for(let i = 0; i < N; i++)
    {

        // Stores the count of
        // smaller primes
        let count = 0;
        for(let j = i + 1; j < N; j++)
        {

            // If A[j] <= A[i] and A[j] is prime
            if (ar[j] <= ar[i] && is_prime(ar[j]))
            {

                // Increase count
                count++;
            }
        }

        // Print the count for
        // the current element
        document.write(count + " ");
    }
}

// Driver Code

    let ar = [ 43, 3, 5, 7, 2, 41 ];
    let N = ar.length;

    // Function call
    countSmallerPrimes(ar, N);

</script>
```

**Output**

```
5 1 1 1 0 0 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是观察上述方法可以通过[从**右到左**迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并使用[分支树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)计算每个数组元素所需的素数来优化。按照以下步骤解决问题:

*   [从右向左遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，通过 **getSum()** 计算当前数组元素右边较小素数的个数。打印获得的计数。
*   现在，[检查当前数组元素是否是质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)，**相应地更新**分支树。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include "bits/stdc++.h"
using namespace std;

const int maxn = 1e6 + 5;
int BITree[maxn];

// Function to check if a
// number is prime or not
bool is_prime(int n)
{
    if (n <= 1)
        return 0;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return 0;
    return 1;
}

// Function to update a Binary Tree
void update_bitree(int BITree[],
                   int index, int value)
{
    while (index <= maxn) {
        BITree[index] += value;
        index += (index & (-index));
    }
}

// Function to find the sum of
// all the elements which are
// less than or equal to index
int sum_bitree(int BITree[], int index)
{
    int s = 0;
    while (index > 0) {
        s += BITree[index];
        index -= (index & (-index));
    }
    return s;
}

// Function to find the number
// of smaller primes on the right
// for every array element
void countSmallerPrimes(int BITree[],
                        int ar[], int N)
{
    int ans[N];

    // Iterate the array in backwards
    for (int i = N - 1; i >= 0; i--) {

        // Calculating the required
        // number of primes
        ans[i] = sum_bitree(BITree, ar[i]);

        // If current array
        // element is prime
        if (is_prime(ar[i]))

            // Update the Fenwick tree
            update_bitree(BITree, ar[i], 1);
    }
    for (int i = 0; i < N; i++)
        cout << ans[i] << " ";
}

// Driver Code
int main()
{

    int ar[] = { 5, 5, 17, 9, 12,
                 15, 11, 7, 39, 3 };
    int N = sizeof ar / sizeof ar[0];

    // Function call
    countSmallerPrimes(BITree, ar, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the
// above approach
//include "bits/stdJava.h"
import java.util.*;
class GFG{

static int maxn =
       (int)1e6 + 5;
static int []BITree =
       new int[maxn];

// Function to check if a
// number is prime or not
static boolean is_prime(int n)
{
  if (n <= 1)
    return false;

  for (int i = 2;
           i * i <= n; i++)
    if (n % i == 0)
      return false;

  return true;
}

// Function to update a Binary Tree
static void update_bitree(int BITree[],
                          int index,
                          int value)
{
  while (index <= maxn)
  {
    BITree[index] += value;
    index += (index & (-index));
  }
}

// Function to find the sum of
// all the elements which are
// less than or equal to index
static int sum_bitree(int BITree[],
                      int index)
{
  int s = 0;
  while (index > 0)
  {
    s += BITree[index];
    index -= (index & (-index));
  }
  return s;
}

// Function to find the number
// of smaller primes on the right
// for every array element
static void countSmallerPrimes(int BITree[],
                               int ar[], int N)
{
  int []ans = new int[N];

  // Iterate the array in backwards
  for (int i = N - 1; i >= 0; i--)
  {
    // Calculating the required
    // number of primes
    ans[i] = sum_bitree(BITree,
                        ar[i]);

    // If current array
    // element is prime
    if (is_prime(ar[i]))

      // Update the Fenwick tree
      update_bitree(BITree,
                    ar[i], 1);
  }

  for (int i = 0; i < N; i++)
    System.out.print(ans[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
  int ar[] = {5, 5, 17, 9, 12,
              15, 11, 7, 39, 3};
  int N = ar.length;

  // Function call
  countSmallerPrimes(BITree, ar, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# include "bits/stdPython.h"
maxn = int(1e6) + 5

BITree = [0] * (maxn)

# Function to check if a
# number is prime or not
def is_prime(n):

    if (n <= 1):
        return False

    i = 2
    while (i * i <= n):
        if (n % i == 0):
            return False

        i += 1

    return True

# Function to update a Binary Tree
def update_bitree(index, value):

    while (index <= maxn):
        BITree[index] += value
        index += (index & (-index))

# Function to find the sum of
# all the elements which are
# less than or equal to index
def sum_bitree(index):

    s = 0
    while (index > 0):
        s += BITree[index]
        index -= (index & (-index))

    return s

# Function to find the number
# of smaller primes on the right
# for every array element
def countSmallerPrimes(ar, N):

    ans = [0] * (N)
    global BITree

    # Iterate the array in backwards
    for i in range(N - 1, 0, -1):

        # Calculating the required
        # number of primes
        ans[i] = sum_bitree(ar[i])

        # If current array
        # element is prime
        if (is_prime(ar[i])):

            # Update the Fenwick tree
            update_bitree(ar[i], 1)

    ans[0] = 2
    for i in range(N):
        print(ans[i], end = " ")

# Driver Code
if __name__ == '__main__':

    ar = [ 5, 5, 17, 9, 12,
           15, 11, 7, 39, 3 ]

    N = len(ar)

    # Function call
    countSmallerPrimes(ar, N)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# Program for the
// above approach
//include "bits/stdJava.h"
using System;
class GFG{

static int maxn =
       (int)1e6 + 5;
static int []BITree =
       new int[maxn];

// Function to check if a
// number is prime or not
static bool is_prime(int n)
{
  if (n <= 1)
    return false;

  for (int i = 2;
           i * i <= n; i++)
    if (n % i == 0)
      return false;

  return true;
}

// Function to update a Binary Tree
static void update_bitree(int []BITree,
                          int index,
                          int value)
{
  while (index <= maxn)
  {
    BITree[index] += value;
    index += (index & (-index));
  }
}

// Function to find the sum of
// all the elements which are
// less than or equal to index
static int sum_bitree(int []BITree,
                      int index)
{
  int s = 0;
  while (index > 0)
  {
    s += BITree[index];
    index -= (index & (-index));
  }
  return s;
}

// Function to find the number
// of smaller primes on the right
// for every array element
static void countSmallerPrimes(int []BITree,
                               int []ar, int N)
{
  int []ans = new int[N];

  // Iterate the array in backwards
  for (int i = N - 1; i >= 0; i--)
  {
    // Calculating the required
    // number of primes
    ans[i] = sum_bitree(BITree,
                        ar[i]);

    // If current array
    // element is prime
    if (is_prime(ar[i]))

      // Update the Fenwick tree
      update_bitree(BITree,
                    ar[i], 1);
  }

  for (int i = 0; i < N; i++)
    Console.Write(ans[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{
  int []ar = {5, 5, 17, 9, 12,
              15, 11, 7, 39, 3};
  int N = ar.Length;

  // Function call
  countSmallerPrimes(BITree, ar, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript Program for the above approach

    let maxn = 1e6 + 5;

    let BITree = new Array(maxn);
    BITree.fill(0);

    // Function to check if a
    // number is prime or not
    function is_prime(n)
    {
      if (n <= 1)
        return false;

      for (let i = 2; i * i <= n; i++)
        if (n % i == 0)
          return false;

      return true;
    }

    // Function to update a Binary Tree
    function update_bitree(BITree, index, value)
    {
      while (index <= maxn)
      {
        BITree[index] += value;
        index += (index & (-index));
      }
    }

    // Function to find the sum of
    // all the elements which are
    // less than or equal to index
    function sum_bitree(BITree, index)
    {
      let s = 0;
      while (index > 0)
      {
        s += BITree[index];
        index -= (index & (-index));
      }
      return s;
    }

    // Function to find the number
    // of smaller primes on the right
    // for every array element
    function countSmallerPrimes(BITree, ar, N)
    {
      let ans = new Array(N);

      // Iterate the array in backwards
      for (let i = N - 1; i >= 0; i--)
      {
        // Calculating the required
        // number of primes
        ans[i] = sum_bitree(BITree, ar[i]);

        // If current array
        // element is prime
        if (is_prime(ar[i]))

          // Update the Fenwick tree
          update_bitree(BITree, ar[i], 1);
      }

      for (let i = 0; i < N; i++)
        document.write(ans[i] + " ");
    }

    let ar = [5, 5, 17, 9, 12, 15, 11, 7, 39, 3];
    let N = ar.length;

    // Function call
    countSmallerPrimes(BITree, ar, N);

</script>
```

**Output**

```
2 1 3 2 3 3 2 1 1 0 
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*