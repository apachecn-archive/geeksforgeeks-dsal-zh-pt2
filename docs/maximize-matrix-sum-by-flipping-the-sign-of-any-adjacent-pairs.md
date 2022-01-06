# 通过翻转任何相邻对的符号最大化矩阵和

> 原文:[https://www . geesforgeks . org/通过翻转任意相邻对的符号来最大化矩阵和/](https://www.geeksforgeeks.org/maximize-matrix-sum-by-flipping-the-sign-of-any-adjacent-pairs/)

给定一个维度为 **N*N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】**，任务是通过任意次翻转相邻元素的符号来找到矩阵元素的最大和。

**示例:**

> **输入:** mat[][] = [[2，-2]，[-2，2]]
> **输出:** 8
> **解释:**
> 按照以下步骤求矩阵的最大和为:
> 
> 1.  翻转相邻元素的符号(arr[0][0]，arr[0][1])会将矩阵修改为 mat[][] = {{-2，2}，{-2，2}}。
> 2.  翻转相邻元素的符号(arr[0][0]，arr[1][0])会将矩阵修改为 mat[][] = {{2，2}，{2，2}}。
> 
> 现在，矩阵元素的总和是 8，这是所有可能的相邻矩阵元素翻转中的最大值。
> 
> **输入:** mat[][] = [[1，2，3]，[-1，-2，-3]，[1，2，3]]
> **输出:** 16

**方法:**给定的问题可以通过观察这样一个事实来解决:如果矩阵中有一个**偶数个负数**，那么所有这些元素都可以转化为正元素，得到最大和。否则，除了一个负元素外，所有矩阵元素都可以翻转**。按照以下步骤解决问题:**

*   求所有矩阵元素的绝对值之和，存储在一个变量中，比如 **S** 。
*   找到具有最小绝对值的矩阵元素，并将其存储在一个变量中，比如 **minElement** 。
*   如果给定矩阵 **mat[][]** 中的负元素数为偶数，则打印最大和为 **S** 。否则，通过排除总和中的最小元素，将**(S–2 * minElement)**的值打印为结果总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// matrix element after flipping the
// signs of adjacent matrix elements
int maxSum(vector<vector<int> >& matrix)
{

    // Initialize row and column
    int r = matrix.size();
    int c = matrix[0].size();

    // Stores the sum of absolute
    // matrix element
    int sum = 0;

    // Find the minimum absolute value
    // in the matrix
    int mini = INT_MAX;

    // Store count of negatives
    int count = 0;

    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            int k = matrix[i][j];

            // Find the smallest absolute
            // value in the matrix
            mini = min(mini, abs(k));

            // Increment the count of
            // negative numbers
            if (k < 0)
                count++;

            // Find the absolute sum
            sum += abs(k);
        }
    }

    // If the count of negatives is
    // even then print the sum
    if (count % 2 == 0) {
        return sum;
    }

    // Subtract minimum absolute
    // element
    else {
        return (sum - 2 * mini);
    }
}

// Driver Code
int main()
{
    vector<vector<int> > matrix
        = { { 2, -2 }, { -2, 2 } };
    cout << maxSum(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum sum of
    // matrix element after flipping the
    // signs of adjacent matrix elements
    static int maxSum(int[][] matrix)
    {

        // Initialize row and column
        int r = matrix.length;
        int c = matrix[0].length;

        // Stores the sum of absolute
        // matrix element
        int sum = 0;

        // Find the minimum absolute value
        // in the matrix
        int mini = Integer.MAX_VALUE;

        // Store count of negatives
        int count = 0;

        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                int k = matrix[i][j];

                // Find the smallest absolute
                // value in the matrix
                mini = Math.min(mini, Math.abs(k));

                // Increment the count of
                // negative numbers
                if (k < 0)
                    count++;

                // Find the absolute sum
                sum += Math.abs(k);
            }
        }

        // If the count of negatives is
        // even then print the sum
        if (count % 2 == 0) {
            return sum;
        }

        // Subtract minimum absolute
        // element
        else {
            return (sum - 2 * mini);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] matrix = { { 2, -2 }, { -2, 2 } };
        System.out.print(maxSum(matrix));
    }
}

// This code is contributed by subham348.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function to find the maximum sum of
# matrix element after flipping the
# signs of adjacent matrix elements
def maxSum(matrix):
    # Initialize row and column
    r = len(matrix)
    c = len(matrix[0])

    # Stores the sum of absolute
    # matrix element
    sum = 0

    # Find the minimum absolute value
    # in the matrix
    mini = sys.maxsize

    # Store count of negatives
    count = 0

    for i in range(r):
        for j in range(c):
            k = matrix[i][j]

            # Find the smallest absolute
            # value in the matrix
            mini = min(mini, abs(k))

            # Increment the count of
            # negative numbers
            if (k < 0):
                count += 1

            # Find the absolute sum
            sum += abs(k)

    # If the count of negatives is
    # even then print the sum
    if (count % 2 == 0):
        return sum

    # Subtract minimum absolute
    # element
    else:
        return (sum - 2 * mini)

# Driver Code
if __name__ == '__main__':
    matrix = [[2, -2],[-2, 2]]
    print(maxSum(matrix))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find the maximum sum of
    // matrix element after flipping the
    // signs of adjacent matrix elements
    static int maxSum(int[,] matrix)
    {

        // Initialize row and column
        int r = matrix.GetLength(0);
        int c = matrix.GetLength(1);

        // Stores the sum of absolute
        // matrix element
        int sum = 0;

        // Find the minimum absolute value
        // in the matrix
        int mini = int.MaxValue;

        // Store count of negatives
        int count = 0;

        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                int k = matrix[i,j];

                // Find the smallest absolute
                // value in the matrix
                mini = Math.Min(mini, Math.Abs(k));

                // Increment the count of
                // negative numbers
                if (k < 0)
                    count++;

                // Find the absolute sum
                sum += Math.Abs(k);
            }
        }

        // If the count of negatives is
        // even then print the sum
        if (count % 2 == 0) {
            return sum;
        }

        // Subtract minimum absolute
        // element
        else {
            return (sum - 2 * mini);
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[,] matrix = { { 2, -2 }, { -2, 2 } };
        Console.Write(maxSum(matrix));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the maximum sum of
        // matrix element after flipping the
        // signs of adjacent matrix elements
        function maxSum(matrix) {

            // Initialize row and column
            let r = matrix.length;
            let c = matrix[0].length;

            // Stores the sum of absolute
            // matrix element
            let sum = 0;

            // Find the minimum absolute value
            // in the matrix
            let mini = Number.MAX_VALUE;

            // Store count of negatives
            let count = 0;

            for (let i = 0; i < r; i++) {
                for (let j = 0; j < c; j++) {
                    let k = matrix[i][j];

                    // Find the smallest absolute
                    // value in the matrix
                    mini = Math.min(mini, Math.abs(k));

                    // Increment the count of
                    // negative numbers
                    if (k < 0)
                        count++;

                    // Find the absolute sum
                    sum += Math.abs(k);
                }
            }

            // If the count of negatives is
            // even then print the sum
            if (count % 2 == 0) {
                return sum;
            }

            // Subtract minimum absolute
            // element
            else {
                return (sum - 2 * mini);
            }
        }

        // Driver Code
        let matrix
            = [[2, -2], [-2, 2]];
        document.write(maxSum(matrix));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*