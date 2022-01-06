# 总和小于或等于 K 的最大尺寸正方形子矩阵

> 原文:[https://www . geesforgeks . org/最大尺寸-平方-总和小于或等于 k 的子矩阵/](https://www.geeksforgeeks.org/maximum-size-square-sub-matrix-with-sum-less-than-or-equals-to-k/)

给定大小为 **M x N** 的矩阵 **arr[][]** ，该矩阵具有正整数和数字 **K** ，任务是找到元素之和小于或等于 **K** 的最大正方形子矩阵的大小。

**示例:**

```
Input: 
arr[][] = { { 1, 1, 3, 2, 4, 3, 2 },
            { 1, 1, 3, 2, 4, 3, 2 },
            { 1, 1, 3, 2, 4, 3, 2 } },
K = 4
Output: 
2
Explanation:
Maximum size square Sub-Matrix 
with sum less than or equals to 4
      1 1
      1 1
Size is 2.

Input: 
arr[][] = { { 1, 1, 3, 2, 4, 3, 2 },
            { 1, 1, 3, 2, 4, 3, 2 },
            { 1, 1, 3, 2, 4, 3, 2 } }, 
K = 22
Output: 
3
Explanation:
Maximum size square Sub-Matrix 
with sum less than or equals to 22
      1 1 3
      1 1 3
      1 1 3
Size is 3\. 
```

**进场:**

1.  对于给定的矩阵 **arr[][]** 创建一个[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)矩阵(比如说**和[][]** )，这样**和【I】【j】**存储大小为 **i x j** 的矩阵的所有元素的和。
2.  对于前缀和矩阵**中的每一行，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)对[][]** 求和，请执行以下操作:
    *   执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，下限为 **0** ，上限为**正方形矩阵最大尺寸**。
    *   找到中间指数(说**中间**)。
    *   如果大小为 **mid** 的所有可能方阵的元素之和小于或等于 **K** ，则更新下限为 **mid + 1** 以寻找大小大于 mid 的最大和。
    *   否则将上限更新为**mid–1**，以找到大小小于 mid 的最大和。
3.  对于上面给定的有效条件，在每次迭代中不断更新方阵的最大尺寸。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum size
    // of matrix with sum <= K
    static void findMaxMatrixSize(int[][] arr, int K)
    {
        int i, j;

        // N size of rows and M size of cols
        int n = arr.length;
        int m = arr[0].length;

        // To store the prefix sum of matrix
        int[][] sum = new int[n + 1][m + 1];

        // Create prefix sum
        for (i = 0; i <= n; i++) {

            // Traverse each rows
            for (j = 0; j <= m; j++) {
                if (i == 0 || j == 0) {
                    sum[i][j] = 0;
                    continue;
                }

                // Update the prefix sum
                // till index i x j
                sum[i][j] = arr[i - 1][j - 1]
                            + sum[i - 1][j] + sum[i][j - 1]
                            - sum[i - 1][j - 1];
            }
        }

        // To store the maximum size of
        // matrix with sum <= K
        int ans = 0;

        // Traverse the sum matrix
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {

                // Index out of bound
                if (i + ans - 1 > n || j + ans - 1 > m)
                    break;

                int mid, lo = ans;

                // Maximum possible size
                // of matrix
                int hi = Math.min(n - i + 1, m - j + 1);

                // Binary Search
                while (lo < hi) {

                    // Find middle index
                    mid = (hi + lo + 1) / 2;

                    // Check whether sum <= K
                    // or not
                    // If Yes check for other
                    // half of the search
                    if (sum[i + mid - 1][j + mid - 1]
                            + sum[i - 1][j - 1]
                            - sum[i + mid - 1][j - 1]
                            - sum[i - 1][j + mid - 1]
                        <= K) {
                        lo = mid;
                    }

                    // Else check it in first
                    // half
                    else {
                        hi = mid - 1;
                    }
                }

                // Update the maximum size matrix
                ans = Math.max(ans, lo);
            }
        }

        // Print the final answer
        System.out.print(ans + "\n");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] arr = { { 1, 1, 3, 2, 4, 3, 2 },
                        { 1, 1, 3, 2, 4, 3, 2 },
                        { 1, 1, 3, 2, 4, 3, 2 } };

        // Given target sum
        int K = 4;

        // Function Call
        findMaxMatrixSize(arr, K);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum size
# of matrix with sum <= K

