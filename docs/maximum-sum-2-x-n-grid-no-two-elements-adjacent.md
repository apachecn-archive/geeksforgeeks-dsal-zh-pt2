# 2×n 网格中的最大和，使得没有两个元素相邻

> 原文:[https://www . geesforgeks . org/maximum-sum-2-x-n-grid-no-two-elements-相邻/](https://www.geeksforgeeks.org/maximum-sum-2-x-n-grid-no-two-elements-adjacent/)

给定一个 2×n 维的矩形网格，我们需要找出最大和，使得没有两个选择的数字是相邻的，垂直的，对角的，或水平的。
**例:**

```
Input: 1 4 5
       2 0 0
Output: 7
If we start from 1 then we can add only 5 or 0\. 
So max_sum = 6 in this case.
If we select 2 then also we can add only 5 or 0.
So max_sum = 7 in this case.
If we select from 4 or 0  then there is no further 
elements can be added.
So, Max sum is 7.

Input: 1 2 3 4 5
       6 7 8 9 10
Output: 24
```

**进场:**

这个问题是[最大和的扩展，这样就没有两个元素是相邻的](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent)。唯一要更改的是获取特定列的两行的最大元素。考虑两种情况，我们逐列遍历并保持最大和。
1)包含当前列的一个元素。在这种情况下，我们在当前列中最多取两个元素。
2)当前列的一个元素被排除(或不包括)
以下是上述步骤的实现。

## C++

```
// C++ program to find maximum sum in a grid such that
// no two elements are adjacent.
#include<bits/stdc++.h>
#define MAX 1000
using namespace std;

// Function to find max sum without adjacent
int maxSum(int grid[2][MAX], int n)
{
    // Sum including maximum element of first column
    int incl = max(grid[0][0], grid[1][0]);

    // Not including first column's element
    int excl = 0, excl_new;

    // Traverse for further elements
    for (int i = 1; i<n; i++ )
    {
        // Update max_sum on including or excluding
        // of previous column
        excl_new = max(excl, incl);

        // Include current column. Add maximum element
        // from both row of current column
        incl = excl + max(grid[0][i], grid[1][i]);

        // If current column doesn't to be included
        excl = excl_new;
    }

    // Return maximum of excl and incl
    // As that will be the maximum sum
    return max(excl, incl);
}

// Driver code
int main()
{
    int grid[2][MAX] = {{ 1, 2, 3, 4, 5},
                        { 6, 7, 8, 9, 10}};

    int n = 5;
    cout << maxSum(grid, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Maximum sum in a 2 x n grid
// such that no two elements are adjacent
import java.util.*;

class GFG {

    // Function to find max sum without adjacent
    public static int maxSum(int grid[][], int n)
    {
        // Sum including maximum element of first
        // column
        int incl = Math.max(grid[0][0], grid[1][0]);

        // Not including first column's element
        int excl = 0, excl_new;

        // Traverse for further elements
        for (int i = 1; i < n; i++ )
        {
            // Update max_sum on including or
            // excluding of previous column
            excl_new = Math.max(excl, incl);

            // Include current column. Add maximum element
            // from both row of current column
            incl = excl + Math.max(grid[0][i], grid[1][i]);

            // If current column doesn't to be included
            excl = excl_new;
        }

        // Return maximum of excl and incl
        // As that will be the maximum sum
        return Math.max(excl, incl);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int grid[][] = {{ 1, 2, 3, 4, 5},
                         { 6, 7, 8, 9, 10}};

         int n = 5;
         System.out.println(maxSum(grid, n));
    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find maximum sum in a grid such that
# no two elements are adjacent.

# Function to find max sum without adjacent
def maxSum(grid, n) :

    # Sum including maximum element of first column
    incl = max(grid[0][0], grid[1][0])

    # Not including first column's element
    excl = 0 

    # Traverse for further elements
    for i in range(1, n) :

        # Update max_sum on including or excluding
        # of previous column
        excl_new = max(excl, incl)

        # Include current column. Add maximum element
        # from both row of current column
        incl = excl + max(grid[0][i], grid[1][i])

        # If current column doesn't to be included
        excl = excl_new

    # Return maximum of excl and incl
    # As that will be the maximum sum
    return max(excl, incl)

# Driver code
if __name__ == "__main__" :

    grid = [ [ 1, 2, 3, 4, 5],
             [ 6, 7, 8, 9, 10] ]
    n = 5
    print(maxSum(grid, n))

// This code is contributed by Ryuga
```

