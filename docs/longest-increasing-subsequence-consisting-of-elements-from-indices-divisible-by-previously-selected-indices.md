# 最长的递增子序列，由可被先前选择的指数整除的指数中的元素组成

> 原文:[https://www . geeksforgeeks . org/最长递增子序列-由索引中的元素组成-可被先前选择的索引除尽/](https://www.geeksforgeeks.org/longest-increasing-subsequence-consisting-of-elements-from-indices-divisible-by-previously-selected-indices/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过从可被所有先前选择的索引整除的索引中选择元素来找到可能的[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的长度。
***注:**考虑基于 1 的索引*

**示例:**

> **输入:** arr[] = {1，4，2，3，6，4，9}
> **输出:** 3
> **解释:**最佳方式是选择出现在索引 1，3 & 6 的元素。从这些索引中选择元素生成的序列{1，2，4}不断增加，每个索引都可以被之前选择的索引整除。
> 因此长度为 3。
> 
> **输入:** arr[] = {2，3，4，5，6，7，8，9}
> **输出:** 4
> **解释:**最佳方式是选择出现在索引 1，2，4 & 8 处的元素。通过从这些索引中选择元素而生成的序列{2，3，5，9}正在增加，并且每个索引都可以被先前选择的索引整除。
> 因此长度为 4。

**简单方法:**最简单的方法是[通过从序列中选择可被序列中所有前面的索引整除的索引来生成可能的数组元素的所有子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)。找出所有这些子序列的长度，并打印得到的最大长度。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的数组 **dp[]** 。在 **dp[]** 表中的 **i** <sup>第</sup>个索引，即 **dp[i]** ，代表直到 **i** <sup>第</sup>个索引所获得的所需类型的最长可能子序列的长度。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**DP【】**，用变量 **j** 遍历 **i** 的所有倍数，使得 **2*i ≤ j ≤ N** 。
    *   对于每个 **j** ，如果 **arr[j] > arr[i]** ，则更新值 **dp[j] = max(dp[j]，dp[i] + 1)** 以包括最长子序列的长度。
    *   否则，检查下一个索引。
*   完成上述步骤后，从数组 **dp[]** 中打印[最大元素作为最长子序列的长度。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find length of longest
// subsequence generated that
// satisfies the specified conditions
int findMaxLength(int N, vector<int> arr)
{

    // Stores the length of longest
    // subsequences of all lengths
    vector<int> dp(N + 1, 1);

    // Iterate through the given array
    for (int i = 1; i <= N; i++) {

        // Iterate through the multiples i
        for (int j = 2 * i; j <= N; j += i) {

            if (arr[i - 1] < arr[j - 1]) {

                // Update dp[j] as maximum
                // of dp[j] and dp[i] + 1
                dp[j] = max(dp[j], dp[i] + 1);
            }
        }
    }

    // Return the maximum element in dp[]
    // as the length of longest subsequence
    return *max_element(dp.begin(), dp.end());
}

// Driver Code
int main()
{
    vector<int> arr{ 2, 3, 4, 5, 6, 7, 8, 9 };
    int N = arr.size();

    // Function Call
    cout << findMaxLength(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find length of longest
// subsequence generated that
// satisfies the specified conditions
static int findMaxLength(int N, int[] arr)
{

    // Stores the length of longest
    // subsequences of all lengths
    int[] dp = new int[N + 1];
    Arrays.fill(dp, 1);

    // Iterate through the given array
    for(int i = 1; i <= N; i++)
    {

        // Iterate through the multiples i
        for(int j = 2 * i; j <= N; j += i)
        {
            if (arr[i - 1] < arr[j - 1])
            {

                // Update dp[j] as maximum
                // of dp[j] and dp[i] + 1
                dp[j] = Math.max(dp[j], dp[i] + 1);
            }
        }
    }

    // Return the maximum element in dp[]
    // as the length of longest subsequence
    return Arrays.stream(dp).max().getAsInt();
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 4, 5, 6, 7, 8, 9 };
    int N = arr.length;

    // Function Call
    System.out.print(findMaxLength(N, arr));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find length of longest
# subsequence generated that
# satisfies the specified conditions
def findMaxLength(N, arr):

    # Stores the length of longest
    # subsequences of all lengths
    dp = [1] * (N + 1)

    # Iterate through the given array
    for i in range(1, N + 1):

        # Iterate through the multiples i
        for j in range(2 * i, N + 1, i):

            if (arr[i - 1] < arr[j - 1]):

                # Update dp[j] as maximum
                # of dp[j] and dp[i] + 1
                dp[j] = max(dp[j], dp[i] + 1)

    # Return the maximum element in dp[]
    # as the length of longest subsequence
    return max(dp)

# Driver Code
if __name__ == '__main__':
    arr=[2, 3, 4, 5, 6, 7, 8, 9]
    N = len(arr)

    # Function Call
    print(findMaxLength(N, arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG{

// Function to find length of longest
// subsequence generated that
// satisfies the specified conditions
static int findMaxLength(int N, int[] arr)
{

    // Stores the length of longest
    // subsequences of all lengths
    int[] dp = new int[N + 1];
    for(int i = 1; i <= N; i++)
    {
        dp[i] = 1;
    }

    // Iterate through the given array
    for(int i = 1; i <= N; i++)
    {

        // Iterate through the multiples i
        for(int j = 2 * i; j <= N; j += i)
        {
            if (arr[i - 1] < arr[j - 1])
            {

                // Update dp[j] as maximum
                // of dp[j] and dp[i] + 1
                dp[j] = Math.Max(dp[j], dp[i] + 1);
            }
        }
    }

    // Return the maximum element in dp[]
    // as the length of longest subsequence
    return dp.Max();;
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 3, 4, 5, 6, 7, 8, 9 };
    int N = arr.Length;

    // Function Call
    Console.WriteLine(findMaxLength(N, arr));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find length of longest
    // subsequence generated that
    // satisfies the specified conditions
    function findMaxLength(N,  arr) {

        // Stores the length of longest
        // subsequences of all lengths
        var dp = Array(N + 1).fill(1);

        // Iterate through the given array
        for (i = 1; i <= N; i++) {

            // Iterate through the multiples i
            for (j = 2 * i; j <= N; j += i) {
                if (arr[i - 1] < arr[j - 1]) {

                    // Update dp[j] as maximum
                    // of dp[j] and dp[i] + 1
                    dp[j] = Math.max(dp[j], dp[i] + 1);
                }
            }
        }

        // Return the maximum element in dp
        // as the length of longest subsequence
        return Math.max.apply(Math,dp);
    }

    // Driver Code

        var arr = [ 2, 3, 4, 5, 6, 7, 8, 9 ];
        var N = arr.length;

        // Function Call
        document.write(findMaxLength(N, arr));
// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*