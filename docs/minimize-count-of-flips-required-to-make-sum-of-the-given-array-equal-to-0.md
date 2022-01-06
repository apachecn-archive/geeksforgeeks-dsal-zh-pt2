# 最小化使给定数组的和等于 0 所需的翻转次数

> 原文:[https://www . geeksforgeeks . org/最小化翻转次数-要求给定数组的总和等于 0/](https://www.geeksforgeeks.org/minimize-count-of-flips-required-to-make-sum-of-the-given-array-equal-to-0/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是最小化需要乘以 **-1** 的元素个数，使得数组元素的[和为 **0** 。如果无法求和 **0** ，则打印**-1”**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) 

**示例:**

> **输入:** arr[] = {2，3，1，4}
> **输出:** 2
> **解释:**
> 将 arr[0]乘以-1。因此，数组修改为{-2，3，1，4}。
> 将 arr[1]乘以-1。因此，数组修改为{-2，-3，1，4}
> 因此，修改后的数组之和为 0，所需的最小运算为 2。
> 
> **输入:** arr[] = {2}
> **输出:** -1。

**天真方法:**最简单的方法是[把数组以各种可能的方式分成两个子集](https://www.geeksforgeeks.org/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum/)。对于每个除法，检查它们的子集和之差是否为 **0** 。如果发现为 **0** ，则结果为较小子集的长度。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决问题:

*   要使所有数组元素的和等于 **0** ，将给定的数组元素分成两个和相等的子集。
*   从给定数组的所有可能子集中，选择大小最小的子集。
*   如果给定数组的和为奇数，则没有子集可以使和为 **0** ，因此返回 **-1**
*   否则，尝试数组所有可能的子集和，检查子集和是否等于**和/2** 。其中**和**是数组所有元素的和。
*   **dp[]** 的递推关系为:

> **dp(i，j) = min (dp(i+1，j–arr[I]]+1)，dp(i+1，j))**
> 其中
> 
> **dp (i，j)** 表示使用具有索引[i，N-1]的元素使和 j 等于 0 的最小运算。
> **j** 代表当前的总和。
> **i** 代表当前指数。

*   使用上述循环，打印 **dp(0，sum/2)** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Initialize dp[][]
int dp[2001][2001];

// Function to find the minimum number
// of operations to make sum of A[] 0
int solve(vector<int>& A, int i,
          int sum, int N)
{
    // Initialize answer
    int res = 2001;

    // Base case
    if (sum < 0 or (i == N and sum != 0)) {
        return 2001;
    }

    // Otherwise, return 0
    if (sum == 0 or i >= N) {
        return dp[i][sum] = 0;
    }

    // Pre-computed subproblem
    if (dp[i][sum] != -1) {
        return dp[i][sum];
    }

    // Recurrence relation for finding
    // the minimum of the sum of subsets
    res = min(solve(A, i + 1, sum - A[i], N) + 1,
              solve(A, i + 1, sum, N));

    // Return the result
    return dp[i][sum] = res;
}

// Function to find the minimum number
// of elements required to be flipped
// to amke sum the array equal to 0
void minOp(vector<int>& A, int N)
{
    int sum = 0;

    // Find the sum of array
    for (auto it : A) {
        sum += it;
    }

    if (sum % 2 == 0) {

        // Initialise dp[][]  with -1
        memset(dp, -1, sizeof(dp));

        int ans = solve(A, 0, sum / 2, N);

        // No solution exists
        if (ans < 0 || ans > N) {
            cout << "-1" << endl;
        }

        // Otherwise
        else {
            cout << ans << endl;
        }
    }

    // If sum is odd, no
    // subset is possible
    else {
        cout << "-1" << endl;
    }
}

// Driver Code
int main()
{
    vector<int> A = { 2, 3, 1, 4 };
    int N = A.size();

    // Function Call
    minOp(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Initialize dp[][]
static int [][]dp = new int[2001][2001];

// Function to find the minimum number
// of operations to make sum of A[] 0
static int solve(int []A, int i,
          int sum, int N)
{

    // Initialize answer
    int res = 2001;

    // Base case
    if (sum < 0 || (i == N && sum != 0))
    {
        return 2001;
    }

    // Otherwise, return 0
    if (sum == 0 || i >= N)
    {
        return dp[i][sum] = 0;
    }

    // Pre-computed subproblem
    if (dp[i][sum] != -1)
    {
        return dp[i][sum];
    }

    // Recurrence relation for finding
    // the minimum of the sum of subsets
    res = Math.min(solve(A, i + 1, sum - A[i], N) + 1,
              solve(A, i + 1, sum, N));

    // Return the result
    return dp[i][sum] = res;
}

// Function to find the minimum number
// of elements required to be flipped
// to amke sum the array equal to 0
static void minOp(int []A, int N)
{
    int sum = 0;

    // Find the sum of array
    for (int it : A)
    {
        sum += it;
    }

    if (sum % 2 == 0)
    {

        // Initialise dp[][]  with -1
        for(int i = 0; i < 2001; i++)
        {
            for (int j = 0; j < 2001; j++)
            {
                dp[i][j] = -1;
            }
        }

        int ans = solve(A, 0, sum / 2, N);

        // No solution exists
        if (ans < 0 || ans > N)
        {
            System.out.print("-1" +"\n");
        }

        // Otherwise
        else
        {
            System.out.print(ans +"\n");
        }
    }

    // If sum is odd, no
    // subset is possible
    else
    {
        System.out.print("-1" +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int []A = { 2, 3, 1, 4 };
    int N = A.length;

    // Function Call
    minOp(A, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Initialize dp[][]
dp = [[-1 for i in range(2001)] for j in range(2001)]

# Function to find the minimum number
# of operations to make sum of A[] 0
def solve(A, i, sum, N):

    # Initialize answer
    res = 2001

    # Base case
    if (sum < 0 or (i == N and sum != 0)):
        return 2001

    # Otherwise, return 0
    if (sum == 0 or i >= N):
        dp[i][sum] = 0
        return 0

    # Pre-computed subproblem
    if (dp[i][sum] != -1):
        return dp[i][sum]

    # Recurrence relation for finding
    # the minimum of the sum of subsets
    res = min(solve(A, i + 1, sum - A[i], N) + 1,
              solve(A, i + 1, sum, N))

    # Return the result
    dp[i][sum] = res
    return res

# Function to find the minimum number
# of elements required to be flipped
# to amke sum the array equal to 0
def minOp(A, N):
    sum = 0

    # Find the sum of array
    for it in A:
        sum += it   
    if (sum % 2 == 0):

        # Initialise dp[][]  with -1
        dp = [[-1 for i in range(2001)] for j in range(2001)]
        ans = solve(A, 0, sum // 2, N)

        # No solution exists
        if (ans < 0 or ans > N):
            print("-1")

        # Otherwise
        else:
            print(ans)

    # If sum is odd, no
    # subset is possible
    else:
        print(-1)

# Driver Code
A = [ 2, 3, 1, 4 ]
N = len(A)

# Function Call
minOp(A, N)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

// Initialize [,]dp
static int [,]dp = new int[2001,2001];

// Function to find the minimum number
// of operations to make sum of []A 0
static int solve(int []A, int i,
          int sum, int N)
{

    // Initialize answer
    int res = 2001;

    // Base case
    if (sum < 0 || (i == N && sum != 0))
    {
        return 2001;
    }

    // Otherwise, return 0
    if (sum == 0 || i >= N)
    {
        return dp[i, sum] = 0;
    }

    // Pre-computed subproblem
    if (dp[i, sum] != -1)
    {
        return dp[i, sum];
    }

    // Recurrence relation for finding
    // the minimum of the sum of subsets
    res = Math.Min(solve(A, i + 1, sum - A[i], N) + 1,
              solve(A, i + 1, sum, N));

    // Return the result
    return dp[i, sum] = res;
}

// Function to find the minimum number
// of elements required to be flipped
// to amke sum the array equal to 0
static void minOp(int []A, int N)
{
    int sum = 0;

    // Find the sum of array
    foreach (int it in A)
    {
        sum += it;
    }

    if (sum % 2 == 0)
    {

        // Initialise [,]dp  with -1
        for(int i = 0; i < 2001; i++)
        {
            for (int j = 0; j < 2001; j++)
            {
                dp[i, j] = -1;
            }
        }

        int ans = solve(A, 0, sum / 2, N);

        // No solution exists
        if (ans < 0 || ans > N)
        {
            Console.Write("-1" +"\n");
        }

        // Otherwise
        else
        {
            Console.Write(ans +"\n");
        }
    }

    // If sum is odd, no
    // subset is possible
    else
    {
        Console.Write("-1" +"\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 3, 1, 4 };
    int N = A.Length;

    // Function Call
    minOp(A, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Initialize dp[][]
let dp= [];
for(var i=0; i<2001; i++) {
    dp[i] = [];
    for(var j=0; j<2001; j++) {
        dp[i][j] = -1;
    }
}

// Function to find the minimum number
// of operations to make sum of A[] 0
function solve( A, i, sum, N){
    // Initialize answer
    let res = 2001;

    // Base case
    if (sum < 0 || (i == N && sum != 0)) {
        return 2001;
    }

    // Otherwise, return 0
    if (sum == 0 || i >= N) {
        dp[i][sum] = 0;
        return dp[i][sum];
    }

    // Pre-computed subproblem
    if (dp[i][sum] != -1) {
        return dp[i][sum];
    }

    // Recurrence relation for finding
    // the minimum of the sum of subsets
    res = Math.min(solve(A, i + 1, sum - A[i], N) + 1,
              solve(A, i + 1, sum, N));

    // Return the result
    dp[i][sum] = res;
    return dp[i][sum];
}

// Function to find the minimum number
// of elements required to be flipped
// to amke sum the array equal to 0
function minOp(A, N){
    let sum = 0;

    // Find the sum of array
    for (let i =0; i< A.length; i++) {
        sum += A[i];
    }
    if (sum % 2 == 0) {

        let dp= [];
        for(var i=0; i<2001; i++) {
            dp[i] = [];
            for(var j=0; j<2001; j++) {
                dp[i][j] = -1;
            }
        }

        let ans = solve(A, 0, Math.floor(sum / 2), N);

        // No solution exists
        if (ans < 0 || ans > N) {
            document.write("-1 <br>");
        }

        // Otherwise
        else {
            document.write(ans,"<br>");
        }
    }

    // If sum is odd, no
    // subset is possible
    else {
         document.write("-1 <br>");
    }
}

// Driver Code
let A = [ 2, 3, 1, 4 ];
let N = A.length;
// Function Call
minOp(A, N);
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(S*N)，其中 S 是给定数组的和。*
***辅助空间:** O(S*N)*