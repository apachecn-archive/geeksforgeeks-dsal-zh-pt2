# 通过翻转最多 K 位

来最大化数量

> 原文:[https://www . geeksforgeeks . org/通过最多翻转 k 位来最大化数量/](https://www.geeksforgeeks.org/maximize-the-number-by-flipping-at-most-k-bits/)

给定一个整数 **N** ，任务是找到在 **N** 的二进制表示中最多翻转 **K** 位可以得到的最大数。
**举例:**

> **输入:** N = 4，K = 1
> **输出:**6
> 4 的二进制等值为 100。
> 翻转第一个 0，我们得到 110
> ，相当于 6。
> **输入:** N = 5，K = 2
> **输出:** 7

**进场:**

*   如果 **N** 的二进制表示中 **0s** 的数量小于 **K** ，则翻转所有 **0s** 。
*   如果 **0s** 的数量大于或等于 **K** ，则翻转最显著的**K**T6】0s。
*   最后，打印最大化的整数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal number n
// to its binary representation
// stored as an array arr[]
void decBinary(int arr[], int n)
{
    int k = log2(n);
    while (n > 0) {
        arr[k--] = n % 2;
        n /= 2;
    }
}

// Function to convert the number
// represented as a binary array
// arr[] into its decimal equivalent
int binaryDec(int arr[], int n)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += arr[i] << (n - i - 1);
    return ans;
}

// Function to return the maximized
// number by flipping atmost k bits
int maxNum(int n, int k)
{

    // Number of bits in n
    int l = log2(n) + 1;

    // Find the binary representation of n
    int a[l] = { 0 };
    decBinary(a, n);

    // To count the number of 0s flipped
    int cn = 0;
    for (int i = 0; i < l; i++) {
        if (a[i] == 0 && cn < k) {
            a[i] = 1;
            cn++;
        }
    }

    // Return the decimal equivalent
    // of the maximized number
    return binaryDec(a, l);
}

// Driver code
int main()
{
    int n = 4, k = 1;

    cout << maxNum(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to convert decimal number n
    // to its binary representation
    // stored as an array arr[]
    static void decBinary(int arr[], int n)
    {
        int k = (int)(Math.log(n) /
                      Math.log(2));

        while (n > 0)
        {
            arr[k--] = n % 2;
            n /= 2;
        }
    }

    // Function to convert the number
    // represented as a binary array
    // arr[] into its decimal equivalent
    static int binaryDec(int arr[], int n)
    {
        int ans = 0;
        for (int i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to return the maximized
    // number by flipping atmost k bits
    static int maxNum(int n, int k)
    {

        // Number of bits in n
        int l = (int)(Math.log(n) /
                      Math.log(2)) + 1;

        // Find the binary representation of n
        int a[] = new int[l];
        decBinary(a, n);

        // To count the number of 0s flipped
        int cn = 0;
        for (int i = 0; i < l; i++)
        {
            if (a[i] == 0 && cn < k)
            {
                a[i] = 1;
                cn++;
            }
        }

        // Return the decimal equivalent
        // of the maximized number
        return binaryDec(a, l);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 4, k = 1;

        System.out.println(maxNum(n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation of the approach

import math

# Function to convert decimal number n
# to its binary representation
# stored as an array arr[]
def decBinary(arr, n):
    k = int(math.log2(n))
    while (n > 0):
        arr[k] = n % 2
        k = k - 1
        n = n//2

# Function to convert the number
# represented as a binary array
# arr[] into its decimal equivalent
def binaryDec(arr, n):
    ans = 0
    for i in range(0, n):
        ans = ans + (arr[i] << (n - i - 1))
    return ans

# Function to return the maximized
# number by flipping atmost k bits
def maxNum(n, k):

    # Number of bits in n
    l = int(math.log2(n)) + 1

    # Find the binary representation of n
    a = [0 for i in range(0, l)]
    decBinary(a, n)

    # To count the number of 0s flipped
    cn = 0
    for i in range(0, l):
        if (a[i] == 0 and cn < k):
            a[i] = 1
            cn = cn + 1

    # Return the decimal equivalent
    # of the maximized number
    return binaryDec(a, l)

# Driver code
n = 4
k = 1

print(maxNum(n, k))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to convert decimal number n
    // to its binary representation
    // stored as an array []arr
    static void decBinary(int []arr, int n)
    {
        int k = (int)(Math.Log(n) /
                      Math.Log(2));

        while (n > 0)
        {
            arr[k--] = n % 2;
            n /= 2;
        }
    }

    // Function to convert the number
    // represented as a binary array
    // []arr into its decimal equivalent
    static int binaryDec(int []arr, int n)
    {
        int ans = 0;
        for (int i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to return the maximized
    // number by flipping atmost k bits
    static int maxNum(int n, int k)
    {

        // Number of bits in n
        int l = (int)(Math.Log(n) /
                      Math.Log(2)) + 1;

        // Find the binary representation of n
        int []a = new int[l];
        decBinary(a, n);

        // To count the number of 0s flipped
        int cn = 0;
        for (int i = 0; i < l; i++)
        {
            if (a[i] == 0 && cn < k)
            {
                a[i] = 1;
                cn++;
            }
        }

        // Return the decimal equivalent
        // of the maximized number
        return binaryDec(a, l);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 4, k = 1;

        Console.WriteLine(maxNum(n, k));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to convert decimal number n
// to its binary representation
// stored as an array arr[]
function decBinary(arr, n) {
    let k = Math.log2(n);
    while (n > 0) {
        arr[k--] = n % 2;
        n = Math.floor(n / 2);
    }
}

// Function to convert the number
// represented as a binary array
// arr[] into its decimal equivalent
function binaryDec(arr, n) {
    let ans = 0;
    for (let i = 0; i < n; i++)
        ans += arr[i] << (n - i - 1);
    return ans;
}

// Function to return the maximized
// number by flipping atmost k bits
function maxNum(n, k) {

    // Number of bits in n
    let l = Math.log2(n) + 1;

    // Find the binary representation of n
    let a = new Array(l).fill(0);
    decBinary(a, n);

    // To count the number of 0s flipped
    let cn = 0;
    for (let i = 0; i < l; i++) {
        if (a[i] == 0 && cn < k) {
            a[i] = 1;
            cn++;
        }
    }

    // Return the decimal equivalent
    // of the maximized number
    return binaryDec(a, l);
}

// Driver code

let n = 4, k = 1;

document.write(maxNum(n, k));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
6
```