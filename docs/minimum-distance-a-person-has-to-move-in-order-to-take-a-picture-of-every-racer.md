# 一个人为了给每个参赛者拍照而必须移动的最小距离

> 原文:[https://www . geeksforgeeks . org/最小距离-一个人必须移动才能拍下每个参赛者的照片/](https://www.geeksforgeeks.org/minimum-distance-a-person-has-to-move-in-order-to-take-a-picture-of-every-racer/)

考虑一条直线跑道。有些选手在特定路段之间的赛道上跑步。一个人正在试着给每个参赛者拍照。如果一个人站在赛车手的跑道段之间，即赛车手的起点和终点之间，他可以给赛车手拍照。给定 **N** 参赛者的起点和终点，以及一个整数 **D** 表示拍照者的初始位置。任务是找到人必须移动的最小距离，以便从最后一点拍摄每个参赛者的照片。如果不可能拍下每一个赛车手的照片，那就打印 **-1** 。

**示例:**

> **输入:**开始[] = {0，2，4}，结束[] = {7，14，6}，D = 3
> **输出:** 1
> 分段为:
> 0。。。。。。7
> 。。2 .。。。。。。。。。。14
> 。。。。4 .6
> 。。。d
> 因此，人必须向 4 移动，即 1 个单位。
> 
> **输入:**开始[] = {1，2}，结束[] = {2，3}，D = 2
> **输出:** 0

**进场:**上述问题可以通过观察来解决，即该人必须在每位选手开始比赛并完成比赛之前领先。所以如果他在最后出发，最先结束的选手的范围内，他可以拍照，否则不行。
在所有给定的选手中找出起点的最大值说**左**和终点的最小值说**右**。现在，

*   **左>右**那么人就不可能拍照打印 **-1** 。
*   如果 **D** 在**【左、右】**范围内，则此人无需移动，答案为 **0** 。
*   否则该人必须移动**分钟(腹肌(左–D)，腹肌(右–D))**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// distance the person has to move
// int order to get the pictures
int minDistance(int start[], int end[], int n, int d)
{

    // To store the minimum ending point
    int left = INT_MIN;

    // To store the maximum starting point
    int right = INT_MAX;

    // Find the values of minSeg and maxSeg
    for (int i = 0; i < n; i++) {
        left = max(left, start[i]);
        right = min(right, end[i]);
    }

    // Impossible
    if (left > right)
        return -1;

    // The person doesn't need to move
    if (d >= left && d <= right)
        return 0;

    // Get closer to the left point
    if (d < left)
        return (left - d);

    // Get closer to the right point
    if (d > right)
        return (d - right);
}

// Driver code
int main()
{
    int start[] = { 0, 2, 4 };
    int end[] = { 7, 14, 6 };
    int n = sizeof(start) / sizeof(int);
    int d = 3;

    cout << minDistance(start, end, n, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;

class GFG
{

    // Function to return the minimum
    // distance the person has to move
    // int order to get the pictures
    static int minDistance(int start[], int end[], int n,
                           int d)
    {

        // To store the minimum ending point
        int left = Integer.MIN_VALUE;

        // To store the maximum starting point
        int right = Integer.MAX_VALUE;

        // Find the values of minSeg and maxSeg
        for (int i = 0; i < n; i++) {
            left = Math.max(left, start[i]);
            right = Math.min(right, end[i]);
        }

        // Impossible
        if (left > right)
            return -1;

        // The person doesn't need to move
        if (d >= left && d <= right)
            return 0;

        // Get closer to the left point
        if (d < left)
            return (left - d);

        // Get closer to the right point
        if (d > right)
            return (d - right);

        return -1;
    }

  // Driver code
    public static void main(String[] args)
    {
        int start[] = { 0, 2, 4 };
        int end[] = { 7, 14, 6 };
        int n = start.length;
        int d = 3;

        System.out.println(minDistance(start, end, n, d));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to return the minimum
# distance the person has to move
# order to get the pictures
def minDistance(start, end, n, d) :

    # To store the minimum ending point
    left = -sys.maxsize

    # To store the maximum starting point
    right = sys.maxsize

    # Find the values of minSeg and maxSeg
    for i in range(n) :
        left = max(left, start[i])
        right = min(right, end[i])

    # Impossible
    if (left > right):
        return -1

    # The person doesn't need to move
    if (d >= left and d <= right):
        return 0

    # Get closer to the left point
    if (d < left) :
        return (left - d)

    # Get closer to the right point
    if (d > right) :
        return (d - right)

# Driver code
start = [ 0, 2, 4 ]
end = [ 7, 14, 6 ]
n = len(start)
d = 3

print(minDistance(start, end, n, d))

# This code is contributed by target_2.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to return the minimum
// distance the person has to move
// int order to get the pictures
static int minDistance(int[] start, int[] end,
                       int n, int d)
{

    // To store the minimum ending point
    int left = Int32.MinValue;

    // To store the maximum starting point
    int right = Int32.MaxValue;

    // Find the values of minSeg and maxSeg
    for(int i = 0; i < n; i++)
    {
        left = Math.Max(left, start[i]);
        right = Math.Min(right, end[i]);
    }

    // Impossible
    if (left > right)
        return -1;

    // The person doesn't need to move
    if (d >= left && d <= right)
        return 0;

    // Get closer to the left point
    if (d < left)
        return (left - d);

    // Get closer to the right point
    if (d > right)
        return (d - right);

    return -1;
}

// Driver Code
public static void Main(String[] args)
{
    int[] start = { 0, 2, 4 };
    int[] end = { 7, 14, 6 };
    int n = start.Length;
    int d = 3;

    Console.Write(minDistance(start, end, n, d));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum
// distance the person has to move
// int order to get the pictures
function minDistance(start, intend, n, d) {
  // To store the minimum ending point
  let left = Number.MIN_SAFE_INTEGER;

  // To store the maximum starting point
  let right = Number.MAX_SAFE_INTEGER;

  // Find the values of minSeg and maxSeg
  for (let i = 0; i < n; i++) {
    left = Math.max(left, start[i]);
    right = Math.min(right, end[i]);
  }

  // Impossible
  if (left > right) return -1;

  // The person doesn't need to move
  if (d >= left && d <= right) return 0;

  // Get closer to the left point
  if (d < left) return left - d;

  // Get closer to the right point
  if (d > right) return d - right;
}

// Driver code

let start = [0, 2, 4];
let end = [7, 14, 6];
let n = start.length;
let d = 3;

document.write(minDistance(start, end, n, d));

</script>
```

**Output**

```
1
```