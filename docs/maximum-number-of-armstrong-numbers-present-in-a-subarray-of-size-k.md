# 大小为 K 的子阵列中阿姆斯特朗数的最大数量

> 原文:[https://www . geeksforgeeks . org/Armstrong-numbers-present-in-a-subarray-size-k/](https://www.geeksforgeeks.org/maximum-number-of-armstrong-numbers-present-in-a-subarray-of-size-k/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找出大小为 **K** 的任意[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中存在的[个阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)的最大计数。

**示例:**

> **输入:** arr[] = {28，2，3，6，153，99，828，24}，K = 6
> **输出:** 4
> **解释:**子阵{2，3，6，153}只包含一组阿姆斯特朗数。因此，计数为 4，这是最大可能值。
> 
> **输入:** arr[] = {1，2，3，6}，K = 2
> T3】输出: 2

**天真方法:**解决给定问题的最简单方法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)大小为 **K** 并且对于每个子阵列，计算作为[阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)的数。检查所有子阵列后，打印获得的最大计数。

***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*

**高效方法:**如果是[阿姆斯壮数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)，可以通过将每个数组元素改为 **1** 来优化上述方法，否则，将数组元素改为 **0** ，然后在更新后的数组中找到 **K** 大小的[最大和子数组。遵循以下步骤获得高效的方法:](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果当前元素 **arr[i]** 是阿姆斯壮数，则用 **1** 替换当前元素。否则，更换为 **0** 。
*   完成上述步骤后，将尺寸为 K 的子阵列的[最大和打印为尺寸为 **K** 的子阵列中**阿姆斯特朗数**的最大计数。](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the value of
// x raised to the power y in O(log y)
int power(int x, unsigned int y)
{
    // Base Case
    if (y == 0)
        return 1;

    // If the power y is even
    if (y % 2 == 0)
        return power(x, y / 2)
               * power(x, y / 2);

    // Otherwise
    return x * power(x, y / 2)
           * power(x, y / 2);
}

// Function to calculate the order of
// the number, i.e. count of digits
int order(int num)
{
    // Stores the total count of digits
    int count = 0;

    // Iterate until num is 0
    while (num) {
        count++;
        num = num / 10;
    }

    return count;
}

// Function to check a number is
// an Armstrong Number or not
int isArmstrong(int N)
{
    // Find the order of the number
    int r = order(N);
    int temp = N, sum = 0;

    // Check for Armstrong Number
    while (temp) {

        int d = temp % 10;
        sum += power(d, r);
        temp = temp / 10;
    }

    // If Armstrong number
    // condition is satisfied
    return (sum == N);
}

// Utility function to find the maximum
// sum of a subarray of size K
int maxSum(int arr[], int N, int K)
{
    // If k is greater than N
    if (N < K) {
        return -1;
    }

    // Find the sum of first
    // subarray of size K
    int res = 0;
    for (int i = 0; i < K; i++) {

        res += arr[i];
    }

    // Find the sum of the
    // remaining subarray
    int curr_sum = res;

    for (int i = K; i < N; i++) {

        curr_sum += arr[i] - arr[i - K];
        res = max(res, curr_sum);
    }

    // Return the maximum sum
    // of subarray of size K
    return res;
}

// Function to find all the
// Armstrong Numbers in the array
int maxArmstrong(int arr[], int N,
                 int K)
{
    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i] is an Armstrong
        // Number, then replace it by
        // 1\. Otherwise, 0
        arr[i] = isArmstrong(arr[i]);
    }

    // Return the resultant count
    return maxSum(arr, N, K);
}

