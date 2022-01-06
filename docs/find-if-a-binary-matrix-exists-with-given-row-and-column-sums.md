# 查找给定行和列和的二元矩阵是否存在

> 原文:[https://www . geeksforgeeks . org/find-if-a-binary-matrix-exists-with-给定行和列-sums/](https://www.geeksforgeeks.org/find-if-a-binary-matrix-exists-with-given-row-and-column-sums/)

给定一个大小为 **R** 的数组**行【**，其中**行【I】**是第 **i <sup>行</sup>至**行的元素之和，另一个大小为 **C** 的数组列【】中**列【I】**是第 **i <sup>列</sup>至**列的元素之和。任务是检查是否有可能构造一个满足给定行和列和的 **R * C** 维的二元矩阵。二进制矩阵是只填充 0 和 1 的矩阵。
求和是指特定行或列中 1 的个数。
**举例:**

> **输入:**行[] = {2，2，2，2，2}，列[] = {5，5，0，0}
> **输出:**是
> 矩阵为
> {1，1，0，0}
> {1，1，0，0，0}
> {1，1，0，0，0}
> {1，1，0，0}
> {1，1，0，0}
> **输入:【T13**

**进场:**

1.  关键思想是矩阵中的任何单元格对行和列总和的贡献相等，因此所有行总和的总和必须等于列总和。
2.  现在，求行和的最大值，如果这个值大于非零列和的个数，那么矩阵就不存在。
3.  如果列和的最大值大于非零行和的数量，则无法构造矩阵。
4.  如果以上 3 个条件都满足，那么矩阵就存在。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if matrix exists
bool matrix_exist(int row[], int column[], int r, int c)
{
    int row_sum = 0;
    int column_sum = 0;
    int row_max = -1;
    int column_max = -1;
    int row_non_zero = 0;
    int column_non_zero = 0;

    // Store sum of rowsums, max of row sum
    // number of non zero row sums
    for (int i = 0; i < r; i++) {
        row_sum += row[i];
        row_max = max(row_max, row[i]);
        if (row[i])
            row_non_zero++;
    }

    // Store sum of column sums, max of column sum
    // number of non zero column sums
    for (int i = 0; i < c; i++) {
        column_sum += column[i];
        column_max = max(column_max, column[i]);
        if (column[i])
            column_non_zero++;
    }

    // Check condition 1, 2, 3
    if ((row_sum != column_sum) ||
        (row_max > column_non_zero) ||
        (column_max > row_non_zero))
        return false;

    return true;
}

// Driver Code
int main()
{
    int row[] = { 2, 2, 2, 2, 2 };
    int column[] = { 5, 5, 0, 0 };
    int r = sizeof(row) / sizeof(row[0]);
    int c = sizeof(column) / sizeof(column[0]);

    if (matrix_exist(row, column, r, c))
        cout << "YES\n";
    else
        cout << "NO\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

    // Function to check if matrix exists
    static boolean matrix_exist(int row[], int column[],
                                        int r, int c)
    {
        int row_sum = 0;
        int column_sum = 0;
        int row_max = -1;
        int column_max = -1;
        int row_non_zero = 0;
        int column_non_zero = 0;

        // Store sum of rowsums, max of row sum
        // number of non zero row sums
        for (int i = 0; i < r; i++)
        {
            row_sum += row[i];
            row_max = Math.max(row_max, row[i]);
            if (row[i] > 0)
            {
                row_non_zero++;
            }
        }

        // Store sum of column sums, max of column sum
        // number of non zero column sums
        for (int i = 0; i < c; i++)
        {
            column_sum += column[i];
            column_max = Math.max(column_max, column[i]);
            if (column[i] > 0)
            {
                column_non_zero++;
            }
        }

        // Check condition 1, 2, 3
        if ((row_sum != column_sum)
                || (row_max > column_non_zero)
                || (column_max > row_non_zero))
        {
            return false;
        }

        return true;
    }

// Driver Code
public static void main(String[] args)
{
    int row[] = { 2, 2, 2, 2, 2 };
    int column[] = { 5, 5, 0, 0 };
    int r = row.length;
    int c = column.length;

    if (matrix_exist(row, column, r, c))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to check if matrix exists
def matrix_exist(row,  column,  r, c):

    row_sum = 0
    column_sum = 0
    row_max = -1
    column_max = -1
    row_non_zero = 0
    column_non_zero = 0

    # Store sum of rowsums, max of row sum
    # number of non zero row sums
    for i in range(r):
        row_sum += row[i]
        row_max = max(row_max, row[i])
        if (row[i]):
            row_non_zero = row_non_zero + 1

    # Store sum of column sums, max of column sum
    # number of non zero column sums
    for i in range(c):
        column_sum = column_sum + column[i]
        column_max = max(column_max, column[i])
        if (column[i]):
            column_non_zero = column_non_zero + 1

    # Check condition 1, 2, 3
    if ((row_sum != column_sum)
        or (row_max > column_non_zero)
        or (column_max > row_non_zero)):

        return False

    return True

# Driver Code
if __name__ == '__main__':
    row = [2, 2, 2, 2, 2]
    column = [5, 5, 0, 0]
    r = len(row)
    c = len(column)
    if matrix_exist(row, column, r, c):
        print("YES")

    else:
        print("NO")

# this code is contributed by nirajgusain5
```

## C#

```
// C# implementation of above approach
using System;

public class GFG{

    // Function to check if matrix exists
    static bool matrix_exist(int[] row, int[] column,
                                        int r, int c)
    {
        int row_sum = 0;
        int column_sum = 0;
        int row_max = -1;
        int column_max = -1;
        int row_non_zero = 0;
        int column_non_zero = 0;

        // Store sum of rowsums, max of row sum
        // number of non zero row sums
        for (int i = 0; i < r; i++)
        {
            row_sum += row[i];
            row_max = Math.Max(row_max, row[i]);
            if (row[i] > 0)
            {
                row_non_zero++;
            }
        }

        // Store sum of column sums, max of column sum
        // number of non zero column sums
        for (int i = 0; i < c; i++)
        {
            column_sum += column[i];
            column_max = Math.Max(column_max, column[i]);
            if (column[i] > 0)
            {
                column_non_zero++;
            }
        }

        // Check condition 1, 2, 3
        if ((row_sum != column_sum)
                || (row_max > column_non_zero)
                || (column_max > row_non_zero))
        {
            return false;
        }

        return true;
    }

    // Driver Code
    static public void Main ()
    {
        int[] row = { 2, 2, 2, 2, 2 };
        int[] column = { 5, 5, 0, 0 };
        int r = row.Length;
        int c = column.Length;

        if (matrix_exist(row, column, r, c))
            Console.Write("YES");
        else
            Console.Write("NO");
    }
}

// This code has been contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check if matrix exists
function matrix_exist(row, column, r, c)
{
    var row_sum = 0;
    var column_sum = 0;
    var row_max = -1;
    var column_max = -1;
    var row_non_zero = 0;
    var column_non_zero = 0;

    // Store sum of rowsums, max of row sum
    // number of non zero row sums
    for (var i = 0; i < r; i++) {
        row_sum += row[i];
        row_max = Math.max(row_max, row[i]);
        if (row[i])
            row_non_zero++;
    }

    // Store sum of column sums, max of column sum
    // number of non zero column sums
    for (var i = 0; i < c; i++) {
        column_sum += column[i];
        column_max = Math.max(column_max, column[i]);
        if (column[i])
            column_non_zero++;
    }

    // Check condition 1, 2, 3
    if ((row_sum != column_sum) ||
        (row_max > column_non_zero) ||
        (column_max > row_non_zero))
        return false;

    return true;
}

// Driver Code
var row = [2, 2, 2, 2, 2];
var column = [5, 5, 0, 0];
var r = row.length;
var c = column.length;
if (matrix_exist(row, column, r, c))
    document.write( "YES");
else
    document.write( "NO");

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)