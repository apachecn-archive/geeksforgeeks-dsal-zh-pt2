# 从给定最大和数组中选择 K 个元素的方式数

> 原文:[https://www . geeksforgeeks . org/从给定最大和数组中选择 k 个元素的方式计数/](https://www.geeksforgeeks.org/count-of-ways-to-choose-k-elements-from-given-array-with-maximum-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)、**arr【】**和一个整数 **K** ，任务是找到选择 **K** 数组元素的方法数量，使得这些 **K** 元素的和是最大可能的和。

**示例:**

> **输入:** arr[] = {3，1，1，2}，K = 3
> **输出:** 2
> **解释:**
> 选择 3 个元素的可能方式有:
> 
> 1.  {arr[0] (=3)，arr[1] (=1)，arr[2] (=1)}，子集的和等于(3+1+1 = 5)。
> 2.  {arr[0] (=3)，arr[1] (=1)，arr[3] (=2)}，子集的和等于(3+1+2 = 6)。
> 3.  {arr[0] (=3)，arr[2] (=1)，arr[3] (=2)}，子集的和等于(3+1+2 = 6)。
> 4.  {arr[1] (=1)，arr[2] (=1)，arr[3] (=2)}，子集的和等于(1+1+2 = 4)。
> 
> 因此，选择具有最大和(= 6)的 K 元素的方式总数等于 2。
> 
> **输入:** arr[] = { 2，3，4，5，2，2 }，K = 4
> T3】输出: 3
> 
> **输入:** arr[]= {5，4，3，3，3，3，3，1，1}，K = 4
> **输出:** 10

**方法:**问题可以通过[对数组进行降序排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)来解决。按照以下步骤解决问题:

*   [按降序排列数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)。
*   在数组的 **K-1** 的前缀中计算 **K <sup>第</sup>个**元素的次数，然后将其存储在一个变量中，比如 **P.**
*   计算数组中第 **K <sup>个</sup>** 元素的次数，然后将其存储在一个变量中，比如 **Q.**
*   最后，打印[的取值方式的取值方式，从 Q 元素](https://www.geeksforgeeks.org/permutation-and-combination/)中取 P 元素，即 **C(Q，P)** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the factorial of an
// integer
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to find the value of nCr
int C(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to select K elements with maximum
// sum
int findWays(int arr[], int N, int K)
{
    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    // Stores the frequency of arr[K-1]
    // in the prefix of K-1
    int p = 0;

    // Stores the frequency of arr[K-1]
    // in the array arr[]
    int q = 0;

    // Iterate over the range [0, K]
    for (int i = 0; i < K; i++) {
        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1]) {
            p++;
        }
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1]) {
            q += 1;
        }
    }
    // Stores the number of ways of
    // selecting p from q elements
    int ans = C(q, p);

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 2, 3, 4, 5, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;

    // Function call
    cout << findWays(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to find the factorial of an
// integer
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to find the value of nCr
static int C(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to select K elements with maximum
// sum
static int findWays(Integer arr[], int N, int K)
{

    // Sort the array in descending order
    Arrays.sort(arr, Collections.reverseOrder());

    // Stores the frequency of arr[K-1]
    // in the prefix of K-1
    int p = 0;

    // Stores the frequency of arr[K-1]
    // in the array arr[]
    int q = 0;

    // Iterate over the range [0, K]
    for (int i = 0; i < K; i++)
    {

        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1]) {
            p++;
        }
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1]) {
            q += 1;
        }
    }

    // Stores the number of ways of
    // selecting p from q elements
    int ans = C(q, p);

    // Return ans
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    Integer arr[] = { 2, 3, 4, 5, 2, 2 };
    int N = arr.length;
    int K = 4;

    // Function call
    System.out.print(findWays(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python for the above approach

# Function to find the factorial of an
# integer
def fact(n):
    res = 1
    for i in range(2, n + 1):
        res = res * i

    return res

# Function to find the value of nCr
def C(n, r):
    return fact(n) / (fact(r) * fact(n - r))

# Function to find the number of ways
# to select K elements with maximum
# sum
def findWays(arr, N, K):

    # Sort the array in descending order
    arr.sort(reverse=True)

    # Stores the frequency of arr[K-1]
    # in the prefix of K-1
    p = 0

    # Stores the frequency of arr[K-1]
    # in the array arr[]
    q = 0

    # Iterate over the range [0, K]
    for i in range(K):

        # If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1]):
            p += 1

    # Traverse the array arr[]
    for i in range(N):

        # If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1]):
            q += 1

    # Stores the number of ways of
    # selecting p from q elements
    ans = C(q, p)

    # Return ans
    return int(ans)

# Driver Code

# Input
arr = [2, 3, 4, 5, 2, 2]
N = len(arr)
K = 4

# Function call
print(findWays(arr, N, K))

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;

class Program{

// Function to find the factorial of an
// integer
static int fact(int n)
{
    int res = 1;
    for(int i = 2; i <= n; i++)
        res = res * i;

    return res;
}

// Function to find the value of nCr
static int C(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to select K elements with maximum
// sum
static int findWays(int []arr, int N, int K)
{

    // Sort the array in descending order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Stores the frequency of arr[K-1]
    // in the prefix of K-1
    int p = 0;

    // Stores the frequency of arr[K-1]
    // in the array arr[]
    int q = 0;

    // Iterate over the range [0, K]
    for(int i = 0; i < K; i++)
    {

        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1])
        {
            p++;
        }
    }

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1])
        {
            q += 1;
        }
    }

    // Stores the number of ways of
    // selecting p from q elements
    int ans = C(q, p);

    // Return ans
    return ans;
}

// Driver code
static void Main()
{
    int []arr = { 2, 3, 4, 5, 2, 2 };
    int N = arr.Length;
    int K = 4;

    // Function call
    Console.Write(findWays(arr, N, K));
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the factorial of an
// integer
function fact(n)
{
    let res = 1;
    for (let i = 2; i <= n; i++)
        res = res * i;

    return res;
}

// Function to find the value of nCr
function C(n, r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to select K elements with maximum
// sum
function findWays(arr, N, K)
{

    // Sort the array in descending order
    arr.sort(function (a, b){ return b - a; });

    // Stores the frequency of arr[K-1]
    // in the prefix of K-1
    let p = 0;

    // Stores the frequency of arr[K-1]
    // in the array arr[]
    let q = 0;

    // Iterate over the range [0, K]
    for(let i = 0; i < K; i++)
    {

        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1])
        {
            p++;
        }
    }

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // If arr[i] is equal to arr[K-1]
        if (arr[i] == arr[K - 1])
        {
            q += 1;
        }
    }

    // Stores the number of ways of
    // selecting p from q elements
    let ans = C(q, p);

    // Return ans
    return ans;
}

// Driver Code

// Input
let arr = [ 2, 3, 4, 5, 2, 2 ];
let N = arr.length;
let K = 4;

// Function call
document.write(findWays(arr, N, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N * log(N)+K)*
T5**辅助空间:** O(1)