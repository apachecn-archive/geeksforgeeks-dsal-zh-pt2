# 求两个列表给定区间的交集

> 原文:[https://www . geesforgeks . org/find-两个列表给出的区间交集/](https://www.geeksforgeeks.org/find-intersection-of-intervals-given-by-two-lists/)

给定两个**二维数组**，表示区间。每个二维数组代表一个区间列表。每个区间列表都是**不相交的**，并且按照递增的顺序排序。查找两个列表共有的交集或范围集。

> 分离意味着列表中没有常见的元素。示例:{1，4}和{5，6}不相交，而{1，4}和{2，5}不相交，因为 2、3 和 4 在两个区间都是公共的。

**例:**

> **输入:** arr1[][] = {{0，4}、{5，10}、{13，20}、{24，25}}
> arr2[][] = {{1，5}、{8，12}、{15，24}、{25，26}}
> **输出:** {{1，4}、{5，5}、{8，10}、{15，20}、{24，24}因此，{1，4}是理想的交叉点。同样，{24，24}完全位于两个区间{24，25}和{15，24}内。
> **输入:** arr1[][] = {{0，2}、{5，10}、{12，22}、{24，25}}
> arr2[][] = {{1，4}、{9，12}、{15，24}、{25，26}}
> **输出:** {{1，2}、{9，10}、{12，12}、{15，15 }因此，{1，2}是理想的交叉点。同样，{12，12}完全位于两个区间{12，22}和{9，12}内。

**进场:**
解决上述问题，可采用[两指针手法](https://www.geeksforgeeks.org/two-pointers-technique/)，步骤如下:

*   维护 [**两个指针**](https://www.geeksforgeeks.org/two-pointers-technique/) i 和 j 分别遍历两个区间列表 arr1 和 arr2。
*   现在，如果 arr1[i]有最小端点，它只能与 arr2[j]相交。同样，如果 arr2[j]有最小端点，它只能与 arr1[i]相交。如果发生相交，找到相交的线段。
*   [l，r]将是相交线段 iff l <= r, where **l = max(arr1[i][0]、arr2[j][0])** 和 **r = min(arr1[i][1]、arr2[j][1])** 。
*   相应地增加 I 和 j 指针以向前移动。

以下是实施办法:

## C++

```
// C++ implementation to find the
// intersection of the two intervals

#include <bits/stdc++.h>
using namespace std;

// Function to print intersecting intervals
void printIntervals(vector<vector<int> > arr1,
                    vector<vector<int> > arr2)
{

    // i and j pointers for
    // arr1 and arr2 respectively
    int i = 0, j = 0;

    // Size of the two lists
    int n = arr1.size(), m = arr2.size();

    // Loop through all intervals unless
    // one of the interval gets exhausted
    while (i < n && j < m) {
        // Left bound for intersecting segment
        int l = max(arr1[i][0], arr2[j][0]);

        // Right bound for intersecting segment
        int r = min(arr1[i][1], arr2[j][1]);

        // If segment is valid print it
        if (l <= r)
            cout << "{" << l << ", "
                 << r << "}\n";

        // If i-th interval's right
        // bound is smaller
        // increment i else
        // increment j
        if (arr1[i][1] < arr2[j][1])
            i++;
        else
            j++;
    }
}

// Driver code
int main()
{

    vector<vector<int> > arr1
        = { { 0, 4 }, { 5, 10 },
            { 13, 20 }, { 24, 25 } };

    vector<vector<int> > arr2
        = { { 1, 5 }, { 8, 12 },
            { 15, 24 }, { 25, 26 } };

    printIntervals(arr1, arr2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// intersecting intervals
class GFG{

// Function to print intersecting intervals
static void printIntervals(int arr1[][],
                           int arr2[][])
{

    // i and j pointers for arr1 and
    // arr2 respectively
    int i = 0, j = 0;

    int n = arr1.length, m = arr2.length;

    // Loop through all intervals unless 
    // one of the interval gets exhausted
    while (i < n && j < m)
    {

        // Left bound for intersecting segment
        int l = Math.max(arr1[i][0], arr2[j][0]);

        // Right bound for intersecting segment
        int r = Math.min(arr1[i][1], arr2[j][1]);

        // If segment is valid print it
        if (l <= r)
            System.out.println("{" + l + ", " +
                                 r + "}");

        // If i-th interval's right bound is
        // smaller increment i else increment j
        if (arr1[i][1] < arr2[j][1])
            i++;
        else
            j++;
    }
}

// Driver code
public static void main(String[] args)
{
    int arr1[][] = { { 0, 4 }, { 5, 10 },
                     { 13, 20 }, { 24, 25 } };

    int arr2[][] = { { 1, 5 }, { 8, 12 },
                     { 15, 24 }, { 25, 26 } };

    printIntervals(arr1, arr2);
}
}

// This code is contributed by sarthak_eddy
```

## 蟒蛇 3

```
# Python3 implementation to find
# intersecting intervals

# Function to print intersecting
# intervals
def printIntervals(arr1, arr2):

    # i and j pointers for arr1
    # and arr2 respectively
    i = j = 0

    n = len(arr1)
    m = len(arr2)

    # Loop through all intervals unless one
    # of the interval gets exhausted
    while i < n and j < m:

        # Left bound for intersecting segment
        l = max(arr1[i][0], arr2[j][0])

        # Right bound for intersecting segment
        r = min(arr1[i][1], arr2[j][1])

        # If segment is valid print it
        if l <= r:
            print('{', l, ',', r, '}')

        # If i-th interval's right bound is
        # smaller increment i else increment j
        if arr1[i][1] < arr2[j][1]:
            i += 1
        else:
            j += 1

# Driver code
arr1 = [ [ 0, 4 ], [ 5, 10 ],
         [ 13, 20 ], [ 24, 25 ] ]

arr2 = [ [ 1, 5 ], [ 8, 12 ],
         [ 15, 24 ], [ 25, 26 ] ]

printIntervals(arr1, arr2)

# This code is contributed by sarthak_eddy
```

## C#

```
// C# implementation to find
// intersecting intervals
using System;
class GFG{

// Function to print intersecting intervals
static void printIntervals(int [,]arr1,
                           int [,]arr2)
{

    // i and j pointers for arr1 and
    // arr2 respectively
    int i = 0, j = 0;

    int n = arr1.GetLength(0),
        m = arr2.GetLength(0);

    // Loop through all intervals unless
    // one of the interval gets exhausted
    while (i < n && j < m)
    {

        // Left bound for intersecting segment
        int l = Math.Max(arr1[i, 0], arr2[j, 0]);

        // Right bound for intersecting segment
        int r = Math.Min(arr1[i, 1], arr2[j, 1]);

        // If segment is valid print it
        if (l <= r)
        Console.WriteLine("{" + l + ", " +
                            r + "}");

        // If i-th interval's right bound is
        // smaller increment i else increment j
        if (arr1[i, 1] < arr2[j, 1])
            i++;
        else
            j++;
    }
}

// Driver code
public static void Main(String[] args)
{
    int [,]arr1 = { { 0, 4 }, { 5, 10 },
                    { 13, 20 }, { 24, 25 } };

    int [,]arr2 = { { 1, 5 }, { 8, 12 },
                    { 15, 24 }, { 25, 26 } };

    printIntervals(arr1, arr2);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation to find
// intersecting intervals
// Function to print intersecting intervals
function printIntervals(arr1, arr2)
{

    // i and j pointers for arr1 and
    // arr2 respectively
    var i = 0, j = 0;

    var n = arr1.length, m = arr2.length;

    // Loop through all intervals unless 
    // one of the interval gets exhausted
    while (i < n && j < m)
    {

        // Left bound for intersecting segment
        var l = Math.max(arr1[i][0], arr2[j][0]);

        // Right bound for intersecting segment
        var r = Math.min(arr1[i][1], arr2[j][1]);

        // If segment is valid print it
        if (l <= r)
            document.write("{" + l + ", " +
                                 r + "}" + "<br>");

        // If i-th interval's right bound is
        // smaller increment i else increment j
        if (arr1[i][1] < arr2[j][1])
            i++;
        else
            j++;
    }
}

// Driver code
    var arr1 = [ [ 0, 4 ], [ 5, 10 ],
                     [ 13, 20 ], [ 24, 25 ] ];

    var arr2 = [ [ 1, 5 ], [ 8, 12 ],
                     [ 15, 24 ], [ 25, 26 ] ];

    printIntervals(arr1, arr2);

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
{1, 4}
{5, 5}
{8, 10}
{15, 20}
{24, 24}
{25, 25}
```

**时间复杂度:** O(N + M)，其中 N 和 M 是二维数组的长度
T3】辅助空间: O(1)