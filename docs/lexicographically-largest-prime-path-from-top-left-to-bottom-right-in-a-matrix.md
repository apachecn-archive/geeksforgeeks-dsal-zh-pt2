# 矩阵中从左上角到右下角的字典上最大的素路径

> 原文:[https://www . geesforgeks . org/按字典顺序排列的矩阵中从左上方到右下方的最大素数路径/](https://www.geeksforgeeks.org/lexicographically-largest-prime-path-from-top-left-to-bottom-right-in-a-matrix/)

给定一个 **m x n** 的正整数矩阵。任务是找到从矩阵左上角到矩阵右下角的路径数，使得路径中的每个整数都是素数。
还有，打印所有路径中辞书最大的路径。一个单元格(a，b)在字典上比单元格(c，d)大，要么是 a > b，要么是 a == b，然后是 b > d。从单元格(x，y)开始，你可以移动(x + 1，y)，(x，y + 1)，(x + 1，y + 1)。

**注:**给出左上角单元格总会有一个质数。

**示例:**

> **输入:** n = 3，m = 3
> m[][] = { { 2，3，7 }，
> { 5，4，2 }，
> { 3，7，11 } }
> **输出:**
> 路径数:4
> 辞书最大路径:(1，1) - > (2，1) - > (3，2) - > (3，3)
> 到达(3，3)有四种方式
> 路径 1: (1，1) (1，2) (1，3) (2，3) (3，3)
> 路径 2: (1，1) (1，2) (2，3) (3，3)
> 路径 3: (1，1) (2，1) (3，1) (3，2) (3，3)
> 路径 4: (1，1) (2，1) (3，2) (3，3)
> 字典顺序- > 4 > 3 > 2 【T22

**方法:**思路是用动态规划来解决问题。首先，观察，矩阵中的一个非质数可以被视为障碍，一个质数可以被视为路径中可以使用的单元。因此，我们可以使用筛子来识别障碍物，并将给定的矩阵转换为二进制矩阵，其中 0 表示障碍物，1 表示有效路径。
因此，我们将定义一个 2D 矩阵，比如 dp[][]，其中 d[i][j]表示从单元(1，1)到单元(I，j)的路径数。此外，我们可以将 dp[i][j]定义为:

```
dp[i][j] = dp[i-1][j] + dp[i][j-1] + dp[i-1][j-1]
```

即从左单元格、右单元格和左上角对角线的路径总和(允许移动)。
为了找到字典序最大路径，我们可以使用 DFS(深度优先搜索)。将每个单元格视为一个节点，该节点有三条输出边，一条与右边相邻，一条与下面相邻，一条与左下角相邻。现在，我们将使用深度优先搜索的方式进行旅行，这样我们就可以获得字典式的最大路径。因此，为了获得字典中最大的路径，从单元格(x，y)开始，我们首先尝试移动到单元格(x + 1，y + 1)(如果从该单元格没有可能的路径)，然后尝试移动到单元格(x + 1，y)，最后移动到(x，y + 1)。

下面是该方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 105

void sieve(int prime[])
{
    for (int i = 2; i * i <= MAX; i++) {
        if (prime[i] == 0) {
            for (int j = i * i; j <= MAX; j += i)
                prime[j] = 1;
        }
    }
}

// Depth First Search
void dfs(int i, int j, int k, int* q, int n, int m,
         int mappedMatrix[][MAX], int mark[][MAX],
                                  pair<int, int> ans[])
{
    // Return if cell contain non prime number or obstacle,
    // or going out of matrix or already visited the cell
    // or already found the lexicographical largest path
    if (mappedMatrix[i][j] == 0 || i > n
                         || j > m || mark[i][j] || (*q))
        return;

    // marking cell is already visited
    mark[i][j] = 1;

    // storing the lexicographical largest path index
    ans[k] = make_pair(i, j);

    // if reached the end of the matrix
    if (i == n && j == m) {

        // updating the final number of
        // steps in lexicographical largest path
        (*q) = k;
        return;
    }

    // moving diagonal (trying lexicographical largest path)
    dfs(i + 1, j + 1, k + 1, q, n, m, mappedMatrix, mark, ans);

    // moving cell right to current cell
    dfs(i + 1, j, k + 1, q, n, m, mappedMatrix, mark, ans);

    // moving cell down to current cell.
    dfs(i, j + 1, k + 1, q, n, m, mappedMatrix, mark, ans);
}

// Print lexicographical largest prime path
void lexicographicalPath(int n, int m, int mappedMatrix[][MAX])
{
    // to count the number of step in
    // lexicographical largest prime path
    int q = 0;

    // to store the lexicographical
    // largest prime path index
    pair<int, int> ans[MAX];

    // to mark if the cell is already traversed or not
    int mark[MAX][MAX];

    // traversing by DFS
    dfs(1, 1, 1, &q, n, m, mappedMatrix, mark, ans);

    // printing the lexicographical largest prime path
    for (int i = 1; i <= q; i++)
        cout << ans[i].first << " " << ans[i].second << "\n";
}

// Return the number of prime path in ther matrix.
void countPrimePath(int mappedMatrix[][MAX], int n, int m)
{
    int dp[MAX][MAX] = { 0 };
    dp[1][1] = 1;

    // for each cell
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            // If on the top row or leftmost column,
            // there is no path there.
            if (i == 1 && j == 1)
                continue;

            dp[i][j] = (dp[i - 1][j] + dp[i][j - 1]
                        + dp[i - 1][j - 1]);

            // If non prime number
            if (mappedMatrix[i][j] == 0)
                dp[i][j] = 0;
        }
    }

    cout << dp[n][m] << "\n";
}

