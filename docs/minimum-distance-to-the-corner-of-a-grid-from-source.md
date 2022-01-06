# 从源到栅格角落的最小距离

> 原文:[https://www . geeksforgeeks . org/从源到网格角落的最小距离/](https://www.geeksforgeeks.org/minimum-distance-to-the-corner-of-a-grid-from-source/)

给定一个有序的二进制网格 **r * c** 和一个初始位置。任务是找到从源到网格任何角落的最小距离。只有当**网格【I】【j】= 0**且仅允许**向左**、**向右**、**向上**和**向下**移动时，才能对单元格**网格【I】【j】**进行移动。如果不存在有效路径，则打印 **-1** 。
**举例:**

> **输入:** i = 1，j = 1，网格[][] = {{0，0，1}，{0，0，0}，{1，1，1}}
> **输出:** 2
> (1，1)—>(1，0)—>(0，0)
> 
> **输入:** i = 0，j = 0，网格[][] = {{0，1}，{1，1}}
> **输出:** 0
> 源已经是网格的一角。

**进场:**

*   如果信号源已经在任何角落，则打印 **0** 。
*   使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 从源开始遍历网格，如下所示:
    *   在队列中插入单元格位置。
    *   从队列中弹出元素，并将其标记为已访问。
    *   对于与弹出移动相邻的每个有效移动，将单元格位置插入队列。
    *   每次移动时，更新单元格距初始位置的最小距离。
*   BFS 建成后，找到从源头到每个角落的最小距离。
*   最后打印其中的最小值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define row 5
#define col 5

// Global variables for grid, minDistance and visited array
int minDistance[row + 1][col + 1], visited[row + 1][col + 1];

// Queue for BFS
queue<pair<int, int> > que;

// Function to find whether the move is valid or not
bool isValid(int grid[][col], int i, int j)
{
    if (i < 0 || j < 0
        || j >= col || i >= row
        || grid[i][j] || visited[i][j])
        return false;

    return true;
}

// Function to return the minimum distance
// from source to the end of the grid
int minDistance(int grid[][col],
                           int sourceRow, int sourceCol)
{
    // If source is one of the destinations
    if ((sourceCol == 0 && sourceRow == 0)
        || (sourceCol == col - 1 && sourceRow == 0)
        || (sourceCol == 0 && sourceRow == row - 1)
        || (sourceCol == col - 1 && sourceRow == row - 1))
        return 0;

    // Set minimum value
    int minFromSource = row * col;

    // Precalculate minDistance of each grid with R * C
    for (int i = 0; i < row; i++)
        for (int j = 0; j < col; j++)
            minDistance[i][j] = row * col;

    // Insert source position in queue
    que.push(make_pair(sourceRow, sourceCol));

    // Update minimum distance to visit source
    minDistance[sourceRow][sourceCol] = 0;

    // Set source to visited
    visited[sourceRow][sourceCol] = 1;

    // BFS approach for calculating the minDistance
    // of each cell from source
    while (!que.empty()) {

        // Iterate over all four cells adjacent
        // to current cell
        pair<int, int> cell = que.front();

        // Initialize position of current cell
        int cellRow = cell.first;
        int cellCol = cell.second;

        // Cell below the current cell
        if (isValid(grid, cellRow + 1, cellCol)) {

            // Push new cell to the queue
            que.push(make_pair(cellRow + 1, cellCol));

            // Update one of its neightbor's distance
            minDistance[cellRow + 1][cellCol]
                = min(minDistance[cellRow + 1][cellCol],
                      minDistance[cellRow][cellCol] + 1);
            visited[cellRow + 1][cellCol] = 1;
        }

        // Above the current cell
        if (isValid(grid, cellRow - 1, cellCol)) {
            que.push(make_pair(cellRow - 1, cellCol));
            minDistance[cellRow - 1][cellCol]
                = min(minDistance[cellRow - 1][cellCol],
                      minDistance[cellRow][cellCol] + 1);
            visited[cellRow - 1][cellCol] = 1;
        }

        // Right cell
        if (isValid(grid, cellRow, cellCol + 1)) {
            que.push(make_pair(cellRow, cellCol + 1));
            minDistance[cellRow][cellCol + 1]
                = min(minDistance[cellRow][cellCol + 1],
                      minDistance[cellRow][cellCol] + 1);
            visited[cellRow][cellCol + 1] = 1;
        }

        // Left cell
        if (isValid(grid, cellRow, cellCol - 1)) {
            que.push(make_pair(cellRow, cellCol - 1));
            minDistance[cellRow][cellCol - 1]
                = min(minDistance[cellRow][cellCol - 1],
                      minDistance[cellRow][cellCol] + 1);
            visited[cellRow][cellCol - 1] = 1;
        }

        // Pop the visited cell
        que.pop();
    }

    int i;

    // Minimum distance to the corner
    // of the first row, first column
    minFromSource = min(minFromSource,
                        minDistance[0][0]);

    // Minimum distance to the corner
    // of the last row, first column
    minFromSource = min(minFromSource,
                        minDistance[row - 1][0]);

    // Minimum distance to the corner
    // of the last row, last column
    minFromSource = min(minFromSource,
                        minDistance[row - 1][col - 1]);

    // Minimum distance to the corner
    // of the first row, last column
    minFromSource = min(minFromSource,
                        minDistance[0][col - 1]);

    // If no path exists
    if (minFromSource == row * col)
        return -1;

    // Return the minimum distance
    return minFromSource;
}

// Driver code
int main()
{
    int sourceRow = 3, sourceCol = 3;
    int grid[row][col] = { 1, 1, 1, 0, 0,
                           0, 0, 1, 0, 1,
                           0, 0, 1, 0, 1,
                           1, 0, 0, 0, 1,
                           1, 1, 0, 1, 0 };

    cout << minDistance(grid, sourceRow, sourceCol);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Pair class
static class Pair
{
    int first,second;
    Pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

static int row = 5;
static int col = 5;

// Global variables for grid, minDistance and visited array
static int minDistance[][] =
            new int[row + 1][col + 1],
            visited[][] = new int[row + 1][col + 1];

// Queue for BFS
static Queue<Pair > que = new LinkedList<>();

// Function to find whether the move is valid or not
static boolean isValid(int grid[][], int i, int j)
{
    if (i < 0 || j < 0
        || j >= col || i >= row
        || grid[i][j] != 0 || visited[i][j] != 0)
        return false;

    return true;
}

// Function to return the minimum distance
// from source to the end of the grid
static int minDistance(int grid[][],
                        int sourceRow, int sourceCol)
{
    // If source is one of the destinations
    if ((sourceCol == 0 && sourceRow == 0)
        || (sourceCol == col - 1 && sourceRow == 0)
        || (sourceCol == 0 && sourceRow == row - 1)
        || (sourceCol == col - 1 && sourceRow == row - 1))
        return 0;

    // Set minimum value
    int minFromSource = row * col;

    // Precalculate minDistance of each grid with R * C
    for (int i = 0; i < row; i++)
        for (int j = 0; j < col; j++)
            minDistance[i][j] = row * col;

    // Insert source position in queue
    que.add(new Pair(sourceRow, sourceCol));

    // Update minimum distance to visit source
    minDistance[sourceRow][sourceCol] = 0;

    // Set source to visited
    visited[sourceRow][sourceCol] = 1;

    // BFS approach for calculating the minDistance
    // of each cell from source
    while (que.size() > 0)
    {

        // Iterate over all four cells adjacent
        // to current cell
        Pair cell = que.peek();

        // Initialize position of current cell
        int cellRow = cell.first;
        int cellCol = cell.second;

        // Cell below the current cell
        if (isValid(grid, cellRow + 1, cellCol))
        {

            // add new cell to the queue
            que.add(new Pair(cellRow + 1, cellCol));

            // Update one of its neightbor's distance
            minDistance[cellRow + 1][cellCol]
                = Math.min(minDistance[cellRow + 1][cellCol],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow + 1][cellCol] = 1;
        }

        // Above the current cell
        if (isValid(grid, cellRow - 1, cellCol))
        {
            que.add(new Pair(cellRow - 1, cellCol));
            minDistance[cellRow - 1][cellCol]
                = Math.min(minDistance[cellRow - 1][cellCol],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow - 1][cellCol] = 1;
        }

        // Right cell
        if (isValid(grid, cellRow, cellCol + 1))
        {
            que.add(new Pair(cellRow, cellCol + 1));
            minDistance[cellRow][cellCol + 1]
                = Math.min(minDistance[cellRow][cellCol + 1],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow][cellCol + 1] = 1;
        }

        // Left cell
        if (isValid(grid, cellRow, cellCol - 1))
        {
            que.add(new Pair(cellRow, cellCol - 1));
            minDistance[cellRow][cellCol - 1]
                = Math.min(minDistance[cellRow][cellCol - 1],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow][cellCol - 1] = 1;
        }

        // remove the visited cell
        que.remove();
    }

    int i;

    // Minimum distance to the corner
    // of the first row, first column
    minFromSource = Math.min(minFromSource,
                        minDistance[0][0]);

    // Minimum distance to the corner
    // of the last row, first column
    minFromSource = Math.min(minFromSource,
                        minDistance[row - 1][0]);

    // Minimum distance to the corner
    // of the last row, last column
    minFromSource = Math.min(minFromSource,
                        minDistance[row - 1][col - 1]);

    // Minimum distance to the corner
    // of the first row, last column
    minFromSource = Math.min(minFromSource,
                        minDistance[0][col - 1]);

    // If no path exists
    if (minFromSource == row * col)
        return -1;

    // Return the minimum distance
    return minFromSource;
}

// Driver code
public static void main(String args[])
{
    int sourceRow = 3, sourceCol = 3;
    int grid[][] = { {1, 1, 1, 0, 0},
                    {0, 0, 1, 0, 1},
                    {0, 0, 1, 0, 1},
                    {1, 0, 0, 0, 1},
                    {1, 1, 0, 1, 0} };

    System.out.println(minDistance(grid, sourceRow, sourceCol));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

row = 5
col = 5

# Global variables for grid, minDistance and visited array
minDistance = [[0 for i in range(col+1)] for j in range(row+1)]
visited = [[0 for i in range(col+1)]for j in range(row+1)]

# Queue for BFS
que = [[0,0]]

# Function to find whether the move is valid or not
def isValid(grid,i,j):
    if (i < 0 or j < 0 or j >= col or
        i >= row or grid[i][j] or visited[i][j]):
        return False
    return True

# Function to return the minimum distance
# from source to the end of the grid
def minDistance1(grid,sourceRow,sourceCol):
    # If source is one of the destinations
    if ((sourceCol == 0 and sourceRow == 0) or
        (sourceCol == col - 1 and sourceRow == 0) or
        (sourceCol == 0 or sourceRow == row - 1) or
        (sourceCol == col - 1 and sourceRow == row - 1)):
        return 0

    # Set minimum value
    minFromSource = row * col

    # Precalculate minDistance of each grid with R * C
    for i in range(row):
        for j in range(col):
            minDistance[i][j] = row * col

    # Insert source position in queue
    que.append([sourceRow, sourceCol])

    # Update minimum distance to visit source
    minDistance[sourceRow][sourceCol] = 0

    # Set source to visited
    visited[sourceRow][sourceCol] = 1

    # BFS approach for calculating the minDistance
    # of each cell from source
    while (len(que)!=0):
        # Iterate over all four cells adjacent
        # to current cell
        cell = que[0]

        # Initialize position of current cell
        cellRow = cell[0]
        cellCol = cell[1]

        # Cell below the current cell
        if (isValid(grid, cellRow + 1, cellCol)):
            # Push new cell to the queue
            que.append([cellRow + 1, cellCol])

            # Update one of its neightbor's distance
            minDistance[cellRow + 1][cellCol] = min(minDistance[cellRow + 1][cellCol],
                                                minDistance[cellRow][cellCol] + 1)
            visited[cellRow + 1][cellCol] = 1

        # Above the current cell
        if (isValid(grid, cellRow - 1, cellCol)):
            que.append([cellRow - 1, cellCol])
            minDistance[cellRow - 1][cellCol] = min(minDistance[cellRow - 1][cellCol],
                                                    minDistance[cellRow][cellCol] + 1)
            visited[cellRow - 1][cellCol] = 1

        # Right cell
        if (isValid(grid, cellRow, cellCol + 1)):
            que.append([cellRow, cellCol + 1])
            minDistance[cellRow][cellCol + 1] = min(minDistance[cellRow][cellCol + 1],
                                                    minDistance[cellRow][cellCol] + 1)
            visited[cellRow][cellCol + 1] = 1

        # Left cell
        if (isValid(grid, cellRow, cellCol - 1)):
            que.append([cellRow, cellCol - 1])
            minDistance[cellRow][cellCol - 1]= min(minDistance[cellRow][cellCol - 1],
                                                minDistance[cellRow][cellCol] + 1)
            visited[cellRow][cellCol - 1] = 1

        # Pop the visited cell
        que.remove(que[0])

    # Minimum distance to the corner
    # of the first row, first column
    minFromSource = min(minFromSource, minDistance[0][0])

    # Minimum distance to the corner
    # of the last row, first column
    minFromSource = min(minFromSource, minDistance[row - 1][0])

    # Minimum distance to the corner
    # of the last row, last column
    minFromSource = min(minFromSource,minDistance[row - 1][col - 1])

    # Minimum distance to the corner
    # of the first row, last column
    minFromSource = min(minFromSource, minDistance[0][col - 1])

    # If no path exists
    if (minFromSource == row * col):
        return -1

    # Return the minimum distance
    return minFromSource

# Driver code
if __name__ == '__main__':
    sourceRow = 3
    sourceCol = 3
    grid = [[1, 1, 1, 0, 0],
            [0, 0, 1, 0, 1],
            [0, 0, 1, 0, 1],
            [1, 0, 0, 0, 1],
            [1, 1, 0, 1, 0]]

    print(minDistance1(grid, sourceRow, sourceCol))

# This code is contributed by
# Surendra_Gangwar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Pair class
class Pair
{
    constructor(a, b)
    {
        this.first = a;
        this.second = b;
    }
}

let row = 5;
let col = 5;

// Global variables for grid, minDistance and visited array
let minDistance = new Array(row + 1);
let visited = new Array(row + 1);
for(let i = 0; i < row + 1; i++)
{
    minDistance[i] = new Array(col+1);
    visited[i] = new Array(col+1);
    for(let j = 0; j < col + 1; j++)
    {
        minDistance[i][j] = 0;
        visited[i][j] = 0;
    }

}

// Queue for BFS
let que = [];

// Function to find whether the move is valid or not
function isValid(grid,i,j)
{
    if (i < 0 || j < 0
        || j >= col || i >= row
        || grid[i][j] != 0 || visited[i][j] != 0)
        return false;

    return true;
}

// Function to return the minimum distance
// from source to the end of the grid
function _minDistance(grid,sourceRow,sourceCol)
{
    // If source is one of the destinations
    if ((sourceCol == 0 && sourceRow == 0)
        || (sourceCol == col - 1 && sourceRow == 0)
        || (sourceCol == 0 && sourceRow == row - 1)
        || (sourceCol == col - 1 && sourceRow == row - 1))
        return 0;

    // Set minimum value
    let minFromSource = row * col;

    // Precalculate minDistance of each grid with R * C
    for (let i = 0; i < row; i++)
        for (let j = 0; j < col; j++)
            minDistance[i][j] = row * col;

    // Insert source position in queue
    que.push(new Pair(sourceRow, sourceCol));

    // Update minimum distance to visit source
    minDistance[sourceRow][sourceCol] = 0;

    // Set source to visited
    visited[sourceRow][sourceCol] = 1;

    // BFS approach for calculating the minDistance
    // of each cell from source
    while (que.length > 0)
    {

        // Iterate over all four cells adjacent
        // to current cell
        let cell = que[0];

        // Initialize position of current cell
        let cellRow = cell.first;
        let cellCol = cell.second;

        // Cell below the current cell
        if (isValid(grid, cellRow + 1, cellCol))
        {

            // add new cell to the queue
            que.push(new Pair(cellRow + 1, cellCol));

            // Update one of its neightbor's distance
            minDistance[cellRow + 1][cellCol]
                = Math.min(minDistance[cellRow + 1][cellCol],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow + 1][cellCol] = 1;
        }

        // Above the current cell
        if (isValid(grid, cellRow - 1, cellCol))
        {
            que.push(new Pair(cellRow - 1, cellCol));
            minDistance[cellRow - 1][cellCol]
                = Math.min(minDistance[cellRow - 1][cellCol],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow - 1][cellCol] = 1;
        }

        // Right cell
        if (isValid(grid, cellRow, cellCol + 1))
        {
            que.push(new Pair(cellRow, cellCol + 1));
            minDistance[cellRow][cellCol + 1]
                = Math.min(minDistance[cellRow][cellCol + 1],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow][cellCol + 1] = 1;
        }

        // Left cell
        if (isValid(grid, cellRow, cellCol - 1))
        {
            que.push(new Pair(cellRow, cellCol - 1));
            minDistance[cellRow][cellCol - 1]
                = Math.min(minDistance[cellRow][cellCol - 1],
                    minDistance[cellRow][cellCol] + 1);
            visited[cellRow][cellCol - 1] = 1;
        }

        // remove the visited cell
        que.shift();
    }

    let i;

    // Minimum distance to the corner
    // of the first row, first column
    minFromSource = Math.min(minFromSource,
                        minDistance[0][0]);

    // Minimum distance to the corner
    // of the last row, first column
    minFromSource = Math.min(minFromSource,
                        minDistance[row - 1][0]);

    // Minimum distance to the corner
    // of the last row, last column
    minFromSource = Math.min(minFromSource,
                        minDistance[row - 1][col - 1]);

    // Minimum distance to the corner
    // of the first row, last column
    minFromSource = Math.min(minFromSource,
                        minDistance[0][col - 1]);

    // If no path exists
    if (minFromSource == row * col)
        return -1;

    // Return the minimum distance
    return minFromSource;
}

// Driver code
let sourceRow = 3, sourceCol = 3;
let grid = [[1, 1, 1, 0, 0],
                    [0, 0, 1, 0, 1],
                    [0, 0, 1, 0, 1],
                    [1, 0, 0, 0, 1],
                    [1, 1, 0, 1, 0]];
document.write(_minDistance(grid, sourceRow, sourceCol));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4
```