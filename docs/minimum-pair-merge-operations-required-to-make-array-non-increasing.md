# 使数组不增加所需的最小对合并操作

> 原文:[https://www . geesforgeks . org/minimum-pair-merge-operations-required-make-array-non-递增/](https://www.geeksforgeeks.org/minimum-pair-merge-operations-required-to-make-array-non-increasing/)

给定一个数组**A【】**，任务是找到从数组中移除两个相邻元素并用它们的和替换所需的最小操作数，从而将数组转换为非递增数组。

**注:**单个元素的数组被认为是非递增的。

**示例:**

> **输入:** A[] = {1，5，3，9，1}
> **输出:** 2
> **解释:**
> 将{1，5}替换为{6}将数组修改为{6，3，9，1}
> 将{6，3}替换为{9}将数组修改为{9，9，1}
> **输入:** A[] = {0，1，2}
> **输出:**

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。一个[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)表用于存储使给定阵列的子阵列从右向左不增加所需的最小操作数。按照以下步骤解决问题:

*   初始化一个数组 **dp[]** ，其中 **dp[i]** 存储使子数组{A[i]，…，A[N]}不增加所需的最小操作数。因此，目标是计算 dp[0]。
*   找到一个最小子阵列..A[j]} 使得**和({A[i] … A[j]}) > val[j+1]** ，其中，val[j+1]是为子阵列 **{A[j + 1]，… A[N]}** 获得的合并和。
*   将 **dp[i]** 更新为**j–I+DP[j+1]**，将**val[I]**更新为**sum({ A[I]…A[j])**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
// to make the array Non-increasing
int solve(vector<int>& a)
{

    // Size of the array
    int n = a.size();

    // Dp table initialization
    vector<int> dp(n + 1, 0), val(n + 1, 0);

    // dp[i]: Stores minimum number of
    // operations required to make
    // subarray {A[i], ..., A[N]} non-increasing
    for (int i = n - 1; i >= 0; i--) {
        long long sum = a[i];
        int j = i;

        while (j + 1 < n and sum < val[j + 1]) {

            // Increment the value of j
            j++;

            // Add current value to sum
            sum += a[j];
        }

        // Update the dp tables
        dp[i] = (j - i) + dp[j + 1];
        val[i] = sum;
    }

    // Return the answer
    return dp[0];
}

// Driver code
int main()
{
    vector<int> arr = { 1, 5, 3, 9, 1 };
    cout << solve(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the minimum operations
// to make the array Non-increasing
static int solve(int []a)
{

    // Size of the array
    int n = a.length;

    // Dp table initialization
    int []dp = new int[n + 1];
    int []val = new int[n + 1];

    // dp[i]: Stores minimum number of
    // operations required to make
    // subarray {A[i], ..., A[N]} non-increasing
    for (int i = n - 1; i >= 0; i--)
    {
        int sum = a[i];
        int j = i;

        while (j + 1 < n && sum < val[j + 1])
        {

            // Increment the value of j
            j++;

            // Add current value to sum
            sum += a[j];
        }

        // Update the dp tables
        dp[i] = (j - i) + dp[j + 1];
        val[i] = sum;
    }

    // Return the answer
    return dp[0];
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 1, 5, 3, 9, 1 };
    System.out.print(solve(arr));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum operations
# to make the array Non-increasing
def solve(a):

    # Size of the array
    n = len(a)

    # Dp table initialization
    dp = [0] * (n + 1)
    val = [0] * (n + 1)

    # dp[i]: Stores minimum number of
    # operations required to make
    # subarray {A[i], ..., A[N]} non-increasing
    for i in range(n - 1, -1, -1):
        sum = a[i]
        j = i

        while(j + 1 < n and sum < val[j + 1]):

            # Increment the value of j
            j += 1

            # Add current value to sum
            sum += a[j]

        # Update the dp tables
        dp[i] = (j - i) + dp[j + 1]
        val[i] = sum

    # Return the answer
    return dp[0]

# Driver Code
arr = [ 1, 5, 3, 9, 1 ]

# Function call
print(solve(arr))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the minimum operations
// to make the array Non-increasing
static int solve(int []a)
{

    // Size of the array
    int n = a.Length;

    // Dp table initialization
    int []dp = new int[n + 1];
    int []val = new int[n + 1];

    // dp[i]: Stores minimum number of
    // operations required to make
    // subarray {A[i], ..., A[N]} non-increasing
    for (int i = n - 1; i >= 0; i--)
    {
        int sum = a[i];
        int j = i;

        while (j + 1 < n && sum < val[j + 1])
        {

            // Increment the value of j
            j++;

            // Add current value to sum
            sum += a[j];
        }

        // Update the dp tables
        dp[i] = (j - i) + dp[j + 1];
        val[i] = sum;
    }

    // Return the answer
    return dp[0];
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 5, 3, 9, 1 };
    Console.Write(solve(arr));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the minimum operations
// to make the array Non-increasing
function solve(a)
{

    // Size of the array
    let n = a.length;

    // Dp table initialization
    let dp = new Array(n+1).fill(0);
    let val = new Array(n+1).fill(0);

    // dp[i]: Stores minimum number of
    // operations required to make
    // subarray {A[i], ..., A[N]} non-increasing
    for (let i = n - 1; i >= 0; i--)
    {
        let sum = a[i];
        let j = i;

        while (j + 1 < n && sum < val[j + 1])
        {

            // Increment the value of j
            j++;

            // Add current value to sum
            sum += a[j];
        }

        // Update the dp tables
        dp[i] = (j - i) + dp[j + 1];
        val[i] = sum;
    }

    // Return the answer
    return dp[0];
}

// Driver Code

    let arr = [ 1, 5, 3, 9, 1 ];
    document.write(solve(arr));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*