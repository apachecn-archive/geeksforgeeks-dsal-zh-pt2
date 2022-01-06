# 最多有 K 个奇数的最大和子阵列

> 原文:[https://www . geeksforgeeks . org/max-sum-subarray-最多有 k 个奇数/](https://www.geeksforgeeks.org/maximum-sum-subarray-having-at-most-k-odd-integers/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到[个最大子阵和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)，使得子阵最多有**个 K** 个奇数。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，K = 1
> **输出:** 15
> **解释:**子阵 arr[3… 5] = {4，5，6}只有 1 个奇数即 5，其所有元素之和为最大可能即 15。
> 
> **输入:** arr[] = {1，1，1，1}，K = 0
> T3】输出: 0

**方法:**给定的问题可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决，类似于本文[中讨论的方法](https://www.geeksforgeeks.org/maximum-sum-subarray-sum-less-equal-given-sum/)。创建一个变量 **odd_cnt** ，存储当前窗口中的奇数个数。如果 **odd_cnt** 的值在任何一点超过 **K** ，则从开始减小窗口大小，否则将该元素包含在当前窗口中。同样，迭代整个数组，并保持变量 **max_sum** 中所有窗口之和的最大值。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// To find subarray with maximum sum
// havinf at most K odd integers
int findMaxSubarraySum(int arr[], int n, int K)
{
    // To store current sum and
    // max sum of subarrays
    int curr_sum = arr[0],
        max_sum = 0, start = 0;

    // Stores the count of odd integers in
    // the current window
    int odd_cnt = arr[0] % 2;

    // Loop to iterate through the given array
    for (int i = 1; i < n; i++) {

        // If odd_cnt becomes greater than
        // K start removing starting elements
        while (start < i
               && odd_cnt + arr[i] % 2 > K) {
            curr_sum -= arr[start];
            odd_cnt -= arr[start] % 2;
            start++;
        }

        // Update max_sum
        max_sum = max(max_sum, curr_sum);

        // If cur_sum becomes negative then
        // start new subarray
        if (curr_sum < 0) {
            curr_sum = 0;
        }

        // Add elements to curr_sum
        curr_sum += arr[i];
        odd_cnt += arr[i] % 2;
    }

    // Adding an extra check for last subarray
    if (odd_cnt <= K)
        max_sum = max(max_sum, curr_sum);

    // Return Answer
    return max_sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 1;

    cout << findMaxSubarraySum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG
{

    // To find subarray with maximum sum
    // havinf at most K odd integers
    public static int findMaxSubarraySum(int arr[], int n, int K)
    {

        // To store current sum and
        // max sum of subarrays
        int curr_sum = arr[0], max_sum = 0, start = 0;

        // Stores the count of odd integers in
        // the current window
        int odd_cnt = arr[0] % 2;

        // Loop to iterate through the given array
        for (int i = 1; i < n; i++) {

            // If odd_cnt becomes greater than
            // K start removing starting elements
            while (start < i && odd_cnt + arr[i] % 2 > K) {
                curr_sum -= arr[start];
                odd_cnt -= arr[start] % 2;
                start++;
            }

            // Update max_sum
            max_sum = Math.max(max_sum, curr_sum);

            // If cur_sum becomes negative then
            // start new subarray
            if (curr_sum < 0) {
                curr_sum = 0;
            }

            // Add elements to curr_sum
            curr_sum += arr[i];
            odd_cnt += arr[i] % 2;
        }

        // Adding an extra check for last subarray
        if (odd_cnt <= K)
            max_sum = Math.max(max_sum, curr_sum);

        // Return Answer
        return max_sum;
    }

    // Driver Code
    public static void main(String args[]) {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int N = arr.length;
        int K = 1;

        System.out.println(findMaxSubarraySum(arr, N, K));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program of the above approach

# To find subarray with maximum sum
# havinf at most K odd integers

def findMaxSubarraySum(arr, n, K):

        # To store current sum and
        # max sum of subarrays
    curr_sum = arr[0]
    max_sum = 0
    start = 0

    # Stores the count of odd integers in
    # the current window
    odd_cnt = arr[0] % 2

    # Loop to iterate through the given array
    for i in range(1, n):

                # If odd_cnt becomes greater than
                # K start removing starting elements
        while (start < i and odd_cnt + arr[i] % 2 > K):
            curr_sum -= arr[start]
            odd_cnt -= arr[start] % 2
            start += 1

            # Update max_sum
        max_sum = max(max_sum, curr_sum)

        # If cur_sum becomes negative then
        # start new subarray
        if (curr_sum < 0):
            curr_sum = 0

            # Add elements to curr_sum
        curr_sum += arr[i]
        odd_cnt += arr[i] % 2

        # Adding an extra check for last subarray
    if (odd_cnt <= K):
        max_sum = max(max_sum, curr_sum)

        #  Return Answer
    return max_sum

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5, 6]
    N = len(arr)
    K = 1

    print(findMaxSubarraySum(arr, N, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program of the above approach
using System;
class GFG
{

    // To find subarray with maximum sum
    // havinf at most K odd integers
    public static int findMaxSubarraySum(int[] arr, int n, int K)
    {

        // To store current sum and
        // max sum of subarrays
        int curr_sum = arr[0], max_sum = 0, start = 0;

        // Stores the count of odd integers in
        // the current window
        int odd_cnt = arr[0] % 2;

        // Loop to iterate through the given array
        for (int i = 1; i < n; i++)
        {

            // If odd_cnt becomes greater than
            // K start removing starting elements
            while (start < i && odd_cnt + arr[i] % 2 > K)
            {
                curr_sum -= arr[start];
                odd_cnt -= arr[start] % 2;
                start++;
            }

            // Update max_sum
            max_sum = Math.Max(max_sum, curr_sum);

            // If cur_sum becomes negative then
            // start new subarray
            if (curr_sum < 0)
            {
                curr_sum = 0;
            }

            // Add elements to curr_sum
            curr_sum += arr[i];
            odd_cnt += arr[i] % 2;
        }

        // Adding an extra check for last subarray
        if (odd_cnt <= K)
            max_sum = Math.Max(max_sum, curr_sum);

        // Return Answer
        return max_sum;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int N = arr.Length;
        int K = 1;

        Console.Write(findMaxSubarraySum(arr, N, K));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// To find subarray with maximum sum
// havinf at most K odd integers
function findMaxSubarraySum(arr, n, K)
{

  // To store current sum and
  // max sum of subarrays
  let curr_sum = arr[0],
    max_sum = 0, start = 0;

  // Stores the count of odd integers in
  // the current window
  let odd_cnt = arr[0] % 2;

  // Loop to iterate through the given array
  for (let i = 1; i < n; i++) {

    // If odd_cnt becomes greater than
    // K start removing starting elements
    while (start < i
      && odd_cnt + arr[i] % 2 > K) {
      curr_sum -= arr[start];
      odd_cnt -= arr[start] % 2;
      start++;
    }

    // Update max_sum
    max_sum = Math.max(max_sum, curr_sum);

    // If cur_sum becomes negative then
    // start new subarray
    if (curr_sum < 0) {
      curr_sum = 0;
    }

    // Add elements to curr_sum
    curr_sum += arr[i];
    odd_cnt += arr[i] % 2;
  }

  // Adding an extra check for last subarray
  if (odd_cnt <= K)
    max_sum = Math.max(max_sum, curr_sum);

  // Return Answer
  return max_sum;
}

// Driver Code

let arr = [1, 2, 3, 4, 5, 6];
let N = arr.length;
let K = 1;

document.write(findMaxSubarraySum(arr, N, K));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)