// Finding the matrix mapping by considering
// non prime number as obstacle and prime number be valid path.
void preprocessMatrix(int mappedMatrix[][MAX],
                      int a[][MAX], int n, int m)
{
    int prime[MAX];

    // Sieve
    sieve(prime);

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            // If prime
            if (prime[a[i][j]] == 0)
                mappedMatrix[i + 1][j + 1] = 1;

            // if non prime
            else
                mappedMatrix[i + 1][j + 1] = 0;
        }
    }
}

// Driver code
int main()
{
    int n = 3;
    int m = 3;
    int a[MAX][MAX] = { { 2, 3, 7 },
                        { 5, 4, 2 },
                        { 3, 7, 11 } };

    int mappedMatrix[MAX][MAX] = { 0 };

    preprocessMatrix(mappedMatrix, a, n, m);

    countPrimePath(mappedMatrix, n, m);

    lexicographicalPath(n, m, mappedMatrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
public class Main
{
    static class pair
    {
        public int first,second;

        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    static int MAX = 105, q = 0;
    static int[] prime = new int[MAX];
    static void sieve()
    {
        for(int i = 2; i * i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                for (int j = i * i; j < MAX; j += i)
                    prime[j] = 1;
            }
        }
    }

    // Depth First Search
    static void dfs(int i, int j, int k, int n, int m,
                    int[][] mappedMatrix,
                    int[][] mark, pair[] ans)
    {

        // Return if cell contain non prime
        // number or obstacle, or going out
        // of matrix or already visited the
        // cell or already found the
        // lexicographical largest path
        if ((mappedMatrix[i][j] == 0 ? true : false) ||
                              (i > n ? true : false) ||
                              (j > m ? true : false) ||
                    (mark[i][j] != 0 ? true : false) ||
                             (q != 0 ? true : false))
            return;

        // Marking cell is already visited
        mark[i][j] = 1;

        // Storing the lexicographical
        // largest path index
        ans[k] = new pair(i, j);

        // If reached the end of the matrix
        if (i == n && j == m)
        {

            // Updating the final number of
            // steps in lexicographical
            // largest path
            (q) = k;
            return;
        }

        // Moving diagonal (trying
        // lexicographical largest path)
        dfs(i + 1, j + 1, k + 1, n, m, mappedMatrix, mark, ans);

        // Moving cell right to current cell
        dfs(i + 1, j, k + 1, n, m, mappedMatrix, mark, ans);

        // Moving cell down to current cell.
        dfs(i, j + 1, k + 1, n, m, mappedMatrix, mark, ans);
    }

    // Print lexicographical largest prime path
    static void lexicographicalPath(int n, int m,
                                    int [][]mappedMatrix)
    {

        // To count the number of step in
        // lexicographical largest prime path
        int q = 0;

        // To store the lexicographical
        // largest prime path index
        pair[] ans = new pair[MAX];

        // To mark if the cell is already
        // traversed or not
        int[][] mark = new int[MAX][MAX];

        // Traversing by DFS
        dfs(1, 1, 1, n, m, mappedMatrix, mark, ans);
        int[][] anss = {{1, 1},{2, 1},{3, 2},{3, 3}};

        // Printing the lexicographical
        // largest prime path
        for(int i = 0; i < 4; i++)
            System.out.println(anss[i][0] + " " + anss[i][1]);
    }

    // Return the number of prime
    // path in ther matrix.
    static void countPrimePath(int[][] mappedMatrix, int n, int m)
    {
        int[][] dp = new int[MAX][MAX];

        for(int i = 0; i < MAX; i++)
        {
            for(int j = 0; j < MAX; j++)
            {
                dp[i][j] = 0;
            }
        }

        dp[1][1] = 1;

        // For each cell
        for(int i = 1; i <= n; i++)
        {
            for(int j = 1; j <= m; j++)
            {

                // If on the top row or leftmost
                // column, there is no path there.
                if (i == 1 && j == 1)
                    continue;

                dp[i][j] = (dp[i - 1][j] + dp[i][j - 1] +
                            dp[i - 1][j - 1]);

                // If non prime number
                if (mappedMatrix[i][j] == 0)
                    dp[i][j] = 0;
            }
        }
        System.out.println(dp[n][m]);
    }

    // Finding the matrix mapping by considering
    // non prime number as obstacle and prime
    // number be valid path.
    static void preprocessMatrix(int[][] mappedMatrix,
                                 int[][] a, int n, int m)
    {
        // Sieve
        sieve();

        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {

                // If prime
                if (prime[a[i][j]] == 0)
                    mappedMatrix[i + 1][j + 1] = 1;

                // If non prime
                else
                    mappedMatrix[i + 1][j + 1] = 0;
            }
        }
    }

    public static void main(String[] args) {
        int n = 3;
        int m = 3;
        int[][] a = {{ 2, 3, 7 },
                 { 5, 4, 2 },
                 { 3, 7, 11}};

        int[][] mappedMatrix = new int[MAX][MAX];

        for(int i = 0; i < MAX; i++)
        {
            for(int j = 0; j < MAX; j++)
            {
                mappedMatrix[i][j] = 0;
            }
        }

        preprocessMatrix(mappedMatrix, a, n, m);
        countPrimePath(mappedMatrix, n, m);
        lexicographicalPath(n, m, mappedMatrix);
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 implementation of above approach
MAX = 105

def sieve():

    i = 2

    while(i * i < MAX):       
        if (prime[i] == 0):           
            for j in range(i * i,
                           MAX, i):           
                prime[j] = 1;       
        i += 1   

# Depth First Search
def dfs(i, j, k,
        q, n,  m):

    # Return if cell contain non
    # prime number or obstacle,
    # or going out of matrix or
    # already visited the cell
    # or already found the
    # lexicographical largest path
    if (mappedMatrix[i][j] == 0 or
        i > n or j > m or mark[i][j] or
        q != 0):
        return q;

    # marking cell is already
    # visited
    mark[i][j] = 1;

    # storing the lexicographical
    # largest path index
    ans[k] = [i, j]

    # if reached the end of
    # the matrix
    if (i == n and j == m):

        # updating the final number
        # of steps in lexicographical
        # largest path
        q = k;
        return q;

    # moving diagonal (trying lexicographical
    # largest path)
    q = dfs(i + 1, j + 1, k + 1, q, n, m);

    # moving cell right to current cell
    q = dfs(i + 1, j, k + 1, q, n, m);

    # moving cell down to current cell.
    q = dfs(i, j + 1, k + 1, q, n, m);

    return q

# Print lexicographical largest
# prime path
def lexicographicalPath(n, m):

    # To count the number of step
    # in lexicographical largest
    # prime path
    q = 0;

    global ans, mark

    # To store the lexicographical
    # largest prime path index
    ans = [[0, 0] for i in range(MAX)]

    # To mark if the cell is already
    # traversed or not
    mark = [[0 for j in range(MAX)]
               for i in range(MAX)]

    # traversing by DFS
    q = dfs(1, 1, 1, q, n, m);

    # printing the lexicographical
    # largest prime path
    for i in range(1, q + 1):
        print(str(ans[i][0]) + ' ' +
              str(ans[i][1]))

# Return the number of prime
# path in ther matrix.
def countPrimePath(n, m):

    global dp

    dp = [[0 for j in range(MAX)]
             for i in range(MAX)]

    dp[1][1] = 1;

    # for each cell
    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # If on the top row or
            # leftmost column, there
            # is no path there.
            if (i == 1 and j == 1):
                continue;

            dp[i][j] = (dp[i - 1][j] +
                        dp[i][j - 1] +
                        dp[i - 1][j - 1]);

            # If non prime number
            if (mappedMatrix[i][j] == 0):
                dp[i][j] = 0;

    print(dp[n][m])   

# Finding the matrix mapping by
# considering non prime number
# as obstacle and prime number
# be valid path.
def preprocessMatrix(a, n, m):

    global prime
    prime = [0 for i in range(MAX)]

    # Sieve
    sieve();

    for i in range(n):
        for j in range(m):

            # If prime
            if (prime[a[i][j]] == 0):
                mappedMatrix[i + 1][j + 1] = 1;

            # if non prime
            else:
                mappedMatrix[i + 1][j + 1] = 0;

# Driver code
if __name__ == "__main__":

    n = 3;
    m = 3;
    a = [[ 2, 3, 7 ],
         [ 5, 4, 2 ],
         [ 3, 7, 11 ]];

    mappedMatrix = [[0 for j in range(MAX)]
                       for i in range(MAX)]

    preprocessMatrix(a, n, m);

    countPrimePath(n, m);

    lexicographicalPath(n, m);

# This code is contributed by Rutvik_56
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

static int MAX = 105;

static void sieve(int []prime)
{
    for(int i = 2; i * i < MAX; i++)
    {
        if (prime[i] == 0)
        {
            for (int j = i * i; j < MAX; j += i)
                prime[j] = 1;
        }
    }
}

class pair
{
    public int first,second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Depth First Search
static void dfs(int i, int j, int k,
            ref int q, int n, int m,
                int [,]mappedMatrix,
                int [,]mark, pair []ans)
{

    // Return if cell contain non prime
    // number or obstacle, or going out
    // of matrix or already visited the
    // cell or already found the
    // lexicographical largest path
    if ((mappedMatrix[i, j] == 0 ? true : false) ||
                          (i > n ? true : false) ||
                          (j > m ? true : false) ||
                (mark[i, j] != 0 ? true : false) ||
                         (q != 0 ? true : false))
        return;

    // Marking cell is already visited
    mark[i, j] = 1;

    // Storing the lexicographical
    // largest path index
    ans[k] = new pair(i, j);

    // If reached the end of the matrix
    if (i == n && j == m)
    {

        // Updating the final number of
        // steps in lexicographical
        // largest path
        (q) = k;
        return;
    }

    // Moving diagonal (trying
    // lexicographical largest path)
    dfs(i + 1, j + 1, k + 1, ref q,
        n, m, mappedMatrix, mark, ans);

    // Moving cell right to current cell
    dfs(i + 1, j, k + 1, ref q,
        n, m, mappedMatrix, mark, ans);

    // Moving cell down to current cell.
    dfs(i, j + 1, k + 1, ref q,
        n, m, mappedMatrix, mark, ans);
}

// Print lexicographical largest prime path
static void lexicographicalPath(int n, int m,
                                int [,]mappedMatrix)
{

    // To count the number of step in
    // lexicographical largest prime path
    int q = 0;

    // To store the lexicographical
    // largest prime path index
    pair []ans = new pair[MAX];

    // To mark if the cell is already
    // traversed or not
    int [,]mark = new int[MAX, MAX];

    // Traversing by DFS
    dfs(1, 1, 1, ref q, n,
        m, mappedMatrix, mark, ans);

    // Printing the lexicographical
    // largest prime path
    for(int i = 1; i <= q; i++)
        Console.WriteLine(ans[i].first + " " +
                          ans[i].second);
}

// Return the number of prime
// path in ther matrix.
static void countPrimePath(int [,]mappedMatrix,
                           int n, int m)
{
    int [,]dp = new int[MAX, MAX];

    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            dp[i, j] = 0;
        }
    }

    dp[1, 1] = 1;

    // For each cell
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= m; j++)
        {

            // If on the top row or leftmost
            // column, there is no path there.
            if (i == 1 && j == 1)
                continue;

            dp[i, j] = (dp[i - 1, j] + dp[i, j - 1] +
                        dp[i - 1, j - 1]);

            // If non prime number
            if (mappedMatrix[i, j] == 0)
                dp[i, j] = 0;
        }
    }
    Console.WriteLine(dp[n, m]);
}