## C#

```
// C# program Code for Maximum sum
// in a 2 x n grid such that no two
// elements are adjacent
using System;   

class GFG
{

// Function to find max sum
// without adjacent
public static int maxSum(int [,]grid, int n)
{
    // Sum including maximum element
    // of first column
    int incl = Math.Max(grid[0, 0],
                        grid[1, 0]);

    // Not including first column's
    // element
    int excl = 0, excl_new;

    // Traverse for further elements
    for (int i = 1; i < n; i++ )
    {
        // Update max_sum on including or
        // excluding of previous column
        excl_new = Math.Max(excl, incl);

        // Include current column. Add
        // maximum element from both
        // row of current column
        incl = excl + Math.Max(grid[0, i],
                               grid[1, i]);

        // If current column doesn't
        // to be included
        excl = excl_new;
    }

    // Return maximum of excl and incl
    // As that will be the maximum sum
    return Math.Max(excl, incl);
}

// Driver Code
public static void Main(String[] args)
{
    int [,]grid = {{ 1, 2, 3, 4, 5},
                   { 6, 7, 8, 9, 10}};

    int n = 5;
    Console.Write(maxSum(grid, n));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum sum
// in a grid such that no two elements
// are adjacent.

// Function to find max sum
// without adjacent
function maxSum($grid, $n)
{
    // Sum including maximum element
    // of first column
    $incl = max($grid[0][0], $grid[1][0]);

    // Not including first column's element
    $excl = 0;
    $excl_new;

    // Traverse for further elements
    for ($i = 1; $i < $n; $i++ )
    {
        // Update max_sum on including or
        // excluding of previous column
        $excl_new = max($excl, $incl);

        // Include current column. Add maximum
        // element from both row of current column
        $incl = $excl + max($grid[0][$i],
                            $grid[1][$i]);

        // If current column doesn't
        // to be included
        $excl = $excl_new;
    }

    // Return maximum of excl and incl
    // As that will be the maximum sum
    return max($excl, $incl);
}

// Driver code
$grid = array(array(1, 2, 3, 4, 5),
              array(6, 7, 8, 9, 10));

$n = 5;
echo maxSum($grid, $n);

// This code is contributed by Sachin..
?>
```

## java 描述语言

```
<script>

// JavaScript program Code for Maximum sum
// in a 2 x n grid such that no two
// elements are adjacent

// Function to find max sum
// without adjacent
function maxSum(grid,n)
{
    // Sum including maximum element
    // of first column
   let incl = Math.max(grid[0][0], grid[1][0]);

    // Not including first column's
    // element
   let excl = 0, excl_new;

    // Traverse for further elements
    for (let i = 1; i < n; i++ )
    {
        // Update max_sum on including or
        // excluding of previous column
        excl_new = Math.max(excl, incl);

        // Include current column. Add
        // maximum element from both
        // row of current column
        incl = excl + Math.max(grid[0][i], grid[1][i]);

        // If current column doesn't
        // to be included
        excl = excl_new;
    }

    // Return maximum of excl and incl
    // As that will be the maximum sum
    return Math.max(excl, incl);
}

// Driver Code

let grid =[[ 1, 2, 3, 4, 5], [6, 7, 8, 9, 10]];

let n = 5;
document.write(maxSum(grid, n));

// This code is contributed
// by PrinciRaj1992

</script>
```

**输出:**

```
24
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。