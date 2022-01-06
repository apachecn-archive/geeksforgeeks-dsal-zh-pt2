# 最小化要添加到给定数组中的元素，使其包含另一个给定数组作为其子序列

> 原文:[https://www . geesforgeks . org/最小化要添加到给定数组中的元素，使其包含另一个给定数组作为其子序列/](https://www.geeksforgeeks.org/minimize-elements-to-be-added-to-a-given-array-such-that-it-contains-another-given-array-as-its-subsequence/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和另一个由 **M** 个整数组成的数组**B【】**，任务是找到要添加到数组**B【】**中的元素的最小数量，使得数组**A【】**成为数组**B【】**的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** N = 5，M = 6，A[] = {1，2，3，4，5}，B[] = {2，5，6，4，9，12}
> **输出:** 3
> **说明:**
> 下面是需要添加的元素:
> 1)在 B[]
> 的元素 2 之前添加 12)在 B[]
> 的元素 6 之后添加 3)在 B[]
> 的最后一个位置添加 5。
> 因此，得到的数组 B[]为{1，2，5，6，3，4，9，12，5}。
> 因此，A[]是 B[]加上 3 个元素后的子序列。
> 
> **输入:** N = 5，M = 5，A[] = {3，4，5，2，7}，B[] = {3，4，7，9，2}
> **输出:** 2
> **说明:**
> 以下是需要添加的元素:
> 1)在元素 4 后添加 5。
> 2)在要素 5 后增加 2。
> 因此，得到的数组 B[]为{3，4，5，2，7，9，2}。
> 因此需要添加 2 个元素。

**天真的方法:**天真的方法是[生成数组的所有子序列 **B**](https://www.geeksforgeeks.org/print-subsequences-string/) ，然后找到该子序列，使得在从数组中添加最小数量的元素时 **A** 使其等于数组 **A** 。打印添加的元素的最小计数。
***时间复杂度:**O(N * 2<sup>M</sup>)*
***辅助空间:** O(M+N)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。想法是在给定的两个数组 **A** 和 **B** 之间找到[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)。主要观察是通过从数组 **A[]** 的长度中减去最长公共子序列的长度，可以找到 **B[]** 中要添加的元素的最小数量，使得 **A[]** 成为其子序列。

因此，数组 **A[]** 的长度与最长公共子序列的长度之差就是所需的结果。

下面是上述方法的实现:

## C++14

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the minimum number
// of the element must be added to make A
// as a subsequence in B
int transformSubsequence(int n, int m,
                         vector<int> A,
                         vector<int> B)
{

    // Base Case
    if (B.size() == 0)
        return n;

    // dp[i][j] indicates the length of
    // LCS of A of length i & B of length j
    vector<vector<int>> dp(n + 1,
           vector<int>(m + 1, 0));

    for(int i = 0; i < n + 1; i++)
    {
        for(int j = 0; j < m + 1; j++)
        {

            // If there are no elements
            // either in A or B then the
            // length of lcs is 0
            if (i == 0 or j == 0)
                dp[i][j] = 0;

            // If the element present at
            // ith and jth index of A and B
            // are equal then include in LCS
            else if (A[i - 1] == B[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];

            // If they are not equal then
            // take the max
            else
                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j - 1]);
        }
    }

    // Return difference of length
    // of A and lcs of A and B
    return n - dp[n][m];
}

