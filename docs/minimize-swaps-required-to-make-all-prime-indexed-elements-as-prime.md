# 尽量减少将所有质数索引元素作为质数所需的互换

> 原文:[https://www . geesforgeks . org/minimum-swaps-required-to-make-all-prime-indexed-elements-as-prime/](https://www.geeksforgeeks.org/minimize-swaps-required-to-make-all-prime-indexed-elements-as-prime/)

给定一个大小为 **N.** 的数组**arr【】**，任务是找到重新排列数组所需的**最小**交换次数，使得所有质数索引元素都是**质数**，如果任务无法完成，打印“ **-1**

**示例:**

> **输入** : N = 5，arr[] = {1，2，3，4，5}
> **输出** : 0
> **解释**:所有质数索引{2，3，5}(基于一个的索引)都有质数元素。因此，所需的最小互换量为 0。
> 
> **输入** : N = 5，arr[] = {2，7，8，5，13}
> **输出** : 1
> **解释**:8 和 5 互换一次，得到质数指数处的所有质数。

**进场:**任务可以用厄拉多塞的[筛子解决。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   迭代数组并检查当前索引是否是质数，如果是质数，检查该索引中的元素。
*   通过观察可以看出，只有当数组中**素数**的总数**大于或等于数组中**素数索引**的总数**时，才有可能达到所需的配置。
*   如果这个条件成立，那么**的最小**掉期数量等于没有质数的质数指数的数量。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

const int mxn = 1e4 + 1;
bool prime[mxn + 1];

// Function to pre-calculate the prime[]
// prime[i] denotes whether
// i is prime or not
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= mxn; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
            // Update all multiples
            // of p greater than or
            // equal to the square of it
            // numbers which are multiple
            // of p and are less than p^2
            // are already been marked.
            for (int i = p * p; i <= mxn; i += p)
                prime[i] = false;
        }
    }
}

