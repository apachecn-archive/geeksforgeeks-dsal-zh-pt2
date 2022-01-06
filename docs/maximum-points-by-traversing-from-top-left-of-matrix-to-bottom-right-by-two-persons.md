# 两个人从矩阵左上到右下遍历的最大点数

> 原文:[https://www . geesforgeks . org/两人从矩阵左上到右下遍历最大点数/](https://www.geeksforgeeks.org/maximum-points-by-traversing-from-top-left-of-matrix-to-bottom-right-by-two-persons/)

给定一个顺序为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/category/data-structures/matrix/) **网格[][]** ，单元格中有数字 **0-9** 。任务是只需向右移动**、**向下移动**，即可找到两人从 **(0，0)** 移动到 **(N-1，M-1)** 时的**最大**收款金额。如果两个人都在同一个牢房，那么只有一个人可以在那个地方取钱。**

****示例:****

> ****输入:**
> 1 1 1
> 1 0 1
> 1 1
> T6】输出: 8
> **解释:**让 1 表示人 1 收钱的地方，2 表示人 2 收钱的地方，那么一个可能的解决方案就是
> 1 1 1
> 2 0 1
> 2 2 1**
> 
> ****输入:**
> 0 9 9 3 3
> 2 9 3 3 3
> 0 3 3 3
> 4 1 1 1
> T7】输出: 52**

