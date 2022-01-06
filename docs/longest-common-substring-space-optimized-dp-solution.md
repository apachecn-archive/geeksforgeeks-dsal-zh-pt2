# 最长公共子串(空间优化 DP 解)

> 原文:[https://www . geesforgeks . org/最长-公共-子串-空间-优化-dp-solution/](https://www.geeksforgeeks.org/longest-common-substring-space-optimized-dp-solution/)

给定两个字符串“X”和“Y”，求最长公共子串的长度。预期的空间复杂度是线性的。
**例:**

```
Input : X = "GeeksforGeeks", Y = "GeeksQuiz"
Output : 5
The longest common substring is "Geeks" and is of
length 5.

Input : X = "abcdxyz", Y = "xyzabcd"
Output : 4
The longest common substring is "abcd" and is of
length 4.
```

![longest-common-substring](img/169220314b5aaea46b3b35ffd3e6a654.png)

我们已经讨论了最长公共子串的基于动态规划的解决方案。解所用的辅助空间是 O(m*n)，其中 m 和 n 是字符串 X 和 y 的长度，解所用的空间可以简化为 O(2*n)。
假设我们在 mat[i][j]位置。现在如果 X[i-1] == Y[j-1]，那么我们把 mat[i-1][j-1]的值加到我们的结果上。也就是说，我们将前一行的值相加，并且前一行下面的所有其他行的值都不会被使用。所以，我们每次只使用两个连续的行。这种观察可以用来减少寻找最长公共子串长度所需的空间。
我们不是创建 m*n 大小的矩阵，而是创建 2*n 大小的矩阵，用一个变量 currRow 来表示这个矩阵的第 0 行或者第 1 行当前都是用来求长度的。最初，当字符串 X 的长度为零时，第 0 行用作当前行。每次迭代结束时，当前行成为前一行，前一行成为新的当前行。

## C++

```
// Space optimized CPP implementation of longest
// common substring.
#include <bits/stdc++.h>
using namespace std;

// Function to find longest common substring.
int LCSubStr(string X, string Y)
{
    // Find length of both the strings.
    int m = X.length();
    int n = Y.length();

    // Variable to store length of longest
    // common substring.
    int result = 0;

    // Matrix to store result of two
    // consecutive rows at a time.
    int len[2][n];

    // Variable to represent which row of
    // matrix is current row.
    int currRow = 0;

    // For a particular value of i and j,
    // len[currRow][j] stores length of longest
    // common substring in string X[0..i] and Y[0..j].
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0) {
                len[currRow][j] = 0;
            }
            else if (X[i - 1] == Y[j - 1]) {
                len[currRow][j] = len[1 - currRow][j - 1] + 1;
                result = max(result, len[currRow][j]);
            }
            else {
                len[currRow][j] = 0;
            }
        }

        // Make current row as previous row and previous
        // row as new current row.
        currRow = 1 - currRow;
    }

    return result;
}

int main()
{
    string X = "GeeksforGeeks";
    string Y = "GeeksQuiz";

    cout << LCSubStr(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Space optimized CPP implementation of
// longest common substring.
import java.io.*;
import java.util.*;

public class GFG {

    // Function to find longest
    // common substring.
    static int LCSubStr(String X, String Y)
    {

        // Find length of both the strings.
        int m = X.length();
        int n = Y.length();

        // Variable to store length of longest
        // common substring.
        int result = 0;

        // Matrix to store result of two
        // consecutive rows at a time.
        int [][]len = new int[2][n];

        // Variable to represent which row of
        // matrix is current row.
        int currRow = 0;

        // For a particular value of
        // i and j, len[currRow][j]
        // stores length of longest
        // common substring in string
        // X[0..i] and Y[0..j].
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 || j == 0) {
                    len[currRow][j] = 0;
                }
                else if (X.charAt(i - 1) ==
                              Y.charAt(j - 1))
                {
                    len[currRow][j] =
                      len[(1 - currRow)][(j - 1)]
                                             + 1;
                    result = Math.max(result,
                                len[currRow][j]);
                }
                else
                {
                    len[currRow][j] = 0;
                }
            }

            // Make current row as previous
            // row and previous row as
            // new current row.
            currRow = 1 - currRow;
        }

        return result;
    }

    // Driver Code
    public static void main(String args[])
    {
        String X = "GeeksforGeeks";
        String Y = "GeeksQuiz";

        System.out.print(LCSubStr(X, Y));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Space optimized Python3 implementation 
# of longest common substring.
import numpy as np

# Function to find longest common substring.
def LCSubStr(X, Y) :

    # Find length of both the strings.
    m = len(X)
    n = len(Y)

    # Variable to store length of
    # longest common substring.
    result = 0

    # Matrix to store result of two
    # consecutive rows at a time.
    len_mat = np.zeros((2, n))

    # Variable to represent which row 
    # of matrix is current row.
    currRow = 0

    # For a particular value of i and j,
    # len_mat[currRow][j] stores length of
    # longest common substring in string
    # X[0..i] and Y[0..j].
    for i in range(m) :
        for j in range(n) :

            if (i == 0 | j == 0) :
                len_mat[currRow][j] = 0

            elif (X[i - 1] == Y[j - 1]) :

                len_mat[currRow][j] = len_mat[1 - currRow][j - 1] + 1
                result = max(result, len_mat[currRow][j])

            else :
                len_mat[currRow][j] = 0

        # Make current row as previous row and
        # previous row as new current row.
        currRow = 1 - currRow

    return result

# Driver Code
if __name__ == "__main__" :

    X = "GeeksforGeeks"
    Y = "GeeksQuiz"

    print(LCSubStr(X, Y))

# This code is contributed by Ryuga
```

## C#

```
// Space optimized C# implementation
// of longest common substring.
using System;
using System.Collections.Generic;
class GFG {

    // Function to find longest
    // common substring.
    static int LCSubStr(string X, string Y)
    {

        // Find length of both the strings.
        int m = X.Length;
        int n = Y.Length;

        // Variable to store length of longest
        // common substring.
        int result = 0;

        // Matrix to store result of two
        // consecutive rows at a time.
        int [,]len = new int[2,n];

        // Variable to represent which row of
        // matrix is current row.
        int currRow = 0;

        // For a particular value of
        // i and j, len[currRow][j]
        // stores length of longest
        // common substring in string
        // X[0..i] and Y[0..j].
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 || j == 0) {
                    len[currRow,j] = 0;
                }
                else if (X[i - 1] == Y[j - 1]) {
                    len[currRow,j] = len[(1 - currRow),
                                          (j - 1)] + 1;
                    result = Math.Max(result, len[currRow, j]);
                }
                else
                {
                    len[currRow,j] = 0;
                }
            }

            // Make current row as previous
            // row and previous row as
            // new current row.
            currRow = 1 - currRow;
        }

        return result;
    }

    // Driver Code
    public static void Main()
    {
        string X = "GeeksforGeeks";
        string Y = "GeeksQuiz";

        Console.Write(LCSubStr(X, Y));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Space optimized PHP implementation
// of longest common substring.

// Function to find
// longest common substring.
function LCSubStr($X, $Y)
{
    // Find length of
    // both the strings.
    $m = strlen($X);
    $n = strlen($Y);

    // Variable to store length
    // of longest common substring.
    $result = 0;

    // Matrix to store result of two
    // consecutive rows at a time.
    $len = array(array(), array(), );

    // Variable to represent which
    // row of matrix is current row.
    $currRow = 0;

    // For a particular value of
    // i and j, len[currRow][j]
    // stores length of longest
    // common substring in string
    // X[0..i] and Y[0..j].
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {
            if ($i == 0 || $j == 0)
            {
                $len[$currRow][$j] = 0;
            }
            else if ($X[$i - 1] == $Y[$j - 1])
            {
                $len[$currRow][$j] =
                        $len[1 - $currRow][$j - 1] + 1;

                $result = max($result,
                              $len[$currRow][$j]);
            }
            else
            {
                $len[$currRow][$j] = 0;
            }
        }

        // Make current row as
        // previous row and previous
        // row as new current row.
        $currRow = 1 - $currRow;
    }

    return $result;
}

// Driver Code
$X = "GeeksforGeeks";
$Y = "GeeksQuiz";

print (LCSubStr($X, $Y));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Space optimized CPP implementation of longest
// common substring.

// Function to find longest common substring.
function LCSubStr(X, Y)
{
    // Find length of both the strings.
    var m = X.length;
    var n = Y.length;

    // Variable to store length of longest
    // common substring.
    var result = 0;

    // Matrix to store result of two
    // consecutive rows at a time.
    var len = Array.from(Array(2), ()=> Array(n));

    // Variable to represent which row of
    // matrix is current row.
    var currRow = 0;

    // For a particular value of i and j,
    // len[currRow][j] stores length of longest
    // common substring in string X[0..i] and Y[0..j].
    for (var i = 0; i <= m; i++) {
        for (var j = 0; j <= n; j++) {
            if (i == 0 || j == 0) {
                len[currRow][j] = 0;
            }
            else if (X[i - 1] == Y[j - 1]) {
                len[currRow][j] = len[1 - currRow][j - 1] + 1;
                result = Math.max(result, len[currRow][j]);
            }
            else {
                len[currRow][j] = 0;
            }
        }

        // Make current row as previous row and previous
        // row as new current row.
        currRow = 1 - currRow;
    }

    return result;
}

// Driver code
var X = "GeeksforGeeks";
var Y = "GeeksQuiz";
document.write( LCSubStr(X, Y));

// This code is contributed by itsok.
</script>
```

**Output :** 

```
5
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(n)