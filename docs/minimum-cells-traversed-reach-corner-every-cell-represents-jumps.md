# 到达每个单元格代表跳跃的角落所经过的最小单元格数

> 原文:[https://www . geesforgeks . org/minimum-cells-traversed-reach-corner-ever-cell-presents-jumps/](https://www.geeksforgeeks.org/minimum-cells-traversed-reach-corner-every-cell-represents-jumps/)

假设 A 位于包含“m”行和“n”列的二维网格的位置(0，0)。他的目标是通过尽可能少的细胞到达这个网格的右下角。
网格的每个单元格都包含一个正整数，定义了 A 到达该单元格时可以向右或向下跳转的单元格数。
找到需要触摸的最小单元格数，以便到达右下角。
**例:**

```
Input : 2 4 2
        5 3 8
        1 1 1
Output :
So following two paths exist to reach (2, 2) from (0, 0)
(0, 0) => (0, 2) => (2, 2) 
(0, 0) => (2, 0) => (2, 1) => (2, 2) 

Hence the output for this test case should be 3 
```

以下是问题的[广度优先搜索(BFS)](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 解决方案:

1.  把这个矩阵想象成树，把(0，0)想象成根，用水平顺序遍历来应用 BFS。
2.  推送队列中的坐标和跳转次数。
3.  在每一级树后弹出队列。
4.  向右下方移动时，将单元格中的值添加到坐标中。
5.  到达右下角时返回跳跃时触摸的单元格数。

## C++

```
// C++ program to reach bottom right corner using
// minimum jumps.
#include <bits/stdc++.h>
using namespace std;
#define R 3
#define C 3

// function to check coordinates are in valid range.
bool safe(int x, int y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;
    return false;
}

// function to return minimum no of cells to reach
// bottom right cell.
int matrixJump(int M[R][C], int R1, int C1)
{
    queue<pair<int, pair<int, int> > > q;

    // push the no of cells and coordinates in a queue.
    q.push(make_pair(1, make_pair(R1, C1)));

    while (!q.empty()) {
        int x = q.front().second.first; // x coordinate
        int y = q.front().second.second; // y coordinate
        int no_of_cells = q.front().first; // no of cells

        q.pop();

        // when it reaches bottom right return no of cells
        if (x == R - 1 && y == C - 1)           
            return no_of_cells;

        int v = M[x][y];

        if (safe(x + v, y))
            q.push(make_pair(no_of_cells + 1, make_pair(x + v, y)));

        if (safe(x, y + v))
            q.push(make_pair(no_of_cells + 1, make_pair(x, y + v)));
    }

    // when destination cannot be reached
    return -1;
}

// driver function
int main()
{
    int M[R][C] = { { 2, 4, 2 },
                    { 5, 3, 8 },
                    { 1, 1, 1 } };
    cout << matrixJump(M, 0, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reach bottom right corner
// using minimum jumps.
import java.util.*;

class GFG
{
static int R = 3, C = 3;

// function to check coordinates are in valid range.
static boolean safe(int x, int y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;
    return false;
}

// pair class
static class pair<T, R>
{
    T first;
    R second;
    pair(T t, R r)
    {
        first = t;
        second = r;
    }
}

// function to return minimum no of cells
// to reach bottom right cell.
static int matrixJump(int M[][], int R1, int C1)
{
    Queue<pair<Integer,
          pair<Integer,
               Integer>>> q = new LinkedList<>();

    // push the no of cells and coordinates in a queue.
    q.add(new pair(1, new pair(R1, C1)));

    while (q.size() > 0)
    {
        int x = q.peek().second.first; // x coordinate
        int y = q.peek().second.second; // y coordinate
        int no_of_cells = q.peek().first; // no of cells

        q.remove();

        // when it reaches bottom right return no of cells
        if (x == R - 1 && y == C - 1)        
            return no_of_cells;

        int v = M[x][y];

        if (safe(x + v, y))
            q.add(new pair(no_of_cells + 1,
                  new pair(x + v, y)));

        if (safe(x, y + v))
            q.add(new pair(no_of_cells + 1,
                  new pair(x, y + v)));
    }

    // when destination cannot be reached
    return -1;
}

// Driver Code
public static void main(String ars[])
{
    int M[][] = {{ 2, 4, 2 },
                 { 5, 3, 8 },
                 { 1, 1, 1 }};
    System.out.print( matrixJump(M, 0, 0));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to reach bottom
# right corner using minimum jumps.

R, C = 3, 3

# Function to check coordinates are in valid range.
def safe(x, y):

    if x < R and y < C and x >= 0 and y >= 0:
        return True
    return False

# Function to return minimum no of
# cells to reach bottom right cell.
def matrixJump(M, R1, C1):

    q = []

    # push the no of cells and coordinates in a queue.
    q.append((1, (R1, C1)))

    while len(q) != 0:
        x = q[0][1][0] # x coordinate
        y = q[0][1][1] # y coordinate
        no_of_cells = q[0][0] # no of cells

        q.pop(0)

        # when it reaches bottom right return no of cells
        if x == R - 1 and y == C - 1:        
            return no_of_cells

        v = M[x][y]

        if safe(x + v, y):
            q.append((no_of_cells + 1, (x + v, y)))

        if safe(x, y + v):
            q.append((no_of_cells + 1, (x, y + v)))

    # when destination cannot be reached
    return -1

# Driver code
if __name__ == "__main__":

    M = [[2, 4, 2],
        [5, 3, 8],
        [1, 1, 1]]

    print(matrixJump(M, 0, 0))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to reach bottom right corner
// using minimum jumps.
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

static int R = 3, C = 3;

// function to check coordinates are in valid range.
static Boolean safe(int x, int y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;
    return false;
}

// Pair class
public class Pair<T, U>
{
    public T first;
    public U second;
    public Pair() {
    }

    public Pair(T first, U second)
    {
        this.first = first;
        this.second = second;
    }

};

// function to return minimum no of cells
// to reach bottom right cell.
static int matrixJump(int [,]M, int R1, int C1)
{
    Queue<Pair<int,Pair<int,int>>> q =
    new Queue<Pair<int,Pair<int,int>>>();

    // push the no of cells and coordinates in a queue.
    q.Enqueue(new Pair<int, Pair<int, int>>(
                1, new Pair<int, int>(R1, C1)));

    while (q.Count > 0)
    {
        int x = q.Peek().second.first; // x coordinate
        int y = q.Peek().second.second; // y coordinate
        int no_of_cells = q.Peek().first; // no of cells

        q.Dequeue();

        // when it reaches bottom right return no of cells
        if (x == R - 1 && y == C - 1)        
            return no_of_cells;

        int v = M[x, y];

        if (safe(x + v, y))
            q.Enqueue(new Pair<int,Pair<int,int>>(no_of_cells + 1,
                new Pair<int,int>(x + v, y)));

        if (safe(x, y + v))
            q.Enqueue(new Pair<int,Pair<int,int>>(no_of_cells + 1,
                new Pair<int,int>(x, y + v)));
    }

    // when destination cannot be reached
    return -1;
}

// Driver Code
public static void Main(String []ars)
{
    int [,]M = {{ 2, 4, 2 },
                { 5, 3, 8 },
                { 1, 1, 1 }};
    Console.Write( matrixJump(M, 0, 0));
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript program to reach bottom right corner
// using minimum jumps.

let R = 3, C = 3;

// function to check coordinates are in valid range.
function safe(x,y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;
    return false;
}

// pair class
class pair
{
    constructor(t,r)
    {
        this.first = t;
        this.second = r;
    }
}

// function to return minimum no of cells
// to reach bottom right cell.
function matrixJump(M,R1,C1)
{
    let q=[];
    // push the no of cells and coordinates in a queue.
    q.push(new pair(1, new pair(R1, C1)));

    while (q.length > 0)
    {
        let x = q[0].second.first; // x coordinate
        let y = q[0].second.second; // y coordinate
        let no_of_cells = q[0].first; // no of cells

        q.shift();

        // when it reaches bottom right return no of cells
        if (x == R - 1 && y == C - 1)        
            return no_of_cells;

        let v = M[x][y];

        if (safe(x + v, y))
            q.push(new pair(no_of_cells + 1,
                  new pair(x + v, y)));

        if (safe(x, y + v))
            q.push(new pair(no_of_cells + 1,
                  new pair(x, y + v)));
    }

    // when destination cannot be reached
    return -1;
}

// Driver Code
let M=[[ 2, 4, 2 ],[ 5, 3, 8 ],[ 1, 1, 1 ]];
document.write( matrixJump(M, 0, 0));                

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
 3
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由 **Kshitiz Gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。