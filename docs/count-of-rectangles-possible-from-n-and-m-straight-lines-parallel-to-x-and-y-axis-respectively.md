# 分别平行于 X 轴和 Y 轴的 N 条和 M 条直线上可能的矩形数

> 原文:[https://www . geeksforgeeks . org/矩形数-可能从 n 和 m 条直线-分别平行于 x 轴和 y 轴/](https://www.geeksforgeeks.org/count-of-rectangles-possible-from-n-and-m-straight-lines-parallel-to-x-and-y-axis-respectively/)

给定两个整数 **N** 和 **M** ，其中 **N** 直线平行于 **X 轴**和 **M** 直线平行于 **Y 轴**，任务是计算这些直线可以形成的矩形数量。
**示例:**

> **输入:** N = 3，M = 6
> **输出:** 45
> **说明:**
> 共有 45 个可能的矩形，3 条平行于 x 轴，6 条平行于 y 轴。
> **输入:** N = 2，M = 4
> **输出:** 6
> **说明:**
> 共有 6 种可能的矩形，其中 2 条平行于 x 轴，4 条平行于 y 轴。

**方法:**
要解决上面提到的问题，我们需要观察到一个矩形是由 4 条直线组成的，其中相对的边是平行的，任意两条边之间的角度是 90°。因此，对于每个矩形，两条边需要平行于 **X 轴**，另外两条边需要平行于 Y 轴。

*   选择两条平行于 X 轴的直线的方法数=**<sup>N</sup>C<sub>2</sub>**<sub>和选择两条平行于 Y 轴的直线的方法数=**<sup>M</sup>C<sub>2</sub>**<sub>。</sub></sub>
*   所以矩形的总数=**<sup>N</sup>C<sub>2 *</sub>T5】MC<sub>2</sub>T9】=**【N *(N–1)/2】*【M *(M–1)/2】****

以下是上述方法的实施:

## C++

```
// C++ Program to count number of
// rectangles formed by N lines
// parallel to X axis M lines
// parallel to Y axis
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// number of rectangles
int count_rectangles(int N, int M)
{
    // Total number of ways to
    // select two lines
    // parallel to X axis
    int p_x = (N * (N - 1)) / 2;

    // Total number of ways
    // to select two lines
    // parallel to Y axis
    int p_y = (M * (M - 1)) / 2;

    // Total number of rectangles
    return p_x * p_y;
}

// Driver Program
int main()
{

    int N = 3;

    int M = 6;

    cout << count_rectangles(N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count number of
// rectangles formed by N lines
// parallel to X axis M lines
// parallel to Y axis
class GFG{

// Function to calculate
// number of rectangles
static int count_rectangles(int N, int M)
{
    // Total number of ways to
    // select two lines
    // parallel to X axis
    int p_x = (N * (N - 1)) / 2;

    // Total number of ways
    // to select two lines
    // parallel to Y axis
    int p_y = (M * (M - 1)) / 2;

    // Total number of rectangles
    return p_x * p_y;
}

// Driver Program
public static void main(String[] args)
{
    int N = 3;
    int M = 6;

    System.out.print(count_rectangles(N, M));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to count number of rectangles
# formed by N lines parallel to X axis
# and M lines parallel to Y axis
def count_rectangles(N, M):

    # Total number of ways to select
    # two lines parallel to X axis
    p_x = (N * (N - 1)) // 2

    # Total number of ways to select
    # two lines parallel to Y axis
    p_y = (M * (M - 1)) // 2

    # Total number of rectangles
    return p_x * p_y

# Driver code
N = 3
M = 6

print(count_rectangles(N, M))

# This code is contributed by himanshu77
```

## C#

```
// C# Program to count number of
// rectangles formed by N lines
// parallel to X axis M lines
// parallel to Y axis
using System;
class GFG{

// Function to calculate
// number of rectangles
static int count_rectangles(int N, int M)
{
    // Total number of ways to
    // select two lines
    // parallel to X axis
    int p_x = (N * (N - 1)) / 2;

    // Total number of ways
    // to select two lines
    // parallel to Y axis
    int p_y = (M * (M - 1)) / 2;

    // Total number of rectangles
    return p_x * p_y;
}

// Driver Program
public static void Main()
{
    int N = 3;
    int M = 6;

    Console.Write(count_rectangles(N, M));
}
}

// This code is contributed by Code_mech
```

## java 描述语言

```
<script>

// JavaScript Program to count number of
// rectangles formed by N lines
// parallel to X axis M lines
// parallel to Y axis

// Function to calculate
// number of rectangles
function count_rectangles(N, M)
{
    // Total number of ways to
    // select two lines
    // parallel to X axis
    let p_x = (N * (N - 1)) / 2;

    // Total number of ways
    // to select two lines
    // parallel to Y axis
    let p_y = (M * (M - 1)) / 2;

    // Total number of rectangles
    return p_x * p_y;
}

// Driver Code

    let N = 3;
    let M = 6;

    document.write(count_rectangles(N, M));

</script>
```

**Output:** 

```
45
```

***时间复杂度:** O(1)*