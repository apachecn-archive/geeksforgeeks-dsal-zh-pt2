# 倒三角中的最大路径和| SET 2

> 原文:[https://www . geesforgeks . org/最大路径-倒三角求和-集合-2/](https://www.geeksforgeeks.org/maximum-path-sum-in-an-inverted-triangle-set-2/)

给定倒三角形的数字。从三角形的底部开始，移动到上一行的**相邻数字**，从下到上找到最大总数。
**例:**

```
Input : 1 5 3
         4 8
          1
Output : 14

Input : 8 5 9 3
         2 4 6
          7 4
           3
Output : 23
```

**逼近:**在[之前的文章](https://www.geeksforgeeks.org/maximum-path-sum-triangle/)中我们看到了一个三角形不倒的问题的逼近。
在这里我们也将使用相同的方法来寻找问题的解决方案，如在[上一篇文章](https://www.geeksforgeeks.org/maximum-path-sum-triangle/)中所讨论的。
如果我们应该左移每个元素，在每个空位置放 0，使其成为一个规则矩阵，那么我们的问题看起来就像[最小成本路径](https://www.geeksforgeeks.org/min-cost-path-dp-6/)。
因此，在将我们的输入三角形元素转换为规则矩阵后，我们应该应用动态规划概念来寻找最大路径和。
应用，自下而上的 DP 我们应该解决我们的问题如下:
**示例:**

```
8 5 9 3
 2 4 6
  7 4
   3

Step 1 :
8 5 9 3
2 4 6 0
7 4 0 0
3 0 0 0

Step 2 :
8 5 9 3
2 4 6 0
10 7 0 0

Step 3 :
8 5 9 3
12 14 13 0

Step 4:
20 19 23 16

Output : 23
```

以下是上述方法的实现:

## C++

```
// C++ program implementation of
// Max sum problem in a triangle
#include <bits/stdc++.h>
using namespace std;
#define N 3

// Function for finding maximum sum
int maxPathSum(int tri[][N])
{
    int ans = 0;

    // Loop for bottom-up calculation
    for (int i = N - 2; i >= 0; i--) {
        for (int j = 0; j < N - i; j++) {

            // For each element, check both
            // elements just below the number
            // and below left to the number
            // add the maximum of them to it
            if (j - 1 >= 0)
                tri[i][j] += max(tri[i + 1][j],
                                 tri[i + 1][j - 1]);
            else
                tri[i][j] += tri[i + 1][j];

            ans = max(ans, tri[i][j]);
        }
    }

    // Return the maximum sum
    return ans;
}

// Driver Code
int main()
{
    int tri[N][N] = { { 1, 5, 3 },
                      { 4, 8, 0 },
                      { 1, 0, 0 } };

    cout << maxPathSum(tri);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program implementation of
// Max sum problem in a triangle

class GFG
{
    static int N = 3;

    // Function for finding maximum sum
    static int maxPathSum(int tri[][])
    {
        int ans = 0;

        // Loop for bottom-up calculation
        for (int i = N - 2; i >= 0; i--)
        {
            for (int j = 0; j < N - i; j++)
            {

                // For each element, check both
                // elements just below the number
                // and below left to the number
                // add the maximum of them to it
                if (j - 1 >= 0)
                    tri[i][j] += Math.max(tri[i + 1][j],
                                    tri[i + 1][j - 1]);
                else
                    tri[i][j] += tri[i + 1][j];

                ans = Math.max(ans, tri[i][j]);
            }
        }

        // Return the maximum sum
        return ans;
    }

    // Driver Code
    public static void main(String []args)
    {
        int tri[][] = { { 1, 5, 3 },
                        { 4, 8, 0 },
                        { 1, 0, 0 } };

        System.out.println(maxPathSum(tri));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python program implementation of
# Max sum problem in a triangle

N = 3

# Function for finding maximum sum
def maxPathSum( tri ):

    ans = 0;

    # Loop for bottom-up calculation
    for i in range(N - 2, -1, -1):
        for j in range(0 , N - i):

            # For each element, check both
            # elements just below the number
            # and below left to the number
            # add the maximum of them to it
            if (j - 1 >= 0):
                tri[i][j] += max(tri[i + 1][j],
                                tri[i + 1][j - 1]);
            else:
                tri[i][j] += tri[i + 1][j];

            ans = max(ans, tri[i][j]);

    # Return the maximum sum
    return ans

# Driver Code

tri = [ [ 1, 5, 3 ],
        [ 4, 8, 0 ],
        [ 1, 0, 0 ] ]

print(maxPathSum(tri))

# This code is contributed by ihritik
```

## C#

```
// C# program implementation of
// Max sum problem in a triangle
using System;

class GFG
{
    static int N = 3;

    // Function for finding maximum sum
    static int maxPathSum(int [,]tri)
    {
        int ans = 0;

        // Loop for bottom-up calculation
        for (int i = N - 2; i >= 0; i--)
        {
            for (int j = 0; j < N - i; j++)
            {

                // For each element, check both
                // elements just below the number
                // and below left to the number
                // add the maximum of them to it
                if (j - 1 >= 0)
                    tri[i, j] += Math.Max(tri[i + 1, j],
                                    tri[i + 1, j - 1]);
                else
                    tri[i, j] += tri[i + 1, j];

                ans = Math.Max(ans, tri[i, j]);
            }
        }

        // Return the maximum sum
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int[,] tri = { { 1, 5, 3 },
                        { 4, 8, 0 },
                        { 1, 0, 0 } };

        Console.WriteLine(maxPathSum(tri));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program implementation of
// Max sum problem in a triangle

$N = 3;

// Function for finding maximum sum
function maxPathSum($tri)
{
    global $N;
    $ans = 0;

    // Loop for bottom-up calculation
    for ($i = $N - 2; $i >= 0; $i--)
    {
        for ($j = 0; $j < $N - $i; $j++)
        {

            // For each element, check both
            // elements just below the number
            // and below left to the number
            // add the maximum of them to it
            if ($j - 1 >= 0)
                $tri[$i][$j] += max($tri[$i + 1][$j],
                                    $tri[$i + 1][$j - 1]);
            else
                $tri[$i][$j] += $tri[$i + 1][$j];

            $ans = max($ans, $tri[$i][$j]);
        }
    }

    // Return the maximum sum
    return $ans;
}

// Driver Code
$tri = array(array( 1, 5, 3 ),
             array( 4, 8, 0 ),
             array( 1, 0, 0 ));

echo maxPathSum($tri);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
//Javascript program implementation of
// Max sum problem in a triangle

N = 3;

// Function for finding maximum sum
function maxPathSum(tri)
{
    var ans = 0;

    // Loop for bottom-up calculation
    for (var i = N - 2; i >= 0; i--) {
        for (var j = 0; j < N - i; j++) {

            // For each element, check both
            // elements just below the number
            // and below left to the number
            // add the maximum of them to it
            if (j - 1 >= 0)
                tri[i][j] += Math.max(tri[i + 1][j],
                                 tri[i + 1][j - 1]);
            else
                tri[i][j] += tri[i + 1][j];

            ans = Math.max(ans, tri[i][j]);
        }
    }

    // Return the maximum sum
    return ans;
}

    var tri =  [[ 1, 5, 3 ],
                      [ 4, 8, 0 ],
                      [ 1, 0, 0 ]];
    document.write(maxPathSum(tri));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
14
```