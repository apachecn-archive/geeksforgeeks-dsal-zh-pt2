# 通过过滤一次子矩阵来最大化二元矩阵

> 原文:[https://www . geesforgeks . org/maximum-binary-matrix-filp ping-submatrix/](https://www.geeksforgeeks.org/maximize-binary-matrix-filpping-submatrix/)

给定一个由 **R** 行和 **C** 列组成的二元矩阵。我们可以翻转到任何大小的子矩阵。翻转意味着将 1 改为 0，将 0 改为 1。任务是最大化矩阵中 1 的数量。输出最大数量的 1。

**示例:**

```
Input : R = 3, C =3
mat[][] = { 0, 0, 1,
            0, 0, 1,
            1, 0, 1 }

Output : 8
Flip
0 0 1
0 0 1
1 0 1

to get

1 1 1
1 1 1
0 1 1

Input : R = 2, C = 3
mat[][] = { 0, 0, 0,
            0, 0, 0 }
Output : 6
```

创建一个由 R 行和 C 列组成的矩阵 one[][]，它通过以下方式预先计算子矩阵中从(0，0)到(I，j)的 one 的数量

```
// Common elements in ones[i-1][j] and 
// ones[i][j-1] are ones[i-1][j-1]
ones[i][j] = ones[i-1][j] + ones[i][j-1] - 
             ones[i-1][j-1] + (mat[i][j] == 1)
```

因为，我们只能翻转一次子矩阵。我们迭代每个单元(I，j)到(I+k–1，I+k–1)的所有可能大小的所有可能子矩阵。在选定的子矩阵中填入数字后，我们计算 1 的总数。
将子矩阵(I，j)翻转为(I+k–1)后，最终矩阵中的 1 总数将是整个矩阵中的 1–所选子矩阵中的 1+所选子矩阵中的 0。结果是:-
1[R][C]–cal(I，j，i + k，j+k–1)+k * k–cal(I，j，I+k–1，j+k–1)
其中 cal(a，b，C，d)表示长度为 C–a 的正方形子矩阵中的 1 的数目。
现在 cal(x1，y1，x2，y2)可以定义为:
1[x2][y2]–1[x2][y1–1]–1[x1–2]

下面是该方法的实现:

## C++

```
// C++ program to find maximum number of ones after
// one flipping in Binary Matrix
#include <bits/stdc++.h>
#define R 3
#define C 3
using namespace std;

// Return number of ones in square submatrix of size
// k x k starting from (x, y)
int cal(int ones[R + 1][C + 1], int x, int y, int k)
{
    return ones[x + k - 1][y + k - 1] - ones[x - 1][y + k - 1]
           - ones[x + k - 1][y - 1] + ones[x - 1][y - 1];
}

// Return maximum number of 1s after flipping a submatrix
int sol(int mat[R][C])
{
    int ans = 0;

    // Precomputing the number of 1s
    int ones[R + 1][C + 1] = {0};
    for (int i = 1; i <= R; i++)
        for (int j = 1; j <= C; j++)
            ones[i][j] = ones[i - 1][j] + ones[i][j - 1] -
                         ones[i - 1][j - 1] +
                         (mat[i - 1][j - 1] == 1);

    // Finding the maximum number of 1s after flipping
    for (int k = 1; k <= min(R, C); k++)
        for (int i = 1; i + k - 1 <= R; i++)
            for (int j = 1; j + k - 1 <= C; j++)
                ans = max(ans, (ones[R][C] + k * k -
                                2 * cal(ones, i, j, k)));
    return ans;
}

// Driver code
int main()
{
    int mat[R][C] = {{0, 0, 1},
        { 0, 0, 1},
        { 1, 0, 1 }
    };

    cout << sol(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of ones after
// one flipping in Binary Matrix
class GFG {

static final int R = 3;
static final int C = 3 ;

// Return number of ones in square submatrix of size
// k x k starting from (x, y)
static int cal(int ones[][], int x, int y, int k)
{
    return ones[x + k - 1][y + k - 1] - ones[x - 1][y + k - 1]
        - ones[x + k - 1][y - 1] + ones[x - 1][y - 1];
}

// Return maximum number of 1s after flipping a submatrix
static int sol(int mat[][])
{
    int ans = 0;
        int val =0;
    // Precomputing the number of 1s
    int ones[][] = new int[R + 1][C + 1];
    for (int i = 1; i <= R; i++)
        for (int j = 1; j <= C; j++) {
                    if(mat[i - 1][j - 1] == 1)
                        val=1;
        ones[i][j] = ones[i - 1][j] + ones[i][j - 1] -
                        ones[i - 1][j - 1] +
                        (val);
                }
    // Finding the maximum number of 1s after flipping
    for (int k = 1; k <= Math.min(R, C); k++)
        for (int i = 1; i + k - 1 <= R; i++)
            for (int j = 1; j + k - 1 <= C; j++)
                ans = Math.max(ans, (ones[R][C] + k * k -
                                2 * cal(ones, i, j, k)));
    return ans;
}

// Driver code
    static public void main(String[] args) {
        int mat[][] = {{0, 0, 1},
        { 0, 0, 1},
        { 1, 0, 1 }
    };

       System.out.println(sol(mat));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find maximum number of
# ones after one flipping in Binary Matrix
R = 3
C = 3

# Return number of ones in square submatrix
# of size k x k starting from (x, y)
def cal(ones, x, y, k):
    return (ones[x + k - 1][y + k - 1] -
            ones[x - 1][y + k - 1] -
            ones[x + k - 1][y - 1] +
            ones[x - 1][y - 1])

# Return maximum number of 1s after
# flipping a submatrix
def sol(mat):
    ans = 0

    # Precomputing the number of 1s
    ones = [[0 for i in range(C + 1)]
               for i in range(R + 1)]
    for i in range(1, R + 1, 1):
        for j in range(1, C + 1, 1):
            ones[i][j] = (ones[i - 1][j] + ones[i][j - 1] -
                          ones[i - 1][j - 1] +
                         (mat[i - 1][j - 1] == 1))

    # Finding the maximum number of 1s
    # after flipping
    for k in range(1, min(R, C) + 1, 1):
        for i in range(1, R - k + 2, 1):
            for j in range(1, C - k + 2, 1):
                ans = max(ans, (ones[R][C] + k * k - 2 *
                            cal(ones, i, j, k)))
    return ans

# Driver code
if __name__ == '__main__':
    mat = [[0, 0, 1],
           [0, 0, 1],
           [1, 0, 1]]

    print(sol(mat))

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to find maximum number of ones after
// one flipping in Binary Matrix
using System;   

public class GFG {

    static readonly int R = 3;
    static readonly int C = 3 ;

    // Return number of ones in square submatrix of size
    // k x k starting from (x, y)
    static int cal(int [,]ones, int x, int y, int k)
    {
        return ones[x + k - 1,y + k - 1] - ones[x - 1,y + k - 1]
            - ones[x + k - 1,y - 1] + ones[x - 1,y - 1];
    }

    // Return maximum number of 1s after flipping a submatrix
    static int sol(int [,]mat)
    {
        int ans = 0;
            int val =0;
        // Precomputing the number of 1s
        int [,]ones = new int[R + 1,C + 1];
        for (int i = 1; i <= R; i++)
            for (int j = 1; j <= C; j++) {
                        if(mat[i - 1,j - 1] == 1)
                            val=1;
            ones[i,j] = ones[i - 1,j] + ones[i,j - 1] -
                            ones[i - 1,j - 1] +
                            (val);
                    }
        // Finding the maximum number of 1s after flipping
        for (int k = 1; k <= Math.Min(R, C); k++)
            for (int i = 1; i + k - 1 <= R; i++)
                for (int j = 1; j + k - 1 <= C; j++)
                    ans = Math.Max(ans, (ones[R,C] + k * k -
                                    2 * cal(ones, i, j, k)));
        return ans;
    }

    // Driver code
    static public void Main() {
        int [,]mat = {{0, 0, 1},
        { 0, 0, 1},
        { 1, 0, 1 }
    };

    Console.WriteLine(sol(mat));
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum number of ones after
// one flipping in Binary Matrix

$R = 3;
$C = 3;

// Return number of ones in square submatrix of size
// k x k starting from (x, y)
function cal($ones, $x, $y, $k)
{
    return $ones[$x + $k - 1][$y + $k - 1] -
            $ones[$x - 1][$y + $k - 1] -
            $ones[$x + $k - 1][$y - 1] +
            $ones[$x - 1][$y - 1];
}

// Return maximum number of 1s after flipping a submatrix
function sol($mat)
{
    global $C,$R;
    $ans = 0;

    // Precomputing the number of 1s
    $ones=array_fill(0,$R + 1,array_fill(0,$C + 1,0));
    for ($i = 1; $i <= $R; $i++)
        for ($j = 1; $j <= $C; $j++)
            $ones[$i][$j] = $ones[$i - 1][$j] + $ones[$i][$j - 1] -
                        $ones[$i - 1][$j - 1] +
                        (int)($mat[$i - 1][$j - 1] == 1);

    // Finding the maximum number of 1s after flipping
    for ($k = 1; $k <= min($R, $C); $k++)
        for ($i = 1; $i + $k - 1 <= $R; $i++)
            for ($j = 1; $j + $k - 1 <= $C; $j++)
                $ans = max($ans, ($ones[$R][$C] + $k * $k -
                                2 * cal($ones, $i, $j, $k)));
    return $ans;
}

    // Driver code
    $mat = array(array(0, 0, 1),
        array( 0, 0, 1),
        array( 1, 0, 1 ));

    echo sol($mat);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find maximum number of ones after
// one flipping in Binary Matrix

let R = 3;
let C = 3 ;

// Return number of ones in square submatrix of size
// k x k starting from (x, y)
function cal(ones, x, y, k)
{
    return ones[x + k - 1][y + k - 1] - ones[x - 1][y + k - 1]
        - ones[x + k - 1][y - 1] + ones[x - 1][y - 1];
}

// Return maximum number of 1s after flipping a submatrix
function sol(mat)
{
    let ans = 0;
        let val =0;
    // Precomputing the number of 1s
    let ones = new Array(R + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < ones.length; i++) {
        ones[i] = new Array(2);
    }

    for (var i = 0; i < ones.length; i++) {
        for (var j = 0; j < ones.length; j++) {
        ones[i][j] = 0;
    }
    }

    for (let i = 1; i <= R; i++)
        for (let j = 1; j <= C; j++) {
                    if(mat[i - 1][j - 1] == 1)
                        val=1;
        ones[i][j] = ones[i - 1][j] + ones[i][j - 1] -
                        ones[i - 1][j - 1] +
                        (val);
                }
    // Finding the maximum number of 1s after flipping
    for (let k = 1; k <= Math.min(R, C); k++)
        for (let i = 1; i + k - 1 <= R; i++)
            for (let j = 1; j + k - 1 <= C; j++)
                ans = Math.max(ans, (ones[R][C] + k * k -
                                2 * cal(ones, i, j, k)));
    return ans;
}

// driver function

        let mat = [[0, 0, 1],
        [ 0, 0, 1],
        [ 1, 0, 1 ]
    ];

       document.write(sol(mat));

// This code is contributed by susmitakundugoaldanga.
</script>   
```

**输出:**

```
8
```

**时间复杂度:** O(R*C*min(R，C))

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。