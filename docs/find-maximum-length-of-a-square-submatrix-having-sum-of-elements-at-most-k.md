# 求元素和最多为 K 的正方形子矩阵的最大长度

> 原文:[https://www . geeksforgeeks . org/find-最大平方长度-最多有 k 个元素之和的子矩阵/](https://www.geeksforgeeks.org/find-maximum-length-of-a-square-submatrix-having-sum-of-elements-at-most-k/)

给定一个 **N x M** 矩阵，其中 **N** 是行数， **M** 是给定矩阵中的列数，以及一个整数 **K** 。任务是找出元素之和小于或等于 **K** 的正方形子矩阵的最大长度，如果没有这样的正方形，则打印 **0** 。

**示例:**

```
Input: r = 4, c = 4 , k = 6
matrix[][] = { {1, 1, 1, 1},
               {1, 0, 0, 0},
               {1, 0, 0, 0},
               {1, 0, 0, 0},
             } 
Output: 3
Explanation:
Square from (0,0) to (2,2) with 
sum 5 is one of the valid answer.

Input: r = 4, c = 4 , k = 1
matrix[][] = { {2, 2, 2},
               {2, 2, 2},
               {2, 2, 2},
               {2, 2, 2},
             } 
Output: 0
Explanation:
There is no valid answer.
```

**方法:**
思路是计算前缀和矩阵。一旦计算出前缀和矩阵，就可以用 O(1)时间复杂度计算出所需的子矩阵和。使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)计算最大长度正方形子矩阵。对于长度为 **cur_max+1** 的每个正方形，其中 **cur_max** 是当前找到的正方形子矩阵的最大长度，我们检查当前子矩阵中长度为 **cur_max+1** 的元素之和是否小于或等于 **K** 。如果是，那么将结果增加 1，否则，我们继续检查。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

    // Function to return maximum
    // length of square submatrix
    // having sum of elements at-most K
    int maxLengthSquare(int row, int column,
                        int arr[][4], int k)
    {
        // Matrix to store prefix sum
        int sum[row + 1][column + 1] ;

        for(int i = 1; i <= row; i++)
            for(int j = 0; j <= column; j++)
                sum[i][j] = 0;

        // Current maximum length
        int cur_max = 1;

        // Variable for storing
        // maximum length of square
        int max = 0;

        for (int i = 1; i <= row; i++)
        {
            for (int j = 1; j <= column; j++)
            {
                // Calculating prefix sum
                sum[i][j] = sum[i - 1][j] + sum[i][j - 1] +
                            arr[i - 1][j - 1] - sum[i - 1][j - 1];

                // Checking whether there
                // exits square with length
                // cur_max+1 or not
                if(i >= cur_max && j >= cur_max &&
                    sum[i][j] - sum[i - cur_max][j]
                    - sum[i][j - cur_max] +
                    sum[i - cur_max][j - cur_max] <= k)
                {
                    max = cur_max++;
                }
            }
        }

        // Returning the
        // maximum length
        return max;
    }

    // Driver code
    int main()
    {

        int row = 4, column = 4;
        int matrix[4][4] = { {1, 1, 1, 1},
                        {1, 0, 0, 0},
                        {1, 0, 0, 0},
                        {1, 0, 0, 0}
                        };

        int k = 6;
        int ans = maxLengthSquare(row, column, matrix, k);
        cout << ans;

        return 0;
    }

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG
{
    // Function to return maximum
    // length of square submatrix
    // having sum of elements at-most K
    public static int maxLengthSquare(int row,int column,
                                        int[][] arr, int k)
    {
        // Matrix to store prefix sum
        int sum[][] = new int[row + 1][column + 1];

        // Current maximum length
        int cur_max = 1;

        // Variable for storing
        // maximum length of square
        int max = 0;

        for (int i = 1; i <= row; i++)
        {
            for (int j = 1; j <= column; j++)
            {
                // Calculating prefix sum
                sum[i][j] = sum[i - 1][j] + sum[i][j - 1] +
                            arr[i - 1][j - 1] - sum[i - 1][j - 1];

                // Checking whether there
                // exits square with length
                // cur_max+1 or not
                if(i >=cur_max&&j>=cur_max&&sum[i][j]-sum[i - cur_max][j]
                            - sum[i][j - cur_max]
                            + sum[i - cur_max][j - cur_max] <= k){
                    max = cur_max++;
                }
            }
        }

        // Returning the
        // maximum length
        return max;
    }

    // Driver code
    public static void main(String args[])
    {

        int row = 4 , column = 4;
        int matrix[][] = { {1, 1, 1, 1},
                        {1, 0, 0, 0},
                        {1, 0, 0, 0},
                        {1, 0, 0, 0}
                        };

        int k = 6;
        int ans = maxLengthSquare(row,column,matrix, k);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import numpy as np

# Function to return maximum
# length of square submatrix
# having sum of elements at-most K
def maxLengthSquare(row, column, arr, k) :

    # Matrix to store prefix sum
    sum = np.zeros((row + 1, column + 1));

    # Current maximum length
    cur_max = 1;

    # Variable for storing
    # maximum length of square
    max = 0;

    for i in range(1, row + 1) :
        for j in range(1, column + 1) :

            # Calculating prefix sum
            sum[i][j] = sum[i - 1][j] + sum[i][j - 1] + \
                        arr[i - 1][j - 1] - \
                        sum[i - 1][j - 1];

            # Checking whether there
            # exits square with length
            # cur_max+1 or not
            if(i >= cur_max and j >= cur_max and
                 sum[i][j] - sum[i - cur_max][j] - sum[i][j -
                                     cur_max] + sum[i -
                                     cur_max][j - cur_max] <= k) :
                max = cur_max;
                cur_max += 1;

    # Returning the maximum length
    return max;

# Driver code
if __name__ == "__main__" :

    row = 4 ;
    column = 4;
    matrix = [[1, 1, 1, 1],
              [1, 0, 0, 0],
              [1, 0, 0, 0],
              [1, 0, 0, 0]];
    k = 6;
    ans = maxLengthSquare(row, column, matrix, k);
    print(ans);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to return maximum
    // length of square submatrix
    // having sum of elements at-most K
    public static int maxLengthSquare(int row,int column,
                                        int[,] arr, int k)
    {
        // Matrix to store prefix sum
        int [,]sum = new int[row + 1,column + 1];

        // Current maximum length
        int cur_max = 1;

        // Variable for storing
        // maximum length of square
        int max = 0;

        for (int i = 1; i <= row; i++)
        {
            for (int j = 1; j <= column; j++)
            {
                // Calculating prefix sum
                sum[i, j] = sum[i - 1, j] + sum[i, j - 1] +
                            arr[i - 1, j - 1] - sum[i - 1, j - 1];

                // Checking whether there
                // exits square with length
                // cur_max+1 or not
                if(i >=cur_max && j>=cur_max && sum[i, j]-sum[i - cur_max, j]
                            - sum[i, j - cur_max]
                            + sum[i - cur_max, j - cur_max] <= k)
                {
                    max = cur_max++;
                }
            }
        }

        // Returning the
        // maximum length
        return max;
    }

    // Driver code
    public static void Main()
    {

        int row = 4 , column = 4;
        int [,]matrix = { {1, 1, 1, 1},
                        {1, 0, 0, 0},
                        {1, 0, 0, 0},
                        {1, 0, 0, 0}
                        };

        int k = 6;
        int ans = maxLengthSquare(row, column, matrix, k);
        Console.WriteLine(ans);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach
// Function to return maximum
// length of square submatrix
// having sum of elements at-most K
function maxLengthSquare(row, column, arr, k) {
    // Matrix to store prefix sum
    let sum = new Array();[row + 1][column + 1];

    for (let i = 0; i < row + 1; i++) {
        let temp = new Array();
        for (let j = 0; j < column + 1; j++) {
            temp.push([])
        }
        sum.push(temp)
    }

    for (let i = 1; i <= row; i++)
        for (let j = 0; j <= column; j++)
            sum[i][j] = 0;

    // Current maximum length
    let cur_max = 1;

    // Variable for storing
    // maximum length of square
    let max = 0;

    for (let i = 1; i <= row; i++) {
        for (let j = 1; j <= column; j++) {
            // Calculating prefix sum
            sum[i][j] = sum[i - 1][j] + sum[i][j - 1] +
                arr[i - 1][j - 1] - sum[i - 1][j - 1];

            // Checking whether there
            // exits square with length
            // cur_max+1 or not
            if (i >= cur_max && j >= cur_max &&
                sum[i][j] - sum[i - cur_max][j]
                - sum[i][j - cur_max] +
                sum[i - cur_max][j - cur_max] <= k) {
                max = cur_max++;
            }
        }
    }

    // Returning the
    // maximum length
    return max;
}

// Driver code

let row = 4, column = 4;
let matrix = [[1, 1, 1, 1],
[1, 0, 0, 0],
[1, 0, 0, 0],
[1, 0, 0, 0]
];

let k = 6;
let ans = maxLengthSquare(row, column, matrix, k);
document.write(ans);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N x M)