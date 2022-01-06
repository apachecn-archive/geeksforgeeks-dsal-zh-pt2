# 通过将相邻元素对重复乘以-1

来最大化矩阵和

> 原文:[https://www . geesforgeks . org/maximum-matrix-sum-by-reply-乘-对-neighborgeks-1/](https://www.geeksforgeeks.org/maximize-matrix-sum-by-repeatedly-multiplying-pairs-of-adjacent-elements-with-1/)

给定维度为 **M × N** 的[矩阵](https://www.geeksforgeeks.org/category/data-structures/matrix/) **A[][]** ，任务是通过重复选择两个相邻的矩阵元素并将它们的值乘以 **-1 来从矩阵中找到最大可能和。**

**示例:**

> **输入:** A[ ][ ] = {{4，-8，6}，{3，7，2}}
> **输出:** 26
> **解释:**
> *将 mat[0][1]和 mat[0][2]乘以-1。矩阵修改为 A[][] = {{4，8，-6}，{3，7，2}}。*
> *将 mat[0][2]和 mat[1][2]乘以-1。矩阵修改为 A[][] = {{4，8，6}，{3，7，-2}}。*
> 因此，矩阵的和= 26，这是可能的最大和。
> 
> **输入:** A[ ][ ] = {{2，9，-5}，{6，1，3}，{-7，4，8}}
> **输出:** 45
> **解释:**
> *将 mat[0][2]和 mat[1][2]乘以-1。矩阵修改为 A[][] =* {{2，9，5}，{6，1，-3}，{-7，4，8}} *。*
> *将 mat[1][1]和 mat[1][2]乘以-1。矩阵修改为 A[][] =* {{2，9，5}，{6，-1，3}，{-7，4，8}} *。*
> *将 mat[1][1]和 mat[2][1]乘以-1。矩阵修改为 A[][] =* {{2，9，5}，{6，1，3}，{-7，-4，8}} *。*
> *将 mat[2][0]和 mat[2][1]乘以-1。矩阵修改为 A[][] =* {{2，9，5}，{6，1，3}，{7，4，8}} *。*
> 因此，矩阵的和= 45，这是可能的最大和。

**方法:**为了最大化给定矩阵的和，执行给定的操作，使得行或列中的最小元素为负(如果不可能使所有行和列元素都为正)。按照以下步骤最大化总和:

*   让具有负值的单元数量为 **x** 。**如果 x 为 0** ，即没有负值，那么矩阵的和已经是最大可能。
*   否则，从矩阵中获取任何负值，并对该元素及其任何相邻单元格执行给定的操作。这导致所选元素变为正。
*   如果选择的相邻元素的值是负的，那么它将变成正的，反之亦然。这样，在每一轮中，两个负值可以变成正值。现在出现了以下两种情况:
    *   **如果 x 为偶数:**在这种情况下， **x/2** 转完之后，所有的负值都可以变成正值。因此，最大可能和等于**所有细胞绝对值的和。**
    *   **如果 x 是奇数:**在这种情况下，以上述方式执行操作后，将剩下一个负值。现在，为了最大化总和，需要最小化被减去的值或具有负号的值。为此，将负号移动到具有最小绝对值的单元格，例如 **minVal** 。因此，最大可能总和是所有单元格绝对值的**总和–2 * minVal**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum sum
// possible of a matrix by multiplying
// pairs of adjacent elements with -1
// any number of times (possibly zero)
void getMaxSum(vector<vector<int> > A,
               int M, int N)
{
    // Store the maximum sum
    // of matrix possible
    int sum = 0;

    // Stores the count of
    // negative values in the matrix
    int negative = 0;

    // Store minimum absolute
    // value present in the matrix
    int minVal = INT_MAX;

    // Traverse the matrix row-wise
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // Update sum
            sum += abs(A[i][j]);

            // If current element is negative,
            // increment the negative count
            if (A[i][j] < 0) {
                negative++;
            }

            // If current value is less than
            // the overall minimum in A[],
            // update the overall minimum
            minVal = min(minVal, abs(A[i][j]));
        }
    }

    // If there are odd number of negative
    // values, then the answer will be
    // sum of the absolute values of
    // all elements - 2* minVal
    if (negative % 2) {
        sum -= 2 * minVal;
    }

    // Print maximum sum
    cout << sum;
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > A = {
        { 4, -8, 6 },
        { 3, 7, 2 }
    };

    // Dimensions of matrix
    int M = A.size();
    int N = A[0].size();

    getMaxSum(A, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
class GFG
{
  static void getMaxSum(int[][] A, int M, int N)
  {

    // Store the maximum sum
    // of matrix possible
    int sum = 0;

    // Stores the count of
    // negative values in the matrix
    int negative = 0;

    // Store minimum absolute
    // value present in the matrix
    int minVal = Integer.MAX_VALUE;

    // Traverse the matrix row-wise
    for (int i = 0; i < M; i++) {
      for (int j = 0; j < N; j++) {

        // Update sum
        sum += Math.abs(A[i][j]);

        // If current element is negative,
        // increment the negative count
        if (A[i][j] < 0) {
          negative++;
        }

        // If current value is less than
        // the overall minimum in A[],
        // update the overall minimum
        minVal
          = Math.min(minVal, Math.abs(A[i][j]));
      }
    }

    // If there are odd number of negative
    // values, then the answer will be
    // sum of the absolute values of
    // all elements - 2* minVal
    if (negative % 2 != 0) {
      sum -= 2 * minVal;
    }

    // Print maximum sum
    System.out.println(sum);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given matrix
    int[][] A = { { 4, -8, 6 }, { 3, 7, 2 } };

    // Dimensions of matrix
    int M = A.length;
    int N = A[0].length;

    getMaxSum(A, M, N);
  }
}

// This code is contributed by aditya7409.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to calculate maximum sum
# possible of a matrix by multiplying
# pairs of adjacent elements with -1
# any number of times (possibly zero)
def getMaxSum(A, M, N):

    # Store the maximum sum
    # of matrix possible
    sum = 0

    # Stores the count of
    # negative values in the matrix
    negative = 0

    # Store minimum absolute
    # value present in the matrix
    minVal = sys.maxsize

    # Traverse the matrix row-wise
    for i in range(M):
        for j in range(N):
            # Update sum
            sum += abs(A[i][j])

            # If current element is negative,
            # increment the negative count
            if (A[i][j] < 0):
                negative +=1

            # If current value is less than
            # the overall minimum in A[],
            # update the overall minimum
            minVal = min(minVal, abs(A[i][j]))

    # If there are odd number of negative
    # values, then the answer will be
    # sum of the absolute values of
    # all elements - 2* minVal
    if (negative % 2):
        sum -= 2 * minVal

    # Print maximum sum
    print(sum)

# Driver Code
if __name__ == '__main__':

    # Given matrix
    A = [[4, -8, 6], [3, 7, 2]]

    # Dimensions of matrix
    M = len(A)
    N = len(A[0])
    getMaxSum(A, M, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate maximum sum
// possible of a matrix by multiplying
// pairs of adjacent elements with -1
// any number of times (possibly zero)
static void getMaxSum(int[,] A, int M, int N)
{

    // Store the maximum sum
    // of matrix possible
    int sum = 0;

    // Stores the count of
    // negative values in the matrix
    int negative = 0;

    // Store minimum absolute
    // value present in the matrix
    int minVal = Int32.MaxValue;

    // Traverse the matrix row-wise
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Update sum
            sum += Math.Abs(A[i, j]);

            // If current element is negative,
            // increment the negative count
            if (A[i, j] < 0)
            {
                negative++;
            }

            // If current value is less than
            // the overall minimum in A[],
            // update the overall minimum
            minVal = Math.Min(minVal,
                              Math.Abs(A[i, j]));
        }
    }

    // If there are odd number of negative
    // values, then the answer will be
    // sum of the absolute values of
    // all elements - 2* minVal
    if (negative % 2 != 0)
    {
        sum -= 2 * minVal;
    }

    // Print maximum sum
    Console.Write(sum);
}

// Driver Code
public static void Main()
{

    // Given matrix
    int[, ] A = { { 4, -8, 6 },
                  { 3, 7, 2 } };

    // Dimensions of matrix
    int M = A.GetLength(0);
    int N = A.GetLength(1);

    getMaxSum(A, M, N);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
//java script code
function getMaxSum(A,M,N)
{

    // Store the maximum sum
    // of matrix possible
    let sum = 0;

    // Stores the count of
    // negative values in the matrix
    let negative = 0;

    // Store minimum absolute
    // value present in the matrix
    let minVal = Number.MAX_VALUE;

    // Traverse the matrix row-wise
    for (let i = 0; i < M; i++) {
    for (let j = 0; j < N; j++) {

        // Update sum
        sum += Math.abs(A[i][j]);

        // If current element is negative,
        // increment the negative count
        if (A[i][j] < 0) {
        negative++;
        }

        // If current value is less than
        // the overall minimum in A[],
        // update the overall minimum
        minVal
        = Math.min(minVal, Math.abs(A[i][j]));
    }
    }

    // If there are odd number of negative
    // values, then the answer will be
    // sum of the absolute values of
    // all elements - 2* minVal
    if (negative % 2 != 0) {
    sum -= 2 * minVal;
    }

    // Print maximum sum
    document.write(sum);
}

// Driver Code

    // Given matrix
    let A = [[4, -8, 6 ], [ 3, 7, 2 ]];

    // Dimensions of matrix
    let M = A.length;
    let N = A[0].length;

    getMaxSum(A, M, N);

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
26
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(1)*