# 矩阵的最大和，其中每个值来自唯一的行和列

> 原文:[https://www . geesforgeks . org/矩阵的最大和-其中每个值来自唯一的行和列/](https://www.geeksforgeeks.org/maximum-sum-of-a-matrix-where-each-value-is-from-a-unique-row-and-column/)

给定一个大小为 **N X N** 的**矩阵**，任务是找到这个矩阵的最大和，其中每个值都是从每行的唯一列中选取的。
**例:**

```
Input: matrix = [[3, 4, 4, 4],
                 [1, 3, 4, 4], 
                 [3, 2, 3, 4], 
                 [4, 4, 4, 4]]
Output: 16
Explanation:
Selecting (0, 1) from row 1 = 4
Selecting (1, 2) from row 2 = 4
Selecting (2, 3) from row 3 = 4
Selecting (3, 0) from row 4 = 4
Therefore, max sum = 4 + 4 + 4 + 4 = 16

Input: matrix = [[0, 1, 0, 1], 
                 [3, 0, 0, 2], 
                 [1, 0, 2, 0], 
                 [0, 2, 0, 0]]
Output: 8
Explanation: 
Selecting (0, 3) from row 1 = 1
Selecting (1, 0) from row 2 = 3
Selecting (2, 2) from row 3 = 2
Selecting (3, 1) from row 4 = 2
Therefore, max sum = 1 + 3 + 2 + 2 = 8
```

**进场:**

*   生成一个大小为 N 的数字字符串，包含从 1 到 N 的数字
*   [求这个字符串的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/) (N！).
*   现在配对是在排列之间完成的，这样每个 N！配对每行都有一个唯一的列。
*   然后计算所有对的值的总和。

以下是上述方法的实现:

## 蟒蛇 3

```
# Python code for maximum sum of
# a Matrix where each value is
# from a unique row and column

# Permutations using library function
from itertools import permutations

# Function MaxSum to find
# maximum sum in matrix
def MaxSum(side, matrix):

    s = ''
    # Generating the string
    for i in range(0, side):
        s = s + str(i)

    # Permutations of s string
    permlist = permutations(s)

    # List all possible case
    cases = []

    # Append all possible case in cases list
    for perm in list(permlist):
        cases.append(''.join(perm))

    # List to store all Sums
    sum = []

    # Iterate over all case
    for c in cases:
        p = []
        tot = 0
        for i in range(0, side):
            p.append(matrix[int(s[i])][int(c[i])])
        p.sort()
        for i in range(side-1, -1, -1):
            tot = tot + p[i]
        sum.append(tot)

    # Maximum of sum list is
    # the max sum
    print(max(sum))

# Driver code
if __name__ == '__main__':

    side = 4
    matrix = [[3, 4, 4, 4], [1, 3, 4, 4], [3, 2, 3, 4], [4, 4, 4, 4]]
    MaxSum(side, matrix)
    side = 3
    matrix = [[1, 2, 3], [6, 5, 4], [7, 9, 8]]
    MaxSum(side, matrix)
```

**Output:** 

```
16
18
```

***时间复杂度:** O(K)* ，其中 K = N！
***辅助空间复杂度:** O(K)* ，其中 K = N！