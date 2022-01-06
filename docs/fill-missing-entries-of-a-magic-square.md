# 填充幻方的缺失条目

> 原文:[https://www . geesforgeks . org/fill-missing-entries-of-a-magic-square/](https://www.geeksforgeeks.org/fill-missing-entries-of-a-magic-square/)

给定一个左对角线元素缺失的 3X3 矩阵 **mat** (设置为 **0** ，考虑到原始矩阵的每一行、每一列和对角线的总和相等，任务是找到缺失的对角线元素并打印原始矩阵。
**例:**

> **输入:** mat[][] = {{0，7，6}，{9，0，1}，{4，3，0 } }
> T3】输出:T5】2 7 6
> 9 5 1
> 4 3 8
> 行和=列和=对角线和= 15
> **输入:** mat[][] = {{0，1，1}，{1，0，1}，{1，1，0}}

**方法:**让**和**表示除对角线元素外的总和，

> 总和=给定矩阵的总和–对角线总和
> 总和= (3 *行总和)–对角线总和
> 总和= (2 *行总和)【自，列总和=行总和=对角线总和】
> 行总和=总和/ 2

因此，我们可以在每一行中插入一个元素，这样该行的总和就是**行总和**
下面是上述方法的实现:

## C++

```
// C++ program to fill blanks with numbers
#include <bits/stdc++.h>
using namespace std;

// Function to print the original matrix
int printFilledDiagonal(int sq[][3])
{
    // Calculate the sum of all the elements
    // of the matrix
    int sum = 0;
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            sum += sq[i][j];

    // Required sum of each row (from the approach)
    sum /= 2;

    for (int i = 0; i < 3; i++) {

        // Row sum excluding the diagonal element
        int rowSum = 0;
        for (int j = 0; j < 3; j++)
            rowSum += sq[i][j];

        // Element that must be inserted at
        // diagonal element of the current row
        sq[i][i] = sum - rowSum;
    }

    // Print the updated matrix
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++)
            cout << sq[i][j] << " ";
        cout << endl;
    }
}

// Driver Program to test above function
int main()
{
    int sq[3][3] = {
        { 0, 7, 6 },
        { 9, 0, 1 },
        { 4, 3, 0 }
    };

    printFilledDiagonal(sq);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to fill blanks with numbers

import java.io.*;

class GFG {

// Function to print the original matrix
static int printFilledDiagonal(int sq[][])
{
    // Calculate the sum of all the elements
    // of the matrix
    int sum = 0;
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            sum += sq[i][j];

    // Required sum of each row (from the approach)
    sum /= 2;

    for (int i = 0; i < 3; i++) {

        // Row sum excluding the diagonal element
        int rowSum = 0;
        for (int j = 0; j < 3; j++)
            rowSum += sq[i][j];

        // Element that must be inserted at
        // diagonal element of the current row
        sq[i][i] = sum - rowSum;
    }

    // Print the updated matrix
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++)
            System.out.print( sq[i][j] + " ");
        System.out.println();
    }
    return 0;
}

// Driver Program to test above function

    public static void main (String[] args) {
        int sq[][] = {
        { 0, 7, 6 },
        { 9, 0, 1 },
        { 4, 3, 0 }
    };

    printFilledDiagonal(sq);
    }

}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to fill blanks
# with numbers

# Function to print the original matrix
def printFilledDiagonal(sq):

    # Calculate the sum of all the
    # elements of the matrix
    Sum = 0
    for i in range(0, 3):
        for j in range(0, 3):
            Sum += sq[i][j]

    # Required sum of each
    # row (from the approach)
    Sum = Sum//2

    for i in range(0, 3):

        # Row sum excluding the
        # diagonal element
        rowSum = 0
        for j in range(0, 3):
            rowSum += sq[i][j]

        # Element that must be inserted
        # at diagonal element of the
        # current row
        sq[i][i] = Sum - rowSum

    # Print the updated matrix
    for i in range(0, 3):
        for j in range(0, 3):
            print(sq[i][j], end = " ")
        print()

# Driver Code
if __name__ == "__main__":

    sq = [[0, 7, 6],
          [9, 0, 1],
          [4, 3, 0]]

    printFilledDiagonal(sq)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to fill blanks with numbers

using System;

class GFG {

// Function to print the original matrix
static int printFilledDiagonal(int [,]sq)
{
    // Calculate the sum of all the elements
    // of the matrix
    int sum = 0;
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            sum += sq[i,j];

    // Required sum of each row (from the approach)
    sum /= 2;

    for (int i = 0; i < 3; i++) {

        // Row sum excluding the diagonal element
        int rowSum = 0;
        for (int j = 0; j < 3; j++)
            rowSum += sq[i,j];

        // Element that must be inserted at
        // diagonal element of the current row
        sq[i,i] = sum - rowSum;
    }

    // Print the updated matrix
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++)
            Console.Write( sq[i,j] + " ");
            Console.WriteLine();
    }
    return 0;
}

// Driver Program to test above function

    public static void Main () {
        int [,]sq = {
        { 0, 7, 6 },
        { 9, 0, 1 },
        { 4, 3, 0 }
    };

    printFilledDiagonal(sq);
    }

}
// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to fill blanks with numbers

// Function to print the original matrix
function printFilledDiagonal($sq)
{
    // Calculate the sum of all the
    // elements of the matrix
    $sum = 0;
    for ($i = 0; $i < 3; $i++)
        for ($j = 0; $j < 3; $j++)
            $sum += $sq[$i][$j];

    // Required sum of each row
    // (from the approach)
    $sum = (int)($sum / 2);

    for ($i = 0; $i < 3; $i++)
    {

        // Row sum excluding the
        // diagonal element
        $rowSum = 0;
        for ($j = 0; $j < 3; $j++)
            $rowSum += $sq[$i][$j];

        // Element that must be inserted at
        // diagonal element of the current row
        $sq[$i][$i] = $sum - $rowSum;
    }

    // Print the updated matrix
    for ($i = 0; $i < 3; $i++)
    {
        for ($j = 0; $j < 3; $j++)
            echo $sq[$i][$j] . " ";
        echo "\n";
    }
}

// Driver Code
$sq = array(array(0, 7, 6),
            array(9, 0, 1),
            array(4, 3, 0));

printFilledDiagonal($sq);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript program to fill blanks with numbers

    // Function to print the original matrix
    function printFilledDiagonal(sq)
    {
        // Calculate the sum of all the elements
        // of the matrix
        let sum = 0;
        for (let i = 0; i < 3; i++)
            for (let j = 0; j < 3; j++)
                sum += sq[i][j];

        // Required sum of each row (from the approach)
        sum /= 2;

        for (let i = 0; i < 3; i++) {

            // Row sum excluding the diagonal element
            let rowSum = 0;
            for (let j = 0; j < 3; j++)
                rowSum += sq[i][j];

            // Element that must be inserted at
            // diagonal element of the current row
            sq[i][i] = sum - rowSum;
        }

        // Print the updated matrix
        for (let i = 0; i < 3; i++) {
            for (let j = 0; j < 3; j++)
                document.write(sq[i][j] + " ");
            document.write("</br>");
        }
        return 0;
    }

    let sq = [
              [ 0, 7, 6 ],
              [ 9, 0, 1 ],
              [ 4, 3, 0 ]
              ];

    printFilledDiagonal(sq);

</script>
```

**Output:** 

```
2 7 6 
9 5 1 
4 3 8
```