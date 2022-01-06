# 分割给定二进制字符串的最小成本

> 原文:[https://www . geesforgeks . org/给定二进制字符串的最小分区成本/](https://www.geeksforgeeks.org/minimum-cost-to-partition-the-given-binary-string/)

给定一个二进制字符串 **str** 和一个整数 **K** ，当每个段的成本是设置比特数与未设置比特数的乘积，总成本是所有单个段的成本之和时，任务是找到将字符串精确划分为 **K** 段所需的最小成本。
**举例:**

> **输入:** str = "110101 "，K = 3
> **输出:** 2
> 11|0|101 是可能的分区之一
> 其中成本为 0 + 0 + 2 = 2
> **输入:** str = "1000000 "，K = 5
> **输出:** 0

**方法:**编写一个函数 **minCost(s，k，Cost，I，n)** 其中 **cost** 是到目前为止的最小成本， **i** 是分区的起始索引， **k** 是要分区的剩余段。现在，从 **i <sup>th</sup>** 索引开始，计算当前分区的开销，并对剩余的子串递归调用相同的函数。为了记录结果，将使用一个 **dp[][]** 数组，其中 **dp[i][j]** 将存储从第 **i <sup>第</sup>** 索引开始将管柱分割成 **j** 零件的最小成本。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1001;

// dp[i][j] will store the minimum cost
// of partitioning the string into j
// parts starting at the ith index
int dp[MAX][MAX];

// Recursive function to find
// the minimum cost required
int minCost(string& s, int k, int cost, int i, int& n)
{

    // If the state has been solved before
    if (dp[i][k] != -1)
        return dp[i][k];

    // If only 1 part is left then the
    // remaining part of the string will
    // be considered as that part
    if (k == 1) {

        // To store the count of 0s and the
        // total characters of the string
        int count_0 = 0, total = n - i;

        // Count the 0s
        while (i < n)
            if (s[i++] == '0')
                count_0++;

        // Memoize and return the updated cost
        dp[i][k] = cost + (count_0
                           * (total - count_0));
        return dp[i][k];
    }

    int curr_cost = INT_MAX;
    int count_0 = 0;

    // Check all the positions to
    // make the current partition
    for (int j = i; j < n - k + 1; j++) {

        // Count the numbers of 0s
        if (s[j] == '0')
            count_0++;
        int curr_part_length = j - i + 1;

        // Cost of partition is equal to
        // (no. of 0s) * (no. of 1s)
        int part_cost = (count_0
                         * (curr_part_length - count_0));

        // string, partitions, curr cost,
        // start index, length
        part_cost += minCost(s, k - 1, 0, j + 1, n);

        // Update the current cost
        curr_cost = min(curr_cost, part_cost);
    }

    // Memoize and return the updated cost
    dp[i][k] = (cost + curr_cost);
    return (cost + curr_cost);
}

// Driver code
int main()
{
    string s = "110101";
    int n = s.length();
    int k = 3;

    // Initialise the dp array
    for (int i = 0; i < MAX; i++) {
        for (int j = 0; j < MAX; j++)
            dp[i][j] = -1;
    }

    // string, partitions, curr cost,
    // start index, length
    cout << minCost(s, k, 0, 0, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

    final static int MAX = 1001;

    // dp[i][j] will store the minimum cost
    // of partitioning the string into j
    // parts starting at the ith index
    static int dp[][] = new int [MAX][MAX];

    // Recursive function to find
    // the minimum cost required
    static int minCost(String s, int k, int cost, int i, int n)
    {

        // If the state has been solved before
        if (dp[i][k] != -1)
            return dp[i][k];

        // If only 1 part is left then the
        // remaining part of the string will
        // be considered as that part
        if (k == 1) {

            // To store the count of 0s and the
            // total characters of the string
            int count_0 = 0, total = n - i;

            // Count the 0s
            while (i < n)
                if (s.charAt(i++) == '0')
                    count_0++;

            // Memoize and return the updated cost
            dp[i][k] = cost + (count_0
                            * (total - count_0));
            return dp[i][k];
        }

        int curr_cost = Integer.MAX_VALUE;
        int count_0 = 0;

        // Check all the positions to
        // make the current partition
        for (int j = i; j < n - k + 1; j++) {

            // Count the numbers of 0s
            if (s.charAt(j) == '0')
                count_0++;
            int curr_part_length = j - i + 1;

            // Cost of partition is equal to
            // (no. of 0s) * (no. of 1s)
            int part_cost = (count_0
                            * (curr_part_length - count_0));

            // string, partitions, curr cost,
            // start index, length
            part_cost += minCost(s, k - 1, 0, j + 1, n);

            // Update the current cost
            curr_cost = Math.min(curr_cost, part_cost);
        }

        // Memoize and return the updated cost
        dp[i][k] = (cost + curr_cost);
        return (cost + curr_cost);
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "110101";
        int n = s.length();
        int k = 3;

        // Initialise the dp array
        for (int i = 0; i < MAX; i++) {
            for (int j = 0; j < MAX; j++)
                dp[i][j] = -1;
        }

        // string, partitions, curr cost,
        // start index, length
        System.out.println(minCost(s, k, 0, 0, n));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import sys
MAX = 1001

# dp[i][j] will store the minimum cost
# of partitioning the string into j
# parts starting at the ith index
dp = [[0 for i in range(MAX)]
         for j in range(MAX)]

# Recursive function to find
# the minimum cost required
def minCost(s, k, cost, i, n):

    # If the state has been solved before
    if (dp[i][k] != -1):
        return dp[i][k]

    # If only 1 part is left then the
    # remaining part of the string will
    # be considered as that part
    if (k == 1):

        # To store the count of 0s and the
        # total characters of the string
        count_0 = 0
        total = n - i

        # Count the 0s
        while (i < n):
            if (s[i] == '0'):
                count_0 += 1
            i += 1

        # Memoize and return the updated cost
        dp[i][k] = cost + (count_0 *
                          (total - count_0))
        return dp[i][k]

    curr_cost = sys.maxsize
    count_0 = 0

    # Check all the positions to
    # make the current partition
    for j in range(i, n - k + 1, 1):

        # Count the numbers of 0s
        if (s[j] == '0'):
            count_0 += 1
        curr_part_length = j - i + 1

        # Cost of partition is equal to
        # (no. of 0s) * (no. of 1s)
        part_cost = (count_0 *
                    (curr_part_length - count_0))

        # string, partitions, curr cost,
        # start index, length
        part_cost += minCost(s, k - 1, 0, j + 1, n)

        # Update the current cost
        curr_cost = min(curr_cost, part_cost)

    # Memoize and return the updated cost
    dp[i][k] = (cost + curr_cost)
    return (cost + curr_cost)

# Driver code
if __name__ == '__main__':
    s = "110101"
    n = len(s)
    k = 3

    # Initialise the dp array
    for i in range(MAX):
        for j in range(MAX):
            dp[i][j] = -1

    # string, partitions, curr cost,
    # start index, length
    print(minCost(s, k, 0, 0, n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach

using System;
using System.Collections.Generic;

class GFG
{

    readonly static int MAX = 1001;

    // dp[i,j] will store the minimum cost
    // of partitioning the string into j
    // parts starting at the ith index
    static int [,]dp = new int [MAX, MAX];

    // Recursive function to find
    // the minimum cost required
    static int minCost(String s, int k, int cost, int i, int n)
    {

        int count_0 = 0;
        // If the state has been solved before
        if (dp[i, k] != -1)
            return dp[i, k];

        // If only 1 part is left then the
        // remaining part of the string will
        // be considered as that part
        if (k == 1)
        {

            // To store the count of 0s and the
            // total characters of the string

            int total = n - i;

            // Count the 0s
            while (i < n)
                if (s[i++] == '0')
                    count_0++;

            // Memoize and return the updated cost
            dp[i, k] = cost + (count_0
                            * (total - count_0));
            return dp[i, k];
        }

        int curr_cost = int.MaxValue;
        count_0 = 0;

        // Check all the positions to
        // make the current partition
        for (int j = i; j < n - k + 1; j++)
        {

            // Count the numbers of 0s
            if (s[j] == '0')
                count_0++;
            int curr_partlength = j - i + 1;

            // Cost of partition is equal to
            // (no. of 0s) * (no. of 1s)
            int part_cost = (count_0
                            * (curr_partlength - count_0));

            // string, partitions, curr cost,
            // start index,.Length
            part_cost += minCost(s, k - 1, 0, j + 1, n);

            // Update the current cost
            curr_cost = Math.Min(curr_cost, part_cost);
        }

        // Memoize and return the updated cost
        dp[i, k] = (cost + curr_cost);
        return (cost + curr_cost);
    }

    // Driver code
    public static void Main (String[] args)
    {
        String s = "110101";
        int n = s.Length;
        int k = 3;

        // Initialise the dp array
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
                dp[i, j] = -1;
        }

        // string, partitions, curr cost,
        // start index,.Length
        Console.WriteLine(minCost(s, k, 0, 0, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let MAX = 1001;

    // dp[i][j] will store the minimum cost
    // of partitioning the string into j
    // parts starting at the ith index
    let dp = new Array(MAX);

    // Recursive function to find
    // the minimum cost required
    function minCost(s, k, cost, i, n)
    {

        // If the state has been solved before
        if (dp[i][k] != -1)
            return dp[i][k];

        // If only 1 part is left then the
        // remaining part of the string will
        // be considered as that part
        if (k == 1) {

            // To store the count of 0s and the
            // total characters of the string
            let count_0 = 0, total = n - i;

            // Count the 0s
            while (i < n)
                if (s[i++] == '0')
                    count_0++;

            // Memoize and return the updated cost
            dp[i][k] = cost + (count_0
                            * (total - count_0));
            return dp[i][k];
        }

        let curr_cost = Number.MAX_VALUE;
        let count_0 = 0;

        // Check all the positions to
        // make the current partition
        for (let j = i; j < n - k + 1; j++) {

            // Count the numbers of 0s
            if (s[j] == '0')
                count_0++;
            let curr_part_length = j - i + 1;

            // Cost of partition is equal to
            // (no. of 0s) * (no. of 1s)
            let part_cost = (count_0 * (curr_part_length - count_0));

            // string, partitions, curr cost,
            // start index, length
            part_cost += minCost(s, k - 1, 0, j + 1, n);

            // Update the current cost
            curr_cost = Math.min(curr_cost, part_cost);
        }

        // Memoize and return the updated cost
        dp[i][k] = (cost + curr_cost);
        return (cost + curr_cost);
    }

    let s = "110101";
    let n = s.length;
    let k = 3;

    // Initialise the dp array
    for (let i = 0; i < MAX; i++) {
      dp[i] = new Array(MAX);
      for (let j = 0; j < MAX; j++)
        dp[i][j] = -1;
    }

    // string, partitions, curr cost,
    // start index, length
    document.write(minCost(s, k, 0, 0, n));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2
```