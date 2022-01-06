# 通过将相邻细胞对重复乘以-1

来最大化矩阵的乘积

> 原文:[https://www . geeksforgeeks . org/通过将相邻单元对与-1 重复相乘来最大化矩阵乘积/](https://www.geeksforgeeks.org/maximize-product-of-a-matrix-by-repeatedly-multiplying-pairs-of-adjacent-cells-with-1/)

给定一个由整数组成的维 **NxN** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**，任务是找出矩阵**mat【】【】**元素的最大[乘积，可能是相邻单元格对重复乘以 **-1** 。
***注意:**任意矩阵元素的值最多可以通过 **-1** 改变一次。*](https://www.geeksforgeeks.org/a-product-array-puzzle/)

**示例:**

> **输入:** arr[][] = {{1，-2}，{2，-3}}
> **输出:** 12
> **解释:**
> 将 arr[0][1]和 arr[1][1]乘以-1。因此，矩阵的乘积= = 1 * 2 * 2 * 3 = 12。
> 
> **输入:** arr[][] = {{2，2}，{-3，1 } }；
> T3【输出: 216

**方法:**给定的问题可以基于以下观察来解决:

*   如果矩阵中负数的[计数为偶数，矩阵](https://www.geeksforgeeks.org/count-negative-numbers-in-a-column-wise-row-wise-sorted-matrix/)中 **0s** 的[计数为 **1** ，则将该 **0** 改为 **1** ，然后打印矩阵中所有元素的乘积作为结果。否则，打印 **0** 作为结果。](https://www.geeksforgeeks.org/count-zeros-in-a-row-wise-and-column-wise-sorted-matrix/)
*   否则，将最小绝对值改为 **1** ，然后打印矩阵中所有元素的乘积作为结果。

按照以下步骤解决问题:

*   通过[遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)**mat【】【】**求给定矩阵中负数的个数(说**数**)和 **0s** (说**零**)。
*   如果**计数**为偶数，**为零**为 **1** ，则打印矩阵中除 **0** 以外的所有数字的乘积。
*   否则[求矩阵](https://www.geeksforgeeks.org/minimum-element-of-each-row-and-each-column-in-a-matrix/)中的最小绝对元素，改为 **1** ，然后打印矩阵中所有数字的乘积作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum
// product of a matrix by multiplying
// pair of adjacent cells with -1
int maxProduct(vector<vector<int> > arr)
{
    int N = arr.size();

    // Stores the count of negative
    // numbers in the given matrix
    int cnt = 0;

    // Stores the count of 0s in
    // the given matrix arr[][]
    int zeros = 0;

    // Stores the minimum absolute value
    int maxValue = INT_MIN;

    vector<int> v;

    // Traverse the given matrix
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Count negative numbers
            if (arr[i][j] < 0) {

                // Update the maximum
                // negative value
                maxValue = max(maxValue,
                               arr[i][j]);
                cnt++;
            }

            // Increment the count
            // of 0s if exists
            if (arr[i][j] == 0)
                zeros++;
        }
    }

    // If there are more than one
    // 0, then print product as 0
    if (zeros > 1) {
        cout << "0";
    }

    int product = 1;

    // Otherwise, find the product of all
    // the elements of the matrix arr[][]
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            if (arr[i][j] == 0)
                continue;

            // Update the product
            product *= (arr[i][j]);
        }
    }

    // If count of negative
    // elements is even
    if (cnt % 2 == 0) {
        return product;
    }

    return product / maxValue;
}
// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 2, -2 }, { -3, 1 } };
    cout << maxProduct(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{

// Function to calculate maximum
// product of a matrix by multiplying
// pair of adjacent cells with -1
static int maxProduct(int[][] arr)
{
    int N = arr.length;

    // Stores the count of negative
    // numbers in the given matrix
    int cnt = 0;

    // Stores the count of 0s in
    // the given matrix arr[][]
    int zeros = 0;

    // Stores the minimum absolute value
    int maxValue = Integer.MIN_VALUE;

    int v[];

    // Traverse the given matrix
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // Count negative numbers
            if (arr[i][j] < 0) {

                // Update the maximum
                // negative value
                maxValue = Math.max(maxValue,
                               arr[i][j]);
                cnt++;
            }

            // Increment the count
            // of 0s if exists
            if (arr[i][j] == 0)
                zeros++;
        }
    }

    // If there are more than one
    // 0, then print product as 0
    if (zeros > 1) {
         System.out.println("0");
    }

    int product = 1;

    // Otherwise, find the product of all
    // the elements of the matrix arr[][]
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            if (arr[i][j] == 0)
                continue;

            // Update the product
            product *= (arr[i][j]);
        }
    }

    // If count of negative
    // elements is even
    if (cnt % 2 == 0) {
        return product;
    }

    return product / maxValue;
}

    // Driver Code
    public static void main(String[] args)
    {

         int[][] mat
        = { { 2, -2 }, { -3, 1 } };
    System.out.println(maxProduct(mat));
    }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate maximum
