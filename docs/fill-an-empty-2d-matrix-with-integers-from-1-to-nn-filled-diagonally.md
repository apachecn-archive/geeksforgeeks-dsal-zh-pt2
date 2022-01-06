# 用对角填充的 1 到 N*N 的整数填充一个空的 2D 矩阵

> 原文:[https://www . geesforgeks . org/fill-a-empty-2d-matrix-with-integers-from-1-nn-filled-对角/](https://www.geeksforgeeks.org/fill-an-empty-2d-matrix-with-integers-from-1-to-nn-filled-diagonally/)

给定一个整数 **N** ，任务是填充大小为 **NxN** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **M** ，从主对角线开始，然后在上下三角形对角线之间交替，以递增的方式，使得从 **1** 到 **N <sup>2</sup>** 的每个数字只出现一次。

**示例:**

```
Input: N = 4
Output: 
1 8 13 16
5 2 9 14
11 6 3 10
15 12 7 4
Explanation:
First filling the main diagonal:
 1   
    2  
       3 
          4
Next, fill the lower diagonal below the main diagonal
 1 
 5  2  
    6  3 
      7  4
Next, fill the upper diagonal above the main diagonal
 1  8 
 5  2  9 
    6  3 10
       7  4
Following the same pattern and altering between 
upper and lower triangular matrix, 
we get the final matrix as
 1  8 13 16
 5  2  9 14
11  6  3 10
15 12  7  4

Input: N = 3
Output:
1 6 9
4 2 7
8 5 3
```

**方法:**按照以下步骤解决问题:

*   初始化一个变量**使**变为 **1** 。这将跟踪当前的数字
*   将变量 **d** 初始化为 **1** 。这将跟踪对角线。
*   使用 **d** 从 **1** 迭代到 **(N+N-1)** 。这是对角线的数量。
    *   如果 d 为偶数，将两个变量 **r** 和 **c** 分别初始化为 **d/2** 和 **0** 。
    *   否则，将两个变量 **r** 和 **c** 分别初始化为 **0** 和 **d/2** 。
    *   迭代到 **r** 和 **c** 都小于 **N**
        *   将矩阵 **M** 更新为**M【r】= cur。**
        *   增加**曲线**、 **r** 和 **c** 。
    *   退出内环后，增加 **d** 。
*   最后，[显示矩阵](https://www.geeksforgeeks.org/print-2-d-array-matrix-java/) **M** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to fill the matrix diagonally alternating
// between upper and lower diagonals
void fillMatrix(int N)
{
    // variables to keep track of
    // diagonals and current number
    int d = 1, cur = 1;
    // Matrix
    int M[N][N];
    // Iterating over all diagonals
    while (d <= 2 * N - 1) {
        int r, c;
        // For lower triangle
        if (d % 2 == 0)
            r = d / 2, c = 0;
        // For upper triangle
        else
            r = 0, c = d / 2;
        // Placing the current number
        // in appropriate position
        while (r < N && c < N) {
            M[r] = cur;
            cur++;
            r++;
            c++;
        }
        d++;
    }

    // Displaying the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cout << M[i][j] << " ";
        }
        cout << endl;
    }
}
// Driver code
int main()
{
    // Input
    int N = 4;

    // Function calling
    fillMatrix(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {
    static void fillmatrix(int m[][], int n)
    {

        int r, c;
        int num = 1, d = 1;
        // 2*n-1 is no of diagonals
        while (d <= 2 * n - 1) {
            // If d%2==0 switch to
            // lower triangular diagonal
            if (d % 2 == 0) {
                r = d / 2;
                c = 0;
                while (r < n && c < n) {
                    m[r] = num++;
                    r++;
                    c++;
                }
            }
            // If d%2==1 switch to
            // upper triangular diagonal
            else {
                r = 0;
                c = d / 2;
                while (c < n && r < n) {
                    m[r] = num++;
                    r++;
                    c++;
                }
            }
            d++;
        }
    }
    // Utility function to display the matrix
    static void display(int m[][], int n)
    {
        int i, j;
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                System.out.printf(m[i][j] + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args)
    {
        int n = 4;
        int[][] m = new int[4][4];
        fillmatrix(m, n);
        display(m, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to fill the matrix diagonally
# alternating between upper and lower diagonals
def fillMatrix(N):

    # Variables to keep track of
    # diagonals and current number
    d = 1
    cur = 1

    # Matrix
    M = [[0 for i in range(N)]
            for i in range(N)]

    # Iterating over all diagonals
    while (d <= 2 * N - 1):
        r, c = 0, 0

        # For lower triangle
        if (d % 2 == 0):
            r = d // 2
            c = 0

        # For upper triangle
        else:
            r = 0
            c = d // 2

        # Placing the current number
        # in appropriate position
        while (r < N and c < N):
            M[r] = cur
            cur += 1
            r += 1
            c += 1

        d += 1

    # Displaying the matrix
    for i in M:
        print(*i)

# Driver code
if __name__ == '__main__':

    # Input
    N = 4

    # Function calling
    fillMatrix(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System.IO;
using System;

class GFG{

static void fillmatrix(int[, ] m, int n)
{
    int r, c;
    int num = 1, d = 1;

    // 2*n-1 is no of diagonals
    while (d <= 2 * n - 1)
    {

        // If d%2==0 switch to
        // lower triangular diagonal
        if (d % 2 == 0)
        {
            r = d / 2;
            c = 0;
            while (r < n && c < n)
            {
                m[r, c] = num++;
                r++;
                c++;
            }
        }

        // If d%2==1 switch to
        // upper triangular diagonal
        else
        {
            r = 0;
            c = d / 2;

            while (c < n && r < n)
            {
                m[r, c] = num++;
                r++;
                c++;
            }
        }
        d++;
    }
}

// Utility function to display the matrix
static void display(int[,] m, int n)
{
    int i, j;
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < n; j++)
        {
            Console.Write(m[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver code
static void Main()
{
    int n = 4;
    int[,] m = new int[4, 4];

    fillmatrix(m, n);
    display(m, n);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach
    function fillmatrix(m, n)
    {

        let r, c;
        let num = 1, d = 1;

        // 2*n-1 is no of diagonals
        while (d <= 2 * n - 1)
        {

            // If d%2==0 switch to
            // lower triangular diagonal
            if (d % 2 == 0)
            {
                r = parseInt(d / 2, 10);
                c = 0;
                while (r < n && c < n)
                {
                    m[r] = num++;
                    r++;
                    c++;
                }
            }

            // If d%2==1 switch to
            // upper triangular diagonal
            else {
                r = 0;
                c = parseInt(d / 2, 10);
                while (c < n && r < n) {
                    m[r] = num++;
                    r++;
                    c++;
                }
            }
            d++;
        }
    }

    // Utility function to display the matrix
    function display(m, n)
    {
        let i, j;
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                document.write(m[i][j] + " ");
            }
            document.write("</br>");
        }
    }

    let n = 4;
    let m = new Array(4);
    for(let i = 0; i < m.length; i++)
    {
        m[i] = new Array(m.length);
        for(let j = 0; j < m.length; j++)
        {
            m[i][j] = 0;
        }
    }
    fillmatrix(m, n);
    display(m, n);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
1 8 13 16 
5 2 9 14 
11 6 3 10 
15 12 7 4 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*