# 从给定矩阵中选择 K 个连续空单元格的方式计数

> 原文:[https://www . geeksforgeeks . org/从给定矩阵中选择 k 个连续空单元格的方式计数/](https://www.geeksforgeeks.org/count-of-ways-to-select-k-consecutive-empty-cells-from-a-given-matrix/)

给定维度为 **N * M** 的二元矩阵 **V[][]** ，其中每个单元格或者是**空**或者是**阻塞**分别用 **0** 和 **1** 标记，任务是统计从同一行或同一列中选择 **K** 个连续空单元格的方式数。
**示例:**

> **输入:** V[][] = {{1，1，0}，{0，0，0}}，K = 2
> **输出:** 3
> **说明:**
> 考虑到基于 1 的索引，可以通过以下方式选择 2 个连续的空单元格:
> [(1，3)，(2，3)]，[(2，1)，(2，2)]，[(2，2)，(2，3)]
> **输入:** V[]

**方法:**
想法是逐行遍历矩阵，对于每一行，计算空的连续单元格的总数。
按照以下步骤解决问题:

*   逐行遍历矩阵，计算连续单元格的数量。如果计数等于或超过 K，则将计数增加 1。
*   每次遇到被阻塞的单元格时，将连续空单元格的计数重置为 0。
*   如果 K？1.
*   返回获得的最终细胞计数。

以下是上述方法的实现:

## C++

```
// C++ program to find no of ways
// to select K consecutive empty
// cells from a row or column
#include <bits/stdc++.h>
using namespace std;

// Function to Traverse
// the matrix row wise
int rowWise(char* v, int n,
            int m, int k)
{
    // Initialize ans
    int ans = 0;

    // Traverse row wise
    for (int i = 0; i < n; i++) {

        // Initialize no of
        // consecutive empty
        // cells
        int countcons = 0;

        for (int j = 0; j < m; j++) {

            // Check if blocked cell is
            // encountered then reset
            // countcons  to 0
            if (*(v + i * m + j) == '1') {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, then
            // increment countcons
            else {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater or equal
            // to K, increment the ans
            if (countcons >= k) {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Function to Traverse the
// matrix column wise
int colWise(char* v, int n,
            int m, int k)
{
    // Initialize ans
    int ans = 0;

    // Traverse column wise
    for (int i = 0; i < m; i++) {

        // Initialize no of
        // consecutive empty cells
        int countcons = 0;

        for (int j = 0; j < n; j++) {

            // Check if blocked cell is
            // encountered then reset
            // countcons  to 0
            if (*(v + j * n + i) == '1') {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, increment
            // countcons
            else {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater than or equal
            // to K, increment the ans
            if (countcons >= k) {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
int main()
{

    int n = 3, m = 3, k = 1;

    char v[n][m] = { '0', '0', '0',
                     '0', '0', '0',
                     '0', '0', '0' };

    // If k = 1 only traverse row wise
    if (k == 1) {
        cout << rowWise(v[0], n, m, k);
    }

    // Traverse both row and column wise
    else {
        cout << colWise(v[0], n, m, k)
                    + rowWise(v[0], n,
                              m, k);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find no of ways
// to select K consecutive empty
// cells from a row or column
import java.util.*;

class GFG{

// Function to Traverse
// the matrix row wise
static int rowWise(char [][]v, int n,
                        int m, int k)
{

    // Initialize ans
    int ans = 0;

    // Traverse row wise
    for(int i = 0; i < n; i++)
    {

        // Initialize no of
        // consecutive empty
        // cells
        int countcons = 0;

        for(int j = 0; j < m; j++)
        {

            // Check if blocked cell is
            // encountered then reset
            // countcons to 0
            if (v[i][j] == '1')
            {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, then
            // increment countcons
            else
            {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater or equal
            // to K, increment the ans
            if (countcons >= k)
            {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Function to Traverse the
// matrix column wise
static int colWise(char [][]v, int n,
                        int m, int k)
{

    // Initialize ans
    int ans = 0;

    // Traverse column wise
    for(int i = 0; i < m; i++)
    {

        // Initialize no of
        // consecutive empty cells
        int countcons = 0;

        for(int j = 0; j < n; j++)
        {

            // Check if blocked cell is
            // encountered then reset
            // countcons to 0
            if (v[j][i] == '1')
            {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, increment
            // countcons
            else
            {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater than or equal
            // to K, increment the ans
            if (countcons >= k)
            {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3, m = 3, k = 1;

    char v[][] = { { '0', '0', '0' },
                   { '0', '0', '0' },
                   { '0', '0', '0' } };

    // If k = 1 only traverse row wise
    if (k == 1)
    {
        System.out.print(rowWise(v, n, m, k));
    }

    // Traverse both row and column wise
    else
    {
        System.out.print(colWise(v, n, m, k) +
                         rowWise(v, n, m, k));
    }
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python 3 program to find no of ways
# to select K consecutive empty
# cells from a row or column

# Function to Traverse
# the matrix row wise
def rowWise(v, n, m, k):

    # Initialize ans
    ans = 0

    # Traverse row wise
    for i in range (n):

        # Initialize no of
        # consecutive empty
        # cells
        countcons = 0

        for j in range (m):

            # Check if blocked cell is
            # encountered then reset
            # countcons  to 0
            if (v[i][j] == '1'):
                countcons = 0

            # Check if empty cell is
            # encountered, then
            # increment countcons
            else:
                countcons += 1

            # Check if number of empty
            # consecutive cells
            # is greater or equal
            # to K, increment the ans
            if (countcons >= k):
                ans += 1

    # Return the count
    return ans

# Function to Traverse the
# matrix column wise
def colWise(v, n, m, k):

    # Initialize ans
    ans = 0

    # Traverse column wise
    for i in range (m):

        # Initialize no of
        # consecutive empty cells
        countcons = 0

        for j in range (n):

            # Check if blocked cell is
            # encountered then reset
            # countcons  to 0
            if (v[j][i] == '1'):
                countcons = 0

            # Check if empty cell is
            # encountered, increment
            # countcons
            else:
                countcons += 1

            # Check if number of empty
            # consecutive cells
            # is greater than or equal
            # to K, increment the ans
            if (countcons >= k):
                ans += 1

    # Return the count
    return ans

# Driver Code
if __name__ == "__main__":

    n = 3
    m = 3
    k = 1

    v = [['0', '0', '0'],
         ['0', '0', '0'],
         ['0', '0', '0']]

    # If k = 1 only
    # traverse row wise
    if (k == 1):
        print (rowWise(v, n, m, k))

    # Traverse both row
    # and column wise
    else:
        print (colWise(v, n, m, k) +
               rowWise(v, n, m, k))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find no of ways
// to select K consecutive empty
// cells from a row or column
using System;

class GFG{

// Function to Traverse
// the matrix row wise
static int rowWise(char [,]v, int n,
                       int m, int k)
{

    // Initialize ans
    int ans = 0;

    // Traverse row wise
    for(int i = 0; i < n; i++)
    {

        // Initialize no of
        // consecutive empty
        // cells
        int countcons = 0;

        for(int j = 0; j < m; j++)
        {

            // Check if blocked cell is
            // encountered then reset
            // countcons to 0
            if (v[i, j] == '1')
            {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, then
            // increment countcons
            else
            {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater or equal
            // to K, increment the ans
            if (countcons >= k)
            {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Function to Traverse the
// matrix column wise
static int colWise(char [,]v, int n,
                       int m, int k)
{

    // Initialize ans
    int ans = 0;

    // Traverse column wise
    for(int i = 0; i < m; i++)
    {

        // Initialize no of
        // consecutive empty cells
        int countcons = 0;

        for(int j = 0; j < n; j++)
        {

            // Check if blocked cell is
            // encountered then reset
            // countcons to 0
            if (v[j, i] == '1')
            {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, increment
            // countcons
            else
            {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater than or equal
            // to K, increment the ans
            if (countcons >= k)
            {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3, m = 3, k = 1;

    char [,]v = { { '0', '0', '0' },
                  { '0', '0', '0' },
                  { '0', '0', '0' } };

    // If k = 1 only traverse row wise
    if (k == 1)
    {
        Console.Write(rowWise(v, n, m, k));
    }

    // Traverse both row and column wise
    else
    {
        Console.Write(colWise(v, n, m, k) +
                      rowWise(v, n, m, k));
    }
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to find no of ways
// to select K consecutive empty
// cells from a row or column

// Function to Traverse
// the matrix row wise
function rowWise(v, n, m, k)
{
    // Initialize ans
    var ans = 0;

    // Traverse row wise
    for (var i = 0; i < n; i++) {

        // Initialize no of
        // consecutive empty
        // cells
        var countcons = 0;

        for (var j = 0; j < m; j++) {

            // Check if blocked cell is
            // encountered then reset
            // countcons  to 0
            if ((v + i * m + j) == '1') {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, then
            // increment countcons
            else {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater or equal
            // to K, increment the ans
            if (countcons >= k) {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Function to Traverse the
// matrix column wise
function colWise(v, n, m, k)
{
    // Initialize ans
    var ans = 0;

    // Traverse column wise
    for (var i = 0; i < m; i++) {

        // Initialize no of
        // consecutive empty cells
        var countcons = 0;

        for (var j = 0; j < n; j++) {

            // Check if blocked cell is
            // encountered then reset
            // countcons  to 0
            if ((v + j * n + i) == '1') {
                countcons = 0;
            }

            // Check if empty cell is
            // encountered, increment
            // countcons
            else {
                countcons++;
            }

            // Check if number of empty
            // consecutive cells
            // is greater than or equal
            // to K, increment the ans
            if (countcons >= k) {
                ans++;
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
var n = 3, m = 3, k = 1;
var v = ['0', '0', '0',
                 '0', '0', '0',
                 '0', '0', '0'];

// If k = 1 only traverse row wise
if (k == 1) {
    document.write( rowWise(v[0], n, m, k));  
}

// Traverse both row and column wise
else {
    document.write( colWise(v[0], n, m, k)
                + rowWise(v[0], n,
                          m, k));
}

// This code is contributed by itsok.
</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N * M)*
***空间复杂度:** O(N * M)*