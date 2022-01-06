# 统计幸存者人数

> 原文:[https://www . geeksforgeeks . org/count-幸存者人数/](https://www.geeksforgeeks.org/count-the-number-of-survivors/)

给定包含字符**【1–9】**、 **P** 和 ***** 的矩阵 **mat[][]** ，其中 **P** 是一个人， ***** 是一个空格。当前单元格中的整数表示炸弹，它可以摧毁半径等于单元格值的物体。任务是统计和打印爆炸中幸存的人数。
**示例:**

```
Input: 
mat[] = { "P***", 
          "****", 
          "2**P", 
          "****" }
Output: 1
Only the person in the third row 
will survive. Note that the person 
in the first row is within the 
radius of the bomb.

Input:
mat[] = { "2***P*", 
          "P*****", 
          "******", 
          "**1***", 
          "******", 
          "*****P" }
Output: 2
The persons in the first and last
row survive.
```

**方法:**逐个字符遍历矩阵字符，如果当前字符是**数字(1–9)**，则将半径内的所有周围元素改为 ***** (在所有八个方向上)，表示该半径内无人生还。遍历完矩阵的所有元素后，计算指示一个人的单元格数，即 **mat[i][j] = 'P'** 。最后打印**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count of
// the people that survived
int countSurvivors(string mat[], int row, int col)
{
    int i, j, count = 0;

    for (i = 0; i < row; i++) {
        for (j = 0; j < col; j++) {

            // If current cell is a bomb
            if (mat[i][j] > '0' && mat[i][j] <= '9') {
                int radius = mat[i][j] - '0';

                // Coordinates of the sub-matrix
                // that will be affected by the blast
                int iMin = max(i - radius, 0);
                int iMax = min(i + radius, row - 1);
                int jMin = max(j - radius, 0);
                int jMax = min(j + radius, col - 1);

                for (int k = iMin; k <= iMax; k++)
                    for (int l = jMin; l <= jMax; l++)

                        // Set the current cell to
                        //  empty space without a person
                        mat[k][l] = '*';
            }
        }
    }

    // Count the remaining persons
    for (i = 0; i < row; i++)
        for (j = 0; j < col; j++)
            if (mat[i][j] == 'P')
                count++;

    return count;
}

// Driver Code
int main()
{
    // Input matrix
    string mat[] = { "P***", "****", "2**P", "****" };

    // Rows and columns of the matrix
    int row = sizeof(mat) / sizeof(mat[0]);
    int col = mat[0].length();

    // Total people survived
    cout << countSurvivors(mat, row, col);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// the people that survived
static int countSurvivors(String mat[], int row, int col)
    {
        int i, j, count = 0;

        for (i = 0; i < row; i++)
        {
            for (j = 0; j < col; j++)
            {

                // If current cell is a bomb
                if (mat[i].charAt(j) > '0' && mat[i].charAt(j) <= '9')
                {
                    int radius = mat[i].charAt(j) - '0';

                    // Coordinates of the sub-matrix
                    // that will be affected by the blast
                    int iMin = Math.max(i - radius, 0);
                    int iMax = Math.min(i + radius, row - 1);
                    int jMin = Math.max(j - radius, 0);
                    int jMax = Math.min(j + radius, col - 1);

                    for (int k = iMin; k <= iMax; k++)
                    {

                        // convert string nto character array
                        char C [] = mat[k].toCharArray();

                        for (int l = jMin; l <= jMax; l++)
                        {
                            // Set the current cell to
                            // empty space without a person
                            C [l] = '*' ;
                        }
                        // convert character array back into the string
                        String s = new String(C) ;
                        mat[k] = s ;
                    }
                }
            }
        }

        // Count the remaining persons
        for (i = 0; i < row; i++)
            for (j = 0; j < col; j++)
                if (mat[i].charAt(j) == 'P')
                    count++;

        return count;
    }

    // Driver Code
    public static void main(String []args)
    {
        // Input matrix
        String mat[] = { "P***", "****", "2**P", "****" };

        // Rows and columns of the matrix
        int row = mat.length ;
        int col = mat[0].length();

        // Total people survived
        System.out.println(countSurvivors(mat, row, col));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function to return the count of
# the people that survived
def countSurvivors(mat, row, col):

    i, j, count = 0, 0, 0

    for i in range(row):
        for j in range(col):

            # If current cell is a bomb
            if (mat[i][j] > '0' and mat[i][j] <= '9'):
                radius = ord(mat[i][j]) - ord('0')

                # Coordinates of the sub-matrix
                # that will be affected by the blast
                iMin = max(i - radius, 0)
                iMax = min(i + radius, row - 1)
                jMin = max(j - radius, 0)
                jMax = min(j + radius, col - 1)

                for k in range(iMin, iMax + 1):
                    for l in range(jMin, jMax + 1):

                        # Set the current cell to
                        # empty space without a person
                        mat[k][l] = '*'

    # Count the remaining persons
    for i in range(row):
        for j in range(col):
            if (mat[i][j] == 'P'):
                count += 1

    return count

# Driver Code

# Input matrix
mat = [["P", "*", "*", "*"],
       ["*", "*", "*", "*"],
       ["2", "*", "*", "P"],
       ["*", "*", "*", "*"]]

# Rows and columns of the matrix
row = len(mat)
col = len(mat[0])

# Total people survived
print(countSurvivors(mat, row, col))

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count of
// the people that survived
static int countSurvivors(String []mat,
                          int row, int col)
{
    int i, j, count = 0;

    for (i = 0; i < row; i++)
    {
        for (j = 0; j < col; j++)
        {

            // If current cell is a bomb
            if (mat[i][j] > '0' && mat[i][j] <= '9')
            {
                int radius = mat[i][j] - '0';

                // Coordinates of the sub-matrix
                // that will be affected by the blast
                int iMin = Math.Max(i - radius, 0);
                int iMax = Math.Min(i + radius, row - 1);
                int jMin = Math.Max(j - radius, 0);
                int jMax = Math.Min(j + radius, col - 1);

                for (int k = iMin; k <= iMax; k++)
                {

                    // convert string nto character array
                    char []C = mat[k].ToCharArray();

                    for (int l = jMin; l <= jMax; l++)
                    {
                        // Set the current cell to
                        // empty space without a person
                        C [l] = '*';
                    }
                    // convert character array back into the string
                    String s = new String(C);
                    mat[k] = s;
                }
            }
        }
    }

    // Count the remaining persons
    for (i = 0; i < row; i++)
        for (j = 0; j < col; j++)
            if (mat[i][j] == 'P')
                count++;

    return count;
}

// Driver Code
public static void Main(String []args)
{
    // Input matrix
    String []mat = { "P***", "****",
                     "2**P", "****" };

    // Rows and columns of the matrix
    int row = mat.Length ;
    int col = mat[0].Length;

    // Total people survived
    Console.WriteLine(countSurvivors(mat, row, col));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the count of
    // the people that survived
    function countSurvivors(mat, row, col)
    {
        let i, j, count = 0;

        for (i = 0; i < row; i++)
        {
            for (j = 0; j < col; j++)
            {

                // If current cell is a bomb
                if (mat[i][j].charCodeAt() > '0'.charCodeAt() &&
                mat[i][j].charCodeAt() <= '9'.charCodeAt())
                {
                    let radius = mat[i][j].charCodeAt() -
                    '0'.charCodeAt();

                    // Coordinates of the sub-matrix
                    // that will be affected by the blast
                    let iMin = Math.max(i - radius, 0);
                    let iMax = Math.min(i + radius, row - 1);
                    let jMin = Math.max(j - radius, 0);
                    let jMax = Math.min(j + radius, col - 1);

                    for (let k = iMin; k <= iMax; k++)
                    {

                        // convert string nto character array
                        let C = mat[k].split('');

                        for (let l = jMin; l <= jMax; l++)
                        {
                            // Set the current cell to
                            // empty space without a person
                            C[l] = '*' ;
                        }
                        // convert character array
                        // back into the string
                        let s = C.join("");
                        mat[k] = s ;
                    }
                }
            }
        }

        // Count the remaining persons
        for (i = 0; i < row; i++)
            for (j = 0; j < col; j++)
                if (mat[i][j] == 'P')
                    count++;

        return count;
    }

      // Input matrix
    let mat = [ "P***", "****", "2**P", "****" ];

    // Rows and columns of the matrix
    let row = mat.length;
    let col = mat[0].length;

    // Total people survived
    document.write(countSurvivors(mat, row, col));

</script>
```

**Output:** 

```
1
```