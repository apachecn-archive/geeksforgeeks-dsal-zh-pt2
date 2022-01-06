# 直角三角形中路径的最大和

> 原文:[https://www . geesforgeks . org/maximum-sum-path-right-number-triangle/](https://www.geeksforgeeks.org/maximum-sum-path-right-number-triangle/)

给定一个数字的直角三角形，找出从顶部到底部的路径上出现的数字总和中最大的一个，这样在每条路径上，下一个数字就位于正下方或右下方一个位置。
**例:**

```
Input : 1
        1 2
        4 1 2
        2 3 1 1        
Output : 9
Explanation : 1 + 1 + 4 + 3

Input : 2
        4 1
        1 2 7
Output : 10
Explanation : 2 + 1 + 7
```

其思想是找到最后一行每个单元格的最大和，并返回这些和的最大值。我们可以通过递归考虑以上两个单元格来递归计算这些和。由于存在重叠的子问题，我们使用动态规划来寻找在最后一行的特定单元格处结束的最大和。
以下是上述思路的实现。

## C++

```
// C++ program to print maximum sum
// in a right triangle of numbers
#include<bits/stdc++.h>
using namespace std;

// function to find maximum sum path
int maxSum(int tri[][3], int n)
{
    // Adding the element of row 1 to both the
    // elements of row 2 to reduce a step from
    // the loop
    if (n > 1)
        tri[1][1] = tri[1][1] + tri[0][0];
        tri[1][0] = tri[1][0] + tri[0][0];

    // Traverse remaining rows
    for(int i = 2; i < n; i++) {
        tri[i][0] = tri[i][0] + tri[i-1][0];
        tri[i][i] = tri[i][i] + tri[i-1][i-1];

        //Loop to traverse columns
        for (int j = 1; j < i; j++){

            // Checking the two conditions,
            // directly below and below right.
            // Considering the greater one

            // tri[i] would store the possible
            // combinations of sum of the paths
            if (tri[i][j] + tri[i-1][j-1] >=
                            tri[i][j] + tri[i-1][j])

                tri[i][j] = tri[i][j] + tri[i-1][j-1];
            else
                tri[i][j] = tri[i][j]+tri[i-1][j];
        }
    }

    // array at n-1 index (tri[i]) stores
    // all possible adding combination, finding
    // the maximum one out of them
    int max=tri[n-1][0];

    for(int i=1;i<n;i++)
    {
        if(max<tri[n-1][i])
            max=tri[n-1][i];
    }

    return max;
}

// driver program
int main(){

    int tri[3][3] = {{1}, {2,1}, {3,3,2}};

    cout<<maxSum(tri, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print maximum sum
// in a right triangle of numbers
class GFG
{

    // function to find maximum sum path
    static int maxSum(int tri[][], int n)
    {

        // Adding the element of row 1 to both the
        // elements of row 2 to reduce a step from
        // the loop
        if (n > 1)
            tri[1][1] = tri[1][1] + tri[0][0];
            tri[1][0] = tri[1][0] + tri[0][0];

        // Traverse remaining rows
        for(int i = 2; i < n; i++) {
            tri[i][0] = tri[i][0] + tri[i-1][0];
            tri[i][i] = tri[i][i] + tri[i-1][i-1];

            //Loop to traverse columns
            for (int j = 1; j < i; j++){

                // Checking the two conditions,
                // directly below and below right.
                // Considering the greater one

                // tri[i] would store the possible
                // combinations of sum of the paths
                if (tri[i][j] + tri[i-1][j-1] >=
                           tri[i][j] + tri[i-1][j])

                    tri[i][j] = tri[i][j]
                                  + tri[i-1][j-1];

                else
                    tri[i][j] = tri[i][j]
                                    + tri[i-1][j];
            }
        }

        // array at n-1 index (tri[i]) stores
        // all possible adding combination,
        // finding the maximum one out of them
        int max = tri[n-1][0];

        for(int i = 1; i < n; i++)
        {
            if(max < tri[n-1][i])
                max = tri[n-1][i];
        }

        return max;
    }

    // Driver code
    public static void main (String[] args)
    {
        int tri[][] = {{1}, {2,1}, {3,3,2}};

        System.out.println(maxSum(tri, 3));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to print maximum sum
# in a right triangle of numbers.

# tri[][] is a 2D array that stores the
# triangle, n is number of lines or rows.
def maxSum(tri, n):

    # Adding the element of row 1 to both the
    # elements of row 2 to reduce a step from
    # the loop
    if n > 1:
        tri[1][1] = tri[1][1]+tri[0][0]
        tri[1][0] = tri[1][0]+tri[0][0]

    # Traverse remaining rows
    for i in range(2, n):
        tri[i][0] = tri[i][0] + tri[i-1][0]
        tri[i][i] = tri[i][i] + tri[i-1][i-1]

        # Loop to traverse columns
        for j in range(1, i):

            # Checking the two conditions, directly below
            # and below right. Considering the greater one

            # tri[i] would store the possible combinations
            # of sum of the paths
            if tri[i][j]+tri[i-1][j-1] >= tri[i][j]+tri[i-1][j]:
                tri[i][j] = tri[i][j] + tri[i-1][j-1]
            else:
                tri[i][j] = tri[i][j]+tri[i-1][j]

    # array at n-1 index (tri[i]) stores all possible
    # adding combination, finding the maximum one
    # out of them
    print max(tri[n-1])

# driver program
tri = [[1], [2,1], [3,3,2]]
maxSum(tri, 3)
```

## C#

```
// C# program to print
// maximum sum in a right
// triangle of numbers
using System;

class GFG
{

    // function to find
    // maximum sum path
    static int maxSum(int [,]tri,
                      int n)
    {

        // Adding the element of row 1
        // to both the elements of row 2
        // to reduce a step from the loop
        if (n > 1)
            tri[1, 1] = tri[1, 1] +
                        tri[0, 0];
            tri[1, 0] = tri[1, 0] +
                        tri[0, 0];

        // Traverse remaining rows
        for(int i = 2; i < n; i++)
        {
            tri[i, 0] = tri[i, 0] +
                        tri[i - 1, 0];
            tri[i, i] = tri[i, i] +
                        tri[i - 1, i - 1];

            //Loop to traverse columns
            for (int j = 1; j < i; j++)
            {

                // Checking the two conditions,
                // directly below and below right.
                // Considering the greater one

                // tri[i] would store the possible
                // combinations of sum of the paths
                if (tri[i, j] + tri[i - 1, j - 1] >=
                    tri[i, j] + tri[i - 1, j])

                    tri[i, j] = tri[i, j] +
                                tri[i - 1, j - 1];

                else
                    tri[i, j] = tri[i, j] +
                                tri[i - 1, j];
            }
        }

        // array at n-1 index (tri[i])
        // stores all possible adding
        // combination, finding the
        // maximum one out of them
        int max = tri[n - 1, 0];

        for(int i = 1; i < n; i++)
        {
            if(max < tri[n - 1, i])
                max = tri[n - 1, i];
        }

        return max;
    }

// Driver Code
public static void Main ()
{

        int [,]tri = {{1,0,0},
                      {2,1,0},
                      {3,3,2}};

        Console.Write(maxSum(tri, 3));
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print maximum sum
// in a right triangle of numbers

// function to find maximum sum path
function maxSum($tri, $n)
{
    // Adding the element of row 1
    // to both the elements of row
    // 2 to reduce a step from the loop
    if ($n > 1)
        $tri[1][1] = $tri[1][1] + $tri[0][0];
        $tri[1][0] = $tri[1][0] + $tri[0][0];

    // Traverse remaining rows
    for($i = 2; $i < $n; $i++)
    {
        $tri[$i][0] = $tri[$i][0] +
                      $tri[$i - 1][0];
        $tri[$i][$i] = $tri[$i][$i] +
                       $tri[$i - 1][$i - 1];

        //Loop to traverse columns
        for ($j = 1; $j < $i; $j++)
        {

            // Checking the two conditions,
            // directly below and below right.
            // Considering the greater one

            // tri[i] would store the possible
            // combinations of sum of the paths
            if ($tri[$i][$j] + $tri[$i - 1][$j - 1] >=
                 $tri[$i][$j] + $tri[$i - 1][$j])

                $tri[$i][$j] = $tri[$i][$j] +
                               $tri[$i - 1][$j - 1];
            else
                $tri[$i][$j] = $tri[$i][$j] +
                               $tri[$i - 1][$j];
        }
    }

    // array at n-1 index (tri[i])
    // stores all possible adding
    // combination, finding the
    // maximum one out of them

    $max = $tri[$n - 1][0];

    for($i = 1; $i < $n; $i++)
    {
        if($max < $tri[$n - 1][$i])
            $max = $tri[$n - 1][$i];
    }

    return $max;
}

// Driver Code
$tri = array(array(1),
             array(2,1),
             array(3,3,2));

echo maxSum($tri, 3);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to print maximum sum
    // in a right triangle of numbers

    // function to find maximum sum path
    function maxSum(tri, n)
    {

        // Adding the element of row 1 to both the
        // elements of row 2 to reduce a step from
        // the loop
        if (n > 1)
            tri[1][1] = tri[1][1] + tri[0][0];
            tri[1][0] = tri[1][0] + tri[0][0];

        // Traverse remaining rows
        for(let i = 2; i < n; i++) {
            tri[i][0] = tri[i][0] + tri[i-1][0];
            tri[i][i] = tri[i][i] + tri[i-1][i-1];

            // Loop to traverse columns
            for (let j = 1; j < i; j++){

                // Checking the two conditions,
                // directly below and below right.
                // Considering the greater one

                // tri[i] would store the possible
                // combinations of sum of the paths
                if (tri[i][j] + tri[i-1][j-1] >=
                           tri[i][j] + tri[i-1][j])

                    tri[i][j] = tri[i][j]
                                  + tri[i-1][j-1];

                else
                    tri[i][j] = tri[i][j]
                                    + tri[i-1][j];
            }
        }

        // array at n-1 index (tri[i]) stores
        // all possible adding combination,
        // finding the maximum one out of them
        let max = tri[n-1][0];

        for(let i = 1; i < n; i++)
        {
            if(max < tri[n-1][i])
                max = tri[n-1][i];
        }

        return max;
    }

    let tri = [[1], [2,1], [3,3,2]];

      document.write(maxSum(tri, 3));

</script>
```

**输出:**

```
6
```

本文由 **Harshit Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。