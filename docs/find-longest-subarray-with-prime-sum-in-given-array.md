# 在给定阵列中找到具有素数和的最长子阵列

> 原文:[https://www . geeksforgeeks . org/find-给定数组中带素数和的最长子数组/](https://www.geeksforgeeks.org/find-longest-subarray-with-prime-sum-in-given-array/)

给定一个数组 **arr** []，任务是找到最长的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其和是一个[素数](https://www.geeksforgeeks.org/prime-numbers/)。

**示例:**

> **输入:** **arr[ ]** = {1，4，2，1}
> **输出:** 3
> **解释:** 4+2+1=7 和 7 是一个素数因此我们得到的子阵是{4，2，1}。
> 
> **输入:****arr【】**= {5，2，11，4，7，19}
> **输出:** 5
> **解释:** 5+2+11+4+7=29 和 29 是质数因此我们得到的子阵是{ 5，2，11，4，7，19}。

**方法:**这个问题可以通过生成所有子阵，并检查每个子阵的和是否为素数来解决。检查质数可以使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。任何子阵列的最大和可以等于原始阵列所有元素的和。按照步骤解决给定的问题。

*   创建一个变量 **total_sum** ，该变量存储**arr【】**中所有元素的总和。
*   对厄拉多塞进行[筛选，直到 **total_sum** 为止，因为任何子阵列都不能有大于那个的和。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   创建一个 **max_sum** 变量来跟踪我们在生成所有子阵列时得到的最大子阵列。
*   用两个循环求**arr【】**所有子阵的和，对于每个子阵，检查和是否为素数。
*   取和为素数的子阵中的最大值。
*   打印 max_sum 作为所需答案。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find whether number is
// prime or not
void SieveOfEratosthenes(
    vector<bool>& prime, int total_sum)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    for (int i = 0; i <= total_sum; i++) {
        prime[i] = true;
    }

    for (int p = 2; p * p <= total_sum; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or equal to the square
            // of it numbers which are multiple of p
            // and are less than p^2 are already
            // been marked.
            for (int i = p * p; i <= total_sum; i += p)
                prime[i] = false;
        }
    }
}

int maxLenSubarrayWithSumPrime(
    vector<int>& arr, int n)
{
    // to store total_sum of original array
    int total_sum = 0;

    // calculate total_sum
    for (int i = 0; i < n; i++) {
        total_sum += arr[i];
    }

    // to store whether the number is
    // prime or not
    vector<bool> prime(total_sum + 1);

    // calling sieve to get prime values
    SieveOfEratosthenes(prime, total_sum);

    // to keep track of current and
    // maximum sum till now
    int max_sum = 0, cur_sum = 0;
    for (int i = 0; i < n; i++) {
        cur_sum = 0;
        for (int j = i; j < n; j++) {
            cur_sum += arr[j];

            // is current sum is prime
            if (prime[cur_sum]) {
                max_sum = max(max_sum, j - i + 1);
            }
        }
    }

    // return maximum sum founded.
    return max_sum;
}

// Driver Code
int main()
{
    int n = 6;
    vector<int> arr = { 5, 2, 11, 4, 7, 19 };

    cout << maxLenSubarrayWithSumPrime(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Utility function to find whether number is
// prime or not
static void SieveOfEratosthenes(
    boolean []prime, int total_sum)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    for (int i = 0; i <= total_sum; i++) {
        prime[i] = true;
    }

    for (int p = 2; p * p <= total_sum; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or equal to the square
            // of it numbers which are multiple of p
            // and are less than p^2 are already
            // been marked.
            for (int i = p * p; i <= total_sum; i += p)
                prime[i] = false;
        }
    }
}

static int maxLenSubarrayWithSumPrime(
    int[] arr, int n)
{
    // to store total_sum of original array
    int total_sum = 0;

    // calculate total_sum
    for (int i = 0; i < n; i++) {
        total_sum += arr[i];
    }

    // to store whether the number is
    // prime or not
    boolean []prime = new boolean[total_sum + 1];

    // calling sieve to get prime values
    SieveOfEratosthenes(prime, total_sum);

    // to keep track of current and
    // maximum sum till now
    int max_sum = 0, cur_sum = 0;
    for (int i = 0; i < n; i++) {
        cur_sum = 0;
        for (int j = i; j < n; j++) {
            cur_sum += arr[j];

            // is current sum is prime
            if (prime[cur_sum]) {
                max_sum = Math.max(max_sum, j - i + 1);
            }
        }
    }

    // return maximum sum founded.
    return max_sum;
}

// Driver Code
public static void main(String[] args)
{
    int n = 6;
    int []arr = { 5, 2, 11, 4, 7, 19 };

    System.out.print(maxLenSubarrayWithSumPrime(arr, n));
}
}

// This code is contributed by shikhasingrajput.
```

## 蟒蛇 3

```
# Python 3 program for above approach