def findMaxMatrixSize(arr, K):

    # N size of rows and M size of cols
    n = len(arr)
    m = len(arr[0])

    # To store the prefix sum of matrix
    sum = [[0 for i in range(m + 1)] for j in range(n + 1)]

    # Create Prefix Sum
    for i in range(n + 1):

        # Traverse each rows
        for j in range(m+1):
            if (i == 0 or j == 0):
                sum[i][j] = 0
                continue

            # Update the prefix sum
            # till index i x j
            sum[i][j] = arr[i - 1][j - 1] + sum[i - 1][j] + \
                sum[i][j - 1]-sum[i - 1][j - 1]

    # To store the maximum size of
    # matrix with sum <= K
    ans = 0

    # Traverse the sum matrix
    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # Index out of bound
            if (i + ans - 1 > n or j + ans - 1 > m):
                break

            mid = ans
            lo = ans

            # Maximum possible size
            # of matrix
            hi = min(n - i + 1, m - j + 1)

            # Binary Search
            while (lo < hi):

                # Find middle index
                mid = (hi + lo + 1) // 2

                # Check whether sum <= K
                # or not
                # If Yes check for other
                # half of the search
                if (sum[i + mid - 1][j + mid - 1] +
                    sum[i - 1][j - 1] -
                    sum[i + mid - 1][j - 1] -
                        sum[i - 1][j + mid - 1] <= K):
                    lo = mid

                # Else check it in first
                # half
                else:
                    hi = mid - 1

            # Update the maximum size matrix
            ans = max(ans, lo)

    # Print the final answer
    print(ans)

# Driver Code
if __name__ == '__main__':
    arr = [[1, 1, 3, 2, 4, 3, 2],
           [1, 1, 3, 2, 4, 3, 2],
           [1, 1, 3, 2, 4, 3, 2]]

    # Given target sum
    K = 4

    # Function Call
    findMaxMatrixSize(arr, K)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the maximum size
    // of matrix with sum <= K
    static void findMaxMatrixSize(int[, ] arr, int K)
    {
        int i, j;

        // N size of rows and M size of cols
        int n = arr.GetLength(0);
        int m = arr.GetLength(1);

        // To store the prefix sum of matrix
        int[, ] sum = new int[n + 1, m + 1];

        // Create prefix sum
        for (i = 0; i <= n; i++) {

            // Traverse each rows
            for (j = 0; j <= m; j++) {
                if (i == 0 || j == 0) {
                    sum[i, j] = 0;
                    continue;
                }

                // Update the prefix sum
                // till index i x j
                sum[i, j] = arr[i - 1, j - 1]
                            + sum[i - 1, j] + sum[i, j - 1]
                            - sum[i - 1, j - 1];
            }
        }

        // To store the maximum size
        // of matrix with sum <= K
        int ans = 0;

        // Traverse the sum matrix
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {

                // Index out of bound
                if (i + ans - 1 > n || j + ans - 1 > m)
                    break;

                int mid, lo = ans;

                // Maximum possible size
                // of matrix
                int hi = Math.Min(n - i + 1, m - j + 1);

                // Binary Search
                while (lo < hi) {

                    // Find middle index
                    mid = (hi + lo + 1) / 2;

                    // Check whether sum <= K
                    // or not
                    // If Yes check for other
                    // half of the search
                    if (sum[i + mid - 1, j + mid - 1]
                            + sum[i - 1, j - 1]
                            - sum[i + mid - 1, j - 1]
                            - sum[i - 1, j + mid - 1]
                        <= K) {
                        lo = mid;
                    }

                    // Else check it in first
                    // half
                    else {
                        hi = mid - 1;
                    }
                }

                // Update the maximum size matrix
                ans = Math.Max(ans, lo);
            }
        }

        // Print the readonly answer
        Console.Write(ans + "\n");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[, ] arr = { { 1, 1, 3, 2, 4, 3, 2 },
                        { 1, 1, 3, 2, 4, 3, 2 },
                        { 1, 1, 3, 2, 4, 3, 2 } };

        // Given target sum
        int K = 4;

        // Function Call
        findMaxMatrixSize(arr, K);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// js program for the above approach

