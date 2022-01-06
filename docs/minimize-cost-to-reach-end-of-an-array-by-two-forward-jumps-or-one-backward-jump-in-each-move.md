# 通过每次移动中的两次向前跳跃或一次向后跳跃来最小化到达阵列末端的成本

> 原文:[https://www . geeksforgeeks . org/通过每次移动中向前跳两次或向后跳一次来最小化到达阵列末端的成本/](https://www.geeksforgeeks.org/minimize-cost-to-reach-end-of-an-array-by-two-forward-jumps-or-one-backward-jump-in-each-move/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从 **i** <sup>th</sup> 索引开始，只需移动到索引 **(i + 2)** 和**(I–1)**即可找到穿过数组或[到达数组末尾](https://www.geeksforgeeks.org/check-if-the-end-of-the-array-can-be-reached-from-a-given-position/)所需的最小成本。

**示例:**

> **输入:** arr[] = {5，1，2，10，100}
> **输出:** 18
> **解释:**
> 最优成本路径(基于 0 的索引):0 → 2 → 1 → 3 → 5
> 因此，最小成本= 5 + 2 + 1 + 10 = 18。
> 
> **输入:** arr[] = {9，4，6，8，5}
> **输出:** 20
> **解释:**
> 最优成本路径(基于 0 的索引):0 → 2 → 4
> 因此，最小成本= 9 + 6 + 5 = 20

**天真方法:**给定的问题可以基于以下观察来解决:

*   由于所有成本都是正的，向后移动一步以上永远不是最佳选择，因此要到达数组的特定索引 **i** ，要么直接从**(I–2)<sup>th</sup>**索引跳转，要么从**(I–1)<sup>th</sup>**跳转到 **(i + 1) <sup>th</sup> 索引，即**(向前跳转 2 次)，然后向后跳转 1 次，即
*   现在，从数组的末尾递归遍历，对于索引**(I–2)**和**(I–1)**处的元素，计算两者的最小开销。因此，可以使用以下递归关系来计算穿过阵列的最小成本:

> **mincost(index)= minimum(min cost(index–2)+arr[I]，mincost(index–1)+arr[I]+arr[I+1])【t1]**

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法既有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)又有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。因此可以使用[记忆或列表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)进行优化。按照以下步骤解决问题:

*   初始化一个数组 **dp[]** ，其中 **dp[i]** 存储达到 **i <sup>th</sup>** 指标的最小成本。
*   将 **dp[0] = arr[0]** 初始化为达到 **0 <sup>第</sup>指数**的成本，等于 **0 <sup>第</sup>指数**本身的值。更新**DP[1]= arr[0]+arr[1]+arr[2]**，达到 **1 <sup>st</sup> 索引**，从**0<sup>th</sup>T19】索引跳转到 **2 <sup>nd</sup> 索引**索引到 **1 <sup>st</sup> 索引**。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)**【2，N–2】**，并将 **dp[i]** 更新为**(DP[I–2]+arr[I])**和**(DP[I–1]+arr[I]+arr[I+1])**的最小值。
*   对于最后一个索引**(N–1)**，更新**DP【N–1】**为最小的**(DP【N–3】+arr【N–1】)**和**(DP【N–2】)**。
*   完成上述步骤后，打印**DP【N–1】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to reach the end of an array
void minCost(int arr[], int n)
{
    // Base Case: When N < 3
    if (n < 3) {
        cout << arr[0];
        return;
    }

    // Store the results in table
    int* dp = new int[n];

    // Initialize base cases
    dp[0] = arr[0];
    dp[1] = dp[0] + arr[1] + arr[2];

    // Iterate over the range[2, N - 2]
    // to construct the dp array
    for (int i = 2; i < n - 1; i++)
        dp[i] = min(dp[i - 2] + arr[i],
                    dp[i - 1] + arr[i]
                        + arr[i + 1]);

    // Handle case for the last index, i.e. N - 1
    dp[n - 1] = min(dp[n - 2],
                    dp[n - 3] + arr[n - 1]);

    // Print the answer
    cout << dp[n - 1];
}

