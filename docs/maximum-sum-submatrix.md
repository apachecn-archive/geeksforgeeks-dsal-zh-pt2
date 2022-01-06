# 最大和子矩阵

> 原文:[https://www.geeksforgeeks.org/maximum-sum-submatrix/](https://www.geeksforgeeks.org/maximum-sum-submatrix/)

**先决条件:** [卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

给定维度为 **N*M** 的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **arr[][]** ，任务是从矩阵 **arr[][]** 中找到最大和子矩阵。

**示例:**

> **输入:** arr[][] = {{0，-2，-7，0 }，{ 9，2，-6，2}，{ -4，1，-4，1}，{ -1，8，0，-2}}
> **输出:** 15
> **解释:**子矩阵{{9，2 }，{-4，1 }，{-1，8}}有一个和 15，这是可能的最大和。
> 
> **输入:** arr[][] = {{1，2}，{-5，-7 } }
> T3】输出: 3

**天真方法:**最简单的方法是[从给定的矩阵](https://www.geeksforgeeks.org/sum-of-all-submatrices-of-a-given-matrix/)生成所有可能的子矩阵，并计算它们的和。最后，打印得到的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum submatrix
void maxSubmatrixSum(
    vector<vector<int> > matrix)
{
    // Stores the number of rows
    // and columns in the matrix
    int r = matrix.size();
    int c = matrix[0].size();

    // Stores maximum submatrix sum
    int maxSubmatrix = 0;

    // Take each row as starting row
    for (int i = 0; i < r; i++) {

        // Take each column as the
        // starting column
        for (int j = 0; j < c; j++) {

            // Take each row as the
            // ending row
            for (int k = i; k < r; k++) {

                // Take each column as
                // the ending column
                for (int l = j; l < c; l++) {

                    // Stores the sum of submatrix
                    // having topleft index(i, j)
                    // and bottom right index (k, l)
                    int sumSubmatrix = 0;

                    // Iterate the submatrix
                    // row-wise and calculate its sum
                    for (int m = i; m <= k; m++) {
                        for (int n = j; n <= l; n++) {
                            sumSubmatrix += matrix[m][n];
                        }
                    }

                    // Update the maximum sum
                    maxSubmatrix
                        = max(maxSubmatrix,
                              sumSubmatrix);
                }
            }
        }
    }

    // Print the answer
    cout << maxSubmatrix;
}

// Driver Code
int main()
{
    vector<vector<int> > matrix = { { 0, -2, -7, 0 },
                                    { 9, 2, -6, 2 },
                                    { -4, 1, -4, 1 },
                                    { -1, 8, 0, -2 } };

    maxSubmatrixSum(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find maximum sum submatrix
static void maxSubmatrixSum(int[][] matrix)
{

    // Stores the number of rows
    // and columns in the matrix
    int r = matrix.length;
    int c = matrix[0].length;

    // Stores maximum submatrix sum
    int maxSubmatrix = 0;

    // Take each row as starting row
    for (int i = 0; i < r; i++) {

        // Take each column as the
        // starting column
        for (int j = 0; j < c; j++) {

            // Take each row as the
            // ending row
            for (int k = i; k < r; k++) {

                // Take each column as
                // the ending column
                for (int l = j; l < c; l++) {

                    // Stores the sum of submatrix
                    // having topleft index(i, j)
                    // and bottom right index (k, l)
                    int sumSubmatrix = 0;

                    // Iterate the submatrix
                    // row-wise and calculate its sum
                    for (int m = i; m <= k; m++) {
                        for (int n = j; n <= l; n++) {
                            sumSubmatrix += matrix[m][n];
                        }
                    }

                    // Update the maximum sum
                    maxSubmatrix
                        = Math.max(maxSubmatrix,
                              sumSubmatrix);
                }
            }
        }
    }

    // Print the answer
    System.out.println(maxSubmatrix);
}

// Driver Code
public static void main(String[] args)
{
    int[][] matrix = { { 0, -2, -7, 0 },
                        { 9, 2, -6, 2 },
                        { -4, 1, -4, 1 },
                        { -1, 8, 0, -2 } };

    maxSubmatrixSum(matrix);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find maximum sum submatrix
def maxSubmatrixSum(matrix):

    # Stores the number of rows
    # and columns in the matrix
    r = len(matrix)
    c = len(matrix[0])

    # Stores maximum submatrix sum
    maxSubmatrix = 0

    # Take each row as starting row
    for i in range(r):

        # Take each column as the
        # starting column
        for j in range(c):

            # Take each row as the
            # ending row
            for k in range(i, r):

                # Take each column as
                # the ending column
                for l in range(j, c):

                    # Stores the sum of submatrix
                    # having topleft index(i, j)
                    # and bottom right index (k, l)
                    sumSubmatrix = 0

                    # Iterate the submatrix
                    # row-wise and calculate its sum
                    for m in range(i, k + 1):
                        for n in range(j, l + 1):
                            sumSubmatrix += matrix[m][n]

                    # Update the maximum sum
                    maxSubmatrix= max(maxSubmatrix, sumSubmatrix)

    # Print the answer
    print (maxSubmatrix)

# Driver Code
if __name__ == '__main__':
    matrix = [ [ 0, -2, -7, 0 ],
                [ 9, 2, -6, 2 ],
                [ -4, 1, -4, 1 ],
                [ -1, 8, 0, -2 ] ]

    maxSubmatrixSum(matrix)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{
// Function to find maximum sum submatrix
static void maxSubmatrixSum(int[,] matrix)
{

    // Stores the number of rows
    // and columns in the matrix
    int r = matrix.GetLength(0);
    int c = matrix.GetLength(1);

    // Stores maximum submatrix sum
    int maxSubmatrix = 0;

    // Take each row as starting row
    for (int i = 0; i < r; i++) {

        // Take each column as the
        // starting column
        for (int j = 0; j < c; j++) {

            // Take each row as the
            // ending row
            for (int k = i; k < r; k++) {

                // Take each column as
                // the ending column
                for (int l = j; l < c; l++) {

                    // Stores the sum of submatrix
                    // having topleft index(i, j)
                    // and bottom right index (k, l)
                    int sumSubmatrix = 0;

                    // Iterate the submatrix
                    // row-wise and calculate its sum
                    for (int m = i; m <= k; m++) {
                        for (int n = j; n <= l; n++) {
                            sumSubmatrix += matrix[m, n];
                        }
                    }

                    // Update the maximum sum
                    maxSubmatrix
                        = Math.Max(maxSubmatrix,
                              sumSubmatrix);
                }
            }
        }
    }

    // Print the answer
    Console.WriteLine(maxSubmatrix);
}

// Driver Code
public static void Main(String []args)
{
    int[,] matrix = { { 0, -2, -7, 0 },
                        { 9, 2, -6, 2 },
                        { -4, 1, -4, 1 },
                        { -1, 8, 0, -2 } };

    maxSubmatrixSum(matrix);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find maximum sum submatrix
    function maxSubmatrixSum(matrix)
    {

        // Stores the number of rows
        // and columns in the matrix
        var r = matrix.length;
        var c = matrix[0].length;

        // Stores maximum submatrix sum
        var maxSubmatrix = 0;

        // Take each row as starting row
        for (i = 0; i < r; i++) {

            // Take each column as the
            // starting column
            for (j = 0; j < c; j++) {

                // Take each row as the
                // ending row
                for (k = i; k < r; k++) {

                    // Take each column as
                    // the ending column
                    for (l = j; l < c; l++) {

                        // Stores the sum of submatrix
                        // having topleft index(i, j)
                        // and bottom right index (k, l)
                        var sumSubmatrix = 0;

                        // Iterate the submatrix
                        // row-wise and calculate its sum
                        for (m = i; m <= k; m++) {
                            for (n = j; n <= l; n++) {
                                sumSubmatrix += matrix[m][n];
                            }
                        }

                        // Update the maximum sum
                        maxSubmatrix = Math.max(maxSubmatrix,
                        sumSubmatrix);
                    }
                }
            }
        }

        // Print the answer
        document.write(maxSubmatrix);
    }

    // Driver Code

        var matrix = [ [ 0, -2, -7, 0 ],
        [ 9, 2, -6, 2 ],
        [ -4, 1, -4, 1 ],
        [ -1, 8, 0, -2 ] ];

        maxSubmatrixSum(matrix);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N<sup>6</sup>)*
***辅助空间:** O(1)*

**使用卡丹算法的有效方法:**上述方法可以使用以下观察值进行优化:

*   固定所需子矩阵的起止列，分别表示**开始**和**结束**。
*   现在，迭代每一行，将从开始到结束列的行总和添加到 **sumSubmatrix** 中，并将其插入数组中。迭代每行后，在这个新创建的数组上执行[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。如果通过应用卡丹算法获得的总和大于总最大总和，则更新总最大总和。
*   在上述步骤中，通过创建一个包含每行前缀和的大小为 **N*M** 的辅助矩阵，可以在恒定时间内计算从开始到结束列的行和。

按照以下步骤解决问题:

*   初始化一个变量，比如说 **maxSum** 为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，来存储最大子阵和。
*   创建一个矩阵**预矩阵【N】【M】**，存储给定矩阵每行的[前缀数组和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   [使用 **i** 作为行索引， **j** 作为列索引，逐行遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，并执行以下步骤:
    *   如果 **i** 的值为 **0** ，则设置**预矩阵【I】【j】= A【I】【j】**。
    *   否则，设置**预矩阵[i][j] =预矩阵[I][j–1]+A[I][j]**。
*   现在，对于范围**【0，M】**内子矩阵列的开始和结束索引的所有可能组合，执行以下步骤:
    *   初始化一个辅助数组 **A[]** ，存储当前子矩阵每行的最大和。
    *   使用**预矩阵**求从开始到结束列的和，如下所示:
        *   如果 **start** 的值为正，则将所需的总和 **S** 存储为**预矩阵[I][end]–预矩阵[I][start–1]**。
        *   否则，将 **S** 更新为**预矩阵【I】【结束】**。
    *   将 **S** 插入一个数组 **arr[]** 。
    *   迭代完子矩阵中的所有行后，在数组**A【】**上执行[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)，并将最大和 **maxSum** 更新为 **maxSum** 的最大值以及在此步骤中执行卡丹算法得到的值。
*   完成以上步骤后，打印 **maxSum** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum continuous
// maximum sum in the array
int kadane(vector<int> v)
{

    // Stores current and maximum sum
    int currSum = 0;
    int maxSum = INT_MIN;

    // Traverse the array v
    for (int i = 0;
         i < (int)v.size(); i++) {

        // Add the value of the
        // current element
        currSum += v[i];

        // Update the maximum sum
        if (currSum > maxSum) {
            maxSum = currSum;
        }

        if (currSum < 0) {
            currSum = 0;
        }
    }

    // Return the maximum sum
    return maxSum;
}

// Function to find the maximum
// submatrix sum
void maxSubmatrixSum(
    vector<vector<int> > A)
{

    // Store the rows and columns
    // of the matrix
    int r = A.size();
    int c = A[0].size();

    // Create an auxiliary matrix
    int** prefix = new int*[r];

    // Traverse the matrix, prefix
    // and initialize it will all 0s
    for (int i = 0; i < r; i++) {

        prefix[i] = new int;
        for (int j = 0; j < c; j++) {
            prefix[i][j] = 0;
        }
    }

    // Calculate prefix sum of all
    // rows of matrix A[][] and
    // store in matrix prefix[]
    for (int i = 0; i < r; i++) {

        for (int j = 0; j < c; j++) {

            // Update the prefix[][]
            if (j == 0)
                prefix[i][j] = A[i][j];
            else
                prefix[i][j] = A[i][j]
                               + prefix[i][j - 1];
        }
    }

    // Store the maximum submatrix sum
    int maxSum = INT_MIN;

    // Iterate for starting column
    for (int i = 0; i < c; i++) {

        // Iterate for last column
        for (int j = i; j < c; j++) {

            // To store current array
            // elements
            vector<int> v;

            // Traverse every row
            for (int k = 0; k < r; k++) {

                // Store the sum of the
                // kth row
                int el = 0;

                // Update the prefix
                // sum
                if (i == 0)
                    el = prefix[k][j];
                else
                    el = prefix[k][j]
                         - prefix[k][i - 1];

                // Push it in a vector
                v.push_back(el);
            }

            // Update the maximum
            // overall sum
            maxSum = max(maxSum, kadane(v));
        }
    }

    // Print the answer
    cout << maxSum << "\n";
}

// Driver Code
int main()
{
    vector<vector<int> > matrix = { { 0, -2, -7, 0 },
                                    { 9, 2, -6, 2 },
                                    { -4, 1, -4, 1 },
                                    { -1, 8, 0, -2 } };

    // Function Call
    maxSubmatrixSum(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to find maximum continuous
  // maximum sum in the array
  static int kadane(Vector<Integer> v)
  {

    // Stores current and maximum sum
    int currSum = 0;
    int maxSum = Integer.MIN_VALUE;

    // Traverse the array v
    for (int i = 0;
         i < (int)v.size(); i++)
    {

      // Add the value of the
      // current element
      currSum += v.get(i);

      // Update the maximum sum
      if (currSum > maxSum)
      {
        maxSum = currSum;
      }

      if (currSum < 0)
      {
        currSum = 0;
      }
    }

    // Return the maximum sum
    return maxSum;
  }

  // Function to find the maximum
  // submatrix sum
  static void maxSubmatrixSum(int [][]A)
  {
    // Store the rows and columns
    // of the matrix
    int r = A.length;
    int c = A[0].length;

    // Create an auxiliary matrix
    int [][]prefix = new int[r][];

    // Traverse the matrix, prefix
    // and initialize it will all 0s
    for (int i = 0; i < r; i++) {

      prefix[i] = new int;
      for (int j = 0; j < c; j++) {
        prefix[i][j] = 0;
      }
    }

    // Calculate prefix sum of all
    // rows of matrix A[][] and
    // store in matrix prefix[]
    for (int i = 0; i < r; i++) {

      for (int j = 0; j < c; j++) {

        // Update the prefix[][]
        if (j == 0)
          prefix[i][j] = A[i][j];
        else
          prefix[i][j] = A[i][j]
          + prefix[i][j - 1];
      }
    }

    // Store the maximum submatrix sum
    int maxSum = Integer.MIN_VALUE;

    // Iterate for starting column
    for (int i = 0; i < c; i++) {

      // Iterate for last column
      for (int j = i; j < c; j++) {

        // To store current array
        // elements
        Vector<Integer> v = new Vector<Integer>();

        // Traverse every row
        for (int k = 0; k < r; k++) {

          // Store the sum of the
          // kth row
          int el = 0;

          // Update the prefix
          // sum
          if (i == 0)
            el = prefix[k][j];
          else
            el = prefix[k][j]
            - prefix[k][i - 1];

          // Push it in a vector
          v.add(el);
        }

        // Update the maximum
        // overall sum
        maxSum = Math.max(maxSum, kadane(v));
      }
    }

    // Print the answer
    System.out.print(maxSum+ "\n");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int [][]matrix = { { 0, -2, -7, 0 },
                      { 9, 2, -6, 2 },
                      { -4, 1, -4, 1 },
                      { -1, 8, 0, -2 } };

    // Function Call
    maxSubmatrixSum(matrix);
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find maximum continuous
# maximum sum in the array
def kadane(v):

    # Stores current and maximum sum
    currSum = 0

    maxSum = -sys.maxsize - 1

    # Traverse the array v
    for i in range(len(v)):

        # Add the value of the
        # current element
        currSum += v[i]

        # Update the maximum sum
        if (currSum > maxSum):
            maxSum = currSum
        if (currSum < 0):
            currSum = 0

    # Return the maximum sum
    return maxSum

# Function to find the maximum
# submatrix sum
def maxSubmatrixSum(A):

    # Store the rows and columns
    # of the matrix
    r = len(A)
    c = len(A[0])

    # Create an auxiliary matrix
    # Traverse the matrix, prefix
    # and initialize it will all 0s
    prefix = [[0 for i in range(c)]
                 for j in range(r)]

    # Calculate prefix sum of all
    # rows of matrix A[][] and
    # store in matrix prefix[]
    for i in range(r):
        for j in range(c):

            # Update the prefix[][]
            if (j == 0):
                prefix[i][j] = A[i][j]
            else:
                prefix[i][j] = A[i][j] + prefix[i][j - 1]

    # Store the maximum submatrix sum
    maxSum = -sys.maxsize - 1

    #  Iterate for starting column
    for i in range(c):

        # Iterate for last column
        for j in range(i, c):

            # To store current array
            # elements
            v = []

            # Traverse every row
            for k in range(r):

                # Store the sum of the
                # kth row
                el = 0

                # Update the prefix
                # sum
                if (i == 0):
                    el = prefix[k][j]
                else:
                    el = prefix[k][j] - prefix[k][i - 1]

                # Push it in a vector
                v.append(el)

            # Update the maximum
            # overall sum
            maxSum = max(maxSum, kadane(v))

    # Print the answer
    print(maxSum)

# Driver Code
matrix = [ [ 0, -2, -7, 0 ],
           [ 9, 2, -6, 2 ],
           [ -4, 1, -4, 1 ],
           [ -1, 8, 0, -2 ] ]

# Function Call
maxSubmatrixSum(matrix)

# This code is contributed by rag2127
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

  // Function to find maximum continuous
  // maximum sum in the array
  static int kadane(List<int> v)
  {

    // Stores current and maximum sum
    int currSum = 0;
    int maxSum = int.MinValue;

    // Traverse the array v
    for (int i = 0;
         i < (int)v.Count; i++)
    {

      // Add the value of the
      // current element
      currSum += v[i];

      // Update the maximum sum
      if (currSum > maxSum)
      {
        maxSum = currSum;
      }

      if (currSum < 0)
      {
        currSum = 0;
      }
    }

    // Return the maximum sum
    return maxSum;
  }

  // Function to find the maximum
  // submatrix sum
  static void maxSubmatrixSum(int [,]A)
  {
    // Store the rows and columns
    // of the matrix
    int r = A.GetLength(0);
    int c = A.GetLength(1);

    // Create an auxiliary matrix
    int [,]prefix = new int[r,c];

    // Traverse the matrix, prefix
    // and initialize it will all 0s
    for (int i = 0; i < r; i++) {
      for (int j = 0; j < c; j++) {
        prefix[i,j] = 0;
      }
    }

    // Calculate prefix sum of all
    // rows of matrix [,]A and
    // store in matrix prefix[]
    for (int i = 0; i < r; i++) {

      for (int j = 0; j < c; j++) {

        // Update the prefix[,]
        if (j == 0)
          prefix[i,j] = A[i,j];
        else
          prefix[i,j] = A[i,j]
          + prefix[i,j - 1];
      }
    }

    // Store the maximum submatrix sum
    int maxSum = int.MinValue;

    // Iterate for starting column
    for (int i = 0; i < c; i++) {

      // Iterate for last column
      for (int j = i; j < c; j++) {

        // To store current array
        // elements
        List<int> v = new List<int>();

        // Traverse every row
        for (int k = 0; k < r; k++) {

          // Store the sum of the
          // kth row
          int el = 0;

          // Update the prefix
          // sum
          if (i == 0)
            el = prefix[k,j];
          else
            el = prefix[k,j]
            - prefix[k,i - 1];

          // Push it in a vector
          v.Add(el);
        }

        // Update the maximum
        // overall sum
        maxSum = Math.Max(maxSum, kadane(v));
      }
    }

    // Print the answer
    Console.Write(maxSum+ "\n");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int [,]matrix = { { 0, -2, -7, 0 },
                      { 9, 2, -6, 2 },
                      { -4, 1, -4, 1 },
                      { -1, 8, 0, -2 } };

    // Function Call
    maxSubmatrixSum(matrix);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find maximum continuous
// maximum sum in the array   
function kadane(v)
{
    // Stores current and maximum sum
    let currSum = 0;
    let maxSum = Number.MIN_VALUE;

    // Traverse the array v
    for (let i = 0;
         i < v.length; i++)
    {

      // Add the value of the
      // current element
      currSum += v[i];

      // Update the maximum sum
      if (currSum > maxSum)
      {
        maxSum = currSum;
      }

      if (currSum < 0)
      {
        currSum = 0;
      }
    }

    // Return the maximum sum
    return maxSum;
}

// Function to find the maximum
// submatrix sum
function maxSubmatrixSum(A)
{
    // Store the rows and columns
    // of the matrix
    let r = A.length;
    let c = A[0].length;

    // Create an auxiliary matrix
    let prefix = new Array(r);

    // Traverse the matrix, prefix
    // and initialize it will all 0s
    for (let i = 0; i < r; i++) {

      prefix[i] = new Array(c);
      for (let j = 0; j < c; j++) {
        prefix[i][j] = 0;
      }
    }

    // Calculate prefix sum of all
    // rows of matrix A[][] and
    // store in matrix prefix[]
    for (let i = 0; i < r; i++) {

      for (let j = 0; j < c; j++) {

        // Update the prefix[][]
        if (j == 0)
          prefix[i][j] = A[i][j];
        else
          prefix[i][j] = A[i][j]
          + prefix[i][j - 1];
      }
    }

    // Store the maximum submatrix sum
    let maxSum = Number.MIN_VALUE;

    // Iterate for starting column
    for (let i = 0; i < c; i++) {

      // Iterate for last column
      for (let j = i; j < c; j++) {

        // To store current array
        // elements
        let v = [];

        // Traverse every row
        for (let k = 0; k < r; k++) {

          // Store the sum of the
          // kth row
          let el = 0;

          // Update the prefix
          // sum
          if (i == 0)
            el = prefix[k][j];
          else
            el = prefix[k][j]
            - prefix[k][i - 1];

          // Push it in a vector
          v.push(el);
        }

        // Update the maximum
        // overall sum
        maxSum = Math.max(maxSum, kadane(v));
      }
    }

    // Print the answer
    document.write(maxSum+ "<br>");
}

// Driver Code
let matrix=[[ 0, -2, -7, 0 ],
                      [ 9, 2, -6, 2 ],
                      [ -4, 1, -4, 1 ],
                      [ -1, 8, 0, -2 ]];
// Function Call
maxSubmatrixSum(matrix);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*