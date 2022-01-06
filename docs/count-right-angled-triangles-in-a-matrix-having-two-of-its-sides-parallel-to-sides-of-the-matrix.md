# 计算一个矩阵中直角三角形的个数，该矩阵的两个边平行于矩阵的边

> 原文:[https://www . geesforgeks . org/count-矩阵中直角三角形的两个边平行于矩阵的边/](https://www.geeksforgeeks.org/count-right-angled-triangles-in-a-matrix-having-two-of-its-sides-parallel-to-sides-of-the-matrix/)

给定尺寸为 **N * M** 的二元[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，任务是计算[直角三角形](https://www.geeksforgeeks.org/dividing-the-rectangle-into-n-right-angled-triangles/)的数量，该直角三角形可以通过连接包含值 **1** 的单元格而形成，使得三角形的任意两条边必须平行于矩形的边。

**示例:**

> **输入:** arr[][] = {{0，1，0}，{1，1，1}，{0，1，0}}
> **输出:** 4
> **说明:**可以形成的直角三角形有(a[1][1]，a[1][0]，a[0][1])，(a[1][1]，a[2][1]，a[1][0])，(a[1][1]，a[1][1]，a[1][2]，a[0]
> 
> **输入:** arr[][] = {{1，0，1，0}，{0，1，1，1}，{1，0，1，0}，{0，1，0，1}}
> **输出:** 16

**方法:**想法是[遍历给定的网格](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)并将每行和每列中存在的 **1** 的计数分别存储在辅助数组**行【】**和**列【】**中。那么对于网格**中的每个单元格【arr】[]**，如果**arr【I】【j】**为 **1** ，那么对于每个单元格**(行[I]–1)*(列[j]–1)**就可以计算出形成直角三角形的总数。按照以下步骤解决问题:

*   用 **0** 初始化数组 **col[]** 和 **row[]** 。
*   [遍历给定的网格](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)并访问每个单元格**arr【I】【j】**。
*   如果 **arr[i][j]** 为 **1** ，则将**行【I】**和**列【j】**增加 **1** 。
*   遍历网格后，用 **0** 初始化变量**和**。
*   再次遍历整个网格，现在，如果 **arr[i][j]** 是 **1** ，那么通过以下方式更新直角三角形的计数:

> **(行[I]–1)*(列[j]–1)**

*   遍历后，将**和**的值打印为直角三角形的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the right-angled
// triangle in the given grid a[][]
int numberOfTriangle(
    vector<vector<int> >& a)
{
    int N = a.size();
    int M = a[0].size();

    // Stores the count of 1s for
    // each row[] and column[]
    int rows[N] = { 0 };
    int columns[M] = { 0 };

    // Find the number of 1s in
    // each of the rows[0, N - 1]
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < M; ++j) {

            // Increment row[i]
            if (a[i][j] == 1) {
                rows[i]++;
            }
        }
    }

    // Find the number of 1s in
    // each of the columns[0, N - 1]
    for (int i = 0; i < M; ++i) {

        for (int j = 0; j < N; ++j) {

            // Increment columns[i]
            if (a[j][i] == 1) {
                columns[i]++;
            }
        }
    }

    // Stores the count of triangles
    int answer = 0;

    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < M; ++j) {

            // If current cell has value 1
            if (a[i][j] == 1) {

                // Update the answer
                answer += (rows[i] - 1)
                          * (columns[j] - 1);
            }
        }

    }
   // Return the count
        return answer;
}

// Driver Code
int main()
{
    // Given grid arr[][]
    vector<vector<int> > arr;

    arr = { { 1, 0, 1, 0 },
            { 0, 1, 1, 1 },
            { 1, 0, 1, 0 },
            { 0, 1, 0, 1 } };

    // Function Call
    cout << numberOfTriangle(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to count the right-angled
// triangle in the given grid a[][]
static int numberOfTriangle(int[][] a)
{
  int N = a.length;
  int M = a[0].length;

  // Stores the count of 1s for
  // each row[] and column[]
  int []rows = new int[N];
  int []columns = new int[M];

  // Find the number of 1s in
  // each of the rows[0, N - 1]
  for (int i = 0; i < N; ++i)
  {
    for (int j = 0; j < M; ++j)
    {
      // Increment row[i]
      if (a[i][j] == 1)
      {
        rows[i]++;
      }
    }
  }

  // Find the number of 1s in
  // each of the columns[0, N - 1]
  for (int i = 0; i < M; ++i)
  {
    for (int j = 0; j < N; ++j)
    {
      // Increment columns[i]
      if (a[j][i] == 1)
      {
        columns[i]++;
      }
    }
  }

  // Stores the count
  // of triangles
  int answer = 0;

  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < M; ++j)
    {
      // If current cell
      // has value 1
      if (a[i][j] == 1)
      {
        // Update the answer
        answer += (rows[i] - 1) *
                  (columns[j] - 1);
      }
    }
  }

  // Return the count
  return answer;
}

