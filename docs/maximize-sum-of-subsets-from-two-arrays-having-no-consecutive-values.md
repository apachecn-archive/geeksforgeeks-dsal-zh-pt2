# 最大化没有连续值的两个数组的子集之和

> 原文:[https://www . geeksforgeeks . org/最大化具有非连续值的两个数组的子集和/](https://www.geeksforgeeks.org/maximize-sum-of-subsets-from-two-arrays-having-no-consecutive-values/)

给定两个长度相等的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr 1【】**和**arr 2【】**，任务是通过从两个数组中选择元素来找到任何可能的子集的最大和，使得子集中没有两个元素应该是连续的。

**示例:**

> **输入:** arr1[] = {-1，-2，4，-4，5}，arr2[] = {-1，-2，-3，4，10}
> **输出:** 14
> **解释:**
> 必选子集{4，10}。因此，sum = 4 + 10 = 14。
> 
> **输入:** arr1[] = {2，5，4，2000}，arr2[] = {-2000，100，23，40}
> **输出:** 2100

**朴素方法:**最简单的方法是[从两个给定的数组中生成所有可能的子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，使得没有两个相邻的元素是连续的，并计算每个子集的和。最后，打印最大可能的总和。
***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的辅助数组 **dp[]** 。
*   这里， **dp[i]** 存储来自两个阵列的子集的最大可能和，使得没有两个元素是连续的。
*   声明一个函数 **maximumSubsetSum():**
    *   基本案例:
        *   **dp[1] =最大值(arr1[1]，arr2[1])。**
        *   **dp[2] =最大值(arr1[1]，arr2[1])、最大值(arr1[2]，arr2[2])。**
    *   对于所有其他情况，会出现以下三种情况:
        *   **dp[i] = max（arr1[i]， scar2[i]， scar1[i] + dp[i – 2]， scar2[i] + dp[i – 2]， dp[i – 1]）。**
*   最后打印**DP【N】**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum subset sum
void maximumSubsetSum(int arr1[],int arr2[], int length)
{

    // Initialize array to store dp states
    int dp[length+1];

    // Base Cases
    if (length == 1)
    {
        cout << (max(arr1[0], arr2[0]));
        return;
    }

    if (length == 2)
    {
        cout << (max(max(arr1[1], arr2[1]), max(arr1[0], arr2[0])));
        return;
    }
    else
    {

        // Pre initializing for dp[0] & dp[1]
        dp[0] = max(arr1[0], arr2[0]);
        dp[1] = max(max(arr1[1], arr2[1]), max(arr1[0], arr2[0]));

        int index = 2;
        while (index < length)
        {

            // Calculating dp[index] based on
            // above formula
            dp[index] = max(max(arr1[index], arr2[index]),
                max(max(arr1[index] + dp[index - 2],
                        arr2[index] + dp[index - 2]),
                    dp[index - 1]));
            ++index;
        }

        // Print maximum subset sum
        cout<<(dp[length - 1]);
    }
}

// Driver Code
int main()
{

  // Given arrays
  int arr1[] = { -1, -2, 4, -4, 5 };
  int arr2[] = { -1, -2, -3, 4, 10 };

  // Length of the array
  int length = 5;
  maximumSubsetSum(arr1, arr2, length);
  return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to calculate maximum subset sum
    static void maximumSubsetSum(int arr1[],
                                 int arr2[],
                                 int length)
    {

        // Initialize array to store dp states
        int dp[] = new int[length + 1];

        // Base Cases
        if (length == 1) {
            System.out.print(
                Math.max(arr1[0], arr2[0]));
            return;
        }

        if (length == 2) {
            System.out.print(
                Math.max(
                    Math.max(arr1[1], arr2[1]),
                    Math.max(arr1[0], arr2[0])));
            return;
        }
        else {

            // Pre initializing for dp[0] & dp[1]
            dp[0] = Math.max(arr1[0], arr2[0]);
            dp[1] = Math.max(
                Math.max(arr1[1], arr2[1]),
                Math.max(arr1[0], arr2[0]));

            int index = 2;
            while (index < length) {

                // Calculating dp[index] based on
                // above formula
                dp[index] = Math.max(
                    Math.max(arr1[index], arr2[index]),
                    Math.max(
                        Math.max(
                            arr1[index] + dp[index - 2],
                            arr2[index] + dp[index - 2]),
                        dp[index - 1]));
                ++index;
            }

            // Print maximum subset sum
            System.out.print(dp[length - 1]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given arrays
        int arr1[] = { -1, -2, 4, -4, 5 };
        int arr2[] = { -1, -2, -3, 4, 10 };

        // Length of the array
        int length = arr1.length;

        maximumSubsetSum(arr1, arr2, length);
    }
}
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to calculate maximum subset sum
def maximumSubsetSum(arr1, arr2, length) :

    # Initialize array to store dp states
    dp = [0] * (length+1)

    # Base Cases
    if (length == 1) :     
        print(max(arr1[0], arr2[0]))
        return
    if (length == 2) :
        print(max(max(arr1[1], arr2[1]), max(arr1[0], arr2[0])))
        return 
    else  :

        # Pre initializing for dp[0] & dp[1]
        dp[0] = max(arr1[0], arr2[0])
        dp[1] = max(max(arr1[1], arr2[1]), max(arr1[0], arr2[0]))
        index = 2
        while (index < length) :

            # Calculating dp[index] based on
            # above formula
            dp[index] = max(max(arr1[index], arr2[index]),
                max(max(arr1[index] + dp[index - 2],
                        arr2[index] + dp[index - 2]),
                    dp[index - 1]))
            index += 1

        # Prmaximum subset sum
        print(dp[length - 1])

# Driver Code

# Given arrays
arr1 = [ -1, -2, 4, -4, 5 ]
arr2 = [ -1, -2, -3, 4, 10 ]

# Length of the array
length = 5
maximumSubsetSum(arr1, arr2, length)

# This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to calculate maximum subset sum
  static void maximumSubsetSum(int[] arr1,
                               int[] arr2,
                               int length)
  {

    // Initialize array to store dp states
    int[] dp = new int[length + 1];

    // Base Cases
    if (length == 1) {
      Console.WriteLine(Math.Max(arr1[0], arr2[0]));
      return;
    }

    if (length == 2)
    {
      Console.WriteLine(Math.Max(
        Math.Max(arr1[1], arr2[1]),
        Math.Max(arr1[0], arr2[0])));
      return;
    }
    else
    {

      // Pre initializing for dp[0] & dp[1]
      dp[0] = Math.Max(arr1[0], arr2[0]);
      dp[1] = Math.Max(Math.Max(arr1[1], arr2[1]),
                       Math.Max(arr1[0], arr2[0]));

      int index = 2;
      while (index < length) {

        // Calculating dp[index] based on
        // above formula
        dp[index] = Math.Max(Math.Max(arr1[index], arr2[index]),
                             Math.Max(Math.Max(arr1[index] +
                                               dp[index - 2],
                                               arr2[index] +
                                               dp[index - 2]),
                                      dp[index - 1]));
        ++index;
      }

      // Print maximum subset sum
      Console.WriteLine(dp[length - 1]);
    }
  }

  // Driver Code
  static public void Main()
  {

    // Given arrays
    int[] arr1 = { -1, -2, 4, -4, 5 };
    int[] arr2 = { -1, -2, -3, 4, 10 };

    // Length of the array
    int length = arr1.Length;

    maximumSubsetSum(arr1, arr2, length);
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// javascript program of the above approach

    // Function to calculate maximum subset sum
    function maximumSubsetSum(arr1, arr2,length)
    {

        // Initialize array to store dp states
        let dp = new Array(length).fill(0);;

        // Base Cases
        if (length == 1) {
            document.write(
                Math.max(arr1[0], arr2[0]));
            return;
        }

        if (length == 2) {
            document.write(
                Math.max(
                    Math.max(arr1[1], arr2[1]),
                    Math.max(arr1[0], arr2[0])));
            return;
        }
        else {

            // Pre initializing for dp[0] & dp[1]
            dp[0] = Math.max(arr1[0], arr2[0]);
            dp[1] = Math.max(
                Math.max(arr1[1], arr2[1]),
                Math.max(arr1[0], arr2[0]));

            let index = 2;
            while (index < length) {

                // Calculating dp[index] based on
                // above formula
                dp[index] = Math.max(
                    Math.max(arr1[index], arr2[index]),
                    Math.max(
                        Math.max(
                            arr1[index] + dp[index - 2],
                            arr2[index] + dp[index - 2]),
                        dp[index - 1]));
                ++index;
            }

            // Prlet maximum subset sum
            document.write(dp[length - 1]);
        }
    }

    // Driver Code

    // Given arrays
        let arr1 = [ -1, -2, 4, -4, 5 ];
        let arr2 = [ -1, -2, -3, 4, 10 ];

        // Length of the array
        let length = arr1.length;

        maximumSubsetSum(arr1, arr2, length);

</script>
```

**Output:** 

```
14
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)