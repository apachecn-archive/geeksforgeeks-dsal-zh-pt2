# 矩阵任意矩形的最大和不超过 K

> 原文:[https://www . geeksforgeeks . org/矩阵任意矩形的最大和不超过 k/](https://www.geeksforgeeks.org/maximum-sum-not-exceeding-k-possible-for-any-rectangle-of-a-matrix/)

给定一个尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**和一个整数 **K** ，任务是从给定矩阵中找出任意矩形的最大可能和，其元素之和最多为 **K** 。

**示例:**

> **输入:** mat[][] ={{1，0，1}，{0，-2，3}}，K = 2
> **输出:** 2
> **解释:**矩阵中任意矩形的最大可能和为 2 ( < = K)，从矩阵{{0，1}，{-2，3}}中获得。
> 
> **输入:** mat[][] = {{2，2，-1}}，K = 3
> **输出:** 3
> **说明:**最大和矩形为{{2，2，-1}}为 3 ( < - K)。

**朴素方法:**最简单的方法是从给定的矩阵中检查所有可能的子矩阵，其元素之和最多是否为**K**。如果发现为真，存储该子矩阵的和。最后，打印得到的这些子矩阵的最大和。

***时间复杂度:**O(N<sup>6</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过使用类似于[在 2D 矩阵](https://www.geeksforgeeks.org/maximum-sum-rectangle-in-a-2d-matrix-dp-27/)中寻找最大和矩形的方法来优化。唯一不同的是矩形的和不能超过 **K** 。其思想是逐个固定左右列，在每次迭代中，存储当前矩形中每行的和，并在这个数组中找到小于 **K** 的最大子阵列和。按照以下步骤解决问题:

*   初始化一个变量，比如 **res** ，它存储子矩阵元素的最大和，该子矩阵的和最多为 K 。
*   [使用左列的变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M–1】**，并执行以下步骤:
    *   初始化一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **V[]** ，以存储左右列对之间每行的元素之和。
    *   使用右列的变量 **j** 迭代范围****【0，M–1】**，并执行以下步骤:

        *   求每行当前左右列之和，更新数组 **V[]** 中的和。
        *   在 **V[]** 中找到和小于**K**T3 的[最大和子阵，并将结果存储在 **ans** 中。](https://www.geeksforgeeks.org/maximum-sum-subarray-having-sum-less-than-or-equal-to-given-sum-using-set/)
        *   如果 **ans** 的值大于 **res** 的值，则将 **res** 更新为 **ans** 。** 
*   **完成上述步骤后，打印 **res** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible
// sum of  arectangle which is less than K
int maxSubarraySum(vector<int>& sum,
                   int k, int row)
{
    int curSum = 0, curMax = INT_MIN;

    // Stores the values (cum_sum - K)
    set<int> sumSet;

    // Insert 0 into the set sumSet
    sumSet.insert(0);

    // Traverse over the rows
    for (int r = 0; r < row; ++r) {

        // Get cumulative sum from [0 to i]
        curSum += sum[r];

        // Search for upperbound of
        // (cSum - K) in the hashmap
        auto it = sumSet.lower_bound(curSum - k);

        // If upper_bound of (cSum - K)
        // exists, then update max sum
        if (it != sumSet.end()) {
            curMax = max(curMax,
                         curSum - *it);
        }

        // Insert cummulative value
        // in the hashmap
        sumSet.insert(curSum);
    }

    // Return the maximum sum
    // which is less than K
    return curMax;
}

// Function to find the maximum sum of
// rectangle such that its sum is no
// larger than K
void maxSumSubmatrix(
    vector<vector<int> >& matrix, int k)
{
    // Stores the number of rows
    // and columns
    int row = matrix.size();
    int col = matrix[0].size();

    // Store the required result
    int ret = INT_MIN;

    // Set the left column
    for (int i = 0; i < col; ++i) {
        vector<int> sum(row, 0);

        // Set the right column for the
        // left column set by outer loop
        for (int j = i; j < col; ++j) {

            // Calculate sum between the
            // current left and right
            // for every row
            for (int r = 0; r < row; ++r) {
                sum[r] += matrix[r][j];
            }

            // Stores the sum of rectangle
            int curMax = maxSubarraySum(
                sum, k, row);

            // Update the overall maximum sum
            ret = max(ret, curMax);
        }
    }

    // Print the result
    cout << ret;
}

// Driver Code
int main()
{
    vector<vector<int> > matrix
        = { { 1, 0, 1 }, { 0, -2, 3 } };
    int K = 2;

    // Function Call
    maxSumSubmatrix(matrix, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

// Function to find the maximum possible
// sum of arectangle which is less than K
    static int maxSubarraySum(int[] sum,
                              int k, int row) {
        int curSum = 0, curMax = Integer.MIN_VALUE;

        // Stores the values (cum_sum - K)
        Set<Integer> sumSet = new HashSet<Integer>();

        // Insert 0 into the set sumSet
        sumSet.add(0);

        // Traverse over the rows
        for (int r = 0; r < row; ++r) {

            // Get cumulative sum from [0 to i]
            curSum += sum[r];

            // Search for upperbound of
            // (cSum - K) in the hashmap
            ArrayList<Integer> list = new ArrayList<Integer>();
            list.addAll(sumSet);

            int it = Integer.MIN_VALUE;
            for (int e : list)
                if (e >= (curSum - k)) {
                    it = e;
                    break;
                }

            // If upper_bound of (cSum - K)
            // exists, then update max sum
            if (it != Integer.MIN_VALUE) {
                curMax = Math.max(curMax,
                                  curSum - it);
            }

            // Insert cummulative value
            // in the hashmap
            sumSet.add(curSum);
        }

        // Return the maximum sum
        // which is less than K
        return curMax;
    }

// Function to find the maximum sum of
// rectangle such that its sum is no
// larger than K
    static void maxSumSubmatrix(int[][] matrix, int k) {

        // Stores the number of rows
        // and columns
        int row = matrix.length;
        int col = matrix[0].length;

        // Store the required result
        int ret = Integer.MIN_VALUE;

        // Set the left column
        for (int i = 0; i < col; ++i) {
            int[] sum = new int[row];

            // Set the right column for the
            // left column set by outer loop
            for (int j = i; j < col; ++j) {

                // Calculate sum between the
                // current left and right
                // for every row
                for (int r = 0; r < row; ++r) {
                    sum[r] += matrix[r][j];
                }

                // Stores the sum of rectangle
                int curMax = maxSubarraySum(
                                 sum, k, row);

                // Update the overall maximum sum
                ret = Math.max(ret, curMax);
            }
        }

        // Print the result
        System.out.print(ret);
    }

// Driver Code
    public static void main (String[] args) {
        int[][] matrix =  { { 5, -4, -3, 4 },
            { -3, -4, 4, 5 },
            {5, 1, 5, -4}
        };
        int K = 8;

        // Function Call
        maxSumSubmatrix(matrix, K);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from bisect import bisect_left, bisect_right
import sys

# Function to find the maximum possible
# sum of  arectangle which is less than K
def maxSubarraySum(sum, k, row):

    curSum, curMax = 0, -sys.maxsize - 1

    # Stores the values (cum_sum - K)
    sumSet = {}

    # Insert 0 into the set sumSet
    sumSet[0] = 1

    # Traverse over the rows
    for r in range(row):

        # Get cumulative sum from [0 to i]
        curSum += sum[r]

        # Search for upperbound of
        # (cSum - K) in the hashmap
        arr = list(sumSet.keys())

        it = bisect_left(arr, curSum - k)

        # If upper_bound of (cSum - K)
        # exists, then update max sum
        if (it != len(arr)):
            curMax = max(curMax, curSum - it)

        # Insert cummulative value
        # in the hashmap
        sumSet[curSum] = 1

    # Return the maximum sum
    # which is less than K
    return curMax

# Function to find the maximum sum of
# rectangle such that its sum is no
# larger than K
def maxSumSubmatrix(matrix, k):

    # Stores the number of rows
    # and columns
    row = len(matrix)
    col = len(matrix[0])

    # Store the required result
    ret = -sys.maxsize - 1

    # Set the left column
    for i in range(col):
        sum = [0] * (row)

        # Set the right column for the
        # left column set by outer loop
        for j in range(i, col):

            # Calculate sum between the
            # current left and right
            # for every row
            for r in range(row):
                sum[r] += matrix[r][j]

            # Stores the sum of rectangle
            curMax = maxSubarraySum(sum, k, row)

            # Update the overall maximum sum
            ret = max(ret, curMax)

    # Print the result
    print(ret)

# Driver Code
if __name__ == '__main__':

    matrix = [ [ 1, 0, 1 ], [ 0, -2, 3 ] ]
    K = 2

    # Function Call
    maxSumSubmatrix(matrix, K)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum possible
// sum of  arectangle which is less than K
static int maxSubarraySum(int[] sum,int k, int row)
{
    int curSum = 0, curMax = Int32.MinValue;

    // Stores the values (cum_sum - K)
    HashSet<int> sumSet = new HashSet<int>();

    // Insert 0 into the set sumSet
    sumSet.Add(0);

    // Traverse over the rows
    for(int r = 0; r < row; ++r)
    {

        // Get cumulative sum from [0 to i]
        curSum += sum[r];

        // Search for upperbound of
        // (cSum - K) in the hashmap
        List<int> list = new List<int>();
        list.AddRange(sumSet);
        int it = list.LastIndexOf(curSum - k);

        // If upper_bound of (cSum - K)
        // exists, then update max sum
        if (it > -1)
        {
            curMax = Math.Max(curMax,
                              curSum - it);
        }

        // Insert cummulative value
        // in the hashmap
        sumSet.Add(curSum);
    }

    // Return the maximum sum
    // which is less than K
    return curMax;
}

// Function to find the maximum sum of
// rectangle such that its sum is no
// larger than K
static void maxSumSubmatrix(int[,] matrix, int k)
{

    // Stores the number of rows
    // and columns
    int row = matrix.GetLength(0);
    int col = matrix.GetLength(1);

    // Store the required result
    int ret = Int32.MinValue;

    // Set the left column
    for(int i = 0; i < col; ++i)
    {
        int[] sum = new int[row];

        // Set the right column for the
        // left column set by outer loop
        for(int j = i; j < col; ++j)
        {

            // Calculate sum between the
            // current left and right
            // for every row
            for(int r = 0; r < row; ++r)
            {
                sum[r] += matrix[r, j];
            }

            // Stores the sum of rectangle
            int curMax = maxSubarraySum(
                sum, k, row);

            // Update the overall maximum sum
            ret = Math.Max(ret, curMax);
        }
    }

    // Print the result
    Console.Write(ret);
}

// Driver Code
static public void Main()
{
    int[,] matrix = { { 1, 0, 1 },
                      { 0, -2, 3 } };
    int K = 2;

    // Function Call
    maxSumSubmatrix(matrix, K);
}
}

// This code is contributed by rag2127
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to find the maximum possible
// sum of  arectangle which is less than K
function maxSubarraySum(sum,k,row)
{
    let curSum = 0, curMax = Number.MIN_VALUE;

    // Stores the values (cum_sum - K)
    let sumSet = new Set();

    // Insert 0 into the set sumSet
    sumSet.add(0);

    // Traverse over the rows
    for(let r = 0; r < row; ++r)
    {

        // Get cumulative sum from [0 to i]
        curSum += sum[r];

        // Search for upperbound of
        // (cSum - K) in the hashmap
        let list = [];
        list=Array.from(sumSet);

        let it = list.lastIndexOf(curSum - k);

        // If upper_bound of (cSum - K)
        // exists, then update max sum
        if (it >-1)
        {
            curMax = Math.max(curMax,
                              curSum - it);
        }

        // Insert cummulative value
        // in the hashmap
        sumSet.add(curSum);
    }

    // Return the maximum sum
    // which is less than K
    return curMax;
}

// Function to find the maximum sum of
// rectangle such that its sum is no
// larger than K
function maxSumSubmatrix(matrix,  k)
{

    // Stores the number of rows
    // and columns
    let row = matrix.length;
    let col = matrix[0].length;

    // Store the required result
    let ret = Number.MIN_VALUE;

    // Set the left column
    for(let i = 0; i < col; ++i)
    {
        let sum = new Array(row);
         for(let j=0;j<row;j++)
            sum[j]=0;
        // Set the right column for the
        // left column set by outer loop
        for(let j = i; j < col; ++j)
        {

            // Calculate sum between the
            // current left and right
            // for every row
            for(let r = 0; r < row; ++r)
            {
                sum[r] += matrix[r][j];
            }

            // Stores the sum of rectangle
            let curMax = maxSubarraySum(
                sum, k, row);

            // Update the overall maximum sum
            ret = Math.max(ret, curMax);
        }
    }

    // Print the result
    document.write(ret);
}

// Driver Code
let matrix=[[ 1, 0, 1 ],
            [ 0, -2, 3 ]];
let K = 2;

maxSumSubmatrix(matrix, K)

// This code is contributed by patel2127

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N<sup>3</sup>* log(N))*
***辅助空间:** O(N)***