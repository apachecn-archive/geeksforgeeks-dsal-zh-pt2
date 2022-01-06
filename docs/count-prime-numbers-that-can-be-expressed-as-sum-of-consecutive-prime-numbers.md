# 计数可以表示为连续素数之和的素数

> 原文:[https://www . geesforgeks . org/count-质数-可以表示为连续质数之和的质数/](https://www.geeksforgeeks.org/count-prime-numbers-that-can-be-expressed-as-sum-of-consecutive-prime-numbers/)

给定一个整数 **N** ，任务是找出直到 **N** 的质数，可以表示为[连续质数](https://www.geeksforgeeks.org/count-primes-that-can-be-expressed-as-sum-of-two-consecutive-primes-and-1/)的和。

**示例:**

> **输入:** N = 45
> **输出:** 3
> **说明:**
> 下面是 45 以内的素数，可以表示为连续素数之和:
> 
> *   5 = 2 + 3
> *   17 = 2 + 3 + 5 + 7
> *   41 = 2 + 3 + 5 + 7 + 11 + 13
> 
> 因此，计数为 3。
> 
> **输入:**N = 4
> T3】输出: 0

**方法:**思路是使用[素性测试算法](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。利用这个，可以找到所有不超过 **N** 的素数。之后，可以找到每个可以表示为连续素数的数。按照以下步骤解决问题:

1.  遍历从 **1** 到 **N** 的每个数字，检查它是否是素数，并将其存储在一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
2.  对向量中所有存储的[质数](https://www.geeksforgeeks.org/prime-numbers/)进行排序。
3.  让向量中存在 **X** 素数。将和初始化为找到的最小素数，即向量中索引 **0** 处的元素。
4.  迭代范围 **[1，X–1]**，并将每个元素添加到**和**中。
5.  相加后，[检查**和**是否为素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)，和是否小于 **N** 。如果发现是真的，则递增计数器。否则，如果**和**变得大于 **N** ，则断开回路。
6.  完成以上所有步骤后，打印**计数器**上存储的素数计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
int isprm(int n)
{
    // Base Case
    if (n <= 1)
        return 0;
    if (n <= 3)
        return 1;
    if (n % 2 == 0 || n % 3 == 0)
        return 0;

    // Iterate till [5, sqrt(N)] to
    // detect primality of numbers
    for (int i = 5;
         i * i <= n; i = i + 6) {

        // If N is divisible by i
        // or i + 2
        if (n % i == 0 || n % (i + 2) == 0)
            return 0;
    }

    // Return 1 if N is prime
    return 1;
}

// Function to count the prime numbers
// which can be expressed as sum of
// consecutive prime numbers
int countprime(int n)
{
    // Initialize count as 0
    int count = 0;

    // Stores prime numbers
    vector<int> primevector;

    for (int i = 2; i <= n; i++) {

        // If i is prime
        if (isprm(i) == 1) {
            primevector.push_back(i);
        }
    }

    // Initialize the sum
    int sum = primevector[0];

    // Find all required primes upto N
    for (int i = 1;
         i < primevector.size(); i++) {

        // Add it to the sum
        sum += primevector[i];
        if (sum > n)
            break;
        if (isprm(sum) == 1) {
            count++;
        }
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    // Given number N
    int N = 45;

    // Function Call
    cout << countprime(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to check if a
// number is prime or not
static int isprm(int n)
{
  // Base Case
  if (n <= 1)
    return  0;
  if (n <= 3)
    return 1;
  if (n % 2 == 0 ||
      n % 3 == 0)
    return 0;

  // Iterate till [5, Math.sqrt(N)]
  // to detect primality of numbers
  for (int i = 5; i * i <= n;
           i = i + 6)
  {
    // If N is divisible by i
    // or i + 2
    if (n % i == 0 ||
        n % (i + 2) == 0)
      return 0;
  }

  // Return 1 if N is prime
  return 1;
}

// Function to count the prime numbers
// which can be expressed as sum of
// consecutive prime numbers
static int countprime(int n)
{
  // Initialize count as 0
  int count = 0;

  // Stores prime numbers
  Vector<Integer> primevector =
                  new Vector<>();

  for (int i = 2; i <= n; i++)
  {
    // If i is prime
    if (isprm(i) == 1)
    {
      primevector.add(i);
    }
  }

  // Initialize the sum
  int sum = primevector.elementAt(0);

  // Find all required primes upto N
  for (int i = 1;
           i < primevector.size(); i++)
  {
    // Add it to the sum
    sum += primevector.elementAt(i);
    if (sum > n)
      break;
    if (isprm(sum) == 1)
    {
      count++;
    }
  }

  // Return the final count
  return count;
}

// Driver Code
public static void main(String[] args)
{
  // Given number N
  int N = 45;

  // Function Call
  System.out.print(countprime(N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a
# number is prime or not
def isprm(n):

    # Base Case
    if (n <= 1):
        return 0
    if (n <= 3):
        return 1
    if (n % 2 == 0 or n % 3 == 0):
        return 0

    # Iterate till [5, sqrt(N)] to
    # detect primality of numbers
    i = 5
    while (i * i <= n):

        # If N is divisible by i
        # or i + 2
        if (n % i == 0 or
            n % (i + 2) == 0):
            return 0

        i = i + 6

    # Return 1 if N is prime
    return 1

# Function to count the prime numbers
# which can be expressed as sum of
# consecutive prime numbers
def countprime(n):

    # Initialize count as 0
    count = 0

    # Stores prime numbers
    primevector = []

    for i in range(2, n + 1):

        # If i is prime
        if (isprm(i) == 1):
            primevector.append(i)

    # Initialize the sum
    sum = primevector[0]

    # Find all required primes upto N
    for i in range(1, len(primevector)):

        # Add it to the sum
        sum += primevector[i]
        if (sum > n):
            break
        if (isprm(sum) == 1):
            count += 1

    # Return the final count
    return count

# Driver Code

# Given number N
N = 45

# Function call
print(countprime(N))

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check if a
// number is prime or not
static int isprm(int n)
{
  // Base Case
  if (n <= 1)
    return  0;
  if (n <= 3)
    return 1;
  if (n % 2 == 0 ||
      n % 3 == 0)
    return 0;

  // Iterate till [5, Math.Sqrt(N)]
  // to detect primality of numbers
  for (int i = 5; i * i <= n;
           i = i + 6)
  {
    // If N is divisible by i
    // or i + 2
    if (n % i == 0 ||
        n % (i + 2) == 0)
      return 0;
  }

  // Return 1 if N is prime
  return 1;
}

// Function to count the prime numbers
// which can be expressed as sum of
// consecutive prime numbers
static int countprime(int n)
{
  // Initialize count as 0
  int count = 0;

  // Stores prime numbers
  List<int> primevector = new List<int>();

  for (int i = 2; i <= n; i++)
  {
    // If i is prime
    if (isprm(i) == 1)
    {
      primevector.Add(i);
    }
  }

  // Initialize the sum
  int sum = primevector[0];

  // Find all required primes upto N
  for (int i = 1; i < primevector.Count; i++)
  {
    // Add it to the sum
    sum += primevector[i];
    if (sum > n)
      break;
    if (isprm(sum) == 1)
    {
      count++;
    }
  }

  // Return the readonly count
  return count;
}

// Driver Code
public static void Main(String[] args)
{
  // Given number N
  int N = 45;

  // Function Call
  Console.Write(countprime(N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if a
// number is prime or not
function isprm(n)
{
    // Base Case
    if (n <= 1)
        return 0;
    if (n <= 3)
        return 1;
    if (n % 2 == 0 || n % 3 == 0)
        return 0;

    // Iterate till [5, sqrt(N)] to
    // detect primality of numbers
    for (var i = 5;
         i * i <= n; i = i + 6) {

        // If N is divisible by i
        // or i + 2
        if (n % i == 0 || n % (i + 2) == 0)
            return 0;
    }

    // Return 1 if N is prime
    return 1;
}

// Function to count the prime numbers
// which can be expressed as sum of
// consecutive prime numbers
function countprime(n)
{
    // Initialize count as 0
    var count = 0;

    // Stores prime numbers
    var primevector = [];

    for (var i = 2; i <= n; i++) {

        // If i is prime
        if (isprm(i) == 1) {
            primevector.push(i);
        }
    }

    // Initialize the sum
    var sum = primevector[0];

    // Find all required primes upto N
    for (var i = 1;
         i < primevector.length; i++) {

        // Add it to the sum
        sum += primevector[i];
        if (sum > n)
            break;
        if (isprm(sum) == 1) {
            count++;
        }
    }

    // Return the final count
    return count;
}

// Driver Code
// Given number N
var N = 45;
// Function Call
document.write( countprime(N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(√N)*

**高效方法:**上述方法可以通过使用厄拉多塞的[筛预计算到 **N** 的素数来优化。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

***时间复杂度:**O(N * log(logN))*
***辅助空间:** O(log(logN))*