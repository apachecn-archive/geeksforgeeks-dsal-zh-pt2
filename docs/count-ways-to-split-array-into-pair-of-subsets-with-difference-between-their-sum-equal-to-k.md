# 计算将数组拆分成子集对的方法，子集对的和之差等于 K

> 原文:[https://www . geeksforgeeks . org/count-将数组拆分成一对子集的方法-它们的和等于 k 之差/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-pair-of-subsets-with-difference-between-their-sum-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出将数组拆分成一对子集的方法，使得它们的和之差为 **K** 。

**示例:**

> **输入:** arr[] = {1，1，2，3}，K = 1
> **输出:** 3
> **解释:**
> 以下分成满足给定条件的一对子集:
> 
> 1.  {1，1，2}，{3}，差值=(1+1+2)–3 = 4–3 = 1。
> 2.  {1，3} {1，2}，差值=(1+3)–(1+2)= 4–3 = 1。
> 3.  {1，3} {1，2}，差值=(1+3)–(1+2)= 4–3 = 1。
> 
> 因此，拆分的方式数为 3。
> 
> **输入:** arr[] = {1，2，3}，K = 2
> **输出:** 1
> **解释:**
> 唯一可能分割成满足给定条件的一对子集的是{1，3}，{2}，其中差=(1+3)–2 = 4–2 = 2。
> 因此，拆分方式的计数为 1。

**天真方法:**解决给定问题的简单方法是[生成所有可能的子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，并将每个子集的总和存储在一个数组中，比如**子集[]** 。然后，[检查数组**子集【】**中是否存在差异为 **K**](https://www.geeksforgeeks.org/count-pairs-difference-equal-k/) 的对。检查所有配对后，打印这些配对的总数作为结果。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*

**高效方法:**上述方法可以使用以下观察值进行优化。

让第一和第二子集的和分别为 **S1** 和 **S2** ，数组元素的和[为](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)T6【Y】T7。

> 现在，两个子集的总和必须等于数组元素的总和。
> 因此，S1 + S2 = Y — (1)
> 要满足给定条件，它们的差必须等于 **K** 。
> 因此，S1-S2 = K—(2)
> 加(1) & (2)，得到的方程为
> S1 = (K + Y)/2 — (3)

因此，对于具有和 **S1** 和 **S2** 的一对子集，等式(3)必须成立，即子集的元素和必须等于 **(K + Y)/2** 。现在，问题简化为用给定的和计算子集的数量。这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决，其递推关系如下:

> DP[I][c]= DP[I+1][c-arr[I]]+DP[I+1][c]

这里， **dp[i][C]** 存储子阵列**arr[I…N–1]**的子集数量，使得它们的和等于 **C** 。
因此，递归非常简单，因为只有两个选择，即要么考虑子集中的 **i <sup>th</sup>** 数组元素，要么不考虑。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define maxN 20
#define maxSum 50
#define minSum 50
#define base 50

// To store the states of DP
int dp[maxN][maxSum + minSum];
bool v[maxN][maxSum + minSum];

// Function to find count of subsets
// with a given sum
int findCnt(int* arr, int i,
            int required_sum,
            int n)
{
    // Base case
    if (i == n) {
        if (required_sum == 0)
            return 1;
        else
            return 0;
    }

    // If an already computed
    // subproblem occurs
    if (v[i][required_sum + base])
        return dp[i][required_sum + base];

    // Set the state as solved
    v[i][required_sum + base] = 1;

    // Recurrence relation
    dp[i][required_sum + base]
        = findCnt(arr, i + 1,
                  required_sum, n)
          + findCnt(arr, i + 1,
                    required_sum - arr[i], n);
    return dp[i][required_sum + base];
}

// Function to count ways to split array into
// pair of subsets with difference K
void countSubsets(int* arr, int K,
                  int n)
{

    // Store the total sum of
    // element of the array
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Calculate sum of array elements
        sum += arr[i];
    }

    // Store the required sum
    int S1 = (sum + K) / 2;

    // Print the number of subsets
    // with sum equal to S1
    cout << findCnt(arr, 0, S1, n);
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 3 };
    int N = sizeof(arr) / sizeof(int);
    int K = 1;

    // Function Call
    countSubsets(arr, K, N);

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
  static int maxN = 20;
  static int maxSum = 50;
  static int minSum = 50;
  static int Base = 50;

  // To store the states of DP
  static int[][] dp = new int[maxN][maxSum + minSum];
  static boolean[][] v = new boolean[maxN][maxSum + minSum];

  // Function to find count of subsets
  // with a given sum
  static int findCnt(int[] arr, int i,
                     int required_sum,
                     int n)
  {
    // Base case
    if (i == n) {
      if (required_sum == 0)
        return 1;
      else
        return 0;
    }

    // If an already computed
    // subproblem occurs
    if (v[i][required_sum + Base])
      return dp[i][required_sum + Base];

    // Set the state as solved
    v[i][required_sum + Base] = true;

    // Recurrence relation
    dp[i][required_sum + Base]
      = findCnt(arr, i + 1,
                required_sum, n)
      + findCnt(arr, i + 1,
                required_sum - arr[i], n);
    return dp[i][required_sum + Base];
  }  

  // Function to count ways to split array into
  // pair of subsets with difference K
  static void countSubsets(int[] arr, int K,
                           int n)
  {
    // Store the total sum of
    // element of the array
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Calculate sum of array elements
      sum += arr[i];
    }

    // Store the required sum
    int S1 = (sum + K) / 2;

    // Print the number of subsets
    // with sum equal to S1
    System.out.print(findCnt(arr, 0, S1, n));
  } 

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 1, 1, 2, 3 };
    int N = arr.length;
    int K = 1;

    // Function Call
    countSubsets(arr, K, N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach
maxN = 20;
maxSum = 50;
minSum = 50;
Base = 50;

# To store the states of DP
dp = [[0 for i in range(maxSum + minSum)] for j in range(maxN)];
v = [[False for i in range(maxSum + minSum)] for j in range(maxN)];

# Function to find count of subsets
# with a given sum
def findCnt(arr, i, required_sum, n):

    # Base case
    if (i == n):
        if (required_sum == 0):
            return 1;
        else:
            return 0;

    # If an already computed
    # subproblem occurs
    if (v[i][required_sum + Base]):
        return dp[i][required_sum + Base];

    # Set the state as solved
    v[i][required_sum + Base] = True;

    # Recurrence relation
    dp[i][required_sum + Base] = findCnt(arr, i + 1, required_sum, n)\
    + findCnt(arr, i + 1, required_sum - arr[i], n);
    return dp[i][required_sum + Base];

# Function to count ways to split array into
# pair of subsets with difference K
def countSubsets(arr, K, n):

    # Store the total sum of
    # element of the array
    sum = 0;

    # Traverse the array
    for i in range(n):

        # Calculate sum of array elements
        sum += arr[i];

    # Store the required sum
    S1 = (sum + K) // 2;

    # Print the number of subsets
    # with sum equal to S1
    print(findCnt(arr, 0, S1, n));

# Driver Code
if __name__ == '__main__':
    arr = [1, 1, 2, 3];
    N = len(arr);
    K = 1;

    # Function Call
    countSubsets(arr, K, N);

    # This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static int maxN = 20;
    static int maxSum = 50;
    static int minSum = 50;
    static int Base = 50;

    // To store the states of DP
    static int[,] dp = new int[maxN, maxSum + minSum];
    static bool[,] v = new bool[maxN, maxSum + minSum];

    // Function to find count of subsets
    // with a given sum
    static int findCnt(int[] arr, int i,
                int required_sum,
                int n)
    {
        // Base case
        if (i == n) {
            if (required_sum == 0)
                return 1;
            else
                return 0;
        }

        // If an already computed
        // subproblem occurs
        if (v[i, required_sum + Base])
            return dp[i, required_sum + Base];

        // Set the state as solved
        v[i,required_sum + Base] = true;

        // Recurrence relation
        dp[i,required_sum + Base]
            = findCnt(arr, i + 1,
                      required_sum, n)
              + findCnt(arr, i + 1,
                        required_sum - arr[i], n);
        return dp[i,required_sum + Base];
    }

    // Function to count ways to split array into
    // pair of subsets with difference K
    static void countSubsets(int[] arr, int K,
                      int n)
    {

        // Store the total sum of
        // element of the array
        int sum = 0;

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // Calculate sum of array elements
            sum += arr[i];
        }

        // Store the required sum
        int S1 = (sum + K) / 2;

        // Print the number of subsets
        // with sum equal to S1
        Console.Write(findCnt(arr, 0, S1, n));
    }  

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 1, 2, 3 };
    int N = arr.Length;
    int K = 1;

    // Function Call
    countSubsets(arr, K, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var maxN = 20;
var maxSum = 50;
var minSum = 50;
var base = 50;

// To store the states of DP
var dp = Array.from(Array(maxN),()=> Array(maxSum+minSum));
var v = Array.from(Array(maxN), ()=> Array(maxSum+minSum));

// Function to find count of subsets
// with a given sum
function findCnt(arr, i, required_sum, n)
{
    // Base case
    if (i == n) {
        if (required_sum == 0)
            return 1;
        else
            return 0;
    }

    // If an already computed
    // subproblem occurs
    if (v[i][required_sum + base])
        return dp[i][required_sum + base];

    // Set the state as solved
    v[i][required_sum + base] = 1;

    // Recurrence relation
    dp[i][required_sum + base]
        = findCnt(arr, i + 1,
                required_sum, n)
        + findCnt(arr, i + 1,
                    required_sum - arr[i], n);
    return dp[i][required_sum + base];
}

// Function to count ways to split array into
// pair of subsets with difference K
function countSubsets(arr, K, n)
{

    // Store the total sum of
    // element of the array
    var sum = 0;

    // Traverse the array
    for (var i = 0; i < n; i++) {

        // Calculate sum of array elements
        sum += arr[i];
    }

    // Store the required sum
    var S1 = (sum + K) / 2;

    // Print the number of subsets
    // with sum equal to S1
    document.write( findCnt(arr, 0, S1, n));
}

// Driver Code
var arr = [ 1, 1, 2, 3 ];
var N = arr.length;
var K = 1;
// Function Call
countSubsets(arr, K, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(N*K)*