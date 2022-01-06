# 对乘积为复合数的数组中的对进行计数

> 原文:[https://www . geeksforgeeks . org/count-pairs-in-a-a-a-array-product-is-composite-number/](https://www.geeksforgeeks.org/count-pairs-in-an-array-whose-product-is-composite-number/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是计算给定数组中乘积为[复合数](https://www.geeksforgeeks.org/composite-number/)的所有对。

**示例:**

> **输入:** arr[] = {1，4，7}
> **输出:** 2
> **解释:**
> 乘积为复合数的对为:(4，7)，(1，4)。
> 因此，要求的输出为 2。
> 
> **输入:** arr[] = {1，2，8，10}
> **输出:** 5

**天真的方法:**想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对。对于每对，检查其元素的乘积是否为[复合数](https://www.geeksforgeeks.org/composite-number/)。如果发现为真，则将计数增加 1。按照以下步骤解决问题:

*   初始化一个变量，比如说 **res** 来存储其乘积为[合成数](https://www.geeksforgeeks.org/composite-number/)的对的计数。
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并生成给定数组的所有可能的对。
*   对于每一对，检查它们的产品是否是复合的。如果发现为真，则将 **res** 的值增加 **1** 。
*   最后，打印 **res** 的值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool isComposite(int N)
{
    // Check if N is multiple
    // of i or not.
    for (int i = 2; i * i <= N;
         i++) {

        // If N is multiple of i.
        if (N % i == 0) {
            return true;
        }
    }

    return false;
}

// Function to get the count
// of pairs whose product
// is a composite number.
int compositePair(int arr[], int N)
{
    // Stores the count of pairs
    // whose product is
    // a composite number
    int res = 0;

    // Generate all possible pairs
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N;
             j++) {

            // Stores the product of
            // element of current pair
            int prod = arr[i] * arr[j];

            // If prod is a
            // composite number
            if (isComposite(prod)) {
                res++;
            }
        }
    }
    return res;
}

// Driver Code
int main()
{

    int arr[] = { 1, 1, 2, 2, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << compositePair(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
class GFG{

// Function to check if a
// number is prime or not
static boolean isComposite(int N)
{
  // Check if N is multiple
  // of i or not.
  for (int i = 2; i * i <= N; i++)
  {
    // If N is multiple of i.
    if (N % i == 0)
    {
      return true;
    }
  }
  return false;
}

// Function to get the count
// of pairs whose product
// is a composite number.
static int compositePair(int arr[],
                         int N)
{
  // Stores the count of pairs
  // whose product is
  // a composite number
  int res = 0;

  // Generate all possible pairs
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      // Stores the product of
      // element of current pair
      int prod = arr[i] * arr[j];

      // If prod is a
      // composite number
      if (isComposite(prod))
      {
        res++;
      }
    }
  }
  return res;
}

// Driver Code
public static void main (String[] args)
{
  int arr[] = {1, 1, 2, 2, 8};
  int N = arr.length;
  System.out.println(compositePair(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a
# number is prime or not
def isComposite(N):

    # Check if N is multiple
    # of i or not.
    for i in range(2, N + 1):
        if i * i > N:
            break

        # If N is multiple of i.
        if (N % i == 0):
            return True

    return False

# Function to get the count
# of pairs whose product
# is a composite number.
def compositePair(arr, N):

    # Stores the count of pairs
    # whose product is
    # a composite number
    res = 0

    # Generate all possible pairs
    for i in range(N):
        for j in range(i + 1, N):

            # Stores the product of
            # element of current pair
            prod = arr[i] * arr[j]

            # If prod is a
            # composite number
            if (isComposite(prod)):
                res += 1

    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 1, 2, 2, 8 ]
    N = len(arr)

    print(compositePair(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to check if a
// number is prime or not
static bool isComposite(int N)
{
  // Check if N is multiple
  // of i or not.
  for (int i = 2; i * i <= N; i++)
  {
    // If N is multiple of i.
    if (N % i == 0)
    {
      return true;
    }
  }
  return false;
}

// Function to get the count
// of pairs whose product
// is a composite number.
static int compositePair(int []arr,
                         int N)
{
  // Stores the count of pairs
  // whose product is
  // a composite number
  int res = 0;

  // Generate all possible pairs
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      // Stores the product of
      // element of current pair
      int prod = arr[i] * arr[j];

      // If prod is a
      // composite number
      if (isComposite(prod))
      {
        res++;
      }
    }
  }
  return res;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {1, 1, 2, 2, 8};
  int N = arr.Length;
  Console.WriteLine(compositePair(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if a
// number is prime or not
function isComposite(N)
{
    var i;
    // Check if N is multiple
    // of i or not.
    for(i = 2; i * i <= N; i++) {

        // If N is multiple of i.
        if (N % i == 0) {
            return true;
        }
    }

    return false;
}

// Function to get the count
// of pairs whose product
// is a composite number.
function compositePair(arr, N)
{
    // Stores the count of pairs
    // whose product is
    // a composite number
     var res = 0;
     var i,j;

    // Generate all possible pairs
    for(i = 0; i < N; i++) {
        for (j = i + 1; j < N;
             j++) {

            // Stores the product of
            // element of current pair
            var prod = arr[i] * arr[j];

            // If prod is a
            // composite number
            if (isComposite(prod)) {
                res++;
            }
        }
    }
    return res;
}

// Driver Code

    var arr = [1, 1, 2, 2, 8];
    var N = arr.length;
    document.write(compositePair(arr, N));

</script>
```

**Output**

```
5
```

***时间复杂度:** O(N <sup>2</sup> √X)，其中 X 是给定数组中一对的最大可能乘积。*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是利用所有质数和 1 都不是合数的事实。按照以下步骤解决问题:

*   初始化两个变量 **cntPrime** 和 **cntOne** 分别存储给定数组中 **1s** 和[素数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的个数。
*   初始化一个变量，比如说 **res** 来存储乘积为复合数的对的计数。
*   乘积不是复合数的总对为:

> CNT concept = CNT prime×cntOne+cntOne×(cntOne–1)/2。

*   因此，乘积为复合数的对的总数为:

> RES = n×n-1)/2–CNT no comp。

*   最后，打印 **res** 的值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define X 1000000

// Function to get all
// the prime numbers in
// the range[1, X]
vector<bool> getPrimeNum()
{
    // Stores the boolean value
    // to check if a number is
    // prime or not
    vector<bool> isPrime(X, true);

    isPrime[0] = false;
    isPrime[1] = false;

    // Mark all non prime
    // numbers as false
    for (int i = 2; i * i <= X;
         i++) {

        // If i is prime number
        if (isPrime[i] == true) {
            for (int j = i * i;
                 j < X; j += i) {

                // Mark j as
                // a composite number
                isPrime[j] = false;
            }
        }
    }
    return isPrime;
}

// Function to get the count of pairs
// whose product is a composite number
int cntPairs(int arr[], int N)
{
    // Stores the boolean value
    // to check if a number is
    // prime or not
    vector<bool> isPrime
        = getPrimeNum();

    // Stores the count of 1s
    int cntOne = 0;

    // Stores the count
    // of prime numbers
    int cntPrime = 0;

    // Traverse the given array.
    for (int i = 0; i < N; i++) {
        if (arr[i] == 1) {
            cntOne += 1;
        }
        else if (isPrime[i]) {
            cntPrime += 1;
        }
    }

    // Stores count of pairs whose
    // product is not a composite number
    int cntNonComp = 0;
    cntNonComp = cntPrime * cntOne
                 + cntOne * (cntOne - 1) / 2;

    // Stores the count of pairs
    // whose product is composite number
    int res = 0;
    res = N * (N - 1) / 2 - cntNonComp;

    return res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 2, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntPairs(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

public static int X = 1000000;

// Function to get all
// the prime numbers in
// the range[1, X]
public static boolean[] getPrimeNum()
{

    // Stores the boolean value
    // to check if a number is
    // prime or not
    boolean isPrime[] = new boolean[X];
    Arrays.fill(isPrime, true);

    isPrime[0] = false;
    isPrime[1] = false;

    // Mark all non prime
    // numbers as false
    for(int i = 2; i * i <= X; i++)
    {

        // If i is prime number
        if (isPrime[i] == true)
        {
            for(int j = i * i; j < X; j += i)
            {

                // Mark j as a composite
                // number
                isPrime[j] = false;
            }
        }
    }
    return isPrime;
}

// Function to get the count of pairs
// whose product is a composite number
public static int cntPairs(int arr[], int N)
{

    // Stores the boolean value
    // to check if a number is
    // prime or not
    boolean isPrime[] = getPrimeNum();

    // Stores the count of 1s
    int cntOne = 0;

    // Stores the count
    // of prime numbers
    int cntPrime = 0;

    // Traverse the given array.
    for(int i = 0; i < N; i++)
    {
        if (arr[i] == 1)
        {
            cntOne += 1;
        }
        else if (isPrime[i])
        {
            cntPrime += 1;
        }
    }

    // Stores count of pairs whose
    // product is not a composite number
    int cntNonComp = 0;
    cntNonComp = cntPrime * cntOne +
                   cntOne * (cntOne - 1) / 2;

    // Stores the count of pairs
    // whose product is composite number
    int res = 0;
    res = N * (N - 1) / 2 - cntNonComp;

    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 2, 2, 8 };
    int N = arr.length;

    System.out.println(cntPairs(arr, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
X = 1000000

# Function to get all
# the prime numbers in
# the range[1, X]
def getPrimeNum():

    # Stores the boolean value
    # to check if a number is
    # prime or not
    isPrime = [True] * (X)

    isPrime[0] = False
    isPrime[1] = False

    # Mark all non prime
    # numbers as false
    i = 2
    while i * i <= X:

        # If i is prime number
        if (isPrime[i] == True):
            for j in range(i * i,
                           X, i):

                # Mark j as
                # a composite number
                isPrime[j] = False

        i += 1

    return isPrime

# Function to get the count
# of pairs whose product
# is a composite number
def cntPairs(arr, N):

    # Stores the boolean value
    # to check if a number is
    # prime or not
    isPrime = getPrimeNum()

    # Stores the count of 1s
    cntOne = 0

    # Stores the count
    # of prime numbers
    cntPrime = 0

    # Traverse the given array.
    for i in range(N):
        if (arr[i] == 1):
            cntOne += 1
        elif (isPrime[i]):
            cntPrime += 1

    # Stores count of pairs whose
    # product is not a composite number
    cntNonComp = 0
    cntNonComp = (cntPrime * cntOne +
                  cntOne * (cntOne - 1) // 2)

    # Stores the count of pairs
    # whose product is composite number
    res = 0
    res = (N * (N - 1) // 2 -
           cntNonComp)

    return res

# Driver Code
if __name__ == "__main__":

    arr = [1, 1, 2, 2, 8]
    N = len(arr)
    print(cntPairs(arr, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

public static int X = 1000000;

// Function to get all
// the prime numbers in
// the range[1, X]
public static bool[] getPrimeNum()
{
  // Stores the bool value
  // to check if a number is
  // prime or not
  bool []isPrime = new bool[X];

  for(int i = 0; i < X; i++)
    isPrime[i] = true;

  isPrime[0] = false;
  isPrime[1] = false;

  // Mark all non prime
  // numbers as false
  for(int i = 2;
          i * i <= X; i++)
  {
    // If i is prime number
    if (isPrime[i] == true)
    {
      for(int j = i * i;
              j < X; j += i)
      {
        // Mark j as a composite
        // number
        isPrime[j] = false;
      }
    }
  }
  return isPrime;
}

// Function to get the count of pairs
// whose product is a composite number
public static int cntPairs(int []arr,
                           int N)
{   
  // Stores the bool value
  // to check if a number is
  // prime or not
  bool []isPrime = getPrimeNum();

  // Stores the count of 1s
  int cntOne = 0;

  // Stores the count
  // of prime numbers
  int cntPrime = 0;

  // Traverse the given array.
  for(int i = 0; i < N; i++)
  {
    if (arr[i] == 1)
    {
      cntOne += 1;
    }
    else if (isPrime[i])
    {
      cntPrime += 1;
    }
  }

  // Stores count of pairs
  // whose product is not
  // a composite number
  int cntNonComp = 0;
  cntNonComp = cntPrime * cntOne +
               cntOne * (cntOne - 1) / 2;

  // Stores the count of pairs
  // whose product is composite number
  int res = 0;
  res = N * (N - 1) / 2 - cntNonComp;

  return res;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {1, 1, 2, 2, 8};
  int N = arr.Length;
  Console.WriteLine(cntPairs(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Js program to implement
// the above approach
let X = 1000000;

// Function to get all
// the prime numbers in
// the range[1, X]
function getPrimeNum()
{
    // Stores the boolean value
    // to check if a number is
    // prime or not
    let prime = [];
    for(let i = 0; i<X; i++){
        prime.push(true);
    }
    prime[0] = false;
    prime[1] = false;

    for (let p = 2; p * p <= prime.length; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {
            // Update all multiples of p,
            // set them to non-prime
            for (let i = p * 2; i <= prime.length; i += p)
                prime[i] = false;
        }
    }
    return prime;
}

// Function to get the count of pairs
// whose product is a composite number
function cntPairs( arr,  N)
{
    // Stores the boolean value
    // to check if a number is
    // prime or not
    let isPrime
        = getPrimeNum();

    // Stores the count of 1s
    let cntOne = 0;

    // Stores the count
    // of prime numbers
    let cntPrime = 0;

    // Traverse the given array.
    for (let i = 0; i < N; i++) {
        if (arr[i] == 1) {
            cntOne += 1;
        }
        else if (isPrime[i]) {
            cntPrime += 1;
        }
    }

    // Stores count of pairs whose
    // product is not a composite number
    let cntNonComp = 0;
    cntNonComp = cntPrime * cntOne
                 + Math.floor(cntOne * (cntOne - 1) / 2);

    // Stores the count of pairs
    // whose product is composite number
    let res = 0;
    res = N *Math.floor( (N - 1) / 2) - cntNonComp;

    return res;
}

// Driver Code
let arr = [ 1, 1, 2, 2, 8 ];
let N = arr.length;
document.write( cntPairs(arr, N));

</script>
```

**Output**

```
5
```

***时间复杂度:** O(N + X × log(log(X))，其中 X 存储给定数组中一对的最大可能乘积。*
***辅助空间:** O(X)*