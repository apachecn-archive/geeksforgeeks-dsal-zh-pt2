# 从给定数组中最多取 K 个元素，找到可被 D 整除的最大子集和

> 原文:[https://www . geesforgeks . org/find-最大子集-和-被 d 整除-从给定数组中最多取 k 个元素/](https://www.geeksforgeeks.org/find-maximum-subset-sum-divisible-by-d-by-taking-at-most-k-elements-from-given-array/)

给定一个大小为 **N** 的数组**A【】**，以及两个数字 **K** 和 **D** ，任务是通过从 **A** 中提取最多 **K** 个元素来计算可被 **D** 整除的最大子集和。

**示例:**

> **输入:** A={11，5，5，1，18}，N=5，K=3，D=7
> **输出:**
> 28
> **解释:**
> 子集{5，5，18}给出了可被 7 整除的最大和=(5+5+18)=28，并且还包含 atmost 3 元素
> 
> **输入:** A={7，7，7，7，7}，N=5，K=2，D = 7
> T3】输出:T5】14

**朴素方法:**朴素方法是[生成 **A** 的所有子集](https://www.geeksforgeeks.org/power-set/)(使用位屏蔽)，对于每个子集，计算和，检查子集的长度是否不大于 **K** ，和是否可被 **D** 整除，并计算其中的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum sum possible by taking at
// most K elements that is divisibly by D
int maximumSum(vector<int> A, int N, int K, int D)
{
    // variable to store final answer
    int ans = 0;
    // Traverse all subsets
    for (int i = 0; i < (1 << N); i++) {
        int sum = 0;
        int c = 0;
        for (int j = 0; j < N; j++) {
            if (i >> j & 1) {
                sum += A[j];
                c++;
            }
        }
        // Update ans if necessary
        // conditions are satisfied
        if (sum % D == 0 && c <= K)
            ans = max(ans, sum);
    }
    return ans;
}
// Driver code
int main()
{
    // Input
    int N = 5, K = 3, D = 7;
    vector<int> A = { 1, 11, 5, 5, 18 };

    // Function call
    cout << maximumSum(A, N, K, D) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate maximum sum
// possible by taking at most K
// elements that is divisibly by D
static int maximumSum(int[] A, int N,
                      int K, int D)
{

    // Variable to store final answer
    int ans = 0;

    // Traverse all subsets
    for(int i = 0; i < (1 << N); i++)
    {
        int sum = 0;
        int c = 0;
        for(int j = 0; j < N; j++)
        {
            if ((i >> j & 1) != 0)
            {
                sum += A[j];
                c++;
            }
        }

        // Update ans if necessary
        // conditions are satisfied
        if (sum % D == 0 && c <= K)
            ans = Math.max(ans, sum);
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 5, K = 3, D = 7;
    int[] A = { 1, 11, 5, 5, 18 };

    // Function call
    System.out.print(maximumSum(A, N, K, D));
}   
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate maximum sum
# possible by taking at most K elements
# that is divisibly by D
def maximumSum(A, N, K, D):

    # Variable to store final answer
    ans = 0

    # Traverse all subsets
    for i in range((1 << N)):
        sum = 0
        c = 0

        for j in range(N):
            if (i >> j & 1):
                sum += A[j]
                c += 1

        # Update ans if necessary
        # conditions are satisfied
        if (sum % D == 0 and c <= K):
            ans = max(ans, sum)

    return ans

# Driver code
if __name__ == '__main__':

    # Input
    N = 5
    K = 3
    D = 7
    A = [ 1, 11, 5, 5, 18 ]

    # Function call
    print(maximumSum(A, N, K, D))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate maximum sum possible
// by taking at most K elements that is divisibly by D
static int maximumSum(List<int> A, int N,
                           int K, int D)
{

    // Variable to store final answer
    int ans = 0;

    // Traverse all subsets
    for(int i = 0; i < (1 << N); i++)
    {
        int sum = 0;
        int c = 0;
        for(int j = 0; j < N; j++)
        {
            if ((i >> j & 1) != 0)
            {
                sum += A[j];
                c++;
            }
        }

        // Update ans if necessary
        // conditions are satisfied
        if (sum % D == 0 && c <= K)
            ans = Math.Max(ans, sum);
    }
    return ans;
}

// Driver code
public static void Main()
{

    // Input
    int N = 5, K = 3, D = 7;
    List<int> A = new List<int>(){ 1, 11, 5, 5, 18 };

    // Function call
    Console.Write(maximumSum(A, N, K, D));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate maximum sum possible by taking at
// most K elements that is divisibly by D
function maximumSum(A, N, K, D) {
    // variable to store final answer
    let ans = 0;
    // Traverse all subsets
    for (let i = 0; i < (1 << N); i++) {
        let sum = 0;
        let c = 0;
        for (let j = 0; j < N; j++) {
            if (i >> j & 1) {
                sum += A[j];
                c++;
            }
        }
        // Update ans if necessary
        // conditions are satisfied
        if (sum % D == 0 && c <= K)
            ans = Math.max(ans, sum);
    }
    return ans;
}
// Driver code

// Input
let N = 5, K = 3, D = 7;
let A = [1, 11, 5, 5, 18];

// Function call
document.write(maximumSum(A, N, K, D) + "<br>");

</script>
```

**Output:** 

```
28
```

***时间复杂度:**O(N . 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**这个问题可以借助[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决，使用 [3D dp 数组](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)，其中 **dp[i][j][p]** 存储最大可能和，如果 **j** 元素被取到带有索引的**且其模 **D** 为 **p** 。按照以下步骤解决问题:**

1.  创建大小为(**N+1)x(K+1)x(D)**的 3D 数组 DP[][][][]，并用-1 初始化它。
2.  从 **1** 迭代到 **N** ，对于每个当前指标 **i** ，执行以下操作:
    1.  将两个变量**元素**和**模块**初始化为**A【I-1】**和**A【I-1】% D**。
    2.  将 **dp[i-1]** 复制到 **dp[i]。**
    3.  从 **1** 迭代到 **K** ，对于每个当前指标 **j** ，执行以下操作:
        1.  将 **dp[i][j][mod]** 更新为 **dp[i][j][mod]** 和**元素的最大值。**
        2.  从 **0** 迭代到 **D-1** ，对于每个当前索引 **p** ，执行以下操作:
            1.  如果 **dp[i-1][j-1][p]** 不等于-1，更新 **dp[i][j][(p+mod)%D]** 为 **dp[i][j][(p+mod)%D]** 和**DP[I-1][j-1][p]+元素的最大值。**
3.  如果 **dp[N][K][0]** 为-1，则答案为 0。
4.  否则，答案是 **dp[N][K][0]。**

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
int maximumSum(vector<int> A, int N, int K, int D)
{
    // Dp vector
    vector<vector<vector<int> > > dp(
        N + 1, vector<vector<int> >(
                   K + 1, vector<int>(D + 1, -1)));
    for (int i = 1; i <= N; i++) {
        // current element
        int element = A[i - 1];
        // current element modulo D
        int mod = A[i - 1] % D;
        // copy previous state
        dp[i] = dp[i - 1];
        for (int j = 1; j <= K; j++) {
            // Transitions
            dp[i][j][mod] = max(dp[i][j][mod], element);
            for (int p = 0; p < D; p++) {
                if (dp[i - 1][j - 1][p] != -1) {
                    dp[i][j][(p + mod) % D] = max(
                        dp[i][j][(p + mod) % D],
                        dp[i - 1][j - 1][p] + element);
                }
            }
        }
    }
    // return answer
    if (dp[N][K][0] == -1)
        return 0;
    return dp[N][K][0];
}
// Driver code
int main()
{
    // Input
    int N = 5, K = 3, D = 7;
    vector<int> A = { 1, 11, 5, 5, 18 };

    // Function call
    cout << maximumSum(A, N, K, D) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

static int maximumSum(int[] A, int N, int K, int D)
{

    // Dp vector
    int[][][] dp = new int[N+1][K+1][D+1];

    for(int i = 0; i < N + 1; i++)
    {
        for(int j = 0; j < K + 1; j++)
        {
            for(int k = 0; k < D + 1; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }

    for (int i = 1; i <= N; i++)
    {

        // current element
        int element = A[i - 1];

        // current element modulo D
        int mod = A[i - 1] % D;

        // copy previous state
        dp[i] = dp[i - 1];
        for (int j = 1; j <= K; j++)
        {

            // Transitions
            dp[i][j][mod] = Math.max(dp[i][j][mod], element);
            for (int p = 0; p < D; p++) {
                if (dp[i - 1][j - 1][p] != -1) {
                    dp[i][j][(p + mod) % D] = Math.max(
                        dp[i][j][(p + mod) % D],
                        dp[i - 1][j - 1][p] + element);
                }
            }
        }
    }

    // return answer
    if (dp[N][K][0] == -1)
        return 0;
    return dp[N][K][0];
}

// Driver Code
public static void main(String[] args)
{
    // Input
    int N = 5, K = 3, D = 7;
    int[] A = { 1, 11, 5, 5, 18 };

    // Function call
    System.out.print(maximumSum(A, N, K, D));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

**Output:** 

```
28
```

***时间复杂度:** O(NKD)*
***辅助空间:** O(NKD)*