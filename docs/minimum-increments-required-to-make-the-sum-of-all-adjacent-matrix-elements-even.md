# 使所有相邻矩阵元素之和相等所需的最小增量

> 原文:[https://www . geesforgeks . org/最小增量-求所有相邻矩阵元素之和-偶数/](https://www.geeksforgeeks.org/minimum-increments-required-to-make-the-sum-of-all-adjacent-matrix-elements-even/)

给定尺寸为 **N × M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**，任务是最小化使相邻矩阵元素之和相等所需的矩阵元素增量数。
**注:**对于任何矩阵元素 **mat[i][j]，**考虑**mat[I–1][j]、mat[i+1][j]、mat[I][j–1]**和 **mat[i][j + 1]** 作为其相邻元素。

**示例:**

> **输入:** mat[][] = {{1，5，6}，{4，7，8}，{2，2，3}}
> **输出:** 4
> **说明:**
> 将单元格 mat[0][0]增加 1，mat[1][1]增加 1，mat[0][1]增加 1，mat[2][2]增加 1。
> 因此，所需的增量总数为 4。因此，修改后的矩阵是{{2，6，6}，{4，8，8}，{2，2，4}}所有相邻元素之和为偶数。
> 
> **输入:** mat[][] = {{1，5，5}，{5，5，5}，{5，1，1}}
> **输出:** 0

**方法:**解决给定问题的思路是基于两个元素之和为**偶数**只有当两个数都为**偶数**或**奇数**时。因此，对于相邻元素之和为偶数的矩阵，所有矩阵元素应具有相同的奇偶性，即要么全部**奇数**要么全部**偶数**。

因此，所需的最小增量数是给定矩阵中**偶数**和**奇数**元素的[计数的最小值。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int MAX = 500;

// Function to find the minimum number
// of increments required to make sum of
// al adjacent matrix elements even
int minOperations(int mat[][MAX], int N)
{
    // Stores the count of odd elements
    int oddCount = 0;

    // Stores the count of even elements
    int evenCount = 0;

    // Iterate the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {

            // If element is odd
            if (mat[i][j] & 1) {

                // Increment odd count
                oddCount++;
            }

            // Otherwise
            else {

                // Increment even count
                evenCount++;
            }
        }
    }

    // Print the minimum of both counts
    cout << min(oddCount, evenCount);
}

// Driver Code
int main()
{
    int mat[][MAX]
        = { { 1, 5, 6 }, { 4, 7, 8 }, { 2, 2, 3 } };
    int N = sizeof(mat) / sizeof(mat[0]);

    minOperations(mat, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

static int MAX = 500;

// Function to find the minimum number
// of increments required to make sum of
// al adjacent matrix elements even
static void minOperations(int mat[][], int N)
{

    // Stores the count of odd elements
    int oddCount = 0;

    // Stores the count of even elements
    int evenCount = 0;

    // Iterate the matrix
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {

            // If element is odd
            if (mat[i][j] % 2== 1) {

                // Increment odd count
                oddCount++;
            }

            // Otherwise
            else {

                // Increment even count
                evenCount++;
            }
        }
    }

    // Print the minimum of both counts
    System.out.print(Math.min(oddCount, evenCount));
}

// Driver Code
public static void main(String[] args)
{
    int mat[][]
        = { { 1, 5, 6 }, { 4, 7, 8 }, { 2, 2, 3 } };
    int N = mat.length;
    minOperations(mat, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
MAX = 500

# Function to find the minimum number
# of increments required to make sum of
# al adjacent matrix elements even
def minOperations(mat, N):

    # Stores the count of odd elements
    oddCount = 0

    # Stores the count of even elements
    evenCount = 0

    # Iterate the matrix
    for i in range(N):
        for j in range(N):

            # If element is odd
            if (mat[i][j] & 1):

                # Increment odd count
                oddCount += 1

            # Otherwise
            else:

                # Increment even count
                evenCount += 1

    # Print the minimum of both counts
    print(min(oddCount, evenCount))

# Driver Code
if __name__ == '__main__':
    mat =  [[1, 5, 6], [4, 7, 8], [2, 2, 3]]
    N = len(mat)

    minOperations(mat, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
  const int MAX = 500;

  // Function to find the minimum number
  // of increments required to make sum of
  // al adjacent matrix elements even
  static void minOperations(int[, ] mat, int N)
  {
    // Stores the count of odd elements
    int oddCount = 0;

    // Stores the count of even elements
    int evenCount = 0;

    // Iterate the matrix
    for (int i = 0; i < N; i++) {
      for (int j = 0; j < N; j++) {

        // If element is odd
        if ((mat[i, j] & 1) != 0) {

          // Increment odd count
          oddCount++;
        }

        // Otherwise
        else {

          // Increment even count
          evenCount++;
        }
      }
    }

    // Print the minimum of both counts
    Console.Write(Math.Min(oddCount, evenCount));
  }

  // Driver Code
  public static void Main()
  {
    int[, ] mat
      = { { 1, 5, 6 }, { 4, 7, 8 }, { 2, 2, 3 } };
    int N = mat.GetLength(0);
    minOperations(mat, N);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
// Java script  program for the above approach

let MAX = 500;

// Function to find the minimum number
// of increments required to make sum of
// al adjacent matrix elements even
function  minOperations(mat,  N)
{

    // Stores the count of odd elements
    let oddCount = 0;

    // Stores the count of even elements
    let evenCount = 0;

    // Iterate the matrix
    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < N; j++)
        {

            // If element is odd
            if (mat[i][j] % 2== 1) {

                // Increment odd count
                oddCount++;
            }

            // Otherwise
            else {

                // Increment even count
                evenCount++;
            }
        }
    }

    // Print the minimum of both counts
    document.write(Math.min(oddCount, evenCount));
}

// Driver Code

    let mat= [ [ 1, 5, 6 ], [ 4, 7, 8 ], [ 2, 2, 3 ] ];
    let N = mat.length;
    minOperations(mat, N);

//contributed by bobby

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*