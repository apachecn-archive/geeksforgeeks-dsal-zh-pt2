# 通过翻转大小为 K 的子矩阵将二进制矩阵 A 转换为 B 的最小操作

> 原文:[https://www . geeksforgeeks . org/通过翻转大小为 k 的子矩阵将最小运算转换为二进制矩阵 a 到 b/](https://www.geeksforgeeks.org/minimum-operations-to-convert-binary-matrix-a-to-b-by-flipping-submatrix-of-size-k/)

给定两个维数为 **N * M** 的二进制矩阵 **A[]** 和 **B[]** 以及一个正整数 **K** ，任务是找到矩阵 **A[][]** 中所需的大小为 **K** 的子矩阵的最小翻转次数，将其转化为矩阵 **B[][]** 。如果无法转换，则打印**-1”**。

**示例**:

> **输入:**A[][]= { '1 '，' 1 '，' 1' }，{ '1 '，' 1 '，' 1' }，{ ' 1 '，' 1 '，' 1' } }，B[][]= { '0 '，' 0 '，' 0 '，' 0' }，{ ' 0 '，' 0' }，K = 3
> **输出:** 1
> **解释:**
> 以下是执行的操作:
> **操作 1:**
> 因此，所需的最小翻转次数为 1 次。
> 
> **输入:** A[][] = { { '1 '，' 0 '，' 0' }，{ '0 '，' 0 '，' 0' }，{ '0 '，' 0 '，' 0' } }，B[][]= { '0 '，' 0 '，' 0 '，' 0' }，{ ' 0 '，' 0' } }，K = 3
> **输出** : -1

**逼近**:给定的问题可以使用[贪婪逼近](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，思路是[遍历给定的矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/) **A[][]** 和 **B[][]** ，如果对应的单元格 **(i，j)** 具有不同的值，则从索引 **(i，j)** 和**中翻转当前大小为 **K** 的子矩阵，计算翻转**的操作遍历给定矩阵后，如果有任何索引使得大小为 **K** 的子矩阵无法翻转，则打印**-1”**，因为无法将矩阵 **A[][]** 转换为 **B[][]** 。否则，打印获得的操作计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the operations
// required  to convert matrix A to B
int minMoves(vector<vector<char>> a,
             vector<vector<char>> b,
             int K)
{
    // Store the sizes of matrix
    int n = a.size(), m = a[0].size();

      // Stores count of flips required
    int cntOperations = 0;

    // Traverse the given matrix
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < m; j++) {

            // Check if the matrix values
              // are not equal
            if (a[i][j] != b[i][j]) {

                // Increment the count
                  // of moves
                cntOperations++;

                // Check if the current
                  // square sized exists
                  // or not
                if (i + K - 1 >= n
                    || j + K - 1 >= m) {
                    return -1;
                }

                // Flip all the bits in this
                // square sized submatrix
                for (int p = 0;
                     p <= K - 1; p++) {
                    for (int q = 0;
                         q <= K - 1; q++) {

                        if (a[i + p][j + q] == '0') {
                            a[i + p][j + q] = '1';
                        }
                        else {
                            a[i + p][j + q] = '0';
                        }
                    }
                }
            }
        }
    }

    // Count of operations required
    return cntOperations;
}

