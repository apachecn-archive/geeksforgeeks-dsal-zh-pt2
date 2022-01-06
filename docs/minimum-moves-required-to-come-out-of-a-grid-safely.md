# 安全离开电网所需的最小移动量

> 原文:[https://www . geeksforgeeks . org/最小移动-要求安全脱离网格/](https://www.geeksforgeeks.org/minimum-moves-required-to-come-out-of-a-grid-safely/)

给定一个大小为 **M * N** 的格子 **mat[][]** ，仅由 **0** s、 **1** s 和 **2** s 组成，其中 **0** 代表空的地方， **1** 代表一个人， **2** 代表火，任务是计算所需的最小移动次数，使该人安全地从格子中出来。在每一步中，火会燃烧它旁边的细胞，人会从当前的细胞移动到它旁边的细胞之一。如果无法从网格中出来，则打印 **-1** 。

**注意:**如果一个人到达网格的一个边界边，他就会从网格中出来。

**示例:**

> **输入:** mat[][] = { { 0，0，0，0 }，{ 2，0，0，0 }，{ 2，1，0，0 }，{ 2，2，0，0 } }
> **输出:** 2
> **解释:**
> 人可能的招式有(2，1) → (2，2) → (2，3)。
> 人在 2 次移动中到达网格的一个边界边(最后一行)，这也是最小可能计数。
> 因此，要求输出为 2。
> 
> **输入:** mat[][] = { { 0，2，0，0 }，{ 2，1，0，2 }，{ 2，0，0，0 }，{ 2，0，2，0 }}
> **输出:** -1

**方法:**问题可以用概念解决问题[烂橘子](https://practice.geeksforgeeks.org/problems/rotten-oranges2536/1)解决。这个想法是表演 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 在蔓延的火以及人的动作。按照以下步骤解决问题:

1.  初始化两个空的[队列](https://www.geeksforgeeks.org/queue-data-structure/) **fQ** 和 **pQ** ，分别存放火能蔓延和人能移动到的牢房。
2.  初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，比如**访问了【】【】**，检查这个人是否已经访问了单元格 **(i，j)** 。
3.  将此人的所有侧面相邻单元格入队，并将所有相邻单元格标记为访问单元格。
4.  将火灾单元的所有侧邻单元入队到 **fQ** 中，并将所有侧邻单元标记为燃烧单元。
5.  初始化一个变量，比如说**深度**，来跟踪两个单元格之间的[最短距离](https://www.geeksforgeeks.org/shortest-distance-two-cells-matrix-grid/)。
6.  当 **pQ** 不为空时，执行以下步骤:
    *   将**深度**增加 1。
    *   将所有单元格从 **pQ** 中出队，并将弹出单元格的所有有效边邻单元格入队。
    *   如果任何排队的相邻单元格出现在网格的边界，则打印深度值。
    *   否则，将所有单元格从 **fQ** 中出列。对于每个弹出的单元，将所有有效的相邻单元入队。
7.  从以上步骤，如果无法从网格中出来，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>

using namespace std;

// Stores size of the grid
int m, n;

// Function to check valid
// cells of the grid
bool valid(int x, int y)
{
    return (x >= 0 && x < m && y >= 0 && y < n);
}

// Checks for the border sides
bool border(int x, int y)
{
    return (x == 0 || x == m - 1 || y == 0 || y == n - 1);
}

// Function to find shortest distance
// between two cells of the grid
int minStep(vector<vector<int>> mat)
{

    // Rows of the grid
    m = mat.size();

    // Column of the grid
    n = mat[0].size();

    // Stores possible move
    // of the person
    int dx[] = { 1, -1, 0, 0 };
    int dy[] = { 0, 0, 1, -1 };

    // Store possible cells visited
    // by the person
    queue<pair<int,int> > pQ;

    // Store possible cells which
    // are burning
    queue<pair<int,int> > fQ;

    // Traverse the grid
    for (int i = 0; i < m; i++){

        for (int j = 0; j < n; j++) {

            // If current cell is
            // burning
            if (mat[i][j] == 2)
                fQ.push({i, j});
            // If person is in
            // the current cell
            else if (mat[i][j] == 1) {
                if (border(i, j))
                    return 0;
                pQ.push({i, j});
            }
        }
    }
    // Stores shortest distance
    // between two cells
    int depth = 0;

    // Check if a cell is visited
    // by the person or not
    vector<vector<int>> visited(n,vector<int>(m,0));

    // While pQ is not empty
    while (pQ.size()>0) {

        // Update depth
        depth++;

        // Popped all the cells from
        // pQ and mark all adjacent cells
        // of as visited
        for (int i = pQ.size(); i > 0;i--) {

            // Front element of
            // the queue pQ
            pair<int,int>  pos = pQ.front();

            // Remove front element of
            // the queue pQ
            pQ.pop();

            // If current cell is burning
            if (mat[pos.first][pos.second] == 2)
                continue;

            // Find all adjacent cells
            for (int j = 0; j < 4; j++) {

                // Stores row number of
                // adjacent cell
                int x = pos.first + dx[j];

                // Stores column number
                // of adjacent cell
                int y = pos.second + dy[j];

                // Checks if current cell
                // is valid
                if (valid(x, y) && mat[x][y] != 2 && !visited[x][y]) {

                    // Mark the cell as visited
                    visited[x][y] = 1;

                    // Enqueue the cell
                    pQ.push(pair<int,int> (x, y));

                    // Checks the escape condition
                    if (border(x, y))
                        return depth;
                }
            }
        }

        // Burn all the adjacent cells
        // of burning cells
        for (int i = fQ.size(); i > 0; i--) {

            // Front element of
            // the queue fQ
            pair<int,int>  pos = fQ.front();

            // Delete front element of
            // the queue fQ
            fQ.pop();

            // Find adjacent cells of
            // burning cell
            for (int j = 0; j < 4; j++) {

                // Stores row number of
                // adjacent cell
                int x = pos.first + dx[j];

                // Stores column number
                // of adjacent cell
                int y = pos.second + dy[j];

                // Checks if current
                // cell is valid
                if (valid(x, y) && mat[x][y] != 2) {

                    mat[x][y] = 2;

                    // Burn all the adjacent
                    // cells of current cell
                    fQ.push(pair<int,int> (x, y));
                }
            }
        }
    }
    return -1;
}

// Driver Code
int main()
{

    // Given grid
    vector<vector<int>> grid = { { 0, 0, 0, 0 },
                     { 2, 0, 0, 0 },
                     { 2, 1, 0, 0 },
                     { 2, 2, 0, 0 } };

    cout<<minStep(grid);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;
class GFG
{

    // Structure of cell
    // of the grid
    static class pair
    {
        int x, y;
        pair(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // Stores size of the grid
    static int m, n;

    // Function to find shortest distance
    // between two cells of the grid
    static int minStep(int[][] mat)
    {

        // Rows of the grid
        m = mat.length;

        // Column of the grid
        n = mat[0].length;

        // Stores possible move
        // of the person
        int dx[] = { 1, -1, 0, 0 };
        int dy[] = { 0, 0, 1, -1 };

        // Store possible cells visited
        // by the person
        Queue<pair> pQ = new LinkedList<>();

        // Store possible cells which
        // are burning
        Queue<pair> fQ = new LinkedList<>();

        // Traverse the grid
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
            {

                // If current cell is
                // burning
                if (mat[i][j] == 2)
                    fQ.add(new pair(i, j));

                // If person is in
                // the current cell
                else if (mat[i][j] == 1)
                {
                    if (border(i, j))
                        return 0;
                    pQ.add(new pair(i, j));
                }
            }

        // Stores shortest distance
        // between two cells
        int depth = 0;

        // Check if a cell is visited
        // by the person or not
        boolean[][] visited
            = new boolean[n][m];

        // While pQ is not empty
        while (!pQ.isEmpty())
        {

            // Update depth
            depth++;

            // Popped all the cells from
            // pQ and mark all adjacent cells
            // of as visited
            for (int i = pQ.size(); i > 0; i--)
            {

                // Front element of
                // the queue pQ
                pair pos = pQ.peek();

                // Remove front element of
                // the queue pQ
                pQ.remove();

                // If current cell is burning
                if (mat[pos.x][pos.y] == 2)
                    continue;

                // Find all adjacent cells
                for (int j = 0; j < 4; j++)
                {

                    // Stores row number of
                    // adjacent cell
                    int x = pos.x + dx[j];

                    // Stores column number
                    // of adjacent cell
                    int y = pos.y + dy[j];

                    // Checks if current cell
                    // is valid
                    if (valid(x, y) && mat[x][y] != 2
                        && !visited[x][y])
                    {

                        // Mark the cell as visited
                        visited[x][y] = true;

                        // Enqueue the cell
                        pQ.add(new pair(x, y));

                        // Checks the escape condition
                        if (border(x, y))
                            return depth;
                    }
                }
            }

            // Burn all the adjacent cells
            // of burning cells
            for (int i = fQ.size(); i > 0; i--)
            {

                // Front element of
                // the queue fQ
                pair pos = fQ.peek();

                // Delete front element of
                // the queue fQ
                fQ.remove();

                // Find adjacent cells of
                // burning cell
                for (int j = 0; j < 4; j++)
                {

                    // Stores row number of
                    // adjacent cell
                    int x = pos.x + dx[j];

                    // Stores column number
                    // of adjacent cell
                    int y = pos.y + dy[j];

                    // Checks if current
                    // cell is valid
                    if (valid(x, y) && mat[x][y] != 2)
                    {

                        mat[x][y] = 2;

                        // Burn all the adjacent
                        // cells of current cell
                        fQ.add(new pair(x, y));
                    }
                }
            }
        }
        return -1;
    }

    // Function to check valid
    // cells of the grid
    static boolean valid(int x, int y)
    {
        return (x >= 0 && x < m
                && y >= 0 && y < n);
    }

    // Checks for the border sides
    static boolean border(int x, int y)
    {
        return (x == 0 || x == m - 1
                || y == 0 || y == n - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given grid
        int[][] grid = { { 0, 0, 0, 0 },
                         { 2, 0, 0, 0 },
                         { 2, 1, 0, 0 },
                         { 2, 2, 0, 0 } };

        System.out.println(minStep(grid));
    }
}

// This code is contributed by mohit kumar 29.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Stores size of the grid
m = 0
n = 0

# Function to check valid
# cells of the grid
def valid(x, y):

    global n
    global m
    return (x >= 0 and x < m and
            y >= 0 and y < n)

# Checks for the border sides
def border(x, y):

    global n
    global m
    return (x == 0 or x == m - 1 or
            y == 0 or y == n - 1)

# Function to find shortest distance
# between two cells of the grid
def minStep(mat):

    global n
    global m

    # Rows of the grid
    m = len(mat)

    # Column of the grid
    n = len(mat[0])

    # Stores possible move
    # of the person
    dx = [1, -1, 0, 0]
    dy = [0, 0, 1, -1]

    # Store possible cells visited
    # by the person
    pQ = []

    # Store possible cells which
    # are burning
    fQ = []

    # Traverse the grid
    for i in range(m):
        for j in range(n):

            # If current cell is
            # burning
            if (mat[i][j] == 2):
                fQ.append([i, j])

            # If person is in
            # the current cell
            elif(mat[i][j] == 1):
                if (border(i, j)):
                    return 0

                pQ.append([i, j])

    # Stores shortest distance
    # between two cells
    depth = 0

    # Check if a cell is visited
    # by the person or not
    visited = [[0 for i in range(m)]
                  for j in range(n)]

    # While pQ is not empty
    while (len(pQ) > 0):

        # Update depth
        depth += 1

        # Popped all the cells from
        # pQ and mark all adjacent cells
        # of as visited
        i = len(pQ)

        while(i > 0):

            # Front element of
            # the queue pQ
            pos = pQ[0]

            # Remove front element of
            # the queue pQ
            pQ.remove(pQ[0])

            # If current cell is burning
            if (mat[pos[0]][pos[1]] == 2):
                continue

            # Find all adjacent cells
            for j in range(4):

                # Stores row number of
                # adjacent cell
                x = pos[0] + dx[j]

                # Stores column number
                # of adjacent cell
                y = pos[1] + dy[j]

                # Checks if current cell
                # is valid
                if (valid(x, y) and mat[x][y] != 2 and
                    visited[x][y] == 0):

                    # Mark the cell as visited
                    visited[x][y] = 1

                    # Enqueue the cell
                    pQ.append([x, y])

                    # Checks the escape condition
                    if (border(x, y)):
                        return depth

            i -= 1

        # Burn all the adjacent cells
        # of burning cells
        i = len(fQ)

        while(i > 0):

            # Front element of
            # the queue fQ
            pos = fQ[0]

            # Delete front element of
            # the queue fQ
            fQ.remove(fQ[0])

            # Find adjacent cells of
            # burning cell
            for j in range(4):

                # Stores row number of
                # adjacent cell
                x = pos[0] + dx[j]

                # Stores column number
                # of adjacent cell
                y = pos[1] + dy[j]

                # Checks if current
                # cell is valid
                if (valid(x, y) and mat[x][y] != 2):
                    mat[x][y] = 2

                    # Burn all the adjacent
                    # cells of current cell
                    fQ.append([x, y])

            i -= 1

    return -1

# Driver Code
if __name__ == '__main__':

    # Given grid
    grid = [ [ 0, 0, 0, 0 ],
             [ 2, 0, 0, 0 ],
             [ 2, 1, 0, 0 ],
             [ 2, 2, 0, 0 ] ]

    print(minStep(grid))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Structure of cell
  // of the grid
  class pair
  {
    public int x, y;
    public pair(int x, int y)
    {
      this.x = x;
      this.y = y;
    }
  }

  // Stores size of the grid
  static int m, n;

  // Function to find shortest distance
  // between two cells of the grid
  static int minStep(int[,] mat)
  {

    // Rows of the grid
    m = mat.GetLength(0);

    // Column of the grid
    n = mat.GetLength(1);

    // Stores possible move
    // of the person
    int []dx = { 1, -1, 0, 0 };
    int []dy = { 0, 0, 1, -1 };

    // Store possible cells visited
    // by the person
    Queue<pair> pQ = new Queue<pair>();

    // Store possible cells which
    // are burning
    Queue<pair> fQ = new Queue<pair>();

    // Traverse the grid
    for (int i = 0; i < m; i++)
      for (int j = 0; j < n; j++)
      {

        // If current cell is
        // burning
        if (mat[i, j] == 2)
          fQ.Enqueue(new pair(i, j));

        // If person is in
        // the current cell
        else if (mat[i, j] == 1)
        {
          if (border(i, j))
            return 0;
          pQ.Enqueue(new pair(i, j));
        }
      }

    // Stores shortest distance
    // between two cells
    int depth = 0;

    // Check if a cell is visited
    // by the person or not
    bool[,] visited
      = new bool[n, m];

    // While pQ is not empty
    while (pQ.Count != 0)
    {

      // Update depth
      depth++;

      // Popped all the cells from
      // pQ and mark all adjacent cells
      // of as visited
      for (int i = pQ.Count; i > 0; i--)
      {

        // Front element of
        // the queue pQ
        pair pos = pQ.Peek();

        // Remove front element of
        // the queue pQ
        pQ.Dequeue();

        // If current cell is burning
        if (mat[pos.x, pos.y] == 2)
          continue;

        // Find all adjacent cells
        for (int j = 0; j < 4; j++)
        {

          // Stores row number of
          // adjacent cell
          int x = pos.x + dx[j];

          // Stores column number
          // of adjacent cell
          int y = pos.y + dy[j];

          // Checks if current cell
          // is valid
          if (valid(x, y) && mat[x, y] != 2
              && !visited[x, y])
          {

            // Mark the cell as visited
            visited[x, y] = true;

            // Enqueue the cell
            pQ.Enqueue(new pair(x, y));

            // Checks the escape condition
            if (border(x, y))
              return depth;
          }
        }
      }

      // Burn all the adjacent cells
      // of burning cells
      for (int i = fQ.Count; i > 0; i--)
      {

        // Front element of
        // the queue fQ
        pair pos = fQ.Peek();

        // Delete front element of
        // the queue fQ
        fQ.Dequeue();

        // Find adjacent cells of
        // burning cell
        for (int j = 0; j < 4; j++)
        {

          // Stores row number of
          // adjacent cell
          int x = pos.x + dx[j];

          // Stores column number
          // of adjacent cell
          int y = pos.y + dy[j];

          // Checks if current
          // cell is valid
          if (valid(x, y) && mat[x, y] != 2)
          {

            mat[x, y] = 2;

            // Burn all the adjacent
            // cells of current cell
            fQ.Enqueue(new pair(x, y));
          }
        }
      }
    }
    return -1;
  }

  // Function to check valid
  // cells of the grid
  static bool valid(int x, int y)
  {
    return (x >= 0 && x < m
            && y >= 0 && y < n);
  }

  // Checks for the border sides
  static bool border(int x, int y)
  {
    return (x == 0 || x == m - 1
            || y == 0 || y == n - 1);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given grid
    int[,] grid = { { 0, 0, 0, 0 },
                   { 2, 0, 0, 0 },
                   { 2, 1, 0, 0 },
                   { 2, 2, 0, 0 } };

    Console.WriteLine(minStep(grid));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Stores size of the grid
var m, n;

// Function to check valid
// cells of the grid
function valid(x, y)
{
    return (x >= 0 && x < m && y >= 0 && y < n);
}

// Checks for the border sides
function border(x, y)
{
    return (x == 0 || x == m - 1 || y == 0 || y == n - 1);
}

// Function to find shortest distance
// between two cells of the grid
function minStep(mat)
{

    // Rows of the grid
    m = mat.length;

    // Column of the grid
    n = mat[0].length;

    // Stores possible move
    // of the person
    var dx = [1, -1, 0, 0];
    var dy = [0, 0, 1, -1];

    // Store possible cells visited
    // by the person
    var pQ = [];

    // Store possible cells which
    // are burning
    var fQ = [];

    // Traverse the grid
    for (var i = 0; i < m; i++){

        for (var j = 0; j < n; j++) {

            // If current cell is
            // burning
            if (mat[i][j] == 2)
                fQ.push([i, j]);
            // If person is in
            // the current cell
            else if (mat[i][j] == 1) {
                if (border(i, j))
                    return 0;
                pQ.push([i, j]);
            }
        }
    }
    // Stores shortest distance
    // between two cells
    var depth = 0;

    // Check if a cell is visited
    // by the person or not
    var visited = Array.from(Array(n), ()=> Array(m).fill(0));

    // While pQ is not empty
    while (pQ.length>0) {

        // Update depth
        depth++;

        // Popped all the cells from
        // pQ and mark all adjacent cells
        // of as visited
        for (var i = pQ.length; i > 0;i--) {

            // Front element of
            // the queue pQ
            var pos = pQ[0];
          // Remove front element of
            // the queue pQ
            pQ.shift();

            // If current cell is burning
            if (mat[pos[0]][pos[1]] == 2)
                continue;

            // Find all adjacent cells
            for (var j = 0; j < 4; j++) {

                // Stores row number of
                // adjacent cell
                var x = pos[0] + dx[j];

                // Stores column number
                // of adjacent cell
                var y = pos[1] + dy[j];

                // Checks if current cell
                // is valid
                if (valid(x, y) && mat[x][y] != 2 && !visited[x][y]) {

                    // Mark the cell as visited
                    visited[x][y] = 1;

                    // Enqueue the cell
                    pQ.push([x, y]);

                    // Checks the escape condition
                    if (border(x, y))
                        return depth;
                }
            }
        }

        // Burn all the adjacent cells
        // of burning cells
        for (var i = fQ.length; i > 0; i--) {

            // Front element of
            // the queue fQ
            var pos = fQ[0];

            // Delete front element of
            // the queue fQ
            fQ.shift();

            // Find adjacent cells of
            // burning cell
            for (var j = 0; j < 4; j++) {

                // Stores row number of
                // adjacent cell
                var x = pos[0] + dx[j];

                // Stores column number
                // of adjacent cell
                var y = pos[1] + dy[j];

                // Checks if current
                // cell is valid
                if (valid(x, y) && mat[x][y] != 2) {

                    mat[x][y] = 2;

                    // Burn all the adjacent
                    // cells of current cell
                    fQ.push([x, y]);
                }
            }
        }
    }
    return -1;
}

// Driver Code
// Given grid
var grid = [ [ 0, 0, 0, 0 ],
                 [ 2, 0, 0, 0 ],
                 [ 2, 1, 0, 0 ],
                 [ 2, 2, 0, 0 ] ];
document.write( minStep(grid));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*