# 求矩阵中正方形的最大边长

> 原文:[https://www . geesforgeks . org/find-矩阵中正方形的最大边长/](https://www.geeksforgeeks.org/find-maximum-side-length-of-square-in-a-matrix/)

给定一个奇数阶的正方形矩阵，任务是找出矩阵中形成的最大正方形的边长。矩阵中的正方形，如果其周长上的所有元素都相同，并且其中心是矩阵的中心，则称之为正方形。矩阵的中心也是边长为 1 的正方形。
**例** :

```
Input : matrix[][] = {2, 3, 0,
                      0, 2, 0,
                      0, 1, 1}
Output : 1

Input : matrix[][] = {2, 2, 2,
                      2, 1, 2,
                      2, 2, 2}
Output : 3
```

任何奇数阶矩阵的中心都是索引为 **i = j = n/2** 的元素。现在，为了找到矩阵中最大的正方形，检查所有距离中心相同的环绕元素。对于偏离中心 I 单位的正方形，检查所有位于 **n/2-i** 和 **n/2+i** 行和列中的元素，以及 **n/2** 和元素索引中的任何一个的差异不超过 I。请在下面的示例中找到具有不同可能边长的正方形的格式。

```
x x x x x
x y y y x
x y c y x
x y y y x
x x x x x
```

需要关注的点:

*   由于中心元素也是正方形的一种形式，最小可能边长是 1。
*   最长的正方形可以是第一行和第一列的所有元素，因此最大可能边长为![n ](img/872c13b29b9001d12460c34eb30ae8d0.png "Rendered by QuickLaTeX.com")

**算法:**

*   迭代 i=0 到 n/2
    *   对于第 I 行和第 n-i-1 行，迭代第 I 列到第 n-i-1 行
        ，反之亦然，检查所有元素是否相同。
    *   如果是，那么正方形的长度是 n-2*i。
    *   否则进行下一次迭代

以下是上述方法的实现:

## C++

```
// C++ program to find max possible side-length
// of a square in a given matrix

#include <bits/stdc++.h>
#define n 5
using namespace std;

// Function to return side-length of square
int largestSideLen(int matrix[][n])
{
    int result = 1;

    // Traverse the matrix
    for (int i = 0; i < n / 2; i++) {

        int element = matrix[i][i];
        int isSquare = 1;

        for (int j = i; j < n - i; j++) {
            // for row i
            if (matrix[i][j] != element)
                isSquare = 0;
            // for row n-i-1
            if (matrix[n - i - 1][j] != element)
                isSquare = 0;
            // for column i
            if (matrix[j][i] != element)
                isSquare = 0;
            // for column n-i-1
            if (matrix[j][n - i - 1] != element)
                isSquare = 0;
        }

        if (isSquare)
            return n - 2 * i;
    }

    // Return result
    return result;
}

// Driver program
int main()
{
    int matrix[n][n] = { 1, 1, 1, 1, 1,
                         1, 2, 2, 2, 1,
                         1, 2, 1, 2, 1,
                         1, 2, 2, 2, 1,
                         1, 1, 1, 1, 1 };

    cout << largestSideLen(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find max possible side-length
// of a square in a given matrix

import java.io.*;

class GFG {
static int n = 5;
    // Function to return side-length of square
static int largestSideLen(int matrix[][])
{
    int result = 1;

    // Traverse the matrix
    for (int i = 0; i < (n / 2); i++) {

        int element = matrix[i][i];
        int isSquare = 1;

        for (int j = i; j < n - i; j++) {
            // for row i
            if (matrix[i][j] != element)
                isSquare = 0;
            // for row n-i-1
            if (matrix[n - i - 1][j] != element)
                isSquare = 0;
            // for column i
            if (matrix[j][i] != element)
                isSquare = 0;
            // for column n-i-1
            if (matrix[j][n - i - 1] != element)
                isSquare = 0;
        }

        if (isSquare > 0)
            return n - (2 * i);
    }

    // Return result
    return result;
}

// Driver program

    public static void main (String[] args) {
        int matrix[][] = {{ 1, 1, 1, 1, 1},
                        {1, 2, 2, 2, 1},
                        {1, 2, 1, 2, 1},
                        {1, 2, 2, 2, 1},
                        {1, 1, 1, 1, 1 }};

    System.out.println (largestSideLen(matrix));

    }
}
```

## 蟒蛇 3

```
# Python 3 program to find max possible
# side-length of a square in a given matrix

n = 5

# Function to return side-length of square
def largestSideLen(matrix):
    result = 1

    # Traverse the matrix
    for i in range(int(n / 2)):
        element = matrix[i][i]
        isSquare = 1

        for j in range(i, n - i):

            # for row i
            if (matrix[i][j] != element):
                isSquare = 0

            # for row n-i-1
            if (matrix[n - i - 1][j] != element):
                isSquare = 0

            # for column i
            if (matrix[j][i] != element):
                isSquare = 0

            # for column n-i-1
            if (matrix[j][n - i - 1] != element):
                isSquare = 0

        if (isSquare):
            return n - 2 * i

    # Return result
    return result

# Driver Code
if __name__ == '__main__':
    matrix = [[1, 1, 1, 1, 1],
              [1, 2, 2, 2, 1],
              [1, 2, 1, 2, 1],
              [1, 2, 2, 2, 1],
              [1, 1, 1, 1, 1]]

    print(largestSideLen(matrix))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C#  program to find max possible side-length
// of a square in a given matrix
using System;

public class GFG{
    static int n = 5;
    // Function to return side-length of square
static int largestSideLen(int [,]matrix)
{
    int result = 1;

    // Traverse the matrix
    for (int i = 0; i < (n / 2); i++) {

        int element = matrix[i,i];
        int isSquare = 1;

        for (int j = i; j < n - i; j++) {
            // for row i
            if (matrix[i,j] != element)
                isSquare = 0;
            // for row n-i-1
            if (matrix[n - i - 1,j] != element)
                isSquare = 0;
            // for column i
            if (matrix[j,i] != element)
                isSquare = 0;
            // for column n-i-1
            if (matrix[j,n - i - 1] != element)
                isSquare = 0;
        }

        if (isSquare > 0)
            return n - (2 * i);
    }

    // Return result
    return result;
}

// Driver program

    static public void Main (){
        int [,]matrix = {{ 1, 1, 1, 1, 1},
                        {1, 2, 2, 2, 1},
                        {1, 2, 1, 2, 1},
                        {1, 2, 2, 2, 1},
                        {1, 1, 1, 1, 1 }};

           Console.WriteLine(largestSideLen(matrix));

    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find max possible
// side-length of a square in a given matrix

// Function to return side-length of square
function largestSideLen($matrix)
{
    $n = 5;
    $result = 1;

    // Traverse the matrix
    for ($i = 0; $i < ($n / 2); $i++)
    {

        $element = $matrix[$i][$i];
        $isSquare = 1;

        for ($j = $i; $j < ($n - $i); $j++)
        {
            // for row i
            if ($matrix[$i][$j] != $element)
                $isSquare = 0;

            // for row n-i-1
            if ($matrix[$n - $i - 1][$j] != $element)
                $isSquare = 0;

            // for column i
            if ($matrix[$j][$i] != $element)
                $isSquare = 0;

            // for column n-i-1
            if ($matrix[$j][$n - $i - 1] != $element)
                $isSquare = 0;
        }

        if ($isSquare)
            return ($n - 2 * $i);
    }

    // Return result
    return $result;
}

// Driver Code
$matrix = array( 1, 1, 1, 1, 1,
                 1, 2, 2, 2, 1,
                 1, 2, 1, 2, 1,
                 1, 2, 2, 2, 1,
                 1, 1, 1, 1, 1 );

echo largestSideLen($matrix);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript program to find max
// possible side-length
// of a square in a given matrix

const n = 5;

// Function to return
// side-length of square
function largestSideLen(matrix)
{
    let result = 1;

    // Traverse the matrix
    for (let i = 0; i < parseInt(n / 2); i++)
    {

        let element = matrix[i][i];
        let isSquare = 1;

        for (let j = i; j < n - i; j++) {
            // for row i
            if (matrix[i][j] != element)
                isSquare = 0;
            // for row n-i-1
            if (matrix[n - i - 1][j] != element)
                isSquare = 0;
            // for column i
            if (matrix[j][i] != element)
                isSquare = 0;
            // for column n-i-1
            if (matrix[j][n - i - 1] != element)
                isSquare = 0;
        }

        if (isSquare)
            return n - 2 * i;
    }

    // Return result
    return result;
}

// Driver program
    let matrix = [ [1, 1, 1, 1, 1],
                   [1, 2, 2, 2, 1],
                   [1, 2, 1, 2, 1],
                   [1, 2, 2, 2, 1],
                   [1, 1, 1, 1, 1 ]];

    document.write(largestSideLen(matrix));

</script>
```

**Output:** 

```
5
```