// Function to find the maximum size
// of matrix with sum <= K
function findMaxMatrixSize(arr, K)
{

    let i, j;

    // N size of rows and M size of cols
    let n = arr.length;
    let m = arr[0].length;

    // To store the prefix sum of matrix
    let sum=[];
    for(i =0;i<n+1;i++){
       sum[i] = [];
       for(j =0;j<m+1;j++){
           sum[i][j] = 0;
       }
    }
    // Create Prefix Sum
    for ( i = 0; i <= n; i++) {

        // Traverse each rows
        for (j = 0; j <= m; j++) {

            if (i == 0 || j == 0) {
                sum[i][j] = 0;
                continue;
            }

            // Update the prefix sum
            // till index i x j
            sum[i][j] = arr[i - 1][j - 1] + sum[i - 1][j]
                        + sum[i][j - 1] - sum[i - 1][j - 1];
        }
    }

    // To store the maximum size of
    // matrix with sum <= K
    let ans = 0;

    // Traverse the sum matrix
    for (i = 1; i <= n; i++) {

        for (j = 1; j <= m; j++) {

            // Index out of bound
            if (i + ans - 1 > n || j + ans - 1 > m)
                break;

            let mid, lo = ans;

            // Maximum possible size
            // of matrix
            let hi = Math.min(n - i + 1, m - j + 1);

            // Binary Search
            while (lo < hi) {

                // Find middle index
                mid = Math.floor((hi + lo + 1) / 2);

                // Check whether sum <= K
                // or not
                // If Yes check for other
                // half of the search
                if (sum[i + mid - 1][j + mid - 1]
                        + sum[i - 1][j - 1]
                        - sum[i + mid - 1][j - 1]
                        - sum[i - 1][j + mid - 1]
                    <= K) {
                    lo = mid;
                }

                // Else check it in first
                // half
                else {
                    hi = mid - 1;
                }
            }

            // Update the maximum size matrix
            ans = Math.max(ans, lo);
        }
    }

    // Print the final answer
    document.write(ans ,'<br>');
}

// Driver Code

    let arr = [[ 1, 1, 3, 2, 4, 3, 2 ],
            [ 1, 1, 3, 2, 4, 3, 2 ],
            [ 1, 1, 3, 2, 4, 3, 2 ]];

    // Given target sum
    let K = 4;

    // Function Call
    findMaxMatrixSize(arr, K);
</script>
```

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum size
// of matrix with sum <= K
void findMaxMatrixSize(vector<vector<int> > arr, int K)
{

    int i, j;

    // N size of rows and M size of cols
    int n = arr.size();
    int m = arr[0].size();

    // To store the prefix sum of matrix
    int sum[n + 1][m + 1];

    // Create Prefix Sum
    for (int i = 0; i <= n; i++) {

        // Traverse each rows
        for (int j = 0; j <= m; j++) {

            if (i == 0 || j == 0) {
                sum[i][j] = 0;
                continue;
            }

            // Update the prefix sum
            // till index i x j
            sum[i][j] = arr[i - 1][j - 1] + sum[i - 1][j]
                        + sum[i][j - 1] - sum[i - 1][j - 1];
        }
    }

    // To store the maximum size of
    // matrix with sum <= K
    int ans = 0;

    // Traverse the sum matrix
    for (i = 1; i <= n; i++) {

        for (j = 1; j <= m; j++) {

            // Index out of bound
            if (i + ans - 1 > n || j + ans - 1 > m)
                break;

            int mid, lo = ans;

            // Maximum possible size
            // of matrix
            int hi = min(n - i + 1, m - j + 1);

            // Binary Search
            while (lo < hi) {

                // Find middle index
                mid = (hi + lo + 1) / 2;

                // Check whether sum <= K
                // or not
                // If Yes check for other
                // half of the search
                if (sum[i + mid - 1][j + mid - 1]
                        + sum[i - 1][j - 1]
                        - sum[i + mid - 1][j - 1]
                        - sum[i - 1][j + mid - 1]
                    <= K) {
                    lo = mid;
                }

                // Else check it in first
                // half
                else {
                    hi = mid - 1;
                }
            }

            // Update the maximum size matrix
            ans = max(ans, lo);
        }
    }

    // Print the final answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    vector<vector<int> > arr;

    arr = { { 1, 1, 3, 2, 4, 3, 2 },
            { 1, 1, 3, 2, 4, 3, 2 },
            { 1, 1, 3, 2, 4, 3, 2 } };

    // Given target sum
    int K = 4;

    // Function Call
    findMaxMatrixSize(arr, K);
    return 0;
}
```

**Output**

```
2
```

**时间复杂度:** O(N*N*log(N))
**辅助空间:** O(M*N)