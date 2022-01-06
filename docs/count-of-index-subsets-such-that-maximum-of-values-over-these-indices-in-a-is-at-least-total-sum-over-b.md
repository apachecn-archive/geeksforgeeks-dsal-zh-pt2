# 索引子集的计数，使得 A 中这些索引的最大值至少是 B 的总和

> 原文:[https://www . geeksforgeeks . org/index-subset-count-of-this-values-max-over-the-index-in-a-is-at-total-sum-b/](https://www.geeksforgeeks.org/count-of-index-subsets-such-that-maximum-of-values-over-these-indices-in-a-is-at-least-total-sum-over-b/)

给定两个由正整数组成的 **N** 数组**A【】**和**B【】**，任务是找到索引的[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的总数，使得数组**A【】**中所有这些索引的最大值大于或等于数组**B【】**中这些索引的所有值之和。

**示例:**

> **输入:** A[] = {3，1}，B[] = {1，2}
> **输出:** 2
> **解释:**
> 索引的可能有效子集总数为{0}、{0，1}
> {0}:最大值(3) > =和(1)
> {1，2}:最大值(1，3) > =和(1，2)
> 
> **输入:** A[] = {1，3，2，6}，B[] = {7，3，2，1 }
> T3】输出: 6

**方法:**借助 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) ，利用 [**子集和问题**](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/) 中讨论的概念可以解决上述问题。其思想是创建一个 **dp[][]** 的维度 **N** * [**数组的最大元素 A[]**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) 。现在， **dp[][]** 矩阵的每个节点，即 **dp[i][j]** 代表具有和 **j** 的第一 **i** 元素的子集的数量。请按照以下步骤解决此问题:

*   创建一个变量，将**和**表示为 **0** 来存储所需子集的总数。
*   创建[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，说 **AB** ，用 A & B 的元素填充，即**AB【I】= { A【I】，B【I】}**。
*   [在第一个元素](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的基础上对这个向量对进行排序。
*   最初 dp 表除了 **dp[0][0] = 1** 之外都是零。
*   [遍历数组 **AB[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) 并考虑 **AB[i]的值。首先**作为最大值，因为 **AB** 在第一个元素上排序，并且它在范围**【0，I】**中最大，并且在每次迭代中，遍历所有可能的和 **j** ，并且对于每次迭代计算子集，直到索引 **i** 通过包括和排除当前元素而具有和 **j** 。
*   完成上述步骤后，[遍历矩阵 **dp[][]**](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/) ，通过检查以下条件检查形成的子集有多少是有效的。如果发现**为真**，则将数值**DP[I–1][j]**加到变量 **ans** 上。

> j+AB[I–1]。第二< = AB[i]。第一

*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of non-empty
// subset of indices such that the maximum
// of values over these indices in A is
// at least the total sum over B[]
int countValidSubsets(int A[], int B[], int N)
{
    int ans = 0;

    vector<pair<int, int> > AB(N);

    // Stores the maximum element in
    // the array A[]
    int mx = INT_MIN;

    // Do the DP in 1-based indexing
    // as there will be no corner case
    // to handle specifically
    for (int i = 0; i <= N; i++) {
        AB[i] = { A[i], B[i] };
        mx = max(mx, A[i]);
    }

    // Sort the pair vector
    sort(AB.begin(), AB.end());

    // dp matrix where dp[i][j] denotes
    // total valid subsets upto index
    // i with sum j
    vector<vector<int> > dp(
        N + 1, vector<int>(mx + 1, 0));

    dp[0][0] = 1;

    // Traverse the array AB[]
    for (int i = 1; i <= N; i++) {
        for (int j = 0; j <= mx; j++) {

            // Selecting the current
            // element in the subset
            if (j + AB[i - 1].second <= mx) {
                dp[i][j + AB[i - 1].second]
                    += dp[i - 1][j];
            }

            // Discarding the element
            dp[i][j] += dp[i - 1][j];
        }
    }

    // Take the count of valid subsets
    for (int i = 1; i <= N; ++i) {
        int cnt = 0;

        // Iterate through all the
        // possible subsets
        for (int j = 0; j <= mx; j++) {

            // Check if the current subsets
            // till index i having sum j
            // are valid
            if (j + AB[i - 1].second
                <= AB[i - 1].first) {
                cnt += dp[i - 1][j];
            }
        }

        // Update the value of ans
        ans += cnt;
    }

    // Return the total count of subsets
    return ans;
}

// Driver Code
int main()
{
    int A[] = { 1, 3, 2, 6 };
    int B[] = { 7, 3, 2, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    cout << countValidSubsets(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to find the number of non-empty
// subset of indices such that the maximum
// of values over these indices in A is
// at least the total sum over B[]
static int countValidSubsets(int A[], int B[], int N)
{
    int ans = 0;

    pair []AB = new pair[N];

    // Stores the maximum element in
    // the array A[]
    int mx = Integer.MIN_VALUE;

    // Do the DP in 1-based indexing
    // as there will be no corner case
    // to handle specifically
    for (int i = 0; i < N; i++) {
        AB[i] = new pair( A[i], B[i] );
        mx = Math.max(mx, A[i]);
    }

    // Sort the pair vector
    Arrays.sort(AB,(a,b)->a.first-b.first);

    // dp matrix where dp[i][j] denotes
    // total valid subsets upto index
    // i with sum j
    int[][] dp= new int[N + 1][mx + 1];

    dp[0][0] = 1;

    // Traverse the array AB[]
    for (int i = 1; i <= N; i++) {
        for (int j = 0; j <= mx; j++) {

            // Selecting the current
            // element in the subset
            if (j + AB[i - 1].second <= mx) {
                dp[i][j + AB[i - 1].second]
                    += dp[i - 1][j];
            }

            // Discarding the element
            dp[i][j] += dp[i - 1][j];
        }
    }

    // Take the count of valid subsets
    for (int i = 1; i <= N; ++i) {
        int cnt = 0;

        // Iterate through all the
        // possible subsets
        for (int j = 0; j <= mx; j++) {

            // Check if the current subsets
            // till index i having sum j
            // are valid
            if (j + AB[i - 1].second
                <= AB[i - 1].first) {
                cnt += dp[i - 1][j];
            }
        }

        // Update the value of ans
        ans += cnt;
    }

    // Return the total count of subsets
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 3, 2, 6 };
    int B[] = { 7, 3, 2, 1 };
    int N = A.length;

    System.out.print(countValidSubsets(A, B, N));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach
INT_MIN = -2147483648

# Function to find the number of non-empty
# subset of indices such that the maximum
# of values over these indices in A is
# at least the total sum over B[]
def countValidSubsets(A, B, N):
    ans = 0
    AB = [[0 for _ in range(2)] for _ in range(N)]

    # Stores the maximum element in
    # the array A[]
    mx = INT_MIN

    # Do the DP in 1-based indexing
    # as there will be no corner case
    # to handle specifically
    for i in range(0, N):
        AB[i] = [A[i], B[i]]
        mx = max(mx, A[i])

        # Sort the pair vector
    AB.sort()

    # dp matrix where dp[i][j] denotes
    # total valid subsets upto index
    # i with sum j
    dp = [[0 for _ in range(mx+1)] for _ in range(N+1)]

    dp[0][0] = 1

    # Traverse the array AB[]
    for i in range(1, N+1):
        for j in range(0, mx+1):

                        # Selecting the current
                        # element in the subset
            if (j + AB[i - 1][1] <= mx):
                dp[i][j + AB[i - 1][1]] += dp[i - 1][j]

                # Discarding the element
            dp[i][j] += dp[i - 1][j]

        # Take the count of valid subsets
    for i in range(1, N+1):
        cnt = 0

        # Iterate through all the
        # possible subsets
        for j in range(0, mx+1):

                        # Check if the current subsets
                        # till index i having sum j
                        # are valid
            if (j + AB[i - 1][1] <= AB[i - 1][0]):
                cnt += dp[i - 1][j]

                # Update the value of ans
        ans += cnt

        # Return the total count of subsets
    return ans

# Driver Code
if __name__ == "__main__":

    A = [1, 3, 2, 6]
    B = [7, 3, 2, 1]
    N = len(A)

    print(countValidSubsets(A, B, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
public class GFG{
    class pair : IComparable<pair>
    {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
         public int CompareTo(pair p)
         {
             return this.first-p.second;
         }
    }

// Function to find the number of non-empty
// subset of indices such that the maximum
// of values over these indices in A is
// at least the total sum over []B
static int countValidSubsets(int []A, int []B, int N)
{
    int ans = 0;

    pair []AB = new pair[N];

    // Stores the maximum element in
    // the array []A
    int mx = int.MinValue;

    // Do the DP in 1-based indexing
    // as there will be no corner case
    // to handle specifically
    for (int i = 0; i < N; i++) {
        AB[i] = new pair( A[i], B[i] );
        mx = Math.Max(mx, A[i]);
    }

    // Sort the pair vector
    Array.Sort(AB);
    AB.Reverse();

    // dp matrix where dp[i,j] denotes
    // total valid subsets upto index
    // i with sum j
    int[,] dp= new int[N + 1,mx + 1];

    dp[0,0] = 1;

    // Traverse the array AB[]
    for (int i = 1; i <= N; i++) {
        for (int j = 0; j <= mx; j++) {

            // Selecting the current
            // element in the subset
            if (j + AB[i - 1].second <= mx) {
                dp[i,j + AB[i - 1].second]
                    += dp[i - 1,j];
            }

            // Discarding the element
            dp[i,j] += dp[i - 1,j];
        }
    }

    // Take the count of valid subsets
    for (int i = 1; i <= N; ++i) {
        int cnt = 0;

        // Iterate through all the
        // possible subsets
        for (int j = 0; j <= mx; j++) {

            // Check if the current subsets
            // till index i having sum j
            // are valid
            if (j + AB[i - 1].second
                <= AB[i - 1].first) {
                cnt += dp[i - 1,j];
            }
        }

        // Update the value of ans
        ans += cnt;
    }

    // Return the total count of subsets
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 1, 3, 2, 6 };
    int []B = { 7, 3, 2, 1 };
    int N = A.Length;

    Console.Write(countValidSubsets(A, B, N));

}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of non-empty
// subset of indices such that the maximum
// of values over these indices in A is
// at least the total sum over B[]
function countValidSubsets(A, B, N) {
  let ans = 0;

  let AB = new Array(N);

  // Stores the maximum element in
  // the array A[]
  let mx = Number.MIN_SAFE_INTEGER;

  // Do the DP in 1-based indexing
  // as there will be no corner case
  // to handle specifically
  for (let i = 0; i < N; i++) {
    AB[i] = [A[i], B[i]];
    mx = Math.max(mx, A[i]);
    console.log(A[i]);
  }

  // Sort the pair vector
  AB.sort((a, b) => a - b);

  // dp matrix where dp[i][j] denotes
  // total valid subsets upto index
  // i with sum j

  let dp = new Array(N + 1).fill(0).map(() => {
    return new Array(mx + 1).fill(0);
  });
  dp[0][0] = 1;

  // Traverse the array AB[]
  for (let i = 1; i <= N; i++)
  {
    for (let j = 0; j <= mx; j++)
    {

      // Selecting the current
      // element in the subset
      if (j + AB[i - 1][1] <= mx) {
        dp[i][j + AB[i - 1][1]] += dp[i - 1][j];
      }

      // Discarding the element
      dp[i][j] += dp[i - 1][j];
    }
  }

  // Take the count of valid subsets
  for (let i = 1; i <= N; ++i)
  {
    let cnt = 0;

    // Iterate through all the
    // possible subsets
    for (let j = 0; j <= mx; j++)
    {

      // Check if the current subsets
      // till index i having sum j
      // are valid
      if (j + AB[i - 1][1] <= AB[i - 1][0]) {
        cnt += dp[i - 1][j];
      }
    }

    // Update the value of ans
    ans += cnt;
  }

  // Return the total count of subsets
  return ans;
}

// Driver Code
let A = [1, 3, 2, 6];
let B = [7, 3, 2, 1];
let N = A.length;

document.write(countValidSubsets(A, B, N));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N*M)，其中 M 为阵中* [*最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(N*M)*