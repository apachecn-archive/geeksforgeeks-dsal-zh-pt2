# N 个给定线段中任何一个可能的最大交叉数

> 原文:[https://www . geesforgeks . org/n 个给定段中任何一个可能的最大交叉数/](https://www.geeksforgeeks.org/maximum-number-of-intersections-possible-for-any-of-the-n-given-segments/)

给定一个由 **N** 对类型 **{L，R}** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，每个数组代表 **X** 轴上的一个线段，任务是找到一个线段与其他线段的最大交点数。

**示例:**

> **输入:** arr[] = {{1，6}，{5，5}，{2，3}}
> **输出:** 2
> **说明:**
> 下面是与其他分段重叠的每个分段的计数:
> 
> 1.  第一个线段[1，6]与 2 个线段[5，5]和[2，3]相交。
> 2.  第二段[5，5]与第一段[1，6]相交。
> 3.  第三段[2，3]与第一段[1，6]相交。
> 
> 因此，所有线段之间的最大交点数为 2。
> 
> **输入:** arr[][] = {{4，8}，{3，6}，{7，11}，{9，10}}
> **输出:** 2

**天真方法:**解决给定问题的最简单方法是迭代所有线段，并通过与所有其他线段进行检查来计算每个线段的交点数，然后打印获得的所有交点数中的最大值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   上述方法可以通过遍历每个线段并使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)计算不与当前线段相交的线段数来进行优化，并从中找出与当前线段相交的线段数
*   假设**【L，R】**为当前线段，**【P，Q】**为另一线段，那么如果 **Q < L** 或 **P > R** 则线段**【L，R】**不与线段**【P，Q】**相交。
*   假设 **X** 为未与线段**【L，R】**相交的线段数，则与线段**【L，R】相交的线段数=(N–1–X)**。

按照以下步骤解决问题:

