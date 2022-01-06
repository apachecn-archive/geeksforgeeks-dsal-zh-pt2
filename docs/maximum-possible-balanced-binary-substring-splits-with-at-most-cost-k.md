# 最大可能的平衡二进制子串分裂，代价为 K

> 原文:[https://www . geesforgeks . org/最大可能平衡-二进制-子串-最高成本拆分-k/](https://www.geeksforgeeks.org/maximum-possible-balanced-binary-substring-splits-with-at-most-cost-k/)

给定一个二进制数组 **arr[]** 和值数组 **val[]** 。任务是找到二进制数组的**最大值**可能的拆分，这样每个段包含相同数量的 **0s** 和 **1s** ，最多使用 **k** 个硬币。每个拆分成本**(val[I]–val[j])<sup>2</sup>**，其中 **i** 和 **j** 是拆分段的相邻指标。

**示例:**

> **输入:** arr[] = {0，1，0，0，1，1}，val[] = {2，5，1，3，6，10}，k = 20
> **输出:** 1
> **说明:**拆分可以通过以下方式完成:0 1 **|** 0 0 1 和成本=(5–1)<sup>2</sup>= 16≤20。
> 
> **输入:** arr[] = {1，0，0，1，0，1，1，0}，val[] = {9，7，5，2，4，12，3，1]，k = 10
> **输出:** 2
> **解释:**拆分可以通过以下方式完成:1 0**|**0 1**|**0 1 1 0

**方法:**使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)(自顶向下的方法)可以解决任务。
遵循以下步骤:

1.  初始化一个二维矩阵，比如尺寸为 K * N 的 **dp**
2.  对于每个索引，有两个**选择，是在该索引上进行切割还是不在该索引上进行切割，前提是 0 和 1 的数量相等。**
3.  **记住要再次使用的值**
4.  **最大化 **count_splits** 的值，以获得最终的最大切割。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[1001][1001];

// Function to find maximum possible splits
// in atmost k coins such that each
// segment contains equal number of 0 and 1
int maximumSplits(int arr[], int val[],
                  int k, int N)
{
    // Base Case
    if (k < 0) {
        return INT_MIN;
    }

    // If already have a stored value
    // return it
    if (dp[k][N] != -1) {
        return dp[k][N];
    }

    // Count for zeros and ones
    int zero = 0, one = 0;

    // Count for number of splits
    int count_split = 0;
    int i;

    // Iterate over the array and
    // search for zeros and ones
    for (i = N - 1; i > 0; i--) {
        arr[i] == 0 ? zero++ : one++;

        // If count of zeros is equal to
        // count of ones
        if (zero == one) {
            // Store the maximum possible one
            count_split = max(
                count_split,
                1
                    + maximumSplits(
                          arr, val,
                          k - pow(val[i]
                                      - val[i - 1],
                                  2),
                          i));
        }
    }

    // If index is at 0, find if
    // it is zero or one and
    // increment the count
    if (i == 0) {
        arr[0] == 0 ? zero++ : one++;

        // If count of zero is not equal to
        // count of one, re-initialize
        // count_split with 0
        if (zero != one) {
            count_split = 0;
        }
    }

    // Store the returned value in dp[]
    return dp[k][N] = count_split;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 0, 1, 0, 1, 1, 0 };
    int val[] = { 9, 7, 5, 2, 4, 12, 3, 1 };
    int k = 10;

    int N = sizeof(arr) / sizeof(arr[0]);
    memset(dp, -1, sizeof(dp));

    cout << maximumSplits(arr, val, k, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
public class GFG
{

static int[][] dp = new int[1001][1001];

// Function to find maximum possible splits
// in atmost k coins such that each
// segment contains equal number of 0 and 1
static int maximumSplits(int[] arr, int[] val,
                  int k, int N)
{

    // Base Case
    if (k < 0) {
        return Integer.MIN_VALUE;
    }

    // If already have a stored value
    // return it
    if (dp[k][N] != -1) {
        return dp[k][N];
    }

    // Count for zeros and ones
    int zero = 0, one = 0;

    // Count for number of splits
    int count_split = 0;
    int i;

    // Iterate over the array and
    // search for zeros and ones
    for (i = N - 1; i > 0; i--) {
        if(arr[i] == 0)
            zero++;
        else
            one++;

        // If count of zeros is equal to
        // count of ones
        if (zero == one) {
            // Store the maximum possible one
            count_split = Math.max(
                count_split,
                1
                    + maximumSplits(
                          arr, val,
                          k - (int)Math.pow(val[i]
                                      - val[i - 1],
                                  2),
                          i));
        }
    }

    // If index is at 0, find if
    // it is zero or one and
    // increment the count
    if (i == 0) {
        if(arr[0] == 0)
            zero++;
        else
            one++;

        // If count of zero is not equal to
        // count of one, re-initialize
        // count_split with 0
        if (zero != one) {
            count_split = 0;
        }
    }

    // Store the returned value in dp[]
    return dp[k][N] = count_split;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 0, 0, 1, 0, 1, 1, 0 };
    int[] val = { 9, 7, 5, 2, 4, 12, 3, 1 };
    int k = 10;

    int N = arr.length;
    int i, j;
    for(i=0;i<1001;i++)
    {
        for(j=0;j<1001;j++)
        {
            dp[i][j] = -1;
        }
    }

    System.out.println(maximumSplits(arr, val, k, N));
}
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# Python Program to implement
# the above approach
dp = [0] * 1001
for i in range(len(dp)):
    dp[i] = [-1] * 1001

# Function to find maximum possible splits
# in atmost k coins such that each
# segment contains equal number of 0 and 1
def maximumSplits(arr, val, k, N):

    # Base Case
    if (k < 0):
        return 10 ** (-9)

    # If already have a stored value
    # return it
    if (dp[k][N] != -1) :
        return dp[k][N]

    # Count for zeros and ones
    zero = 0
    one = 0

    # Count for number of splits
    count_split = 0

    # Iterate over the array and
    # search for zeros and ones
    for i in range(N - 1, 0, -1):
        if (arr[i] == 0):
            zero += 1
        else: one += 1

        # If count of zeros is equal to
        # count of ones
        if (zero == one):

            # Store the maximum possible one
            count_split = max(
                count_split, 1
                + maximumSplits(
                    arr, val,
                    k - pow(val[i]
                                 - val[i - 1],
                                 2), i))

    # If index is at 0, find if
    # it is zero or one and
    # increment the count
    if (i == 0):
        if (arr[i] == 0):
            zero += 1
        else: one -= 1

        # If count of zero is not equal to
        # count of one, re-initialize
        # count_split with 0
        if (zero != one):
            count_split = 0

    # Store the returned value in dp[]
    dp[k][N] = count_split
    return dp[k][N]

# Driver Code
arr = [1, 0, 0, 1, 0, 1, 1, 0]
val = [9, 7, 5, 2, 4, 12, 3, 1]
k = 10

N = len(arr)

print(maximumSplits(arr, val, k, N))

# This code is contributed by Saurabh Jaiswal
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{

static int[,] dp = new int[1001, 1001];

// Function to find maximum possible splits
// in atmost k coins such that each
// segment contains equal number of 0 and 1
static int maximumSplits(int[] arr, int[] val,
                  int k, int N)
{
    // Base Case
    if (k < 0) {
        return Int32.MinValue;
    }

    // If already have a stored value
    // return it
    if (dp[k, N] != -1) {
        return dp[k, N];
    }

    // Count for zeros and ones
    int zero = 0, one = 0;

    // Count for number of splits
    int count_split = 0;
    int i;

    // Iterate over the array and
    // search for zeros and ones
    for (i = N - 1; i > 0; i--) {
        if(arr[i] == 0)
            zero++;
        else
            one++;

        // If count of zeros is equal to
        // count of ones
        if (zero == one) {
            // Store the maximum possible one
            count_split = Math.Max(
                count_split,
                1
                    + maximumSplits(
                          arr, val,
                          k - (int)Math.Pow(val[i]
                                      - val[i - 1],
                                  2),
                          i));
        }
    }

    // If index is at 0, find if
    // it is zero or one and
    // increment the count
    if (i == 0) {
        if(arr[0] == 0)
            zero++;
        else
            one++;

        // If count of zero is not equal to
        // count of one, re-initialize
        // count_split with 0
        if (zero != one) {
            count_split = 0;
        }
    }

    // Store the returned value in dp[]
    return dp[k, N] = count_split;
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 1, 0, 0, 1, 0, 1, 1, 0 };
    int[] val = { 9, 7, 5, 2, 4, 12, 3, 1 };
    int k = 10;

    int N = arr.Length;
    int i, j;
    for(i=0;i<1001;i++)
    {
        for(j=0;j<1001;j++)
        {
            dp[i, j] = -1;
        }
    }

    Console.WriteLine(maximumSplits(arr, val, k, N));
}
}

