# 矩阵中距离给定单元格最远的单元格

> 原文:[https://www . geeksforgeeks . org/矩阵中给定单元的最远单元/](https://www.geeksforgeeks.org/farthest-cell-from-a-given-cell-in-a-matrix/)

给定整数 **N** 、 **M** 、 **R** 和 **C** ，其中 **N** 和 **M** 表示矩阵中的行数和列数， **(R，C)** 表示该矩阵中的一个单元，任务是找出距离该单元最远的单元的距离 **(R，C)** 。
***注:**矩阵一次只能水平或垂直遍历。*

**示例:**

> **输入:** N = 15，M = 12，R = 1，C = 6
> **输出:** 20
> **说明:**从所有四个角计算的最大距离是 20，5，19，6。因此，20 是必需的答案。
> 
> **输入:** N = 15，M = 12，R = 2，C = 4
> T3】输出: 21

**天真法:**最简单的方法是[遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，计算矩阵每个像元到给定像元的距离 **(R，C)** ，保持所有距离的最大值。

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，观察到矩阵中距离任何细胞最远的细胞将是四个最角落的细胞之一，即 **(1，1)，(1，M)，(N，1)，(N，M)** 。

按照以下步骤解决问题:

*   初始化 **d1** 、 **d2** 、 **d3** 和 **d4** 分别等于**N+M–R–C**、**R+C–2**、**N–R+C–1**和**M–C+R–1**。
*   打印 **d1** 、 **d2** 、 **d3** 和 **d4** 中的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the farthest
// cell distance from the given cell
void farthestCellDistance(int N, int M,
                          int R, int C)
{
    // Distance from all the
    // cornermost cells

    // From cell(N, M)
    int d1 = N + M - R - C;

    // From Cell(1, 1)
    int d2 = R + C - 2;

    // From cell(N, 1)
    int d3 = N - R + C - 1;

    // From cell(1, M)
    int d4 = M - C + R - 1;

    // Finding out maximum
    int maxDistance = max(d1,
                          max(d2,
                              max(d3, d4)));

    // Print the answer
    cout << maxDistance;
}

// Driver Code
int main()
{
    int N = 15, M = 12, R = 1, C = 6;
    farthestCellDistance(N, M, R, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the farthest
// cell distance from the given cell
static void farthestCellDistance(int N, int M,
                                 int R, int C)
{

    // Distance from all the
    // cornermost cells

    // From cell(N, M)
    int d1 = N + M - R - C;

    // From Cell(1, 1)
    int d2 = R + C - 2;

    // From cell(N, 1)
    int d3 = N - R + C - 1;

    // From cell(1, M)
    int d4 = M - C + R - 1;

    // Finding out maximum
    int maxDistance = Math.max(d1, Math.max(
                  d2, Math.max(d3, d4)));

    // Print the answer
    System.out.println(maxDistance);
}

// Driver Code
public static void main(String[] args)
{
    int N = 15, M = 12, R = 1, C = 6;

    farthestCellDistance(N, M, R, C);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the farthest
# cell distance from the given cell
def farthestCellDistance(N, M, R, C):

    # Distance from all the
    # cornermost cells

    # From cell(N, M)
    d1 = N + M - R - C;

    # From Cell(1, 1)
    d2 = R + C - 2;

    # From cell(N, 1)
    d3 = N - R + C - 1;

    # From cell(1, M)
    d4 = M - C + R - 1;

    # Finding out maximum
    maxDistance = max(d1, max(d2, max(d3, d4)));

    # Prthe answer
    print(maxDistance);

# Driver Code
if __name__ == '__main__':
    N = 15;
    M = 12;
    R = 1;
    C = 6;

    farthestCellDistance(N, M, R, C);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the farthest
// cell distance from the given cell
static void farthestCellDistance(int N, int M,
                                 int R, int C)
{

    // Distance from all the
    // cornermost cells

    // From cell(N, M)
    int d1 = N + M - R - C;

    // From Cell(1, 1)
    int d2 = R + C - 2;

    // From cell(N, 1)
    int d3 = N - R + C - 1;

    // From cell(1, M)
    int d4 = M - C + R - 1;

    // Finding out maximum
    int maxDistance = Math.Max(d1, Math.Max(
                  d2, Math.Max(d3, d4)));

    // Print the answer
    Console.WriteLine(maxDistance);
}

// Driver Code
static public void Main()
{
    int N = 15, M = 12, R = 1, C = 6;

    farthestCellDistance(N, M, R, C);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// Java script program for the above approach

// Function to find the farthest
// cell distance from the given cell
function farthestCellDistance( N,  M,
                                 R,  C)
{

    // Distance from all the
    // cornermost cells

    // From cell(N, M)
    let d1 = N + M - R - C;

    // From Cell(1, 1)
    let d2 = R + C - 2;

    // From cell(N, 1)
    let d3 = N - R + C - 1;

    // From cell(1, M)
    let d4 = M - C + R - 1;

    // Finding out maximum
    let maxDistance = Math.max(d1, Math.max(
                d2, Math.max(d3, d4)));

    // Print the answer
    document.write(maxDistance);
}

// Driver Code

    let N = 15, M = 12, R = 1, C = 6;

    farthestCellDistance(N, M, R, C);

// This code is contributed by Bobby
</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)