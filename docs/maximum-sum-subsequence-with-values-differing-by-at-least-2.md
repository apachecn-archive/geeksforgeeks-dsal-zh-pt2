# 值相差至少 2 的最大和子序列

> 原文:[https://www . geeksforgeeks . org/最大和子序列带值-至少相差-2/](https://www.geeksforgeeks.org/maximum-sum-subsequence-with-values-differing-by-at-least-2/)

给定一个大小为 **N** 的正整数数组 **arr[]** ，任务是在序列中没有 2 个数字应与该值相邻的约束下，求一个子序列的最大和，即如果答案中考虑了 **arr[i]** ，则既不能选择 **arr[i]-1** 的出现，也不能选择 **arr[i]+1** 的出现。

**示例:**

> **输入:** arr[] = {2，2，2}
> **输出:** 6
> **解释:**
> 最大和子序列将是[2，2，2]，因为它不包含 1 或 3 的任何出现。因此总和= 2 + 2 + 2 = 6
> 
> **输入:** arr[] = {2，2，3}
> **输出:** 4
> **解释:**
> 子序列 1: [2，2]，因为它不包含 1 或 3 的任何出现。因此和= 2 + 2 = 4
> 子序列 2: [3]，因为它不包含 2 或 4 的任何出现。因此总和= 3
> 因此，最大总和= 4

**求解方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，类似于本文的[。](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)

1.  [创建一个](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/) [地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储元素 I 在序列中出现的次数。
2.  要找到答案，首先很容易将问题分解成更小的问题。在这种情况下，将序列分成更小的序列，并为其找到最优解。
3.  对于只包含 0 的数字序列，答案是 0。类似地，如果一个序列只包含数字 0 和 1，那么解决方法就是计数[1]*1。
4.  现在构建这个问题的递归解决方案。对于只包含数字 0 到 n 的数字序列，可以选择是否选择第 n 个元素。

> DP[I]= max(DP[I–1]，DP[I–2]+I * freq[I])
> DP[I-1]代表不挑第 ith 个数，那么这个数在可以考虑之前。
> DP[I–2]+I * freq[I]代表选取第 ith 个数字，然后是消除之前的数字。因此，在此之前的数字被考虑。

## C++

```
// C++ program to find maximum sum
// subsequence with values
// differing by at least 2

#include <bits/stdc++.h>
using namespace std;

// function to find maximum sum
// subsequence such that two
// adjacent values elements are
// not selected
int get_max_sum(int arr[], int n)
{
    // map to store the frequency
    // of array elements
    unordered_map<int, int> freq;

    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // make a dp array to store
    // answer upto i th value
    int dp[100001];
    memset(dp, 0, sizeof(dp));

    // base cases
    dp[0] = 0;
    dp[1] = freq[0];

    // iterate for all possible
    // values  of arr[i]
    for (int i = 2; i <= 100000; i++) {
        dp[i] = max(dp[i - 1],
                    dp[i - 2] + i * freq[i]);
    }

    // return the last value
    return dp[100000];
}

// Driver function
int main()
{

    int N = 3;
    int arr[] = { 2, 2, 3 };
    cout << get_max_sum(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum
// subsequence with values
// differing by at least 2
import java.util.*;
import java.lang.*;

class GFG{

// Function to find maximum sum
// subsequence such that two
// adjacent values elements are
// not selected
public static int get_max_sum(int arr[], int n)
{

    // map to store the frequency
    // of array elements
    HashMap<Integer,
            Integer> freq = new HashMap<Integer,
                                        Integer>();

    for(int i = 0; i < n; i++)
    {
        if (freq.containsKey(arr[i]))
        {
            int x = freq.get(arr[i]);
            freq.replace(arr[i], x + 1);
        }
        else
            freq.put(arr[i], 1);
    }

    // Make a dp array to store
    // answer upto i th value
    int[] dp = new int[100001];
    for(int i = 0; i < 100001; i++)
        dp[i] = 0;

    // Base cases
    dp[0] = 0;
    if (freq.containsKey(0))
        dp[1] = freq.get(0);
    else
        dp[1] = 0;

    // Iterate for all possible
    // values of arr[i]
    for(int i = 2; i <= 100000; i++)
    {
        int temp = (freq.containsKey(i)) ?
                    freq.get(i) : 0;
        dp[i] = Math.max(dp[i - 1],
                         dp[i - 2] + i * temp);
    }

    // Return the last value
    return dp[100000];
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    int arr[] = { 2, 2, 3 };

    System.out.println(get_max_sum(arr, N));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to find maximum sum
# subsequence with values
# differing by at least 2
from collections import defaultdict

# Function to find maximum sum
# subsequence such that two
# adjacent values elements are
# not selected
def get_max_sum(arr, n):

    # Map to store the frequency
    # of array elements
    freq = defaultdict(lambda : 0)

    for i in range(n):
        freq[arr[i]] += 1

    # Make a dp array to store
    # answer upto i th value
    dp = [0] * 100001

    # Base cases
    dp[0] = 0
    dp[1] = freq[0]

    # Iterate for all possible
    # values of arr[i]
    for i in range(2, 100000 + 1):
        dp[i] = max(dp[i - 1],
                    dp[i - 2] + i * freq[i])

    # Return the last value
    return dp[100000]

# Driver code
N = 3
arr = [ 2, 2, 3 ]

print(get_max_sum(arr, N))

# This code is contributed by stutipathak31jan
```

## C#

```
// C# program to find maximum sum
// subsequence with values
// differing by at least 2
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum sum
// subsequence such that two
// adjacent values elements are
// not selected
public static int get_max_sum(int []arr, int n)
{

    // map to store the frequency
    // of array elements
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    for(int i = 0; i < n; i++)
    {
        if (freq.ContainsKey(arr[i]))
        {
            int x = freq[arr[i]];
            freq[arr[i]]= x + 1;
        }
        else
            freq.Add(arr[i], 1);
    }

    // Make a dp array to store
    // answer upto i th value
    int[] dp = new int[100001];
    for(int i = 0; i < 100001; i++)
        dp[i] = 0;

    // Base cases
    dp[0] = 0;
    if (freq.ContainsKey(0))
        dp[1] = freq[0];
    else
        dp[1] = 0;

    // Iterate for all possible
    // values of arr[i]
    for(int i = 2; i <= 100000; i++)
    {
        int temp = (freq.ContainsKey(i)) ?
                    freq[i] : 0;
        dp[i] = Math.Max(dp[i - 1],
                         dp[i - 2] + i * temp);
    }

    // Return the last value
    return dp[100000];
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    int []arr = { 2, 2, 3 };

    Console.WriteLine(get_max_sum(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to find maximum sum
// subsequence with values
// differing by at least 2

// function to find maximum sum
// subsequence such that two
// adjacent values elements are
// not selected
function get_max_sum(arr, n)
{
    // map to store the frequency
    // of array elements
    var freq = new Map();

    for (var i = 0; i < n; i++) {
        if(freq.has(arr[i]))
            freq.set(arr[i], freq.get(arr[i])+1)
        else
            freq.set(arr[i], 1)
    }

    // make a dp array to store
    // answer upto i th value
    var dp = Array(100001).fill(0);

    // base cases
    dp[0] = 0;
    dp[1] = (freq.has(0)?freq.get(0):0);

    // iterate for all possible
    // values  of arr[i]
    for (var i = 2; i <= 100000; i++) {
        dp[i] = Math.max(dp[i - 1],
                    dp[i - 2] + i * (freq.has(i)?freq.get(i):0));
    }

    // return the last value
    return dp[100000];
}

// Driver function
var N = 3;
var arr = [2, 2, 3];
document.write( get_max_sum(arr, N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*