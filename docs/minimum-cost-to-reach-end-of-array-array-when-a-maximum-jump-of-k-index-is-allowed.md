# 当允许 K 个索引的最大跳跃时到达数组末尾的最小代价

> 原文:[https://www . geeksforgeeks . org/当允许 k 索引的最大跳跃时到达阵列末端的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-reach-end-of-array-array-when-a-maximum-jump-of-k-index-is-allowed/)

给定一个由 **N** 整数和一个整数 **K** 组成的数组 **arr[]** ，如果 **j ≤ i + k** ，则可以从一个索引 **i** 移动到任何其他的 **j** 。从一个指标 **i** 移动到另一个指标 **j** 的成本是**ABS(arr[I]–arr[j])**。最初，我们从索引 **0** 开始，我们需要到达最后一个索引，即**N–1**。任务是以尽可能低的成本达到最后一个指标。
**举例:**

> **输入:** arr[] = {10，30，40，50，20}，k = 3
> **输出:** 30
> 0 - > 1 - > 4
> 总成本将为:|10-30| + |30-20| = 30
> **输入:** arr[] = {40，10，20，70，80，10}，k = 4 【T10

**方法 1:** 这个问题可以用动态规划来解决。我们从索引 0 开始，可以访问从 i+1 到 i+k 的任何索引，因此所有路径的最小开销将存储在 dp[i]中。一旦我们到达 N-1，这将是我们的基本情况。使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)来记忆状态，这样我们就不需要再次访问状态来降低复杂性。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
// to reach the last index
int FindMinimumCost(int ind, int a[],
                    int n, int k, int dp[])
{

    // If we reach the last index
    if (ind == (n - 1))
        return 0;

    // Already visited state
    else if (dp[ind] != -1)
        return dp[ind];
    else {

        // Initially maximum
        int ans = INT_MAX;

        // Visit all possible reachable index
        for (int i = 1; i <= k; i++) {

            // If inside range
            if (ind + i < n)
                ans = min(ans, abs(a[ind + i] - a[ind])
                          + FindMinimumCost(ind + i, a,
                                             n, k, dp));

            // We cannot move any further
            else
                break;
        }

        // Memoize
        return dp[ind] = ans;
    }
}

