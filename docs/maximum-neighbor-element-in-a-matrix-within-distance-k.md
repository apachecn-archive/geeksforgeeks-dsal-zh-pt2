# 距离为 K 的矩阵中最大相邻元素

> 原文:[https://www . geeksforgeeks . org/距离内矩阵元素最大邻居-k/](https://www.geeksforgeeks.org/maximum-neighbor-element-in-a-matrix-within-distance-k/)

给定一个矩阵 **mat[][]** 和一个整数 **K** ，任务是为矩阵的每个元素找到绝对距离为 K 的最大邻居。
换句话说，对于每个矩阵[i][j]求最大矩阵[p][q]，使得 ABS(I-p)+ABS(j-q)≤k。
**示例:**

> **输入:** mat[][] = {{1，2}，{4，5}}，K = 1
> **输出:** {{4，5}，{5，5}}
> **解释:**
> 元素 mat[0][0] = 4(距离= 1)
> 元素 mat[0][1] = 5(距离= 1)
> 元素 mat[1][0] = 5(距离= 1)的最大邻居 {4，5，6}，{7，8，9}}，K = 2
> **输出:** {{7，8，9}，{8，9，9}，{9，9，9}}

**方法:**思路是从 1 到 **K** 循环迭代，从距离小于或等于 K 的邻居中选择元素，每次迭代矩阵，找到矩阵每个元素的最大相邻元素。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// maximum neighbor element within
// the distance of less than K

#include <bits/stdc++.h>

using namespace std;

// Function to print the matrix
void printMatrix(vector<vector<int> > A)
{
    // Loop to iterate over the matrix
    for (int i = 0; i < A.size(); i++) {
        for (int j = 0; j < A[0].size(); j++)
            cout << A[i][j] << ' ';
        cout << '\n';
    }
}

// Function to find the maximum
// neighbor within the distance
// of less than equal to K
vector<vector<int> > getMaxNeighbour(
        vector<vector<int> >& A, int K)
{
    vector<vector<int> > ans = A;

    // Loop to find the maximum
    // element within the distance
    // of less than K
    for (int q = 1; q <= K; q++) {
        for (int i = 0; i < A.size(); i++) {
            for (int j = 0; j < A[0].size(); j++) {
                int maxi = ans[i][j];
                if (i > 0)
                    maxi = max(
                        maxi, ans[i - 1][j]);
                if (j > 0)
                    maxi = max(
                        maxi, ans[i][j - 1]);
                if (i < A.size() - 1)
                    maxi = max(
                        maxi, ans[i + 1][j]);
                if (j < A[0].size() - 1)
                    maxi = max(
                        maxi, ans[i][j + 1]);
                A[i][j] = maxi;
            }
        }
        ans = A;
    }
    return ans;
}

// Driver Code
int main()
{
    vector<vector<int> > B = { { 1, 2, 3 },
                  { 4, 5, 6 }, { 7, 8, 9 } };
    printMatrix(getMaxNeighbour(B, 2));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum neighbor element within
// the distance of less than K
import java.util.*;

class GFG {

    // Function to print the matrix
    static void printMatrix(int[][] A)
    {

        // Loop to iterate over the matrix
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < A[0].length; j++)
                System.out.print(A[i][j] + " ");
            System.out.print('\n');
        }
    }

    // Function to copy content of one matrix into another
    static void copyMatrix(int[][] A, int[][] B)
    {
        int row = B.length;
        int col = B[0].length;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                A[i][j] = B[i][j];
            }
        }
    }

    // Function to find the maximum
    // neighbor within the distance
    // of less than equal to K
    static int[][] getMaxNeighbour(int[][] A, int K)
    {
        int[][] ans = new int[A.length][A[0].length];
        copyMatrix(ans, A);

        // Loop to find the maximum
        // element within the distance
        // of less than K
        for (int q = 1; q <= K; q++) {
            for (int i = 0; i < A.length; i++) {
                for (int j = 0; j < A[0].length; j++) {
                    int maxi = ans[i][j];
                    if (i > 0)
                        maxi
                            = Math.max(maxi, ans[i - 1][j]);
                    if (j > 0)
                        maxi
                            = Math.max(maxi, ans[i][j - 1]);
                    if (i < A.length - 1)
                        maxi
                            = Math.max(maxi, ans[i + 1][j]);
                    if (j < A[0].length - 1)
                        maxi
                            = Math.max(maxi, ans[i][j + 1]);
                    A[i][j] = maxi;
                }
            }
            copyMatrix(ans, A);
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] B
            = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

        printMatrix(getMaxNeighbour(B, 2));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum neighbor element within
# the distance of less than K

# Function to print the matrix
def printMatrix(A):

    # Loop to iterate over the matrix
    for i in range(len(A)):
        for j in range(len(A[0])):
            print(A[i][j], end = ' ')
        print()

# Function to find the maximum
# neighbor within the distance
# of less than equal to K
def getMaxNeighbour( A, K ):

    ans = A;

    # Loop to find the maximum
    # element within the distance
    # of less than K
    for q in range(1, K + 1):
        for i in range(len(A)):
            for j in range(len(A[0])):

                maxi = ans[i][j];

                if (i > 0):
                    maxi = max(maxi, ans[i - 1][j]);
                if (j > 0):
                    maxi = max(maxi, ans[i][j - 1]);

                if (i < len(A) - 1):
                    maxi = max(maxi, ans[i + 1][j]);

                if (j < len(A[0]) - 1):
                    maxi = max(maxi, ans[i][j + 1]);

                A[i][j] = maxi;

        ans = A;

    return ans;

# Driver Code
if __name__=='__main__':

    B = [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]
    printMatrix(getMaxNeighbour(B, 2));

# This code is contributed by ruttvik_56
```

## C#

```
// C# implementation to find the
// maximum neighbor element within
// the distance of less than K
using System;

class GFG{

// Function to print the matrix
static void printMatrix(int [,] A)
{

    // Loop to iterate over the matrix
    for(int i = 0; i < A.GetLength(0); i++)
    {
       for(int j = 0; j < A.GetLength(1); j++)
          Console.Write(A[i, j] + " ");
       Console.Write('\n');
    }
}

// Function to find the maximum
// neighbor within the distance
// of less than equal to K
static int [,] getMaxNeighbour(int [,] A,
                               int K)
{
    int [,] ans = A;

    // Loop to find the maximum
    // element within the distance
    // of less than K
    for(int q = 1; q <= K; q++)
    {
       for(int i = 0; i < A.GetLength(0); i++)
       {
          for(int j = 0; j < A.GetLength(1); j++)
          {
             int maxi = ans[i, j];
             if (i > 0)
                 maxi = Math.Max(maxi,
                                 ans[i - 1, j]);
             if (j > 0)
                 maxi = Math.Max(maxi,
                                 ans[i, j - 1]);
             if (i < A.GetLength(0) - 1)
                 maxi = Math.Max(maxi,
                                 ans[i + 1, j]);
             if (j < A.GetLength(0) - 1)
                 maxi = Math.Max(maxi,
                                 ans[i, j + 1]);
             A[i, j] = maxi;
          }
       }
       ans = A;
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int [,] B = { { 1, 2, 3 },
                  { 4, 5, 6 },
                  { 7, 8, 9 } };

    printMatrix(getMaxNeighbour(B, 2));
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
7 8 9 
8 9 9 
9 9 9
```

**时间复杂度:**O(M * N * K)
T3】空间复杂度: O(M*N)