****方法:**问题可以通过使用[递归](https://www.geeksforgeeks.org/recursion/)来解决，通过在每个单元中向下和向右移动两个人，并在从 **(0，0)** 到 **(N-1，M-1)** 的所有路径中找到 [**最大**路径和。所以这个想法是找到所有可能路径的成本，并找到它们的最大值。](https://www.geeksforgeeks.org/maximum-path-sum-matrix/)**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const static int MAXR = 20, MAXC = 20;
int cache[MAXC][MAXR][MAXC][MAXR],
    dp[MAXC][MAXR][MAXC][MAXR];
int n, m;
vector<string> grid;

// Function to find maximum money collected
// when moving from (0, 0) to (N-1, M-1)
int maxMoney(int x1, int y1, int x2, int y2)
{
    // Out of bounds of grid
    if (x1 >= n || y1 >= m || x2 >= n || y2 >= m)
        return 0;
    if (cache[x1][y1][x2][y2] != 0)
        return dp[x1][y1][x2][y2];

    // Mark state as visited
    cache[x1][y1][x2][y2] = 1;

    // Collect money from the grid cell
    int money = grid[y1][x1] - '0';
    if (x1 != x2 || y1 != y2)
        money += grid[y2][x2] - '0';

    // Take maximum of all possibilities
    return dp[x1][y1][x2][y2]
           = money
             + max(
                   max(maxMoney(x1 + 1, y1, x2 + 1, y2),
                       maxMoney(x1, y1 + 1, x2 + 1, y2)),
                   max(maxMoney(x1 + 1, y1, x2, y2 + 1),
                       maxMoney(x1, y1 + 1, x2, y2 + 1)));
}

// Driver Code
int32_t main()
{
    // Given Input
    n = 3;
    m = 3;
    grid.push_back("111");
    grid.push_back("101");
    grid.push_back("111");

    // Function Call
    cout << maxMoney(0, 0, 0, 0);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

static int MAXR = 20, MAXC = 20;
static int [][][][]cache = new int[MAXC][MAXR][MAXC][MAXR];
static int [][][][]dp = new int[MAXC][MAXR][MAXC][MAXR];
static int n, m;
static Vector<String> grid = new Vector<String>();

// Function to find maximum money collected
// when moving from (0, 0) to (N-1, M-1)
static int maxMoney(int x1, int y1, int x2, int y2)
{
    // Out of bounds of grid
    if (x1 >= n || y1 >= m || x2 >= n || y2 >= m)
        return 0;
    if (cache[x1][y1][x2][y2] != 0)
        return dp[x1][y1][x2][y2];

    // Mark state as visited
    cache[x1][y1][x2][y2] = 1;

    // Collect money from the grid cell
    int money = grid.get(y1).charAt(x1)- '0';
    if (x1 != x2 || y1 != y2)
        money += grid.get(y2).charAt(x2) - '0';

    // Take maximum of all possibilities
    return dp[x1][y1][x2][y2]
           = money
             + Math.max(
                   Math.max(maxMoney(x1 + 1, y1, x2 + 1, y2),
                       maxMoney(x1, y1 + 1, x2 + 1, y2)),
                   Math.max(maxMoney(x1 + 1, y1, x2, y2 + 1),
                       maxMoney(x1, y1 + 1, x2, y2 + 1)));
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    n = 3;
    m = 3;
    grid.add("111");
    grid.add("101");
    grid.add("111");

    // Function Call
    System.out.print(maxMoney(0, 0, 0, 0));

}
}

// This code is contributed by Princi Singh
```

## **蟒蛇 3**

```
# Python3 program for the above approach
MAXR, MAXC = 20, 20

cache  = [[[[0 for i in range(MAXR)] for j in range(MAXC)] for k in range(MAXR)] for l in range(MAXC)]
dp  = [[[[0 for i in range(MAXR)] for j in range(MAXC)] for k in range(MAXR)] for l in range(MAXC)]

grid = []

# Function to find maximum money collected
# when moving from (0, 0) to (N-1, M-1)
def maxMoney(x1, y1, x2, y2):
    # Out of bounds of grid
    if (x1 >= n or y1 >= m or x2 >= n or y2 >= m):
        return 0
    if (cache[x1][y1][x2][y2] != 0):
        return dp[x1][y1][x2][y2]

    # Mark state as visited
    cache[x1][y1][x2][y2] = 1

    # Collect money from the grid cell
    money = ord(grid[y1][x1]) - ord('0')
    if (x1 != x2 or y1 != y2):
        money += ord(grid[y2][x2]) - ord('0')

    dp[x1][y1][x2][y2] = money + max(max(maxMoney(x1 + 1, y1, x2 + 1, y2),  maxMoney(x1, y1 + 1, x2 + 1, y2)),
                   max(maxMoney(x1 + 1, y1, x2, y2 + 1),
                       maxMoney(x1, y1 + 1, x2, y2 + 1)))

    # Take maximum of all possibilities
    return dp[x1][y1][x2][y2]

# Given Input
n = 3
m = 3
grid.append("111")
grid.append("101")
grid.append("111")

# Function Call
print(maxMoney(0, 0, 0, 0))

# This code is contributed by suresh07.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

static int MAXR = 20, MAXC = 20;
static int [,,,]cache = new int[MAXC,MAXR,MAXC,MAXR];
static int [,,,]dp = new int[MAXC,MAXR,MAXC,MAXR];
static int n, m;
static List<String> grid = new List<String>();

// Function to find maximum money collected
// when moving from (0, 0) to (N-1, M-1)
static int maxMoney(int x1, int y1, int x2, int y2)
{

    // Out of bounds of grid
    if (x1 >= n || y1 >= m || x2 >= n || y2 >= m)
        return 0;
    if (cache[x1,y1,x2,y2] != 0)
        return dp[x1,y1,x2,y2];

    // Mark state as visited
    cache[x1,y1,x2,y2] = 1;

    // Collect money from the grid cell
    int money = grid[y1][x1]- '0';
    if (x1 != x2 || y1 != y2)
        money += grid[y2][x2] - '0';

    // Take maximum of all possibilities
    return dp[x1,y1,x2,y2]
           = money
             + Math.Max(
                   Math.Max(maxMoney(x1 + 1, y1, x2 + 1, y2),
                       maxMoney(x1, y1 + 1, x2 + 1, y2)),
                   Math.Max(maxMoney(x1 + 1, y1, x2, y2 + 1),
                       maxMoney(x1, y1 + 1, x2, y2 + 1)));
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    n = 3;
    m = 3;
    grid.Add("111");
    grid.Add("101");
    grid.Add("111");

    // Function Call
    Console.Write(maxMoney(0, 0, 0, 0));

}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
    // Javascript program for the above approach

    let MAXR = 20, MAXC = 20;
    let cache = new Array(MAXC);
    let dp = new Array(MAXC);
    for(let i = 0; i < MAXR; i++)
    {
        dp[i] = new Array(MAXR);
        cache[i] = new Array(MAXR);
        for(let j = 0; j < MAXC; j++)
        {
            dp[i][j] = new Array(MAXC);
            cache[i][j] = new Array(MAXC);
            for(let k = 0; k < MAXR; k++)
            {
                dp[i][j][k] = new Array(MAXR);
                cache[i][j][k] = new Array(MAXR);
                for(let l = 0; l < MAXR; l++)
                {
                    dp[i][j][k][l] = 0;
                    cache[i][j][k][l] = 0;
                }
            }
        }
    }
    let n, m;
    let grid = [];

    // Function to find maximum money collected
    // when moving from (0, 0) to (N-1, M-1)
    function maxMoney(x1, y1, x2, y2)
    {

        // Out of bounds of grid
        if (x1 >= n || y1 >= m || x2 >= n || y2 >= m)
            return 0;
        if (cache[x1][y1][x2][y2] != 0)
            return dp[x1][y1][x2][y2];

        // Mark state as visited
        cache[x1][y1][x2][y2] = 1;

        // Collect money from the grid cell
        let money = grid[y1][x1]- '0';
        if (x1 != x2 || y1 != y2)
            money += grid[y2][x2] - '0';

        // Take maximum of all possibilities
        dp[x1][y1][x2][y2]
               = money
                 + Math.max(
                       Math.max(maxMoney(x1 + 1, y1, x2 + 1, y2),
                           maxMoney(x1, y1 + 1, x2 + 1, y2)),
                       Math.max(maxMoney(x1 + 1, y1, x2, y2 + 1),
                           maxMoney(x1, y1 + 1, x2, y2 + 1)));
          return dp[x1][y1][x2][y2];
    }

    // Given Input
    n = 3;
    m = 3;
    grid.push("111");
    grid.push("101");
    grid.push("111");

    // Function Call
    document.write(maxMoney(0, 0, 0, 0));

// This code is contributed by divyeshrabadiya07.
</script>
```

****Output**

```
8
```** 

*****时间复杂度:**O(2<sup>N</sup>* 2<sup>M</sup>)*
***辅助空间:** O((N*M) <sup>2</sup> )***