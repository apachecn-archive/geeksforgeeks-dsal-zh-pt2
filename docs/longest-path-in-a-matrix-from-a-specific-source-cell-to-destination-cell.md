# 矩阵中从特定源单元到目的单元的最长路径

> 原文:[https://www . geesforgeks . org/从特定源单元到目标单元的矩阵中最长路径/](https://www.geeksforgeeks.org/longest-path-in-a-matrix-from-a-specific-source-cell-to-destination-cell/)

给定矩阵 **mat[][]，**以及源节点和目的节点的坐标，任务是找到从源到目的地的最长路径的长度。

**示例:**

> **输入:** mat[][] = {{5，6，7，8}，{4，1，0，9}，{3，2，11，10}}，src = {1，1}，dest = {2，2 }
> T3】输出:11
> T6】解释:坐标(1，1)和(2，2)之间的最长路径有 11 个节点，路径给出为 1->2->3-
> 
> ****输入:** mat = {{5，4，1，0}，{6，3，2，0}，{7，8，9，0}}，src = {0，1}，dest = {2，2 }
> T3】输出: 12**

****方法:**给定的问题可以使用[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)来解决。想法是使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来探索从源到目的地的每条路径，并计算路径之间的节点数量。按照以下步骤解决问题:**

*   **从源节点到目的节点应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

    *   在上述四个方向上遍历，在每个节点上，增加遍历的节点数。
    *   在**访问过的[][]** [数组](https://www.geeksforgeeks.org/array-data-structure/)中，将当前路径中的节点标记为已访问，并递归调用所有四个方向上的未访问节点。
    *   到达目的地节点后，更新到达目的地所需行进的最大节点数。** 
*   **保持所有路径上节点的最大数量，这是必需的答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Depth-First-Search function for
// recursion and backtracking
void dfs(vector<vector<int>> mat, int maxi[],
         vector<vector<int>> visited, int len,
         int i, int j, int dest[])
{

    // Return if current node is already
    // visited or it is out of bounds
    if (i < 0 || j < 0 || i == mat.size() || j == mat[0].size() || visited[i][j])
        return;

    // If reached the destination
    // then update maximum length
    if (i == dest[0] && j == dest[1])
    {

        // Update max
        maxi[0] = max(maxi[0], len);

        return;
    }

    // Mark current node as visited
    visited[i][j] = true;

    // Recursive call in all
    // the four directions
    dfs(mat, maxi, visited, len + 1, i, j - 1, dest);
    dfs(mat, maxi, visited, len + 1, i + 1, j, dest);
    dfs(mat, maxi, visited, len + 1, i - 1, j, dest);
    dfs(mat, maxi, visited, len + 1, i, j + 1, dest);

    // Mark current cell as unvisited
    visited[i][j] = false;
}

// Function to find the length of
// the longest path between two nodes
int longestPath(vector<vector<int>> mat, int src[],
                int dest[])
{

    // Initialize a variable to
    // calculate longest path
    int maxi[1];
    maxi[0] = 0;

    // Number of rows
    int N = mat.size();

    // Number of columns
    int M = mat[0].size();

    // Initialize a boolean matrix to
    // keep track of the cells visited
    vector<vector<int>> visited(N, vector<int>(M, 0));

    // Call the depth-first-search
    dfs(mat, maxi, visited, 0, src[0], src[1], dest);

    // Return the answer
    return maxi[0] + 1;
}

// Driver code
int main()
{
    vector<vector<int>> mat = {{5, 6, 7, 8},
                               {4, 1, 0, 9},
                               {3, 2, 11, 10}};
    int src[] = {1, 1};
    int dest[] = {2, 2};

    cout << (longestPath(mat, src, dest));
}

// This code is contributed by Potta Lokesh
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation for the above approach
import java.io.*;
import java.lang.Math;
import java.util.*;

// Driver code
class GFG {

    // Function to find the length of
    // the longest path between two nodes
    public static int longestPath(int[][] mat, int[] src,
                                  int[] dest)
    {

        // Initialize a variable to
        // calculate longest path
        int[] max = new int[1];

        // Number of rows
        int N = mat.length;

        // Number of columns
        int M = mat[0].length;

        // Initialize a boolean matrix to
        // keep track of the cells visited
        boolean[][] visited = new boolean[N][M];

        // Call the depth-first-search
        dfs(mat, max, visited, 0, src[0], src[1], dest);

        // Return the answer
        return max[0] + 1;
    }

    // Depth-First-Search function for
    // recursion and backtracking
    public static void dfs(int[][] mat, int[] max,
                           boolean[][] visited, int len,
                           int i, int j, int[] dest)
    {
        // Return if current node is already
        // visited or it is out of bounds
        if (i < 0 || j < 0 || i == mat.length
            || j == mat[0].length || visited[i][j])
            return;

        // If reached the destination
        // then update maximum length
        if (i == dest[0] && j == dest[1]) {

            // Update max
            max[0] = Math.max(max[0], len);

            return;
        }

        // Mark current node as visited
        visited[i][j] = true;

        // Recursive call in all
        // the four directions
        dfs(mat, max, visited, len + 1, i, j - 1, dest);
        dfs(mat, max, visited, len + 1, i + 1, j, dest);
        dfs(mat, max, visited, len + 1, i - 1, j, dest);
        dfs(mat, max, visited, len + 1, i, j + 1, dest);

        // Mark current cell as unvisited
        visited[i][j] = false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[][] mat = { { 5, 6, 7, 8 },
                        { 4, 1, 0, 9 },
                        { 3, 2, 11, 10 } };
        int[] src = { 1, 1 };
        int[] dest = { 2, 2 };

        System.out.println(longestPath(mat, src, dest));
    }
}
```

## **蟒蛇 3**

```
# Python 3 implementation for the above approach

# Depth-First-Search function for
# recursion and backtracking
def dfs(mat, maxi, visited, length, i, j, dest):

    # Return if current node is already
    # visited or it is out of bounds
    if (i < 0 or j < 0 or i == len(mat) or j == len(mat[0]) or visited[i][j]):
        return

    # If reached the destination
    # then update maximum length
    if (i == dest[0] and j == dest[1]):

        # Update max
        maxi[0] = max(maxi[0], length)

        return

    # Mark current node as visited
    visited[i][j] = True

    # Recursive call in all
    # the four directions
    dfs(mat, maxi, visited, length + 1, i, j - 1, dest)
    dfs(mat, maxi, visited, length + 1, i + 1, j, dest)
    dfs(mat, maxi, visited, length + 1, i - 1, j, dest)
    dfs(mat, maxi, visited, length + 1, i, j + 1, dest)

    # Mark current cell as unvisited
    visited[i][j] = False

# Function to find the length of
# the longest path between two nodes
def longestPath(mat,  src,
                dest):

    # Initialize a variable to
    # calculate longest path
    maxi = [0]*1
    maxi[0] = 0

    # Number of rows
    N = len(mat)

    # Number of columns
    M = len(mat[0])

    # Initialize a boolean matrix to
    # keep track of the cells visited
    visited = [[0 for x in range(M)] for y in range(N)]

    # Call the depth-first-search
    dfs(mat, maxi, visited, 0, src[0], src[1], dest)

    # Return the answer
    return maxi[0] + 1

# Driver code
if __name__ == "__main__":

    mat = [[5, 6, 7, 8],
           [4, 1, 0, 9],
           [3, 2, 11, 10]]
    src = [1, 1]
    dest = [2, 2]

    print(longestPath(mat, src, dest))

    # This code is contributed by ukasp.
```

## **C#**

```
// C# implementation for the above approach
using System;

// Driver code
class GFG {

    // Function to find the length of
    // the longest path between two nodes
    public static int longestPath(int[,] mat, int[] src,
                                  int[] dest)
    {

        // Initialize a variable to
        // calculate longest path
        int[] max = new int[1];

        // Number of rows
        int N = mat.GetLength(0);

        // Number of columns
        int M = mat.GetLength(1);

        // Initialize a boolean matrix to
        // keep track of the cells visited
        bool[,] visited = new bool[N, M];

        // Call the depth-first-search
        dfs(mat, max, visited, 0, src[0], src[1], dest);

        // Return the answer
        return max[0] + 1;
    }

    // Depth-First-Search function for
    // recursion and backtracking
    public static void dfs(int[,] mat, int[] max,
                           bool[,] visited, int len,
                           int i, int j, int[] dest)
    {

        // Return if current node is already
        // visited or it is out of bounds
        if (i < 0 || j < 0 || i == mat.GetLength(0)
            || j == mat.GetLength(1)|| visited[i, j])
            return;

        // If reached the destination
        // then update maximum length
        if (i == dest[0] && j == dest[1]) {

            // Update max
            max[0] = Math.Max(max[0], len);

            return;
        }

        // Mark current node as visited
        visited[i, j] = true;

        // Recursive call in all
        // the four directions
        dfs(mat, max, visited, len + 1, i, j - 1, dest);
        dfs(mat, max, visited, len + 1, i + 1, j, dest);
        dfs(mat, max, visited, len + 1, i - 1, j, dest);
        dfs(mat, max, visited, len + 1, i, j + 1, dest);

        // Mark current cell as unvisited
        visited[i, j] = false;
    }

    // Driver code
    public static void Main()
    {
        int[,] mat = { { 5, 6, 7, 8 },
                        { 4, 1, 0, 9 },
                        { 3, 2, 11, 10 } };
        int[] src = { 1, 1 };
        int[] dest = { 2, 2 };

        Console.Write(longestPath(mat, src, dest));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

```
<script>
// Javascript implementation for the above approach

// Depth-First-Search function for
// recursion and backtracking
function dfs(mat, maxi, visited, len, i, j, dest) {

    // Return if current node is already
    // visited or it is out of bounds
    if (i < 0 || j < 0 || i == mat.length || j == mat[0].length || visited[i][j])
        return;

    // If reached the destination
    // then update maximum length
    if (i == dest[0] && j == dest[1]) {

        // Update max
        maxi[0] = Math.max(maxi[0], len);

        return;
    }

    // Mark current node as visited
    visited[i][j] = true;

    // Recursive call in all
    // the four directions
    dfs(mat, maxi, visited, len + 1, i, j - 1, dest);
    dfs(mat, maxi, visited, len + 1, i + 1, j, dest);
    dfs(mat, maxi, visited, len + 1, i - 1, j, dest);
    dfs(mat, maxi, visited, len + 1, i, j + 1, dest);

    // Mark current cell as unvisited
    visited[i][j] = false;
}

// Function to find the length of
// the longest path between two nodes
function longestPath(mat, src, dest) {

    // Initialize a variable to
    // calculate longest path
    let maxi = new Array(1);
    maxi[0] = 0;

    // Number of rows
    let N = mat.length;

    // Number of columns
    let M = mat[0].length;

    // Initialize a boolean matrix to
    // keep track of the cells visited
    let visited = new Array(N).fill(0).map(() => new Array(M).fill(0));

    // Call the depth-first-search
    dfs(mat, maxi, visited, 0, src[0], src[1], dest);

    // Return the answer
    return maxi[0] + 1;
}

// Driver code
let mat = [[5, 6, 7, 8], [4, 1, 0, 9], [3, 2, 11, 1]];
let src = [1, 1];
let dest = [2, 2];

document.write(longestPath(mat, src, dest));

// This code is contributed by gfgking
</script>
```

****Output**

```
11
```** 

*****时间复杂度:**O(4<sup>(N+M)</sup>)*
***辅助空间:** O(N * M)***