# 求所有元素相等的最大平方子矩阵

> 原文:[https://www . geeksforgeeks . org/find-全等元最大平方子矩阵/](https://www.geeksforgeeks.org/finding-the-maximum-square-sub-matrix-with-all-equal-elements/)

给定一个 N×N 矩阵，确定最大 K，使得 K×K 是一个所有元素相等的子矩阵，即这个子矩阵中的所有元素必须相同。
约束:
1<= N<= 1000
0<= A<sub>I，j</sub>T13】= 10<sup>9</sup>
**示例:**

```

Input : a[][] = {{2, 3, 3},
                 {2, 3, 3},
                 {2, 2, 2}}
Output : 2
Explanation: A 2x2 matrix is formed from index
A0,1 to A1,2

Input : a[][]  = {{9, 9, 9, 8},
                  {9, 9, 9, 6},
                  {9, 9, 9, 3},
                  {2, 2, 2, 2}
Output : 3
Explanation : A 3x3 matrix is formed from index
A0,0 to A2,2
```

**方法一(朴素方法)**
我们可以很容易地在 O(n <sup>3</sup> 时间内找到所有的正方形子矩阵，并检查每个子矩阵在 O(n <sup>2</sup> 时间内是否包含相等的元素，这使得算法的总运行时间为 O(n <sup>5</sup> )。
**方法二(动态规划)**
对于每个单元(I，j)，我们存储 K 的最大值，使得 K×K 是所有元素相等的子矩阵，并且(I，j)的位置是最右下的元素。
和 DP <sub>i，j</sub> 取决于{DP <sub>i-1，j</sub> ，DP <sub>i，j-1</sub> ，DP <sub>i-1，j-1</sub> }

```
If Ai, j is equal to {Ai-1, j, Ai, j-1, Ai-1, j-1}, 
   all the three values:
    DPi, j = min(DPi-1, j, DPi, j-1, DPi-1, j-1) + 1
Else
    DPi, j = 1  // Matrix Size 1 

The answer would be the maximum of all DPi, j's
```

下面是以上步骤的实现。

## C++

```
// C++ program to find maximum K such that K x K
// is a submatrix with equal elements.
#include<bits/stdc++.h>
#define Row 6
#define Col 6
using namespace std;

// Returns size of the largest square sub-matrix
// with all same elements.
int largestKSubmatrix(int a[][Col])
{
    int dp[Row][Col];
    memset(dp, sizeof(dp), 0);

    int result = 0;
    for (int i = 0 ; i < Row ; i++)
    {
        for (int j = 0 ; j < Col ; j++)
        {
            // If elements is at top row or first
            // column, it wont form a  square
            // matrix's bottom-right
            if (i == 0 || j == 0)
                dp[i][j] = 1;

            else
            {
                // Check if adjacent elements are equal
                if (a[i][j] == a[i-1][j] &&
                    a[i][j] == a[i][j-1] &&
                    a[i][j] == a[i-1][j-1] )
                    dp[i][j] = min(min(dp[i-1][j], dp[i][j-1]),
                                      dp[i-1][j-1] ) + 1;

                // If not equal, then it will form a 1x1
                // submatrix
                else dp[i][j] = 1;
            }

            // Update result at each (i,j)
            result = max(result, dp[i][j]);
        }
    }

    return result;
}

// Driven Program
int main()
{
    int a[Row][Col] = { 2, 2, 3, 3, 4, 4,
                        5, 5, 7, 7, 7, 4,
                        1, 2, 7, 7, 7, 4,
                        4, 4, 7, 7, 7, 4,
                        5, 5, 5, 1, 2, 7,
                        8, 7, 9, 4, 4, 4
                      };

    cout << largestKSubmatrix(a) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum 
// K such that K x K is a 
// submatrix with equal elements.
class GFG 
{
    static int Row = 6, Col = 6;

    // Returns size of the largest 
    // square sub-matrix with
    // all same elements.
    static int largestKSubmatrix(int [][]a)
    {
        int [][]dp = new int [Row][Col];
        int result = 0;
        for (int i = 0 ; 
                 i < Row ; i++)
        {
            for (int j = 0 ;
                     j < Col ; j++)
            {
                // If elements is at top 
                // row or first column, 
                // it wont form a square
                // matrix's bottom-right
                if (i == 0 || j == 0)
                    dp[i][j] = 1;

                else
                {
                    // Check if adjacent
                    // elements are equal
                    if (a[i][j] == a[i - 1][j] && 
                        a[i][j] == a[i][j - 1] && 
                        a[i][j] == a[i - 1][j - 1])
                    {
                    dp[i][j] = (dp[i - 1][j] > dp[i][j - 1] &&
                                dp[i - 1][j] > dp[i - 1][j - 1] + 1) ? 
                                                        dp[i - 1][j] :
                               (dp[i][j - 1] > dp[i - 1][j] && 
                                dp[i][j - 1] > dp[i - 1][j - 1] + 1) ? 
                                                        dp[i][j - 1] :
                                                 dp[i - 1][j - 1] + 1;
                    }             

                    // If not equal, then it
                    // will form a 1x1 submatrix
                    else dp[i][j] = 1;
                }

                // Update result at each (i,j)
                result = result > dp[i][j] ?
                                    result : dp[i][j];
            }
        }
        return result;
    }

    // Driver code
    public static void main(String[] args) 
    {
        int [][]a = {{2, 2, 3, 3, 4, 4},
                     {5, 5, 7, 7, 7, 4},
                     {1, 2, 7, 7, 7, 4},
                     {4, 4, 7, 7, 7, 4},
                     {5, 5, 5, 1, 2, 7},
                      {8, 7, 9, 4, 4, 4}};

        System.out.println(largestKSubmatrix(a));

    }
}

// This code is contributed
// by ChitraNayal
```

## C#

```
// C# program to find maximum 
// K such that K x K is a
// submatrix with equal elements.
using System;

class GFG 
{
    static int Row = 6, Col = 6;

    // Returns size of the 
    // largest square sub-matrix
    // with all same elements.
    static int largestKSubmatrix(int[,] a)
    {
        int[,] dp = new int [Row, Col];
        int result = 0;
        for (int i = 0 ; i < Row ; i++)
        {
            for (int j = 0 ; 
                     j < Col ; j++)
            {
                // If elements is at top 
                // row or first column, 
                // it wont form a square
                // matrix's bottom-right
                if (i == 0 || j == 0)
                    dp[i, j] = 1;

                else
                {
                    // Check if adjacent 
                    // elements are equal
                    if (a[i, j] == a[i - 1, j] && 
                        a[i, j] == a[i, j - 1] && 
                        a[i, j] == a[i - 1, j - 1])
                    {
                     dp[i, j] = (dp[i - 1, j] > dp[i, j - 1] && 
                                 dp[i - 1, j] > dp[i - 1, j - 1] + 1) ? 
                                                         dp[i - 1, j] : 
                                 (dp[i, j - 1] > dp[i - 1, j] &&
                                  dp[i, j - 1] > dp[i - 1, j - 1] + 1) ? 
                                                          dp[i, j - 1] : 
                                                   dp[i - 1, j - 1] + 1;
                    }             

                    // If not equal, then 
                    // it will form a 1x1
                    // submatrix
                    else dp[i, j] = 1;
                }

                // Update result at each (i,j)
                result = result > dp[i, j] ? 
                                    result : dp[i, j];
            }
        }
        return result;
    }

    // Driver Code
    public static void Main() 
    {
        int[,] a = {{2, 2, 3, 3, 4, 4},
                    {5, 5, 7, 7, 7, 4},
                    {1, 2, 7, 7, 7, 4},
                    {4, 4, 7, 7, 7, 4},
                    {5, 5, 5, 1, 2, 7},
                    {8, 7, 9, 4, 4, 4}};

        Console.Write(largestKSubmatrix(a));
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find 
# maximum K such that K x K
# is a submatrix with equal 
# elements.
Row = 6
Col = 6

# Returns size of the 
# largest square sub-matrix
# with all same elements.
def largestKSubmatrix(a):
    dp = [[0 for x in range(Row)]
             for y in range(Col)]

    result = 0
    for i in range(Row ):
        for j in range(Col):

            # If elements is at top 
            # row or first column, 
            # it wont form a square
            # matrix's bottom-right
            if (i == 0 or j == 0):
                dp[i][j] = 1

            else:

                # Check if adjacent 
                # elements are equal
                if (a[i][j] == a[i - 1][j] and
                    a[i][j] == a[i][j - 1] and
                    a[i][j] == a[i - 1][j - 1]):

                    dp[i][j] = min(min(dp[i - 1][j], 
                                       dp[i][j - 1]),
                                       dp[i - 1][j - 1] ) + 1

                # If not equal, then  
                # it will form a 1x1
                # submatrix
                else:
                    dp[i][j] = 1

            # Update result at each (i,j)
            result = max(result, dp[i][j])

    return result

# Driver Code
a = [[ 2, 2, 3, 3, 4, 4],
     [ 5, 5, 7, 7, 7, 4],
     [ 1, 2, 7, 7, 7, 4],
     [ 4, 4, 7, 7, 7, 4],
     [ 5, 5, 5, 1, 2, 7],
     [ 8, 7, 9, 4, 4, 4]];

print(largestKSubmatrix(a))

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php 
// Java program to find maximum 
// K such that K x K is a
// submatrix with equal elements.
$Row = 6;
$Col = 6;

// Returns size of the largest
// square sub-matrix with 
// all same elements.
function largestKSubmatrix(&$a)
{
    global $Row, $Col;

    $result = 0;
    for ($i = 0 ; 
         $i < $Row ; $i++)
    {
        for ($j = 0 ; 
             $j < $Col ; $j++)
        {
            // If elements is at 
            // top row or first
            // column, it wont form
            // a square matrix's 
            // bottom-right
            if ($i == 0 || $j == 0)
                $dp[$i][$j] = 1;

            else
            {
                // Check if adjacent 
                // elements are equal
                if ($a[$i][$j] == $a[$i - 1][$j] &&
                    $a[$i][$j] == $a[$i][$j - 1] &&
                    $a[$i][$j] == $a[$i - 1][$j - 1] )
                    $dp[$i][$j] = min(min($dp[$i - 1][$j], 
                                          $dp[$i][$j - 1]),
                                          $dp[$i - 1][$j - 1] ) + 1;

                // If not equal, then it 
                // will form a 1x1 submatrix
                else $dp[$i][$j] = 1;
            }

            // Update result at each (i,j)
            $result = max($result, 
                          $dp[$i][$j]);
        }
    }

    return $result;
}

// Driver Code
$a = array(array(2, 2, 3, 3, 4, 4),
           array(5, 5, 7, 7, 7, 4),
           array(1, 2, 7, 7, 7, 4),
           array(4, 4, 7, 7, 7, 4),
           array(5, 5, 5, 1, 2, 7),
           array(8, 7, 9, 4, 4, 4));

echo largestKSubmatrix($a);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum 
// K such that K x K is a 
// submatrix with equal elements.

    let Row = 6, Col = 6;

    // Returns size of the largest 
    // square sub-matrix with
    // all same elements.
    function largestKSubmatrix(a)
    {
        let dp = new Array(Row);
        for(let i = 0; i < Row; i++)
        {
            dp[i] = new Array(Col);
            for(let j = 0; j < Col; j++)
            {
                dp[i][j] = 0;
            }
        }
        let result = 0;
        for (let i = 0 ; 
                 i < Row ; i++)
        {
            for (let j = 0 ;
                     j < Col ; j++)
            {
                // If elements is at top 
                // row or first column, 
                // it wont form a square
                // matrix's bottom-right
                if (i == 0 || j == 0)
                    dp[i][j] = 1;

                else
                {
                    // Check if adjacent
                    // elements are equal
                    if (a[i][j] == a[i - 1][j] && 
                        a[i][j] == a[i][j - 1] && 
                        a[i][j] == a[i - 1][j - 1])
                    {
                    dp[i][j] = (dp[i - 1][j] > dp[i][j - 1] &&
                                dp[i - 1][j] > dp[i - 1][j - 1] + 1) ? 
                                                        dp[i - 1][j] :
                               (dp[i][j - 1] > dp[i - 1][j] && 
                                dp[i][j - 1] > dp[i - 1][j - 1] + 1) ? 
                                                        dp[i][j - 1] :
                                                 dp[i - 1][j - 1] + 1;
                    }             

                    // If not equal, then it
                    // will form a 1x1 submatrix
                    else dp[i][j] = 1;
                }

                // Update result at each (i,j)
                result = result > dp[i][j] ?
                                    result : dp[i][j];
            }
        }
        return result;
    }

    // Driver code
    let a = [[ 2, 2, 3, 3, 4, 4],
     [ 5, 5, 7, 7, 7, 4],
     [ 1, 2, 7, 7, 7, 4],
     [ 4, 4, 7, 7, 7, 4],
     [ 5, 5, 5, 1, 2, 7],
     [ 8, 7, 9, 4, 4, 4]];

    document.write(largestKSubmatrix(a));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
3
```

**时间复杂度:**O(Row * Col)
T3】辅助空间: O(Row * Col)
本文由 **Shubham Gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。