// Function to count minimum number
// of swaps required
int countMin(int arr[], int n)
{
    // To count the minimum number of swaps
    // required to convert the array into
    // perfectly prime
    int cMinSwaps = 0;

    // To count total number of prime
    // indexes in the array
    int cPrimeIndices = 0;

    // To count the total number of
    // prime numbers in the array

    int cPrimeNos = 0;

    for (int i = 0; i < n; i++) {
        // Check whether index
        // is prime or not

        if (prime[i + 1]) {
            cPrimeIndices++;

            // Element is not prime
            if (!prime[arr[i]])
                cMinSwaps++;
            else
                cPrimeNos++;
        }
        else if (prime[arr[i]]) {
            cPrimeNos++;
        }
    }

    // If the total number of prime numbers
    // is greater than or equal to the total
    // number of prime indices, then it is
    // possible to convert the array into
    // perfectly prime
    if (cPrimeNos >= cPrimeIndices)
        return cMinSwaps;
    else
        return -1;
}
// Driver Code
int main()
{
    // Pre-calculate prime[]
    SieveOfEratosthenes();

    int n = 5;
    int arr[5] = { 2, 7, 8, 5, 13 };

    cout << countMin(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    static boolean prime[] = new boolean[(int)1e4 + 2];
    static void SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value in
        // prime[i] will finally be false if i is Not a
        // prime, else true.

        for (int i = 0; i < (int)1e4 + 2; i++)
            prime[i] = true;

        for (int p = 2; p * p < (int)1e4 + 2; p++)
        {

            // If prime[p] is not changed, then it is a
            // prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p * p; i < (int)1e4 + 2;
                     i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to count minimum number
    // of swaps required
    static int countMin(int[] arr, int n)
    {

        // To count the minimum number of swaps
        // required to convert the array into
        // perfectly prime
        int cMinSwaps = 0;

        // To count total number of prime
        // indexes in the array
        int cPrimeIndices = 0;

        // To count the total number of
        // prime numbers in the array

        int cPrimeNos = 0;

        for (int i = 0; i < n; i++) {
            // Check whether index
            // is prime or not

            if (prime[i + 1]) {
                cPrimeIndices++;

                // Element is not prime
                if (prime[arr[i]] == false)
                    cMinSwaps++;
                else
                    cPrimeNos++;
            }
            else if (prime[arr[i]]) {
                cPrimeNos++;
            }
        }

        // If the total number of prime numbers
        // is greater than or equal to the total
        // number of prime indices, then it is
        // possible to convert the array into
        // perfectly prime
        if (cPrimeNos >= cPrimeIndices)
            return cMinSwaps;
        else
            return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Pre-calculate prime[]
        SieveOfEratosthenes();

        int n = 5;
        int arr[] = { 2, 7, 8, 5, 13 };

        System.out.println(countMin(arr, n));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach
import math

mxn = 10000 + 1
prime = [True for _ in range(mxn + 1)]

# Function to pre-calculate the prime[]
# prime[i] denotes whether
# i is prime or not
def SieveOfEratosthenes():
    global prime
    for p in range(2, int(math.sqrt(mxn)) + 1):

                # If prime[p] is not changed,
                # then it is a prime
        if (prime[p] == True):
                        # Update all multiples
                        # of p greater than or
                        # equal to the square of it
                        # numbers which are multiple
                        # of p and are less than p^2
                        # are already been marked.

            for i in range(p*p, mxn+1, p):
                prime[i] = False

# Function to count minimum number
# of swaps required
def countMin(arr, n):

        # To count the minimum number of swaps
        # required to convert the array into
        # perfectly prime
    cMinSwaps = 0

    # To count total number of prime
    # indexes in the array
    cPrimeIndices = 0

    # To count the total number of
    # prime numbers in the array

    cPrimeNos = 0

    for i in range(0, n):
                # Check whether index
                # is prime or not

        if (prime[i + 1]):
            cPrimeIndices += 1

            # Element is not prime
            if (not prime[arr[i]]):
                cMinSwaps += 1
            else:
                cPrimeNos += 1

        elif (prime[arr[i]]):
            cPrimeNos += 1

    # If the total number of prime numbers
    # is greater than or equal to the total
    # number of prime indices, then it is
    # possible to convert the array into
    # perfectly prime
    if (cPrimeNos >= cPrimeIndices):
        return cMinSwaps
    else:
        return -1

# Driver Code
if __name__ == "__main__":

    # Pre-calculate prime[]
    SieveOfEratosthenes()

    n = 5
    arr = [2, 7, 8, 5, 13]

    print(countMin(arr, n))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

class GFG
{
    static bool[] prime = new bool[(int)1e4 + 2];
    static void SieveOfEratosthenes()
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value in
        // prime[i] will finally be false if i is Not a
        // prime, else true.
        for (int i = 0; i < (int)1e4 + 2; i++)
            prime[i] = true;

        for (int p = 2; p * p < (int)1e4 + 2; p++) {

            // If prime[p] is not changed, then it is a
            // prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * p; i < (int)1e4 + 2;
                     i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to count minimum number
    // of swaps required
    static int countMin(int[] arr, int n)
    {

        // To count the minimum number of swaps
        // required to convert the array into
        // perfectly prime
        int cMinSwaps = 0;

        // To count total number of prime
        // indexes in the array
        int cPrimeIndices = 0;

        // To count the total number of
        // prime numbers in the array

        int cPrimeNos = 0;

        for (int i = 0; i < n; i++) {
            // Check whether index
            // is prime or not

            if (prime[i + 1]) {
                cPrimeIndices++;

                // Element is not prime
                if (prime[arr[i]] == false)
                    cMinSwaps++;
                else
                    cPrimeNos++;
            }
            else if (prime[arr[i]]) {
                cPrimeNos++;
            }
        }

        // If the total number of prime numbers
        // is greater than or equal to the total
        // number of prime indices, then it is
        // possible to convert the array into
        // perfectly prime
        if (cPrimeNos >= cPrimeIndices)
            return cMinSwaps;
        else
            return -1;
    }

    // Driver Code
    public static void Main()
    {

        // Pre-calculate prime[]
        SieveOfEratosthenes();

        int n = 5;
        int[] arr = { 2, 7, 8, 5, 13 };

        Console.Write(countMin(arr, n));
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
const mxn = 1e4 + 1;
let prime = new Array(mxn + 1);

// Function to pre-calculate the prime[]
// prime[i] denotes whether
// i is prime or not
function SieveOfEratosthenes() {
  prime.fill(true);

  for (let p = 2; p * p <= mxn; p++)
  {

    // If prime[p] is not changed,
    // then it is a prime
    if (prime[p] == true)
    {

      // Update all multiples
      // of p greater than or
      // equal to the square of it
      // numbers which are multiple
      // of p and are less than p^2
      // are already been marked.
      for (let i = p * p; i <= mxn; i += p) prime[i] = false;
    }
  }
}

// Function to count minimum number
// of swaps required
function countMin(arr, n)
{

  // To count the minimum number of swaps
  // required to convert the array into
  // perfectly prime
  let cMinSwaps = 0;

  // To count total number of prime
  // indexes in the array
  let cPrimeIndices = 0;

  // To count the total number of
  // prime numbers in the array

  let cPrimeNos = 0;

  for (let i = 0; i < n; i++) {
    // Check whether index
    // is prime or not

    if (prime[i + 1]) {
      cPrimeIndices++;

      // Element is not prime
      if (!prime[arr[i]]) cMinSwaps++;
      else cPrimeNos++;
    } else if (prime[arr[i]]) {
      cPrimeNos++;
    }
  }

  // If the total number of prime numbers
  // is greater than or equal to the total
  // number of prime indices, then it is
  // possible to convert the array into
  // perfectly prime
  if (cPrimeNos >= cPrimeIndices) return cMinSwaps;
  else return -1;
}

// Driver Code

// Pre-calculate prime[]
SieveOfEratosthenes();

let n = 5;
let arr = [2, 7, 8, 5, 13];

document.write(countMin(arr, n));

// This code is contributed by gfgking.
</script>
```

**Output**

```
1
```

***时间复杂度***:O(mxn(log(log(mxn)))
***辅助空间*** : O(mxn)