from math import sqrt
# Utility function to find whether number is
# prime or not
def SieveOfEratosthenes(prime, total_sum):
    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true.
    # A value in prime[i] will finally be false
    # if i is Not a prime, else true.
    for i in range(total_sum+1):
        prime[i] = True

    for p in range(2,int(sqrt(total_sum)),1):
        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # greater than or equal to the square
            # of it numbers which are multiple of p
            # and are less than p^2 are already
            # been marked.
            for i in range(p * p,total_sum+1,p):
                prime[i] = False

def maxLenSubarrayWithSumPrime(arr, n):
    # to store total_sum of original array
    total_sum = 0

    # calculate total_sum
    for i in range(n):
        total_sum += arr[i]

    # to store whether the number is
    # prime or not
    prime = [ False for i in range(total_sum + 1)]

    # calling sieve to get prime values
    SieveOfEratosthenes(prime, total_sum)

    # to keep track of current and
    # maximum sum till now
    max_sum = 0
    cur_sum = 0
    for i in range(n):
        cur_sum = 0
        for j in range(i,n,1):
            cur_sum += arr[j]

            # is current sum is prime
            if (prime[cur_sum]):
                max_sum = max(max_sum, j - i + 1)

    # return maximum sum founded.
    return max_sum

# Driver Code
if __name__ == '__main__':
    n = 6
    arr = [5, 2, 11, 4, 7, 19]
    print(maxLenSubarrayWithSumPrime(arr, n))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for above approach
using System;
class GFG {

    // Utility function to find whether number is
    // prime or not
    static void SieveOfEratosthenes(bool[] prime,
                                    int total_sum)
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true.
        // A value in prime[i] will finally be false
        // if i is Not a prime, else true.
        for (int i = 0; i <= total_sum; i++) {
            prime[i] = true;
        }

        for (int p = 2; p * p <= total_sum; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                // greater than or equal to the square
                // of it numbers which are multiple of p
                // and are less than p^2 are already
                // been marked.
                for (int i = p * p; i <= total_sum; i += p)
                    prime[i] = false;
            }
        }
    }

    static int maxLenSubarrayWithSumPrime(int[] arr, int n)
    {
        // to store total_sum of original array
        int total_sum = 0;

        // calculate total_sum
        for (int i = 0; i < n; i++) {
            total_sum += arr[i];
        }

        // to store whether the number is
        // prime or not
        bool[] prime = new bool[total_sum + 1];

        // calling sieve to get prime values
        SieveOfEratosthenes(prime, total_sum);

        // to keep track of current and
        // maximum sum till now
        int max_sum = 0, cur_sum = 0;
        for (int i = 0; i < n; i++) {
            cur_sum = 0;
            for (int j = i; j < n; j++) {
                cur_sum += arr[j];

                // is current sum is prime
                if (prime[cur_sum]) {
                    max_sum = Math.Max(max_sum, j - i + 1);
                }
            }
        }

        // return maximum sum founded.
        return max_sum;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int n = 6;
        int[] arr = { 5, 2, 11, 4, 7, 19 };

        Console.WriteLine(
            maxLenSubarrayWithSumPrime(arr, n));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Utility function to find whether number is
        // prime or not
        function SieveOfEratosthenes(
            prime, total_sum)
        {

            // Create a boolean array "prime[0..n]" and
            // initialize all entries it as true.
            // A value in prime[i] will finally be false
            // if i is Not a prime, else true.
            for (let i = 0; i <= total_sum; i++) {
                prime[i] = true;
            }

            for (let p = 2; p * p <= total_sum; p++) {

                // If prime[p] is not changed,
                // then it is a prime
                if (prime[p] == true) {

                    // Update all multiples of p
                    // greater than or equal to the square
                    // of it numbers which are multiple of p
                    // and are less than p^2 are already
                    // been marked.
                    for (let i = p * p; i <= total_sum; i += p)
                        prime[i] = false;
                }
            }
            return prime;
        }

        function maxLenSubarrayWithSumPrime(
            arr, n)
        {

            // to store total_sum of original array
            let total_sum = 0;

            // calculate total_sum
            for (let i = 0; i < n; i++) {
                total_sum += arr[i];
            }

            // to store whether the number is
            // prime or not
            let prime = new Array(total_sum + 1);
            // calling sieve to get prime values
            prime = SieveOfEratosthenes(prime, total_sum);

            // to keep track of current and
            // maximum sum till now
            let max_sum = 0, cur_sum = 0;
            for (let i = 0; i < n; i++) {
                cur_sum = 0;
                for (let j = i; j < n; j++) {
                    cur_sum += arr[j];

                    // is current sum is prime
                    if (prime[cur_sum]) {
                        max_sum = Math.max(max_sum, j - i + 1);
                    }
                }
            }

            // return maximum sum founded.
            return max_sum;
        }

        // Driver Code
        let n = 6;
        let arr = [5, 2, 11, 4, 7, 19];

        document.write(maxLenSubarrayWithSumPrime(arr, n));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
5
```

**时间复杂度:**o(n^2)
T3】辅助复杂度: O(N)