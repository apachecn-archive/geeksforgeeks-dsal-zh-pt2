# 矩阵中给定范围 L 到 R 内的数字计数

> 原文:[https://www . geeksforgeeks . org/给定范围内的数字计数-l-r-矩阵中有哪些数字/](https://www.geeksforgeeks.org/count-of-numbers-in-given-range-l-to-r-which-are-present-in-a-matrix/)

给定一个**矩阵(mat[][])** ，该矩阵按行和列的递增顺序排序。给出了两个整数， **L 和 R** ，我们的任务是统计矩阵在[L，R]范围内的元素个数。
**例:**

> **输入:** L = 3，R = 11，矩阵=
> {{1，6，9}
> {2，7，11}
> {3，8，12}}
> **输出:** 6
> **说明:**
> 在这个范围【3，11】内的元素是 3，6，7，8，9，11。
> **输入:** L = 20，R = 26，矩阵=
> {{1，6，19}
> {2，7，31}
> {3，8，42}}
> **输出:** 0
> **说明:**
> 此范围内无元素。

**天真方法:**要解决上面提到的问题，天真的方法是通过矩阵进行 [**逐行遍历**](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/) 。
对于每一行，我们检查该行的每个元素，如果它在给定的范围内，那么我们增加计数。最后，我们返回计数。
***时间复杂度:** O(M * N)，其中 M 为行数，N 为列数。*
**高效途径:**优化上述途径:

1.  首先我们**计算小于 L** 的元素。让我们把它看作是*第一个*。我们从第一列的最后一个元素开始遍历，这包括以下两个步骤:
    *   如果当前迭代元素小于 L，我们将 count1 增加相应的行+ 1，因为当前元素(包括当前元素)上方的列中的元素必须小于 L。我们增加列索引。
    *   如果当前迭代元素大于或等于 L，我们减少行索引。我们这样做，直到行或列索引变得无效。
2.  接下来我们**计算小于或等于 R** 的元素。我们就当是*县 2* 吧。我们从第一列的最后一个元素开始遍历，这包括两个步骤:
    *   如果当前迭代元素小于或等于 R，我们将 count2 增加相应的行+ 1，因为当前元素(包括当前元素)上方的列中的元素必须小于或等于 R。我们增加列索引。
    *   如果当前迭代元素大于 R，我们减少行索引。我们这样做，直到行或列索引变得无效。
3.  最后，我们返回第 2 列和第 1 列的差值，这将是所需的答案。

以下是上述方法的实现:

## C++

```
// C++ implementation to count
// all elements in a Matrix
// which lies in the given range

#include <bits/stdc++.h>
using namespace std;

#define M 3
#define N 3

// Counting elements in range [L, R]
int countElements(int mat[M][N],
                  int L, int R)
{
    // Count elements less than L
    int count1 = 0;
    int row = M - 1, col = 0;

    while (row >= 0 && col < N) {

        // Check if the current iterating
        // element is less than L
        if (mat[row][col] < L) {
            count1 += (row + 1);
            col++;
        }
        else {
            row--;
        }
    }

    // counting elements less
    // than or equal to R
    int count2 = 0;
    row = M - 1, col = 0;

    while (row >= 0 && col < N) {

        // Check if the current iterating
        // element is less than R
        if (mat[row][col] <= R) {
            count2 += (row + 1);
            col++;
        }
        else {
            row--;
        }
    }

    // return the final result
    return count2 - count1;
}

// Driver code
int main()
{

    int mat[M][N] = { { 1, 6, 19 },
                      { 2, 7, 31 },
                      { 3, 8, 42 } };

    int L = 10, R = 26;

    cout << countElements(mat, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// all elements in a Matrix
// which lies in the given range
import java.util.*;
import java.lang.*;
class GFG{

static int N = 3;
static int M = 3;

// Counting elements in range [L, R]
static int countElements(int[][] mat,
                         int L, int R)
{
    // Count elements less than L
    int count1 = 0;
    int row = M - 1, col = 0;

    while (row >= 0 && col < N)
    {

        // Check if the current iterating
        // element is less than L
        if (mat[row][col] < L)
        {
            count1 += (row + 1);
            col++;
        }
        else
        {
            row--;
        }
    }

    // counting elements less
    // than or equal to R
    int count2 = 0;
    row = M - 1;
    col = 0;

    while (row >= 0 && col < N)
    {

        // Check if the current iterating
        // element is less than R
        if (mat[row][col] <= R)
        {
            count2 += (row + 1);
            col++;
        }
        else
        {
            row--;
        }
    }

    // return the final result
    return count2 - count1;
}

// Driver code
public static void main(String[] args)
{
    int[][] mat = { { 1, 6, 19 },
                    { 2, 7, 31 },
                    { 3, 8, 42 } };

    int L = 10, R = 26;

    System.out.println(countElements(mat, L, R));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to count
# all elements in a matrix which
# lies in the given range

M = 3
N = 3

# Counting elements in range [L, R]
def countElements(mat, L, R):

    # Count elements less than L
    count1 = 0
    row = M - 1
    col = 0

    while row >= 0 and col < N:

        # Check if the current iterating
        # element is less than L
        if mat[row][col] < L:
            count1 += (row + 1)
            col += 1

        else:
            row -= 1

    # Counting elements less
    # than or equal to R
    count2 = 0
    row = M - 1
    col = 0

    while row >= 0 and col < N:

        # Check if the current iterating
        # element is less than R
        if mat[row][col] <= R:
            count2 += (row + 1)
            col += 1

        else:
            row -= 1

    # Return the final result
    return count2 - count1

# Driver code
mat = [ [ 1, 6, 19 ],
        [ 2, 7, 31 ],
        [ 3, 8, 42 ] ]
L = 10
R = 26

print(countElements(mat, L, R))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to count
// all elements in a Matrix
// which lies in the given range
using System;
class GFG{

static int N = 3;
static int M = 3;

// Counting elements in range [L, R]
static int countElements(int[,] mat,
                         int L, int R)
{
    // Count elements less than L
    int count1 = 0;
    int row = M - 1, col = 0;

    while (row >= 0 && col < N)
    {

        // Check if the current iterating
        // element is less than L
        if (mat[row, col] < L)
        {
            count1 += (row + 1);
            col++;
        }
        else
        {
            row--;
        }
    }

    // counting elements less
    // than or equal to R
    int count2 = 0;
    row = M - 1;
    col = 0;

    while (row >= 0 && col < N)
    {

        // Check if the current iterating
        // element is less than R
        if (mat[row, col] <= R)
        {
            count2 += (row + 1);
            col++;
        }
        else
        {
            row--;
        }
    }

    // return the final result
    return count2 - count1;
}

// Driver code
public static void Main()
{
    int[,] mat = { { 1, 6, 19 },
                   { 2, 7, 31 },
                   { 3, 8, 42 } };

    int L = 10, R = 26;

    Console.Write(countElements(mat, L, R));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to count
// all elements in a Matrix
// which lies in the given range

M = 3;
N = 3;

// Counting elements in range [L, R]
function countElements( mat, L,  R)
{
    // Count elements less than L
    var count1 = 0;
    var row = M - 1, col = 0;

    while (row >= 0 && col < N) {

        // Check if the current iterating
        // element is less than L
        if (mat[row][col] < L) {
            count1 += (row + 1);
            col++;
        }
        else {
            row--;
        }
    }

    // counting elements less
    // than or equal to R
    var count2 = 0;
    row = M - 1, col = 0;

    while (row >= 0 && col < N) {

        // Check if the current iterating
        // element is less than R
        if (mat[row][col] <= R) {
            count2 += (row + 1);
            col++;
        }
        else {
            row--;
        }
    }

    // return the final result
    return count2 - count1;
}

    var mat = [ [ 1, 6, 19 ],
                      [ 2, 7, 31 ],
                      [ 3, 8, 42 ] ];

    var L = 10, R = 26;

    document.write( countElements(mat, L, R));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(M + N)。m 是行数，N 是列数。*
***辅助空间复杂度:** O(1)。*