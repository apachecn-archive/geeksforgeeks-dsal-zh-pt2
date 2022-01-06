# 终止于矩阵最后一行任意元素的最大权重路径

> 原文:[https://www . geesforgeks . org/最大权重-路径-结束-元素-最后一行-矩阵/](https://www.geeksforgeeks.org/maximum-weight-path-ending-element-last-row-matrix/)

给定一个整数矩阵，其中每个元素代表单元格的权重。求矩阵中权重最大的路径。路径遍历规则为:

*   它应该从左上角的元素开始。
*   路径可以在最后一行的任何元素处结束。
*   我们可以从一个单元格(I，j)转到后面两个单元格。
    1.  下移:(i+1，j)
    2.  对角线移动:(i+1，j+1)

示例:

```
Input : N = 5
        mat[5][5] = {{ 4, 2 ,3 ,4 ,1 },
                     { 2 , 9 ,1 ,10 ,5 },
                     {15, 1 ,3 , 0 ,20 },
                     {16 ,92, 41, 44 ,1},
                     {8, 142, 6, 4, 8} };
Output : 255
Path with max weight : 4 + 2 +15 + 92 + 142 = 255                 
```

上述问题可以递归定义。

```
Let maxCost(i, j) be the cost maximum cost to
reach mat[i][j].  Since end point can be any point
in last row, we finally return maximum of all values
maxCost(N-1, j) where j varies from 0 to N-1.

If i == 0 and j == 0
   maxCost(0, 0) = mat[0][0]

// We can traverse through first column only by
// down move
Else if j = 0
  maxCost(i, 0) = maxCost(i-1, 0) + mat[i][0]

// In other cases, a cell mat[i][j] can be reached
// through previous two cells ma[i-1][j] and 
// mat[i-1][j-1]
Else
  maxCost(i, j) = mat[i][j] + max(maxCost(i-1, j),
                                maxCost(i-1, j-1)),
```

如果画出上述递归解的递归树，可以观察到[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。由于问题有重叠的子问题，我们可以使用动态规划来有效地解决它。下面是基于动态规划的解决方案。

## C++

```
// C++ program to find the path having the
// maximum weight in matrix
#include<bits/stdc++.h>
using namespace std;
const int MAX = 1000;

/* Function which return the maximum weight
   path sum */
int maxCost(int mat[][MAX], int N)
{
    // creat 2D matrix to store the sum of the path
    int dp[N][N];
    memset(dp, 0, sizeof(dp));

    dp[0][0] = mat[0][0];

    // Initialize first column of total weight
    // array (dp[i to N][0])
    for (int i=1; i<N; i++)
        dp[i][0] = mat[i][0] + dp[i-1][0];

    // Calculate rest paht sum of weight matrix
    for (int i=1; i<N; i++)
       for (int j=1; j<i+1&&j<N; j++)
          dp[i][j] = mat[i][j] +
                    max(dp[i-1][j-1], dp[i-1][j]);

    // find the max weight path sum to rech
    // the last row
    int result = 0;
    for (int i=0; i<N; i++)
        if (result < dp[N-1][i])
            result = dp[N-1][i];

    // return maximum weight path sum
    return result;
}

// Driver program
int main()
{
    int mat[MAX][MAX] = {  { 4, 1 ,5 ,6 , 1 },
        { 2 ,9 ,2 ,11 ,10 },
        { 15,1 ,3 ,15, 2 },
        { 16, 92, 41,4,3},
        { 8, 142, 6, 4, 8 }
    };
    int N = 5;
    cout << "Maximum Path Sum : "
        << maxCost(mat, N)<<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Maximum weight path ending at
// any element of last row in a matrix
import java.util.*;

class GFG {

    /* Function which return the maximum weight
       path sum */
    public static int maxCost(int mat[][], int N)
    {
        // create 2D matrix to store the sum of
        // the path
        int dp[][]=new int[N][N];

        dp[0][0] = mat[0][0];

        // Initialize first column of total
        // weight array (dp[i to N][0])
        for (int i = 1; i < N; i++)
            dp[i][0] = mat[i][0] + dp[i-1][0];

        // Calculate rest path sum of weight matrix
        for (int i = 1; i < N; i++)
           for (int j = 1; j < i + 1 && j < N; j++)
              dp[i][j] = mat[i][j] +
                        Math.max(dp[i-1][j-1],
                                 dp[i-1][j]);

        // find the max weight path sum to reach
        // the last row
        int result = 0;
        for (int i = 0; i < N; i++)
            if (result < dp[N-1][i])
                result = dp[N-1][i];

        // return maximum weight path sum
        return result;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int mat[][] = {  { 4, 1 ,5 ,6 , 1 },
                { 2 ,9 ,2 ,11 ,10 },
                { 15,1 ,3 ,15, 2 },
                { 16, 92, 41,4,3},
                { 8, 142, 6, 4, 8 }
            };
            int N = 5;
           System.out.println("Maximum Path Sum : "+
                               maxCost(mat, N));
    }
}
// This code is contributed by Arnav Kr. Mandal. 
```

## 蟒蛇 3

```
# Python3 program to find the path
# having the maximum weight in matrix

MAX = 1000

# Function which return the
# maximum weight path sum
def maxCost(mat, N):

    # creat 2D matrix to store the sum of the path
    dp = [[0 for i in range(N)] for j in range(N)]

    dp[0][0] = mat[0][0]

    # Initialize first column of total weight
    # array (dp[i to N][0])
    for i in range(1, N):
        dp[i][0] = mat[i][0] + dp[i - 1][0]

    # Calculate rest path sum of weight matrix
    for i in range(1, N):
        for j in range(1, min(i + 1, N)):
            dp[i][j] = mat[i][j] + \
                       max(dp[i - 1][j - 1],
                           dp[i - 1][j])

    # find the max weight path sum to reach
    # the last row
    result = 0
    for i in range(N):
        if (result < dp[N - 1][i]):
            result = dp[N - 1][i]

    # return maximum weight path sum
    return result

# Driver Program

mat = [ [4, 1 ,5 ,6 , 1],
        [2 ,9 ,2 ,11 ,10],
        [15,1 ,3 ,15, 2],
        [16, 92, 41,4,3],
        [8, 142, 6, 4, 8]]

N = 5
print('Maximum Path Sum :', maxCost(mat, N))

# This code is contributed by Soumen Ghosh.
```

## C#

```
// C# Code for Maximum weight path
// ending at any element of last
// row in a matrix
using System;

class GFG {

    /* Function which return the
    maximum weight path sum */
    public static int maxCost(int [,] mat, int N)
    {

        // create 2D matrix to store the
        // sum of the path
        int [,] dp = new int[N,N];

        dp[0,0] = mat[0,0];

        // Initialize first column of total
        // weight array (dp[i to N][0])
        for (int i = 1; i < N; i++)
            dp[i,0] = mat[i,0] + dp[i-1,0];

        // Calculate rest path sum of weight matrix
        for (int i = 1; i < N; i++)
            for (int j = 1; j < i + 1 && j < N; j++)
                dp[i,j] = mat[i,j] +
                   Math.Max(dp[i-1,j-1], dp[i-1,j]);

        // find the max weight path sum to reach
        // the last row
        int result = 0;

        for (int i = 0; i < N; i++)
            if (result < dp[N-1,i])
                result = dp[N-1,i];

        // return maximum weight path sum
        return result;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int [,] mat = { { 4, 1 ,5 ,6 , 1 },
                        { 2 ,9 ,2 ,11 ,10 },
                        { 15,1 ,3 ,15, 2 },
                        { 16, 92, 41,4,3},
                        { 8, 142, 6, 4, 8 }
                      };
        int N = 5;

        Console.Write("Maximum Path Sum : "
                           + maxCost(mat, N));
    }
}

// This code is contributed by KRV.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the path having the
// maximum weight in matrix

/* Function which return the maximum weight
path sum */
function maxCost($mat, $N)
{
    // creat 2D matrix to store the sum of the path
    $dp = array(array()) ;
    //memset(dp, 0, sizeof(dp));

    $dp[0][0] = $mat[0][0];

    // Initialize first column of total weight
    // array (dp[i to N][0])
    for ($i=1; $i<$N; $i++)
        $dp[$i][0] = $mat[$i][0] + $dp[$i-1][0];

    // Calculate rest path sum of weight matrix
    for ($i=1; $i<$N; $i++) {
    for ($j=1; $j<$i+1 && $j<$N; $j++)
        $dp[$i][$j] = $mat[$i][$j] + max($dp[$i-1][$j-1], $dp[$i-1][$j]);
        }
    // find the max weight path sum to rech
    // the last row
    $result = 0;
    for ($i=0; $i<$N; $i++)
        if ($result < $dp[$N-1][$i])
            $result = $dp[$N-1][$i];

    // return maximum weight path sum
    return $result;
}

    // Driver program

$mat = array( array( 4, 1 ,5 ,6 , 1 ),
        array( 2 ,9 ,2 ,11 ,10 ),
        array( 15,1 ,3 ,15, 2 ),
        array( 16, 92, 41,4,3),
        array( 8, 142, 6, 4, 8 ) );

$N = 5;
echo "Maximum Path Sum : ", maxCost($mat, $N) ;

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript Code for Maximum weight path ending at
    // any element of last row in a matrix

    /* Function which return the maximum weight
       path sum */
    function maxCost(mat, N)
    {
        // create 2D matrix to store the sum of
        // the path
        let dp = new Array(N);

        for (let i = 0; i < N; i++)
        {
            dp[i] = new Array(N);
            for (let j = 0; j < N; j++)
            {
                dp[i][j] = 0;
            }
        }

        dp[0][0] = mat[0][0];

        // Initialize first column of total
        // weight array (dp[i to N][0])
        for (let i = 1; i < N; i++)
            dp[i][0] = mat[i][0] + dp[i-1][0];

        // Calculate rest path sum of weight matrix
        for (let i = 1; i < N; i++)
           for (let j = 1; j < i + 1 && j < N; j++)
              dp[i][j] = mat[i][j] +
                        Math.max(dp[i-1][j-1],
                                 dp[i-1][j]);

        // find the max weight path sum to reach
        // the last row
        let result = 0;
        for (let i = 0; i < N; i++)
            if (result < dp[N-1][i])
                result = dp[N-1][i];

        // return maximum weight path sum
        return result;
    }

    let mat = [  [ 4, 1 ,5 ,6 , 1 ],
                 [ 2 ,9 ,2 ,11 ,10 ],
                  [ 15,1 ,3 ,15, 2 ],
                   [ 16, 92, 41,4,3],
                   [ 8, 142, 6, 4, 8 ]
                ];
    let N = 5;
    document.write("Maximum Path Sum : "+
                       maxCost(mat, N));

</script>
```

**输出:**

```
Maximum Path Sum : 255
```

**时间复杂度:** O(N*N)
本文由[**Nishant _ Singh(pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。