*   将线段的所有左点存储在一个[数组中](https://www.geeksforgeeks.org/introduction-to-arrays/)表示 **L[]** ，数组中线段的所有右点表示 **R[]** 。
*   [将阵列 **L[]** 和 **R[]** 按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化一个变量，说**计数**为 **0** 来存储一个线段的最大交点的计数。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下步骤:
    *   使用[下界()](https://www.geeksforgeeks.org/binary-search-functions-in-c-stl-binary_search-lower_bound-and-upper_bound/)计算当前线段 **{arr[i][0]，arr[i][1]}** 剩余的线段数，并将其存储在一个变量中，比如 **cnt** 。
    *   使用[上界()](https://www.geeksforgeeks.org/upper_bound-in-cpp/)计算当前线段 **{arr[i][0]，arr[i][1]}** 的线段数，并以此增加 **cnt** 的计数。
    *   更新**计数**的值，作为**计数**和**(N–CNT–1)**的最大值。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of intersections one segment has with
// all the other given segments
int maximumIntersections(int arr[][2],
                         int N)
{
    // Stores the resultant maximum count
    int count = 0;

    // Stores the starting and the
    // ending points
    int L[N], R[N];

    for (int i = 0; i < N; i++) {
        L[i] = arr[i][0];
        R[i] = arr[i][1];
    }

    // Sort arrays points in the
    // ascending order
    sort(L, L + N);
    sort(R, R + N);

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        int l = arr[i][0];
        int r = arr[i][1];

        // Find the count of segments
        // on left of ith segment
        int x = lower_bound(R, R + N, l) - R;

        // Find the count of segments
        // on right of ith segment
        int y = N - (upper_bound(L, L + N, r) - L);

        // Find the total segments not
        // intersecting with the current
        // segment
        int cnt = x + y;

        // Store the count of segments
        // that intersect with the
        // ith segment
        cnt = N - cnt - 1;

        // Update the value of count
        count = max(count, cnt);
    }

    // Return  the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[][2] = { { 1, 6 }, { 5, 5 }, { 2, 3 } };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumIntersections(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.util.*;

class GFG
{static int lower_bound(int[] a, int low, int high, long element)
    {
        while(low < high)
        {
            int middle = low + (high - low) / 2;
            if(element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }
static int maximumIntersections(int [][]arr,
                         int N)
{
    // Stores the resultant maximum count
    int count = 0;

    // Stores the starting and the
    // ending points
    int[] L = new int[N];
    int[] R = new int[N];
    for (int i = 0; i < N; i++) {
        L[i] = arr[i][0];
        R[i] = arr[i][1];
    }

    // Sort arrays points in the
    // ascending order
    Arrays.sort(L);
    Arrays.sort(R);

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        int l = arr[i][0];
        int r = arr[i][1];

        // Find the count of segments
        // on left of ith segment
        int x = lower_bound(L, 0,N, l);

        // Find the count of segments
        // on right of ith segment
        int y = N-lower_bound(R, 0,N, r+1);

        // Find the total segments not
        // intersecting with the current
        // segment
        int cnt = x + y;

        // Store the count of segments
        // that intersect with the
        // ith segment
        cnt = N - cnt - 1;

        // Update the value of count
        count = Math.max(count, cnt);
    }

    // Return  the resultant count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[][] = { { 1, 6 }, { 5, 5 }, { 2, 3 } };
    int N = arr.length;
    System.out.println(maximumIntersections(arr, N));
}
}

// This code is contributed by stream_cipher.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from bisect import bisect_left, bisect_right

def lower_bound(a, low, high, element):

    while(low < high):

        middle = low + (high - low) // 2
        if(element > a[middle]):
            low = middle + 1
        else:
            high = middle

    return low

# Function to find the maximum number
# of intersections one segment has with
# all the other given segments
def maximumIntersections(arr,
                         N):

    # Stores the resultant maximum count
    count = 0

    # Stores the starting and the
    # ending points
    L = [0]*N
    R = [0]*N

    for i in range(N):
        L[i] = arr[i][0]
        R[i] = arr[i][1]

    # Sort arrays points in the
    # ascending order
    L.sort()
    R.sort()

    # Traverse the array arr[]
    for i in range(N):
        l = arr[i][0]
        r = arr[i][1]

        # Find the count of segments
        # on left of ith segment
        x = lower_bound(L, 0, N, l)

        # Find the count of segments
        # on right of ith segment
        y = N-lower_bound(R, 0, N, r+1)

        # Find the total segments not
        # intersecting with the current
        # segment
        cnt = x + y

        # Store the count of segments
        # that intersect with the
        # ith segment
        cnt = N - cnt - 1

        # Update the value of count
        count = max(count, cnt)

    # Return  the resultant count
    return count

# Driver Code
if __name__ == "__main__":

    arr = [[1, 6], [5, 5], [2, 3]]
    N = len(arr)
    print(maximumIntersections(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int lower_bound(int[] a, int low,
                       int high, long element)
{
    while(low < high)
    {
        int middle = low + (high - low) / 2;

        if (element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

static int maximumIntersections(int [,]arr,
                                int N)
{

    // Stores the resultant maximum count
    int count = 0;

    // Stores the starting and the
    // ending points
    int[] L = new int[N];
    int[] R = new int[N];
    for(int i = 0; i < N; i++)
    {
        L[i] = arr[i, 0];
        R[i] = arr[i, 1];
    }

    // Sort arrays points in the
    // ascending order
    Array.Sort(L);
    Array.Sort(R);

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        int l = arr[i, 0];
        int r = arr[i, 1];

        // Find the count of segments
        // on left of ith segment
        int x = lower_bound(L, 0, N, l);

        // Find the count of segments
        // on right of ith segment
        int y = N-lower_bound(R, 0, N, r + 1);

        // Find the total segments not
        // intersecting with the current
        // segment
        int cnt = x + y;

        // Store the count of segments
        // that intersect with the
        // ith segment
        cnt = N - cnt - 1;

        // Update the value of count
        count = Math.Max(count, cnt);
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int [,]arr = new int[3, 2]{ { 1, 6 },
                                { 5, 5 },
                                { 2, 3 } };
    int N = 3;

    Console.Write(maximumIntersections(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach
function lower_bound(a, low, high, element)
{
    while(low < high)
    {
        let middle = low + Math.floor(
            (high - low) / 2);

        if (element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Function to find the maximum number
// of intersections one segment has with
// all the other given segments
function maximumLetersections(arr, N)
{

    // Stores the resultant maximum count
    let count = 0;

    // Stores the starting and the
    // ending polets
    let L = Array.from({length: N}, (_, i) => 0);
    let R = Array.from({length: N}, (_, i) => 0);
    for(let i = 0; i < N; i++)
    {
        L[i] = arr[i][0];
        R[i] = arr[i][1];
    }

    // Sort arrays polets in the
    // ascending order
    L.sort();
    R.sort();

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {
        let l = arr[i][0];
        let r = arr[i][1];

        // Find the count of segments
        // on left of ith segment
        let x = lower_bound(L, 0, N, l);

        // Find the count of segments
        // on right of ith segment
        let y = N-lower_bound(R, 0, N, r + 1);

        // Find the total segments not
        // letersecting with the current
        // segment
        let cnt = x + y;

        // Store the count of segments
        // that letersect with the
        // ith segment
        cnt = N - cnt - 1;

        // Update the value of count
        count = Math.max(count, cnt);
    }

    // Return the resultant count
    return count;
}

// Driver Code
let arr = [ [ 1, 6 ], [ 5, 5 ], [ 2, 3 ] ];
let N = arr.length;

document.write(maximumLetersections(arr, N));

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*