// Driver Code
int main()
{
    vector<vector<char> > A = { { '1', '0', '0' },
                                { '0', '0', '0' },
                                { '0', '0', '0' } };
    vector<vector<char> > B = { { '0', '0', '0' },
                                { '0', '0', '0' },
                                { '0', '0', '0' } };
    int K = 3;

    cout << minMoves(A, B, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to count the operations
    // required  to convert matrix A to B
    static int minMoves(char a[][],char b[][], int K)
    {

        // Store the sizes of matrix
        int n = a.length;
        int m = a[0].length;

          // Stores count of flips required
        int cntOperations = 0;

        // Traverse the given matrix
        for (int i = 0; i < n; i++) {

            for (int j = 0; j < m; j++) {

                // Check if the matrix values
                  // are not equal
                if (a[i][j] != b[i][j]) {

                    // Increment the count
                      // of moves
                    cntOperations++;

                    // Check if the current
                      // square sized exists
                      // or not
                    if (i + K - 1 >= n
                        || j + K - 1 >= m) {
                        return -1;
                    }

                    // Flip all the bits in this
                    // square sized submatrix
                    for (int p = 0;
                         p <= K - 1; p++) {
                        for (int q = 0;
                             q <= K - 1; q++) {

                            if (a[i + p][j + q] == '0') {
                                a[i + p][j + q] = '1';
                            }
                            else {
                                a[i + p][j + q] = '0';
                            }
                        }
                    }
                }
            }
        }

        // Count of operations required
        return cntOperations;
    }

    // Driver Code
    public static void main (String[] args)
    {
        char A[][] = { { '1', '0', '0' },
                                    { '0', '0', '0' },
                                    { '0', '0', '0' } };
        char B[][] = { { '0', '0', '0' },
                                    { '0', '0', '0' },
                                    { '0', '0', '0' } };
        int K = 3;
        System.out.println(minMoves(A, B, K));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Function to count the operations
# required to convert matrix A to B
def minMoves(a, b, K):

        # Store the sizes of matrix
    n = len(a)
    m = len(a[0])

    # Stores count of flips required
    cntOperations = 0

    # Traverse the given matrix
    for i in range(0, n):

        for j in range(0, m):

                        # Check if the matrix values
                        # are not equal
            if (a[i][j] != b[i][j]):

                                # Increment the count
                                # of moves
                cntOperations += 1

                # Check if the current
                # square sized exists
                # or not
                if (i + K - 1 >= n or j + K - 1 >= m):
                    return -1

                    # Flip all the bits in this
                    # square sized submatrix
                for p in range(0, K):
                    for q in range(0, K):

                        if (a[i + p][j + q] == '0'):
                            a[i + p][j + q] = '1'

                        else:
                            a[i + p][j + q] = '0'

        # Count of operations required
    return cntOperations

# Driver Code
if __name__ == "__main__":

    A = [['1', '0', '0'], ['0', '0', '0'], ['0', '0', '0']]
    B = [['0', '0', '0'], ['0', '0', '0'], ['0', '0', '0']]
    K = 3
    print(minMoves(A, B, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count the operations
  // required  to convert matrix A to B
  static int minMoves(char[,] a, char[,] b, int K)
  {

    // Store the sizes of matrix
    int n = a.Length;
    int m = a.GetLength(0);

    // Stores count of flips required
    int cntOperations = 0;

    // Traverse the given matrix
    for (int i = 0; i < n; i++)
    {

      for (int j = 0; j < m; j++)
      {

        // Check if the matrix values
        // are not equal
        if (a[i, j] != b[i, j])
        {

          // Increment the count
          // of moves
          cntOperations++;

          // Check if the current
          // square sized exists
          // or not
          if (i + K - 1 >= n
              || j + K - 1 >= m)
          {
            return -1;
          }

          // Flip all the bits in this
          // square sized submatrix
          for (int p = 0;
               p <= K - 1; p++)
          {
            for (int q = 0;
                 q <= K - 1; q++)
            {

              if (a[i + p, j + q] == '0')
              {
                a[i + p, j + q] = '1';
              }
              else
              {
                a[i + p, j + q] = '0';
              }
            }
          }
        }
      }
    }

    // Count of operations required
    return cntOperations;
  }

  // Driver Code
  public static void Main()
  {
    char[,] A = new char[,]{ { '1', '0', '0' },
                            { '0', '0', '0' },
                            { '0', '0', '0' } };
    char[,] B = new char[,]{ { '0', '0', '0' },
                            { '0', '0', '0' },
                            { '0', '0', '0' } };
    int K = 3;
    Console.WriteLine(minMoves(A, B, K));
  }
}

// This code is contributed by Saurabh.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to count the operations
        // required  to convert matrix A to B
        function minMoves(a, b, K)
        {

            // Store the sizes of matrix
            let n = a.length, m = a[0].length;

            // Stores count of flips required
            let cntOperations = 0;

            // Traverse the given matrix
            for (let i = 0; i < n; i++) {

                for (let j = 0; j < m; j++) {

                    // Check if the matrix values
                    // are not equal
                    if (a[i][j] != b[i][j]) {

                        // Increment the count
                        // of moves
                        cntOperations++;

                        // Check if the current
                        // square sized exists
                        // or not
                        if (i + K - 1 >= n
                            || j + K - 1 >= m) {
                            return -1;
                        }

                        // Flip all the bits in this
                        // square sized submatrix
                        for (let p = 0;
                            p <= K - 1; p++) {
                            for (let q = 0;
                                q <= K - 1; q++) {

                                if (a[i + p][j + q] == '0') {
                                    a[i + p][j + q] = '1';
                                }
                                else {
                                    a[i + p][j + q] = '0';
                                }
                            }
                        }
                    }
                }
            }

            // Count of operations required
            return cntOperations;
        }

        // Driver Code
        let A = [['1', '0', '0'],
        ['0', '0', '0'],
        ['0', '0', '0']];
        let B = [['0', '0', '0'],
        ['0', '0', '0'],
        ['0', '0', '0']];
        let K = 3;

        document.write(minMoves(A, B, K));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
-1
```

***时间复杂度:**O(N * M * K<sup>2</sup>)*
***辅助空间:** O(1)*