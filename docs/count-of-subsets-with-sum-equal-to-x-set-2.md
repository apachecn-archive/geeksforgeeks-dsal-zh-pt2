# 和等于 X 的子集计数|集合-2

> 原文:[https://www . geesforgeks . org/sum 等于 x-set-2 的子集计数/](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x-set-2/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **X** ，任务是找出和等于 **X** 的子集数量。

**示例:**

> **输入:** arr[] = {1，2，3，3}，X = 6
> **输出:** 3
> **解释:**所有可能的子集为{1，2，3}、{1，2，3}和{3，3}。
> 
> **输入:** arr[] = {1，1，1，1}，X = 1
> T3】输出: 4

**空间高效方法:**这个问题已经在文章[这里](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)讨论过了。本文关注的是类似的[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)方法，它只使用 **O(X)** 空间。上面文章中讨论的解决这个问题的标准 DP 关系是:

> DP[I][c]= DP[I–1][c–arr[I]]+DP[I–1][c]

其中 **dp[i][C]** 存储[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) **arr[0… i]** 的子集数量，使得它们的总和等于 **C** 。可以注意到， **dp[i] <sup>第</sup>** 状态只需要**DP[I–1]<sup>第</sup>** 状态的数组值。因此，上述关系可以简化为以下内容:

> DP[c]= DP[c–arr[I]+DP[c]

这里需要注意的一点是，在计算**DP【C】**的过程中，变量 **C** 必须以递减的顺序迭代，以避免子集和计数中**arr【I】**的重复。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of subsets
// having the given sum
int subsetSum(int arr[], int n, int sum)
{
    // Initializing the dp-table
    int dp[sum + 1] = {};

    // Case for sum of elements in empty set
    dp[0] = 1;

    // Loop to iterate over array elements
    for (int i = 0; i < n; i++) {
        for (int j = sum; j >= 0; j--) {

            // If j-arr[i] is a valid index
            if (j - arr[i] >= 0) {
                dp[j] = dp[j - arr[i]] + dp[j];
            }
        }
    }

    // Return answer
    return dp[sum];
}

// Driven Code
int main()
{
    int arr[] = { 1, 1, 1, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int sum = 1;

    cout << subsetSum(arr, N, sum) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
public class GFG
{

// Function to find the count of subsets
// having the given sum
static int subsetSum(int arr[], int n, int sum)
{
    // Initializing the dp-table
    int dp[] = new int[sum + 1];

    // Case for sum of elements in empty set
    dp[0] = 1;

    // Loop to iterate over array elements
    for (int i = 0; i < n; i++) {
        for (int j = sum; j >= 0; j--) {

            // If j-arr[i] is a valid index
            if (j - arr[i] >= 0) {
                dp[j] = dp[j - arr[i]] + dp[j];
            }
        }
    }

    // Return answer
    return dp[sum];
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 1, 1, 1 };
    int N = arr.length;
    int sum = 1;

    System.out.println(subsetSum(arr, N, sum));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to find the count of subsets
# having the given sum
def subsetSum(arr, n, sum):

    # Initializing the dp-table
    dp = [0] * (sum + 1)

    # Case for sum of elements in empty set
    dp[0] = 1;

    # Loop to iterate over array elements
    for i in range(n):
        for j in range(sum, 0, -1):

            # If j-arr[i] is a valid index
            if (j - arr[i] >= 0):
                dp[j] = dp[j - arr[i]] + dp[j];
    # Return answer
    return dp[sum];

# Driven Code
arr = [1, 1, 1, 1];
N = len(arr)
sum = 1;

print(subsetSum(arr, N, sum))

# This code is contributed by gfgking.
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG
{

// Function to find the count of subsets
// having the given sum
static int subsetSum(int []arr, int n, int sum)
{

    // Initializing the dp-table
    int []dp = new int[sum + 1];

    // Case for sum of elements in empty set
    dp[0] = 1;

    // Loop to iterate over array elements
    for (int i = 0; i < n; i++) {
        for (int j = sum; j >= 0; j--) {

            // If j-arr[i] is a valid index
            if (j - arr[i] >= 0) {
                dp[j] = dp[j - arr[i]] + dp[j];
            }
        }
    }

    // Return answer
    return dp[sum];
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1, 1, 1 };
    int N = arr.Length;
    int sum = 1;

    Console.WriteLine(subsetSum(arr, N, sum));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to find the count of subsets
// having the given sum
function subsetSum(arr, n, sum)
{

    // Initializing the dp-table
    let dp = new Array(sum + 1).fill(0)

    // Case for sum of elements in empty set
    dp[0] = 1;

    // Loop to iterate over array elements
    for (let i = 0; i < n; i++) {
        for (let j = sum; j >= 0; j--) {

            // If j-arr[i] is a valid index
            if (j - arr[i] >= 0) {
                dp[j] = dp[j - arr[i]] + dp[j];
            }
        }
    }

    // Return answer
    return dp[sum];
}

// Driven Code
let arr = [1, 1, 1, 1];
let N = arr.length;
let sum = 1;

document.write(subsetSum(arr, N, sum))

// This code is contributed by gfgking.
</script>
```

**Output**

```
4
```

***时间复杂度:** O(N * X)*
***辅助空间:** O(X)*