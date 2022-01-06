# 二进制矩阵中的最大十进制值路径

> 原文:[https://www . geesforgeks . org/最大十进制值二进制矩阵路径/](https://www.geeksforgeeks.org/maximum-decimal-value-path-in-a-binary-matrix/)

给定二进制方阵[n*n]。在从左上角到右下角的路径中查找最大整数值。我们使用遍历路径的位来计算整数值。我们从索引[0，0]开始，到索引[n-1][n-1]结束。从索引[i，j]，我们可以移动[i，j+1]或[i+1，j]。

示例:

```
Input : mat[][] = {{1, 1, 0, 1},
                   {0, 1, 1, 0},
                   {1, 0, 0, 1},
                   {1, 0, 1, 1}}
Output : 111
Explanation : 
Path :   (0,0) -> (0,1) -> (1,1) -> (1,2) ->
         (2,2) -> (3,2) ->(3,3)  
Decimal value : 1*(2^0) + 1*(2^1) + 1*(2^2) + 1*(2^3) + 
                0*(2^4) + 1*(2^5) + 1*(2^6) = 111
```

上述问题可以递归定义如下:

```
// p indicates power of 2, initially  p = i = j = 0
MaxDecimalValue(mat, i, j, p) 

   // If i or j is our of boundary
   If i >= n || j >= n  
      return 0

   // Compute rest of matrix find maximum decimal value 
   result  max(MaxDecimalValue(mat, i, j+1, p+1), 
               MaxDecimalValue(mat, i+1, j, p+1))

   If mat[i][j] == 1  
      return power(2, p) + result
   Else
      return result 
```

下面是上面递归算法的实现。

## C++

```

// C++ program to find maximum decimal value path in
// binary matrix
#include<bits/stdc++.h>
using namespace std;

#define N 4

// Returns maximum decimal value in binary matrix.
// Here p indicate power of 2
long long int maxDecimalValue(int mat[][N], int i, int j,
                                                   int p)
{
    // Out of matrix boundary
    if (i >= N || j >= N )
        return 0;

    int result = max(maxDecimalValue(mat, i, j+1, p+1),
                     maxDecimalValue(mat, i+1, j, p+1));

    // If current matrix value is 1 then return result +
    // power(2, p) else result
    if (mat[i][j] == 1)
        return pow(2, p) + result;
    else
        return result;
}

//Driver program
int main()
{
    int mat[][4] = {{ 1 ,1 ,0 ,1 },
        { 0 ,1 ,1 ,0 },
        { 1 ,0 ,0 ,1 },
        { 1 ,0 ,1 ,1 },
    };

    cout << maxDecimalValue(mat, 0, 0, 0) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum decimal value path in
// binary matrix

class GFG {

    static final int N = 4;

// Returns maximum decimal value in binary matrix.
// Here p indicate power of 2
    static int maxDecimalValue(int mat[][], int i, int j,
            int p) {
        // Out of matrix boundary
        if (i >= N || j >= N) {
            return 0;
        }

        int result = Math.max(maxDecimalValue(mat, i, j + 1, p + 1),
                maxDecimalValue(mat, i + 1, j, p + 1));

        // If current matrix value is 1 then return result +
        // power(2, p) else result
        if (mat[i][j] == 1) {
            return (int) (Math.pow(2, p) + result);
        } else {
            return result;
        }
    }

// Driver program
    public static void main(String[] args) {
        int mat[][] = {{1, 1, 0, 1},
        {0, 1, 1, 0},
        {1, 0, 0, 1},
        {1, 0, 1, 1},};

        System.out.println(maxDecimalValue(mat, 0, 0, 0));
    }
}
//this code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find maximum decimal
# value path in binary matrix
N =4

# Returns maximum decimal value in binary
# matrix. Here p indicate power of 2
def maxDecimalValue(mat, i, j, p):

    # Out of matrix boundary
    if i >= N or j >= N:
        return 0

    result = max(
        maxDecimalValue(mat, i, j+1, p+1),
        maxDecimalValue(mat, i+1, j, p+1))

    # If current matrix value is 1 then
    # return result + power(2, p) else
    # result
    if mat[i][j] == 1:
        return pow(2, p) + result
    else:
        return result

# Driver Program
mat = [ [1, 1, 0, 1],
        [0, 1, 1, 0],
        [1, 0, 0, 1],
        [1, 0, 1, 1] ]

print(maxDecimalValue(mat, 0, 0, 0))

# This code is contributed by Shrikant13.
```

## C#

```
// C# program to find maximum decimal value path in
// binary matrix

using System;
class GFG {

    static int N = 4;

// Returns maximum decimal value in binary matrix.
// Here p indicate power of 2
    static int maxDecimalValue(int[,] mat, int i,
                                int j,int p)
    {
        // Out of matrix boundary
        if (i >= N || j >= N) {
            return 0;
        }

        int result = Math.Max(maxDecimalValue(mat, i, j + 1, p + 1),
                    maxDecimalValue(mat, i + 1, j, p + 1));

        // If current matrix value is 1 then return result +
        // power(2, p) else result
        if (mat[i,j] == 1)
        {
            return (int) (Math.Pow(2, p) + result);
        } else
        {
            return result;
        }
    }

// Driver program
    public static void Main() {
        int[,] mat = {{1, 1, 0, 1},
        {0, 1, 1, 0},
        {1, 0, 0, 1},
        {1, 0, 1, 1},};

        Console.Write(maxDecimalValue(mat, 0, 0, 0));
    }
}
// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// decimal value path in binary
// matrix

// Returns maximum decimal value
// in binary matrix. Here p
// indicate power of 2
function maxDecimalValue($mat, $i,
                          $j, $p)
{
    $N=4;

    // Out of matrix boundary
    if ($i >= $N || $j >= $N )
        return 0;

    $result = max(maxDecimalValue($mat, $i,
                            $j + 1, $p + 1),
                  maxDecimalValue($mat, $i + 1,
                                $j, $p + 1));

    // If current matrix value
    // is 1 then return result +
    // power(2, p) else result
    if ($mat[$i][$j] == 1)
        return pow(2, $p) + $result;
    else
        return $result;
}

    // Driver Code
    $mat = array(array(1 ,1 ,0 ,1),
                 array(0 ,1 ,1 ,0),
                 array(1 ,0 ,0 ,1),
                 array(1 ,0 ,1 ,1));

    echo maxDecimalValue($mat, 0, 0, 0) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum
// decimal value path in binary matrix
let N = 4;

// Returns maximum decimal value in
// binary matrix.Here p indicate power of 2
function maxDecimalValue(mat, i, j, p)
{

    // Out of matrix boundary
    if (i >= N || j >= N)
    {
        return 0;
    }

    let result = Math.max(maxDecimalValue(mat, i, j + 1,
                                                  p + 1),
                          maxDecimalValue(mat, i + 1, j,
                                               p + 1));

    // If current matrix value is 1 then
    // return result + power(2, p) else result
    if (mat[i][j] == 1)
    {
        return (Math.pow(2, p) + result);
    }
    else
    {
        return result;
    }
}

// Driver Code
let mat = [ [ 1, 1, 0, 1 ],
            [ 0, 1, 1, 0 ],
            [ 1, 0, 0, 1 ],
            [ 1, 0, 1, 1 ] ];

document.write(maxDecimalValue(mat, 0, 0, 0));

// This code is contributed by souravghosh0416            

</script>
```

**输出:**

```
111
```

上述递归解的时间复杂度为**指数**。

```
 Here matrix [3][3]               
            (2 2)
          /        \
     (1 2)          (2 1)
    /     \        /     \
 (0 2)   (1 1)   (1 1)   (2 1)
 /  \    /   \    /  \    / \ 
.    .  .    .    .   .   .  .
.    .  .    .    .   .   .  . and so no 
```

如果看到上面递归解的递归树，可以观察到[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。由于问题有重叠的子问题，我们可以使用动态规划来有效地解决它。下面是基于动态规划的解决方案。

下面是使用动态编程实现上述问题

## C++

```
// C++ program to find Maximum decimal value Path in
// Binary matrix
#include<bits/stdc++.h>
using namespace std;
#define N 4

// Returns maximum decimal value in binary matrix.
// Here p indicate power of 2
long long int MaximumDecimalValue(int mat[][N], int n)
{
    int dp[n][n];
    memset(dp, 0, sizeof(dp));
    if (mat[0][0] == 1)
        dp[0][0] = 1 ; // 1*(2^0)

    // Compute binary stream of first row of matrix
    // and store result in dp[0][i]
    for (int i=1; i<n; i++)
    {
        // indicate 1*(2^i) + result of previous
        if (mat[0][i] == 1)
            dp[0][i] = dp[0][i-1] + pow(2, i);

        // indicate 0*(2^i) + result of previous
        else
            dp[0][i] = dp[0][i-1];
    }

    // Compute binary stream of first column of matrix
    // and store result in dp[i][0]
    for (int i = 1 ; i <n ; i++ )
    {
        // indicate 1*(2^i) + result of previous
        if (mat[i][0] == 1)
            dp[i][0] = dp[i-1][0] + pow(2, i);

        // indicate 0*(2^i) + result of previous
        else
            dp[i][0] = dp[i-1][0];
    }

    // Traversal rest Binary matrix and Compute maximum
    // decimal value
    for (int i=1 ; i < n ; i++ )
    {
        for (int j=1 ; j < n ; j++ )
        {
            // Here (i+j) indicate the current power of
            // 2 in path that is 2^(i+j)
            if (mat[i][j] == 1)
                dp[i][j] = max(dp[i][j-1], dp[i-1][j]) +
                                             pow(2, i+j);
            else
                dp[i][j] = max(dp[i][j-1], dp[i-1][j]);
        }
     }

    // Return maximum decimal value in binary matrix
    return dp[n-1][n-1];
}

// Driver program
int main()
{
    int mat[][4] = {{ 1 ,1 ,0 ,1 },
        { 0 ,1 ,1 ,0 },
        { 1 ,0 ,0 ,1 },
        { 1 ,0 ,1 ,1 },
    };
    cout << MaximumDecimalValue(mat, 4) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Maximum decimal value Path in
// Binary matrix
public class GFG {

    final static int N = 4;
// Returns maximum decimal value in binary matrix.
// Here p indicate power of 2

    static int MaximumDecimalValue(int mat[][], int n) {
        int dp[][] = new int[n][n];
        if (mat[0][0] == 1) {
            dp[0][0] = 1; // 1*(2^0)
        }
        // Compute binary stream of first row of matrix
        // and store result in dp[0][i]
        for (int i = 1; i < n; i++) {
            // indicate 1*(2^i) + result of previous
            if (mat[0][i] == 1) {
                dp[0][i] = (int) (dp[0][i - 1] + Math.pow(2, i));
            } // indicate 0*(2^i) + result of previous
            else {
                dp[0][i] = dp[0][i - 1];
            }
        }

        // Compute binary stream of first column of matrix
        // and store result in dp[i][0]
        for (int i = 1; i < n; i++) {
            // indicate 1*(2^i) + result of previous
            if (mat[i][0] == 1) {
                dp[i][0] = (int) (dp[i - 1][0] + Math.pow(2, i));
            } // indicate 0*(2^i) + result of previous
            else {
                dp[i][0] = dp[i - 1][0];
            }
        }

        // Traversal rest Binary matrix and Compute maximum
        // decimal value
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < n; j++) {
                // Here (i+j) indicate the current power of
                // 2 in path that is 2^(i+j)
                if (mat[i][j] == 1) {
                    dp[i][j] = (int) (Math.max(dp[i][j - 1], dp[i - 1][j])
                            + Math.pow(2, i + j));
                } else {
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }

        // Return maximum decimal value in binary matrix
        return dp[n - 1][n - 1];
    }

// Driver program
    public static void main(String[] args) {

        int mat[][] = {{1, 1, 0, 1},
        {0, 1, 1, 0},
        {1, 0, 0, 1},
        {1, 0, 1, 1},};
        System.out.println(MaximumDecimalValue(mat, 4));
    }
}
/*This code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python3 program to find Maximum decimal
# value Path in
# Binary matrix

N=4

# Returns maximum decimal value in binary matrix.
# Here p indicate power of 2
def MaximumDecimalValue(mat, n):
    dp=[[0 for i in range(n)] for i in range(n)]
    if (mat[0][0] == 1):
        dp[0][0] = 1     # 1*(2^0)

    # Compute binary stream of first row of matrix
    # and store result in dp[0][i]
    for i in range(1,n):

        # indicate 1*(2^i) + result of previous
        if (mat[0][i] == 1):
            dp[0][i] = dp[0][i-1] + 2**i

        # indicate 0*(2^i) + result of previous
        else:
            dp[0][i] = dp[0][i-1]

    # Compute binary stream of first column of matrix
    # and store result in dp[i][0]
    for i in range(1,n):

        # indicate 1*(2^i) + result of previous
        if (mat[i][0] == 1):
            dp[i][0] = dp[i-1][0] + 2**i

        # indicate 0*(2^i) + result of previous
    else:
        dp[i][0] = dp[i-1][0]

    # Traversal rest Binary matrix and Compute maximum
    # decimal value
    for i in range(1,n):
        for j in range(1,n):

            # Here (i+j) indicate the current power of
            # 2 in path that is 2^(i+j)
            if (mat[i][j] == 1):
                dp[i][j] = max(dp[i][j-1], dp[i-1][j])+(2**(i+j))
            else:
                dp[i][j] = max(dp[i][j-1], dp[i-1][j])

    # Return maximum decimal value in binary matrix
    return dp[n-1][n-1]

# Driver program
if __name__=='__main__':

    mat = [[ 1 ,1 ,0 ,1 ],
          [ 0 ,1 ,1 ,0 ],
          [ 1 ,0 ,0 ,1 ],
          [ 1 ,0 ,1 ,1 ]]

    print (MaximumDecimalValue(mat, 4))

#this code is contributed by sahilshelangia
```

## C#

```
// C# program to find Maximum decimal value Path in
// Binary matrix
using System;
public class GFG {

    readonly static int N = 4;
// Returns maximum decimal value in binary matrix.
// Here p indicate power of 2

    static int MaximumDecimalValue(int [,]mat, int n) {
        int [,]dp = new int[n,n];
        if (mat[0,0] == 1) {
            dp[0,0] = 1; // 1*(2^0)
        }
        // Compute binary stream of first row of matrix
        // and store result in dp[0,i]
        for (int i = 1; i < n; i++) {
            // indicate 1*(2^i) + result of previous
            if (mat[0,i] == 1) {
                dp[0,i] = (int) (dp[0,i - 1] + Math.Pow(2, i));
            } // indicate 0*(2^i) + result of previous
            else {
                dp[0,i] = dp[0,i - 1];
            }
        }

        // Compute binary stream of first column of matrix
        // and store result in dp[i,0]
        for (int i = 1; i < n; i++) {
            // indicate 1*(2^i) + result of previous
            if (mat[i,0] == 1) {
                dp[i,0] = (int) (dp[i - 1,0] + Math.Pow(2, i));
            } // indicate 0*(2^i) + result of previous
            else {
                dp[i,0] = dp[i - 1,0];
            }
        }

        // Traversal rest Binary matrix and Compute maximum
        // decimal value
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < n; j++) {
                // Here (i+j) indicate the current power of
                // 2 in path that is 2^(i+j)
                if (mat[i,j] == 1) {
                    dp[i,j] = (int) (Math.Max(dp[i,j - 1], dp[i - 1,j])
                            + Math.Pow(2, i + j));
                } else {
                    dp[i,j] = Math.Max(dp[i,j - 1], dp[i - 1,j]);
                }
            }
        }

        // Return maximum decimal value in binary matrix
        return dp[n - 1,n - 1];
    }

// Driver program
    public static void Main() {

        int [,]mat = {{1, 1, 0, 1},
        {0, 1, 1, 0},
        {1, 0, 0, 1},
        {1, 0, 1, 1},};
        Console.Write(MaximumDecimalValue(mat, 4));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find Maximum decimal value Path in
// Binary matrix

    let N = 4;
    // Returns maximum decimal value in binary matrix.
    // Here p indicate power of 2
    function MaximumDecimalValue(mat,n)
    {
        let dp=new Array(n);
        for(let i = 0; i < n; i++)
        {
            dp[i] = new Array(n);
            for(let j = 0; j < n; j++)
            {
                dp[i][j] = 0;
            }
        }

        if (mat[0][0] == 1) {
            dp[0][0] = 1; // 1*(2^0)
        }
        // Compute binary stream of first row of matrix
        // and store result in dp[0][i]
        for (let i = 1; i < n; i++)
        {

            // indicate 1*(2^i) + result of previous
            if (mat[0][i] == 1)
            {
                dp[0][i] = dp[0][i - 1] + Math.pow(2, i);
            }

            // indicate 0*(2^i) + result of previous
            else
            {
                dp[0][i] = dp[0][i - 1];
            }
        }

        // Compute binary stream of first column of matrix
        // and store result in dp[i][0]
        for (let i = 1; i < n; i++)
        {

            // indicate 1*(2^i) + result of previous
            if (mat[i][0] == 1)
            {
                dp[i][0] = Math.floor(dp[i - 1][0] + Math.pow(2, i));
            }

            // indicate 0*(2^i) + result of previous
            else
            {
                dp[i][0] = dp[i - 1][0];
            }
        }

        // Traversal rest Binary matrix and Compute maximum
        // decimal value
        for (let i = 1; i < n; i++)
        {
            for (let j = 1; j < n; j++)
            {

                // Here (i+j) indicate the current power of
                // 2 in path that is 2^(i+j)
                if (mat[i][j] == 1)
                {
                    dp[i][j] = Math.floor(Math.max(dp[i][j - 1], dp[i - 1][j])
                            + Math.pow(2, i + j));
                }
                else
                {
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }

        // Return maximum decimal value in binary matrix
        return dp[n - 1][n - 1];
    }

    // Driver program
    let mat = [[ 1 ,1 ,0 ,1 ],
          [ 0 ,1 ,1 ,0 ],
          [ 1 ,0 ,0 ,1 ],
          [ 1 ,0 ,1 ,1 ]];
    document.write(MaximumDecimalValue(mat, 4))

    // This code is contributed by rag2127.
</script>
```

**输出:**

```
111
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup>

本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。