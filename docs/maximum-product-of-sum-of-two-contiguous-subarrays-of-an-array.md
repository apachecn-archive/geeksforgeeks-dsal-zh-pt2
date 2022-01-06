# 一个阵列的两个相邻子阵列之和的最大乘积

> 原文:[https://www . geeksforgeeks . org/数组的两个连续子数组之和的最大乘积/](https://www.geeksforgeeks.org/maximum-product-of-sum-of-two-contiguous-subarrays-of-an-array/)

给定一个正整数数组**arr[]****N**，任务是将数组拆分成两个相邻的子数组，使得两个相邻子数组之和的乘积最大。

**示例:**

> **输入:** arr[] = {4，10，1，7，2，9}
> **输出:** 270
> 所有可能的分区及其和的乘积为:
> {4}和{10，1，7，2，9} - >和的乘积= 116
> {4，10}和{1，7，2，9} - >和的乘积= 266
> {4，10，1}和 9} - >总和的乘积= 242
> {4，10，1，7，2}和{9} - >总和的乘积= 216
> 
> **输入:** arr[] = {4，10，11，10，4 }
> T3】输出: 350

**天真方法:**一个简单的方法是逐个考虑子阵列的所有可能的划分，并计算子阵列和的最大乘积。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// product of sum for any partition
int maxProdSum(int arr[], int n)
{
    int leftArraySum = 0, maxProduct = 0;

    // Traversing the array
    for (int i = 0; i < n; i++) {

        // Compute left array sum
        leftArraySum += arr[i];

        // Compute right array sum
        int rightArraySum = 0;
        for (int j = i + 1; j < n; j++) {
            rightArraySum += arr[j];
        }

        // Multiplying left and right subarray sum
        int k = leftArraySum * rightArraySum;

        // Checking for the maximum product
        // of sum of left and right subarray
        if (k > maxProduct) {
            maxProduct = k;
        }
    }

    // Printing the maximum product
    return maxProduct;
}

