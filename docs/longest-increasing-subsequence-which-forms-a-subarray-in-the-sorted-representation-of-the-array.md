# 在数组的排序表示中形成子数组的最长递增子序列

> 原文:[https://www . geeksforgeeks . org/在数组的排序表示中形成子数组的最长递增子序列/](https://www.geeksforgeeks.org/longest-increasing-subsequence-which-forms-a-subarray-in-the-sorted-representation-of-the-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到[个最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)的长度，以便在对原始数组进行排序时形成一个[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** arr[] = {2，6，4，8，2，9 }
> **输出:** 3
> **解释:**
> 排序数组:{ 2，2，4，6，8，9}
> 原始数组所有可能的非递减序列为
> {2}、{6}、{4}、{8}、{2}、{9}、{ 2，2}、{6，8}、{8，9 }、{ 6 }
> 在上述所有子序列中，{6，8，9}是最长的子序列，它是数组排序表示中的一个子数组。
> 
> **输入:** arr[] = { 5，5，6，6，5，5，5，6，5，5 }
> **输出:** 7
> **解释:**
> 排序数组:{ 5，5，5，5，5，5，5，5，6，6}
> {5，5，5，5，5，5，5 }是以数组的排序形式形成子数组的最长子序列。

**天真方法:**想法是[生成数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，然后在对原始数组排序时检查它们中的哪一个形成了最长的子数组。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)途径解决这个问题。以下是步骤:

1.  在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中存储给定数组中每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
2.  将原始数组存储在临时数组中，并对给定数组进行排序。
3.  初始化一个大小为 **N*3** 的 2D 数组，其中:
    *   **dp[N][i]** 将存储数字计数 **X** 直到位置 **i** 。
    *   **dp[x][1]** 将存储数量计数 **X** +数量计数**(X–1)**直到位置 **i** 。
    *   **dp[x][2]** 将存储序列的实际长度直到位置 **i** 。
4.  [迭代原始数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于原始数组中的每个索引 **i** ，仅当所有**(X–1)**元素都已经包含在子序列中时，才包含当前位置 **i** 的元素，并更新 **dp[][]** 中的值，并在此状态后更新最大子序列大小。
5.  完成上述步骤后，打印最大子序列大小。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest increasing sorted sequence
int LongestSequence(int a[], int n)
{
    // Stores the count of all elements
    map<int, int> m;

    int ar[n + 1], i, j;

    // Store the original array
    for (i = 1; i <= n; i++) {
        ar[i] = a[i - 1];
    }

    // Sort the array
    sort(a, a + n);

    int c = 1;
    m[a[0]] = c;

    for (i = 1; i <= n; i++) {

        // If adjacent element
        // are not same
        if (a[i] != a[i - 1]) {

            // Increment count
            c++;
            m[a[i]] = c;
        }
    }

    // Store frequency of each element
    map<int, int> cnt;

    // Initialize a DP array
    int dp[n + 1][3] = { 0 };
    cnt[0] = 0;

    // Iterate over the array ar[]
    for (i = 1; i <= n; i++) {
        ar[i] = m[ar[i]];
        cnt[ar[i]]++;
    }

    // Length of the longest
    // increasing sorted sequence
    int ans = 0, x;

    // Iterate over the array
    for (i = 1; i <= n; i++) {

        // Current element
        x = ar[i];

        // If the element has been
        // encountered the first time
        if (dp[x][0] == 0) {

            // If all the x - 1 previous
            // elements have already appeared
            if (dp[x - 1][0] == cnt[x - 1]) {
                dp[x][1] = dp[x - 1][1];
                dp[x][2] = dp[x - 1][1];
            }

            // Otherwise
            else {
                dp[x][1] = dp[x - 1][0];
            }
        }

        dp[x][2] = max(dp[x - 1][0],
                       dp[x][2]);

        if (dp[x - 1][0] == cnt[x - 1]) {

            // If all x-1 elements have
            // already been encountered
            dp[x][2] = max(dp[x][2],
                           dp[x - 1][1]);
        }
        for (j = 0; j < 3; j++) {

            // Increment the count of
            // the current element
            dp[x][j]++;

            // Update maximum
            // subsequence size
            ans = max(ans, dp[x][j]);
        }
    }

    // Return the maximum
    // subsequence size
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 6, 4, 8, 2, 9 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << LongestSequence(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the length of the
// longest increasing sorted sequence
static int LongestSequence(int a[], int n)
{

    // Stores the count of all elements
    HashMap<Integer, Integer> m = new HashMap<>();

    int ar[] = new int[n + 1];
    int i = 0;
    int j = 0;

    // Store the original array
    for(i = 1; i <= n; i++)
    {
        ar[i] = a[i - 1];
    }

    // Sort the array
    Arrays.sort(a);

    int c = 1;
    m.put(a[0], c);

    for(i = 1; i < n; i++)
    {

        // If adjacent element
        // are not same
        if (a[i] != a[i - 1])
        {

            // Increment count
            c++;
            m.put(a[i], c);
        }
    }

    // Store frequency of each element
    HashMap<Integer, Integer> cnt = new HashMap<>();

    // Initialize a DP array
    int dp[][] = new int[n + 1][3];

    cnt.put(0, 0);

    // Iterate over the array ar[]
    for(i = 1; i <= n; i++)
    {
        ar[i] = m.get(ar[i]);

        if (cnt.containsKey(ar[i]))
            cnt.put(ar[i], cnt.get(ar[i]) + 1);
        else
            cnt.put(ar[i], 1);
    }

    // Length of the longest
    // increasing sorted sequence
    int ans = 0, x;

    // Iterate over the array
    for(i = 1; i <= n; i++)
    {

        // Current element
        x = ar[i];

        // If the element has been
        // encountered the first time
        if (dp[x][0] == 0)
        {

            // If all the x - 1 previous
            // elements have already appeared
            if (dp[x - 1][0] == cnt.get(x - 1))
            {
                dp[x][1] = dp[x - 1][1];
                dp[x][2] = dp[x - 1][1];
            }

            // Otherwise
            else
            {
                dp[x][1] = dp[x - 1][0];
            }
        }

        dp[x][2] = Math.max(dp[x - 1][0],
                            dp[x][2]);

        if (dp[x - 1][0] == cnt.get(x - 1))
        {

            // If all x-1 elements have
            // already been encountered
            dp[x][2] = Math.max(dp[x][2],
                                dp[x - 1][1]);
        }
        for(j = 0; j < 3; j++)
        {

            // Increment the count of
            // the current element
            dp[x][j]++;

            // Update maximum
            // subsequence size
            ans = Math.max(ans, dp[x][j]);
        }
    }

    // Return the maximum
    // subsequence size
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 6, 4, 8, 2, 9 };
    int n = arr.length;

    System.out.println(LongestSequence(arr, n));
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to find the length of the
# longest increasing sorted sequence
def LongestSequence(a, n):

  # Stores the count of all elements
  m = {i : 0 for i in range(100)}

  ar = [0 for i in range(n + 1)]

  # Store the original array
  for i in range(1, n + 1):
    ar[i] = a[i - 1]

  # Sort the array
  a.sort(reverse = False)

  c = 1
  m[a[0]] = c

  for i in range(1, n):

    # If adjacent element
    # are not same
    if (a[i] != a[i - 1]):

      # Increment count
      c += 1
      m[a[i]] = c

  # Store frequency of each element
  cnt = {i : 0 for i in range(100)}

  # Initialize a DP array
  dp = [[0 for i in range(3)]
           for j in range(n + 1)]

  cnt[0] = 0

  # Iterate over the array ar[]
  for i in range(1, n + 1):

    ar[i] = m[ar[i]]
    cnt[ar[i]] += 1

  # Length of the longest
  # increasing sorted sequence
  ans = 0

  # Iterate over the array
  for i in range(1, n + 1):

    # Current element
    x = ar[i]

    # If the element has been
    # encountered the first time
    if (dp[x][0] == 0):

      # If all the x - 1 previous
      # elements have already appeared
      if (dp[x - 1][0] == cnt[x - 1]):
        dp[x][1] = dp[x - 1][1]
        dp[x][2] = dp[x - 1][1]

      # Otherwise
      else:
        dp[x][1] = dp[x - 1][0]

      dp[x][2] = max(dp[x - 1][0], dp[x][2])

      if (dp[x - 1][0] == cnt[x - 1]):

        # If all x-1 elements have
        # already been encountered
        dp[x][2] = max(dp[x][2], dp[x - 1][1])

      for j in range(3):

        # Increment the count of
        # the current element
        dp[x][j] += 1

        # Update maximum
        # subsequence size
        ans = max(ans, dp[x][j])

  # Return the maximum
  # subsequence size
  return ans

# Driver Code
if __name__ == '__main__':

  arr =  [ 2, 6, 4, 8, 2, 9 ]

  N = len(arr)

  # Function call
  print(LongestSequence(arr, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find the length of the
// longest increasing sorted sequence
static int LongestSequence(int []a, int n)
{

    // Stores the count of all elements
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    int []ar = new int[n + 1];
    int i = 0;
    int j = 0;

    // Store the original array
    for(i = 1; i <= n; i++)
    {
        ar[i] = a[i - 1];
    }

    // Sort the array
    Array.Sort(a);

    int c = 1;
    m[a[0]]= c;

    for(i = 1; i < n; i++)
    {

        // If adjacent element
        // are not same
        if (a[i] != a[i - 1])
        {

            // Increment count
            c++;
            m[a[i]]= c;
        }
    }

    // Store frequency of each element
    Dictionary<int,
               int>cnt = new Dictionary<int,
                                        int>();

    // Initialize a DP array
    int [,]dp = new int[n + 1, 3];

    cnt[0] = 0;

    // Iterate over the array ar[]
    for(i = 1; i <= n; i++)
    {
        ar[i] = m[ar[i]];

        if (cnt.ContainsKey(ar[i]))
            cnt[ar[i]]= cnt[ar[i]] + 1;
        else
            cnt[ar[i]]= 1;
    }

    // Length of the longest
    // increasing sorted sequence
    int ans = 0, x;

    // Iterate over the array
    for(i = 1; i <= n; i++)
    {

        // Current element
        x = ar[i];

        // If the element has been
        // encountered the first time
        if (dp[x, 0] == 0)
        {

            // If all the x - 1 previous
            // elements have already appeared
            if (dp[x - 1, 0] == cnt[x - 1])
            {
                dp[x, 1] = dp[x - 1, 1];
                dp[x, 2] = dp[x - 1, 1];
            }

            // Otherwise
            else
            {
                dp[x, 1] = dp[x - 1, 0];
            }
        }

        dp[x, 2] = Math.Max(dp[x - 1, 0],
                            dp[x, 2]);

        if (dp[x - 1, 0] == cnt[x - 1])
        {

            // If all x-1 elements have
            // already been encountered
            dp[x, 2] = Math.Max(dp[x, 2],
                                dp[x - 1, 1]);
        }
        for(j = 0; j < 3; j++)
        {

            // Increment the count of
            // the current element
            dp[x, j]++;

            // Update maximum
            // subsequence size
            ans = Math.Max(ans, dp[x, j]);
        }
    }

    // Return the maximum
    // subsequence size
    return ans;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 6, 4, 8, 2, 9 };
    int n = arr.Length;

    Console.WriteLine(LongestSequence(arr, n));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the length of the
// longest increasing sorted sequence
function LongestSequence(a, n)
{
    // Stores the count of all elements
    var m = new Map();

    var ar = Array(n+1).fill(0), i, j;

    // Store the original array
    for (i = 1; i <= n; i++) {
        ar[i] = a[i - 1];
    }

    // Sort the array
    a.sort((a,b)=>a-b);

    var c = 1;
    m.set(a[0], c);

    for (i = 1; i <= n; i++) {

        // If adjacent element
        // are not same
        if (a[i] != a[i - 1]) {

            // Increment count
            c++;
            m.set(a[i], c);
        }
    }

    // Store frequency of each element
    var cnt = new Map();

    // Initialize a DP array
    var dp = Array.from(Array(n+1), ()=>Array(3).fill(0));
    cnt.set(0, 0);

    // Iterate over the array ar[]
    for (i = 1; i <= n; i++) {
        ar[i] = m.get(ar[i]);
        if(cnt.has(ar[i]))
            cnt.set(ar[i], cnt.get(ar[i])+1)
        else
            cnt.set(ar[i], 1)
    }

    // Length of the longest
    // increasing sorted sequence
    var ans = 0, x;

    // Iterate over the array
    for (i = 1; i <= n; i++) {

        // Current element
        x = ar[i];

        // If the element has been
        // encountered the first time
        if (dp[x][0] == 0) {

            // If all the x - 1 previous
            // elements have already appeared
            if (dp[x - 1][0] == cnt.get(x - 1)) {
                dp[x][1] = dp[x - 1][1];
                dp[x][2] = dp[x - 1][1];
            }

            // Otherwise
            else {
                dp[x][1] = dp[x - 1][0];
            }
        }

        dp[x][2] = Math.max(dp[x - 1][0],
                       dp[x][2]);

        if (dp[x - 1][0] == cnt[x - 1]) {

            // If all x-1 elements have
            // already been encountered
            dp[x][2] = Math.max(dp[x][2],
                           dp[x - 1][1]);
        }
        for (j = 0; j < 3; j++) {

            // Increment the count of
            // the current element
            dp[x][j]++;

            // Update maximum
            // subsequence size
            ans = Math.max(ans, dp[x][j]);
        }
    }

    // Return the maximum
    // subsequence size
    return ans;
}

// Driver Code

var arr = [2, 6, 4, 8, 2, 9];
var N = arr.length;

// Function Call
document.write( LongestSequence(arr, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)