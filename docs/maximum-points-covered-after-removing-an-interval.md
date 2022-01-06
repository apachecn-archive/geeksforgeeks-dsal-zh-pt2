# 移除间隔后覆盖的最大点数

> 原文:[https://www . geeksforgeeks . org/移除间隔后覆盖的最大点数/](https://www.geeksforgeeks.org/maximum-points-covered-after-removing-an-interval/)

给定形式为**【l，r】**的 **N** 间隔和整数 **Q** 。任务是找到区间，当删除该区间时，将覆盖最大数量的点(所有其余区间的并集)。**注意**所有给定的间隔只包括 **1** 到 **Q** 之间的数字。
**示例:**

> **输入:**间隔[][] = {{1，4}，{4，5}，{5，6}，{6，7}，{3，5}}，Q = 7
> **输出:**在索引 4
> 处删除间隔后，最大覆盖率为 7 当删除最后一个间隔时，我们能够使用剩余的间隔
> {1，2，3，4，5，6，7}覆盖给定的点，这是最大可能的覆盖率。
> (如果去掉区间{4，5}或{5，6}，答案也会一样)
> **输入:**区间[][] = {{3，3}，{2，2}，{3，4}}，Q = 4
> **输出:**在索引 0
> 去掉区间后最大覆盖率为 3

**进场:**

*   首先使用大小为 **n + 1** 的数组**标记[]** 。如果**标记【I】= k**，这意味着精确的 **k** 间隔中有点 **i** 。
*   保持计数，所有间隔覆盖的数字总数。
*   现在我们必须遍历所有的区间，检查每个区间是否被删除，然后从计数中删除多少个数字。
*   为了在删除每个间隔后检查新的计数，我们需要维护一个数组 **count1[]** ，其中 **count1[i]** 告诉从 **1** 到 **i** 有多少个数字恰好在一个间隔中出现。
*   任何间隔的新计数将是**计数–(计数 1[r]–计数 1[l-1])** 。因为只有那些恰好出现在一个时间间隔内并且属于**【l，r】**的数字必须从实际计数中排除。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function To find the required interval
void solve(int interval[][2], int N, int Q)
{
    int Mark[Q] = { 0 };
    for (int i = 0; i < N; i++) {
        int l = interval[i][0] - 1;
        int r = interval[i][1] - 1;
        for (int j = l; j <= r; j++)
            Mark[j]++;
    }

    // Total Count of covered numbers
    int count = 0;
    for (int i = 0; i < Q; i++) {
        if (Mark[i])
            count++;
    }

    // Array to store numbers that occur
    // exactly in one interval till ith interval
    int count1[Q] = { 0 };
    if (Mark[0] == 1)
        count1[0] = 1;
    for (int i = 1; i < Q; i++) {
        if (Mark[i] == 1)
            count1[i] = count1[i - 1] + 1;
        else
            count1[i] = count1[i - 1];
    }

    int maxindex;
    int maxcoverage = 0;
    for (int i = 0; i < N; i++) {
        int l = interval[i][0] - 1;
        int r = interval[i][1] - 1;

        // Calculate New count by removing all numbers
        // in range [l, r] occurring exactly once
        int elem1;
        if (l != 0)
            elem1 = count1[r] - count1[l - 1];
        else
            elem1 = count1[r];
        if (count - elem1 >= maxcoverage) {
            maxcoverage = count - elem1;
            maxindex = i;
        }
    }
    cout << "Maximum Coverage is " << maxcoverage
         << " after removing interval at index "
         << maxindex;
}

// Driver code
int main()
{
    int interval[][2] = { { 1, 4 },
                          { 4, 5 },
                          { 5, 6 },
                          { 6, 7 },
                          { 3, 5 } };
    int N = sizeof(interval) / sizeof(interval[0]);
    int Q = 7;
    solve(interval, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function To find the required interval
static void solve(int interval[][], int N, int Q)
{
    int Mark[] = new int[Q];
    for (int i = 0; i < N; i++)
    {
        int l = interval[i][0] - 1;
        int r = interval[i][1] - 1;
        for (int j = l; j <= r; j++)
            Mark[j]++;
    }

    // Total Count of covered numbers
    int count = 0;
    for (int i = 0; i < Q; i++)
    {
        if (Mark[i] != 0)
            count++;
    }

    // Array to store numbers that occur
    // exactly in one interval till ith interval
    int count1[] = new int[Q];
    if (Mark[0] == 1)
        count1[0] = 1;
    for (int i = 1; i < Q; i++)
    {
        if (Mark[i] == 1)
            count1[i] = count1[i - 1] + 1;
        else
            count1[i] = count1[i - 1];
    }

    int maxindex = 0;
    int maxcoverage = 0;
    for (int i = 0; i < N; i++)
    {
        int l = interval[i][0] - 1;
        int r = interval[i][1] - 1;

        // Calculate New count by removing all numbers
        // in range [l, r] occurring exactly once
        int elem1;
        if (l != 0)
            elem1 = count1[r] - count1[l - 1];
        else
            elem1 = count1[r];
        if (count - elem1 >= maxcoverage)
        {
            maxcoverage = count - elem1;
            maxindex = i;
        }
    }
    System.out.println("Maximum Coverage is " + maxcoverage
        + " after removing interval at index "
        + maxindex);
}

// Driver code
public static void main(String[] args)
{
        int interval[][] = { { 1, 4 },
                        { 4, 5 },
                        { 5, 6 },
                        { 6, 7 },
                        { 3, 5 } };
    int N = interval.length;
    int Q = 7;
    solve(interval, N, Q);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function To find the required interval
def solve(interval, N, Q):

    Mark = [0 for i in range(Q)]
    for i in range(N):
        l = interval[i][0] - 1
        r = interval[i][1] - 1
        for j in range(l, r + 1):
            Mark[j] += 1

    # Total Count of covered numbers
    count = 0
    for i in range(Q):
        if (Mark[i]):
            count += 1

    # Array to store numbers that occur
    # exactly in one interval till ith interval
    count1 = [0 for i in range(Q)]
    if (Mark[0] == 1):
        count1[0] = 1
    for i in range(1, Q):
        if (Mark[i] == 1):
            count1[i] = count1[i - 1] + 1
        else:
            count1[i] = count1[i - 1]

    maxindex = 0
    maxcoverage = 0
    for i in range(N):
        l = interval[i][0] - 1
        r = interval[i][1] - 1

        # Calculate New count by removing all numbers
        # in range [l, r] occurring exactly once
        elem1 = 0
        if (l != 0):
            elem1 = count1[r] - count1[l - 1]
        else:
            elem1 = count1[r]
        if (count - elem1 >= maxcoverage):
            maxcoverage = count - elem1
            maxindex = i

    print("Maximum Coverage is", maxcoverage,
          "after removing interval at index", maxindex)

# Driver code
interval = [[ 1, 4 ],
            [ 4, 5 ],
            [ 5, 6 ],
            [ 6, 7 ],
            [ 3, 5 ]]
N = len(interval)
Q = 7
solve(interval, N, Q)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function To find the required interval
static void solve(int[,] interval, int N, int Q)
{
    int[] Mark = new int[Q];
    for (int i = 0; i < N; i++)
    {
        int l = interval[i,0] - 1;
        int r = interval[i,1] - 1;
        for (int j = l; j <= r; j++)
            Mark[j]++;
    }

    // Total Count of covered numbers
    int count = 0;
    for (int i = 0; i < Q; i++)
    {
        if (Mark[i] != 0)
            count++;
    }

    // Array to store numbers that occur
    // exactly in one interval till ith interval
    int[] count1 = new int[Q];
    if (Mark[0] == 1)
        count1[0] = 1;
    for (int i = 1; i < Q; i++)
    {
        if (Mark[i] == 1)
            count1[i] = count1[i - 1] + 1;
        else
            count1[i] = count1[i - 1];
    }

    int maxindex = 0;
    int maxcoverage = 0;
    for (int i = 0; i < N; i++)
    {
        int l = interval[i,0] - 1;
        int r = interval[i,1] - 1;

        // Calculate New count by removing all numbers
        // in range [l, r] occurring exactly once
        int elem1;
        if (l != 0)
            elem1 = count1[r] - count1[l - 1];
        else
            elem1 = count1[r];
        if (count - elem1 >= maxcoverage)
        {
            maxcoverage = count - elem1;
            maxindex = i;
        }
    }
    Console.WriteLine("Maximum Coverage is " + maxcoverage
        + " after removing interval at index "
        + maxindex);
}

// Driver code
public static void Main()
{
    int[,] interval = { { 1, 4 },
                    { 4, 5 },
                    { 5, 6 },
                    { 6, 7 },
                    { 3, 5 } };
    int N = interval.Length;

    int Q = 7;
    solve(interval, N/2, Q);
}
}

/* This code contributed by Code_Mech */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function To find the required interval
function solve(interval, N, Q)
{
    var Mark = Array(Q).fill(0);
    for (var i = 0; i < N; i++) {
        var l = interval[i][0] - 1;
        var r = interval[i][1] - 1;
        for (var j = l; j <= r; j++)
            Mark[j]++;
    }

    // Total Count of covered numbers
    var count = 0;
    for (var i = 0; i < Q; i++) {
        if (Mark[i])
            count++;
    }

    // Array to store numbers that occur
    // exactly in one interval till ith interval
    var count1 = Array(Q).fill(0);
    if (Mark[0] == 1)
        count1[0] = 1;
    for (var i = 1; i < Q; i++) {
        if (Mark[i] == 1)
            count1[i] = count1[i - 1] + 1;
        else
            count1[i] = count1[i - 1];
    }

    var maxindex;
    var maxcoverage = 0;
    for (var i = 0; i < N; i++) {
        var l = interval[i][0] - 1;
        var r = interval[i][1] - 1;

        // Calculate New count by removing all numbers
        // in range [l, r] occurring exactly once
        var elem1;
        if (l != 0)
            elem1 = count1[r] - count1[l - 1];
        else
            elem1 = count1[r];
        if (count - elem1 >= maxcoverage) {
            maxcoverage = count - elem1;
            maxindex = i;
        }
    }
    document.write( "Maximum Coverage is " + maxcoverage
         + " after removing interval at index "
         + maxindex);
}

// Driver code
var interval = [ [ 1, 4 ],
                      [ 4, 5 ],
                      [ 5, 6 ],
                      [ 6, 7 ],
                      [ 3, 5 ] ];
var N = interval.length;
var Q = 7;
solve(interval, N, Q);

</script>
```

**Output:** 

```
Maximum Coverage is 7 after removing interval at index 4
```