// Driver code
int main()
{
    int arr[] = { 4, 10, 1, 7, 2, 9 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxProdSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum
// product of sum for any partition
static int maxProdSum(int arr[], int n)
{
    int leftArraySum = 0, maxProduct = 0;

    // Traversing the array
    for (int i = 0; i < n; i++)
    {

        // Compute left array sum
        leftArraySum += arr[i];

        // Compute right array sum
        int rightArraySum = 0;
        for (int j = i + 1; j < n; j++)
        {
            rightArraySum += arr[j];
        }

        // Multiplying left and right subarray sum
        int k = leftArraySum * rightArraySum;

        // Checking for the maximum product
        // of sum of left and right subarray
        if (k > maxProduct)
        {
            maxProduct = k;
        }
    }

    // Printing the maximum product
    return maxProduct;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 10, 1, 7, 2, 9 };
    int n = arr.length;

    System.out.print(maxProdSum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# product of sum for any partition
def maxProdSum(arr, n):
    leftArraySum = 0;
    maxProduct = 0;

    # Traversing the array
    for i in range(n):

        # Compute left array sum
        leftArraySum += arr[i];

        # Compute right array sum
        rightArraySum = 0;
        for j in range(i + 1, n):
            rightArraySum += arr[j];

        # Multiplying left and right subarray sum
        k = leftArraySum * rightArraySum;

        # Checking for the maximum product
        # of sum of left and right subarray
        if (k > maxProduct):
            maxProduct = k;

    # Printing the maximum product
    return maxProduct;

# Driver code
if __name__ == '__main__':
    arr = [ 4, 10, 1, 7, 2, 9 ];
    n = len(arr);

    print(maxProdSum(arr, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum
// product of sum for any partition
static int maxProdSum(int []arr, int n)
{
    int leftArraySum = 0, maxProduct = 0;

    // Traversing the array
    for (int i = 0; i < n; i++)
    {

        // Compute left array sum
        leftArraySum += arr[i];

        // Compute right array sum
        int rightArraySum = 0;
        for (int j = i + 1; j < n; j++)
        {
            rightArraySum += arr[j];
        }

        // Multiplying left and right subarray sum
        int k = leftArraySum * rightArraySum;

        // Checking for the maximum product
        // of sum of left and right subarray
        if (k > maxProduct)
        {
            maxProduct = k;
        }
    }

    // Printing the maximum product
    return maxProduct;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 10, 1, 7, 2, 9 };
    int n = arr.Length;

    Console.Write(maxProdSum(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximum
// product of sum for any partition
function maxProdSum(arr, n) {
    let leftArraySum = 0, maxProduct = 0;

    // Traversing the array
    for (let i = 0; i < n; i++) {

        // Compute left array sum
        leftArraySum += arr[i];

        // Compute right array sum
        let rightArraySum = 0;
        for (let j = i + 1; j < n; j++) {
            rightArraySum += arr[j];
        }

        // Multiplying left and right subarray sum
        let k = leftArraySum * rightArraySum;

        // Checking for the maximum product
        // of sum of left and right subarray
        if (k > maxProduct) {
            maxProduct = k;
        }
    }

    // Printing the maximum product
    return maxProduct;
}

// Driver code

let arr = [4, 10, 1, 7, 2, 9];
let n = arr.length;

document.write(maxProdSum(arr, n));
</script>
```

**Output:** 

```
270
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(1)

**有效方法:**更好的方法是使用[前缀数组和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念，这有助于计算两个相邻子数组的和。

*   可以计算元素的前缀和。
*   左数组和是第 i <sup>个</sup>位置的值。
*   右数组和是最后一个位置的值–第 i <sup>个</sup>位置。
*   现在计算 **k** ，一些左右子阵列的乘积。
*   找到并打印这些数组的最大乘积。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// product of sum for any partition
int maxProdSum(int arr[], int n)
{
    int prefixArraySum[n], maxProduct = 0;

    // Initialise prefixArraySum[0]
    // with arr[0] element
    prefixArraySum[0] = arr[0];

    // Traverse array elements
    // to compute prefix array sum
    for (int i = 1; i < n; i++) {
        prefixArraySum[i] = prefixArraySum[i - 1]
                            + arr[i];
    }

    for (int i = 0; i < n - 1; i++) {
        // Compute left and right array sum
        int leftArraySum = prefixArraySum[i];
        int rightArraySum = prefixArraySum[n - 1]
                            - prefixArraySum[i];

        // Multiplying left and right subarray sum
        int k = leftArraySum * rightArraySum;

        // Checking for maximum product of
        // the sum of left and right subarray
        if (k > maxProduct) {
            maxProduct = k;
        }
    }

    // Printing the maximum value
    return maxProduct;
}

// Driver code
int main()
{
    int arr[] = { 4, 10, 1, 7, 2, 9 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxProdSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum
// product of sum for any partition
static int maxProdSum(int arr[], int n)
{
    int []prefixArraySum = new int[n];
    int maxProduct = 0;

    // Initialise prefixArraySum[0]
    // with arr[0] element
    prefixArraySum[0] = arr[0];

    // Traverse array elements
    // to compute prefix array sum
    for (int i = 1; i < n; i++)
    {
        prefixArraySum[i] = prefixArraySum[i - 1]
                            + arr[i];
    }

    for (int i = 0; i < n - 1; i++)
    {
        // Compute left and right array sum
        int leftArraySum = prefixArraySum[i];
        int rightArraySum = prefixArraySum[n - 1]
                            - prefixArraySum[i];

        // Multiplying left and right subarray sum
        int k = leftArraySum * rightArraySum;

        // Checking for maximum product of
        // the sum of left and right subarray
        if (k > maxProduct)
        {
            maxProduct = k;
        }
    }

    // Printing the maximum value
    return maxProduct;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 10, 1, 7, 2, 9 };
    int n = arr.length;

    System.out.print(maxProdSum(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the maximum
# product of sum for any partition
def maxProdSum(arr, n):

    prefixArraySum = [0] * n
    maxProduct = 0

    # Initialise prefixArraySum[0]
    # with arr[0] element
    prefixArraySum[0] = arr[0]

    # Traverse array elements
    # to compute prefix array sum
    for i in range(1, n):
        prefixArraySum[i] = prefixArraySum[i - 1] + arr[i]

    for i in range(n - 1):

        # Compute left and right array sum
        leftArraySum = prefixArraySum[i]
        rightArraySum = prefixArraySum[n - 1] - \
                        prefixArraySum[i]

        # Multiplying left and right subarray sum
        k = leftArraySum * rightArraySum

        # Checking for maximum product of
        # the sum of left and right subarray
        if (k > maxProduct):
            maxProduct = k

    # Printing the maximum value
    return maxProduct

# Driver code
arr = [4, 10, 1, 7, 2, 9]
n = len(arr)
print(maxProdSum(arr, n))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum
// product of sum for any partition
static int maxProdSum(int []arr, int n)
{
    int []prefixArraySum = new int[n];
    int maxProduct = 0;

    // Initialise prefixArraySum[0]
    // with arr[0] element
    prefixArraySum[0] = arr[0];

    // Traverse array elements
    // to compute prefix array sum
    for (int i = 1; i < n; i++)
    {
        prefixArraySum[i] = prefixArraySum[i - 1]
                            + arr[i];
    }

    for (int i = 0; i < n - 1; i++)
    {
        // Compute left and right array sum
        int leftArraySum = prefixArraySum[i];
        int rightArraySum = prefixArraySum[n - 1]
                            - prefixArraySum[i];

        // Multiplying left and right subarray sum
        int k = leftArraySum * rightArraySum;

        // Checking for maximum product of
        // the sum of left and right subarray
        if (k > maxProduct)
        {
            maxProduct = k;
        }
    }

    // Printing the maximum value
    return maxProduct;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 10, 1, 7, 2, 9 };
    int n = arr.Length;

    Console.Write(maxProdSum(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximum
// product of sum for any partition
function maxProdSum(arr, n)
{
    let prefixArraySum = [], maxProduct = 0;

    // Initialise prefixArraySum[0]
    // with arr[0] element
    prefixArraySum[0] = arr[0];

    // Traverse array elements
    // to compute prefix array sum
    for (let i = 1; i < n; i++) {
        prefixArraySum[i] = prefixArraySum[i - 1]
                            + arr[i];
    }

    for (let i = 0; i < n - 1; i++) {
        // Compute left and right array sum
        let leftArraySum = prefixArraySum[i];
        let rightArraySum = prefixArraySum[n - 1]
                            - prefixArraySum[i];

        // Multiplying left and right subarray sum
        let k = leftArraySum * rightArraySum;

        // Checking for maximum product of
        // the sum of left and right subarray
        if (k > maxProduct) {
            maxProduct = k;
        }
    }

    // Printing the maximum value
    return maxProduct;
}

// Driver code
let arr = [ 4, 10, 1, 7, 2, 9 ];
let n = arr.length;

document.write(maxProdSum(arr, n));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output:** 

```
270
```

**时间复杂度:** O(n)

**辅助空间:** O(n)