// Driver Code
int main()
{
    int N = 5;
    int M = 6;

    // Given sequence A and B
    vector<int> A = { 1, 2, 3, 4, 5 };
    vector<int> B = { 2, 5, 6, 4, 9, 12 };

    // Function call
    cout << transformSubsequence(N, M, A, B);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function that finds the minimum number
// of the element must be added to make A
// as a subsequence in B
static int transformSubsequence(int n, int m,
                                int []A, int []B)
{
  // Base Case
  if (B.length == 0)
    return n;

  // dp[i][j] indicates the length of
  // LCS of A of length i & B of length j
  int [][]dp = new int[n + 1][m + 1];

  for(int i = 0; i < n + 1; i++)
  {
    for(int j = 0; j < m + 1; j++)
    {
      // If there are no elements
      // either in A or B then the
      // length of lcs is 0
      if (i == 0 || j == 0)
        dp[i][j] = 0;

      // If the element present at
      // ith and jth index of A and B
      // are equal then include in LCS
      else if (A[i - 1] == B[j - 1])
        dp[i][j] = 1 + dp[i - 1][j - 1];

      // If they are not equal then
      // take the max
      else
        dp[i][j] = Math.max(dp[i - 1][j],
                            dp[i][j - 1]);
    }
  }

  // Return difference of length
  // of A and lcs of A and B
  return n - dp[n][m];
}

// Driver Code
public static void main(String[] args)
{
  int N = 5;
  int M = 6;

  // Given sequence A and B
  int []A = {1, 2, 3, 4, 5};
  int []B = {2, 5, 6, 4, 9, 12};

  // Function call
  System.out.print(transformSubsequence(N, M, A, B));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the minimum number
# of the element must be added to make A
# as a subsequence in B
def transformSubsequence(n, m, A, B):

    # Base Case
    if B is None or len(B) == 0:
        return n

    # dp[i][j] indicates the length of
    # LCS of A of length i & B of length j
    dp = [[0 for col in range(m + 1)]
        for row in range(n + 1)]

    for i in range(n + 1):

        for j in range(m + 1):

            # If there are no elements
            # either in A or B then the
            # length of lcs is 0
            if i == 0 or j == 0:
                dp[i][j] = 0

            # If the element present at
            # ith and jth index of A and B
            # are equal then include in LCS
            elif A[i-1] == B[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]

            # If they are not equal then
            # take the max
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    # Return difference of length
    # of A and lcs of A and B
    return n - dp[n][m]

# Driver Code
if __name__ == "__main__":

    N = 5
    M = 6

    # Given Sequence A and B
    A = [1, 2, 3, 4, 5]
    B = [2, 5, 6, 4, 9, 12]

    # Function Call
    print(transformSubsequence(N, M, A, B))
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that finds the minimum number
// of the element must be added to make A
// as a subsequence in B
static int transformSubsequence(int n, int m,
                                int []A, int []B)
{
  // Base Case
  if (B.Length == 0)
    return n;

  // dp[i,j] indicates the length of
  // LCS of A of length i & B of length j
  int [,]dp = new int[n + 1, m + 1];

  for(int i = 0; i < n + 1; i++)
  {
    for(int j = 0; j < m + 1; j++)
    {
      // If there are no elements
      // either in A or B then the
      // length of lcs is 0
      if (i == 0 || j == 0)
        dp[i, j] = 0;

      // If the element present at
      // ith and jth index of A and B
      // are equal then include in LCS
      else if (A[i - 1] == B[j - 1])
        dp[i, j] = 1 + dp[i - 1, j - 1];

      // If they are not equal then
      // take the max
      else
        dp[i, j] = Math.Max(dp[i - 1, j],
                            dp[i, j - 1]);
    }
  }

  // Return difference of length
  // of A and lcs of A and B
  return n - dp[n, m];
}

// Driver Code
public static void Main(String[] args)
{
  int N = 5;
  int M = 6;

  // Given sequence A and B
  int []A = {1, 2, 3, 4, 5};
  int []B = {2, 5, 6, 4, 9, 12};

  // Function call
  Console.Write(transformSubsequence(N, M,
                                     A, B));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that finds the minimum number
// of the element must be added to make A
// as a subsequence in B
function transformSubsequence(n, m, A, B)
{

    // Base Case
    if (B.length == 0)
        return n;

    // dp[i][j] indicates the length of
    // LCS of A of length i & B of length j
    var dp = Array.from(Array(n+1), ()=>Array(m+1).fill(0));

    for(var i = 0; i < n + 1; i++)
    {
        for(var j = 0; j < m + 1; j++)
        {

            // If there are no elements
            // either in A or B then the
            // length of lcs is 0
            if (i == 0 || j == 0)
                dp[i][j] = 0;

            // If the element present at
            // ith and jth index of A and B
            // are equal then include in LCS
            else if (A[i - 1] == B[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];

            // If they are not equal then
            // take the max
            else
                dp[i][j] = Math.max(dp[i - 1][j],
                               dp[i][j - 1]);
        }
    }

    // Return difference of length
    // of A and lcs of A and B
    return n - dp[n][m];
}

// Driver Code

var N = 5;
var M = 6;

// Given sequence A and B
var A = [1, 2, 3, 4, 5 ];
var B = [2, 5, 6, 4, 9, 12 ];

// Function call
document.write( transformSubsequence(N, M, A, B));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(M*M)，其中 N 和 M 分别是数组 A[]和 B[]的长度。*
***辅助空间:** O(M*N)*