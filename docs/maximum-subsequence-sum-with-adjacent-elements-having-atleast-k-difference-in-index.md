# 相邻元素在索引中至少有 K 个差异的最大子序列和

> 原文:[https://www . geeksforgeeks . org/最大子序列与相邻元素之和-至少有-k 个索引差异/](https://www.geeksforgeeks.org/maximum-subsequence-sum-with-adjacent-elements-having-atleast-k-difference-in-index/)

给定一个由长度为 **N** 的整数和一个整数 **K** (1 ≤ k ≤ N)组成的数组**arr【】**，任务是找到数组中最大的子序列和，使得该子序列中的相邻元素在它们在原始数组中的索引中至少有 **K** 的差异。

**示例:**

> **输入:** arr[] = {1，2，-2，4，3，1}，K = 4
> **输出:** 4
> **解释:**
> 这样可以选择的子序列:{1，3}、{1，1}、{2，1}
> 最大和= (1 + 3) = 4 的子序列
> 选择的元素是 a[0]和 a[4](指数之间的差= 4)
> 
> **输入:** arr[] = {1，2，72，4，3}，K = 2
> **输出:** 76
> **解释:**
> 这样可以选择的子序列–{ {1，72，3}、{2，4}、{2，3}、{1，4}、{ 1，3}}
> 最大和= (1 + 72 + 3) = 76
> 选择的元素是 a[0]，

**天真方法:** [生成数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)并检查每个子集是否满足两个相邻元素的索引至少相差 K 的条件。如果是，则将它的总和与迄今为止获得的最大总和进行比较，如果它大于迄今为止获得的总和，则更新总和。
高效**方法:**这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决。其中，对于数组中的每个元素，考虑这样的情况:如果我们取这个元素，那么它对最终得到的和有贡献。如果是，那么把它加到那个元素的 DP 数组中。

让我们决定“dp”的状态。假设 dp[i]是从索引“0”开始到索引“I”结束的子数组的最大可能和。现在，我们必须找到这个状态和低阶状态之间的递归关系。
现在数组的递归关系对于每个索引 I 有两个选择

*   选择当前索引:
    在这种情况下，可以选择的元素在索引 i-k 处。
    所以，

```
dp[i] = arr[i] + dp[i - k]
```

*   跳过当前索引。
    在这种情况下，可以选择的元素在索引 i-1 处。
    所以，

```
dp[i] = dp[i - 1]
```

对于每个指数，选择给出该指数最大和的条件，因此最终的[递推关系](https://www.geeksforgeeks.org/different-types-recurrence-relations-solutions/)将是:

> dp[i] = max（dp[i – 1]， scar[i] + dp[i – k]）

下面是上述方法的实现。

## C++

```
// C++ implementation to find the
// maximum sum subsequence such that
// two adjacent element have atleast
// difference of K in their indices

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// between two elements a and b
int maxi(int a, int b)
{
    if (a > b) {
        return a;
    }
    else {
        return b;
    }
}

// Function to find the maximum sum
// subsequence such that two adjacent
// element have atleast difference
// of K in their indices
int max_sum(int arr[], int n, int k)
{
    // DP Array to store the maximum
    // sum obtained till now
    int dp[n];

    // Either select the first element
    // or Nothing
    dp[0] = maxi(0, arr[0]);
    int i = 1;

    // Either Select the (i - 1) element
    // or let the previous best answer be
    // the current best answer
    while (i < k) {
        dp[i] = maxi(dp[i - 1], arr[i]);
        i++;
    }
    i = k;

    // Either select the best sum
    // till previous_index or select the
    // current element + best_sum till index-k
    while (i < n) {
        dp[i] = maxi(dp[i - 1], arr[i] + dp[i - k]);
        i++;
    }
    return dp[n - 1];
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, -2, 4, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    cout << max_sum(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum subsequence such that
// two adjacent element have atleast
// difference of K in their indices
class GFG
{

    // Function to find the maximum sum
    // subsequence such that two adjacent
    // element have atleast difference
    // of K in their indices
    static int max_sum(int arr[], int n, int k)
    {
        // DP Array to store the maximum
        // sum obtained till now
        int dp[] = new int[n];

        // Either select the first element
        // or Nothing
        dp[0] = Math.max(0, arr[0]);
        int i = 1;

        // Either Select the (i - 1) element
        // or let the previous best answer be
        // the current best answer
        while (i < k)
        {
            dp[i] = Math.max(dp[i - 1], arr[i]);
            i++;
        }
        i = k;

        // Either select the best sum
        // till previous_index or select the
        // current element + best_sum till index-k
        while (i < n)
        {
            dp[i] = Math.max(dp[i - 1],
                    arr[i] + dp[i - k]);
            i++;
        }
        return dp[n - 1];
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, -2, 4, 3, 1 };
        int n = arr.length;
        int k = 4;
        System.out.println(max_sum(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum sum subsequence such that
# two adjacent element have atleast
# difference of K in their indices

# Function to find the maximum sum
# subsequence such that two adjacent
# element have atleast difference
# of K in their indices
def max_sum(arr, n, k) :

    # DP Array to store the maximum
    # sum obtained till now
    dp = [0] * n;

    # Either select the first element
    # or Nothing
    dp[0] = max(0, arr[0]);
    i = 1;

    # Either Select the (i - 1) element
    # or let the previous best answer be
    # the current best answer
    while (i < k) :
        dp[i] = max(dp[i - 1], arr[i]);
        i += 1;

    i = k;

    # Either select the best sum
    # till previous_index or select the
    # current element + best_sum till index-k
    while (i < n) :
        dp[i] = max(dp[i - 1], arr[i] + dp[i - k]);
        i += 1;

    return dp[n - 1];

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, -2, 4, 3, 1 ];
    n = len(arr)
    k = 4;
    print(max_sum(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// maximum sum subsequence such that
// two adjacent element have atleast
// difference of K in their indices
using System;

class GFG
{

    // Function to find the maximum sum
    // subsequence such that two adjacent
    // element have atleast difference
    // of K in their indices
    static int max_sum(int []arr, int n, int k)
    {
        // DP Array to store the maximum
        // sum obtained till now
        int []dp = new int[n];

        // Either select the first element
        // or Nothing
        dp[0] = Math.Max(0, arr[0]);
        int i = 1;

        // Either Select the (i - 1) element
        // or let the previous best answer be
        // the current best answer
        while (i < k)
        {
            dp[i] = Math.Max(dp[i - 1], arr[i]);
            i++;
        }
        i = k;

        // Either select the best sum
        // till previous_index or select the
        // current element + best_sum till index-k
        while (i < n)
        {
            dp[i] = Math.Max(dp[i - 1],
                    arr[i] + dp[i - k]);
            i++;
        }
        return dp[n - 1];
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 2, -2, 4, 3, 1 };
        int n = arr.Length;
        int k = 4;
        Console.WriteLine(max_sum(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation to find the
// maximum sum subsequence such that
// two adjacent element have atleast
// difference of K in their indices

// Function to find the maximum sum
// subsequence such that two adjacent
// element have atleast difference
// of K in their indices
function max_sum(arr , n , k)
{
    // DP Array to store the maximum
    // sum obtained till now
    var dp = Array.from({length: n}, (_, i) => 0);

    // Either select the first element
    // or Nothing
    dp[0] = Math.max(0, arr[0]);
    var i = 1;

    // Either Select the (i - 1) element
    // or let the previous best answer be
    // the current best answer
    while (i < k)
    {
        dp[i] = Math.max(dp[i - 1], arr[i]);
        i++;
    }
    i = k;

    // Either select the best sum
    // till previous_index or select the
    // current element + best_sum till index-k
    while (i < n)
    {
        dp[i] = Math.max(dp[i - 1],
                arr[i] + dp[i - k]);
        i++;
    }
    return dp[n - 1];
}

// Driver Code
var arr = [ 1, 2, -2, 4, 3, 1 ];
var n = arr.length;
var k = 4;
document.write(max_sum(arr, n, k));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)