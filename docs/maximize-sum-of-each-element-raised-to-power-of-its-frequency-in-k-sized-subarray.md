# 在 K 大小的子阵列中，最大化每个元素与其频率的幂的和

> 原文:[https://www . geeksforgeeks . org/最大化每个元素的总和-k 尺寸子阵列中其频率的幂/](https://www.geeksforgeeks.org/maximize-sum-of-each-element-raised-to-power-of-its-frequency-in-k-sized-subarray/)

给定一个由 **N** 个元素组成的 [**数组**](https://www.geeksforgeeks.org/array-data-structure/)**【arr】**和一个整数 **K** 。任务是在大小为 **K** 的子阵列中找到元素的最大和，每个元素在子阵列中提升到其频率的幂。

**示例:**

> **输入:** arr[] = { 2，1，2，3，3}，N = 5，K = 3
> **输出:** 11
> **解释:**大小为 3 的所需子阵列= { 2，3，3 }。总和为 2 <sup>1</sup> + 3 <sup>2</sup> = 11，这是可能的最大总和。
> 
> **输入:** arr[] = { 4，9，6，5}，N = 4，K = 3
> **输出:** 20
> **说明:**大小为 3 的两个子阵分别为{ 4，9，6}和{9，6，5}。子阵列{9，6，5}的总和= 20。

**天真方法:**最简单的方法是生成所有的子阵。然后对每个子阵列计算元素的频率，并生成总和。现在核对总数，找出最大值。

**时间复杂度:**O(N * K)
T3】辅助空间: O(N*K)

**高效方法:**一种高效的方法是使用 [**滑动窗口**](https://www.geeksforgeeks.org/window-sliding-technique/) 的概念来避免生成所有的子阵列。然后计算每个窗口中元素的频率，并求出总和。所有窗口中最大的和就是答案。

**时间复杂度:**O(N * K)
T3】辅助空间: O(K)

**最有效的方法:**这个想法也是基于滑动窗口技术。但是在这种方法中，避免了对每个窗口的每个元素的频率进行计数。按照下面的步骤来实现这个想法:

*   保持大小为 **K** 的窗口，表示子阵列。
*   当窗口**向右移动一个位置**时**减去**窗口最左边元素和窗口最右边元素的贡献。
*   现在**调整频率**通过递减窗口最左边元素的频率和递增窗口最右边元素的频率。
*   **根据紧挨着窗口左边的元素和窗口最右边的元素的新频率，将**的贡献加回去。

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>

using namespace std;
#define mod 1000000007

// Function to find the maximum sum
// of a K sized subarray
long long int maxSum(vector<int>& arr,
                     int N, int K)
{
    long long int ans = 0;

    // Map to store frequency of elements
    // of the K sized subarray
    unordered_map<int, int> freq;
    for (int j = 0; j < K; j++) {
        freq[arr[j]]++;
    }

    long long int sum = 0;

    // Sum of the first K sized subarray
    for (auto m : freq)
        sum = (sum
               + ((long long int)
                  (pow(m.first, m.second)))
                     % mod)% mod;

    // Variable to store ans
    ans = max(ans, sum);

    for (int i = 1; i <= N - K; i++) {
        // Subtract the contribution of
        // the element immediately left
        // to the subarray
        sum -= freq[arr[i - 1]] > 0
                   ?
          ((long long int)
           (pow(arr[i - 1],
               freq[arr[i - 1]])))% mod
          : 0;

        // Update the frequency of
        // the element immediately left
        // to the subarray
        freq[arr[i - 1]]--;

        // Add back the contribution of
        // the element immediately left
        // to the subarray
        sum += freq[arr[i - 1]] > 0
                   ?
          ((long long int)
           (pow(arr[i - 1],
                freq[arr[i - 1]])))% mod
                   : 0;

        // Subtract the contribution of
        // the rightmost element
        // of the subarray
        sum -= freq[arr[i + K - 1]] > 0
                   ?
          ((long long int)
           (pow(arr[i + K - 1],
                freq[arr[i + K - 1]])))% mod
                   : 0;

        // Update the frequency of the
        // rightmost element of the subarray
        freq[arr[i + K - 1]]++;

        // Add back the contribution of the
        // rightmost element of the subarray
        sum += freq[arr[i + K - 1]] > 0
                   ?
          ((long long int)
           (pow(arr[i + K - 1],
                freq[arr[i + K - 1]])))% mod
                   : 0;

        // Update the answer
        ans = max(ans, sum);
    }

    return ans;
}

// Driver code
int main()
{
    // Declare the variable
    int N = 5, K = 3;

    vector<int> arr = { 2, 1, 2, 3, 3 };

    // Output the variable to STDOUT
    cout << maxSum(arr, N, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python code for the above approach
mod = 1000000007

# Function to find the maximum sum
# of a K sized subarray
def maxSum(arr, N, K):
    ans = 0

    # Map to store frequency of elements
    # of the K sized subarray
    freq = [0] * 100001
    for j in range(K):
        freq[arr[j]] += 1

    sum = 0

    # Sum of the first K sized subarray
    for i in range(len(freq)):
        if (freq[i] != 0):
            sum += ((i ** freq[i]) % mod) % mod

    # Variable to store ans
    ans = max(ans, sum)

    for i in range(1, N - K + 1):
        # Subtract the contribution of
        # the element immediately left
        # to the subarray
        sum -= ((arr[i - 1] ** freq[arr[i - 1]])
                ) % mod if freq[arr[i - 1]] > 0 else 0

        # Update the frequency of
        # the element immediately left
        # to the subarray
        freq[arr[i - 1]] -= 1

        # Add back the contribution of
        # the element immediately left
        # to the subarray
        sum += ((arr[i - 1] ** freq[arr[i - 1]])
                ) % mod if freq[arr[i - 1]] > 0 else 0

        # Subtract the contribution of
        # the rightmost element
        # of the subarray
        sum -= ((arr[i + K - 1] ** freq[arr[i + K - 1]])
                ) % mod if freq[arr[i + K - 1]] > 0 else 0

        # Update the frequency of the
        # rightmost element of the subarray
        freq[arr[i + K - 1]] += 1

        # Add back the contribution of the
        # rightmost element of the subarray
        sum += ((arr[i + K - 1] ** freq[arr[i + K - 1]])
                ) % mod if freq[arr[i + K - 1]] > 0 else 0

        # Update the answer
        print("ans = ",ans, "sum = ",sum)
        ans = max(ans, sum)

    return ans

# Driver code

# Declare the variable
N = 5
K = 3

arr = [2, 1, 2, 3, 3]

print(maxSum(arr, N, K))

# This code is contributed by gfgking
```

## C#

```
// C# code to implement above approach
using System;
using System.Collections.Generic;
class GFG {
  static int mod = 1000000007;

  // Function to find the maximum sum
  // of a K sized subarray
  static long maxSum(List<int> arr, int N, int K)
  {
    long ans = 0;

    // Map to store frequency of elements
    // of the K sized subarray
    Dictionary<int, int> freq
      = new Dictionary<int, int>();
    for (int j = 0; j < K; j++) {
      if (freq.ContainsKey(arr[j]))
        freq[arr[j]]++;
      else
        freq[arr[j]] = 1;
    }

    long sum = 0;

    // Sum of the first K sized subarray
    foreach(KeyValuePair<int, int> m in freq)
    {
      sum = (sum
             + ((long)(Math.Pow(m.Key, m.Value)))
             % mod)
        % mod;
    }

    // Variable to store ans
    ans = Math.Max(ans, sum);

    for (int i = 1; i <= N - K; i++) {
      // Subtract the contribution of
      // the element immediately left
      // to the subarray
      if (freq.ContainsKey(arr[i - 1])) {
        sum -= freq[arr[i - 1]] > 0
          ? ((long)(Math.Pow(
            arr[i - 1],
            freq[arr[i - 1]])))
          % mod
          : 0;

        // Update the frequency of
        // the element immediately left
        // to the subarray
        freq[arr[i - 1]]--;

        // Add back the contribution of
        // the element immediately left
        // to the subarray
        sum += freq[arr[i - 1]] > 0
          ? ((long)(Math.Pow(
            arr[i - 1],
            freq[arr[i - 1]])))
          % mod
          : 0;
      }
      // Subtract the contribution of
      // the rightmost element
      // of the subarray
      if (freq.ContainsKey(arr[i + K - 1])) {
        sum -= freq[arr[i + K - 1]] > 0
          ? ((long)(Math.Pow(
            arr[i + K - 1],
            freq[arr[i + K - 1]])))
          % mod
          : 0;
      }

      // Update the frequency of the
      // rightmost element of the subarray
      if (freq.ContainsKey(arr[i + K - 1]))
        freq[arr[i + K - 1]]++;
      else
        freq[arr[i + K - 1]] = 1;

      // Add back the contribution of the
      // rightmost element of the subarray

      sum += freq[arr[i + K - 1]] > 0
        ? ((long)(Math.Pow(
          arr[i + K - 1],
          freq[arr[i + K - 1]])))
        % mod
        : 0;

      // Update the answer
      ans = Math.Max(ans, sum);
    }
    return ans;
  }

  // Driver code
  public static void Main()
  {
    // Declare the variable
    int N = 5, K = 3;

    List<int> arr = new List<int>() { 2, 1, 2, 3, 3 };

    // Output the variable to STDOUT
    Console.WriteLine(maxSum(arr, N, K));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       let mod = 1000000007

       // Function to find the maximum sum
       // of a K sized subarray
       function maxSum(arr,
           N, K) {
           let ans = 0;

           // Map to store frequency of elements
           // of the K sized subarray
           let freq = new Array(100001).fill(0);
           for (let j = 0; j < K; j++) {
               freq[arr[j]]++;
           }

           let sum = 0;

           // Sum of the first K sized subarray
           for (let i = 0; i < freq.length; i++)
               if (freq[i] != 0) {
                   sum = (sum
                       + (
                           (Math.pow(i, freq[i])))
                       % mod) % mod;
               }
           // Variable to store ans
           ans = Math.max(ans, sum);

           for (let i = 1; i <= N - K; i++) {
               // Subtract the contribution of
               // the element immediately left
               // to the subarray
               sum -= freq[arr[i - 1]] > 0
                   ?
                   (
                       (Math.pow(arr[i - 1],
                           freq[arr[i - 1]]))) % mod
                   : 0;

               // Update the frequency of
               // the element immediately left
               // to the subarray
               freq[arr[i - 1]]--;

               // Add back the contribution of
               // the element immediately left
               // to the subarray
               sum += freq[arr[i - 1]] > 0
                   ?
                   (
                       (Math.pow(arr[i - 1],
                           freq[arr[i - 1]]))) % mod
                   : 0;

               // Subtract the contribution of
               // the rightmost element
               // of the subarray
               sum -= freq[arr[i + K - 1]] > 0
                   ?
                   (
                       (Math.pow(arr[i + K - 1],
                           freq[arr[i + K - 1]]))) % mod
                   : 0;

               // Update the frequency of the
               // rightmost element of the subarray
               freq[arr[i + K - 1]]++;

               // Add back the contribution of the
               // rightmost element of the subarray
               sum += freq[arr[i + K - 1]] > 0
                   ?
                   (
                       (Math.pow(arr[i + K - 1],
                           freq[arr[i + K - 1]]))) % mod
                   : 0;

               // Update the answer
               ans = Math.max(ans, sum);
           }

           return ans;
       }

       // Driver code

       // Declare the variable
       let N = 5, K = 3;

       let arr = [2, 1, 2, 3, 3];

       document.write(maxSum(arr, N, K));
 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
11
```

**时间复杂度:**O(N)
T3】辅助空间: O(K)