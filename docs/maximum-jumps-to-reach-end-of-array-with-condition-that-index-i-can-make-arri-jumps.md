# 到达数组末尾的最大跳转，条件是索引 I 可以进行 arr[i]跳转

> 原文:[https://www . geeksforgeeks . org/最大跳跃到达带条件的数组末尾-索引-i-can-make-arri-jumps/](https://www.geeksforgeeks.org/maximum-jumps-to-reach-end-of-array-with-condition-that-index-i-can-make-arri-jumps/)

给定整数 **N** 和大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的情况下，任务是在给定索引 **i** 可以使**arr【I】**跳跃并到达位置**I+arr【I】**的约束下，找到到达数组末尾的最大跳跃。

**示例:**

> **输入:** N = 5，arr[] = {2，3，5，7，9}
> **输出:** 12
> **解释:**
> 在索引 0 处进行 2 次跳转并移动到索引 2，然后进行 5 次跳转以到达索引 7，该索引不在数组中，因此跳转总数为(2+5)=7。
> 在索引 1 处进行 3+9= 12 次跳跃
> 在索引 2 处进行 5 次跳跃
> 在索引 3 处进行 7 次跳跃
> 在索引 4 处进行 9 次跳跃
> 
> **输入:arr[]** ={2，2，1，2，3，3}
> 输出: 8

**做法:**思路是用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 来解决这个问题。按照以下步骤解决问题。

*   将大小为 **N** 的数组 **dp** 初始化为 0。 **dp[i]** 存储从索引 **i** 到达数组末尾所需的跳转次数。另外，将整数**和**初始化为 0。
*   [从数组末尾遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)使用 for 循环
    *   将 **arr[i]** 分配给 **dp[i]** ，因为 **arr[i]** 是从该索引的最小跳跃次数。
    *   现在初始化一个变量，比如说 **j** 并赋值 **j = i+arr[i]。**
    *   如果 **j** 的值小于 **N** ，则在**DP【I】**上加上**DP【j】**。
    *   将 **ans** 的值更新为[最大](https://www.geeksforgeeks.org/max-min-python/) ( **ans** 、**DP【I】**)
*   完成上述步骤后，打印 **ans 的值。**

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// jumps to reach end of array
void findMaxJumps(int arr[], int N)
{
    // Stores the jumps needed
    // to reach end from each index
    int dp[N] = { 0 };
    int ans = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--) {
        dp[i] = arr[i];
        int j = i + arr[i];

        // Check if j is less
        // than N
        if (j < N) {

            // Add dp[j] to the
            // value of dp[i]
            dp[i] = dp[i] + dp[j];
        }

        // Update the value
        // of ans
        ans = max(ans, dp[i]);
    }

    // Print the value of ans
    cout << ans;
}

// Driver Code
int main()
{

    int arr[] = { 2, 3, 5, 7, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findMaxJumps(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach

import java.io.*;

class GFG {

// Function to find the maximum
// jumps to reach end of array
static void findMaxJumps(int arr[], int N)
{
    // Stores the jumps needed
    // to reach end from each index
    int dp[] = new int [N];
    int ans = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--) {
        dp[i] = arr[i];
        int j = i + arr[i];

        // Check if j is less
        // than N
        if (j < N) {

            // Add dp[j] to the
            // value of dp[i]
            dp[i] = dp[i] + dp[j];
        }

        // Update the value
        // of ans
        ans = Math.max(ans, dp[i]);
    }

    // Print the value of ans
    System.out.println(ans);
}

// Driver Code
public static void main (String[] args) {
    int arr[] = { 2, 3, 5, 7, 9 };
    int N = arr.length;

    findMaxJumps(arr, N);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python 3 code for the above approach

# Function to find the maximum
# jumps to reach end of array
def findMaxJumps(arr, N):

    # Stores the jumps needed
    # to reach end from each index
    dp = [0 for i in range(N)]
    ans = 0

    # Traverse the array
    i = N - 1
    while(i >= 0):
        dp[i] = arr[i]
        j = i + arr[i]

        # Check if j is less
        # than N
        if (j < N):

            # Add dp[j] to the
            # value of dp[i]
            dp[i] = dp[i] + dp[j]

        # Update the value
        # of ans
        ans = max(ans, dp[i])
        i -= 1

    # Print the value of ans
    print(ans)

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 5, 7, 9]
    N =  len(arr)

    findMaxJumps(arr, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# code for the above approach

using System;

class GFG {

    // Function to find the maximum
    // jumps to reach end of array
    static void findMaxJumps(int[] arr, int N)
    {
        // Stores the jumps needed
        // to reach end from each index
        int[] dp = new int[N];
        int ans = 0;

        // Traverse the array
        for (int i = N - 1; i >= 0; i--) {
            dp[i] = arr[i];
            int j = i + arr[i];

            // Check if j is less
            // than N
            if (j < N) {

                // Add dp[j] to the
                // value of dp[i]
                dp[i] = dp[i] + dp[j];
            }

            // Update the value
            // of ans
            ans = Math.Max(ans, dp[i]);
        }

        // Print the value of ans
        Console.Write(ans);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 2, 3, 5, 7, 9 };
        int N = arr.Length;

        findMaxJumps(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to find the maximum
// jumps to reach end of array
function findMaxJumps(arr, N)
{

    // Stores the jumps needed
    // to reach end from each index
    let dp = new Array(N).fill(0);
    let ans = 0;

    // Traverse the array
    for (let i = N - 1; i >= 0; i--) {
        dp[i] = arr[i];
        let j = i + arr[i];

        // Check if j is less
        // than N
        if (j < N) {

            // Add dp[j] to the
            // value of dp[i]
            dp[i] = dp[i] + dp[j];
        }

        // Update the value
        // of ans
        ans = Math.max(ans, dp[i]);
    }

    // Print the value of ans
    document.write(ans);
}

// Driver Code
let arr = [2, 3, 5, 7, 9];
let N = arr.length;

findMaxJumps(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
12
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)