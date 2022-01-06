# 通过向右、向下或对角移动计算从 M×N 矩阵的左上角到右下角的可能路径数

> 原文:[https://www . geeksforgeeks . org/从左上方到右下方通过向右下方或对角移动矩阵计算可能路径数/](https://www.geeksforgeeks.org/count-of-possible-paths-from-top-left-to-bottom-right-of-a-m-x-n-matrix-by-moving-right-down-or-diagonally/)

给定 2 个整数 **M** 和 **N，**的任务是找到一个 **M x N** 矩阵从左上方到右下方的所有可能路径的计数，约束条件是，从每个单元格开始，您只能移动到**右侧或下方或对角**

**示例:**

> **输入:** M = 3，N = 3
> **输出:** 13
> **说明:**共有以下 13 条路径:VVHH，VH，HVVH，DVH，VDH，VHHV，hvhvhv，DHV，HHVV，HDV，VHD，HVD，DD 其中 V 代表垂直，H 代表水平，D 代表对角路径。
> 
> **输入:** M = 2，N = 2
> T3】输出: 3

**方法:**思路是用[递归](http://www.geeksforgeeks.org/recursion/)求路径总数。这种方法与[这篇](https://www.geeksforgeeks.org/count-possible-paths-top-left-bottom-right-nxm-matrix/)文章中讨论的方法非常相似。按照以下步骤解决问题:

*   如果 **M** 或 **N** 等于 **1，**则返回 **1。**
*   否则创建一个递归函数 numberOfPaths()对分别代表垂直、水平和对角线运动的值 **{M-1，N}、{M，N-1}** 和 **{M-1，N-1}** 调用相同的函数。

下面是上述方法的实现:

## C++

```
// C++  program for the above approach
#include <iostream>
using namespace std;

// Returns count of possible paths to
// reach cell at row number M and column
// number N from the topmost leftmost
// cell (cell at 1, 1)
int numberOfPaths(int M, int N)
{

    // If either given row number or
    // given column number is first
    if (M == 1 || N == 1)
        return 1;

    // Horizontal Paths +
    // Vertical Paths +
    // Diagonal Paths
    return numberOfPaths(M - 1, N) 
          + numberOfPaths(M, N - 1)
           + numberOfPaths(M - 1, N - 1);
}

// Driver Code
int main()
{
    cout << numberOfPaths(3, 3);
    return 0;
}
```

**Output**

```
13
```

***时间复杂度:**O(3<sup>M * N</sup>)*
***辅助空间:** O(1)*