# product of a matrix by multiplying
# pair of adjacent cells with -1
def maxProduct(arr):

    N = len(arr)

    # Stores the count of negative
    # numbers in the given matrix
    cnt = 0

    # Stores the count of 0s in
    # the given matrix arr[][]
    zeros = 0

    # Stores the minimum absolute value
    maxValue = -10**9

    v = []

    # Traverse the given matrix
    for i in range(N):
        for j in range(N):

            # Count negative numbers
            if (arr[i][j] < 0):

                # Update the maximum
                # negative value
                maxValue = max(maxValue, arr[i][j])
                cnt += 1

            # Increment the count
            # of 0s if exists
            if (arr[i][j] == 0):
                zeros += 1

    # If there are more than one
    # 0, then prproduct as 0
    if (zeros > 1):
        print("0")

    product = 1

    # Otherwise, find the product of all
    # the elements of the matrix arr[][]
    for i in range(N):
        for j in range(N):
            if (arr[i][j] == 0):
                continue

            # Update the product
            product *= (arr[i][j])

    # If count of negative
    # elements is even
    if (cnt % 2 == 0):
        return product

    return product // maxValue

# Driver Code
if __name__ == '__main__':

    mat = [ [ 2, -2 ], [ -3, 1 ] ]
    print (maxProduct(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate maximum
// product of a matrix by multiplying
// pair of adjacent cells with -1
static int maxProduct(int[,] arr)
{
    int N = arr.GetLength(0);

    // Stores the count of negative
    // numbers in the given matrix
    int cnt = 0;

    // Stores the count of 0s in
    // the given matrix arr[][]
    int zeros = 0;

    // Stores the minimum absolute value
    int maxValue = Int32.MinValue;

    //int[] v;

    // Traverse the given matrix
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Count negative numbers
            if (arr[i, j] < 0)
            {

                // Update the maximum
                // negative value
                maxValue = Math.Max(maxValue,
                                    arr[i, j]);
                cnt++;
            }

            // Increment the count
            // of 0s if exists
            if (arr[i, j] == 0)
                zeros++;
        }
    }

    // If there are more than one
    // 0, then print product as 0
    if (zeros > 1)
    {
         Console.WriteLine("0");
    }

    int product = 1;

    // Otherwise, find the product of all
    // the elements of the matrix arr[][]
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {
            if (arr[i, j] == 0)
                continue;

            // Update the product
            product *= (arr[i, j]);
        }
    }

    // If count of negative
    // elements is even
    if (cnt % 2 == 0)
    {
        return product;
    }
    return Math.Abs(product / maxValue);
}

// Driver code
public static void Main(String []args)
{
    int[,] mat = { { 2, -2 }, { -3, 1 } };
     Console.Write(maxProduct(mat));
}
}

// This code is contriobuted by code_hunt
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to calculate maximum
// product of a matrix by multiplying
// pair of adjacent cells with -1
function maxProduct(arr)
{
    let N = arr.length;

    // Stores the count of negative
    // numbers in the given matrix
    let cnt = 0;

    // Stores the count of 0s in
    // the given matrix arr[][]
    let zeros = 0;

    // Stores the minimum absolute value
    let maxValue = Number.MIN_VALUE;

    let v = new Array();

    // Traverse the given matrix
    for (let i = 0; i < N; i++) {

        for (let j = 0; j < N; j++) {

            // Count negative numbers
            if (arr[i][j] < 0) {

                // Update the maximum
                // negative value
                maxValue = Math.max(maxValue,
                               arr[i][j]);
                cnt++;
            }

            // Increment the count
            // of 0s if exists
            if (arr[i][j] == 0)
                zeros++;
        }
    }

    // If there are more than one
    // 0, then print product as 0
    if (zeros > 1) {
         document.write("0");
    }

    let product = 1;

    // Otherwise, find the product of all
    // the elements of the matrix arr[][]
    for (let i = 0; i < N; i++) {

        for (let j = 0; j < N; j++) {

            if (arr[i][j] == 0)
                continue;

            // Update the product
            product *= (arr[i][j]);
        }
    }

    // If count of negative
    // elements is even
    if (cnt % 2 == 0) {
        return product;
    }

    return product / maxValue;
}

// Driver Code

     let mat
        = [[ 2, -2 ], [ -3, 1 ]];
   document.write(maxProduct(mat));

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*