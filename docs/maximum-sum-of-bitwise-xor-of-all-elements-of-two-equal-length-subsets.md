# 两个等长子集所有元素的按位异或的最大和

> 原文:[https://www . geesforgeks . org/两个等长子集的所有元素的最大按位异或和/](https://www.geeksforgeeks.org/maximum-sum-of-bitwise-xor-of-all-elements-of-two-equal-length-subsets/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **N** 是一个偶数。任务是将给定的 **N** 个整数分成两个相等的子集，使得两个子集的所有元素的按位异或之和最大。

**示例:**

> **输入:** N= 4，arr[] = {1，2，3，4}
> **输出:** 10
> **解释:**
> 有 3 种可能的方式:
> (1，2)(3，4) = (1^2)+(3^4) = 10
> (1，3)(2，4) = (1^3)+(2^3) = 8
> (1，4)(2，3) = (1^4)+(2^3) = 6
> 因此，最大和= 0
> 
> **输入:** N= 6，arr[] = {4，5，3，2，5，6 }
> T3】输出: 17

**天真方法:**想法是检查每一个可能的 **N/2** 对的分布。打印两个子集所有元素之和的最大值[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，思路是使用[使用位屏蔽的动态编程](https://www.geeksforgeeks.org/bitmasking-dynamic-programming-set-2-tsp/)。按照以下步骤解决问题:

1.  最初，位掩码为 0，如果该位被置位，则该对已被选取。
2.  遍历所有可能的对，检查是否可以选择一对，即 **i 和 j** 的位没有设置在**掩码**中:
    *   如果有可能获取该对，则找到当前对的**位异或**和，并递归检查下一对。
    *   否则检查下一对元素。
3.  对于每个递归调用，继续更新上面步骤中的最大异或对和。
4.  打印保存在 **dp【掩码】**中的所有可能对的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function that finds the maximum
// Bitwise XOR sum of the two subset
int xorSum(int a[], int n,
           int mask, int dp[])
{
  // Check if the current state is
  // already computed
  if (dp[mask] != -1)
  {
    return dp[mask];
  }

  // Initialize answer to minimum value
  int max_value = 0;

  // Iterate through all possible pairs
  for (int i = 0; i < n; i++)
  {
    for (int j = i + 1; j < n; j++)
    {

      // Check whether ith bit and
      // jth bit of mask is not
      // set then pick the pair
      if (i != j &&
         (mask & (1 << i)) == 0 &&
         (mask & (1 << j)) == 0)
      {

        // For all possible pairs
        // find maximum value pick
        // current a[i], a[j] and
        // set i, j th bits in mask
        max_value = max(max_value, (a[i] ^ a[j]) +
                        xorSum(a, n, (mask | (1 << i) |
                                               (1 << j)), dp));
      }
    }
  }

  // Store the maximum value
  // and return the answer
  return dp[mask] = max_value;
}

// Driver Code
int main()
{
   int n = 4;

   // Given array arr[]
   int arr[] = { 1, 2, 3, 4 };

   // Declare Initialize the dp states
   int dp[(1 << n) + 5];
   memset(dp, -1, sizeof(dp));

   // Function Call
   cout << (xorSum(arr, n, 0, dp));
}

// This code is contributed by Rohit_ranjan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

public class GFG {

    // Function that finds the maximum
    // Bitwise XOR sum of the two subset
    public static int xorSum(int a[], int n,
                             int mask, int[] dp)
    {
        // Check if the current state is
        // already computed
        if (dp[mask] != -1) {
            return dp[mask];
        }

        // Initialize answer to minimum value
        int max_value = 0;

        // Iterate through all possible pairs
        for (int i = 0; i < n; i++) {

            for (int j = i + 1; j < n; j++) {

                // Check whether ith bit and
                // jth bit of mask is not
                // set then pick the pair
                if (i != j
                    && (mask & (1 << i)) == 0
                    && (mask & (1 << j)) == 0) {

                    // For all possible pairs
                    // find maximum value pick
                    // current a[i], a[j] and
                    // set i, j th bits in mask
                    max_value = Math.max(
                        max_value,
                        (a[i] ^ a[j])
                            + xorSum(a, n,
                                     (mask | (1 << i)
                                      | (1 << j)),
                                     dp));
                }
            }
        }

        // Store the maximum value
        // and return the answer
        return dp[mask] = max_value;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 4;

        // Given array arr[]
        int arr[] = { 1, 2, 3, 4 };

        // Declare Initialize the dp states
        int dp[] = new int[(1 << n) + 5];
        Arrays.fill(dp, -1);

        // Function Call
        System.out.println(xorSum(arr, n, 0, dp));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function that finds the maximum
# Bitwise XOR sum of the two subset
def xorSum(a, n, mask, dp):

    # Check if the current state is
    # already computed
    if(dp[mask] != -1):
        return dp[mask]

    # Initialize answer to minimum value
    max_value = 0

    # Iterate through all possible pairs
    for i in range(n):
        for j in range(i + 1, n):

            # Check whether ith bit and
            # jth bit of mask is not
            # set then pick the pair
            if(i != j and
              (mask & (1 << i)) == 0 and
              (mask & (1 << j)) == 0):

                # For all possible pairs
                # find maximum value pick
                # current a[i], a[j] and
                # set i, j th bits in mask
                max_value = max(max_value,
                               (a[i] ^ a[j]) +
                                xorSum(a, n,
                                (mask | (1 << i) |
                                (1 << j)), dp))

    # Store the maximum value
    # and return the answer
    dp[mask] = max_value

    return dp[mask]

# Driver Code
n = 4

# Given array arr[]
arr = [ 1, 2, 3, 4 ]

# Declare Initialize the dp states
dp = [-1] * ((1 << n) + 5)

# Function call
print(xorSum(arr, n, 0, dp))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that finds the maximum
// Bitwise XOR sum of the two subset
public static int xorSum(int []a, int n,
                         int mask, int[] dp)
{

    // Check if the current state is
    // already computed
    if (dp[mask] != -1)
    {
        return dp[mask];
    }

    // Initialize answer to minimum value
    int max_value = 0;

    // Iterate through all possible pairs
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Check whether ith bit and
            // jth bit of mask is not
            // set then pick the pair
            if (i != j &&
               (mask & (1 << i)) == 0 &&
               (mask & (1 << j)) == 0)
            {

                // For all possible pairs
                // find maximum value pick
                // current a[i], a[j] and
                // set i, j th bits in mask
                max_value = Math.Max(
                            max_value,
                            (a[i] ^ a[j]) +
                            xorSum(a, n, (mask |
                            (1 << i) | (1 << j)), dp));
            }
        }
    }

    // Store the maximum value
    // and return the answer
    return dp[mask] = max_value;
}

// Driver Code
public static void Main(String []args)
{
    int n = 4;

    // Given array []arr
    int []arr = { 1, 2, 3, 4 };

    // Declare Initialize the dp states
    int []dp = new int[(1 << n) + 5];
    for(int i = 0; i < dp.Length; i++)
        dp[i] = -1;

    // Function call
    Console.WriteLine(xorSum(arr, n, 0, dp));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that finds the maximum
// Bitwise XOR sum of the two subset
function xorSum(a, n, mask, dp)
{
  // Check if the current state is
  // already computed
  if (dp[mask] != -1)
  {
    return dp[mask];
  }

  // Initialize answer to minimum value
  var max_value = 0;

  // Iterate through all possible pairs
  for (var i = 0; i < n; i++)
  {
    for (var j = i + 1; j < n; j++)
    {

      // Check whether ith bit and
      // jth bit of mask is not
      // set then pick the pair
      if (i != j &&
         (mask & (1 << i)) == 0 &&
         (mask & (1 << j)) == 0)
      {

        // For all possible pairs
        // find maximum value pick
        // current a[i], a[j] and
        // set i, j th bits in mask
        max_value = Math.max(max_value, (a[i] ^ a[j]) +
                        xorSum(a, n, (mask | (1 << i) |
                                        (1 << j)), dp));
      }
    }
  }

  // Store the maximum value
  // and return the answer
  return dp[mask] = max_value;
}

// Driver Code

var n = 4;

// Given array arr[]
var arr = [1, 2, 3, 4];

// Declare Initialize the dp states
var dp = Array((1 << n) + 5).fill(-1);

// Function Call
document.write(xorSum(arr, n, 0, dp));

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N <sup>2</sup> *2 <sup>N</sup> ，其中 N 为给定数组的大小*
***辅助空间:** O(N)*