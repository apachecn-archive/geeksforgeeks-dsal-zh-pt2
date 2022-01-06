# 最小移动次数，之后出现一个 3×3 的彩色方块

> 原文:[https://www . geesforgeks . org/最小移动次数-存在后-a-3x 3-彩色方块/](https://www.geeksforgeeks.org/minimum-number-of-moves-after-which-there-exists-a-3x3-coloured-square/)

给定一个最初为空的 **N * N** 板和一系列查询，每个查询由两个整数 **X** 和 **Y** 组成，其中单元格 **(X，Y)** 被绘制。任务是打印查询的编号，之后板中会有一个 **3 * 3** 的方块，上面画着所有的单元格。
如果在处理完所有查询后没有这样的方块，则打印 **-1** 。
**举例:**

> **输入:** N = 4，q = {{1，1}、{1，2}、{1，3}、{2，2}、{2，3}、{1，4}、{2，4}、{3，2}、{3，3}、{4，1}}
> **输出:** 10
> 第 10 次移动后，存在一个 3X3 的正方形，从(1，1)到(3，3)(基于 1 的索引)。
> **输入:** N = 3，q = {(1，1)，{1，2}，{1，3}}
> **输出:** -1

**方法:**这里的一个重要观察是，每次我们给一个正方形着色时，它都可以以 9 种不同的方式成为所需正方形的一部分(3 * 3 正方形的任何单元)。对于每一种可能性，检查当前单元格是否是绘制所有 9 个单元格的任何正方形的一部分。如果条件满足，打印到目前为止已处理的查询数量，否则在所有查询处理完毕后打印 **-1** 。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if the coordinate is inside the grid
bool valid(int x, int y, int n)
{
    if (x < 1 || y < 1 || x > n || y > n)
        return false;
    return true;
}

// Function that returns the count of squares
// that are coloured in the 3X3 square
// with (cx, cy) being the top left corner
int count(int n, int cx, int cy,
          vector<vector<bool> >& board)
{
    int ct = 0;

    // Iterate through 3 rows
    for (int x = cx; x <= cx + 2; x++)

        // Iterate through 3 columns
        for (int y = cy; y <= cy + 2; y++)

            // Check if the current square
            // is valid and coloured
            if (valid(x, y, n))
                ct += board[x][y];
    return ct;
}

// Function that returns the query
// number after which the grid will
// have a 3X3 coloured square
int minimumMoveSquare(int n, int m,
                      vector<pair<int, int> > moves)
{
    int x, y;
    vector<vector<bool> > board(n + 1);

    // Initialize all squares to be uncoloured
    for (int i = 1; i <= n; i++)
        board[i].resize(n + 1, false);
    for (int i = 0; i < moves.size(); i++) {
        x = moves[i].first;
        y = moves[i].second;

        // Mark the current square as coloured
        board[x][y] = true;

        // Check if any of the 3X3 squares
        // which contains the current square
        // is fully coloured
        for (int cx = x - 2; cx <= x; cx++)
            for (int cy = y - 2; cy <= y; cy++)
                if (count(n, cx, cy, board) == 9)
                    return i + 1;
    }

    return -1;
}

// Driver code
int main()
{
    int n = 3;
    vector<pair<int, int> > moves = { { 1, 1 },
                                      { 1, 2 },
                                      { 1, 3 } };
    int m = moves.size();

    cout << minimumMoveSquare(n, m, moves);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns True
# if the coordinate is inside the grid
def valid(x, y, n):

    if (x < 1 or y < 1 or x > n or y > n):
        return False;
    return True;

# Function that returns the count of squares
# that are coloured in the 3X3 square
# with (cx, cy) being the top left corner
def count(n, cx, cy, board):

    ct = 0;

    # Iterate through 3 rows
    for x in range(cx, cx + 3):

        # Iterate through 3 columns
        for y in range(cy + 3):

            # Check if the current square
            # is valid and coloured
            if (valid(x, y, n)):
                ct += board[x][y];
    return ct;

# Function that returns the query
# number after which the grid will
# have a 3X3 coloured square
def minimumMoveSquare(n, m, moves):

    x = 0
    y = 0
    board=[[] for i in range(n + 1)]

    # Initialize all squares to be uncoloured
    for i in range(1, n + 1):
        board[i] = [False for i in range(n + 1)]

    for  i in range(len(moves)):

        x = moves[i][0];
        y = moves[i][1];

        # Mark the current square as coloured
        board[x][y] = True;

        # Check if any of the 3X3 squares
        # which contains the current square
        # is fully coloured
        for cx in range(x - 2, x + 1 ):
            for cy in range(y - 2, y + 1):   
                if (count(n, cx, cy, board) == 9):
                    return i + 1;
    return -1;

# Driver code
if __name__=='__main__':

    n = 3;
    moves = [[ 1, 1 ],[ 1, 2 ], [ 1, 3 ]]
    m = len(moves)

    print(minimumMoveSquare(n, m, moves))

    # This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if the coordinate is inside the grid
function valid(x, y, n)
{
    if (x < 1 || y < 1 || x > n || y > n)
        return false;
    return true;
}

// Function that returns the count of squares
// that are coloured in the 3X3 square
// with (cx, cy) being the top left corner
function count(n, cx, cy, board)
{
    var ct = 0;

    // Iterate through 3 rows
    for (var x = cx; x <= cx + 2; x++)

        // Iterate through 3 columns
        for (var y = cy; y <= cy + 2; y++)

            // Check if the current square
            // is valid and coloured
            if (valid(x, y, n))
                ct += board[x][y];
    return ct;
}

// Function that returns the query
// number after which the grid will
// have a 3X3 coloured square
function minimumMoveSquare(n, m, moves)
{
    var x, y;
    var board = Array.from(Array(n+1), ()=>Array(n+1).fill(false));

    for (var i = 0; i < moves.length; i++) {
        x = moves[i][0];
        y = moves[i][1];

        // Mark the current square as coloured
        board[x][y] = true;

        // Check if any of the 3X3 squares
        // which contains the current square
        // is fully coloured
        for (var cx = x - 2; cx <= x; cx++)
            for (var cy = y - 2; cy <= y; cy++)
                if (count(n, cx, cy, board) == 9)
                    return i + 1;
    }

    return -1;
}

// Driver code
var n = 3;
var moves = [ [ 1, 1 ],
                                  [ 1, 2 ],
                                  [ 1, 3 ] ];
var m = moves.length;
document.write( minimumMoveSquare(n, m, moves));

// This code is contributed by famously.
</script>
```

**Output:** 

```
-1
```