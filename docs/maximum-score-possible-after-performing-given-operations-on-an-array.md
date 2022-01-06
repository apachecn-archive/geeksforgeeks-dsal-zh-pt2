# 对数组执行给定操作后的最大可能得分

> 原文:[https://www . geeksforgeeks . org/在阵列上执行给定操作后的最大可能得分/](https://www.geeksforgeeks.org/maximum-score-possible-after-performing-given-operations-on-an-array/)

给定一个大小为 **N** 的数组 **A** ，任务是找到这个数组的最大可能得分。通过对数组 **N** 次
执行以下操作来计算数组的分数

1.  如果操作是奇数，分数将按当前数组所有元素的总和递增。

2.  如果操作是偶数编号的，分数将减去当前数组中所有元素的总和。

3.  每次操作后，移除剩余数组的第一个或最后一个元素。

**例:**

> **输入:** A = {1，2，3，4，2，6}
> **输出:** 13
> **说明:**
> 最优操作为:
> 1。行动 1 很奇怪。
> - >所以把数组的和加到分数上:分数= 0 + 18 = 18
> - >从最后一个去掉 6，
> - >新数组 A = [1，2，3，4，2]
> 2。行动 2 是偶数。
> - >所以从得分中减去数组的和:得分= 18–12 = 6
> ->从最后一个中去掉 2，
> - >新数组 A = [1，2，3，4]
> 3。行动 1 很奇怪。
> - >所以把数组的和加到分数上:分数= 6 + 10 = 16
> - >从最后一个中去掉 4，
> - >新数组 A = [1，2，3]
> 4。行动 4 是偶数。
> - >所以从分数中减去数组的和:Score = 16–6 = 10
> ->从开始去掉 1，
> - >新数组 A = [2，3]
> 5。5 号行动很奇怪。
> - >所以把数组的和加到分数上:Score = 10 + 5 = 15
> - >从最后一个去掉 3，
> - >新数组 A = [2]
> 6。行动 6 是偶数。
> - >所以从分数中减去数组的和:Score = 15–2 = 13
> ->先去掉 2，
> - >新数组 A = []
> 数组是空的，所以不能再做进一步的操作。
> **输入:** A = [5，2，2，8，1，16，7，9，12，4]
> **输出:** 50

**天真的做法**T2】

1.  在每个操作中，我们必须移除最左边或最右边的元素。一个简单的方法是考虑所有可能的方法来移除元素，并为每个分支计算分数，并从所有分支中找到最大分数。这可以简单地使用[递归](https://www.geeksforgeeks.org/recursion/)来完成。

2.  我们在每个步骤中需要保留的信息是
    *   剩下的数组**【l，r】**，其中 l 代表最左边的索引，r 代表最右边的，
    *   操作号，以及
    *   当前分数。
3.  为了在每个递归步骤中从[l，r]最佳地计算任何数组的和，我们将保留一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
    使用前缀和数组，来自[l，r]的新和可以在 O(1)中计算为:

> 总和(l，r) =前缀 _ 总和[r]–前缀 _ 总和[l-1]

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum
// score after given operations

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// maximum score recursively
int maxScore(
    int l, int r,
    int prefix_sum[],
    int num)
{

    // Base case
    if (l > r)
        return 0;

    // Sum of array in range (l, r)
    int current_sum
        = prefix_sum[r]
          - (l - 1 >= 0
                 ? prefix_sum[l - 1]
                 : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, by removing
    // leftmost and rightmost element
    // and selecting the maximum value
    return current_sum
           + max(
                 maxScore(
                     l + 1, r,
                     prefix_sum,
                     num + 1),
                 maxScore(
                     l, r - 1,
                     prefix_sum,
                     num + 1));
}

// Function to find the max score
int findMaxScore(int a[], int n)
{
    // Prefix sum array
    int prefix_sum[n] = { 0 };

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (int i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    return maxScore(0, n - 1,
                    prefix_sum, 1);
}

// Driver code
int main()
{
    int n = 6;
    int A[n] = { 1, 2, 3, 4, 2, 6 };

    cout << findMaxScore(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// score after given operations
import java.util.*;

class GFG{

// Function to calculate
// maximum score recursively
static int maxScore(
    int l, int r,
    int prefix_sum[],
    int num)
{

    // Base case
    if (l > r)
        return 0;

    // Sum of array in range (l, r)
    int current_sum
        = prefix_sum[r]
        - (l - 1 >= 0
                ? prefix_sum[l - 1]
                : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, by removing
    // leftmost and rightmost element
    // and selecting the maximum value
    return current_sum
        + Math.max(maxScore(l + 1, r,
                            prefix_sum,
                            num + 1),
                    maxScore(l, r - 1,
                            prefix_sum,
                            num + 1));
}

// Function to find the max score
static int findMaxScore(int a[], int n)
{
    // Prefix sum array
    int prefix_sum[] = new int[n];

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (int i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    return maxScore(0, n - 1,
                    prefix_sum, 1);
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    int A[] = { 1, 2, 3, 4, 2, 6 };

    System.out.print(findMaxScore(A, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# score after given operations

# Function to calculate maximum
# score recursively
def maxScore(l, r, prefix_sum, num):

    # Base case
    if (l > r):
        return 0;

    # Sum of array in range (l, r)
    if((l - 1) >= 0):
        current_sum = (prefix_sum[r] -
                       prefix_sum[l - 1])
    else:
        current_sum = prefix_sum[r] - 0

    # If the operation is even-numbered
    # the score is decremented
    if (num % 2 == 0):
        current_sum *= -1;

    # Exploring all paths, by removing
    # leftmost and rightmost element
    # and selecting the maximum value
    return current_sum + max(maxScore(l + 1, r,
                                      prefix_sum,
                                      num + 1),
                             maxScore(l, r - 1,
                                      prefix_sum,
                                      num + 1));

# Function to find the max score
def findMaxScore(a, n):

    # Prefix sum array
    prefix_sum = [0] * n

    prefix_sum[0] = a[0]

    # Calculating prefix_sum
    for i in range(1, n):
        prefix_sum[i] = prefix_sum[i - 1] + a[i];

    return maxScore(0, n - 1, prefix_sum, 1);

# Driver code
n = 6;
A = [ 1, 2, 3, 4, 2, 6 ]
ans = findMaxScore(A, n)

print(ans)

# This code is contributed by SoumikMondal
```

## C#

```
// C# program to find the maximum
// score after given operations
using System;

class GFG{

// Function to calculate
// maximum score recursively
static int maxScore(
    int l, int r,
    int []prefix_sum,
    int num)
{

    // Base case
    if (l > r)
        return 0;

    // Sum of array in range (l, r)
    int current_sum
        = prefix_sum[r]
        - (l - 1 >= 0
                ? prefix_sum[l - 1]
                : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, by removing
    // leftmost and rightmost element
    // and selecting the maximum value
    return current_sum
        + Math.Max(maxScore(l + 1, r,
                            prefix_sum,
                            num + 1),
                    maxScore(l, r - 1,
                            prefix_sum,
                            num + 1));
}

// Function to find the max score
static int findMaxScore(int []a, int n)
{
    // Prefix sum array
    int []prefix_sum = new int[n];

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (int i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    return maxScore(0, n - 1,
                    prefix_sum, 1);
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;
    int []A = { 1, 2, 3, 4, 2, 6 };

    Console.Write(findMaxScore(A, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum
// score after given operations

// Function to calculate
// maximum score recursively
function maxScore(l, r, prefix_sum, num)
{

    // Base case
    if (l > r)
        return 0;

    // Sum of array in range (l, r)
    let current_sum
        = prefix_sum[r]
        - (l - 1 >= 0
                ? prefix_sum[l - 1]
                : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, by removing
    // leftmost and rightmost element
    // and selecting the maximum value
    return current_sum
        + Math.max(
                maxScore(
                    l + 1, r,
                    prefix_sum,
                    num + 1),
                maxScore(
                    l, r - 1,
                    prefix_sum,
                    num + 1));
}

// Function to find the max score
function findMaxScore(a, n)
{
    // Prefix sum array
    let prefix_sum = new Uint8Array(n);

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (let i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    return maxScore(0, n - 1,
                    prefix_sum, 1);
}

// Driver code

    let n = 6;
    let A = [ 1, 2, 3, 4, 2, 6 ];

    document.write(findMaxScore(A, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(2 <sup>N</sup> )*
**高效进场**

*   在前面的方法中，可以观察到我们多次计算相同的子问题，即它遵循[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)的性质。所以我们可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决问题

*   在上述递归解决方案中，我们只需要使用 [dp 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)添加[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)。各州将是:

> **DP 表状态= dp[l][r][num]**
> ，其中 **l** 和 **r** 代表当前数组的端点， **num** 代表操作号。

下面是递归代码的记忆方法的实现:

## C++

```
// C++ program to find the maximum
// Score after given operations

#include <bits/stdc++.h>
using namespace std;

// Memoizing by the use of a table
int dp[100][100][100];

// Function to calculate maximum score
int MaximumScoreDP(int l, int r,
                   int prefix_sum[],
                   int num)
{
    // Bse case
    if (l > r)
        return 0;

    // If the same state has
    // already been computed
    if (dp[l][r][num] != -1)
        return dp[l][r][num];

    // Sum of array in range (l, r)
    int current_sum
        = prefix_sum[r]
          - (l - 1 >= 0
                 ? prefix_sum[l - 1]
                 : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, and storing
    // maximum value in DP table to avoid
    // further repetitive recursive calls
    dp[l][r][num] = current_sum
                    + max(
                          MaximumScoreDP(
                              l + 1, r,
                              prefix_sum,
                              num + 1),
                          MaximumScoreDP(
                              l, r - 1,
                              prefix_sum,
                              num + 1));

    return dp[l][r][num];
}

// Function to find the max score
int findMaxScore(int a[], int n)
{
    // Prefix sum array
    int prefix_sum[n] = { 0 };

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (int i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    // Initialising the DP table,
    // -1 represents the subproblem
    // hasn't been solved yet
    memset(dp, -1, sizeof(dp));

    return MaximumScoreDP(
        0, n - 1,
        prefix_sum, 1);
}

// Driver code
int main()
{
    int n = 6;
    int A[n] = { 1, 2, 3, 4, 2, 6 };

    cout << findMaxScore(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// Score after given operations

class GFG{

// Memoizing by the use of a table
static int [][][]dp = new int[100][100][100];

// Function to calculate maximum score
static int MaximumScoreDP(int l, int r,
                   int prefix_sum[],
                   int num)
{
    // Bse case
    if (l > r)
        return 0;

    // If the same state has
    // already been computed
    if (dp[l][r][num] != -1)
        return dp[l][r][num];

    // Sum of array in range (l, r)
    int current_sum
        = prefix_sum[r]
          - (l - 1 >= 0
                 ? prefix_sum[l - 1]
                 : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, and storing
    // maximum value in DP table to avoid
    // further repetitive recursive calls
    dp[l][r][num] = current_sum
                    + Math.max(
                          MaximumScoreDP(
                              l + 1, r,
                              prefix_sum,
                              num + 1),
                          MaximumScoreDP(
                              l, r - 1,
                              prefix_sum,
                              num + 1));

    return dp[l][r][num];
}

// Function to find the max score
static int findMaxScore(int a[], int n)
{
    // Prefix sum array
    int []prefix_sum = new int[n];

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (int i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    // Initialising the DP table,
    // -1 represents the subproblem
    // hasn't been solved yet
    for(int i = 0;i<100;i++){
       for(int j = 0;j<100;j++){
           for(int l=0;l<100;l++)
           dp[i][j][l]=-1;
       }
   }

    return MaximumScoreDP(
        0, n - 1,
        prefix_sum, 1);
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    int A[] = { 1, 2, 3, 4, 2, 6 };

    System.out.print(findMaxScore(A, n));
}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# python3 program to find the maximum
# Score after given operations

# Memoizing by the use of a table
dp = [[[-1 for x in range(100)]for y in range(100)]for z in range(100)]

# Function to calculate maximum score

def MaximumScoreDP(l, r, prefix_sum,
                   num):

    # Bse case
    if (l > r):
        return 0

    # If the same state has
    # already been computed
    if (dp[l][r][num] != -1):
        return dp[l][r][num]

    # Sum of array in range (l, r)
    current_sum = prefix_sum[r]
    if (l - 1 >= 0):
        current_sum -= prefix_sum[l - 1]

    # If the operation is even-numbered
    # the score is decremented
    if (num % 2 == 0):
        current_sum *= -1

    # Exploring all paths, and storing
    # maximum value in DP table to avoid
    # further repetitive recursive calls
    dp[l][r][num] = (current_sum
                     + max(
                         MaximumScoreDP(
                             l + 1, r,
                             prefix_sum,
                             num + 1),
                         MaximumScoreDP(
                             l, r - 1,
                             prefix_sum,
                             num + 1)))

    return dp[l][r][num]

# Function to find the max score
def findMaxScore(a, n):

    # Prefix sum array
    prefix_sum = [0]*n

    prefix_sum[0] = a[0]

    # Calculating prefix_sum
    for i in range(1, n):
        prefix_sum[i] = prefix_sum[i - 1] + a[i]

    # Initialising the DP table,
    # -1 represents the subproblem
    # hasn't been solved yet
    global dp

    return MaximumScoreDP(
        0, n - 1,
        prefix_sum, 1)

# Driver code
if __name__ == "__main__":

    n = 6
    A = [1, 2, 3, 4, 2, 6]

    print(findMaxScore(A, n))
```

## C#

```
// C# program to find the maximum
// Score after given operations

using System;

public class GFG{

// Memoizing by the use of a table
static int [,,]dp = new int[100,100,100];

// Function to calculate maximum score
static int MaximumScoreDP(int l, int r,
                   int []prefix_sum,
                   int num)
{
    // Bse case
    if (l > r)
        return 0;

    // If the same state has
    // already been computed
    if (dp[l,r,num] != -1)
        return dp[l,r,num];

    // Sum of array in range (l, r)
    int current_sum
        = prefix_sum[r]
          - (l - 1 >= 0
                 ? prefix_sum[l - 1]
                 : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, and storing
    // maximum value in DP table to avoid
    // further repetitive recursive calls
    dp[l,r,num] = current_sum
                    + Math.Max(
                          MaximumScoreDP(
                              l + 1, r,
                              prefix_sum,
                              num + 1),
                          MaximumScoreDP(
                              l, r - 1,
                              prefix_sum,
                              num + 1));

    return dp[l,r,num];
}

// Function to find the max score
static int findMaxScore(int []a, int n)
{
    // Prefix sum array
    int []prefix_sum = new int[n];

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (int i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    // Initialising the DP table,
    // -1 represents the subproblem
    // hasn't been solved yet
    for(int i = 0;i<100;i++){
       for(int j = 0;j<100;j++){
           for(int l=0;l<100;l++)
           dp[i,j,l]=-1;
       }
   }

    return MaximumScoreDP(
        0, n - 1,
        prefix_sum, 1);
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;
    int []A = { 1, 2, 3, 4, 2, 6 };

    Console.Write(findMaxScore(A, n));
}
}

// This code contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum
// Score after given operations

// Memoizing by the use of a table
let dp = new Array(100);
// Initialising the DP table,
    // -1 represents the subproblem
    // hasn't been solved yet
for(let i=0;i<100;i++)
{
    dp[i]=new Array(100);
    for(let j=0;j<100;j++)
    {
        dp[i][j]=new Array(100);
        for(let k=0;k<100;k++)
        {
            dp[i][j][k]=-1;
        }
    }
}

// Function to calculate maximum score
function MaximumScoreDP(l,r,prefix_sum,num)
{
    // Bse case
    if (l > r)
        return 0;

    // If the same state has
    // already been computed
    if (dp[l][r][num] != -1)
        return dp[l][r][num];

    // Sum of array in range (l, r)
    let current_sum
        = prefix_sum[r]
          - (l - 1 >= 0
                 ? prefix_sum[l - 1]
                 : 0);

    // If the operation is even-numbered
    // the score is decremented
    if (num % 2 == 0)
        current_sum *= -1;

    // Exploring all paths, and storing
    // maximum value in DP table to avoid
    // further repetitive recursive calls
    dp[l][r][num] = current_sum
                    + Math.max(
                          MaximumScoreDP(
                              l + 1, r,
                              prefix_sum,
                              num + 1),
                          MaximumScoreDP(
                              l, r - 1,
                              prefix_sum,
                              num + 1));

    return dp[l][r][num];
}

// Function to find the max score
function findMaxScore(a,n)
{
    // Prefix sum array
    let prefix_sum = new Array(n);

    prefix_sum[0] = a[0];

    // Calculating prefix_sum
    for (let i = 1; i < n; i++) {
        prefix_sum[i]
            = prefix_sum[i - 1] + a[i];
    }

    // Initialising the DP table,
    // -1 represents the subproblem
    // hasn't been solved yet

    return MaximumScoreDP(
        0, n - 1,
        prefix_sum, 1);
}

// Driver code
let n = 6;
let A=[1, 2, 3, 4, 2, 6 ];
document.write(findMaxScore(A, n));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N <sup>3</sup> )*