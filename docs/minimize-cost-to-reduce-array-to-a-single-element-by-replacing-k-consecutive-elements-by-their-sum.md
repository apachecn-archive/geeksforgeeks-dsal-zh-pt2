# 通过将 K 个连续的元素替换为它们的和来最小化成本，从而将数组缩减为单个元素

> 原文:[https://www . geeksforgeeks . org/通过用它们的总和替换 k 个连续元素来最小化将数组减少到单个元素的成本/](https://www.geeksforgeeks.org/minimize-cost-to-reduce-array-to-a-single-element-by-replacing-k-consecutive-elements-by-their-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找到将给定数组缩减为单个元素所需的最小成本，其中用其和替换 **K** 连续数组元素的成本等于 **K** 连续元素的总和。如果无法将给定数组简化为单个元素，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，5，1，2，6}，K = 3
> **输出:** 25
> **解释:**
> 替换{arr[1]，arr[2]，arr[3]}修改 arr[] = {3，8，6}。成本= 8
> 替换{arr[0]，arr[1]，arr[2]}会修改 arr[] = {17}。成本= 17。
> 因此，将所有数组元素合并为一个的总成本= 8 + 17 = 25
> 
> **输入:** arr[] = {3，2，4，1}，K = 3
> **输出:** -1
> 合并任意 K (=3)个连续的数组元素在数组中留下 2 个元素。
> 因此，要求的输出为-1。

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。以下是循环关系:

> 由于数组的大小在每次替换操作后减少(K–1)，
> dp[i][j] = min(dp[i][x]，dp[x+1][j])，X = i +整数*(K–1)
> 其中，dp[i][j]存储在区间[i，j]中合并最大数目的数组元素的最小成本，如果可能，最左边的元素 arr[i]总是参与合并

按照以下步骤解决问题:

*   如果**(N–1)%(K–1)！= 0** 然后打印 **-1** 。
*   初始化一个[数组](https://www.geeksforgeeks.org/python-list/)，比如 prefixSum[]来存储给定数组的前缀和。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/python-using-2d-arrays-lists-the-right-way/)，比如说 **dp[][]** ，其中 **dp[i][j]** 存储在区间**【I，j】**内合并数组元素最大数目的最小代价。
*   使用上述差压状态之间的关系填写差压表。
*   最后，打印**DP【0】【N–1】**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to reduce given array to a single
// element by replacing consecutive
// K array elements
int minimumCostToMergeK(int arr[], int K, int N)
{

    // If (N - 1) is not
    // multiple of (K - 1)
    if ((N - 1) % (K - 1) != 0)
    {
        return -1;
    }

    // Store prefix sum of the array
    int prefixSum[N + 1] = {0};

    // Iterate over the range [1, N]
    for(int i = 1; i < (N + 1); i++)
    {

        // Update prefixSum[i]
        prefixSum[i] = (prefixSum[i - 1] + arr[i - 1]);

    }

    // dp[i][j]: Store minimum cost to
    // merge array elements interval [i, j]
    int dp[N][N];
    memset(dp, 0, sizeof(dp));

    // L: Stores length of interval [i, j]
    for(int L = K; L < (N + 1); L++)
    {

        // Iterate over each interval
        // [i, j] of length L in in [0, N]
        for(int i = 0; i < (N - L + 1); i++)
        {

            // Stores index of last element
            // of the interval [i, j]
            int j = i + L - 1;

            // If L is greater than K
            if (L > K)
            {
                int temp = INT_MAX;
                for(int x = i; x < j; x += K - 1)
                {
                    temp = min(temp, dp[i][x] +
                                     dp[x + 1][j]);
                }

                // Update dp[i][j]
                dp[i][j] = temp;
            }

            // If (L - 1) is multiple of (K - 1)
            if ((L - 1) % (K - 1) == 0)
            {

                // Update dp[i][j]
                dp[i][j] += (prefixSum[j + 1] -
                             prefixSum[i]);
            }
        }
    }

    // Return dp[0][N - 1]
    return dp[0][N - 1];
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 1, 2, 6 };
    int K = 3;

      // Stores length of arr
      int N = sizeof(arr) / sizeof(arr[0]);

    cout << minimumCostToMergeK(arr, K, N);
}

// This code is contributed by rag2127
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the minimum cost
  // to reduce given array to a single
  // element by replacing consecutive
  // K array elements
  static int minimumCostToMergeK(int arr[], int K, int N)
  {

    // If (N - 1) is not
    // multiple of (K - 1)
    if ((N - 1) % (K - 1) != 0)
    {
      return -1;
    }

    // Store prefix sum of the array
    int []prefixSum = new int[N + 1];

    // Iterate over the range [1, N]
    for(int i = 1; i < (N + 1); i++)
    {

      // Update prefixSum[i]
      prefixSum[i] = (prefixSum[i - 1] + arr[i - 1]);

    }

    // dp[i][j]: Store minimum cost to
    // merge array elements interval [i, j]
    int [][]dp = new int[N][N];

    // L: Stores length of interval [i, j]
    for(int L = K; L < (N + 1); L++)
    {

      // Iterate over each interval
      // [i, j] of length L in in [0, N]
      for(int i = 0; i < (N - L + 1); i++)
      {

        // Stores index of last element
        // of the interval [i, j]
        int j = i + L - 1;

        // If L is greater than K
        if (L > K)
        {
          int temp = Integer.MAX_VALUE;
          for(int x = i; x < j; x += K - 1)
          {
            temp = Math.min(temp, dp[i][x] +
                            dp[x + 1][j]);
          }

          // Update dp[i][j]
          dp[i][j] = temp;
        }

        // If (L - 1) is multiple of (K - 1)
        if ((L - 1) % (K - 1) == 0)
        {

          // Update dp[i][j]
          dp[i][j] += (prefixSum[j + 1] -
                       prefixSum[i]);
        }
      }
    }

    // Return dp[0][N - 1]
    return dp[0][N - 1];
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 3, 5, 1, 2, 6 };
    int K = 3;

    // Stores length of arr
    int N = arr.length;
    System.out.print(minimumCostToMergeK(arr, K, N));
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum cost
# to reduce given array to a single
# element by replacing consecutive
# K array elements
def minimumCostToMergeK(arr, K): 

    # Stores length of arr
    N = len(arr)

    # If (N - 1) is not
    # multiple of (K - 1)
    if (N - 1) % (K - 1) != 0:
        return -1

    # Store prefix sum of the array
    prefixSum = [0] * (N + 1)

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Update prefixSum[i]
        prefixSum[i] = (prefixSum[i - 1]
                         + arr[i - 1])

    # dp[i][j]: Store minimum cost to
    # merge array elements interval [i, j]
    dp = [[0]*N for _ in range(N)]

    # L: Stores length of interval [i, j]
    for L in range(K, N + 1):

        # Iterate over each interval
        # [i, j] of length L in in [0, N]
        for i in range(N - L + 1):

            # Stores index of last element
            # of the interval [i, j]
            j = i + L - 1

            # If L is greater than K
            if L > K:

                # Update dp[i][j]
                dp[i][j] =(
                     min([dp[i][x] + dp[x + 1][j]
                     for x in range(i, j, K-1)]))

            # If (L - 1) is multiple of (K - 1)               
            if (L - 1) % (K - 1) == 0:

                # Update dp[i][j]
                dp[i][j] += (prefixSum[j + 1]
                              - prefixSum[i])

    # Return dp[0][N - 1]
    return dp[0][N-1]

if __name__ == "__main__":
    arr = [3, 5, 1, 2, 6]
    K = 3
    print(minimumCostToMergeK(arr, K))
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find the minimum cost
  // to reduce given array to a single
  // element by replacing consecutive
  // K array elements
  static int minimumCostToMergeK(int []arr, int K, int N)
  {

    // If (N - 1) is not
    // multiple of (K - 1)
    if ((N - 1) % (K - 1) != 0)
    {
      return -1;
    }

    // Store prefix sum of the array
    int []prefixSum = new int[N + 1];

    // Iterate over the range [1, N]
    for(int i = 1; i < (N + 1); i++)
    {

      // Update prefixSum[i]
      prefixSum[i] = (prefixSum[i - 1] + arr[i - 1]);

    }

    // dp[i,j]: Store minimum cost to
    // merge array elements interval [i, j]
    int [,]dp = new int[N,N];

    // L: Stores length of interval [i, j]
    for(int L = K; L < (N + 1); L++)
    {

      // Iterate over each interval
      // [i, j] of length L in in [0, N]
      for(int i = 0; i < (N - L + 1); i++)
      {

        // Stores index of last element
        // of the interval [i, j]
        int j = i + L - 1;

        // If L is greater than K
        if (L > K)
        {
          int temp = int.MaxValue;
          for(int x = i; x < j; x += K - 1)
          {
            temp = Math.Min(temp, dp[i, x] +
                            dp[x + 1, j]);
          }

          // Update dp[i,j]
          dp[i, j] = temp;
        }

        // If (L - 1) is multiple of (K - 1)
        if ((L - 1) % (K - 1) == 0)
        {

          // Update dp[i,j]
          dp[i, j] += (prefixSum[j + 1] -
                       prefixSum[i]);
        }
      }
    }

    // Return dp[0,N - 1]
    return dp[0, N - 1];
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 3, 5, 1, 2, 6 };
    int K = 3;

    // Stores length of arr
    int N = arr.Length;
    Console.Write(minimumCostToMergeK(arr, K, N));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to find the minimum cost
    // to reduce given array to a single
    // element by replacing consecutive
    // K array elements
    function minimumCostToMergeK(arr , K , N)
    {

        // If (N - 1) is not
        // multiple of (K - 1)
        if ((N - 1) % (K - 1) != 0) {
            return -1;
        }

        // Store prefix sum of the array
        var prefixSum = Array(N + 1).fill(0);

        // Iterate over the range [1, N]
        for (i = 1; i < (N + 1); i++) {

            // Update prefixSum[i]
            prefixSum[i] = (prefixSum[i - 1] + arr[i - 1]);

        }

        // dp[i][j]: Store minimum cost to
        // merge array elements interval [i, j]
        var dp = Array(N);
        for( i = 0; i<N;i++)
        dp[i] = Array(N).fill(0);

        // L: Stores length of interval [i, j]
        for (L = K; L < (N + 1); L++) {

            // Iterate over each interval
            // [i, j] of length L in in [0, N]
            for (i = 0; i < (N - L + 1); i++) {

                // Stores index of last element
                // of the interval [i, j]
                var j = i + L - 1;

                // If L is greater than K
                if (L > K) {
                    var temp = Number.MAX_VALUE;
                    for (x = i; x < j; x += K - 1) {
                        temp = Math.min(temp, dp[i][x] + dp[x + 1][j]);
                    }

                    // Update dp[i][j]
                    dp[i][j] = temp;
                }

                // If (L - 1) is multiple of (K - 1)
                if ((L - 1) % (K - 1) == 0) {

                    // Update dp[i][j]
                    dp[i][j] += (prefixSum[j + 1] - prefixSum[i]);
                }
            }
        }

        // Return dp[0][N - 1]
        return dp[0][N - 1];
    }

    // Driver Code

        var arr = [ 3, 5, 1, 2, 6 ];
        var K = 3;

        // Stores length of arr
        var N = arr.length;
        document.write(minimumCostToMergeK(arr, K, N));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
25
```

***时间复杂度:**O(N<sup>2</sup>* K)*
***辅助空间:** O(N <sup>2</sup> )*