# 柯斯特法构造幻方

> 原文:[https://www . geeksforgeeks . org/coxeter-method-to-construction-the-magic-square/](https://www.geeksforgeeks.org/coxeter-method-to-construct-the-magic-square/)

给定一个奇数 **N** ，任务是找到秩序的幻方 **N** 。

**示例:**

> **输入:** N = 3
> **输出:**
> 6 1 8
> 7 5 3
> 2 9 4
> **输入:** N = 5
> **输出:**
> 15 8 1 24 17
> 16 14 7 5 23
> 22 20 13 6 4
> 3 21 19 12 10
> 9 2 25 18

**接近**将数值 1 放在第一行的中间。假设位置是(I，j)。

1.  现在向上移动一个单元格，向左移动一个单元格。向上或向左移动时，如果我们超出了正方形的边界，那么考虑正方形对面的一个盒子。Let (row，col)是位置。
2.  如果(行，列)处的幻方值为空，则(I，j)
3.  如果魔法[row][col]不为空，则通过将 I 增加 1 从位置(I，j)向下移动到下一行。但是，当向下移动时，如果我们超出了正方形的边界，那么考虑正方形对面的一个盒子。
4.  在幻方中的位置(I，j)插入下一个更高的数字。
5.  重复步骤 1，直到所有方块都填满。

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;
const int MAX = 10;

// Function to print the generated square
void print(int mat[MAX][MAX], int n)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << " " << mat[i][j];
        }
        cout << '\n';
    }
}

// Function to generate the magic
// square of order n
void magic_square(int magic[MAX][MAX], int n)
{
    // Position of the first value
    int i = 0;
    int j = (n - 1) / 2;

    // First value is placed
    // in the magic square
    magic[i][j] = 1;

    for (int k = 2; k <= n * n; k++) {

        // Up position
        int row = (i - 1 < 0) ? (n - 1) : (i - 1);

        // Left position
        int col = (j - 1 < 0) ? (n - 1) : (j - 1);

        // If no item is present
        if (magic[row][col] == 0) {

            // Move up and left
            i = row, j = col;
        }

        // Otherwise
        else {

            // Move downwards
            i = (i + 1) % n;
        }

        // Place the next value
        magic[i][j] = k;
    }
}

// Driver code
int main()
{
    int magic[MAX][MAX] = { 0 };
    int n = 3;

    if (n % 2 == 1) {

        // Generate the magic square
        magic_square(magic, n);

        // Print the magic square
        print(magic, n);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int MAX = 10;

    // Function to print the generated square
    static void print(int mat[][], int n)
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                System.out.print(mat[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Function to generate the magic
    // square of order n
    static void magic_square(int magic[][], int n)
    {
        // Position of the first value
        int i = 0;
        int j = (n - 1) / 2;

        // First value is placed
        // in the magic square
        magic[i][j] = 1;

        for (int k = 2; k <= n * n; k++)
        {

            // Up position
            int row = (i - 1 < 0) ?
                          (n - 1) : (i - 1);

            // Left position
            int col = (j - 1 < 0) ?
                          (n - 1) : (j - 1);

            // If no item is present
            if (magic[row][col] == 0)
            {

                // Move up and left
                i = row; j = col;
            }

            // Otherwise
            else
            {

                // Move downwards
                i = (i + 1) % n;
            }

            // Place the next value
            magic[i][j] = k;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int magic[][] = new int[MAX][MAX];

        int n = 3;

        if (n % 2 == 1)
        {

            // Generate the magic square
            magic_square(magic, n);

            // Print the magic square
            print(magic, n);
        }
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 10

# Function to print the generated square
def printf(mat, n):
    for i in range(n):
        for j in range(n):
            print(mat[i][j], end = " ")

        print("\n", end = "")

# Function to generate the magic
# square of order n
def magic_square(magic,n):

    # Position of the first value
    i = 0
    j = (n - 1) // 2

    # First value is placed
    # in the magic square
    magic[i][j] = 1

    for k in range(2, n * n + 1, 1):

        # Up position
        if(i - 1 < 0):
            row = (n - 1)
        else:
            row = (i - 1)

        # Left position
        if(j - 1 < 0):
            col = (n - 1)
        else:
            col = (j - 1)

        # If no item is present
        if (magic[row][col] == 0):

            # Move up and left
            i = row
            j = col

        # Otherwise
        else:

            # Move downwards
            i = (i + 1) % n

        # Place the next value
        magic[i][j] = k

# Driver code
if __name__ == '__main__':
    magic = [[0 for i in range(MAX)]
                for j in range(MAX)]
    n = 3

    if (n % 2 == 1):

        # Generate the magic square
        magic_square(magic, n)

        # Print the magic square
        printf(magic, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MAX = 10;

    // Function to print the generated square
    static void print(int [,]mat, int n)
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                Console.Write(mat[i, j] + " ");
            }
            Console.WriteLine();
        }
    }

    // Function to generate the magic
    // square of order n
    static void magic_square(int [,]magic, int n)
    {
        // Position of the first value
        int i = 0;
        int j = (n - 1) / 2;

        // First value is placed
        // in the magic square
        magic[i, j] = 1;

        for (int k = 2; k <= n * n; k++)
        {

            // Up position
            int row = (i - 1 < 0) ?
                          (n - 1) : (i - 1);

            // Left position
            int col = (j - 1 < 0) ?
                          (n - 1) : (j - 1);

            // If no item is present
            if (magic[row, col] == 0)
            {

                // Move up and left
                i = row; j = col;
            }

            // Otherwise
            else
            {

                // Move downwards
                i = (i + 1) % n;
            }

            // Place the next value
            magic[i, j] = k;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int [,]magic = new int[MAX, MAX];

        int n = 3;

        if (n % 2 == 1)
        {

            // Generate the magic square
            magic_square(magic, n);

            // Print the magic square
            print(magic, n);
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 10;

// Function to print the generated square
function print( mat, n)
{
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < n; j++) {
            document.write(mat[i][j]+" ");
        }
        document.write("<br>");
    }
}

// Function to generate the magic
// square of order n
function magic_square(magic, n)
{
    // Position of the first value
    var i = 0;
    var j = parseInt((n - 1) / 2);

    // First value is placed
    // in the magic square
    magic[i][j] = 1;

    for (var k = 2; k <= n * n; k++) {

        // Up position
        var row = (i - 1 < 0) ? (n - 1) : (i - 1);

        // Left position
        var col = (j - 1 < 0) ? (n - 1) : (j - 1);

        // If no item is present
        if (magic[row][col] == 0) {

            // Move up and left
            i = row, j = col;
        }

        // Otherwise
        else {

            // Move downwards
            i = (i + 1) % n;
        }

        // Place the next value
        magic[i][j] = k;
    }
}

// Driver code
var magic = Array.from(Array(MAX), ()=> Array(MAX).fill(0));
var n = 3;
if (n % 2 == 1) {
    // Generate the magic square
    magic_square(magic, n);
    // Print the magic square
    print(magic, n);
}

</script>
```

**Output:** 

```
6   1   8
7   5   3 
2   9   4
```

**时间复杂度** : O(北^ 2)。
**辅助空间** : O(北^ 2)。