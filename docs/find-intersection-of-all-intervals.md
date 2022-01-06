# 查找所有区间的交集

> 原文:[https://www . geesforgeks . org/find-所有区间的交集/](https://www.geeksforgeeks.org/find-intersection-of-all-intervals/)

给定**【l，r】**形式的 **N** 区间，任务是找到所有区间的交集。交点是位于所有给定区间内的区间。如果不存在这样的交集，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {{1，6}、{2，8}、{3，10}、{5，8}}
> **输出:**【5，6】
> 【5，6】是所有给定区间中的公共区间。
> **输入:** arr[] = {{1，6}，{8，18}}
> **输出:** -1
> 两个给定范围之间不存在交集。

**进场:**

*   首先，将第一个区间视为所需答案。
*   现在，从第二个间隔开始，尝试搜索交叉点。可能会出现两种情况:
    1.  **【L1，R1】****【L2，R2】**之间不存在交集。只有当 **r1 < l2** 或 **r2 < l1** 时才有可能。在这种情况下，答案将是 **0** ，即不存在交集。
    2.  **【L1，R1】**和**【L2，R2】**之间存在交集。那么所需的交叉路口将是**【最大(l1，l2)，最小(r1，R2)】**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the intersection
void findIntersection(int intervals[][2], int N)
{
    // First interval
    int l = intervals[0][0];
    int r = intervals[0][1];

    // Check rest of the intervals and find the intersection
    for (int i = 1; i < N; i++) {

        // If no intersection exists
        if (intervals[i][0] > r || intervals[i][1] < l) {
            cout << -1;
            return;
        }

        // Else update the intersection
        else {
            l = max(l, intervals[i][0]);
            r = min(r, intervals[i][1]);
        }
    }

    cout << "[" << l << ", " << r << "]";
}

// Driver code
int main()
{
    int intervals[][2] = {
        { 1, 6 },
        { 2, 8 },
        { 3, 10 },
        { 5, 8 }
    };
    int N = sizeof(intervals) / sizeof(intervals[0]);
    findIntersection(intervals, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to print the intersection
static void findIntersection(int intervals[][], int N)
{
    // First interval
    int l = intervals[0][0];
    int r = intervals[0][1];

    // Check rest of the intervals
    // and find the intersection
    for (int i = 1; i < N; i++)
    {

        // If no intersection exists
        if (intervals[i][0] > r ||
            intervals[i][1] < l)
        {
            System.out.println(-1);
            return;
        }

        // Else update the intersection
        else
        {
            l = Math.max(l, intervals[i][0]);
            r = Math.min(r, intervals[i][1]);
        }
    }
    System.out.println ("[" + l +", " + r + "]");
}

    // Driver code
    public static void main (String[] args)
    {

        int intervals[][] = {{ 1, 6 },
                            { 2, 8 },
                            { 3, 10 },
                            { 5, 8 }};
        int N = intervals.length;
        findIntersection(intervals, N);
    }
}

// This Code is contributed by ajit..
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to print the intersection
def findIntersection(intervals,N):

    # First interval
    l = intervals[0][0]
    r = intervals[0][1]

    # Check rest of the intervals
    # and find the intersection
    for i in range(1,N):

        # If no intersection exists
        if (intervals[i][0] > r or intervals[i][1] < l):
            print(-1)

        # Else update the intersection
        else:
            l = max(l, intervals[i][0])
            r = min(r, intervals[i][1])

    print("[",l,", ",r,"]")

# Driver code

intervals= [
            [ 1, 6 ],
            [ 2, 8 ],
            [ 3, 10 ],
            [ 5, 8 ]
            ]
N =len(intervals)
findIntersection(intervals, N)

# this code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the intersection
static void findIntersection(int [,]intervals, int N)
{
    // First interval
    int l = intervals[0, 0];
    int r = intervals[0, 1];

    // Check rest of the intervals
    // and find the intersection
    for (int i = 1; i < N; i++)
    {

        // If no intersection exists
        if (intervals[i, 0] > r ||
            intervals[i, 1] < l)
        {
            Console.WriteLine(-1);
            return;
        }

        // Else update the intersection
        else
        {
            l = Math.Max(l, intervals[i, 0]);
            r = Math.Min(r, intervals[i, 1]);
        }
    }
    Console.WriteLine("[" + l + ", " + r + "]");
}

// Driver code
public static void Main()
{
    int [,]intervals = {{ 1, 6 }, { 2, 8 },
                        { 3, 10 }, { 5, 8 }};
    int N = intervals.GetLength(0);
    findIntersection(intervals, N);
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the intersection
function findIntersection($intervals, $N)
{
    // First interval
    $l = $intervals[0][0];
    $r = $intervals[0][1];

    // Check rest of the intervals and
    // find the intersection
    for ($i = 1; $i < $N; $i++)
    {

        // If no intersection exists
        if ($intervals[$i][0] > $r ||
            $intervals[$i][1] < $l)
        {
            echo -1;
            return;
        }

        // Else update the intersection
        else
        {
            $l = max($l, $intervals[$i][0]);
            $r = min($r, $intervals[$i][1]);
        }
    }

    echo "[" . $l . ", " . $r . "]";
}

// Driver code
$intervals = array(array(1, 6), array(2, 8),
                   array(3, 10), array(5, 8));
$N = sizeof($intervals);
findIntersection($intervals, $N);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to print the intersection
    function findIntersection(intervals, N)
    {
        // First interval
        let l = intervals[0][0];
        let r = intervals[0][1];

        // Check rest of the intervals
        // and find the intersection
        for (let i = 1; i < N; i++)
        {

            // If no intersection exists
            if (intervals[i][0] > r ||
                intervals[i][1] < l)
            {
                document.write(-1 + "</br>");
                return;
            }

            // Else update the intersection
            else
            {
                l = Math.max(l, intervals[i][0]);
                r = Math.min(r, intervals[i][1]);
            }
        }
        document.write("[" + l +", " + r + "]" + "</br>");
    }

    let intervals = [[ 1, 6 ],
                     [ 2, 8 ],
                     [ 3, 10],
                     [ 5, 8 ]];
    let N = intervals.length;
    findIntersection(intervals, N);

</script>
```

**Output:** 

```
[5, 6]
```