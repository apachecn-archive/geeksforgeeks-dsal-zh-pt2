# 设置二元矩阵所有元素所需的最小运算次数

> 原文:[https://www . geesforgeks . org/最小操作数-设置二进制矩阵的所有元素所需的操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-set-all-elements-of-a-binary-matrix/)

给定由维度 **M * N** 的**1 和 0**组成的二元矩阵 **mat[][]** ，任务是找到将所有 0 转换为 1 的操作数。在每个操作中，所有 1 都可以将相邻的 0 转换为 1。
**注:**对角元素不视为矩阵中某个数的相邻元素。
**举例:**

> **输入:** mat[][] = {{0，1，1，0，1}，
> {0，1，0，1，0}，
> {0，0，0，0，1}，
> {0，0，1，0，0，0}}
> **输出:** 2
> **说明:**所有相邻元素都是左/右/上/下方向。
> 运算前的矩阵为:
> 0 1 1 0 1
> 0 1 0 1 0
> 0 0 0 1
> 0 1 0 0
> 在上例中，运算如下:
> 运算 1 后， 矩阵将为:
> **1**1 1**1**1
> **1**1**1**1**1**T30】0**1**T33】1T35】11
> 0**1**1**1**T42】1T44】术后

**进场:**

1.  [遍历整个矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，将值为 1 的矩阵元素的坐标推入[队列](https://www.geeksforgeeks.org/queue-data-structure/)。
2.  将队列的大小保存在变量 **x** 中。
3.  遍历 **x** 迭代的队列。
4.  对于每次迭代，都会遇到值为 1 的元素的位置。将相邻位置的值转换为 1(仅当相邻元素为 0 时)，然后将新转换的 1 的坐标推送到队列中。
5.  在每一次 **x** 迭代中，一旦执行了步骤 4，就将队列的前面元素出列。
6.  一旦遍历了队列的 **x** 元素，就将操作数的计数增加到 1。
7.  重复步骤 2 到步骤 6，直到队列为空。
8.  返回队列为空后的操作数计数。如果矩阵全为 1，则不执行任何操作，计数为 0。

下面是上述方法的实现。

## C++

```
// C++ code for the above approach.

#include <bits/stdc++.h>
using namespace std;

// function to check whether the
// adjacent neighbour is a valid
// index or not
bool check(int row, int col,
           int r, int c) {

    return (r >= 0 && r < row
            && c >= 0 && c < col);
}

// function to calculate the
// number of operations
int bfs(int row, int col,
        int *grid) {

    // direction matrix to find
    // adjacent neighbours
    int dir[4][2] = { { 1, 0 },
                      { -1, 0 },
                      { 0, 1 },
                      { 0, -1 } };

    // queue with pair to store
    // the indices of elements
    queue<pair<int, int> > q;

    // scanning the matrix to push
    // initial 1 elements
    for (int i = 0; i < row; i++)
    {
        for (int j = 0;
             j < col; j++) {

          if (*((grid+i*col) + j))
            q.push(make_pair(i, j));
        }
    }

    // Step 2 to Step 6
    int op = -1;
    while (!q.empty()) {

      int x = q.size();
      for (int k = 0;
           k < x; k++) {

        pair<int, int> p =
                 q.front();
        q.pop();

        // adding the values of
        // direction matrix to the
        // current element to get
        // 4 possible adjacent
        // neighbours
        for (int i = 0;
             i < 4; i++) {

          int r = p.first +
                  dir[i][0];
          int c = p.second +
                  dir[i][1];

          // checking the validity
          // of the neighbour
          if (*((grid+r*col) + c) == 0
             && check(row, col, r, c)) {

            // pushing it to the queue
            // and converting it to 1
            q.push(make_pair(r, c));
            *((grid+r*col) + c) = 1;
          }
        }
      }
      // increasing the operation by 1
      // after the first pass
      op++;
    }
    return op;
}

// Driver code
int main()
{
  int row = 4, col = 5;
  int grid[][col] =
          { { 0, 1, 1, 0, 1 },
            { 0, 1, 0, 1, 0 },
            { 0, 0, 0, 0, 1 },
            { 0, 0, 1, 0, 0 } };

  cout << bfs(row, col,
              (int *)grid);
}
```

## 蟒蛇 3

```
# Python 3 code for the above approach.

# function to check whether the
# adjacent neighbour is a valid
# index or not
def check(row, col, r, c):
    return (r >= 0 and r < row
            and c >= 0 and c < col)

# function to calculate the
# number of operations
def bfs(row, col, grid):

    # direction matrix to find
    # adjacent neighbours
    dir = [[1, 0],
           [-1, 0],
           [0, 1],
           [0, -1]]

    # queue with pair to store
    # the indices of elements
    q = []

    # scanning the matrix to push
    # initial 1 elements
    for i in range(row):
        for j in range(col):
            if (grid[i][j]):
                q.insert(0, [i, j])

    # Step 2 to Step 6
    op = -1
    while (len(q) != 0):
        x = len(q)
        for k in range(x):
            p = q[0]
            q.pop(0)

            # adding the values of
            # direction matrix to the
            # current element to get
            # 4 possible adjacent
            # neighbours
            for i in range(4):
                r = p[0] + dir[i][0]
                c = p[1] + dir[i][1]

                # checking the validity
                # of the neighbour
                if (check(row, col, r, c)
                        and grid[r] == 0 ):

                    # pushing it to the queue
                    # and converting it to 1
                    q.insert(0, [r, c])
                    grid[r] = 1

        # increasing the operation by 1
        # after the first pass
        op += 1

    return op
    #return 0

# Driver code
if __name__ == "__main__":

    row = 4
    col = 5
    grid = [[0, 1, 1, 0, 1],
            [0, 1, 0, 1, 0],
            [0, 0, 0, 0, 1],
            [0, 0, 1, 0, 0]]

    print(bfs(row, col,
              grid))

    # This code is contributed by ukasp.
```

**Output:** 

```
2
```

***时间复杂度:** O(M * N)*
***辅助空间复杂度:** O(M * N)*