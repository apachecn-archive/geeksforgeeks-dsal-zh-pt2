# 计数总和超过剩余矩阵总和的行

> 原文:[https://www . geeksforgeeks . org/计数-总和超过剩余总和的行数-矩阵/](https://www.geeksforgeeks.org/count-rows-with-sum-exceeding-sum-of-the-remaining-matrix/)

给定维度为 **N * M** 的矩阵 **mat[][]** ，任务是计算其总和超过矩阵剩余元素总和的行数。

**示例:**

> **输入:** mat[][] = {{1，5}，{2，3}}
> **输出:** 1
> **说明:**
> 第一行{1，5}元素之和超过剩余矩阵{2，3}之和。
> 
> **输入:** mat[][] = {{2，-1，5}，{-3，0，-2}，{5，1，2 } }
> T3】输出: 2

**方法:**解决问题的思路是预先计算给定矩阵元素的总和，对于每一行，检查当前行的元素总和是否大于矩阵其余部分的元素总和，即***curr sum>(total sum–curr sum)。*** 对于满足上述条件的每一行，增加 ***计数*** 。最后，打印完成矩阵遍历后得到的 ***计数*** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;
#define N 3
#define M 3

// Function to count the number of rows
// whose sum exceeds the sum of
// elements of the remaining matrix
 void countRows(int mat[M][N])
{
   // To store the result
   int count = 0;

   // Stores the total sum of
   // the matrix elements
   int totalSum = 0;

   // Calculate the total sum
   for (int i = 0; i < N; i++)
   {
     for (int j = 0; j < M; j++)
     {
       totalSum += mat[i][j];
     }
   }

   // Traverse to check for each row
   for (int i = 0; i < N; i++)
   {
     // Stores the sum of elements
     // of the current row
     int currSum = 0;

     // Calculate the sum of elements
     // of the current row
     for (int j = 0; j < M; j++)
     {
       currSum += mat[i][j];
     }

     // If sum of current row exceeds
     // the sum of rest of the matrix
     if (currSum > totalSum - currSum)

       // Increase count
       count++;
   }

   // Print the result
   cout << count;
}

// Driver Code
int main()
{
  // Given matrix
  int mat[N][M] = {{2, -1, 5},
                   {-3, 0, -2},
                   {5, 1, 2}};

  // Function Call
  countRows(mat);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to count the number of rows
    // whose sum exceeds the sum of
    // elements of the remaining matrix
    static void countRows(int[][] mat)
    {
        // Stores the matrix dimensions
        int n = mat.length;
        int m = mat[0].length;

        // To store the result
        int count = 0;

        // Stores the total sum of
        // the matrix elements
        int totalSum = 0;

        // Calculate the total sum
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                totalSum += mat[i][j];
            }
        }

        // Traverse to check for each row
        for (int i = 0; i < n; i++) {

            // Stores the sum of elements
            // of the current row
            int currSum = 0;

            // Calculate the sum of elements
            // of the current row
            for (int j = 0; j < m; j++) {
                currSum += mat[i][j];
            }

            // If sum of current row exceeds
            // the sum of rest of the matrix
            if (currSum > totalSum - currSum)

                // Increase count
                count++;
        }

        // Print the result
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given matrix
        int[][] mat
            = { { 2, -1, 5 },
                { -3, 0, -2 },
                { 5, 1, 2 } };

        // Function Call
        countRows(mat);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number of rows
# whose sum exceeds the sum of elements
# of the remaining matrix
def countRows(mat):

    # Stores the matrix dimensions
    n = len(mat)
    m = len(mat[0])

    # To store the result
    count = 0

    # Stores the total sum of
    # the matrix elements
    totalSum = 0

    # Calculate the total sum
    for i in range(n):
        for j in range(m):
            totalSum += mat[i][j]

    # Traverse to check for each row
    for i in range(n):

        # Stores the sum of elements
        # of the current row
        currSum = 0

        # Calculate the sum of elements
        # of the current row
        for j in range(m):
            currSum += mat[i][j]

        # If sum of current row exceeds
        # the sum of rest of the matrix
        if (currSum > totalSum - currSum):

            # Increase count
            count += 1

    # Print the result
    print(count)

# Driver Code
if __name__ == '__main__':

    # Given matrix
    mat = [ [ 2, -1, 5 ],
            [ -3, 0, -2 ],
            [ 5, 1, 2 ] ]

    # Function call
    countRows(mat)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to count the number of rows
// whose sum exceeds the sum of
// elements of the remaining matrix
static void countRows(int[,] mat)
{
  // Stores the matrix dimensions
  int n = mat.GetLength(0);
  int m = mat.GetLength(1);

  // To store the result
  int count = 0;

  // Stores the total sum of
  // the matrix elements
  int totalSum = 0;

  // Calculate the total sum
  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < m; j++)
    {
      totalSum += mat[i, j];
    }
  }

  // Traverse to check for each row
  for (int i = 0; i < n; i++)
  {
    // Stores the sum of elements
    // of the current row
    int currSum = 0;

    // Calculate the sum of elements
    // of the current row
    for (int j = 0; j < m; j++)
    {
      currSum += mat[i, j];
    }

    // If sum of current row exceeds
    // the sum of rest of the matrix
    if (currSum > totalSum - currSum)

      // Increase count
      count++;
  }

  // Print the result
  Console.WriteLine(count);
}

// Driver Code
public static void Main(String[] args)
{
  // Given matrix
  int[,] mat = {{2, -1, 5},
                {-3, 0, -2},
                {5, 1, 2}};

  // Function Call
  countRows(mat);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach
var N = 3
var M = 3

// Function to count the number of rows
// whose sum exceeds the sum of
// elements of the remaining matrix
function countRows( mat)
{
   // To store the result
   var count = 0;

   // Stores the total sum of
   // the matrix elements
   var totalSum = 0;

   // Calculate the total sum
   for (var i = 0; i < N; i++)
   {
     for (var j = 0; j < M; j++)
     {
       totalSum += mat[i][j];
     }
   }

   // Traverse to check for each row
   for (var i = 0; i < N; i++)
   {
     // Stores the sum of elements
     // of the current row
     var currSum = 0;

     // Calculate the sum of elements
     // of the current row
     for (var j = 0; j < M; j++)
     {
       currSum += mat[i][j];
     }

     // If sum of current row exceeds
     // the sum of rest of the matrix
     if (currSum > totalSum - currSum)

       // Increase count
       count++;
   }

   // Print the result
   document.write( count);
}

// Driver Code
// Given matrix
var mat = [[2, -1, 5],
                 [-3, 0, -2],
                 [5, 1, 2]];

// Function Call
countRows(mat);

// This code is contributed by itsok.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*