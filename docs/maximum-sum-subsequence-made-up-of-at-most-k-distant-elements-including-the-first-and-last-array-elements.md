# 最大和子序列由最多 K 个距离元素组成，包括第一个和最后一个数组元素

> 原文:[https://www . geeksforgeeks . org/最大和子序列-由最多 k 个距离元素组成-包括第一个和最后一个数组元素/](https://www.geeksforgeeks.org/maximum-sum-subsequence-made-up-of-at-most-k-distant-elements-including-the-first-and-last-array-elements/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在满足以下条件的子序列中打印最大可能和:

1.  子序列中包含元素**arr[N–1]**和 **arr[0]** 。
2.  子序列中的相邻元素之间的距离最多为 **K** 个索引。

**示例:**

> **输入:** arr[] = {10，-5，-2，4，0，3}，K = 3
> **输出:** 17
> **解释:**
> 可能的方式之一如下:
> 将 arr[0]包含到子序列中。总和= 10。
> 在子序列中包含 arr[3]。因此，sum = 10 + 4 = 14。
> 在子序列中包含 arr[5]。因此，总和= 14 + 3 = 17。
> 因此，最大可能和为 17。
> 
> **输入:** arr[] = {1，-5，-20，4，-1，3，-6，-3}，K = 2
> **输出:** 0

**天真方法:**最简单的方法是[从**arr【】**中找到所有可能的子序列](https://www.geeksforgeeks.org/maximum-sum-subsequence-least-k-distant-elements/)，相邻元素的索引之间最多有 **K** 个差异，从索引 **0** 开始，到索引**(N–1)**结束。计算所有这些子序列的和。最后，打印得到的所有总和的最大值。
***时间复杂度:**O(N * 2<sup>N</sup>)*
*T21】辅助空间: O(N)*

**高效方法:**上述方法可以通过使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)和[德格](https://www.geeksforgeeks.org/deque-in-python/)进行优化。按照以下步骤解决问题:

*   初始化一个数组，比如 **dp[]** ，将获得的最大值存储到当前索引。
*   初始化一组配对，比如说 **Q** ，来存储配对 **{dp[i]，i}** 。
*   将 **arr[0]** 的值分配给 **dp[0]** ，[将配对 **{dp[0]，0}** 推入德格](https://www.geeksforgeeks.org/dequepush_back-c-stl/)。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   将 **dp[i]** 增加 **arr[i]** 和德格中最大值之和，即 **dp[i] = arr[i] + Q[0][0]** 。
    *   如果 **Q[-1][0]** 小于 **dp[i]** ，则从终点穿越德格 **Q** 并[弹出最后一个元素](https://www.geeksforgeeks.org/how-to-get-the-first-and-last-elements-of-deque-in-python/)。
    *   将配对 **{dp[i]，i}** 追加到 deque 中。
    *   检查德格 **q** 的[第一个元素的索引是否等于**(I–K)**，然后，](https://www.geeksforgeeks.org/dequefront-dequeback-c-stl/)[从德格](https://www.geeksforgeeks.org/deque-in-python/) **Q** 弹出第一个元素。
*   完成上述步骤后，打印存储在 **dp[]** 最后一个索引处的值，即**DP[N–1]**作为结果。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find maximum sum
// of a subsequence satisfying
// the given conditions
int maxResult(int arr[], int k, int n){

  // Stores the maximum sum
  int dp[n] = {0};

  // Starting index of
  // the subsequence
  dp[0] = arr[0];

  // Stores the pair of maximum value
  // and the index of that value
  deque<pair<int,int>> q;
  q.push_back({arr[0], 0});

  // Traverse the array
  for (int i = 1; i < n; i++)
  {

    // Increment the first value
    // of deque by arr[i] and
    // store it in dp[i]
    dp[i] = arr[i] + q.front().first;

    // Delete all the values which
    // are less than dp[i] in deque
    while (q.size() > 0 and q.back().first < dp[i])
      q.pop_back();

    // Append the current pair of
    // value and index in deque
    q.push_back({dp[i], i});

    // If first value of the
    // queue is at a distance > K
    if (i - k == q.front().second)
      q.pop_front();
  }

  // Return the value at the last index
  return dp[n - 1];
}

// Driver Code
int main()
{
  int arr[] = {10, -5, -2, 4, 0, 3};
  int K = 3;
  int n = sizeof(arr)/sizeof(arr[0]);
  cout<<maxResult(arr, K,n);

}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Pair class Store (x,y) Pair
    static class Pair {
        int x, y;

        Pair(int x, int y) {
            this.x = x;
            this.y = y;
        }

    }

    // Function to find maximum sum
    // of a subsequence satisfying
    // the given conditions
    private static int maxResult(int[] arr, int k, int n) {

        // Stores the maximum sum
        int dp[] = new int[n];

        // Starting index of
        // the subsequence
        dp[0] = arr[0];

        // Stores the pair of maximum value
        // and the index of that value
        Deque<Pair> q = new LinkedList<Pair>();
        q.add(new Pair(arr[0], 0));

        // Traverse the array
        for (int i = 1; i < n; i++)
        {

          // Increment the first value
          // of deque by arr[i] and
          // store it in dp[i]
          dp[i] = arr[i] + q.peekFirst().x;

          // Delete all the values which
          // are less than dp[i] in deque
          while (q.size() > 0 && q.peekLast().x < dp[i])
            q.pollLast();

          // Append the current pair of
          // value and index in deque
          q.add(new Pair(dp[i], i));

          // If first value of the
          // queue is at a distance > K
          if (i - k == q.peekFirst().y)
            q.pollFirst();
        }

        // Return the value at the last index
        return dp[n - 1];

    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {10, -5, -2, 4, 0, 3};
        int K = 3;
        int n = arr.length;
        System.out.println(maxResult(arr, K,n));
    }

}

// This code is contributed by Dheeraj Bhagchandani.
```

## 蟒蛇 3

```
# Python program for the above approach
from collections import deque

# Function to find maximum sum
# of a subsequence satisfying
# the given conditions
def maxResult(arr, k):

    # Stores the maximum sum
    dp = [0]*len(arr)

    # Starting index of
    # the subsequence
    dp[0] = arr[0]

    # Stores the pair of maximum value
    # and the index of that value
    q = deque([(arr[0], 0)])

    # Traverse the array
    for i in range(1, len(arr)):

        # Increment the first value
        # of deque by arr[i] and
        # store it in dp[i]
        dp[i] = arr[i] + q[0][0]

        # Delete all the values which
        # are less than dp[i] in deque
        while q and q[-1][0] < dp[i]:
            q.pop()

        # Append the current pair of
        # value and index in deque
        q.append((dp[i], i))

        # If first value of the
        # queue is at a distance > K
        if i - k == q[0][1]:
            q.popleft()

    # Return the value at the last index
    return dp[-1]

# Driver Code

arr = [10, -5, -2, 4, 0, 3]
K = 3
print(maxResult(arr, K))
```

**Output:** 

```
17
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)