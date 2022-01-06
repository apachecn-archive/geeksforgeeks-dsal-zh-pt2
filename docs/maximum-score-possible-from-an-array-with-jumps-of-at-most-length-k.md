# 最多跳跃长度为 K 的数组的最大可能得分

> 原文:[https://www . geeksforgeeks . org/最大可能长度跳跃数组得分-k/](https://www.geeksforgeeks.org/maximum-score-possible-from-an-array-with-jumps-of-at-most-length-k/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K** ，**0**索引，任务是通过执行以下操作收集可能的最大得分:

*   从 **0 <sup>第</sup>个**索引的数组开始。
*   每次移动最多跳 **K** 个指标，到达数组的最后一个指标。
*   将每次跳转后达到的每个索引的值相加。
    *   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **dp[]** 来存储之前计算的结果。
    *   现在，从第**0**索引开始，对每个第**I**索引执行以下操作:
        *   如果当前索引大于或等于最后一个元素的索引，则返回数组的最后一个元素。
        *   如果当前索引的值是预先计算的，则返回预先计算的值。
        *   否则，计算通过移动到范围 **i + 1** 至 **i + K** 中的所有步骤可以获得的最大分数，并使用以下递归关系将各个指数的结果存储在 **dp[]** 数组中:

> **dp[i] = max（dp[i + 1]， dp[i + 2]， dp[i + 3]， .....， dp[i + K]） + A[i].。**

*   现在，打印 **dp[0]** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum
// score of an index
int maxScore(int i, int A[], int K, int N, int dp[])
{
    // Base Case
    if (i >= N - 1)
        return A[N - 1];

    // If the value for the current
    // index is pre-calculated
    if (dp[i] != -1)
        return dp[i];

    int score = INT_MIN;

    // Calculate maximum score
    // for all the steps in the
    // range from i + 1 to i + k
    for (int j = 1; j <= K; j++) {

        // Score for index (i + j)
        score = max(score, maxScore(i + j, A, K, N, dp));
    }

    // Update dp[i] and return
    // the maximum value
    return dp[i] = score + A[i];
}

// Function to get maximum score
// possible from the array A[]
int getScore(int A[], int N, int K)
{
    // Array to store memoization
    int dp[N];

    // Initialize dp[] with -1
    for (int i = 0; i < N; i++)
        dp[i] = -1;

    cout << maxScore(0, A, K, N, dp);
}

// Driver Code
int main()
{
    int A[] = { 100, -30, -50, -15, -20, -30 };
    int K = 3;
    int N = sizeof(A) / sizeof(A[0]);

    getScore(A, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.io.*;
import java.math.*;
import java.util.*;
public class GFG
{

  // Function to count the maximum
  // score of an index
  static int maxScore(int i, int A[], int K, int N,
                      int dp[])
  {

    // Base Case
    if (i >= N - 1)
      return A[N - 1];

    // If the value for the current
    // index is pre-calculated
    if (dp[i] != -1)
      return dp[i];
    int score = Integer.MIN_VALUE;

    // Calculate maximum score
    // for all the steps in the
    // range from i + 1 to i + k
    for (int j = 1; j <= K; j++)
    {

      // Score for index (i + j)
      score = Math.max(score,
                       maxScore(i + j, A, K, N, dp));
    }

    // Update dp[i] and return
    // the maximum value
    return dp[i] = score + A[i];
  }

  // Function to get maximum score
  // possible from the array A[]
  static void getScore(int A[], int N, int K)
  {

    // Array to store memoization
    int dp[] = new int[N];

    // Initialize dp[] with -1
    for (int i = 0; i < N; i++)
      dp[i] = -1;
    System.out.println(maxScore(0, A, K, N, dp));
  }

  // Driver Code
  public static void main(String args[])
  {
    int A[] = { 100, -30, -50, -15, -20, -30 };
    int K = 3;
    int N = A.length;

    getScore(A, N, K);
  }
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python program for the above approach
import sys

# Function to count the maximum
# score of an index
def maxScore(i, A, K, N, dp):

    # Base Case
    if (i >= N - 1):
        return A[N - 1];

    # If the value for the current
    # index is pre-calculated
    if (dp[i] != -1):
        return dp[i];
    score = 1-sys.maxsize;

    # Calculate maximum score
    # for all the steps in the
    # range from i + 1 to i + k
    for j in range(1, K + 1):

        # Score for index (i + j)
        score = max(score, maxScore(i + j, A, K, N, dp));

    # Update dp[i] and return
    # the maximum value
    dp[i] = score + A[i];
    return dp[i];

# Function to get maximum score
# possible from the array A
def getScore(A, N, K):
    # Array to store memoization
    dp = [0]*N;

    # Initialize dp with -1
    for i in range(N):
        dp[i] = -1;
    print(maxScore(0, A, K, N, dp));

# Driver Code
if __name__ == '__main__':
    A = [100, -30, -50, -15, -20, -30];
    K = 3;
    N = len(A);

    getScore(A, N, K);

# This code contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count the maximum
  // score of an index
  static int maxScore(int i, int []A, int K, int N,
                      int []dp)
  {

    // Base Case
    if (i >= N - 1)
      return A[N - 1];

    // If the value for the current
    // index is pre-calculated
    if (dp[i] != -1)
      return dp[i];
    int score = int.MinValue;

    // Calculate maximum score
    // for all the steps in the
    // range from i + 1 to i + k
    for (int j = 1; j <= K; j++)
    {

      // Score for index (i + j)
      score = Math.Max(score,
                       maxScore(i + j, A, K, N, dp));
    }

    // Update dp[i] and return
    // the maximum value
    return dp[i] = score + A[i];
  }

  // Function to get maximum score
  // possible from the array A[]
  static void getScore(int []A, int N, int K)
  {

    // Array to store memoization
    int []dp = new int[N];

    // Initialize dp[] with -1
    for (int i = 0; i < N; i++)
      dp[i] = -1;
    Console.WriteLine(maxScore(0, A, K, N, dp));
  }

// Driver Code
static public void Main()
{
    int []A = { 100, -30, -50, -15, -20, -30 };
    int K = 3;
    int N = A.Length;

    getScore(A, N, K);
}
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>
// javascript program of the above approach

  // Function to count the maximum
  // score of an index
  function maxScore(i, A, K, N,
                      dp)
  {

    // Base Case
    if (i >= N - 1)
      return A[N - 1];

    // If the value for the current
    // index is pre-calculated
    if (dp[i] != -1)
      return dp[i];
    let score = -1000;

    // Calculate maximum score
    // for all the steps in the
    // range from i + 1 to i + k
    for (let j = 1; j <= K; j++)
    {

      // Score for index (i + j)
      score = Math.max(score,
                       maxScore(i + j, A, K, N, dp));
    }

    // Update dp[i] and return
    // the maximum value
    return dp[i] = score + A[i];
  }

  // Function to get maximum score
  // possible from the array A[]
  function getScore(A, N, K)
  {

    // Array to store memoization
    let dp = new Array(N).fill(-1);

    document.write(maxScore(0, A, K, N, dp));
  }

    // Driver Code

    let A = [ 100, -30, -50, -15, -20, -30 ];
    let K = 3;
    let N = A.length;

    getScore(A, N, K);

</script>
```

**Output**

```
55
```

***时间复杂度:** O(N * K)*

***辅助空间:** O(N * K)*

**高效方法:**按照以下步骤解决问题

*   初始化一个[最大堆](https://www.geeksforgeeks.org/heap-data-structure/)来存储之前的 **K** 指数的结果。
*   现在，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** 计算所有指标的最大得分。
    *   对于第**0**指数，得分将是第**0**指数的值。
    *   现在，对于范围**【1，N-1】**中的每一个 **i <sup>th</sup>** 指数。
        *   首先，从[最大堆](https://www.geeksforgeeks.org/max-heap-in-java/)中删除指数小于**I–K**的最大得分。
        *   现在计算**I<sup>th</sup>T3】指数的最高分。
            **最大得分= A[i] +最大堆顶部的得分**。**
        *   现在将最大得分插入到最大堆及其索引中。
*   返回获得的**最高分**。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure to sort a priority queue on
// the basis of first element of the pair
struct mycomp {
    bool operator()(pair<int, int> p1,
                    pair<int, int> p2)
    {
        return p1.first < p2.first;
    }
};

// Function to calculate maximum
// score possible from the array A[]
int maxScore(int A[], int K, int N)
{
    // Stores the score of previous k indices
    priority_queue<pair<int, int>,
                vector<pair<int, int> >, mycomp>
        maxheap;

    // Stores the maximum
    // score for current index
    int maxScore = 0;

    // Maximum score at first index
    maxheap.push({ A[0], 0 });

    // Traverse the array to calculate
    // maximum score for all indices
    for (int i = 1; i < N; i++) {

        // Remove maximum scores for
        // indices less than i - K
        while (maxheap.top().second < (i - K)) {
            maxheap.pop();
        }

        // Calculate maximum score for current index
        maxScore = A[i] + maxheap.top().first;

        // Push maximum score of
        // current index along
        // with index in maxheap
        maxheap.push({ maxScore, i });
    }

    // Return the maximum score
    return maxScore;
}

// Driver Code
int main()
{
    int A[] = { -44, -17, -54, 79 };
    int K = 2;
    int N = sizeof(A) / sizeof(A[0]);

    // Function call to calculate
    // maximum score from the array A[]
    cout << maxScore(A, K, N);

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate maximum
// score possible from the array A[]
function maxScore(A, K, N)
{

    // Stores the score of previous k indices
    var maxheap = [];

    // Stores the maximum
    // score for current index
    var maxScore = 0;

    // Maximum score at first index
    maxheap.push([A[0], 0]);

    // Traverse the array to calculate
    // maximum score for all indices
    for (var i = 1; i < N; i++) {

        // Remove maximum scores for
        // indices less than i - K
        while (maxheap[maxheap.length-1][1] < (i - K)) {
            maxheap.pop();
        }

        // Calculate maximum score for current index
        maxScore = A[i] + maxheap[maxheap.length-1][0];

        // Push maximum score of
        // current index along
        // with index in maxheap
        maxheap.push([maxScore, i]);
        maxheap.sort();
    }

    // Return the maximum score
    return maxScore;
}

// Driver Code
var A = [-44, -17, -54, 79];
var K = 2;
var N = A.length;

// Function call to calculate
// maximum score from the array A[]
document.write(maxScore(A, K, N));

// This code is contributed by noob2000.
</script>
```

**Output**

```
18
```

***时间复杂度:** O(N * log K)*

***辅助空间:** O(N)*