// This code is contributed by sanjoy_62.
```

## **java 描述语言**

```
<script>

      // JavaScript Program to implement
      // the above approach
      let dp = new Array(1001);
      for (let i = 0; i < dp.length; i++) {
          dp[i] = new Array(1001).fill(-1);
      }

      // Function to find maximum possible splits
      // in atmost k coins such that each
      // segment contains equal number of 0 and 1
      function maximumSplits(arr, val,
          k, N)
      {

          // Base Case
          if (k < 0) {
              return Number.MIN_VALUE;
          }

          // If already have a stored value
          // return it
          if (dp[k][N] != -1) {
              return dp[k][N];
          }

          // Count for zeros and ones
          let zero = 0, one = 0;

          // Count for number of splits
          let count_split = 0;
          let i;

          // Iterate over the array and
          // search for zeros and ones
          for (i = N - 1; i > 0; i--) {
              arr[i] == 0 ? zero++ : one++;

              // If count of zeros is equal to
              // count of ones
              if (zero == one)
              {

                  // Store the maximum possible one
                  count_split = Math.max(
                      count_split, 1
                      + maximumSplits(
                          arr, val,
                          k - Math.pow(val[i]
                              - val[i - 1],
                              2), i));
              }
          }

          // If index is at 0, find if
          // it is zero or one and
          // increment the count
          if (i == 0) {
              arr[0] == 0 ? zero++ : one++;

              // If count of zero is not equal to
              // count of one, re-initialize
              // count_split with 0
              if (zero != one) {
                  count_split = 0;
              }
          }

          // Store the returned value in dp[]
          return dp[k][N] = count_split;
      }

      // Driver Code
      let arr = [1, 0, 0, 1, 0, 1, 1, 0];
      let val = [9, 7, 5, 2, 4, 12, 3, 1];
      let k = 10;

      let N = arr.length;

      document.write(maximumSplits(arr, val, k, N))

  // This code is contributed by Potta Lokesh
  </script>
```

****Output**

```
2
```** 

*****时间复杂度*****:**O(N * K)
***辅助空间*** : O(N*K)**