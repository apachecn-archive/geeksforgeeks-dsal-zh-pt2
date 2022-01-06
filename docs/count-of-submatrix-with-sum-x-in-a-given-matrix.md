# 给定矩阵中和为 X 的子矩阵的计数

> 原文:[https://www . geeksforgeeks . org/给定矩阵中有 x 的子矩阵计数/](https://www.geeksforgeeks.org/count-of-submatrix-with-sum-x-in-a-given-matrix/)

给定一个大小为 **N x M** 的**矩阵**和一个整数 **X** ，任务是找出元素之和等于 **X** 的矩阵中子正方形的数量。
**举例:**

> **输入:** N = 4，M = 5，X = 10，arr[][]={{2，4，3，2，10}，{3，1，1，1，5}，{1，1，2，1，4}，{2，1，1，1，3}}
> **输出:** 3
> **解释:**
> {10}，{{2，4}，{3，1}}和{{1，1，1
> **输入:** N = 3，M = 4，X = 8，arr[][]={{3，1，5，3}，{2，2，6}，{1，2，2，4}}
> **输出:** 2
> **解释:**
> 子方块{{2，2}，{2，2}}和{{3，1}，{2，2}}有和 8。

**天真法:**
解决问题最简单的方法是生成所有可能的子正方形，并检查[子正方形所有元素之和](https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/)等于 **X** 。
***时间复杂度:**O(N<sup>3</sup>* M<sup>3</sup>)*
***辅助空间:** O(1)*
**高效方法:**为了优化上述天真方法，将所有矩阵的所有元素求和，直到每个单元都必须被制作。以下是步骤:

*   在 *O(N * M)* 计算复杂度中，预先计算左上角在(0，0)右下角在(I，j)的所有矩形的和。
*   现在，可以观察到，对于每个左上角，由于矩阵的元素是正的，所以最多可以有一个和为 **X** 的正方形。
*   记住这一点，我们可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来检查是否存在一个带有和 **X** 的正方形。
*   对于矩阵中的每个单元格 **(i，j)** ，将其固定为子正方形的左上角。然后，以 **(i，j)** 为左上角，遍历所有可能的子方块，如果和不等于 **X** 则增加计数。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Size of a column
#define m 5

// Function to find the count of submatrix
// whose sum is X
int countSubsquare(int arr[][m],
                   int n, int X)
{
    int dp[n + 1][m + 1];

    memset(dp, 0, sizeof(dp));

    // Copying arr to dp and making
    // it indexed 1
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < m; j++) {

            dp[i + 1][j + 1] = arr[i][j];
        }
    }

    // Precalculate and store the sum
    // of all rectangles with upper
    // left corner at (0, 0);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {

            // Calculating sum in
            // a 2d grid
            dp[i][j] += dp[i - 1][j]
                        + dp[i][j - 1]
                        - dp[i - 1][j - 1];
        }
    }

    // Stores the answer
    int cnt = 0;

    for (int i = 1; i <= n; i++) {

        for (int j = 1; j <= m; j++) {

            // Fix upper left corner
            // at {i, j} and perform
            // binary search on all
            // such possible squares

            // Minimum length of square
            int lo = 1;

            // Maximum length of square
            int hi = min(n - i, m - j) + 1;

            // Flag to set if sub-square
            // with sum X is found
            bool found = false;

            while (lo <= hi) {
                int mid = (lo + hi) / 2;

                // Calculate lower
                // right index if upper
                // right corner is at {i, j}
                int ni = i + mid - 1;
                int nj = j + mid - 1;

                // Calculate the sum of
                // elements in the submatrix
                // with upper left column
                // {i, j} and lower right
                // column at {ni, nj};
                int sum = dp[ni][nj]
                          - dp[ni][j - 1]
                          - dp[i - 1][nj]
                          + dp[i - 1][j - 1];

                if (sum >= X) {

                    // If sum X is found
                    if (sum == X) {
                        found = true;
                    }

                    hi = mid - 1;

                    // If sum > X, then size of
                    // the square with sum X
                    // must be less than mid
                }
                else {

                    // If sum < X, then size of
                    // the square with sum X
                    // must be greater than mid
                    lo = mid + 1;
                }
            }

            // If found, increment
            // count by 1;
            if (found == true) {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver Code
int main()
{
    int N = 4, X = 10;

    // Given Matrix arr[][]
    int arr[N][m] = { { 2, 4, 3, 2, 10 },
                      { 3, 1, 1, 1, 5 },
                      { 1, 1, 2, 1, 4 },
                      { 2, 1, 1, 1, 3 } };

    // Function Call
    cout << countSubsquare(arr, N, X)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Size of a column
static final int m = 5;

// Function to find the count of submatrix
// whose sum is X
static int countSubsquare(int arr[][],
                          int n, int X)
{
    int [][]dp = new int[n + 1][m + 1];

    // Copying arr to dp and making
    // it indexed 1
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            dp[i + 1][j + 1] = arr[i][j];
        }
    }

    // Precalculate and store the sum
    // of all rectangles with upper
    // left corner at (0, 0);
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {

            // Calculating sum in
            // a 2d grid
            dp[i][j] += dp[i - 1][j] +
                          dp[i][j - 1] -
                          dp[i - 1][j - 1];
        }
    }

    // Stores the answer
    int cnt = 0;

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {

            // Fix upper left corner
            // at {i, j} and perform
            // binary search on all
            // such possible squares

            // Minimum length of square
            int lo = 1;

            // Maximum length of square
            int hi = Math.min(n - i, m - j) + 1;

            // Flag to set if sub-square
            // with sum X is found
            boolean found = false;

            while (lo <= hi)
            {
                int mid = (lo + hi) / 2;

                // Calculate lower
                // right index if upper
                // right corner is at {i, j}
                int ni = i + mid - 1;
                int nj = j + mid - 1;

                // Calculate the sum of
                // elements in the submatrix
                // with upper left column
                // {i, j} and lower right
                // column at {ni, nj};
                int sum = dp[ni][nj] -
                            dp[ni][j - 1] -
                          dp[i - 1][nj] +
                          dp[i - 1][j - 1];

                if (sum >= X)
                {

                    // If sum X is found
                    if (sum == X)
                    {
                        found = true;
                    }

                    hi = mid - 1;

                    // If sum > X, then size of
                    // the square with sum X
                    // must be less than mid
                }
                else
                {

                    // If sum < X, then size of
                    // the square with sum X
                    // must be greater than mid
                    lo = mid + 1;
                }
            }

            // If found, increment
            // count by 1;
            if (found == true)
            {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int N = 4, X = 10;

    // Given Matrix arr[][]
    int arr[][] = { { 2, 4, 3, 2, 10 },
                    { 3, 1, 1, 1, 5 },
                    { 1, 1, 2, 1, 4 },
                    { 2, 1, 1, 1, 3 } };

    // Function Call
    System.out.print(countSubsquare(arr, N, X) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Size of a column
m = 5

# Function to find the count of
# submatrix whose sum is X
def countSubsquare(arr, n, X):

    dp = [[ 0 for x in range(m + 1)]
              for y in range(n + 1)]

    # Copying arr to dp and making
    # it indexed 1
    for i in range(n):
        for j in range(m):
            dp[i + 1][j + 1] = arr[i][j]

    # Precalculate and store the sum
    # of all rectangles with upper
    # left corner at (0, 0);
    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # Calculating sum in
            # a 2d grid
            dp[i][j] += (dp[i - 1][j] +
                         dp[i][j - 1] -
                         dp[i - 1][j - 1])

    # Stores the answer
    cnt = 0

    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # Fix upper left corner
            # at {i, j} and perform
            # binary search on all
            # such possible squares

            # Minimum length of square
            lo = 1

            # Maximum length of square
            hi = min(n - i, m - j) + 1

            # Flag to set if sub-square
            # with sum X is found
            found = False

            while (lo <= hi):
                mid = (lo + hi) // 2

                # Calculate lower right
                # index if upper right
                # corner is at {i, j}
                ni = i + mid - 1
                nj = j + mid - 1

                # Calculate the sum of
                # elements in the submatrix
                # with upper left column
                # {i, j} and lower right
                # column at {ni, nj};
                sum = (dp[ni][nj] -
                       dp[ni][j - 1] -
                       dp[i - 1][nj] +
                       dp[i - 1][j - 1])

                if (sum >= X):

                    # If sum X is found
                    if (sum == X):
                        found = True

                    hi = mid - 1

                    # If sum > X, then size of
                    # the square with sum X
                    # must be less than mid
                else:

                    # If sum < X, then size of
                    # the square with sum X
                    # must be greater than mid
                    lo = mid + 1

            # If found, increment
            # count by 1;
            if (found == True):
                cnt += 1
    return cnt

# Driver Code
if __name__ =="__main__":

    N, X = 4, 10

    # Given matrix arr[][]
    arr = [ [ 2, 4, 3, 2, 10 ],
            [ 3, 1, 1, 1, 5 ],
            [ 1, 1, 2, 1, 4 ],
            [ 2, 1, 1, 1, 3 ] ]

    # Function call
    print(countSubsquare(arr, N, X))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Size of a column
static readonly int m = 5;

// Function to find the count of submatrix
// whose sum is X
static int countSubsquare(int [,]arr,
                          int n, int X)
{
    int [,]dp = new int[n + 1, m + 1];

    // Copying arr to dp and making
    // it indexed 1
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            dp[i + 1, j + 1] = arr[i, j];
        }
    }

    // Precalculate and store the sum
    // of all rectangles with upper
    // left corner at (0, 0);
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= m; j++)
        {

            // Calculating sum in
            // a 2d grid
            dp[i, j] += dp[i - 1, j] +
                        dp[i, j - 1] -
                        dp[i - 1, j - 1];
        }
    }

    // Stores the answer
    int cnt = 0;

    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= m; j++)
        {

            // Fix upper left corner
            // at {i, j} and perform
            // binary search on all
            // such possible squares

            // Minimum length of square
            int lo = 1;

            // Maximum length of square
            int hi = Math.Min(n - i, m - j) + 1;

            // Flag to set if sub-square
            // with sum X is found
            bool found = false;

            while (lo <= hi)
            {
                int mid = (lo + hi) / 2;

                // Calculate lower
                // right index if upper
                // right corner is at {i, j}
                int ni = i + mid - 1;
                int nj = j + mid - 1;

                // Calculate the sum of
                // elements in the submatrix
                // with upper left column
                // {i, j} and lower right
                // column at {ni, nj};
                int sum = dp[ni, nj] -
                          dp[ni, j - 1] -
                          dp[i - 1, nj] +
                          dp[i - 1, j - 1];

                if (sum >= X)
                {

                    // If sum X is found
                    if (sum == X)
                    {
                        found = true;
                    }

                    hi = mid - 1;

                    // If sum > X, then size of
                    // the square with sum X
                    // must be less than mid
                }
                else
                {

                    // If sum < X, then size of
                    // the square with sum X
                    // must be greater than mid
                    lo = mid + 1;
                }
            }

            // If found, increment
            // count by 1;
            if (found == true)
            {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4, X = 10;

    // Given Matrix [,]arr
    int [,]arr = { { 2, 4, 3, 2, 10 },
                   { 3, 1, 1, 1, 5 },
                   { 1, 1, 2, 1, 4 },
                   { 2, 1, 1, 1, 3 } };

    // Function call
    Console.Write(countSubsquare(arr, N, X) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Size of a column
     var m = 5;

    // Function to find the count of submatrix
    // whose sum is X
    function countSubsquare(arr , n , X) {
        var dp = Array(n + 1);
        for(var i =0;i<n+1;i++)
        dp[i] = Array(m + 1).fill(0);

        // Copying arr to dp and making
        // it indexed 1
        for (i = 0; i < n; i++) {
            for (j = 0; j < m; j++) {
                dp[i + 1][j + 1] = arr[i][j];
            }
        }

        // Precalculate and store the sum
        // of all rectangles with upper
        // left corner at (0, 0);
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {

                // Calculating sum in
                // a 2d grid
                dp[i][j] += dp[i - 1][j] +
                dp[i][j - 1] - dp[i - 1][j - 1];
            }
        }

        // Stores the answer
        var cnt = 0;

        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {

                // Fix upper left corner
                // at {i, j} and perform
                // binary search on all
                // such possible squares

                // Minimum length of square
                var lo = 1;

                // Maximum length of square
                var hi = Math.min(n - i, m - j) + 1;

                // Flag to set if sub-square
                // with sum X is found
                var found = false;

                while (lo <= hi) {
                    var mid = parseInt((lo + hi) / 2);

                    // Calculate lower
                    // right index if upper
                    // right corner is at {i, j}
                    var ni = i + mid - 1;
                    var nj = j + mid - 1;

                    // Calculate the sum of
                    // elements in the submatrix
                    // with upper left column
                    // {i, j} and lower right
                    // column at {ni, nj];
                    var sum = dp[ni][nj] - dp[ni][j - 1] -
                    dp[i - 1][nj] + dp[i - 1][j - 1];

                    if (sum >= X) {

                        // If sum X is found
                        if (sum == X) {
                            found = true;
                        }

                        hi = mid - 1;

                        // If sum > X, then size of
                        // the square with sum X
                        // must be less than mid
                    } else {

                        // If sum < X, then size of
                        // the square with sum X
                        // must be greater than mid
                        lo = mid + 1;
                    }
                }

                // If found, increment
                // count by 1;
                if (found == true) {
                    cnt++;
                }
            }
        }
        return cnt;
    }

    // Driver Code

        var N = 4, X = 10;

        // Given Matrix arr
        var arr = [ [ 2, 4, 3, 2, 10 ],
                    [ 3, 1, 1, 1, 5 ],
                    [ 1, 1, 2, 1, 4 ],
                    [ 2, 1, 1, 1, 3 ] ];

        // Function Call
        document.write(countSubsquare(arr, N, X) + "<br/>");

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * M * log(max(N，M)))*
***辅助空间:** O(N * M)*