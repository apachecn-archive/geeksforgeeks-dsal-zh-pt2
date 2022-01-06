# 给定条件下遍历整个矩阵的最小初始顶点

> 原文:[https://www . geesforgeks . org/最小值-初始-顶点-遍历-整矩阵-给定-条件/](https://www.geeksforgeeks.org/minimum-initial-vertices-traverse-whole-matrix-given-conditions/)

给我们一个矩阵，每个单元格包含不同的值。我们的目标是找到矩阵中位置的最小集合，使得整个矩阵可以从集合中的位置开始遍历。
我们可以在以下条件下遍历矩阵:

*   我们只能移动到那些值小于或等于当前单元格值的邻居。小区的邻居被定义为与给定小区共享一侧的小区。

**示例:**

```
Input : 1 2 3
        2 3 1
        1 1 1
Output : 1 1
         0 2
If we start from 1, 1 we can cover 6 
vertices in the order (1, 1) -> (1, 0) -> (2, 0) 
-> (2, 1) -> (2, 2) -> (1, 2). We cannot cover
the entire matrix with this vertex. Remaining 
vertices can be covered (0, 2) -> (0, 1) -> (0, 0). 

Input : 3 3
        1 1
Output : 0 1
If we start from 0, 1, we can traverse 
the entire matrix from this single vertex 
in this order (0, 0) -> (0, 1) -> (1, 1) -> (1, 0). 
Traversing the matrix in this order 
satisfies all the conditions stated above.
```

从上面的例子中，我们可以很容易地识别出，为了使用最小数量的位置，我们必须从具有最高单元格值的位置开始。因此，我们选择矩阵中包含最高值的位置。我们在一个单独的数组中取具有最高值的顶点。我们在从
最高值开始的每个顶点执行[离散傅立叶变换](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。如果我们在 dfs 期间遇到任何未访问的顶点，那么我们必须将这个顶点包含在我们的集合中。当所有的单元都被处理后，集合就包含了需要的顶点。

**这是如何工作的？**
我们需要访问所有顶点，要达到最大值，我们必须从它们开始。如果两个最大值不相邻，则必须选择两个最大值。如果两个最大值是相邻的，那么它们中的任何一个都可以被拾取，因为允许移动到相等值的相邻值。

## C++

```
// C++ program to find minimum initial
// vertices to reach whole matrix.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// (n, m) is current source cell from which
// we need to do DFS. N and M are total no.
// of rows and columns.
void dfs(int n, int m, bool visit[][MAX],
         int adj[][MAX], int N, int M)
{
    // Marking the vertex as visited
    visit[n][m] = 1;

    // If below neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (n + 1 < N &&
        adj[n][m] >= adj[n + 1][m] &&
        !visit[n + 1][m])
        dfs(n + 1, m, visit, adj, N, M);

    // If right neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (m + 1 < M &&
        adj[n][m] >= adj[n][m + 1] &&
        !visit[n][m + 1])
        dfs(n, m + 1, visit, adj, N, M);

    // If above neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (n - 1 >= 0 &&
        adj[n][m] >= adj[n - 1][m] &&
        !visit[n - 1][m])
        dfs(n - 1, m, visit, adj, N, M);

    // If left neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (m - 1 >= 0 &&
        adj[n][m] >= adj[n][m - 1] &&
        !visit[n][m - 1])
        dfs(n, m - 1, visit, adj, N, M);
}

void printMinSources(int adj[][MAX], int N, int M)
{
    // Storing the cell value and cell indices
    // in a vector.
    vector<pair<long int, pair<int, int> > > x;
    for (int i = 0; i < N; i++)
        for (int j = 0; j < M; j++)
            x.push_back(make_pair(adj[i][j],
                        make_pair(i, j)));

    // Sorting the newly created array according
    // to cell values
    sort(x.begin(), x.end());

    // Create a visited array for DFS and
    // initialize it as false.
    bool visit[N][MAX];
    memset(visit, false, sizeof(visit));

    // Applying dfs for each vertex with
    // highest value
    for (int i = x.size()-1; i >=0 ; i--)
    {
        // If the given vertex is not visited
        // then include it in the set
        if (!visit[x[i].second.first][x[i].second.second])
        {
            cout << x[i].second.first << " "
                 << x[i].second.second << endl;
            dfs(x[i].second.first, x[i].second.second,
               visit, adj, N, M);
        }
    }
}

// Driver code
int main()
{
    int N = 2, M = 2;

    int adj[N][MAX] = {{3, 3},
                       {1, 1}};
    printMinSources(adj, N, M);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find minimum initial
# vertices to reach whole matrix
MAX = 100

# (n, m) is current source cell from which
# we need to do DFS. N and M are total no.
# of rows and columns.
def dfs(n, m, visit, adj, N, M):

    # Marking the vertex as visited
    visit[n][m] = 1

    # If below neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (n + 1 < N and
        adj[n][m] >= adj[n + 1][m] and
        not visit[n + 1][m]):
        dfs(n + 1, m, visit, adj, N, M)

    # If right neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (m + 1 < M and
        adj[n][m] >= adj[n][m + 1] and
        not visit[n][m + 1]):
        dfs(n, m + 1, visit, adj, N, M)

    # If above neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (n - 1 >= 0 and
        adj[n][m] >= adj[n - 1][m] and
        not visit[n - 1][m]):
        dfs(n - 1, m, visit, adj, N, M)

    # If left neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (m - 1 >= 0 and
        adj[n][m] >= adj[n][m - 1] and
        not visit[n][m - 1]):
        dfs(n, m - 1, visit, adj, N, M)

def printMinSources(adj, N, M):

    # Storing the cell value and cell
    # indices in a vector.
    x = []

    for i in range(N):
        for j in range(M):
            x.append([adj[i][j], [i, j]])

    # Sorting the newly created array according
    # to cell values
    x.sort()

    # Create a visited array for DFS and
    # initialize it as false.
    visit = [[False for i in range(MAX)]
                    for i in range(N)]

    # Applying dfs for each vertex with
    # highest value
    for i in range(len(x) - 1, -1, -1):

        # If the given vertex is not visited
        # then include it in the set
        if (not visit[x[i][1][0]][x[i][1][1]]):
            print('{} {}'.format(x[i][1][0],
                                 x[i][1][1]))

            dfs(x[i][1][0],
                x[i][1][1],
                visit, adj, N, M)

# Driver code
if __name__=='__main__':

    N = 2
    M = 2

    adj = [ [ 3, 3 ], [ 1, 1 ] ]

    printMinSources(adj, N, M)

# This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to find minimum initial
// vertices to reach whole matrix.

var MAX = 100;

// (n, m) is current source cell from which
// we need to do DFS. N and M are total no.
// of rows and columns.
function dfs( n,  m,  visit, adj, N, M)
{
    // Marking the vertex as visited
    visit[n][m] = 1;

    // If below neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (n + 1 < N &&
        adj[n][m] >= adj[n + 1][m] &&
        !visit[n + 1][m])
        dfs(n + 1, m, visit, adj, N, M);

    // If right neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (m + 1 < M &&
        adj[n][m] >= adj[n][m + 1] &&
        !visit[n][m + 1])
        dfs(n, m + 1, visit, adj, N, M);

    // If above neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (n - 1 >= 0 &&
        adj[n][m] >= adj[n - 1][m] &&
        !visit[n - 1][m])
        dfs(n - 1, m, visit, adj, N, M);

    // If left neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (m - 1 >= 0 &&
        adj[n][m] >= adj[n][m - 1] &&
        !visit[n][m - 1])
        dfs(n, m - 1, visit, adj, N, M);
}

function printMinSources( adj,  N,  M)
{
    // Storing the cell value and cell indices
    // in a vector.
    var x = [];
    for (var i = 0; i < N; i++)
        for (var j = 0; j < M; j++)
            x.push([adj[i][j],[i, j]]);

    // Sorting the newly created array according
    // to cell values
    x = x.sort();

    // Create a visited array for DFS and
    // initialize it as false.
    var visit = new Array(N);
    for (var i = 0; i < N; i++) {
        visit[i] = [];
        for (var j = 0; j < MAX; j++) {
            visit[i].push(false);
        }
    }

    // Applying dfs for each vertex with
    // highest value
    for (var i = x.length-1; i >=0 ; i--)
    {
        // If the given vertex is not visited
        // then include it in the set
        if (!visit[x[i][1][0]][x[i][1][1]])
        {
            document.write(x[i][1][0] + " "
                 + x[i][1][1] + "<br>");
            dfs(x[i][1][0], x[i][1][1],
               visit, adj, N, M);
        }
    }
}

// driver code
var N = 2
var M = 2

var adj = [ [ 3, 3 ], [ 1, 1 ] ]

printMinSources(adj, N, M)
// This code contributed by shivani
</script>
```

**输出:**

```
0 1
```