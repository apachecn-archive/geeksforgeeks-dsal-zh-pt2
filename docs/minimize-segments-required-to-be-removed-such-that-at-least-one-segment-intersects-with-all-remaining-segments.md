# 最小化需要移除的线段，使得至少一个线段与所有剩余线段相交

> 原文:[https://www . geesforgeks . org/minimum-segments-需要删除-这样-至少有一个段与所有剩余的段相交/](https://www.geeksforgeeks.org/minimize-segments-required-to-be-removed-such-that-at-least-one-segment-intersects-with-all-remaining-segments/)

给定一个由 **N** 对**【L，R】**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】【】**，其中 **L** 和 **R** 表示一个段的起始和结束索引，任务是找到必须从数组中删除的最小数量的段，使得剩余的数组包含至少一个与数组中存在的所有其他段相交的段。

**示例:**

> **输入:** arr[] = {{1，2}、{5，6}、{6，7}、{7，10}、{8，9}}
> **输出:** 2
> **说明:**删除分段{1，2}和{5，6}。因此，剩余的数组包含与所有其他段相交的段{7，10}。
> 
> **输入:** a[] = {{1，2}，{2，3}，{1，5}，{4，5}}
> **输出:** 0
> **解释:**线段{1，5}已经与所有其他剩余线段相交。因此，不需要删除任何片段。

**方法:**最大可能的答案是**(N–1)**，因为从**arr【】**中删除**(N–1)**段后，只剩下一段了。这条线段与自身相交。为了得到最少的答案，这个想法是迭代所有的线段，对于每个线段，检查不与它相交的线段的数量。

两段**【f<sub>1</sub>、s<sub>1</sub>**和**【f<sub>2</sub>、s<sub>2</sub>**仅在**最大值(f <sub>1</sub> 、f <sub>2</sub> ) ≤ min(s <sub>1</sub> 、s <sub>2</sub> )** 时相交。
因此，如果**f<sub>1</sub>，s<sub>1</sub>**与**f<sub>2</sub>，s<sub>2</sub>**不相交，那么只有两种可能:

1.  **s<sub>1</sub><f<sub>2</sub>**<sub>即段 1 在段 2 开始之前结束</sub>
2.  **f<sub>1</sub>T6<sub>s</sub>2**即段 1 在段 2 结束后开始。

按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，将每个线段的起点和终点分别存储在**起点[]** 和**终点[]** 中。
*   [按递增顺序对数组](https://www.geeksforgeeks.org/sort-c-stl/)、**起点[]** 和**终点[]** 进行排序。
*   将**和**初始化为**(N–1)**，以存储所需的最小删除次数。
*   再次遍历数组， **arr[]** ，对于每个段:
    *   分别在**左删除**和**右删除**中存储满足第一个和第二个不相交条件的线段数。
    *   如果 **leftDelete + rightDelete** 小于 **ans** ，则将 **ans** 设置为 **leftDelete + rightDelete** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of segments required to be deleted
void minSegments(pair<int, int> segments[],
                 int n)
{
    // Stores the start and end points
    int startPoints[n], endPoints[n];

    // Traverse segments and fill the
    // startPoints and endPoints
    for (int i = 0; i < n; i++) {
        startPoints[i] = segments[i].first;
        endPoints[i] = segments[i].second;
    }

    // Sort the startPoints
    sort(startPoints, startPoints + n);

    // Sort the startPoints
    sort(endPoints, endPoints + n);

    // Store the minimum number of
    // deletions required and
    // initialize with (N - 1)
    int ans = n - 1;

    // Traverse the array segments[]
    for (int i = 0; i < n; i++) {

        // Store the starting point
        int f = segments[i].first;

        // Store the ending point
        int s = segments[i].second;

        // Store the number of segments
        // satisfying the first condition
        // of non-intersection
        int leftDelete
            = lower_bound(endPoints,
                          endPoints + n, f)
              - endPoints;

        // Store the number of segments
        // satisfying the second condition
        // of non-intersection
        int rightDelete = max(
            0, n - (int)(upper_bound(startPoints,
                                     startPoints + n, s)
                         - startPoints));

        // Update answer
        ans = min(ans,
                  leftDelete
                      + rightDelete);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    pair<int, int> arr[] = {
        { 1, 2 }, { 5, 6 },
        { 6, 7 }, { 7, 10 }, { 8, 9 }
    };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minSegments(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Pair class
static class Pair
{
    int first;
    int second;

    Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

public static int lower_bound(int arr[], int key)
{
    int l = -1, r = arr.length;
    while (l + 1 < r)
    {
        int m = (l + r) >>> 1;
        if (arr[m] >= key)
            r = m;
        else
            l = m;
    }
    return r;
}

public static int upper_bound(int arr[], int key)
{
    int l = -1, r = arr.length;
    while (l + 1 < r)
    {
        int m = (l + r) >>> 1;
        if (arr[m] <= key)
            l = m;
        else
            r = m;
    }
    return l + 1;
}

// Function to find the minimum number
// of segments required to be deleted
static void minSegments(Pair segments[], int n)
{

    // Stores the start and end points
    int startPoints[] = new int[n];
    int endPoints[] = new int[n];

    // Traverse segments and fill the
    // startPoints and endPoints
    for(int i = 0; i < n; i++)
    {
        startPoints[i] = segments[i].first;
        endPoints[i] = segments[i].second;
    }

    // Sort the startPoints
    Arrays.sort(startPoints);

    // Sort the startPoints
    Arrays.sort(endPoints);

    // Store the minimum number of
    // deletions required and
    // initialize with (N - 1)
    int ans = n - 1;

    // Traverse the array segments[]
    for(int i = 0; i < n; i++)
    {

        // Store the starting point
        int f = segments[i].first;

        // Store the ending point
        int s = segments[i].second;

        // Store the number of segments
        // satisfying the first condition
        // of non-intersection
        int leftDelete = lower_bound(endPoints, f);

        // Store the number of segments
        // satisfying the second condition
        // of non-intersection
        int rightDelete = Math.max(
            0, n - (int)(upper_bound(startPoints, s)));

        // Update answer
        ans = Math.min(ans, leftDelete + rightDelete);
    }

    // Print the answer
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    Pair arr[] = { new Pair(1, 2), new Pair(5, 6),
                   new Pair(6, 7), new Pair(7, 10),
                   new Pair(8, 9) };
    int N = arr.length;

    // Function Call
    minSegments(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Pyhton3 program for the above approach

from bisect import bisect_left,bisect_right
# Function to find the minimum number
# of segments required to be deleted
def minSegments(segments, n):
    # Stores the start and end points
    startPoints = [0 for i in range(n)]
    endPoints = [0 for i in range(n)]

    # Traverse segments and fill the
    # startPoints and endPoints
    for i in range(n):
        startPoints[i] = segments[i][0]
        endPoints[i] = segments[i][1]

    # Sort the startPoints
    startPoints.sort(reverse = False)

    # Sort the startPoints
    endPoints.sort(reverse= False)

    # Store the minimum number of
    # deletions required and
    # initialize with (N - 1)
    ans = n - 1

    # Traverse the array segments[]
    for i in range(n):
        # Store the starting point
        f = segments[i][0]

        # Store the ending point
        s = segments[i][1]

        # Store the number of segments
        # satisfying the first condition
        # of non-intersection
        leftDelete = bisect_left(endPoints, f)

        # Store the number of segments
        # satisfying the second condition
        # of non-intersection
        rightDelete = max(0, n - bisect_right(startPoints,s))

        # Update answer
        ans = min(ans, leftDelete + rightDelete)

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':
    arr = [[1, 2],[5, 6], [6, 7],[7, 10],[8, 9]]
    N = len(arr)

    # Function Call
    minSegments(arr, N)

    # This code is contributed by ipg2016107.
```

**Output:** 

```
2
```

***时间复杂度:**O(N *(log N<sup>2</sup>)*
***辅助空间:** O(N)*