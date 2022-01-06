# 从数组中最大化所选数字的总和以清空它|设置 2

> 原文:[https://www . geeksforgeeks . org/从数组到空集合最大化选定数字的总和-2/](https://www.geeksforgeeks.org/maximize-sum-of-selected-numbers-from-array-to-empty-it-set-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在所有操作中最大化所选数字的总和，以便在每个操作中，选择一个数字 **A <sub>i</sub>** ，删除它的一个出现，并删除数组中所有出现的**A<sub>I</sub>–1**和 **A <sub>i</sub> + 1** (如果它们存在的话)，直到

**示例:**

> **输入:** arr[] = {3，4，2}
> **输出:** 6
> **说明:**第一次操作，选择 4，删除。因此，从 arr[]中删除所有出现的 3 和 5。操作后的数组是 arr[] = {2}。在第二次操作中，选择 2。因此，所有选定数字的总和= 4+2 = 6，这是最大可能值。
> 
> **输入:** arr[] = {2，2，3，3，3，4}
> **输出:** 9
> **说明:**第一次操作，选择 3，删除。因此，从 arr[]中删除所有出现的 2 和 4。操作后的数组是 arr[] = {3，3}。在第二次和第三次操作中，选择 3。因此，所有选定数字的总和= 3+3+3 = 9，这是最大可能值。

**方法:**给定的问题可以通过计算数组元素的频率，然后找到最大和来解决，这在本文的[上一篇文章](https://www.geeksforgeeks.org/maximize-sum-selected-numbers-performing-following-operation/)中讨论过。

**时间复杂度:** O(M + F)，其中 **M** 是数组的[最大元素，F 是一个数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的[最大频率。
**辅助空间:** O(M)，其中 **M** 为数组](https://www.geeksforgeeks.org/frequent-element-array/)的[最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

[**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) **方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化求解。可以观察到，如果选择数组**arr【】**的一个数 **A <sub>i</sub>** ，它会将**A<sub>I</sub>* freq【A<sub>I</sub>**贡献到最终的和中。根据这一观察，按照以下步骤解决给定的问题:

*   创建一个数组 **freq[]** ，存储数组 **arr[]** 中每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   创建一个 **1D** 数组 **dp[]** ，其中 **dp[i]** 代表给定数组中范围**【1，I】**内所选值的最大可能和。
*   对于 **i** 的每个值，有两种可能的情况如下:
    *   情况 1，选择 **i** 。在这种情况下， **dp[i] = freq[i] * i + dp[i-2]** 的值。
    *   情况 2，选择**I–1**。在这种情况下， **dp[i] = dp[i-1]** 的值。
*   因此，上述问题的 DP 关系为:

> **DP[I]= max(DP[I–1]，(freq[I]* I)+DP[I–2])**范围[0，MAX]内 I 的所有值，其中 MAX 是 arr[]中的最大整数

*   存储在**DP【MAX】**中的值是要求的答案。

下面是上述方法的实现:

## C++

```
// cpp program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// selected numbers from an array to make
// the array empty
int maximizeSum(vector<int> arr)
{

    // Edge Case
    if (arr.size() == 0)
        return 0;

    // Stores the frequency of each element
    // in the range [0, MAX] where MAX is
    // the maximum integer in the array arr

    int mx= *max_element(arr.begin(),arr.end());
    int freq[mx + 1]={0};

    // Loop to iterate over array arr[]
    for (int i : arr)
        freq[i] += 1;

    // Stores the DP states
    int dp[mx + 1]={0};

    // Initially dp[1] = freq[1]
    dp[1] = freq[1];

    // Iterate over the range [2, MAX]
    for (int i = 2; i < mx + 1; i++)
        dp[i] = max(freq[i] * i + dp[i - 2],
                    dp[i - 1]);

    // Return Answer
    return dp[mx];
}

// Driver Code
int main()
{
    vector<int> arr = {2, 2, 3, 3, 3, 4};

    // Function Call
    cout << (maximizeSum(arr));
}

// This code is contributed by amreshkumar3.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
class GFG
{

    // Utility function to find
    // maximum value of an element in array
    static int getMax(int [] arr)
    {
        int max = Integer.MIN_VALUE;

          for(int i = 0; i < arr.length; i++)
        {
           if(arr[i] > max)
             max = arr[i];
        }

          return max;

    }

    // Function to find the maximum sum of
    // selected numbers from an array to make
    // the array empty
    static int maximizeSum(int [] arr)
    {

        // Edge Case
        if (arr.length == 0)
            return 0;

        // Stores the frequency of each element
        // in the range [0, MAX] where MAX is
        // the maximum integer in the array arr

        int max = getMax(arr);
        int [] freq = new int[max + 1];

        // Loop to iterate over array arr[]
        for (int i : arr)
          freq[i] += 1;

        // Stores the DP states
        int[] dp = new int[max + 1];

        // Initially dp[1] = freq[1]
        dp[1] = freq[1];

        // Iterate over the range [2, MAX]
        for (int i = 2; i < max + 1; i++)
            dp[i] = Math.max(freq[i] * i + dp[i - 2],
                             dp[i - 1]);

        // Return Answer
        return dp[max];
    }

    // Driver Code
    public static void main(String [] args)
    {
        int [] arr = { 2, 2, 3, 3, 3, 4 };

        // Function Call
        System.out.println((maximizeSum(arr)));
    }
}

// This code is contributed by AR_Gaurav
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum sum of
# selected numbers from an array to make
# the array empty
def maximizeSum(arr):

    # Edge Case
    if not arr:
        return 0

    # Stores the frequency of each element
    # in the range [0, MAX] where MAX is
    # the maximum integer in the array arr
    freq = [0] * (max(arr)+1)

    # Loop to iterate over array arr[]
    for i in arr:
        freq[i] += 1

    # Stores the DP states
    dp = [0] * (max(arr)+1)

    # Initially dp[1] = freq[1]
    dp[1] = freq[1]

    # Iterate over the range [2, MAX]
    for i in range(2, max(arr)+1):
        dp[i] = max(freq[i]*i + dp[i-2], dp[i-1])

    # Return Answer
    return dp[max(arr)]

# Driver Code
arr = [2, 2, 3, 3, 3, 4]

# Function Call
print(maximizeSum(arr))
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
class GFG
{

    // Function to find the maximum sum of
    // selected numbers from an array to make
    // the array empty
    static int maximizeSum(int[] arr)
    {

        // Edge Case
        if (arr.Length == 0)
            return 0;

        // Stores the frequency of each element
        // in the range [0, MAX] where MAX is
        // the maximum integer in the array arr
        int[] freq = new int[(arr.Max() + 1)];

        // Loop to iterate over array arr[]
        foreach(int i in arr) freq[i] += 1;

        // Stores the DP states
        int[] dp = new int[(arr.Max() + 1)];

        // Initially dp[1] = freq[1]
        dp[1] = freq[1];

        // Iterate over the range [2, MAX]
        for (int i = 2; i < arr.Max() + 1; i++)
            dp[i] = Math.Max(freq[i] * i + dp[i - 2],
                             dp[i - 1]);

        // Return Answer
        return dp[arr.Max()];
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 2, 3, 3, 3, 4 };

        // Function Call
        Console.WriteLine((maximizeSum(arr)));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach

      // Function to find the maximum sum of
      // selected numbers from an array to make
      // the array empty
      function maximizeSum(arr) {

          // Edge Case
          if (arr.length == 0)
              return 0;

          // Stores the frequency of each element
          // in the range [0, MAX] where MAX is
          // the maximum integer in the array arr
          let freq = new Array(Math.max(...arr) + 1).fill(0);

          // Loop to iterate over array arr[]
          for (let i = 0; i < arr.length; i++)
              freq[arr[i]] += 1

          // Stores the DP states
          let dp = new Array(Math.max(...arr) + 1).fill(0);

          // Initially dp[1] = freq[1]
          dp[1] = freq[1]

          // Iterate over the range [2, MAX]
          for (let i = 2; i <= Math.max(...arr) + 1; i++)
              dp[i] = Math.max(freq[i] * i + dp[i - 2], dp[i - 1])

          // Return Answer
          return dp[Math.max(...arr)]
      }
      // Driver Code
      let arr = [2, 2, 3, 3, 3, 4]

      // Function Call
      document.write(maximizeSum(arr))

   // This code is contributed by Potta Lokesh

  </script>
```

**Output:** 

```
9
```

***时间复杂度:** O(M + F)，其中 **M** 是* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(M)，其中 **M** 是* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*