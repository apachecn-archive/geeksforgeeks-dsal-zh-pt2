# 最小化将矩阵中的所有 1 移动到给定索引所需的步骤

> 原文:[https://www . geesforgeks . org/将矩阵中所有 1 移动到给定索引所需的最小化步骤/](https://www.geeksforgeeks.org/minimize-steps-required-to-move-all-1s-in-a-matrix-to-a-given-index/)

给定大小为 **NxM** 的二进制矩阵 **mat[][]** 和两个整数 **X** 和 **Y** ，任务是找到将给定矩阵中的所有 **1 的**移动到单元格 **(X，Y)** 所需的最小步数，其中，一步涉及将单元格**向左、向右、向上**或向下**移动。
**举例:**** 

> ****输入:** mat[][] = { {1，0，1}，{0，1，0}，{1，0，1} }，X = 1，Y = 1
> **输出:** 8
> **说明:**
> 单元格(0，0)，(0，2)，(1，1)，(2，0)和(2，2)由 1 组成。
> 将索引(0，0)处的 1 移动到(1，1)需要 2 个步骤
> (0，0) - > (0，1) - > (1，0)
> 将索引(0，2)处的 1 移动到(1，1)需要 2 个步骤
> 将索引(2，0)处的 1 移动到(1，1)需要 2 个步骤
> 将索引(2，2)处的 1 移动到(1，1)需要 2 个步骤
> 因此，需要 8 个步骤。
> **输入:** mat[][] = { {1，0，0，0}，{0，1，0，1}，{1，0，1，1} }，X = 0，Y = 2
> **输出:** 15**

****方法:**
思路是遍历给定矩阵，找到由 **1** 组成的单元。对于由 **1** 组成的任何单元 **(i，j)** ，根据给定的方向到达 **(X，Y)** 所需的最小步数由下式给出:** 

```
Minimum steps = abs(X - i) + abs(Y - j)
```

**使用上述公式计算给定矩阵**mat【】【】**中包含 **1** 的每个单元格所需的总步数。
以下是上述方法的实施:** 

## **C++**

```
// C++ program to calculate
// the minimum steps
// required to reach
// a given cell from all
// cells consisting of 1's
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return the minimum
// number of steps required
// to move all 1s to (X, Y)
int findAns(vector<vector<int> > mat,
            int x, int y,
            int n, int m)
{
    int ans = 0;

    // Iterate the given matrix
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < m; j++) {

            // Update the answer with
            // minimum moves required
            // for the given element
            // to reach the given index
            if (mat[i][j] == 1) {

                ans += abs(x - i)
                    + abs(y - j);
            }
        }
    }

    // Return the number
    // of steps
    return ans;
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > mat
        = { { 1, 0, 0, 0 },
            { 0, 1, 0, 1 },
            { 1, 0, 1, 1 } };

    // Given position
    int x = 0, y = 2;

    // Function Call
    cout << findAns(mat, x, y,
                    mat.size(),
                    mat[0].size())
        << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to calculate the
// minimum steps required to reach
// a given cell from all cells
// consisting of 1's
import java.util.*;

class GFG{

// Function to calculate and
// return the minimum number
// of steps required to move
// all 1s to (X, Y)
static int findAns(int [][]mat,
                   int x, int y,
                   int n, int m)
{
    int ans = 0;

    // Iterate the given matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Update the answer with
            // minimum moves required
            // for the given element
            // to reach the given index
            if (mat[i][j] == 1)
            {
                ans += Math.abs(x - i) +
                       Math.abs(y - j);
            }
        }
    }

    // Return the number
    // of steps
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Given matrix
    int [][]mat = { { 1, 0, 0, 0 },
                    { 0, 1, 0, 1 },
                    { 1, 0, 1, 1 } };

    // Given position
    int x = 0, y = 2;

    // Function Call
    System.out.print(findAns(mat, x, y,
                             mat.length,
                             mat[0].length) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## **蟒蛇 3**

```
# Python3 program to calculate
# the minimum steps required to
# reach a given cell from all
# cells consisting of 1's

# Function to calculate and
# return the minimum number
# of steps required to move
# all 1s to (X, Y)
def findAns(mat, x, y, n, m):

    ans = 0

    # Iterate the given matrix
    for i in range(n):
        for j in range(m):

            # Update the answer with
            # minimum moves required
            # for the given element
            # to reach the given index
            if (mat[i][j] == 1):
                ans += (abs(x - i) +
                        abs(y - j))

    # Return the number
    # of steps
    return ans

# Driver Code

# Given matrix
mat = [ [ 1, 0, 0, 0 ],
        [ 0, 1, 0, 1 ],
        [ 1, 0, 1, 1 ] ]

# Given position
x = 0
y = 2

# Function call
print(findAns(mat, x, y, len(mat),
                        len(mat[0])))

# This code is contributed by shubhamsingh10
```

## **C#**

```
// C# program to calculate the
// minimum steps required to reach
// a given cell from all cells
// consisting of 1's
using System;

class GFG{

// Function to calculate and
// return the minimum number
// of steps required to move
// all 1s to (X, Y)
static int findAns(int [,]mat,
                   int x, int y,
                   int n, int m)
{
    int ans = 0;

    // Iterate the given matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Update the answer with
            // minimum moves required
            // for the given element
            // to reach the given index
            if (mat[i, j] == 1)
            {
                ans += Math.Abs(x - i) +
                       Math.Abs(y - j);
            }
        }
    }

    // Return the number
    // of steps
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Given matrix
    int [,]mat = { { 1, 0, 0, 0 },
                   { 0, 1, 0, 1 },
                   { 1, 0, 1, 1 } };

    // Given position
    int x = 0, y = 2;

    // Function call
    Console.Write(findAns(mat, x, y,
                          mat.GetLength(0),
                          mat.GetLength(1)) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

// JavaScript program to calculate the
// minimum steps required to reach
// a given cell from all cells
// consisting of 1's

// Function to calculate and
// return the minimum number
// of steps required to move
// all 1s to (X, Y)
function findAns(mat, x, y,
                   n, m)
{
    let ans = 0;

    // Iterate the given matrix
    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < m; j++)
        {

            // Update the answer with
            // minimum moves required
            // for the given element
            // to reach the given index
            if (mat[i][j] == 1)
            {
                ans += Math.abs(x - i) +
                       Math.abs(y - j);
            }
        }
    }

    // Return the number
    // of steps
    return ans;
}

// Driver Code

    // Given matrix
    let mat = [[ 1, 0, 0, 0 ],
                    [ 0, 1, 0, 1 ],
                    [ 1, 0, 1, 1 ]];

    // Given position
    let x = 0, y = 2;

    // Function Call
    document.write(findAns(mat, x, y,
                             mat.length,
                             mat[0].length) + "<br/>");

</script>
```

****Output:** 

```
15
```** 

****时间复杂度:***O(N * M)*
T5】辅助空间: *O(1)***