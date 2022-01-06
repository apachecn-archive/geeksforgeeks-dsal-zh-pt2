# 双背包|动态编程

> 原文:[https://www . geesforgeks . org/双背包-动态编程/](https://www.geeksforgeeks.org/double-knapsack-dynamic-programming/)

给定一个包含“N”个不同项目重量的数组“arr”，以及两个可以承受“W1”和“W2”重量的背包，任务是找到数组“arr”的最大子集的和，该子集可以放入两个背包中。不允许将任何物品一分为二，即一件物品应作为一个整体放入其中一个袋子中。
**例:**

> **输入:** arr[] = {8，3，2}
> W1 = 10，W2 = 3
> **输出:** 13
> 第一个和第三个物体进入第一个背包。第二个物体放在第二个背包里。因此，总重量变为 13。
> **输入:** arr[] = {8，5，3}
> W1 = 10，W2 = 3
> **输出:** 11

**解决方案:**
递归解决方案是尝试所有可能的填充两个背包的方法，并选择重量最大的一个。
为了优化上述想法，我们需要确定 DP 的状态，我们将在此基础上构建我们的解决方案。稍加观察，我们可以确定这可以用三种状态 **(i，w1_r，w2_r)** 来表示。这里的‘I’表示我们试图存储的元素的索引，w1_r 表示第一个背包的剩余空间，w2_r 表示第二个背包的剩余空间。因此，该问题可以使用具有递归关系的三维动态规划
来解决

```
DP[i][w1_r][w2_r] = max( DP[i + 1][w1_r][w2_r],
                    arr[i] + DP[i + 1][w1_r - arr[i]][w2_r],
                    arr[i] + DP[i + 1][w1_r][w2_r - arr[i]])
```

以上递推关系解释如下:

> 对于每个“我”，我们可以选择:
> 
> 1.  不要选择项目“I”。
> 2.  在第一个背包中填入“I”项。
> 3.  在第二个背包中填入“I”项。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define maxN 31
#define maxW 31
using namespace std;

// 3D array to store
// states of DP
int dp[maxN][maxW][maxW];

// w1_r represents remaining capacity of 1st knapsack
// w2_r represents remaining capacity of 2nd knapsack
// i represents index of the array arr we are working on
int maxWeight(int* arr, int n, int w1_r, int w2_r, int i)
{
    // Base case
    if (i == n)
        return 0;
    if (dp[i][w1_r][w2_r] != -1)
        return dp[i][w1_r][w2_r];

    // Variables to store the result of three
    // parts of recurrence relation
    int fill_w1 = 0, fill_w2 = 0, fill_none = 0;

    if (w1_r >= arr[i])
        fill_w1 = arr[i] +
         maxWeight(arr, n, w1_r - arr[i], w2_r, i + 1);

    if (w2_r >= arr[i])
        fill_w2 = arr[i] +
         maxWeight(arr, n, w1_r, w2_r - arr[i], i + 1);

    fill_none = maxWeight(arr, n, w1_r, w2_r, i + 1);

    // Store the state in the 3D array
    dp[i][w1_r][w2_r] = max(fill_none, max(fill_w1, fill_w2));

    return dp[i][w1_r][w2_r];
}

// Driver code
int main()
{
    // Input array
    int arr[] = { 8, 2, 3 };

    // Initializing the array with -1
    memset(dp, -1, sizeof(dp));

    // Number of elements in the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Capacity of knapsacks
    int w1 = 10, w2 = 3;

    // Function to be called
    cout << maxWeight(arr, n, w1, w2, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    static int maxN = 31;
    static int maxW = 31;

    // 3D array to store
    // states of DP
    static int dp [][][] = new int[maxN][maxW][maxW];

    // w1_r represents remaining capacity of 1st knapsack
    // w2_r represents remaining capacity of 2nd knapsack
    // i represents index of the array arr we are working on
    static int maxWeight(int arr [] , int n, int w1_r, int w2_r, int i)
    {
        // Base case
        if (i == n)
            return 0;
        if (dp[i][w1_r][w2_r] != -1)
            return dp[i][w1_r][w2_r];

        // Variables to store the result of three
        // parts of recurrence relation
        int fill_w1 = 0, fill_w2 = 0, fill_none = 0;

        if (w1_r >= arr[i])
            fill_w1 = arr[i] +
            maxWeight(arr, n, w1_r - arr[i], w2_r, i + 1);

        if (w2_r >= arr[i])
            fill_w2 = arr[i] +
            maxWeight(arr, n, w1_r, w2_r - arr[i], i + 1);

        fill_none = maxWeight(arr, n, w1_r, w2_r, i + 1);

        // Store the state in the 3D array
        dp[i][w1_r][w2_r] = Math.max(fill_none, Math.max(fill_w1, fill_w2));

        return dp[i][w1_r][w2_r];
    }

    // Driver code
    public static void main (String[] args)
    {

        // Input array
        int arr[] = { 8, 2, 3 };

        // Initializing the array with -1

        for (int i = 0; i < maxN ; i++)
            for (int j = 0; j < maxW ; j++)
                for (int k = 0; k < maxW ; k++)
                        dp[i][j][k] = -1;

        // Number of elements in the array
        int n = arr.length;

        // Capacity of knapsacks
        int w1 = 10, w2 = 3;

        // Function to be called
        System.out.println(maxWeight(arr, n, w1, w2, 0));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# w1_r represents remaining capacity of 1st knapsack
# w2_r represents remaining capacity of 2nd knapsack
# i represents index of the array arr we are working on
def maxWeight(arr, n, w1_r, w2_r, i):

    # Base case
    if i == n:
        return 0
    if dp[i][w1_r][w2_r] != -1:
        return dp[i][w1_r][w2_r]

    # Variables to store the result of three
    # parts of recurrence relation
    fill_w1, fill_w2, fill_none = 0, 0, 0

    if w1_r >= arr[i]:
        fill_w1 = arr[i] + maxWeight(arr, n, w1_r - arr[i],
                                             w2_r, i + 1)

    if w2_r >= arr[i]:
        fill_w2 = arr[i] + maxWeight(arr, n, w1_r,
                                     w2_r - arr[i], i + 1)

    fill_none = maxWeight(arr, n, w1_r, w2_r, i + 1)

    # Store the state in the 3D array
    dp[i][w1_r][w2_r] = max(fill_none, max(fill_w1,
                                           fill_w2))

    return dp[i][w1_r][w2_r]

# Driver code
if __name__ == "__main__":

    # Input array
    arr = [8, 2, 3]
    maxN, maxW = 31, 31

    # 3D array to store
    # states of DP
    dp = [[[-1] * maxW] * maxW] * maxN

    # Number of elements in the array
    n = len(arr)

    # Capacity of knapsacks
    w1, w2 = 10, 3

    # Function to be called
    print(maxWeight(arr, n, w1, w2, 0))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int maxN = 31;
    static int maxW = 31;

    // 3D array to store
    // states of DP
    static int [ , , ] dp = new int[maxN, maxW, maxW];

    // w1_r represents remaining capacity of 1st knapsack
    // w2_r represents remaining capacity of 2nd knapsack
    // i represents index of the array arr we are working on
    static int maxWeight(int [] arr, int n, int w1_r,
                                    int w2_r, int i)
    {
        // Base case
        if (i == n)
            return 0;
        if (dp[i ,w1_r, w2_r] != -1)
            return dp[i, w1_r, w2_r];

        // Variables to store the result of three
        // parts of recurrence relation
        int fill_w1 = 0, fill_w2 = 0, fill_none = 0;

        if (w1_r >= arr[i])
            fill_w1 = arr[i] +
            maxWeight(arr, n, w1_r - arr[i], w2_r, i + 1);

        if (w2_r >= arr[i])
            fill_w2 = arr[i] +
            maxWeight(arr, n, w1_r, w2_r - arr[i], i + 1);

        fill_none = maxWeight(arr, n, w1_r, w2_r, i + 1);

        // Store the state in the 3D array
        dp[i, w1_r, w2_r] = Math.Max(fill_none, Math.Max(fill_w1, fill_w2));

        return dp[i, w1_r, w2_r];
    }

    // Driver code
    public static void Main ()
    {

        // Input array
        int [] arr = { 8, 2, 3 };

        // Initializing the array with -1

        for (int i = 0; i < maxN ; i++)
            for (int j = 0; j < maxW ; j++)
                for (int k = 0; k < maxW ; k++)
                        dp[i, j, k] = -1;

        // Number of elements in the array
        int n = arr.Length;

        // Capacity of knapsacks
        int w1 = 10, w2 = 3;

        // Function to be called
        Console.WriteLine(maxWeight(arr, n, w1, w2, 0));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

var maxN = 31
var maxW = 31

// 3D array to store
// states of DP
var dp = Array(maxN);

for(var i=0;i<maxN;i++)
{
    dp[i] = Array(maxW);
    for(var j =0; j<maxW; j++)
    {
        dp[i][j] = Array(maxW).fill(-1);
    }
}

// w1_r represents remaining
// capacity of 1st knapsack
// w2_r represents remaining
// capacity of 2nd knapsack
// i represents index of the array arr
// we are working on
function maxWeight(arr, n, w1_r, w2_r, i)
{
    // Base case
    if (i == n)
        return 0;
    if (dp[i][w1_r][w2_r] != -1)
        return dp[i][w1_r][w2_r];

    // Variables to store the result of three
    // parts of recurrence relation
    var fill_w1 = 0, fill_w2 = 0, fill_none = 0;

    if (w1_r >= arr[i])
        fill_w1 = arr[i] +
         maxWeight(arr, n, w1_r - arr[i],
         w2_r, i + 1);

    if (w2_r >= arr[i])
        fill_w2 = arr[i] +
         maxWeight(arr, n, w1_r, w2_r -
         arr[i], i + 1);

    fill_none = maxWeight(arr, n, w1_r,
    w2_r, i + 1);

    // Store the state in the 3D array
    dp[i][w1_r][w2_r] = Math.max(fill_none,
    Math.max(fill_w1, fill_w2));

    return dp[i][w1_r][w2_r];
}

// Driver code
// Input array
var arr = [8, 2, 3 ];

// Number of elements in the array
var n = arr.length;

// Capacity of knapsacks
var w1 = 10, w2 = 3;

// Function to be called
document.write( maxWeight(arr, n, w1, w2, 0));

</script>
```

**Output:** 

```
13
```

**时间复杂度:**O(N * W1 * W2)
T3】辅助空间: O(N*W1*W2))