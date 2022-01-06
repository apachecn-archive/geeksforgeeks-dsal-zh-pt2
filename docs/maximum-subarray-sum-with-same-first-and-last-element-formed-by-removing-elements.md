# 通过移除元素形成的第一个和最后一个元素相同的最大子阵列和

> 原文:[https://www . geesforgeks . org/maximum-subarray-sum-具有相同的第一个和最后一个元素-通过移除元素形成/](https://www.geeksforgeeks.org/maximum-subarray-sum-with-same-first-and-last-element-formed-by-removing-elements/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出长度为**至少为 2 个**的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大和，该子数组的第一个和最后一个元素在移除任意数量的数组元素后是相同的。如果没有这样的数组，则打印 **0** 。

**示例:**

> **输入:** arr[] = { -1，-3，-2，4，-1，3}
> **输出:** 2
> **解释:**选择子数组{-1，-3，-2，4，-1}，去掉元素-3 和-2，使子数组为{-1，4，-1}，求和等于 2，即最大值。
> 
> **输入:**arr[]= {-1 }
> T3】输出: 0

**方法:**给定的问题可以用这样的思想来解决:首先[找到第一个和最后一个元素相同的所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并移除那些第一个和最后一个元素之间的所有负元素。这个想法可以通过使用[无序地图](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)在[本文](Maximum length of the sub-array whose first and last elements are same)中讨论的想法来实现。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说 **res** 为 **INT_MIN** ，它存储子阵列的合成最大和。
*   初始化一个变量，比如说 **currentSum** 为 **0** ，存储数组的运行[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   [初始化一个无序映射](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-user-defined-class-in-cpp/)，比如说 **memo[]** ，它存储了用前缀和映射的每个数组元素的值。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   将当前数组元素**arr【I】**的值添加到变量 **currentSum** 中。
    *   [如果地图](https://www.geeksforgeeks.org/map-find-function-in-c-stl/)中存在**arr【I】**，如果**arr【I】**的值为正，则将 **res** 的值更新为 **res** 和**的最大值(当前值–M[arr[I]]+arr[I])**。否则，将 res 值更新为 **res** 和**的最大值(current tsum–M[arr[I]]+2 * arr[I])**。
    *   否则，插入用**货币**映射的值**arr【I】**。
    *   如果当前值 **arr[i]** 为负，则从 **currentSum** 中递减，以排除可能的子阵列的负元素。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// of sub-array
int maximumSubarraySum(vector<int>& arr)
{

    // Initialize the variables
    int N = arr.size();
    unordered_map<int, int> memo;
    int res = INT_MIN;
    int currsum = 0, currval = 0;

    // Traverse over the range
    for (int i = 0; i < N; ++i) {

        // Add the current value to the
        // variable currsum for prefix sum
        currval = arr[i];
        currsum = currsum + currval;

        // Calculate the result
        if (memo.count(currval) != 0) {
            if (currval > 0)
                res = max(
                    res,
                    currsum - memo[currval]
                        + currval);
            else
                res = max(
                    res,
                    currsum - memo[currval]
                        + 2 * currval);
        }
        else
            memo[currval] = currsum;
        if (currval < 0)
            currsum = currsum - currval;
    }

    // Return the answer
    return res;
}

// Driver Code
int main()
{
    vector<int> arr = { -1, -3, 4, 0, -1, -2 };
    cout << maximumSubarraySum(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to find the maximum sum
    // of sub-array
    static int maximumSubarraySum(int arr[], int N)
    {

        // Initialize the variables
        HashMap<Integer, Integer> memo = new HashMap<>();
        int res = Integer.MIN_VALUE;
        int currsum = 0, currval = 0;

        // Traverse over the range
        for (int i = 0; i < N; ++i) {

            // Add the current value to the
            // variable currsum for prefix sum
            currval = arr[i];
            currsum = currsum + currval;

            // Calculate the result
            if (memo.containsKey(currval)) {
                if (currval > 0)
                    res = Math.max(
                        res, currsum - memo.get(currval)
                                 + currval);
                else
                    res = Math.max(
                        res, currsum - memo.get(currval)
                                 + 2 * currval);
            }
            else
                memo.put(currval, currsum);
            if (currval < 0)
                currsum = currsum - currval;
        }

        // Return the answer
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { -1, -3, 4, 0, -1, -2 };
        int N = 6;
        System.out.println(maximumSubarraySum(arr, N));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the maximum sum
# of sub-array
def maximumSubarraySum(arr) :

    # Initialize the variables
    N = len(arr);
    memo = {};
    res = -(sys.maxsize - 1);
    currsum = 0;
    currval = 0;

    # Traverse over the range
    for i in range(N) :

        # Add the current value to the
        # variable currsum for prefix sum
        currval = arr[i];
        currsum = currsum + currval;

        # Calculate the result
        if currval in memo :

            if (currval > 0) :
                res = max(res,currsum - memo[currval] + currval);
            else :
                res = max(res,currsum - memo[currval] + 2 * currval);

        else :
            memo[currval] = currsum;

        if (currval < 0) :
            currsum = currsum - currval;

    # Return the answer
    return res;

# Driver Code
if __name__ == "__main__" :

    arr = [ -1, -3, 4, 0, -1, -2 ];
    print(maximumSubarraySum(arr));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

    // Function to find the maximum sum
    // of sub-array
    static int maximumSubarraySum(int[] arr, int N)
    {

        // Initialize the variables
        Dictionary<int, int> memo = new
                Dictionary<int, int>();
        int res = Int32.MinValue;
        int currsum = 0, currval = 0;

        // Traverse over the range
        for (int i = 0; i < N; ++i) {

            // Add the current value to the
            // variable currsum for prefix sum
            currval = arr[i];
            currsum = currsum + currval;

            // Calculate the result
            if (memo.ContainsKey(currval)) {
                if (currval > 0)
                    res = Math.Max(
                        res, currsum - memo[(currval)]
                                 + currval);
                else
                    res = Math.Max(
                        res, currsum - memo[(currval)]
                                 + 2 * currval);
            }
            else
                memo.Add(currval, currsum);
            if (currval < 0)
                currsum = currsum - currval;
        }

        // Return the answer
        return res;
    }

// Driver Code
public static void Main()
{
    int[] arr = { -1, -3, 4, 0, -1, -2 };
    int N = 6;
    Console.WriteLine(maximumSubarraySum(arr, N));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the maximum sum
        // of sub-array
        function maximumSubarraySum(arr) {

            // Initialize the variables
            let N = arr.length;
            let memo = new Map();
            let res = -99999999;
            let currsum = 0, currval = 0;

            // Traverse over the range
            for (let i = 0; i < N; ++i) {

                // Add the current value to the
                // variable currsum for prefix sum
                currval = arr[i];
                currsum = currsum + currval;

                // Calculate the result
                if (memo.has(currval)) {
                    if (currval > 0)
                        res = Math.max(
                            res,
                            currsum - memo.get(currval)
                            + currval);
                    else
                        res = Math.max(
                            res,
                            currsum - memo.get(currval)
                            + 2 * currval);
                }
                else
                    memo.set(currval, currsum);
                if (currval < 0)
                    currsum = currsum - currval;
            }

            // Return the answer
            return res;
        }

        // Driver Code
        let arr = [-1, -3, 4, 0, -1, -2];
        document.write(maximumSubarraySum(arr));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)