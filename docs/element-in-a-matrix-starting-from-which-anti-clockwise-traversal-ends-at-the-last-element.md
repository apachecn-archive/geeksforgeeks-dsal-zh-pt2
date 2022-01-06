# 矩阵中的元素，从最后一个元素开始逆时针遍历

> 原文:[https://www . geesforgeks . org/矩阵中的元素-从哪个开始-逆时针-遍历-在最后一个元素结束/](https://www.geeksforgeeks.org/element-in-a-matrix-starting-from-which-anti-clockwise-traversal-ends-at-the-last-element/)

给定大小为 **n X n** 的 **mat[][]** ，任务是找到元素 **X** ，这样如果从 **X** 开始逆时针遍历，那么最终要打印的元素是**mat【n–1】【n–1】**。

> 矩阵的逆时针遍历，mat[][] =
> {{1，2，3}，
> {4，5，6}，
> {7，8，9}}
> 从元素 5 开始将是 5，6，3，2，1，4，7，8，9。

**例:**

> **输入:** mat[][] = {{1，2}，{3，4}}
> **输出:** 2
> 如果我们从 mat[0][1]即 2 开始遍历，那么
> 我们将以 mat[1][1]处的元素结束，即 4。
> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}}
> **输出:** 5

**方法:**从**mat【n–1】【n–1】**处的元素开始，以相反的顺序(即顺时针)遍历矩阵。当遍历矩阵的所有元素时，最后访问的元素将是结果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to print last element
// Of given matrix
int printLastElement(int mat[][2], int n)
{

    // Starting row index
    int si = 0;

    // Starting column index
    int sj = 0;

    // Ending row index
    int ei = n - 1;

    // Ending column index
    int ej = n - 1;

    // Track the move
    int direction = 0;

    // While starting index is less than ending
    // row index or starting column index
    // is less the ending column index
    while (si < ei || sj < ej) {

        // Switch cases for all direction
        // Move under all cases for all
        // directions
        switch (direction % 4) {
        case 0:
            sj++;
            break;
        case 1:
            ei--;
            break;
        case 2:
            ej--;
            break;
        case 3:
            si++;
            break;
        }

        // Increment direction by one
        // for each case
        direction++;
    }

    // Finally return the last element
    // If not found return 0
    return mat[si][sj];

    return 0;
}

// Driver code
int main()
{
    int n = 2;
    int mat[][2] = { { 1, 2 }, { 3, 4 } };
    cout << printLastElement(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to print last element
// Of given matrix
static int printLastElement(int mat[][], int n)
{

    // Starting row index
    int si = 0;

    // Starting column index
    int sj = 0;

    // Ending row index
    int ei = n - 1;

    // Ending column index
    int ej = n - 1;

    // Track the move
    int direction = 0;

    // While starting index is less than ending
    // row index or starting column index
    // is less the ending column index
    while (si < ei || sj < ej)
    {

        // Switch cases for all direction
        // Move under all cases for all
        // directions
        switch (direction % 4)
        {
        case 0:
            sj++;
            break;
        case 1:
            ei--;
            break;
        case 2:
            ej--;
            break;
        case 3:
            si++;
            break;
        }

        // Increment direction by one
        // for each case
        direction++;
    }

    // Finally return the last element
    // If not found return 0
    return mat[si][sj];

}

// Driver code
public static void main(String[] args)
{
    int n = 2;
    int mat[][] = new int[][]{{ 1, 2 }, { 3, 4 }};
    System.out.println(printLastElement(mat, n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print last element
# Of given matrix
def printLastElement(mat, n):

    # Starting row index
    si = 0

    # Starting column index
    sj = 0

    # Ending row index
    ei = n - 1

    # Ending column index
    ej = n - 1

    # Track the move
    direction = 0

    # While starting index is less than ending
    # row index or starting column index
    # is less the ending column index
    while (si < ei or sj < ej):

        # Switch cases for all direction
        # Move under all cases for all
        # directions
        if (direction % 4 == 0):
            sj += 1
        if (direction % 4 == 1):
            ei -= 1
        if (direction % 4 == 2):
            ej -= 1
        if (direction % 4 == 3):
            si += 1

        # Increment direction by one
        # for each case
        direction += 1

    # Finally return the last element
    # If not found return 0
    return mat[si][sj]

    return 0

# Driver code
if __name__ == '__main__':
    n = 2
    mat = [[1, 2], [3, 4 ]]
    print(printLastElement(mat, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to print last element
// Of given matrix
static int printLastElement(int [,]mat, int n)
{

    // Starting row index
    int si = 0;

    // Starting column index
    int sj = 0;

    // Ending row index
    int ei = n - 1;

    // Ending column index
    int ej = n - 1;

    // Track the move
    int direction = 0;

    // While starting index is less than ending
    // row index or starting column index
    // is less the ending column index
    while (si < ei || sj < ej)
    {

        // Switch cases for all direction
        // Move under all cases for all
        // directions
        switch (direction % 4)
        {
            case 0:
                sj++;
                break;
            case 1:
                ei--;
                break;
            case 2:
                ej--;
                break;
            case 3:
                si++;
                break;
        }

        // Increment direction by one
        // for each case
        direction++;
    }

    // Finally return the last element
    // If not found return 0
    return mat[si, sj];

}

// Driver code
public static void Main()
{
    int n = 2;
    int [,]mat = {{ 1, 2 }, { 3, 4 }};

    Console.WriteLine(printLastElement(mat, n));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print last element
// Of given matrix
function printLastElement($mat, $n)
{

    // Starting row index
    $si = 0;

    // Starting column index
    $sj = 0;

    // Ending row index
    $ei = $n - 1;

    // Ending column index
    $ej = $n - 1;

    // Track the move
    $direction = 0;

    // While starting index is less than ending
    // row index or starting column index
    // is less the ending column index
    while ($si < $ei || $sj < $ej)
    {

        // Switch cases for all direction
        // Move under all cases for all
        // directions
        switch ($direction % 4)
        {
            case 0:
                $sj++;
                break;
            case 1:
                $ei--;
                break;
            case 2:
                $ej--;
                break;
            case 3:
                $si++;
                break;
        }

        // Increment direction by one
        // for each case
        $direction++;
    }

    // Finally return the last element
    // If not found return 0
    return $mat[$si][$sj];

    return 0;
}

// Driver code
$n = 2;
$mat = array(array(1, 2),
             array(3, 4));
echo printLastElement($mat, $n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to print last element
    // Of given matrix
    function printLastElement(mat , n) {

        // Starting row index
        var si = 0;

        // Starting column index
        var sj = 0;

        // Ending row index
        var ei = n - 1;

        // Ending column index
        var ej = n - 1;

        // Track the move
        var direction = 0;

        // While starting index is less than ending
        // row index or starting column index
        // is less the ending column index
        while (si < ei || sj < ej) {

            // Switch cases for all direction
            // Move under all cases for all
            // directions
            switch (direction % 4) {
            case 0:
                sj++;
                break;
            case 1:
                ei--;
                break;
            case 2:
                ej--;
                break;
            case 3:
                si++;
                break;
            }

            // Increment direction by one
            // for each case
            direction++;
        }

        // Finally return the last element
        // If not found return 0
        return mat[si][sj];

    }

    // Driver code

        var n = 2;
        var mat = [[ 1, 2 ], [ 3, 4 ] ];
        document.write(printLastElement(mat, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(1)