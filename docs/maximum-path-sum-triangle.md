# 三角形中的最大路径和。

> 原文:[https://www.geeksforgeeks.org/maximum-path-sum-triangle/](https://www.geeksforgeeks.org/maximum-path-sum-triangle/)

我们已经以三角形的形式给出了数字，从三角形的顶部开始，移动到下面一行的相邻数字，从上到下找到最大总数。
**例:**

```
Input : 
   3
  7 4
 2 4 6
8 5 9 3
Output : 23
Explanation : 3 + 7 + 4 + 9 = 23 

Input :
   8
 -4 4
 2 2 6
1 1 1 1
Output : 19
Explanation : 8 + 4 + 6 + 1 = 19 
```

我们可以通过检查每一条可能的路径来完成这种蛮力，但是这需要很长时间，所以我们应该尝试在动态编程的帮助下解决这个问题，这样可以降低时间复杂度。
如果我们应该左移每个元素，在每个空位置放 0，使其成为一个正则矩阵，那么我们的问题看起来就像[最小代价路径。](https://www.geeksforgeeks.org/dynamic-programming-set-6-min-cost-path/)
因此，在将我们的输入三角形元素转换成规则矩阵后，我们应该应用动态规划概念来找到最大路径和。
应用，DP 自下而上的方式我们应该解决我们的问题如下:
**例:**

```
   3
  7 4
 2 4 6
8 5 9 3

Step 1 :
3 0 0 0
7 4 0 0
2 4 6 0
8 5 9 3

Step 2 :
3  0  0  0
7  4  0  0
10 13 15 0

Step 3 :
3  0  0  0
20 19 0  0

Step 4:
23 0 0 0

output : 23
```

## C++

```
// C++ program for Dynamic
// Programming implementation of
// Max sum problem in a triangle
#include<bits/stdc++.h>
using namespace std;
#define N 3

//  Function for finding maximum sum
int maxPathSum(int tri[][N], int m, int n)
{
     // loop for bottom-up calculation
     for (int i=m-1; i>=0; i--)
     {
        for (int j=0; j<=i; j++)
        {
            // for each element, check both
            // elements just below the number
            // and below right to the number
            // add the maximum of them to it
            if (tri[i+1][j] > tri[i+1][j+1])
                tri[i][j] += tri[i+1][j];
            else
                tri[i][j] += tri[i+1][j+1];
        }
     }

     // return the top element
     // which stores the maximum sum
     return tri[0][0];
}

/* Driver program to test above functions */
int main()
{
   int tri[N][N] = {  {1, 0, 0},
                      {4, 8, 0},
                      {1, 5, 3} };
   cout << maxPathSum(tri, 2, 2);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for Dynamic
// Programming implementation of
// Max sum problem in a triangle
import java.io.*;

class GFG {

    static int N = 3;

    // Function for finding maximum sum
    static int maxPathSum(int tri[][], int m, int n)
    {
        // loop for bottom-up calculation
        for (int i = m - 1; i >= 0; i--)
        {
            for (int j = 0; j <= i; j++)
            {
                // for each element, check both
                // elements just below the number
                // and below right to the number
                // add the maximum of them to it
                if (tri[i + 1][j] > tri[i + 1][j + 1])
                    tri[i][j] += tri[i + 1][j];
                else
                    tri[i][j] += tri[i + 1][j + 1];
            }
        }

        // return the top element
        // which stores the maximum sum
        return tri[0][0];
    }

    /* Driver program to test above functions */
    public static void main (String[] args)
    {
        int tri[][] = { {1, 0, 0},
                        {4, 8, 0},
                        {1, 5, 3} };
        System.out.println ( maxPathSum(tri, 2, 2));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program for
# Dynamic Programming
# implementation of Max
# sum problem in a
# triangle

N = 3

# Function for finding maximum sum
def maxPathSum(tri, m, n):

    # loop for bottom-up calculation
    for i in range(m-1, -1, -1):
        for j in range(i+1):

            # for each element, check both
            # elements just below the number
            # and below right to the number
            # add the maximum of them to it
            if (tri[i+1][j] > tri[i+1][j+1]):
                tri[i][j] += tri[i+1][j]
            else:
                tri[i][j] += tri[i+1][j+1]

    # return the top element
    # which stores the maximum sum
    return tri[0][0]

# Driver program to test above function

tri = [[1, 0, 0],
       [4, 8, 0],
       [1, 5, 3]]
print(maxPathSum(tri, 2, 2))

# This code is contributed
# by Soumen Ghosh.
```

## C#

```
// C# Program for Dynamic Programming
// implementation of Max sum problem
// in a triangle
using System;

class GFG {

    // Function for finding maximum sum
    static int maxPathSum(int [,]tri,
                          int m, int n)
    {
        // loop for bottom-up calculation
        for (int i = m - 1; i >= 0; i--)
        {
            for (int j = 0; j <= i; j++)
            {
                // for each element,
                // check both elements
                // just below the number
                // and below right to
                // the number add the
                // maximum of them to it
                if (tri[i + 1,j] >
                       tri[i + 1,j + 1])
                    tri[i,j] +=
                           tri[i + 1,j];
                else
                    tri[i,j] +=
                       tri[i + 1,j + 1];
            }
        }

        // return the top element
        // which stores the maximum sum
        return tri[0,0];
    }

    /* Driver program to test above
    functions */
    public static void Main ()
    {
        int [,]tri = { {1, 0, 0},
                        {4, 8, 0},
                        {1, 5, 3} };

        Console.Write (
             maxPathSum(tri, 2, 2));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Dynamic
// Programming implementation of
// Max sum problem in a triangle

// Function for finding
// maximum sum
function maxPathSum($tri, $m, $n)
{
    // loop for bottom-up
    // calculation
    for ( $i = $m - 1; $i >= 0; $i--)
    {
        for ($j = 0; $j <= $i; $j++)
        {
            // for each element, check
            // both elements just below
            // the number and below right
            // to the number add the maximum
            // of them to it
            if ($tri[$i + 1][$j] > $tri[$i + 1]
                                       [$j + 1])
                $tri[$i][$j] += $tri[$i + 1][$j];
            else
                $tri[$i][$j] += $tri[$i + 1]
                                    [$j + 1];
        }
    }

    // return the top element
    // which stores the maximum sum
    return $tri[0][0];
}

// Driver Code
$tri= array(array(1, 0, 0),
            array(4, 8, 0),
            array(1, 5, 3));
echo maxPathSum($tri, 2, 2);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript Program for Dynamic
// Programming implementation of
// Max sum problem in a triangle
    let N = 3;

    // Function for finding maximum sum
    function maxPathSum(tri, m, n)
    {

        // loop for bottom-up calculation
        for (let i = m - 1; i >= 0; i--)
        {
            for (let j = 0; j <= i; j++)
            {

                // for each element, check both
                // elements just below the number
                // and below right to the number
                // add the maximum of them to it
                if (tri[i + 1][j] > tri[i + 1][j + 1])
                    tri[i][j] += tri[i + 1][j];
                else
                    tri[i][j] += tri[i + 1][j + 1];
            }
        }

        // return the top element
        // which stores the maximum sum
        return tri[0][0];
    }

// Driver code   
    let tri = [[1, 0, 0],
                  [4, 8, 0],
                  [1, 5, 3]];
       document.write( maxPathSum(tri, 2, 2));

// This code is contributed by susmitakundugoaldanga.           
</script>
```

**输出:**

```
14
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。