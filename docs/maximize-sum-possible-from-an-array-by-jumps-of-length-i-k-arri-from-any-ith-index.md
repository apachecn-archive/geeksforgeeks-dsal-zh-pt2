# 通过从任意第一个索引

跳转长度 i + K * arr[i]，最大化数组中可能的和

> 原文:[https://www . geesforgeks . org/最大化长度为 I-k-arri-from-any-with-index/](https://www.geeksforgeeks.org/maximize-sum-possible-from-an-array-by-jumps-of-length-i-k-arri-from-any-ith-index/)

给定一个由 **N** 正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过从数组的任意 **i <sup>th</sup>** 跳转 ( *< N* )长度来找到数组元素的最大可能和。

**示例:**

> **输入:** arr[] = {1，2，1，4}，K = 2
> **输出:** 4
> **解释:**
> 起始索引 i = 0，数组的索引遍历为{0，2}
> 因此，答案为 4。
> 
> **输入:** arr[] = {2，1，3，1，2}，K = 3
> T3】输出: 3

**天真方法:**最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)在范围**【0，N–1】**内的每个可能的起始索引，并从每个可能的索引 **i** 中找到通过取 **(i + K*arr[i])** 的跳转所获得的所有和的最大值。在所有遍历之后，打印得到的最大和。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。其思想是使用辅助数组 **dp[]** ，使得 **dp[i]** 存储通过使用以下递归关系选择 **i** 作为起始索引而获得的和:

> dp[i] = dp[i + K*arr[i]] + 疤痕[i]

按照以下步骤解决问题:

*   用{ **0** }初始化一个大小为 **N** 的辅助数组 **dp[]** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N–1，0】**，并执行以下步骤:
    *   如果**(I+K * arr[I]≥N)**的值，则将 **dp[i]** 的值更新为 **arr[i]** 。
    *   否则，将 **dp[i]** 的值更新为 **dp[i + K*arr[i]] + arr[i]** 。
*   完成上述步骤后，打印数组 **dp[]** 中的[最大值作为最终的最大和。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// possible by jumps of length
// i + K*arr[i] from any i-th index
void maxSum(int arr[], int N, int K)
{
    // Initialize an array dp[]
    int dp[N + 2] = { 0 };

    // Stores the maximum sum
    int maxval = 0;

    // Iterate over the range [N-1, 0]
    for (int i = N - 1; i >= 0; i--) {

        // If length of the jump exceeds N
        if ((i + K * arr[i]) >= N) {

            // Set dp[i] as arr[i]
            dp[i] = arr[i];
        }

        // Otherwise, update dp[i] as
        // sum of dp[i + K * arr[i]] and arr[i]
        else {
            dp[i] = dp[i + K * arr[i]] + arr[i];
        }

        // Update the overall maximum sum
        maxval = max(maxval, dp[i]);
    }

    // Print the answer
    cout << maxval;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 3, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    maxSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the maximum sum
// possible by jumps of length
// i + K*arr[i] from any i-th index
static void maxSum(int arr[], int N, int K)
{

    // Initialize an array dp[]
    int[] dp = new int[N + 2];
    Arrays.fill(dp, 0);

    // Stores the maximum sum
    int maxval = 0;

    // Iterate over the range [N-1, 0]
    for (int i = N - 1; i >= 0; i--)
    {

        // If length of the jump exceeds N
        if ((i + K * arr[i]) >= N)
        {

            // Set dp[i] as arr[i]
            dp[i] = arr[i];
        }

        // Otherwise, update dp[i] as
        // sum of dp[i + K * arr[i]] and arr[i]
        else {
            dp[i] = dp[i + K * arr[i]] + arr[i];
        }

        // Update the overall maximum sum
        maxval = Math.max(maxval, dp[i]);
    }

    // Print the answer
    System.out.print(maxval);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 3, 1, 2 };
    int N = arr.length;
    int K = 3;
    maxSum(arr, N, K);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum sum
# possible by jumps of length
# i + K*arr[i] from any i-th index
def maxSum(arr, N, K):
    # Initialize an array dp[]
    dp = [0 for i in range(N+2)]

    # Stores the maximum sum
    maxval = 0

    # Iterate over the range [N-1, 0]
    i = N - 1
    while(i >= 0):
        # If length of the jump exceeds N
        if ((i + K * arr[i]) >= N):
            # Set dp[i] as arr[i]
            dp[i] = arr[i]

        # Otherwise, update dp[i] as
        # sum of dp[i + K * arr[i]] and arr[i]
        else:
            dp[i] = dp[i + K * arr[i]] + arr[i]

        # Update the overall maximum sum
        maxval = max(maxval, dp[i])
        i -= 1

    # Print the answer
    print(maxval)

# Driver Code
if __name__ == '__main__':
    arr =  [2, 1, 3, 1, 2]
    N = len(arr)
    K = 3
    maxSum(arr, N, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the maximum sum
// possible by jumps of length
// i + K*arr[i] from any i-th index
static void maxSum(int[] arr, int N, int K)
{

    // Initialize an array dp[]
    int[] dp = new int[N + 2];
    for(int i = 0; i< N+2; i++)
    {
        dp[i] = 0;
    }

    // Stores the maximum sum
    int maxval = 0;

    // Iterate over the range [N-1, 0]
    for (int i = N - 1; i >= 0; i--)
    {

        // If length of the jump exceeds N
        if ((i + K * arr[i]) >= N)
        {

            // Set dp[i] as arr[i]
            dp[i] = arr[i];
        }

        // Otherwise, update dp[i] as
        // sum of dp[i + K * arr[i]] and arr[i]
        else {
            dp[i] = dp[i + K * arr[i]] + arr[i];
        }

        // Update the overall maximum sum
        maxval = Math.Max(maxval, dp[i]);
    }

    // Print the answer
    Console.WriteLine(maxval);
}

// Driver Code
static public void Main()
{
    int[] arr = { 2, 1, 3, 1, 2 };
    int N = arr.Length;
    int K = 3;
    maxSum(arr, N, K);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum sum
// possible by jumps of length
// i + K*arr[i] from any i-th index
function maxSum(arr, N, K)
{

    // Initialize an array dp[]
    let dp = [];
    for(let i = 0; i < N + 2; i++)
    {
        dp[i] = 0;
    }

    // Stores the maximum sum
    let maxval = 0;

    // Iterate over the range [N-1, 0]
    for (let i = N - 1; i >= 0; i--)
    {

        // If length of the jump exceeds N
        if ((i + K * arr[i]) >= N)
        {

            // Set dp[i] as arr[i]
            dp[i] = arr[i];
        }

        // Otherwise, update dp[i] as
        // sum of dp[i + K * arr[i]] and arr[i]
        else {
            dp[i] = dp[i + K * arr[i]] + arr[i];
        }

        // Update the overall maximum sum
        maxval = Math.max(maxval, dp[i]);
    }

    // Print the answer
    document.write(maxval);
}

// Driver Code

    let arr = [ 2, 1, 3, 1, 2 ];
    let N = arr.length;
    let K = 3;
    maxSum(arr, N, K);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)