// Driver Code
int main()
{
    int a[] = { 10, 30, 40, 50, 20 };
    int k = 3;
    int n = sizeof(a) / sizeof(a[0]);
    int dp[n];
    memset(dp, -1, sizeof dp);
    cout << FindMinimumCost(0, a, n, k, dp);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GfG
{

// Function to return the minimum cost
// to reach the last index
static int FindMinimumCost(int ind, int a[],
                        int n, int k, int dp[])
{

    // If we reach the last index
    if (ind == (n - 1))
        return 0;

    // Already visited state
    else if (dp[ind] != -1)
        return dp[ind];
    else {

        // Initially maximum
        int ans = Integer.MAX_VALUE;

        // Visit all possible reachable index
        for (int i = 1; i <= k; i++)
        {

            // If inside range
            if (ind + i < n)
                ans = Math.min(ans, Math.abs(a[ind + i] - a[ind]) +
                            FindMinimumCost(ind + i, a, n, k, dp));

            // We cannot move any further
            else
                break;
        }

        // Memoize
        return dp[ind] = ans;
    }
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 10, 30, 40, 50, 20 };
    int k = 3;
    int n = a.length;
    int dp[] = new int[n];
    Arrays.fill(dp, -1);
    System.out.println(FindMinimumCost(0, a, n, k, dp));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import sys

# Function to return the minimum cost
# to reach the last index
def FindMinimumCost(ind, a, n, k, dp):

    # If we reach the last index
    if (ind == (n - 1)):
        return 0

    # Already visited state
    elif (dp[ind] != -1):
        return dp[ind]
    else:

        # Initially maximum
        ans = sys.maxsize

        # Visit all possible reachable index
        for i in range(1, k + 1):

            # If inside range
            if (ind + i < n):
                ans = min(ans, abs(a[ind + i] - a[ind]) +
                      FindMinimumCost(ind + i, a, n, k, dp))

            # We cannot move any further
            else:
                break

        # Memoize
        dp[ind] = ans
        return ans

# Driver Code
if __name__ == '__main__':
    a = [10, 30, 40, 50, 20]
    k = 3
    n = len(a)
    dp = [-1 for i in range(n)]
    print(FindMinimumCost(0, a, n, k, dp))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GfG
{

    // Function to return the minimum cost
    // to reach the last index
    static int FindMinimumCost(int ind, int []a,
                            int n, int k, int []dp)
    {

        // If we reach the last index
        if (ind == (n - 1))
            return 0;

        // Already visited state
        else if (dp[ind] != -1)
            return dp[ind];

        else {

            // Initially maximum
            int ans = int.MaxValue;

            // Visit all possible reachable index
            for (int i = 1; i <= k; i++)
            {

                // If inside range
                if (ind + i < n)
                    ans = Math.Min(ans, Math.Abs(a[ind + i] - a[ind]) +
                                FindMinimumCost(ind + i, a, n, k, dp));

                // We cannot move any further
                else
                    break;
            }

            // Memoize
            return dp[ind] = ans;
        }
    }

    // Driver Code
    public static void Main()
    {
        int []a = { 10, 30, 40, 50, 20 };
        int k = 3;
        int n = a.Length;
        int []dp = new int[n];
        for(int i = 0; i < n ; i++)
            dp[i] = -1 ;

        Console.WriteLine(FindMinimumCost(0, a, n, k, dp));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum cost
// to reach the last index
function FindMinimumCost($ind, $a, $n, $k, $dp)
{

    // If we reach the last index
    if ($ind == ($n - 1))
        return 0;

    // Already visited state
    else if ($dp[$ind] != -1)
        return $dp[$ind];
    else
    {

        // Initially maximum
        $ans = PHP_INT_MAX;

        // Visit all possible reachable index
        for ($i = 1; $i <= $k; $i++)
        {

            // If inside range
            if ($ind + $i < $n)
                $ans = min($ans, abs($a[$ind + $i] - $a[$ind]) +
                     FindMinimumCost($ind + $i, $a, $n, $k, $dp));

            // We cannot move any further
            else
                break;
        }

        // Memoize
        return $dp[$ind] = $ans;
    }
}

// Driver Code
$a = array(10, 30, 40, 50, 20 );
$k = 3;
$n = sizeof($a);
$dp = array();
$dp = array_fill(0, $n, -1);
echo(FindMinimumCost(0, $a, $n, $k, $dp));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the minimum cost
    // to reach the last index
    function FindMinimumCost(ind , a , n , k , dp) {

        // If we reach the last index
        if (ind == (n - 1))
            return 0;

        // Already visited state
        else if (dp[ind] != -1)
            return dp[ind];
        else {

            // Initially maximum
            var ans = Number.MAX_VALUE;

            // Visit all possible reachable index
            for (var i = 1; i <= k; i++) {

                // If inside range
                if (ind + i < n)
                    ans = Math.min(ans, Math.abs(a[ind + i] - a[ind])
                    + FindMinimumCost(ind + i, a, n, k, dp));

                // We cannot move any further
                else
                    break;
            }

            // Memoize
            return dp[ind] = ans;
        }
    }

    // Driver Code

        var a = [ 10, 30, 40, 50, 20];
        var k = 3;
        var n = a.length;
        var dp = Array(n).fill(-1);

        document.write(FindMinimumCost(0, a, n, k, dp));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
30
```

**时间复杂度:** O(N * K)
**辅助空间:** O(N)
**途径 2:**
第二种途径也需要使用动态规划。这种方法基于贝尔曼·福特的单源最短路径 DP 解决方案。在贝尔曼的福特 SSSP 中，主要思想是通过在边上最小化来找到下一个顶点，我们可以像在数组的两个元素的 abs 值上最小化一样来找到下一个索引。
为了解决任何动力定位问题，我们首先猜测子问题的所有可能的解决方案并记忆它们，然后选择子问题的最佳解决方案。我们为问题
写 Recurrence:Recurrence:DP(j)= min { DP(I)+ABS(A[I]–A[j])}其中 I 在[0，N-1]中，j 在[i + 1，j + k + 1]中，k 是允许的跳跃次数。这也可以和 SSSP 的放松相提并论。我们将放松每一个可接近的指数。

> //基本情况
> 备忘[0]= 0；
> 为(i = 0 至 N-1)
> 为(j = i+1 至 i+k+1)
> memo[j] = min(memo[j]，memo[I]+ABS(A[I]–A[j])；

下面是自下而上方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>

using namespace std;

// Function for returning the min of two elements
int min(int a, int b) {
    return (a > b) ? b : a;
}

int minCostJumpsDP(vector <int> & A, int k) {
    // for calculating the number of elements
    int size = A.size();

    // Allocating Memo table and
    // initializing with INT_MAX
    vector <int> x(size, INT_MAX); 

    // Base case
    x[0] = 0;

    // For every element relax every reachable
    // element ie relax next k elements
    for (int i = 0; i < size; i++) {
        // reaching next k element
        for (int j = i + 1; j < i + k + 1; j++) {
            // Relaxing the element
            x[j] = min(x[j], x[i] + abs(A[i] - A[j]));
        }
    }

    // return the last element in the array
    return x[size - 1];
}

// Driver Code
int main()
{
    vector <int> input { 83, 26, 37, 35, 33, 35, 56 };
    cout << minCostJumpsDP(input, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function for returning the
// min of two elements
static int min(int a, int b)
{
    return (a > b) ? b : a;
}

static int minCostJumpsDP(int []A, int k)
{
    // for calculating the number of elements
    int size = A.length;

    // Allocating Memo table and
    // initializing with INT_MAX
    int []x = new int[size];
    Arrays.fill(x, Integer.MAX_VALUE);

    // Base case
    x[0] = 0;

    // For every element relax every reachable
    // element ie relax next k elements
    for (int i = 0; i < size; i++)
    {
        // reaching next k element
        for (int j = i + 1;
                 j < i + k + 1 &&
                 j < size; j++)
        {
            // Relaxing the element
            x[j] = min(x[j], x[i] +
              Math.abs(A[i] - A[j]));
        }
    }

    // return the last element in the array
    return x[size - 1];
}

// Driver Code
public static void main(String []args)
{
    int []input = { 83, 26, 37, 35, 33, 35, 56 };
    System.out.println(minCostJumpsDP(input, 3));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

def minCostJumpsDP(A, k):

    # for calculating the number of elements
    size = len(A)

    # Allocating Memo table and
    # initializing with INT_MAX
    x = [sys.maxsize] * (size)

    # Base case
    x[0] = 0

    # For every element relax every reachable
    # element ie relax next k elements
    for i in range(size):

        # reaching next k element
        j = i+1
        while j < i + k + 1 and j < size:

            # Relaxing the element
            x[j] = min(x[j], x[i] + abs(A[i] - A[j]))
            j += 1

    # return the last element in the array
    return x[size - 1]

# Driver Code
if __name__ == "__main__":

    input_ = [83, 26, 37, 35, 33, 35, 56]
    print(minCostJumpsDP(input_, 3))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function for returning the
// min of two elements
static int min(int a, int b)
{
    return (a > b) ? b : a;
}

static int minCostJumpsDP(int []A, int k)
{
    // for calculating the number of elements
    int size = A.Length;

    // Allocating Memo table and
    // initializing with INT_MAX
    int []x = new int[size];
    for (int i = 0; i < size; i++)
        x[i] = int.MaxValue;
    // Base case
    x[0] = 0;

    // For every element relax every reachable
    // element ie relax next k elements
    for (int i = 0; i < size; i++)
    {
        // reaching next k element
        for (int j = i + 1;
                 j < i + k + 1 &&
                 j < size; j++)
        {
            // Relaxing the element
            x[j] = min(x[j], x[i] +
            Math.Abs(A[i] - A[j]));
        }
    }

    // return the last element in the array
    return x[size - 1];
}

// Driver Code
public static void Main(String []args)
{
    int []input = { 83, 26, 37, 35, 33, 35, 56 };
    Console.WriteLine(minCostJumpsDP(input, 3));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function for returning the
    // min of two elements
    function min(a, b)
    {
        return (a > b) ? b : a;
    }

    function minCostJumpsDP(A, k)
    {
        // for calculating the number of elements
        let size = A.length;

        // Allocating Memo table and
        // initializing with INT_MAX
        let x = new Array(size);
        for (let i = 0; i < size; i++)
            x[i] = Number.MAX_VALUE;
        // Base case
        x[0] = 0;

        // For every element relax every reachable
        // element ie relax next k elements
        for (let i = 0; i < size; i++)
        {
            // reaching next k element
            for (let j = i + 1;
                     j < i + k + 1 &&
                     j < size; j++)
            {
                // Relaxing the element
                x[j] = min(x[j], x[i] +
                Math.abs(A[i] - A[j]));
            }
        }

        // return the last element in the array
        return x[size - 1];
    }

    let input = [ 83, 26, 37, 35, 33, 35, 56 ];
    document.write(minCostJumpsDP(input, 3));

</script>
```

**Output:** 

```
69
```

**时间复杂度:**O(N * K)
T3】辅助空间: O(N)