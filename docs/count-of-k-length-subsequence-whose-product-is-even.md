# 乘积为偶数的 K 长度子序列的计数

> 原文:[https://www . geesforgeks . org/count-of-k-length-subsequel-谁的产品是偶数/](https://www.geeksforgeeks.org/count-of-k-length-subsequence-whose-product-is-even/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是从给定的数组 **arr** 中找出长度为 **K** 的非空子序列的个数，使得子序列的乘积为偶数。
**例:**

> **输入:**arr[]=【2，3，1，7】，K = 3
> **输出:** 3
> **解释:**
> 有 3 个长度为 3 的子序列，其乘积为偶数{2，3，1}、{2，3，7}、{2，1，7}。
> **输入:** arr[] = [2，4]，K = 1
> **输出:** 2
> **说明:**
> 有 2 个长度为 1 的子序列，其乘积为偶数{2} {4}。

**方法:**
要解决上述问题，我们必须找到长度为 K 的子序列的总数，并减去乘积为奇数的 K 长度子序列的计数。

1.  为了使子序列的乘积为奇数，我们必须选择 K 个数为奇数。
2.  所以乘积为奇数的长度为 K 的子序列的个数可能是**求 K 个奇数**，即“ *o 选择 k* 或![_{k}^{o}\textrm{C}  ](img/7d8dac833b6b2326a3986626459a2e23.png "Rendered by QuickLaTeX.com")T5”，其中 *o* 是子序列中奇数的个数。
3.  ![\text{So count of a subsequence with even product = } _{k}^{n}\textrm{C} - _{k}^{o}\textrm{C}  ](img/fa77172992c479ecaf3659e4c8b344e9.png "Rendered by QuickLaTeX.com")
    其中 *n* 和 *o* 分别是总数和奇数的计数。

以下是上述程序的实现:

## C++

```
// C++ implementation to Count of K
// length subsequence whose
// Product is even

#include <bits/stdc++.h>
using namespace std;

int fact(int n);

// Function to calculate nCr
int nCr(int n, int r)
{
    if (r > n)
        return 0;
    return fact(n)
           / (fact(r)
              * fact(n - r));
}

// Returns factorial of n
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function for finding number
// of K length subsequences
// whose product is even number
int countSubsequences(
    int arr[], int n, int k)
{
    int countOdd = 0;

    // counting odd numbers in the array
    for (int i = 0; i < n; i++) {
        if (arr[i] & 1)
            countOdd++;
    }
    int ans = nCr(n, k)
              - nCr(countOdd, k);

    return ans;
}

// Driver code
int main()
{

    int arr[] = { 2, 4 };
    int K = 1;

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countSubsequences(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count of K
// length subsequence whose product
// is even
import java.util.*;

class GFG{

// Function to calculate nCr
static int nCr(int n, int r)
{
    if (r > n)
        return 0;
    return fact(n) / (fact(r) *
                      fact(n - r));
}

// Returns factorial of n
static int fact(int n)
{
    int res = 1;
    for(int i = 2; i <= n; i++)
        res = res * i;

    return res;
}

// Function for finding number
// of K length subsequences
// whose product is even number
static int countSubsequences(int arr[],
                             int n, int k)
{
    int countOdd = 0;

    // Counting odd numbers in the array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            countOdd++;
    }
    int ans = nCr(n, k) - nCr(countOdd, k);

    return ans;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 2, 4 };
    int K = 1;

    int N = arr.length;

    System.out.println(countSubsequences(arr, N, K));
}
}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python3 implementation to Count of K
# length subsequence whose
# Product is even

# Function to calculate nCr
def nCr(n, r):

    if (r > n):
        return 0
    return fact(n) // (fact(r) *
                       fact(n - r))

# Returns factorial of n
def fact(n):

    res = 1
    for i in range(2, n + 1):
        res = res * i

    return res

# Function for finding number
# of K length subsequences
# whose product is even number
def countSubsequences(arr, n, k):

    countOdd = 0

    # Counting odd numbers in the array
    for i in range(n):
        if (arr[i] & 1):
            countOdd += 1;

    ans = nCr(n, k) - nCr(countOdd, k);

    return ans

# Driver code
arr = [ 2, 4 ]
K = 1

N = len(arr)

print(countSubsequences(arr, N, K))

# This code is contributed by ANKITKUAR34
```

## C#

```
// C# implementation to count of K
// length subsequence whose product
// is even
using System;

class GFG{

// Function to calculate nCr
static int nCr(int n, int r)
{
    if (r > n)
        return 0;

    return fact(n) / (fact(r) *
                      fact(n - r));
}

// Returns factorial of n
static int fact(int n)
{
    int res = 1;
    for(int i = 2; i <= n; i++)
        res = res * i;

    return res;
}

// Function for finding number
// of K length subsequences
// whose product is even number
static int countSubsequences(int []arr,
                             int n, int k)
{
    int countOdd = 0;

    // Counting odd numbers in the array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            countOdd++;
    }
    int ans = nCr(n, k) - nCr(countOdd, k);

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 2, 4 };
    int K = 1;

    int N = arr.Length;

    Console.WriteLine(countSubsequences(arr, N, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript implementation to Count of K
// length subsequence whose
// Product is even

// Function to calculate nCr
function nCr(n, r)
{
    if (r > n)
        return 0;
    return fact(n)
           / (fact(r)
              * fact(n - r));
}

// Returns factorial of n
function fact(n)
{
    var res = 1;
    for (var i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function for finding number
// of K length subsequences
// whose product is even number
function countSubsequences( arr, n, k)
{
    var countOdd = 0;

    // counting odd numbers in the array
    for (var i = 0; i < n; i++) {
        if (arr[i] & 1)
            countOdd++;
    }
    var ans = nCr(n, k)
              - nCr(countOdd, k);

    return ans;
}

// Driver code
var arr = [ 2, 4 ];
var K = 1;
var N = arr.length;
document.write( countSubsequences(arr, N, K));

</script>
```

**Output:** 

```
2
```