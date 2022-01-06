# 从第 0 行的任何单元格开始到第(N-1)行的任何单元格结束的最大路径总和

> 原文:[https://www . geesforgeks . org/max-path-sum-start-cell-0-row-end-cell-n-1-row/](https://www.geeksforgeeks.org/maximum-path-sum-starting-cell-0-th-row-ending-cell-n-1-th-row/)

给定一个正整数的矩阵矩阵。从单元(I，j)
只有三种可能的移动

1.  (i+1，j)
2.  (i+1，j-1)
3.  (i+1，j+1)

从第 0 行的任何一列开始，返回到第 N-1 行的所有路径的最大和。
**例:**

```
Input : mat[4][4] = { {4, 2, 3, 4},
                      {2, 9, 1, 10},
                      {15, 1, 3, 0},
                      {16, 92, 41, 44} };
Output :120
path : 4 + 9 + 15 + 92 = 120 
```

问于:**亚马逊采访**

上述问题可以递归定义。
设初始位置为 maximumpathssum(N-1，j)，其中 j 从 0 到 N-1 不等。我们返回开始遍历所有路径之间的最大值(N-1，j) [其中 j 从 0 到 N-1 变化]

```
i = N-1, j = 0 to N -1
int MaximumPath(Mat[][N], I, j)

  // IF we reached to first row of 
  // matrix then return value of that 
  // element  
  IF ( i == 0 && j = 0 )
  return    Mat[i][j]

  // out of matrix bound 
  IF( i = N || j < 0 )
   return 0;

  // call all rest position that we reached
  // from current position and find maximum 
  // between them and add current value in 
  // that path 
  return max(MaximumPath(Mat, i-1, j), 
             MaximumPath(Mat, i-1, j-1), 
             MaximumPath(Mat, i-1, j+1)))
             + Mat[i][j];
```

如果画出上述递归解的递归树，可以观察到[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。由于问题有重叠的子问题，我们可以使用动态规划来有效地解决它。下面是基于动态规划的解决方案。

## C++

```
// C++ program to find Maximum path sum
// start any column in row '0' and ends
// up to any column in row 'n-1'
#include<bits/stdc++.h>
using namespace std;
#define N 4

// function find maximum sum path
int MaximumPath(int Mat[][N])
{
    int result = 0 ;

    // create 2D matrix to store the sum
    // of the path
    int dp[N][N+2];

    // initialize all dp matrix as '0'
    memset(dp, 0, sizeof(dp));

    // copy all element of first column into
    // 'dp' first column
    for (int i = 0 ; i < N ; i++)
        dp[0][i+1] = Mat[0][i];

    for (int i = 1 ; i < N ; i++)
        for (int j = 1 ; j <= N ; j++)
            dp[i][j] = max(dp[i-1][j-1],
                           max(dp[i-1][j],
                               dp[i-1][j+1])) +
                       Mat[i][j-1] ;

    // Find maximum path sum that end ups
    // at  any column of last row 'N-1'
    for (int i=0; i<=N; i++)
        result = max(result, dp[N-1][i]);

    // return maximum sum path
    return result ;
}

// driver program to test above function
int main()
{
    int Mat[4][4] = { { 4, 2 , 3 , 4 },
        { 2 , 9 , 1 , 10},
        { 15, 1 , 3 , 0 },
        { 16 ,92, 41, 44 }
    };

    cout << MaximumPath ( Mat ) <<endl ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Maximum path sum
// start any column in row '0' and ends
// up to any column in row 'n-1'
import java.util.*;

class GFG {

    static int N = 4;

    // function find maximum sum path
    static int MaximumPath(int Mat[][])
    {
        int result = 0;

        // create 2D matrix to store the sum
        // of the path
        int dp[][] = new int[N][N + 2];

        // initialize all dp matrix as '0'
        for (int[] rows : dp)
            Arrays.fill(rows, 0);

        // copy all element of first column into
        // 'dp' first column
        for (int i = 0; i < N; i++)
            dp[0][i + 1] = Mat[0][i];

        for (int i = 1; i < N; i++)
            for (int j = 1; j <= N; j++)
                dp[i][j] = Math.max(dp[i - 1][j - 1],
                                    Math.max(dp[i - 1][j],
                                    dp[i - 1][j + 1])) +
                                    Mat[i][j - 1];

        // Find maximum path sum that end ups
        // at any column of last row 'N-1'
        for (int i = 0; i <= N; i++)
            result = Math.max(result, dp[N - 1][i]);

        // return maximum sum path
        return result;
    }

    // driver code
    public static void main(String arg[])
    {
        int Mat[][] = { { 4, 2, 3, 4 },
                        { 2, 9, 1, 10 },
                        { 15, 1, 3, 0 },
                        { 16, 92, 41, 44 } };

        System.out.println(MaximumPath(Mat));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# Maximum path sum
# start any column in
# row '0' and ends
# up to any column in row 'n-1'

N = 4

# function find maximum sum path
def MaximumPath(Mat):

    result = 0

    # create 2D matrix to store the sum
    # of the path
    # initialize all dp matrix as '0'
    dp = [[0 for i in range(N+2)] for j in range(N)]

    # copy all element of first column into
    # dp first column
    for i in range(N):
        for j in range(1, N+1):
            dp[i][j] = max(dp[i-1][j-1],
                           max(dp[i-1][j],
                               dp[i-1][j+1])) + \
                       Mat[i][j-1]

    # Find maximum path sum that end ups
    # at any column of last row 'N-1'
    for i in range(N+1):
        result = max(result, dp[N-1][i])

    # return maximum sum path
    return result

# driver program to test above function
Mat = [[4, 2, 3, 4],
       [2, 9, 1, 10],
       [15, 1, 3, 0],
       [16, 92, 41, 44]]

print(MaximumPath(Mat))

# This code is contributed by Soumen Ghosh.
```

## C#

```
// C# program to find Maximum path sum
// start any column in row '0' and ends
// up to any column in row 'n-1'
using System;

class GFG {

    static int N = 4;

    // function find maximum sum path
    static int MaximumPath(int [,] Mat)
    {
        int result = 0;

        // create 2D matrix to store the sum
        // of the path
        int [,]dp = new int[N,N + 2];

        // initialize all dp matrix as '0'
        //for (int[] rows : dp)
        //    Arrays.fill(rows, 0);

        // copy all element of first column into
        // 'dp' first column
        for (int i = 0; i < N; i++)
            dp[0,i + 1] = Mat[0,i];

        for (int i = 1; i < N; i++)
            for (int j = 1; j <= N; j++)
                dp[i,j] = Math.Max(dp[i - 1,j - 1],
                                    Math.Max(dp[i - 1,j],
                                    dp[i - 1,j + 1])) +
                                    Mat[i,j - 1];

        // Find maximum path sum that end ups
        // at any column of last row 'N-1'
        for (int i = 0; i <= N; i++)
            result = Math.Max(result, dp[N - 1,i]);

        // return maximum sum path
        return result;
    }

    // driver code
    public static void Main()
    {
        int [,]Mat = { { 4, 2, 3, 4 },
                        { 2, 9, 1, 10 },
                        { 15, 1, 3, 0 },
                        { 16, 92, 41, 44 } };

        Console.WriteLine(MaximumPath(Mat));
    }
}

// This code is contributed by Ryuga.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Maximum path sum
// start any column in row '0' and ends
// up to any column in row 'n-1'
$N = 4;

// function find maximum sum path
function MaximumPath(&$Mat)
{
    global $N;
    $result = 0;

    // create 2D matrix to store the sum
    // of the path
    $dp = array_fill(0, $N,
          array_fill(0, $N + 2, NULL));

    // copy all element of first column
    // into 'dp' first column
    for ($i = 0 ; $i < $N ; $i++)
        $dp[0][$i + 1] = $Mat[0][$i];

    for ($i = 1 ; $i < $N ; $i++)
        for ($j = 1 ; $j <= $N ; $j++)
            $dp[$i][$j] = max($dp[$i - 1][$j - 1],
                          max($dp[$i - 1][$j],
                              $dp[$i - 1][$j + 1])) +
                              $Mat[$i][$j - 1] ;

    // Find maximum path sum that end ups
    // at any column of last row 'N-1'
    for ($i = 0; $i <= $N; $i++)
        $result = max($result, $dp[$N - 1][$i]);

    // return maximum sum path
    return $result ;
}

// Driver Code
$Mat = array(array(4, 2 , 3 , 4),
             array(2 , 9 , 1 , 10),
             array(15, 1 , 3 , 0),
             array(16 ,92, 41, 44));

echo MaximumPath ($Mat) . "\n" ;

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find Maximum path sum
// start any column in row '0' and ends
// up to any column in row 'n-1'

    let N = 4;

    // function find maximum sum path
    function MaximumPath(Mat)
    {
        let result = 0;

        // create 2D matrix to store the sum
        // of the path
        let dp = new Array(N);

        // initialize all dp matrix as '0'
        for(let i=0;i<N;i++)
        {
            dp[i]=new Array(N+2);
            for(let j=0;j<N+2;j++)
            {
                dp[i][j]=0;
            }
        }

        // copy all element of first column into
        // 'dp' first column
        for (let i = 0; i < N; i++)
            dp[0][i + 1] = Mat[0][i];

        for (let i = 1; i < N; i++)
            for (let j = 1; j <= N; j++)
                dp[i][j] = Math.max(dp[i - 1][j - 1],
                                    Math.max(dp[i - 1][j],
                                    dp[i - 1][j + 1])) +
                                    Mat[i][j - 1];

        // Find maximum path sum that end ups
        // at any column of last row 'N-1'
        for (let i = 0; i <= N; i++)
            result = Math.max(result, dp[N - 1][i]);

        // return maximum sum path
        return result;
    }

    // driver code
    let Mat = [[4, 2, 3, 4],
       [2, 9, 1, 10],
       [15, 1, 3, 0],
       [16, 92, 41, 44]]
    document.write(MaximumPath(Mat))

    // This code is contributed by rag2127

</script>
```

**输出:**

```
120
```

**时间复杂度:** O(N <sup>2</sup> )
本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。