// Driver Code
public static void main(String[] args)
{
  // Given grid arr[][]
  int [][]arr = {{1, 0, 1, 0},
                 {0, 1, 1, 1},
                 {1, 0, 1, 0},
                 {0, 1, 0, 1}};

  // Function Call
  System.out.print(numberOfTriangle(arr));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the right-angled
# triangle in the given grid a[][]
def numberOfTriangle(a):

    N = len(a)
    M = len(a[0])

    # Stores the count of 1s for
    # each row[] and column[]
    rows = [0] * N
    columns = [0] * M

    # Find the number of 1s in
    # each of the rows[0, N - 1]
    for i in range(N):
        for j in range(M):

            # Increment row[i]
            if (a[i][j] == 1):
                rows[i] += 1

    # Find the number of 1s in
    # each of the columns[0, N - 1]
    for i in range(M):
        for j in range(N):

            # Increment columns[i]
            if (a[j][i] == 1):
                columns[i] += 1

    # Stores the count of triangles
    answer = 0

    for i in range(N):
        for j in range(M):

            # If current cell has value 1
            if (a[i][j] == 1):

                # Update the answer
                answer += ((rows[i] - 1) *
                      (columns[j] - 1))

    # Return the count
    return answer

# Driver Code
if __name__ == '__main__':

    # Given grid arr
    arr = [ [ 1, 0, 1, 0 ],
            [ 0, 1, 1, 1 ],
            [ 1, 0, 1, 0 ],
            [ 0, 1, 0, 1 ] ]

    # Function call
    print(numberOfTriangle(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to count the right-angled
// triangle in the given grid[,]a
static int numberOfTriangle(int[,] a)
{
  int N = a.GetLength(0);
  int M = a.GetLength(1);

  // Stores the count of 1s for
  // each []row and column[]
  int []rows = new int[N];
  int []columns = new int[M];

  // Find the number of 1s in
  // each of the rows[0, N - 1]
  for(int i = 0; i < N; ++i)
  {
    for(int j = 0; j < M; ++j)
    {

      // Increment row[i]
      if (a[i, j] == 1)
      {
        rows[i]++;
      }
    }
  }

  // Find the number of 1s in
  // each of the columns[0, N - 1]
  for(int i = 0; i < M; ++i)
  {
    for(int j = 0; j < N; ++j)
    {

      // Increment columns[i]
      if (a[j, i] == 1)
      {
        columns[i]++;
      }
    }
  }

  // Stores the count
  // of triangles
  int answer = 0;

  for(int i = 0; i < N; i++)
  {
    for(int j = 0; j < M; ++j)
    {

      // If current cell
      // has value 1
      if (a[i, j] == 1)
      {

        // Update the answer
        answer += (rows[i] - 1) *
               (columns[j] - 1);
      }
    }
  }

  // Return the count
  return answer;
}

// Driver Code
public static void Main(String[] args)
{

  // Given grid [,]arr
  int [,]arr = { { 1, 0, 1, 0 },
                 { 0, 1, 1, 1 },
                 { 1, 0, 1, 0 },
                 { 0, 1, 0, 1 } };

  // Function Call
  Console.Write(numberOfTriangle(arr));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach
// Function to count the right-angled
// triangle in the given grid a
function numberOfTriangle(a)
{
  var N = a.length;
  var M = a[0].length;

  // Stores the count of 1s for
  // each row and column
  var rows = Array.from({length: N}, (_, i) => 0);
  var columns = Array.from({length: M}, (_, i) => 0);

  // Find the number of 1s in
  // each of the rows[0, N - 1]
  for (i = 0; i < N; ++i)
  {
    for (j = 0; j < M; ++j)
    {
      // Increment row[i]
      if (a[i][j] == 1)
      {
        rows[i]++;
      }
    }
  }

  // Find the number of 1s in
  // each of the columns[0, N - 1]
  for (i = 0; i < M; ++i)
  {
    for (j = 0; j < N; ++j)
    {
      // Increment columns[i]
      if (a[j][i] == 1)
      {
        columns[i]++;
      }
    }
  }

  // Stores the count
  // of triangles
  var answer = 0;

  for (i = 0; i < N; i++)
  {
    for (j = 0; j < M; ++j)
    {
      // If current cell
      // has value 1
      if (a[i][j] == 1)
      {
        // Update the answer
        answer += (rows[i] - 1) *
                  (columns[j] - 1);
      }
    }
  }

  // Return the count
  return answer;
}

// Driver Code

  // Given grid arr
  var arr = [[1, 0, 1, 0],
                 [0, 1, 1, 1],
                 [1, 0, 1, 0],
                 [0, 1, 0, 1]];

  // Function Call
  document.write(numberOfTriangle(arr));

// This code contributed by shikhasingrajput

</script>
```

**Output**

```
16
```

***时间复杂度:** O(N*M)，其中 NxM 是给定网格的维数。*
***空间复杂度:** O(N*M)*