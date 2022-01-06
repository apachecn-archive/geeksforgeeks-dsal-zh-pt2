# 填充 NxM 网格所需的最小整数数量

> 原文:[https://www . geeksforgeeks . org/填充 nxm 网格所需的最小整数数量/](https://www.geeksforgeeks.org/minimum-number-of-integers-required-to-fill-the-nxm-grid/)

给定大小的网格(NxM)将被整数填充。

网格中单元格的填充应以下列方式进行:

1.  假设 A、B 和 C 是三个单元，B 和 C 与 A 共用一个边
2.  单元格 B 和 C 的值必须不同。
3.  设 L 是网格中不同整数的个数。
4.  每个单元格应该包含从 1 到 1 的值

任务是找到 L 的最小值和任何结果网格。

**示例:**

```
Input: N = 1, M = 2
Output:
L = 2
grid = {1, 2}

Input: 2 3
Output:
L = 3
grid = {{1, 2, 3},
        {1, 2, 3}}
Explanation: Integers in the neighbors 
of cell (2, 2) are 1, 2 and 3.
All numbers are pairwise distinct.

```

**方法:**
假设两个细胞与另一个细胞共用一个边，必须是不同的。对于每个这样的单元，网格中可能最多有 8 个单元，它们的值必须不同。
将遵循 4 色问题:填充区域所需的最大颜色为 4。

1.  对于 N <4 or M<4
    所需的整数数量可以从 1 到 4 不等。
    检查 8 个单元格，然后填充当前单元格。
    如果 8 个单元格中不同整数的个数小于 L，则用剩余的整数填充当前单元格，否则用 L+1 个整数填充当前单元格。
2.  对于 N>=4 和 M>=4
    根据 4 色问题，所需的整数个数必须为 4。
    用 4×4 矩阵填充 NxM 矩阵。

    ```
    1 2 3 4
    1 2 3 4
    3 4 1 2
    3 4 1 2
    ```

下面是上述方法的实现:

**实施:**

```
# Python 3 implementation of
# above approach

# Function to display the matrix
def display_matrix(A):
    for i in A:
        print(*i)

# Function for calculation
def cal_main(A, L, x, i, j):
    s = set()

    # Checking 8 cells and
    # then fill the current cell.
    if (i - 2) >= 0:
        s.add(A[i - 2][j])
    if (i + 2) < N:
        s.add(A[i + 2][j])
    if (j - 2) >= 0:
        s.add(A[i][j - 2])
    if (j + 2) < M:
        s.add(A[i][j + 2])
    if (i - 1) >= 0 and (j - 1) >= 0:
        s.add(A[i - 1][j - 1])
    if (i - 1) >= 0 and (j + 1) < M:
        s.add(A[i - 1][j + 1])
    if (i + 1) < N and (j - 1) >= 0:
        s.add(A[i + 1][j - 1])
    if (i + 1) < N and (j + 1) < M:
        s.add(A[i + 1][j + 1])

    # Set to contain distinct value
    # of integers in 8 cells.
    s = s.difference({0})

    if len(s) < L:

        # Set contain remaining integers
        w = x.difference(s)

        # fill the current cell
        # with maximum remaining integer
        A[i][j] = max(w)
    else:

        # fill the current cells with L + 1 integer.
        A[i][j] = L + 1
        L += 1

        # Increase the value of L
        x.add(L)
    return A, L, x

# Function to find the number
# of distinct integers
def solve(N, M):

    # initialise the list (NxM) with 0.
    A = []
    for i in range(N):
        K = []
        for j in range(M):
            K.append(0)
        A.append(K)

    # Set to contain distinct
    # value of integers from 1-L
    x = set()
    L = 0

    # Number of integer required
    # may vary from 1 to 4.
    if N < 4 or M < 4:
        if N > M:  # if N is greater
            for i in range(N):
                for j in range(M):
                    cal_main(A, L, x, i, j)

        else:
            # if M is greater
            for j in range(M):
                for i in range(N):
                    cal_main(A, L, x, i, j)
    else:

        # Number of integer required
        # must be 4
        L = 4

        # 4×4 matrix to fill the NxM matrix.
        m4 = [[1, 2, 3, 4], 
            [1, 2, 3, 4], 
            [3, 4, 1, 2], 
            [3, 4, 1, 2]]

        for i in range(4):
            for j in range(4):
                A[i][j] = m4[i][j]
        for i in range(4, N):
            for j in range(4):
                A[i][j] = m4[i % 4][j]
        for j in range(4, M):
            for i in range(N):
                A[i][j] = A[i][j % 4]
    print(L)
    display_matrix(A)

# Driver Code
if __name__ == "__main__":

    # sample input
    # Number of rows and columns
    N, M = 10, 5
    solve(N, M)
```

**Output:**

```
4
1 2 3 4 1 2 3 4 1 2
1 2 3 4 1 2 3 4 1 2
3 4 1 2 3 4 1 2 3 4
3 4 1 2 3 4 1 2 3 4
1 2 3 4 1 2 3 4 1 2
1 2 3 4 1 2 3 4 1 2
3 4 1 2 3 4 1 2 3 4
3 4 1 2 3 4 1 2 3 4
1 2 3 4 1 2 3 4 1 2
1 2 3 4 1 2 3 4 1 2

```