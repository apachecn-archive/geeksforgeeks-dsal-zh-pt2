# 形成算术级数的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列形成算术级数-ap/](https://www.geeksforgeeks.org/longest-subsequence-forming-an-arithmetic-progression-ap/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到形成[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)的最长子序列的长度。

**示例:**

> **输入:** arr[] = {5，10，15，20，25，30}
> **输出:** 6
> **说明:**
> 整套在 AP 有共性区别= 5。
> 因此，长度为 4。
> 
> **输入:** arr[] = { 20，1，15，3，10，5，8 }
> **输出:** 4
> **解释:**
> 具有相同差异的最长子序列是{ 20，15，10，5 }。
> 上述子序列对于每个连续的对具有相同的差异，即(15–20)=(10–15)=(5–10)=-5。
> 因此长度为 4。

**天真方法:**解决问题最简单的方法是[生成给定数组的所有可能子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)并打印相邻元素对之间具有相同差异的最长子序列的长度。 ***时间***

***复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。以下是步骤:

1.  初始化一个辅助矩阵 **dp[][]** ，其中 **dp[i][j]** 表示从 **i** 开始的子序列的长度，与 **j** 有共同的区别。
2.  使用嵌套循环 **i** 迭代数组，从**N–1**到 **0** 和 **j** 从 **i+1** 到 **N** 。
    *   假设 **arr[i]** 和 **arr[j]** 是序列的前两个元素，让它们的差为 **d** 。
    *   现在，出现了两种情况:
        1.  **dp[j][d] = 0** :不存在以 **arr[j]** 开头，与 **d** 不同的序列。在这种情况下 **dp[i][d] = 2** ，因为我们在序列中只能有 **arr[i]** 和 **arr[j]** 。
        2.  **dp[j][d] > 0** :存在以 **arr[j]** 开始的序列，相邻元素之间的差异为 **d** 。在这种情况下，关系为 **dp[i][d] = 1 + dp[j][d]** 。
3.  最后，打印所有形成的子序列的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds the longest
// arithmetic subsequence having the
// same absolute difference
int lenghtOfLongestAP(int A[], int n)
{

    // Stores the length of sequences
    // having same difference
    unordered_map<int,
                  unordered_map<int, int> >
        dp;

    // Stores the resultant length
    int res = 2;

    // Iterate over the array
    for (int i = 0; i < n; ++i) {

        for (int j = i + 1; j < n; ++j) {

            int d = A[j] - A[i];

            // Update length of subsequence
            dp[d][j] = dp[d].count(i)
                           ? dp[d][i] + 1
                           : 2;

            res = max(res, dp[d][j]);
        }
    }

    // Return res
    return res;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 20, 1, 15, 3, 10, 5, 8 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << lenghtOfLongestAP(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function that finds the longest
// arithmetic subsequence having the
// same absolute difference
static int lenghtOfLongestAP(int A[], int n)
{

    // Stores the length of sequences
    // having same difference
    Map<Integer,
    Map<Integer,
        Integer>> dp = new HashMap<Integer,
                               Map<Integer,
                                   Integer>>();

    // Stores the resultant length
    int res = 2;

    // Iterate over the array
    for(int i = 0; i < n; ++i)
    {
        for(int j = i + 1; j < n; ++j)
        {
            int d = A[j] - A[i];
            Map<Integer, Integer> temp;

            // Update length of subsequence
            if (dp.containsKey(d))
            {
                temp = dp.get(d);

                if (temp.containsKey(i))
                    temp.put(j, temp.get(i) + 1);
                else
                    temp.put(j, 2);
            }
            else
            {
                temp = new HashMap<Integer, Integer>();
                temp.put(j, 2);
            }
            dp.put(d, temp);
            res = Math.max(res, temp.get(j));
        }
    }

    // Return res
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 20, 1, 15, 3, 10, 5, 8 };

    int N = arr.length;

    // Function Call
    System.out.println(lenghtOfLongestAP(arr, N));
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the longest
# arithmetic subsequence having the
# same absolute difference
def lenghtOfLongestAP(A, n) :

    # Stores the length of sequences
    # having same difference
    dp = {}

    # Stores the resultant length
    res = 2

    # Iterate over the array
    for i in range(n) :

        for j in range(i + 1, n) :

            d = A[j] - A[i]

            # Update length of subsequence
            if d in dp :
                if i in dp[d] :
                    dp[d][j] = dp[d][i] + 1
                else :
                    dp[d][j] = 2
            else :
                dp[d] = {}
                dp[d][j] = 2

            if d in dp :
                if j in dp[d] :
                    res = max(res, dp[d][j])

    # Return res
    return res

# Given array arr[]
arr = [ 20, 1, 15, 3, 10, 5, 8 ]

N = len(arr)

# Function Call
print(lenghtOfLongestAP(arr, N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function that finds the longest
// arithmetic subsequence having the
// same absolute difference
static int lenghtOfLongestAP(int []A, int n)
{

    // Stores the length of sequences
    // having same difference
    Dictionary<int,
    Dictionary<int, int>> dp = new Dictionary<int,
                                   Dictionary<int, int>>();

    // Stores the resultant length
    int res = 2;

    // Iterate over the array
    for(int i = 0; i < n; ++i)
    {
        for(int j = i + 1; j < n; ++j)
        {
            int d = A[j] - A[i];

            // Update length of subsequence
            if (dp.ContainsKey(d))
            {
                 if (dp[d].ContainsKey(i))
                {
                    dp[d][j] = dp[d][i] + 1;   
                }
                else
                {
                    dp[d][j] = 2;
                }
            }
            else
            {
                dp[d] = new Dictionary<int, int>();
                dp[d][j] = 2;
            }
            res = Math.Max(res, dp[d][j]);
        }
    }

    // Return res
    return res;
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 20, 1, 15, 3, 10, 5, 8 };

    int N = arr.Length;

    // Function call
    Console.Write(lenghtOfLongestAP(arr, N));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that finds the longest
// arithmetic subsequence having the
// same absolute difference
function lenghtOfLongestAP(A, n)
{

    // Stores the length of sequences
    // having same difference
    var dp = new Map();

    // Stores the resultant length
    var res = 2;

    // Iterate over the array
    for (var i = 0; i < n; ++i) {

        for (var j = i + 1; j < n; ++j) {

            var d = A[j] - A[i];

             // Update length of subsequence
             if (dp.has(d))
            {
                 if (dp.get(d).has(i))
                {
                    var tmp = dp.get(d);
                    tmp.set(j, dp.get(d).get(i)+1);
                }
                else
                {
                    var tmp = new Map();
                    tmp.set(j, 2);
                    dp.set(d, tmp);
                }
            }
            else
            {
                var tmp = new Map();
                tmp.set(j, 2);
                dp.set(d, tmp);
            }
            res = Math.max(res, dp.get(d).get(j));
        }
    }

    // Return res
    return res;
}

// Driver Code

// Given array arr[]
var arr = [20, 1, 15, 3, 10, 5, 8];
var N = arr.length;

// Function Call
document.write( lenghtOfLongestAP(arr, N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*