// Driver Code
int main()
{
    int arr[] = { 28, 2, 3, 6, 153,
                  99, 828, 24 };
    int K = 6;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maxArmstrong(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function to calculate the value of
// x raised to the power y in O(log y)
static int power(int x, int y)
{

    // Base Case
    if (y == 0)
        return 1;

    // If the power y is even
    if (y % 2 == 0)
        return power(x, y / 2) *
               power(x, y / 2);

    // Otherwise
    return x * power(x, y / 2) *
               power(x, y / 2);
}

// Function to calculate the order of
// the number, i.e. count of digits
static int order(int num)
{

    // Stores the total count of digits
    int count = 0;

    // Iterate until num is 0
    while (num > 0)
    {
        count++;
        num = num / 10;
    }
    return count;
}

// Function to check a number is
// an Armstrong Number or not
static int isArmstrong(int N)
{

    // Find the order of the number
    int r = order(N);
    int temp = N, sum = 0;

    // Check for Armstrong Number
    while (temp > 0)
    {
        int d = temp % 10;
        sum += power(d, r);
        temp = temp / 10;
    }

    // If Armstrong number
    // condition is satisfied
    if (sum == N)
        return 1;

    return 0;
}

// Utility function to find the maximum
// sum of a subarray of size K
static int maxSum(int[] arr, int N, int K)
{

    // If k is greater than N
    if (N < K)
    {
        return -1;
    }

    // Find the sum of first
    // subarray of size K
    int res = 0;
    for(int i = 0; i < K; i++)
    {
        res += arr[i];
    }

    // Find the sum of the
    // remaining subarray
    int curr_sum = res;

    for(int i = K; i < N; i++)
    {
        curr_sum += arr[i] - arr[i - K];
        res = Math.max(res, curr_sum);
    }

    // Return the maximum sum
    // of subarray of size K
    return res;
}

// Function to find all the
// Armstrong Numbers in the array
static int maxArmstrong(int[] arr, int N,
                        int K)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is an Armstrong
        // Number, then replace it by
        // 1\. Otherwise, 0
        arr[i] = isArmstrong(arr[i]);
    }

    // Return the resultant count
    return maxSum(arr, N, K);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 28, 2, 3, 6, 153,
                  99, 828, 24 };
    int K = 6;
    int N = arr.length;

    System.out.println(maxArmstrong(arr, N, K));
}
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate the value of
# x raised to the power y in O(log y)
def power(x, y):
    # Base Case
    if (y == 0):
        return 1

    # If the power y is even
    if (y % 2 == 0):
        return power(x, y // 2) * power(x, y // 2)

    # Otherwise
    return x * power(x, y // 2) * power(x, y // 2)

# Function to calculate the order of
# the number, i.e. count of digits
def order(num):
    # Stores the total count of digits
    count = 0

    # Iterate until num is 0
    while (num):
        count += 1
        num = num // 10

    return count

# Function to check a number is
# an Armstrong Number or not
def isArmstrong(N):
    # Find the order of the number
    r = order(N)
    temp = N
    sum = 0

    # Check for Armstrong Number
    while (temp):
        d = temp % 10
        sum += power(d, r)
        temp = temp // 10

    # If Armstrong number
    # condition is satisfied
    return (sum == N)

# Utility function to find the maximum
# sum of a subarray of size K
def maxSum(arr, N, K):
    # If k is greater than N
    if (N < K):
        return -1

    # Find the sum of first
    # subarray of size K
    res = 0
    for i in range(K):
        res += arr[i]

    # Find the sum of the
    # remaining subarray
    curr_sum = res

    for i in range(K,N,1):
        curr_sum += arr[i] - arr[i - K]
        res = max(res, curr_sum)

    # Return the maximum sum
    # of subarray of size K
    return res

# Function to find all the
# Armstrong Numbers in the array
def maxArmstrong(arr, N, K):

    # Traverse the array arr[]
    for i in range(N):

        # If arr[i] is an Armstrong
        # Number, then replace it by
        # 1\. Otherwise, 0
        arr[i] = isArmstrong(arr[i])

    # Return the resultant count
    return maxSum(arr, N, K)

# Driver Code
if __name__ == '__main__':
    arr = [28, 2, 3, 6, 153,99, 828, 24]
    K = 6
    N = len(arr)
    print(maxArmstrong(arr, N, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to calculate the value of
// x raised to the power y in O(log y)
static int power(int x, int y)
{

    // Base Case
    if (y == 0)
        return 1;

    // If the power y is even
    if (y % 2 == 0)
        return power(x, y / 2) *
               power(x, y / 2);

    // Otherwise
    return x * power(x, y / 2) *
               power(x, y / 2);
}

// Function to calculate the order of
// the number, i.e. count of digits
static int order(int num)
{

    // Stores the total count of digits
    int count = 0;

    // Iterate until num is 0
    while (num > 0)
    {
        count++;
        num = num / 10;
    }
    return count;
}

// Function to check a number is
// an Armstrong Number or not
static int isArmstrong(int N)
{

    // Find the order of the number
    int r = order(N);
    int temp = N, sum = 0;

    // Check for Armstrong Number
    while (temp > 0)
    {
        int d = temp % 10;
        sum += power(d, r);
        temp = temp / 10;
    }

    // If Armstrong number
    // condition is satisfied
    if (sum == N)
        return 1;

    return 0;
}

// Utility function to find the maximum
// sum of a subarray of size K
static int maxSum(int[] arr, int N, int K)
{

    // If k is greater than N
    if (N < K)
    {
        return -1;
    }

    // Find the sum of first
    // subarray of size K
    int res = 0;
    for(int i = 0; i < K; i++)
    {
        res += arr[i];
    }

    // Find the sum of the
    // remaining subarray
    int curr_sum = res;

    for(int i = K; i < N; i++)
    {
        curr_sum += arr[i] - arr[i - K];
        res = Math.Max(res, curr_sum);
    }

    // Return the maximum sum
    // of subarray of size K
    return res;
}

// Function to find all the
// Armstrong Numbers in the array
static int maxArmstrong(int[] arr, int N,
                        int K)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is an Armstrong
        // Number, then replace it by
        // 1\. Otherwise, 0
        arr[i] = isArmstrong(arr[i]);
    }

    // Return the resultant count
    return maxSum(arr, N, K);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 28, 2, 3, 6, 153,
                  99, 828, 24 };
    int K = 6;
    int N = arr.Length;

    Console.Write(maxArmstrong(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the value of
// x raised to the power y in O(log y)
function power(x, y)
{
    // Base Case
    if (y == 0)
        return 1;

    // If the power y is even
    if (y % 2 == 0)
        return power(x, Math.floor(y / 2)) *
               power(x, Math.floor(y / 2));

    // Otherwise
    return x * power(x, Math.floor(y / 2)) *
               power(x, Math.floor(y / 2));
}

// Function to calculate the order of
// the number, i.e. count of digits
function order(num)
{

    // Stores the total count of digits
    let count = 0;

    // Iterate until num is 0
    while (num)
    {
        count++;
        num = Math.floor(num / 10);
    }
    return count;
}

// Function to check a number is
// an Armstrong Number or not
function isArmstrong(N)
{

    // Find the order of the number
    let r = order(N);
    let temp = N,
    sum = 0;

    // Check for Armstrong Number
    while (temp)
    {
        let d = temp % 10;
        sum += power(d, r);
        temp = Math.floor(temp / 10);
    }

    // If Armstrong number
    // condition is satisfied
    return sum == N;
}

// Utility function to find the maximum
// sum of a subarray of size K
function maxSum(arr, N, K)
{

    // If k is greater than N
    if (N < K)
    {
        return -1;
    }

    // Find the sum of first
    // subarray of size K
    let res = 0;
    for(let i = 0; i < K; i++)
    {
        res += arr[i];
    }

    // Find the sum of the
    // remaining subarray
    let curr_sum = res;

    for(let i = K; i < N; i++)
    {
        curr_sum += arr[i] - arr[i - K];
        res = Math.max(res, curr_sum);
    }

    // Return the maximum sum
    // of subarray of size K
    return res;
}

// Function to find all the
// Armstrong Numbers in the array
function maxArmstrong(arr, N, K)
{

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // If arr[i] is an Armstrong
        // Number, then replace it by
        // 1\. Otherwise, 0
        arr[i] = isArmstrong(arr[i]);
    }

    // Return the resultant count
    return maxSum(arr, N, K);
}

// Driver Code
let arr = [ 28, 2, 3, 6, 153, 99, 828, 24 ];
let K = 6;
let N = arr.length;

document.write(maxArmstrong(arr, N, K));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * d)，其中 d 为任意数组元素的最大位数。*
***辅助空间:** O(N)*