# 恰好具有 K 个素数的子阵列的计数

> 原文:[https://www . geeksforgeeks . org/子阵列计数-精确 k-素数/](https://www.geeksforgeeks.org/count-of-subarrays-having-exactly-k-prime-numbers/)

给定一个由 **N** 个整数和一个数字 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是用精确的 **K** [质数](https://www.geeksforgeeks.org/prime-numbers/)来统计子阵的数量。
**例:**

> **输入:** arr[] = {1，2，3，4}，K = 2
> **输出:** 4
> **说明:**
> 由于数组中素数总数为 2。所以 2 个质数的 4 个子阵是:
> 1。{2，3}
> 2。{1，2，3}
> 3。{2，3，4}
> 4。{1，2，3，4}
> **输入:** arr[] = {2，4，5}，K = 3
> **输出:** 0
> **解释:**
> 因为数组中素数的总数是 2，小于 K(K = 3)。
> 所以没有这样的 K 素数的子阵。

**进场:**

1.  遍历给定数组**arr[]**[检查元素是否为质数](https://www.geeksforgeeks.org/java-program-to-check-if-a-number-is-prime-or-not/)。
2.  如果当前元素是质数，则将该索引处的数组值更改为 1，否则将该索引处的值更改为 0。
3.  现在给定的数组被转换成二进制数组。
4.  使用本文[中讨论的方法，在上述二进制数组中找到总和等于**K**T3 的子数组的](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/)[计数。](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/)

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// A utility function to check if
// the number n is prime or not
bool isPrime(int n)
{
    int i;

    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0) {
        return false;
    }

    for (i = 5; i * i <= n; i += 6) {

        // If n is divisible by i & i+2
        // then it is not prime
        if (n % i == 0
            || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// Function to find number of subarrays
// with sum exactly equal to k
int findSubarraySum(int arr[], int n, int K)
{
    // STL map to store number of subarrays
    // starting from index zero having
    // particular value of sum.
    unordered_map<int, int> prevSum;

    int res = 0;

    // To store the sum of element traverse
    // so far
    int currsum = 0;

    for (int i = 0; i < n; i++) {

        // Add current element to currsum
        currsum += arr[i];

        // If currsum = K, then a new
        // subarray is found
        if (currsum == K) {
            res++;
        }

        // If currsum > K then find the
        // no. of subarrays with sum
        // currsum - K and exclude those
        // subarrays
        if (prevSum.find(currsum - K)
            != prevSum.end())
            res += (prevSum[currsum - K]);

        // Add currsum to count of
        // different values of sum
        prevSum[currsum]++;
    }

    // Return the final result
    return res;
}

// Function to count the subarray with K primes
void countSubarray(int arr[], int n, int K)
{
    // Update the array element
    for (int i = 0; i < n; i++) {

        // If current element is prime
        // then update the arr[i] to 1
        if (isPrime(arr[i])) {
            arr[i] = 1;
        }

        // Else change arr[i] to 0
        else {
            arr[i] = 0;
        }
    }

    // Function Call
    cout << findSubarraySum(arr, n, K);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countSubarray(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // A utility function to check if
    // the number n is prime or not
    static boolean isPrime(int n) {
        int i;

        // Base Cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check to skip middle five
        // numbers in below loop
        if (n % 2 == 0 || n % 3 == 0) {
            return false;
        }

        for (i = 5; i * i <= n; i += 6) {

            // If n is divisible by i & i+2
            // then it is not prime
            if (n % i == 0 || n % (i + 2) == 0) {
                return false;
            }
        }

        return true;
    }

    // Function to find number of subarrays
    // with sum exactly equal to k
    static int findSubarraySum(int arr[], int n, int K)
    {
        // STL map to store number of subarrays
        // starting from index zero having
        // particular value of sum.
        HashMap<Integer, Integer> prevSum =
             new HashMap<Integer, Integer>();

        int res = 0;

        // To store the sum of element traverse
        // so far
        int currsum = 0;

        for (int i = 0; i < n; i++) {

            // Add current element to currsum
            currsum += arr[i];

            // If currsum = K, then a new
            // subarray is found
            if (currsum == K) {
                res++;
            }

            // If currsum > K then find the
            // no. of subarrays with sum
            // currsum - K and exclude those
            // subarrays
            if (prevSum.containsKey(currsum - K)) {
                res += (prevSum.get(currsum - K));
            }
            // Add currsum to count of
            // different values of sum
            if (prevSum.containsKey(currsum))
                prevSum.put(currsum, prevSum.get(currsum) + 1);
            else
                prevSum.put(currsum, 1);
        }

        // Return the final result
        return res;
    }

    // Function to count the subarray with K primes
    static void countSubarray(int arr[], int n, int K) {
        // Update the array element
        for (int i = 0; i < n; i++) {

            // If current element is prime
            // then update the arr[i] to 1
            if (isPrime(arr[i])) {
                arr[i] = 1;
            }

            // Else change arr[i] to 0
            else {
                arr[i] = 0;
            }
        }

        // Function Call
        System.out.print(findSubarraySum(arr, n, K));
    }

    // Driver Code
    public static void main(String[] args) {
        int arr[] = { 1, 2, 3, 4 };
        int K = 2;
        int N = arr.length;

        // Function Call
        countSubarray(arr, N, K);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# A utility function to check if
# the number n is prime or not
def isPrime(n):
    # Base Cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # Check to skip middle five
    # numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5,int(sqrt(n))+1,6):
        # If n is divisible by i & i+2
        # then it is not prime
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# Function to find number of subarrays
# with sum exactly equal to k
def findSubarraySum(arr,n,K):
    # STL map to store number of subarrays
    # starting from index zero having
    # particular value of sum.
    prevSum = {i:0 for i in range(100)}

    res = 0

    # To store the sum of element traverse
    # so far
    currsum = 0

    for i in range(n):
        # Add current element to currsum
        currsum += arr[i]

        # If currsum = K, then a new
        # subarray is found
        if (currsum == K):
            res += 1

        # If currsum > K then find the
        # no. of subarrays with sum
        # currsum - K and exclude those
        # subarrays
        if (currsum - K) in prevSum:
            res += (prevSum[currsum - K])

        # Add currsum to count of
        # different values of sum
        prevSum[currsum] += 1

    # Return the final result
    return res

# Function to count the subarray with K primes
def countSubarray(arr,n,K):
    # Update the array element
    for i in range(n):
        # If current element is prime
        # then update the arr[i] to 1
        if (isPrime(arr[i])):
            arr[i] = 1

        # Else change arr[i] to 0
        else:
            arr[i] = 0

    # Function Call
    print(findSubarraySum(arr, n, K))

# Driver Code
if __name__ == '__main__':
    arr =  [1, 2, 3, 4]
    K = 2
    N = len(arr)

    # Function Call
    countSubarray(arr, N, K)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// A utility function to check if
// the number n is prime or not
static bool isPrime(int n)
{
    int i;

    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
    {
        return false;
    }

    for(i = 5; i * i <= n; i += 6)
    {

       // If n is divisible by i & i+2
       // then it is not prime
       if (n % i == 0 || n % (i + 2) == 0)
       {
           return false;
       }
    }
    return true;
}

// Function to find number of subarrays
// with sum exactly equal to k
static int findSubarraySum(int []arr, int n,
                                      int K)
{

    // STL map to store number of subarrays
    // starting from index zero having
    // particular value of sum.
    Dictionary<int, int> prevSum = new Dictionary<int, int>();

    int res = 0;

    // To store the sum of element traverse
    // so far
    int currsum = 0;

    for(int i = 0; i < n; i++)
    {

       // Add current element to currsum
       currsum += arr[i];

       // If currsum = K, then a new
       // subarray is found
       if (currsum == K)
       {
           res++;
       }

       // If currsum > K then find the
       // no. of subarrays with sum
       // currsum - K and exclude those
       // subarrays
       if (prevSum.ContainsKey(currsum - K))
       {
           res += (prevSum[currsum - K]);
       }

       // Add currsum to count of
       // different values of sum
       if (prevSum.ContainsKey(currsum))
       {
           prevSum[currsum] = prevSum[currsum] + 1;
       }
       else
       {
           prevSum.Add(currsum, 1);
       }
    }

    // Return the readonly result
    return res;
}

// Function to count the subarray with K primes
static void countSubarray(int []arr, int n, int K)
{

    // Update the array element
    for(int i = 0; i < n; i++)
    {

       // If current element is prime
       // then update the arr[i] to 1
       if (isPrime(arr[i]))
       {
           arr[i] = 1;
       }

       // Else change arr[i] to 0
       else
       {
           arr[i] = 0;
       }
    }

    // Function Call
    Console.Write(findSubarraySum(arr, n, K));
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4 };
    int K = 2;
    int N = arr.Length;

    // Function Call
    countSubarray(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// A utility function to check if
// the number n is prime or not
function isPrime(n)
{
    let i;

    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0) {
        return false;
    }

    for (i = 5; i * i <= n; i += 6) {

        // If n is divisible by i & i+2
        // then it is not prime
        if (n % i == 0
            || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// Function to find number of subarrays
// with sum exactly equal to k
function findSubarraySum(arr, n, K)
{
    // STL map to store number of subarrays
    // starting from index zero having
    // particular value of sum.
    let prevSum = new Map();

    let res = 0;

    // To store the sum of element traverse
    // so far
    let currsum = 0;

    for (let i = 0; i < n; i++) {

        // Add current element to currsum
        currsum += arr[i];

        // If currsum = K, then a new
        // subarray is found
        if (currsum == K) {
            res++;
        }

        // If currsum > K then find the
        // no. of subarrays with sum
        // currsum - K and exclude those
        // subarrays
        if (prevSum.has(currsum - K))
            res += (prevSum.get(currsum - K));

        // Add currsum to count of
        // different values of sum
        if(prevSum.has(currsum)){
            prevSum.set(currsum, prevSum.get(currsum) + 1)
        }else{
            prevSum.set(currsum, 1)
        }
    }

    // Return the final result
    return res;
}

// Function to count the subarray with K primes
function countSubarray(arr, n, K)
{
    // Update the array element
    for (let i = 0; i < n; i++) {

        // If current element is prime
        // then update the arr[i] to 1
        if (isPrime(arr[i])) {
            arr[i] = 1;
        }

        // Else change arr[i] to 0
        else {
            arr[i] = 0;
        }
    }

    // Function Call
    document.write(findSubarraySum(arr, n, K));
}

// Driver Code

let arr = [ 1, 2, 3, 4 ];
let K = 2;
let N = arr.length;

// Function Call
countSubarray(arr, N, K);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log(log(N)))*

***辅助空间:**O(N)*T4】