// Driver Code
int main()
{
    int arr[] = { 9, 4, 6, 8, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    minCost(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function to find the minimum cost
    // to reach the end of an array
    static void minCost(int arr[], int n)
    {

        // Base Case: When N < 3
        if (n < 3) {
            System.out.println(arr[0]);
            return;
        }

        // Store the results in table
        int dp[] = new int[n];

        // Initialize base cases
        dp[0] = arr[0];
        dp[1] = dp[0] + arr[1] + arr[2];

        // Iterate over the range[2, N - 2]
        // to construct the dp array
        for (int i = 2; i < n - 1; i++)
            dp[i] = Math.min(dp[i - 2] + arr[i],
                           dp[i - 1] + arr[i] + arr[i + 1]);

        // Handle case for the last index, i.e. N - 1
        dp[n - 1] = Math.min(dp[n - 2], dp[n - 3] + arr[n - 1]);

        // Print the answer
        System.out.println(dp[n - 1]);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 9, 4, 6, 8, 5 };
        int N = arr.length;
        minCost(arr, N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum cost
# to reach the end of an array
def minCost(arr, n):

    # Base Case: When N < 3
    if (n < 3):
        print(arr[0])
        return

    # Store the results in table
    dp = [0] * n

    # Initialize base cases
    dp[0] = arr[0]
    dp[1] = dp[0] + arr[1] + arr[2]

    # Iterate over the range[2, N - 2]
    # to construct the dp array
    for i in range(2, n - 1):
        dp[i] = min(dp[i - 2] + arr[i],
                    dp[i - 1] + arr[i]
                    + arr[i + 1])

    # Handle case for the last index, i.e. N - 1
    dp[n - 1] = min(dp[n - 2],
                    dp[n - 3] + arr[n - 1])

    # Print the answer
    print(dp[n - 1])

# Driver Code
if __name__ == "__main__":

    arr = [9, 4, 6, 8, 5]
    N = len(arr)
    minCost(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# Program to implement
// the above approach
using System;
public class GFG
{

  // Function to find the minimum cost
  // to reach the end of an array
  static void minCost(int []arr, int n)
  {

    // Base Case: When N < 3
    if (n < 3) {
      Console.WriteLine(arr[0]);
      return;
    }

    // Store the results in table
    int []dp = new int[n];

    // Initialize base cases
    dp[0] = arr[0];
    dp[1] = dp[0] + arr[1] + arr[2];

    // Iterate over the range[2, N - 2]
    // to construct the dp array
    for (int i = 2; i < n - 1; i++)
      dp[i] = Math.Min(dp[i - 2] + arr[i],
                       dp[i - 1] + arr[i] + arr[i + 1]);

    // Handle case for the last index, i.e. N - 1
    dp[n - 1] = Math.Min(dp[n - 2], dp[n - 3] + arr[n - 1]);

    // Print the answer
    Console.WriteLine(dp[n - 1]);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int []arr = { 9, 4, 6, 8, 5 };
    int N = arr.Length;
    minCost(arr, N);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find the minimum cost
    // to reach the end of an array
    function minCost(arr, n)
    {

        // Base Case: When N < 3
        if (n < 3) {
            document.write(arr[0]);
            return;
        }

        // Store the results in table
        let dp = [];

        // Initialize base cases
        dp[0] = arr[0];
        dp[1] = dp[0] + arr[1] + arr[2];

        // Iterate over the range[2, N - 2]
        // to construct the dp array
        for (let i = 2; i < n - 1; i++)
            dp[i] = Math.min(dp[i - 2] + arr[i],
                           dp[i - 1] + arr[i] + arr[i + 1]);

        // Handle case for the last index, i.e. N - 1
        dp[n - 1] = Math.min(dp[n - 2], dp[n - 3] + arr[n - 1]);

        // Prlet the answer
        document.write(dp[n - 1]);
    }

// Driver Code

        let arr = [ 9, 4, 6, 8, 5 ];
        let N = arr.length;
        minCost(arr, N);

</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)