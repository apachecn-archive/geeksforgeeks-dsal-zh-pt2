# 求二进制矩阵中的最大路径长度

> 原文:[https://www . geesforgeks . org/find-二进制矩阵中的最大路径长度/](https://www.geeksforgeeks.org/find-maximum-path-length-in-a-binary-matrix/)

给定一个正方形矩阵 *mat* ，其每个元素要么是 *0* 要么是 *1* 。值 1 表示已连接，0 表示未连接。任务是在将 Atmos 1*0*改为 *1* 后，找到矩阵中路径的最大长度。路径是一组 4 个方向相连的 1。

**示例:**

> **输入:** mat[][] = {{1，1}，{1，0}}
> **输出:** 4
> 仅将 0 更改为 1，最大路径的长度将为 4。
> 
> **输入:** mat[][] = {{1，1}，{1，1 } }
> T3】输出: 4

**天真的做法:**想法是把每个‘0’一个一个改成‘1’，做一个[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)找到最大路径的大小。

**高效方法:**在幼稚方法中，我们已经检查了每一个‘0’。然而，我们也可以通过存储每个组的大小来提高效率，这样我们就不必使用深度优先搜索来再次重复计算相同的大小。

**注意:**当 0 接触到同一个组时，我们需要小心。例如，考虑网格= [[0，1]，[1，1]]。将 *0* 更改为 *1* 后， *0* 的右侧和底部邻居将属于同一组。

我们可以通过跟踪组 *Id* (或*索引*)来解决这个问题，这对于每个组都是唯一的。

*   对于每个组，用值*索引*填充它，并记住它的大小作为数组*区域【索引】*中的一个元素，可以通过深度优先搜索找到它..
*   然后对于每个 *0* ，查看相邻的组标识并添加这些组的面积，并为我们正在切换的 *0* 添加 *1* 。这会给我们答案，我们从之前的答案中取其最大值。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 implementation of above approach

# check if index is within range
def neighbors(r, c, N):
    for nr, nc in ((r - 1, c), (r + 1, c), (r, c - 1), (r, c + 1)):
        if 0 <= nr < N and 0 <= nc < N:
            yield nr, nc

# dfs to calculate length of path
def dfs(R, C, index, grid, N):
    ans = 1
    grid[R][C] = index
    for nr, nc in neighbors(R, C, N):
        if grid[nr][nc] == 1:
            ans += dfs(nr, nc, index)

    return ans

# function to return largest possible length of Path
def largestPath(grid):

    N = len(grid)

    area = {}
    index = 2

    for i in range(N):
        for j in range(N):
            if grid[i][j] == 1:
                area[index] = dfs(i, j, index, grid, N)
                index += 1

    ans = max(area.values() or [0])

    for i in range(N):
        for j in range(N):
            if grid[i][j] == 0:
                seen = {grid[nr][nc] for nr, nc in neighbors(i, j, N) if grid[nr][nc] > 1}
                ans = max(ans, 1 + sum(area[i] for i in seen))

    # return maximum possible length
    return ans

# Driver code
I = [[1, 0], [0, 1]]

# Function call to print answer
print(largestPath(I))

# This code is written by
# Sanjit_Prasad
```

**Output:**

```
3

```