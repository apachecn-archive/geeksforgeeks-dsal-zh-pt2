# 具有第一元素增加和第二元素减少的对阵列中最长的子序列。

> 原文:[https://www . geeksforgeeks . org/从具有第一元素递增和第二元素递减的对数组中选择最长的子序列/](https://www.geeksforgeeks.org/longest-subsequence-from-an-array-of-pairs-having-first-element-increasing-and-second-element-decreasing/)

给定一个大小为 **N** 的[对数组](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **A[][]** ，任务是找到第一个元素增加而第二个元素减少的最长子序列。

***例:***

> ***输入:**A[]= {*1，2}，{2，2}，{3，1}}，N = 3
> T5】输出:2
> T8】说明:满足条件的最长子序列长度为 2，由{1，2}和{3，1}组成；
> 
> **输入:** A[] = {{1，3}，{2，5}，{3，2}，{5，2}，{4，1}}，N = 5
> **输出:** 3

**天真方法:**最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)。对于数组中的每一对，都有两种可能的选择，即是否将当前对包含在子序列中。因此，[递归地迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并找到所需的最长子序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find the length of
// the longest subsequence of pairs whose first
// element is increasing and second is decreasing
int longestSubSequence(pair<int, int> A[], int N,
                       int ind = 0,
                       int lastf = INT_MIN,
                       int lasts = INT_MAX)
{

    // Base case
    if (ind == N)
        return 0;

    // Not include the current pair
    // in the longest subsequence
    int ans = longestSubSequence(A, N, ind + 1,
                                 lastf, lasts);

    // Including the current pair
    // in the longest subsequence
    if (A[ind].first > lastf
        && A[ind].second < lasts)

        ans = max(ans, longestSubSequence(A, N, ind + 1,
                                          A[ind].first,
                                          A[ind].second)
                           + 1);

    return ans;
}

// Driver Code
int main()
{
    // Given Input
    pair<int, int> A[] = { { 1, 2 },
                           { 2, 2 },
                           { 3, 1 } };

    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << longestSubSequence(A, N) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Recursive function to find the length of
// the longest subsequence of pairs whose first
// element is increasing and second is decreasing
public static Integer longestSubSequence(int[][] A, int N, int ind,
                                         int lastf, int lasts)
{
    ind = (ind > 0 ? ind : 0);
    lastf = (lastf > 0 ? lastf: Integer.MIN_VALUE);
    lasts = (lasts > 0 ? lasts: Integer.MAX_VALUE);

    // Base case
    if (ind == N)
        return 0;

    // Not include the current pair
    // in the longest subsequence
    int ans = longestSubSequence(A, N, ind + 1,
                                 lastf, lasts);

    // Including the current pair
    // in the longest subsequence
    if (A[ind][0] > lastf && A[ind][1] < lasts)

        ans = Math.max(ans, longestSubSequence(A, N, ind + 1,
                                   A[ind][0], A[ind][1]) + 1);

    return ans;
}

public static int longestSubSequence(int[][] A, int N)
{
    return longestSubSequence(A, N, 0, 0, 0);
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int[][] A = { { 1, 2 }, { 2, 2 }, { 3, 1 } };
    int N = A.length;

    // Function Call
    System.out.println(longestSubSequence(A, N));
}
}

// This code is contributed by _saurabh_jaiswal
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Recursive function to find the length of
# the longest subsequence of pairs whose first
# element is increasing and second is decreasing
def longestSubSequence(A,  N,
                       ind=0,
                       lastf=-sys.maxsize-1,
                       lasts=sys.maxsize):

    # Base case
    if (ind == N):
        return 0

    # Not include the current pair
    # in the longest subsequence
    ans = longestSubSequence(A, N, ind + 1,
                             lastf, lasts)

    # Including the current pair
    # in the longest subsequence
    if (A[ind][0] > lastf
            and A[ind][1] < lasts):

        ans = max(ans, longestSubSequence(A, N, ind + 1,
                                          A[ind][0],
                                          A[ind][1])
                  + 1)

    return ans

# Driver Code
if __name__ == "__main__":

    # Given Input
    A = [[1, 2],
         [2, 2],
         [3, 1]]

    N = len(A)

    # Function Call
    print(longestSubSequence(A, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to find the length of
// the longest subsequence of pairs whose first
// element is increasing and second is decreasing
public static int longestSubSequence(int[,] A, int N, int ind,
                                         int lastf, int lasts)
{
    ind = (ind > 0 ? ind : 0);
    lastf = (lastf > 0 ? lastf: Int32.MinValue);
    lasts = (lasts > 0 ? lasts: Int32.MaxValue);

    // Base case
    if (ind == N)
        return 0;

    // Not include the current pair
    // in the longest subsequence
    int ans = longestSubSequence(A, N, ind + 1,
                                 lastf, lasts);

    // Including the current pair
    // in the longest subsequence
    if (A[ind, 0] > lastf && A[ind, 1] < lasts)

        ans = Math.Max(ans, longestSubSequence(A, N, ind + 1,
                                   A[ind, 0], A[ind, 1]) + 1);

    return ans;
}

public static int longestSubSequence(int[,] A, int N)
{
    return longestSubSequence(A, N, 0, 0, 0);
}

// Driver Code
public static void Main()
{
    // Given Input
    int[,] A = { { 1, 2 }, { 2, 2 }, { 3, 1 } };
    int N = A.GetLength(0);

    // Function Call
    Console.Write(longestSubSequence(A, N));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the length of the
// longest subsequence of pairs whose first
// element is increasing and second is decreasing
function longestSubSequence(A, N)
{
    // dp[i]: Stores the longest
    // subsequence upto i
    let dp = new Array(N);
    for (let i = 0; i < N; i++) {

        // Base case
        dp[i] = 1;

        for (let j = 0; j < i; j++) {

            // When the conditions hold
            if (A[j][0] < A[i][0]
                && A[j][1] > A[i][1]) {

                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
    }

    // Finally, print the required answer
    document.write(dp[N - 1] + "<br>");
}

// Driver Code

    // Given Input
    let A = [ [ 1, 2 ],
            [ 2, 2 ],
            [ 3, 1 ] ];

    let N = A.length;

    // Function Call
    longestSubSequence(A, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**该问题具有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构属性](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。因此，这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。像其他典型的[动态规划](https://www.geeksforgeeks.org/dynamic-programming/) ( **DP** )问题一样，通过构造存储子问题结果的临时数组，可以避免重新计算相同的子问题。

按照以下步骤解决此问题:

*   初始化一个 **dp[]** 数组，其中 **dp[i]** 存储最长子序列的长度，该最长子序列可以使用索引为 **i** 的元素形成。
*   [使用变量 **i** : 遍历范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**
    *   **基本情况:**更新**DP【I】**为 **1。**
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，I–1】**:
        *   **If**A【j】。第一**小于**一【我】。首先**和**A【j】。第二个**大于 **A[i]。其次，**然后更新 **dp[i]** 为 **dp[i]** 和 **dp[j] + 1 的最大值。****
    *   **最后打印**DP【N-1】**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest subsequence of pairs whose first
// element is increasing and second is decreasing
void longestSubSequence(pair<int, int> A[], int N)
{
    // dp[i]: Stores the longest
    // subsequence upto i
    int dp[N];
    for (int i = 0; i < N; i++) {

        // Base case
        dp[i] = 1;

        for (int j = 0; j < i; j++) {

            // When the conditions hold
            if (A[j].first < A[i].first
                && A[j].second > A[i].second) {

                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }

    // Finally, print the required answer
    cout << dp[N - 1] << endl;
}

// Driver Code
int main()
{
    // Given Input
    pair<int, int> A[] = { { 1, 2 },
                           { 2, 2 },
                           { 3, 1 } };

    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    longestSubSequence(A, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
class GFG{

// Function to find the length of the
// longest subsequence of pairs whose first
// element is increasing and second is decreasing
public static void longestSubSequence(int[][] A, int N)
{

    // dp[i]: Stores the longest
    // subsequence upto i
    int[] dp = new int[N];

    for(int i = 0; i < N; i++)
    {

        // Base case
        dp[i] = 1;

        for(int j = 0; j < i; j++)
        {

            // When the conditions hold
            if (A[j][0] < A[i][0] && A[j][1] > A[i][1])
            {
                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
    }

    // Finally, print the required answer
    System.out.println(dp[N - 1]);
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int[][] A = { { 1, 2 },
                  { 2, 2 },
                  { 3, 1 } };

    int N = A.length;

    // Function Call
    longestSubSequence(A, N);
}
}

// This code is contributed by gfgking
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the length of the
# longest subsequence of pairs whose first
# element is increasing and second is decreasing
def longestSubSequence(A, N):

    # dp[i]: Stores the longest
    # subsequence upto i
    dp = [0]*N
    for i in range(N):

        # Base case
        dp[i] = 1

        for j in range(i):

            # When the conditions hold
            if (A[j][0] < A[i][0] and A[j][1] > A[i][1]):
                dp[i] = max(dp[i], dp[j] + 1)

    # Finally, prthe required answer
    print (dp[N - 1])

# Driver Code
if __name__ == '__main__':

    #Given Input
    A = [ [ 1, 2 ],
           [ 2, 2 ],
           [ 3, 1 ] ]

    N = len(A)

    #Function Call
    longestSubSequence(A, N)

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the length of the
    // longest subsequence of pairs whose first
    // element is increasing and second is decreasing
    static void longestSubSequence(int[,] A, int N)
    {

        // dp[i]: Stores the longest
        // subsequence upto i
        int[] dp = new int[N];

        for(int i = 0; i < N; i++)
        {

            // Base case
            dp[i] = 1;

            for(int j = 0; j < i; j++)
            {

                // When the conditions hold
                if (A[j,0] < A[i,0] && A[j,1] > A[i,1])
                {
                    dp[i] = Math.Max(dp[i], dp[j] + 1);
                }
            }
        }

        // Finally, print the required answer
        Console.Write(dp[N - 1]);
    }

  static void Main()
  {

    // Given Input
    int[,] A = { { 1, 2 },
                  { 2, 2 },
                  { 3, 1 } };

    int N = A.GetLength(0);

    // Function Call
    longestSubSequence(A, N);
  }
}

// This code is contributed by decode2207.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to find the length of the
// longest subsequence of pairs whose first
// element is increasing and second is decreasing
function longestSubSequence(A, N) {
    // dp[i]: Stores the longest
    // subsequence upto i
    let dp = new Array(N);
    for (let i = 0; i < N; i++) {

        // Base case
        dp[i] = 1;

        for (let j = 0; j < i; j++) {

            // When the conditions hold
            if (A[j][0] < A[i][0]
                && A[j][1] > A[i][1]) {

                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
    }

    // Finally, print the required answer
    document.write(dp[N - 1] + "<br>");
}

// Driver Code

// Given Input
let A = [[1, 2],
[2, 2],
[3, 1]];

let N = A.length;

// Function Call
longestSubSequence(A, N);

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)***