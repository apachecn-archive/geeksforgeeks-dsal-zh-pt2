# 允许向左、向右、向下和向上移动的最小成本路径

> 原文:[https://www . geesforgeks . org/最低成本-路径-左-右-底部-移动-允许/](https://www.geeksforgeeks.org/minimum-cost-path-left-right-bottom-moves-allowed/)

给定一个二维网格，其中每个单元格都包含整数成本，该成本表示遍历该单元格的成本，我们需要找到一条从左上角单元格到右下角单元格的路径，通过该路径产生的总成本最小。
**注:**假设投入矩阵中不存在负成本周期。
这个问题是下面问题的延伸。
[允许右移和下移的最小成本路径。](https://www.geeksforgeeks.org/dynamic-programming-set-6-min-cost-path/)
在前面的问题中，只允许向右和向下，但在这个问题中，我们可以向下、向上、向右和向左，即在所有 4 个方向上。
示例:

```
A cost grid is given in below diagram, minimum 
cost to reach bottom right from top left 
is 327 (= 31 + 10 + 13 + 47 + 65 + 12 + 18 + 
6 + 33 + 11 + 20 + 41 + 20)

The chosen least cost path is shown in green.
```

不可能使用类似于先前问题的动态编程来解决这个问题，因为这里当前状态不仅取决于右和底部单元，还取决于左和上部单元。我们使用[迪克斯特拉算法](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)来解决这个问题。网格的每个单元代表一个顶点和邻近顶点的相邻单元。我们不会从这些单元格中生成一个明确的图形，而是使用 dijkstra 算法中的矩阵。
在下面的代码中[使用了迪克斯特拉算法的实现](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-set-in-stl/)。下面实现的代码被改变以处理矩阵表示的隐式图。也请参见下面代码中 dx 和 dy 数组的使用，这些数组用于简化访问每个单元的相邻顶点的过程。

## C++

```
// C++ program to get least cost path in a grid from
// top-left to bottom-right
#include <bits/stdc++.h>
using namespace std;

#define ROW 5
#define COL 5

// structure for information of each cell
struct cell
{
    int x, y;
    int distance;
    cell(int x, int y, int distance) :
        x(x), y(y), distance(distance) {}
};

// Utility method for comparing two cells
bool operator<(const cell& a, const cell& b)
{
    if (a.distance == b.distance)
    {
        if (a.x != b.x)
            return (a.x < b.x);
        else
            return (a.y < b.y);
    }
    return (a.distance < b.distance);
}

// Utility method to check whether a point is
// inside the grid or not
bool isInsideGrid(int i, int j)
{
    return (i >= 0 && i < ROW && j >= 0 && j < COL);
}

// Method returns minimum cost to reach bottom
// right from top left
int shortest(int grid[ROW][COL], int row, int col)
{
    int dis[row][col];

    // initializing distance array by INT_MAX
    for (int i = 0; i < row; i++)
        for (int j = 0; j < col; j++)
            dis[i][j] = INT_MAX;

    // direction arrays for simplification of getting
    // neighbour
    int dx[] = {-1, 0, 1, 0};
    int dy[] = {0, 1, 0, -1};

    set<cell> st;

    // insert (0, 0) cell with 0 distance
    st.insert(cell(0, 0, 0));

    // initialize distance of (0, 0) with its grid value
    dis[0][0] = grid[0][0];

    // loop for standard dijkstra's algorithm
    while (!st.empty())
    {
        // get the cell with minimum distance and delete
        // it from the set
        cell k = *st.begin();
        st.erase(st.begin());

        // looping through all neighbours
        for (int i = 0; i < 4; i++)
        {
            int x = k.x + dx[i];
            int y = k.y + dy[i];

            // if not inside boundary, ignore them
            if (!isInsideGrid(x, y))
                continue;

            // If distance from current cell is smaller, then
            // update distance of neighbour cell
            if (dis[x][y] > dis[k.x][k.y] + grid[x][y])
            {
                // If cell is already there in set, then
                // remove its previous entry
                if (dis[x][y] != INT_MAX)
                    st.erase(st.find(cell(x, y, dis[x][y])));

                // update the distance and insert new updated
                // cell in set
                dis[x][y] = dis[k.x][k.y] + grid[x][y];
                st.insert(cell(x, y, dis[x][y]));
            }
        }
    }

    // uncomment below code to print distance
    // of each cell from (0, 0)
    /*
    for (int i = 0; i < row; i++, cout << endl)
        for (int j = 0; j < col; j++)
            cout << dis[i][j] << " ";
    */
    // dis[row - 1][col - 1] will represent final
    // distance of bottom right cell from top left cell
    return dis[row - 1][col - 1];
}

// Driver code to test above methods
int main()
{
    int grid[ROW][COL] =
    {
        31, 100, 65, 12, 18,
        10, 13, 47, 157, 6,
        100, 113, 174, 11, 33,
        88, 124, 41, 20, 140,
        99, 32, 111, 41, 20
    };

    cout << shortest(grid, ROW, COL) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get least cost path
// in a grid from top-left to bottom-right
import java.io.*;
import java.util.*;

class GFG{

static int[] dx = { -1, 0, 1, 0 };
static int[] dy = { 0, 1, 0, -1 };
static int ROW = 5;
static int COL = 5;

// Custom class for representing
// row-index, column-index &
// distance of each cell
static class Cell
{
    int x;
    int y;
    int distance;

    Cell(int x, int y, int distance)
    {
        this.x = x;
        this.y = y;
        this.distance = distance;
    }
}

// Custom comparator for inserting cells
// into Priority Queue
static class distanceComparator
  implements Comparator<Cell>
{
    public int compare(Cell a, Cell b)
    {
        if (a.distance < b.distance)
        {
            return -1;
        }
        else if (a.distance > b.distance)
        {
            return 1;
        }
        else {return 0;}
    }
}

// Utility method to check whether current
// cell is inside grid or not
static boolean isInsideGrid(int i, int j)
{
    return (i >= 0 && i < ROW &&
            j >= 0 && j < COL);
}

// Method to return shortest path from
// top-corner to bottom-corner in 2D grid
static int shortestPath(int[][] grid, int row,
                                      int col)
{
    int[][] dist = new int[row][col];

    // Initializing distance array by INT_MAX
    for(int i = 0; i < row; i++)
    {
        for(int j = 0; j < col; j++)
        {
            dist[i][j] = Integer.MAX_VALUE;
        }
    }

    // Initialized source distance as
    // initial grid position value
    dist[0][0] = grid[0][0];

    PriorityQueue<Cell> pq = new PriorityQueue<Cell>(
                  row * col, new distanceComparator());

    // Insert source cell to priority queue
    pq.add(new Cell(0, 0, dist[0][0]));
    while (!pq.isEmpty())
    {
        Cell curr = pq.poll();
        for(int i = 0; i < 4; i++)
        {
            int rows = curr.x + dx[i];
            int cols = curr.y + dy[i];

            if (isInsideGrid(rows, cols))
            {
                if (dist[rows][cols] >
                    dist[curr.x][curr.y] +
                    grid[rows][cols])
                {

                    // If Cell is already been reached once,
                    // remove it from priority queue
                    if (dist[rows][cols] != Integer.MAX_VALUE)
                    {
                        Cell adj = new Cell(rows, cols,
                                       dist[rows][cols]);

                        pq.remove(adj);
                    }

                    // Insert cell with updated distance
                    dist[rows][cols] = dist[curr.x][curr.y] +
                                       grid[rows][cols];

                    pq.add(new Cell(rows, cols,
                               dist[rows][cols]));
                }
            }
        }
    }
    return dist[row - 1][col - 1];
}

// Driver code
public static void main(String[] args)
throws IOException
{
    int[][] grid = { { 31, 100, 65, 12, 18 },
                     { 10, 13, 47, 157, 6 },
                     { 100, 113, 174, 11, 33 },
                     { 88, 124, 41, 20, 140 },
                     { 99, 32, 111, 41, 20 } };

    System.out.println(shortestPath(grid, ROW, COL));
}
}

// This code is contributed by jigyansu
```

## java 描述语言

```
<script>

// Javascript program to get least cost path in a grid from
// top-left to bottom-right
var ROW = 5
var COL = 5

// structure for information of each cell
class cell
{
    constructor(x, y, distance)
    {
        this.x = x;
        this.y = y;
        this.distance = distance;
    }
};

// Utility method to check whether a point is
// inside the grid or not
function isInsideGrid(i, j)
{
    return (i >= 0 && i < ROW && j >= 0 && j < COL);
}

// Method returns minimum cost to reach bottom
// right from top left
function shortest(grid, row, col)
{
    var dis = Array.from(Array(row), ()=>Array(col).fill(0));

    // initializing distance array by INT_MAX
    for (var i = 0; i < row; i++)
        for (var j = 0; j < col; j++)
            dis[i][j] = 1000000000;

    // direction arrays for simplification of getting
    // neighbour
    var dx = [-1, 0, 1, 0];
    var dy = [0, 1, 0, -1];

    var st = [];

    // insert (0, 0) cell with 0 distance
    st.push(new cell(0, 0, 0));

    // initialize distance of (0, 0) with its grid value
    dis[0][0] = grid[0][0];

    // loop for standard dijkstra's algorithm
    while (st.length!=0)
    {
        // get the cell with minimum distance and delete
        // it from the set
        var k = st[0];
        st.shift();

        // looping through all neighbours
        for (var i = 0; i < 4; i++)
        {
            var x = k.x + dx[i];
            var y = k.y + dy[i];

            // if not inside boundary, ignore them
            if (!isInsideGrid(x, y))
                continue;

            // If distance from current cell is smaller, then
            // update distance of neighbour cell
            if (dis[x][y] > dis[k.x][k.y] + grid[x][y])
            {
                // update the distance and insert new updated
                // cell in set
                dis[x][y] = dis[k.x][k.y] + grid[x][y];
                st.push(new cell(x, y, dis[x][y]));
            }
        }
        st.sort((a,b)=>{
            if (a.distance == b.distance)
    {
        if (a.x != b.x)
            return (a.x - b.x);
        else
            return (a.y - b.y);
    }
    return (a.distance - b.distance);
        });
    }

    // uncomment below code to print distance
    // of each cell from (0, 0)
    /*
    for (int i = 0; i < row; i++, cout << endl)
        for (int j = 0; j < col; j++)
            cout << dis[i][j] << " ";
    */
    // dis[row - 1][col - 1] will represent final
    // distance of bottom right cell from top left cell
    return dis[row - 1][col - 1];
}

// Driver code to test above methods
var grid =
[
    [31, 100, 65, 12, 18],
    [10, 13, 47, 157, 6],
    [100, 113, 174, 11, 33],
    [88, 124, 41, 20, 140],
    [99, 32, 111, 41, 20]
];
document.write(shortest(grid, ROW, COL));

// This code is contributed by rutvik_56.

</script>
```

**输出:**

```
327
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。