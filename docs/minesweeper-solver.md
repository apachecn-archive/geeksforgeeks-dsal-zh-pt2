# 扫雷艇解算器

> 原文:[https://www.geeksforgeeks.org/minesweeper-solver/](https://www.geeksforgeeks.org/minesweeper-solver/)

给定一个维度为 **N*M** 的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**arr【】【】【】**，代表一个[扫雷舰](https://www.geeksforgeeks.org/cpp-implementation-minesweeper-game/)矩阵，其中每个像元包含一个范围为**【0，9】**的整数，代表其自身以及与其相邻的所有八个像元的地雷数量，任务是解决扫雷舰并揭开矩阵中的所有地雷。打印含有地雷的单元格的**‘X’**，打印所有其他空单元格的**“_”**。如果无法解决扫雷艇，则打印**-1”**。

**示例:**

> **输入:**
> arr[][] = {{1，1，0，0，1，1}，
> {2，3，2，1，1，2，2}，
> {3，5，3，2，1，2，2}，
> {3，6，5，3，0，2，2}，
> {2，4，3，2，0，1}，
> {2，3，3，2，2 }
> **输出:**
> _ _ _ _
> x _ _ _ _ _ x _
> _ x _ _ _×x
> x _ x _ _ _ _
> _ x _ _ _×x
> _ _ _ _
> _ x _ _ x _ _
> 
> **输入:**
> arr[][] = {{0，0，0，0，0，0}，
> {0，0，0，0，1，1}，
> {0，0，0，0，1，1}，
> {0，0，1，1，1，1，1，1，1，1}，
> {0，0，2，2，0，0}，
> {0，0，2，2，2，0，0} 0}}
> **输出:**
> _ _ _ _
> _ _ _ _
> _ _ _ x
> _ _ _ _
> _ _ _ x _ _
> _ _ _ x _ _
> _ _ _ _

**<u>输入生成</u> :** 要求解给定的[扫雷舰矩阵](https://www.geeksforgeeks.org/cpp-implementation-minesweeper-game/) **arr[][]** ，它必须是有效的输入，即扫雷舰矩阵必须是可解的。因此，输入矩阵是在 **generateMineField()** 函数中生成的。按照以下步骤生成输入扫雷矩阵:

*   生成输入的输入是雷场的大小 **N** 和 **M** 以及雷场的概率 **P** (或密度)。
*   如果雷区内没有地雷，概率 **P** 等于 **0** ，如果雷区内所有细胞都是地雷，概率 **P** 等于 **100** 。
*   为每个单元选择一个[随机数](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)，如果该随机数小于 **P** ，则将一个地雷分配给网格，并生成一个布尔数组**地雷[][]** 。
*   约束求解器的输入是每个网格的状态，该网格计算其自身的地雷及其周围的八个单元。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the number of rows
// and columns of the matrix
int N, M;

// Stores the final generated input
int arr[100][100];

// Direction arrays
int dx[9] = { -1, 0, 1, -1, 0, 1, -1, 0, 1 };
int dy[9] = { 0, 0, 0, -1, -1, -1, 1, 1, 1 };

// Function to check if the
// cell location is valid
bool isValid(int x, int y)
{
    // Returns true if valid
    return (x >= 0 && y >= 0
            && x < N && y < M);
}

// Function to generate a valid minesweeper
// matrix of size ROW * COL with P being
// the probability of a cell being a mine
void generateMineField(int ROW, int COL, int P)
{
    // Generates the random
    // number every time
    srand(time(NULL));

    int rand_val;

    // Stores whether a cell
    // contains a mine or not
    int mines[ROW][COL];

    // Iterate through each cell
    // of the matrix mine
    for (int x = 0; x < ROW; x++) {
        for (int y = 0; y < COL; y++) {
            // Generate a random value
            // from the range [0, 100]
            rand_val = rand() % 100;

            // If rand_val is less than P
            if (rand_val < P)

                // MArk mines[x][y] as True
                mines[x][y] = true;

            // Otherwise, mark
            // mines[x][y] as False
            else
                mines[x][y] = false;
        }
    }

    cout << "Generated Input:\n";

    // Iterate through each cell (x, y)
    for (int x = 0; x < ROW; x++) {
        for (int y = 0; y < COL; y++) {
            arr[x][y] = 0;

            // Count the number of mines
            // around the cell (x, y)
            // and store in arr[x][y]
            for (int k = 0; k < 9; k++) {
                // If current adjacent cell is valid
                if (isValid(x + dx[k], y + dy[k])
                    && (mines[x + dx[k]][y + dy[k]]))
                    arr[x][y]++;
            }

            // Print the value at
            // the current cell
            cout << arr[x][y] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    N = 7, M = 7;
    int P = 20;

    // Function call to generate
    // a valid minesweeper matrix
    generateMineField(N, M, 15);
}
```

**Output:** 

```
Generated Input:
0 1 1 1 1 1 1 
1 3 3 3 2 2 1 
1 2 2 2 2 2 1 
1 2 2 2 1 1 0 
1 2 1 1 1 1 1 
1 3 2 2 1 1 1 
1 3 2 2 1 1 1
```

**方法:**给定的问题可以使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。这个想法是[迭代一个矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)的每个单元，基于从相邻单元获得的信息，分配一个**地雷**给那个单元。

按照以下步骤解决给定的问题:

*   初始化一个矩阵，比如**网格[][]** ，**访问了[][]** ，以存储结果网格，并在遍历网格时跟踪访问的单元格。将所有网格值初始化为**假**。
*   声明一个递归函数 **solveMineSweeper()** 来接受数组**arr【】【】**、**grid【】【】**、**visited【】【】**作为参数。
    *   如果所有的单元都被访问，并且一个矿被分配给满足给定输入**网格[][]** 的单元，那么对于当前递归调用返回**真**。
    *   如果访问了所有单元格，但解决方案不满足输入**网格[]** ，则为当前递归调用返回**假**。
    *   如果发现以上两个条件**为假，**则找到一个未访问的单元格 **(x，y)** 并将 **(x，y)** 标记为已访问。
    *   如果一个**地雷**可以被分配到 **(x，y)** 位置，那么执行以下步骤:
        *   将**网格【x】【y】**标记为**真**。
        *   通过 **1** 减少矩阵**arr【】【】**中 **(x，y)** 相邻单元格的地雷数量。
        *   [递归调用](https://www.geeksforgeeks.org/recursive-functions/)获得**solveminesweaver()**，其中 **(x，y)** 有一个地雷，如果它返回 **true** ，则存在一个解。当前递归调用返回**真**。
        *   否则，重置 **(x，y)** 位置，即将**网格【x】【y】**标记为**假**，将矩阵**arr【】【】**中 **(x，y)** 相邻单元的地雷数增加 **1** 。
    *   如果函数**solvemineswaver()****(x，y)** 没有地雷，返回 **true** ，则表示有解存在。从当前递归调用返回**真**。
    *   如果上一步的递归调用返回 **false，**表示解不存在。因此，从当前递归调用中返回 **false** 。
*   如果函数**solvemineswaver(网格、arr、已访问)**返回的值为**真**，则存在一个解。打印矩阵**网格【】【】**作为所需的解决方案。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the number of rows
// and columns in given matrix
int N, M;

// Maximum number of rows
// and columns possible
#define MAXM 100
#define MAXN 100

// Directional Arrays
int dx[9] = { -1, 0, 1, -1, 0, 1, -1, 0, 1 };
int dy[9] = { 0, 0, 0, -1, -1, -1, 1, 1, 1 };

// Function to check if the
// cell (x, y) is valid or not
bool isValid(int x, int y)
{
    return (x >= 0 && y >= 0
            && x < N && y < M);
}

// Function to print the matrix grid[][]
void printGrid(bool grid[MAXN][MAXM])
{
    for (int row = 0; row < N; row++) {
        for (int col = 0; col < M; col++) {
            if (grid[row][col])
                cout << "x ";
            else
                cout << "_ ";
        }
        cout << endl;
    }
}

// Function to check if the cell (x, y)
// is valid to have a mine or not
bool isSafe(int arr[MAXN][MAXM], int x, int y)
{

    // Check if the cell (x, y) is a
    // valid cell or not
    if (!isValid(x, y))
        return false;

    // Check if any of the neighbouring cell
    // of (x, y) supports (x, y) to have a mine
    for (int i = 0; i < 9; i++) {

        if (isValid(x + dx[i], y + dy[i])
            && (arr[x + dx[i]][y + dy[i]] - 1 < 0))
            return (false);
    }

    // If (x, y) is valid to have a mine
    for (int i = 0; i < 9; i++) {
        if (isValid(x + dx[i], y + dy[i]))

            // Reduce count of mines in
            // the neighboring cells
            arr[x + dx[i]][y + dy[i]]--;
    }

    return true;
}

// Function to check if there
// exists any unvisited cell or not
bool findUnvisited(bool visited[MAXN][MAXM],
                   int& x, int& y)
{
    for (x = 0; x < N; x++)
        for (y = 0; y < M; y++)
            if (!visited[x][y])
                return (true);
    return (false);
}

// Function to check if all the cells
// are visited or not and the input array
// is satisfied with the mine assignments
bool isDone(int arr[MAXN][MAXM],
            bool visited[MAXN][MAXM])
{
    bool done = true;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            done
                = done && (arr[i][j] == 0)
                  && visited[i][j];
        }
    }

    return (done);
}

// Function to solve the minesweeper matrix
bool SolveMinesweeper(bool grid[MAXN][MAXM],
                      int arr[MAXN][MAXM],
                      bool visited[MAXN][MAXM])
{

    // Function call to check if each cell
    // is visited and the solved grid is
    // satisfying the given input matrix
    bool done = isDone(arr, visited);

    // If the solution exists and
    // and all cells are visited
    if (done)
        return true;

    int x, y;

    // Function call to check if all
    // the cells are visited or not
    if (!findUnvisited(visited, x, y))
        return false;

    // Mark cell (x, y) as visited
    visited[x][y] = true;

    // Function call to check if it is
    // safe to assign a mine at (x, y)
    if (isSafe(arr, x, y)) {

        // Mark the position with a mine
        grid[x][y] = true;

        // Recursive call with (x, y) having a mine
        if (SolveMinesweeper(grid, arr, visited))

            // If solution exists, then return true
            return true;

        // Reset the position x, y
        grid[x][y] = false;
        for (int i = 0; i < 9; i++) {
            if (isValid(x + dx[i], y + dy[i]))
                arr[x + dx[i]][y + dy[i]]++;
        }
    }

    // Recursive call without (x, y) having a mine
    if (SolveMinesweeper(grid, arr, visited))

        // If solution exists then return true
        return true;

    // Mark the position as unvisited again
    visited[x][y] = false;

    // If no solution exists
    return false;
}

void minesweeperOperations(int arr[MAXN][MAXN], int N,
                           int M)
{

    // Stores the final result
    bool grid[MAXN][MAXM];

    // Stores whether the position
    // (x, y) is visited or not
    bool visited[MAXN][MAXM];

    // Initialize grid[][] and
    // visited[][] to false
    memset(grid, false, sizeof(grid));
    memset(visited, false, sizeof(visited));

    // If the solution to the input
    // minesweeper matrix exists
    if (SolveMinesweeper(grid, arr, visited)) {

        // Function call to print the grid[][]
        printGrid(grid);
    }

    // No solution exists
    else
        printf("No solution exists\n");
}

// Driver Code
int main()
{
    // Given input
    N = 7;
    M = 7;
    int arr[MAXN][MAXN] = {
        { 1, 1, 0, 0, 1, 1, 1 },
        { 2, 3, 2, 1, 1, 2, 2 },
        { 3, 5, 3, 2, 1, 2, 2 },
        { 3, 6, 5, 3, 0, 2, 2 },
        { 2, 4, 3, 2, 0, 1, 1 },
        { 2, 3, 3, 2, 1, 2, 1 },
        { 1, 1, 1, 1, 1, 1, 0 }
    };

    // Function call to perform
    // generate and solve a minesweeper
    minesweeperOperations(arr, N, M);

    return 0;
}
```

**Output:** 

```
_ _ _ _ _ _ _ 
x _ _ _ _ x _ 
_ x x _ _ _ x 
x _ x _ _ _ _ 
_ x x _ _ _ x 
_ _ _ _ _ _ _ 
_ x _ _ x _ _
```

***时间复杂度:**O(2<sup>N * M</sup>* N * M)*
***辅助空间:** O(N * M)*