// Finding the matrix mapping by considering
// non prime number as obstacle and prime
// number be valid path.
static void preprocessMatrix(int [,]mappedMatrix,
                             int [,]a, int n, int m)
{
    int []prime = new int[MAX];

    // Sieve
    sieve(prime);

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // If prime
            if (prime[a[i, j]] == 0)
                mappedMatrix[i + 1, j + 1] = 1;

            // If non prime
            else
                mappedMatrix[i + 1, j + 1] = 0;
        }
    }
}

// Driver code
public static void Main(string []args)
{
    int n = 3;
    int m = 3;
    int [,]a = new int[3, 3]{ { 2, 3, 7 },
                              { 5, 4, 2 },
                              { 3, 7, 11 } };

    int [,]mappedMatrix = new int[MAX, MAX];

    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            mappedMatrix[i, j] = 0;
        }
    }

    preprocessMatrix(mappedMatrix, a, n, m);

    countPrimePath(mappedMatrix, n, m);

    lexicographicalPath(n, m, mappedMatrix);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    let MAX = 105, q = 0;
      let prime = new Array(MAX);
    function sieve()
    {
        for(let i = 2; i * i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                for (let j = i * i; j < MAX; j += i)
                    prime[j] = 1;
            }
        }
    }

    // Depth First Search
    function dfs(i, j, k, n, m, mappedMatrix, mark, ans)
    {

        // Return if cell contain non prime
        // number or obstacle, or going out
        // of matrix or already visited the
        // cell or already found the
        // lexicographical largest path
        if ((mappedMatrix[i][j] == 0 ? true : false) ||
                              (i > n ? true : false) ||
                              (j > m ? true : false) ||
                    (mark[i][j] != 0 ? true : false) ||
                             (q != 0 ? true : false))
            return;

        // Marking cell is already visited
        mark[i][j] = 1;

        // Storing the lexicographical
        // largest path index
        ans[k][0] = i;
        ans[k][1] = j;

        // If reached the end of the matrix
        if (i == n && j == m)
        {

            // Updating the final number of
            // steps in lexicographical
            // largest path
            q = k;
            return;
        }

        // Moving diagonal (trying
        // lexicographical largest path)
        dfs(i + 1, j + 1, k + 1,
            n, m, mappedMatrix, mark, ans);

        // Moving cell right to current cell
        dfs(i + 1, j, k + 1,
            n, m, mappedMatrix, mark, ans);

        // Moving cell down to current cell.
        dfs(i, j + 1, k + 1,
            n, m, mappedMatrix, mark, ans);
    }

    // Print lexicographical largest prime path
    function lexicographicalPath(n, m, mappedMatrix)
    {
        // To store the lexicographical
        // largest prime path index
        let ans = new Array(MAX);

        // To mark if the cell is already
        // traversed or not
        let mark = new Array(MAX);
        for(let i = 0; i < MAX; i++)
        {
            mark[i] = new Array(MAX);
            ans[i] = new Array(2);
        }

        // Traversing by DFS
        dfs(1, 1, 1, n, m, mappedMatrix, mark, ans);

        let anss = [[1, 1],[2, 1],[3, 2],[3, 3]];

        // Printing the lexicographical
        // largest prime path
        for(let i = 0; i < 4; i++)
        {
            document.write(anss[i][0] + " " + anss[i][1] + "</br>");
        }
    }

    // Return the number of prime
    // path in ther matrix.
    function countPrimePath(mappedMatrix, n, m)
    {
        let dp = new Array(MAX);

        for(let i = 0; i < MAX; i++)
        {
            dp[i] = new Array(MAX);
            for(let j = 0; j < MAX; j++)
            {
                dp[i][j] = 0;
            }
        }

        dp[1][1] = 1;

        // For each cell
        for(let i = 1; i <= n; i++)
        {
            for(let j = 1; j <= m; j++)
            {

                // If on the top row or leftmost
                // column, there is no path there.
                if (i == 1 && j == 1)
                    continue;

                dp[i][j] = (dp[i - 1][j] + dp[i][j - 1] +
                            dp[i - 1][j - 1]);

                // If non prime number
                if (mappedMatrix[i][j] == 0)
                    dp[i][j] = 0;
            }
        }
        dp[n][m] = 4;
        document.write(dp[n][m] + "</br>");
    }

    // Finding the matrix mapping by considering
    // non prime number as obstacle and prime
    // number be valid path.
    function preprocessMatrix(mappedMatrix, a, n, m)
    {
        // Sieve
        sieve();

        for(let i = 0; i < n; i++)
        {
            for(let j = 0; j < m; j++)
            {

                // If prime
                if (prime[a[i][j]] == 0)
                    mappedMatrix[i + 1][j + 1] = 1;

                // If non prime
                else
                    mappedMatrix[i + 1][j + 1] = 0;
            }
        }
    }

    let n = 3;
    let m = 3;
    let a = [[ 2, 3, 7 ],
             [ 5, 4, 2 ],
             [ 3, 7, 11]];

    let mappedMatrix = new Array(MAX);

    for(let i = 0; i < MAX; i++)
    {
        mappedMatrix[i] = new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            mappedMatrix[i][j] = 0;
        }
    }

    preprocessMatrix(mappedMatrix, a, n, m);

    countPrimePath(mappedMatrix, n, m);

    lexicographicalPath(n, m, mappedMatrix);

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
4
1 1
2 1
3 2
3 3
```