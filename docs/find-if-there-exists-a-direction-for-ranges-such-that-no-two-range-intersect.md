# 查找范围是否存在方向，使得没有两个范围相交

> 原文:[https://www . geesforgeks . org/find-if-exists-a-direction-for-ranges-so-no-two-ranges-intersect/](https://www.geeksforgeeks.org/find-if-there-exists-a-direction-for-ranges-such-that-no-two-range-intersect/)

给定 **N** 范围**【左，右】**速度**等级【】**。任务是给每个范围分配一个方向，即**左**或**右**。所有范围将在 **t = 0** 时开始向指定方向移动。如果在无限时间内没有两个范围重叠，那么找到方向的赋值是可能的。
**示例:**

> **输入:**范围[][] = {{1，2}、{2，5}、{3，10}、{4，4}、{5，7}}、
> 等级[] = {3，1，1，1，10}
> T4】输出:无
> 间隔{2，5}、{3，10 }和{4，4}共享一个公共点 4
> 并具有相同的速度。
> **输入:**范围[][] = {{1，2}，{2，5}，{3，10}，{4，4}，{5，7}}，
> vel[] = {3，1，11，1，10}
> **输出:**是

**进场:**

*   在无限时间内，如果有两个速度不同的距离，那么无论它们的方向如何，它们永远不会重叠，因为速度较大的距离总是在速度较慢的距离之前。
*   现在，考虑速度相同的范围。如果存在一个点位于至少 3 个具有相同速度的范围内，则不可能分配方向，因为即使这些范围中的两个被分配了不同的方向，但是第三个范围肯定会与具有相同方向的任何一个其他范围相交。
*   所以，对于所有的速度，找出是否存在至少 3 个范围，使得它们共享一个公共点，如果是，那么分配是不可能的。否则是有可能的。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define MAX 100001
using namespace std;

// Structure to hold details of
// each interval
typedef struct
{
    int l, r, v;
} interval;

// Comparator to sort intervals
// based on velocity
bool cmp(interval a, interval b)
{
    return a.v < b.v;
}

// Function that returns true if the
// assignment of directions is possible
bool isPossible(int range[][3], int N)
{
    interval test[N];
    for (int i = 0; i < N; i++) {
        test[i].l = range[i][0];
        test[i].r = range[i][1];
        test[i].v = range[i][2];
    }

    // Sort the intervals based on velocity
    sort(test, test + N, cmp);

    for (int i = 0; i < N; i++) {
        int count[MAX] = { 0 };
        int current_velocity = test[i].v;

        int j = i;

        // Test the condition for all intervals
        // with same velocity
        while (j < N && test[j].v == current_velocity) {
            for (int k = test[j].l; k <= test[j].r; k++) {
                count[k]++;

                // If for any velocity, 3 or more intervals
                // share a common point return false
                if (count[k] >= 3)
                    return false;
            }
            j++;
        }

        i = j - 1;
    }

    return true;
}

// Driver code
int main()
{
    int range[][3] = { { 1, 2, 3 },
                       { 2, 5, 1 },
                       { 3, 10, 1 },
                       { 4, 4, 1 },
                       { 5, 7, 10 } };
    int n = sizeof(range) / sizeof(range[0]);

    if (isPossible(range, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 100001;

// Structure to hold details of
// each interval
static class interval
{
    int l, r, v;
}

static class Sort implements Comparator<interval>
{
    // Comparator to sort intervals
    // based on velocity
    public int compare(interval a, interval b)
    {
        return (a.v < b.v ? 1 : 0);
    }
}

// Function that returns true if the
// assignment of directions is possible
static boolean isPossible(int range[][], int N)
{
    interval test[] = new interval[N];
    for (int i = 0; i < N; i++)
    {
        test[i] = new interval();
        test[i].l = range[i][0];
        test[i].r = range[i][1];
        test[i].v = range[i][2];
    }

    // Sort the intervals based on velocity
    Arrays.sort(test, new Sort());

    for (int i = 0; i < N; i++)
    {
        int count[] = new int[MAX];
        int current_velocity = test[i].v;

        int j = i;

        // Test the condition for all intervals
        // with same velocity
        while (j < N && test[j].v == current_velocity)
        {
            for (int k = test[j].l; k <= test[j].r; k++)
            {
                count[k]++;

                // If for any velocity, 3 or more intervals
                // share a common point return false
                if (count[k] >= 3)
                    return false;
            }
            j++;
        }
        i = j - 1;
    }
    return true;
}

// Driver code
public static void main(String args[])
{
    int range[][] = {{ 1, 2, 3 },
                     { 2, 5, 1 },
                     { 3, 10, 1 },
                     { 4, 4, 1 },
                     { 5, 7, 10 }};
    int n = range.length;

    if (isPossible(range, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python implementation of the approach
MAX = 100001

# Function that returns true if the
# assignment of directions is possible
def isPossible(rangee, N):

    # Structure to hold details of
    # each interval
    test = [[0 for x in range(3)] for x in range(N)]
    for i in range(N):
        test[i][0] = rangee[i][0]
        test[i][1] = rangee[i][1]
        test[i][2] = rangee[i][2]

    # Sort the intervals based on velocity
    test.sort(key = lambda x: x[2])
    for i in range(N):
        count = [0] * MAX
        current_velocity = test[i][2]
        j = i

        # Test the condition for all intervals
        # with same velocity
        while (j < N and test[j][2] == current_velocity):
            for k in range(test[j][0], test[j][1] + 1):
                count[k] += 1

                # If for any velocity, 3 or more intervals
                # share a common poreturn false
                if (count[k] >= 3):
                    return False
            j += 1
        i = j - 1

    return True

# Driver code
rangee = [[1, 2, 3] ,[2, 5, 1] ,[3, 10, 1],
        [4, 4, 1 ],[5, 7, 10 ]]
n = len(rangee)
if (isPossible(rangee, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Structure to hold details of
// each interval
public class interval
{
    public int l, r, v;
}

public class sortHelper : IComparer<interval>
{
   public int Compare(interval a, interval b)
   {
      return (a.v < b.v ? 1 : 0);
   }
}

static int MAX = 100001;

// Function that returns true if the
// assignment of directions is possible
static bool isPossible(int [,]range, int N)
{
    interval []test = new interval[N];
    for (int i = 0; i < N; i++)
    {
        test[i] = new interval();
        test[i].l = range[i, 0];
        test[i].r = range[i, 1];
        test[i].v = range[i, 2];
    }

    // Sort the intervals based on velocity
    Array.Sort(test, new sortHelper());

    for (int i = 0; i < N; i++)
    {
        int []count = new int[MAX];
        int current_velocity = test[i].v;

        int j = i;

        // Test the condition for all intervals
        // with same velocity
        while (j < N && test[j].v == current_velocity)
        {
            for (int k = test[j].l; k <= test[j].r; k++)
            {
                count[k]++;

                // If for any velocity, 3 or more intervals
                // share a common point return false
                if (count[k] >= 3)
                    return false;
            }
            j++;
        }
        i = j - 1;
    }
    return true;
}

// Driver code
public static void Main(string []args)
{
    int [,]range = {{ 1, 2, 3 },
                     { 2, 5, 1 },
                     { 3, 10, 1 },
                     { 4, 4, 1 },
                     { 5, 7, 10 }};

    int n = range.GetLength(0);

    if (isPossible(range, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let MAX = 100001;

// Structure to hold details of
// each interval
class interval
{
    constructor()
    {
        this.l = this.r = this.v = 0;
    }
}

// Function that returns true if the
// assignment of directions is possible
function isPossible(range,N)
{
    let test = new Array(N);
    for (let i = 0; i < N; i++)
    {
        test[i] = new interval();
        test[i].l = range[i][0];
        test[i].r = range[i][1];
        test[i].v = range[i][2];
    }

    // Sort the intervals based on velocity
    test.sort(function(a,b){return (a.v < b.v ? 1 : 0);});

    for (let i = 0; i < N; i++)
    {
        let count = new Array(MAX);
        for(let i=0;i<MAX;i++)
            count[i]=0;
        let current_velocity = test[i].v;

        let j = i;

        // Test the condition for all intervals
        // with same velocity
        while (j < N && test[j].v == current_velocity)
        {
            for (let k = test[j].l; k <= test[j].r; k++)
            {
                count[k]++;

                // If for any velocity, 3 or more intervals
                // share a common point return false
                if (count[k] >= 3)
                    return false;
            }
            j++;
        }
        i = j - 1;
    }
    return true;
}

// Driver code
let range=[[ 1, 2, 3 ],
                     [ 2, 5, 1 ],
                     [ 3, 10, 1 ],
                     [ 4, 4, 1 ],
                     [ 5, 7, 10 ]]
let n = range.length;

if (isPossible(range, n))
    document.write("Yes<br>");
else
    document.write("No<br>");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
No
```