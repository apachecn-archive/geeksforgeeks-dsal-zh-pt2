# 神奇图案

> 原文:[https://www.geeksforgeeks.org/magical-pattern/](https://www.geeksforgeeks.org/magical-pattern/)

给定一个整数 N 作为输入，任务是打印魔法图案，如下所示:

> n。。3 2 1 2 3 .。N
> 。。。。。。。。。。。
> 3 3 3 3 2 1 2 3 3 3 3
> 2 2 2 2 1 2 2 2 2 2 2
> 1 1 1 1 1 1 1 1
> 2 2 2 1 2 2 2 2 2 2 2
> 3 3 3 1 2 3 3 3 3 3 3
> 。。。。。。。。。。。
> 北。3 2 1 2 3 .。N

**例:**

```
Input: 3
Output: 
        3 2 1 2 3 
        2 2 1 2 2  
        1 1 1 1 1 
        2 2 1 2 2 
        3 2 1 2 3 

Input: 4
Output: 
        4 3 2 1 2 3 4                                                                   
        3 3 2 1 2 3 3                                                                   
        2 2 2 1 2 2 2                                                                   
        1 1 1 1 1 1 1                                                                   
        2 2 2 1 2 2 2                                                                   
        3 3 2 1 2 3 3                                                                   
        4 3 2 1 2 3 4  
```

**进场:**

1.  考虑输入 N = 3，因此重叠矩阵的行= 5，列= 5(即 2 * N–1)，所有条目为零。
2.  定义三个变量 start = N，inc = 0 和 dec = 2 * N–1 进行操作。
3.  运行一个循环，直到开始变为零。
4.  带有 inc 或(dec–1)的行或带有 inc 或(dec–1)的列用起始值填充。
    因此在开始=3 时
    矩阵将是
    3 3 3 3 3 3 3
    3 0 0 0 3
    3 0 0 3
    3 0 0 3
    3 3 3 3 3

5.  递减 dec、start 和递增 inc 值。
6.  重复步骤 3
7.  循环将在 start=0 时停止，并获得所需的模式

以下是上述方法的实现:

## C++

```
// C++ program to print the magical pattern

#include <iostream>
using namespace std;

void overLapping(int N, int matrix[100][100])
{

    int max, inc = 0, dec, start;

    // The size of matrix
    max = 2 * N - 1;

    // Fixing the range
    dec = max;

    // Overlapping value
    start = N;

    while (start != 0) {
        for (int row = 0; row < max; row++) {
            for (int col = 0; col < max; col++) {
                if (row == inc
                    || row == dec - 1
                    || col == dec - 1
                    || col == inc) {

                    matrix[row][col] = start;
                }
            }
        }
        start--;
        inc++;
        dec--;
    }

    // return matrix;
}

void DisplayMatrix(int matrix[][100], int max)
{
    // To display the overlapping matrix
    for (int row = 0; row < max; row++) {
        for (int col = 0; col < max; col++) {
            cout <<" "<< matrix[row][col];
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int N;

    // Get the value of N
    N = 3;

    // Declaring the overlapping matrix
    int matrix[100][100];

    // Create the magical matrix
    overLapping(N, matrix);

    // Print the magical matrix
    DisplayMatrix(matrix, (2 * N - 1));
}
```

## C

```
// C program to print the magical pattern
#include <stdio.h>

void overLapping(int N, int matrix[100][100])
{

    int max, inc = 0, dec, start;

    // The size of matrix
    max = 2 * N - 1;

    // Fixing the range
    dec = max;

    // Overlapping value
    start = N;

    while (start != 0) {
        for (int row = 0; row < max; row++) {
            for (int col = 0; col < max; col++) {
                if (row == inc
                    || row == dec - 1
                    || col == dec - 1
                    || col == inc) {

                    matrix[row][col] = start;
                }
            }
        }
        start--;
        inc++;
        dec--;
    }

    // return matrix;
}

void DisplayMatrix(int matrix[][100], int max)
{
    // To display the overlapping matrix
    for (int row = 0; row < max; row++) {
        for (int col = 0; col < max; col++) {
            printf("%d ", matrix[row][col]);
        }
        printf("\n");
    }
}

// Driver code
int main()
{
    int N = 3;

    // Declaring the overlapping matrix
    int matrix[100][100];

    // Create the magical matrix
    overLapping(N, matrix);

    // Print the magical matrix
    DisplayMatrix(matrix, (2 * N - 1));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the magical pattern

class GFG {

    static void overLapping(int N, int matrix[][]) {

        int max, inc = 0, dec, start;

        // The size of matrix
        max = 2 * N - 1;

        // Fixing the range
        dec = max;

        // Overlapping value
        start = N;

        while (start != 0) {
            for (int row = 0; row < max; row++) {
                for (int col = 0; col < max; col++) {
                    if (row == inc
                            || row == dec - 1
                            || col == dec - 1
                            || col == inc) {

                        matrix[row][col] = start;
                    }
                }
            }
            start--;
            inc++;
            dec--;
        }

        // return matrix;
    }

    static void DisplayMatrix(int matrix[][], int max) {
        // To display the overlapping matrix
        for (int row = 0; row < max; row++) {
            for (int col = 0; col < max; col++) {
                System.out.printf("%d ", matrix[row][col]);
            }
            System.out.printf("\n");
        }
    }

// Driver code
    public static void main(String[] args) {
        int N = 3;

        // Declaring the overlapping matrix
        int matrix[][] = new int[100][100];

        // Create the magical matrix
        overLapping(N, matrix);

        // Print the magical matrix
        DisplayMatrix(matrix, (2 * N - 1));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 program to print the magical pattern

def overLapping(N, matrix):

    inc = 0

    # The size of matrix
    Max = 2 * N - 1

    # Fixing the range
    dec = Max

    # Overlapping value
    start = N

    while (start != 0):
        for row in range(Max):
            for col in range(Max):
                if (row == inc or row == dec - 1 or
                    col == dec - 1 or col == inc):
                    matrix[row][col] = start

        start -= 1
        inc += 1
        dec -= 1

    # return matrix

def DisplayMatrix(matrix, Max):

    # To display the overlapping matrix
    for row in range(Max):
        for col in range(Max):
            print(matrix[row][col], end = " ")

        print()

# Driver code

# Get the value of N
N = 3

# Declaring the overlapping matrix
matrix = [[0 for i in range(100)]
             for i in range(100)]

# Create the magical matrix
overLapping(N, matrix)

# Print the magical matrix
DisplayMatrix(matrix, (2 * N - 1))

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# program to print the magical pattern
using System;

class GFG
{
public static void overLapping(int N,
                               int[,] matrix)
{
    int max, inc = 0, dec, start;
    max = 2 * N - 1;
    dec = max;
    start = N;

    while (start != 0)
    {
        for (int row = 0; row < max; row++)
        {
            for (int col = 0; col < max; col++)
            {
                if (row == inc || row == dec - 1 ||
                    col == dec - 1 || col == inc)
                {
                    matrix[row, col] = start;
                }
            }
        }
        start--;
        inc++;
        dec--;
    }
}

public static void DisplayMatrix(int[,] matrix, int max)
{
    for (int row = 0; row < max; row++)
    {
        for (int col = 0; col < max; col++)
        {
            Console.Write(" {0}", matrix[row, col]);
        }
        Console.Write("\n");
    }
}

// Driver Code
public static void Main()
{
    int N;
    N = 3;

    int[,] matrix = new int[100, 100];

    overLapping(N, matrix);
    DisplayMatrix(matrix, (2 * N - 1));
}
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the magical pattern

function overLapping($N, &$matrix)
{

    $max; $inc = 0; $dec; $start;

    // The size of matrix
    $max = 2 * $N - 1;

    // Fixing the range
    $dec = $max;

    // Overlapping value
    $start = $N;

    while ($start != 0)
    {
        for ($row = 0; $row < $max; $row++)
        {
            for ($col = 0; $col < $max; $col++)
            {
                if ($row == $inc || $row == $dec - 1 ||
                    $col == $dec - 1 || $col == $inc)
                {
                    $matrix[$row][$col] = $start;
                }
            }
        }
        $start--;
        $inc++;
        $dec--;
    }

    // return matrix;
}

function DisplayMatrix($matrix, $max)
{
    // To display the overlapping matrix
    for ($row = 0; $row < $max; $row++)
    {
        for ($col = 0; $col < $max; $col++)
        {
            echo $matrix[$row][$col] . " ";
        }
        echo "\n";
    }
}

// Driver code

// Get the value of N
$N = 3;

// Declaring the overlapping matrix
$matrix = array();

// Create the magical matrix
overLapping($N, $matrix);

// Print the magical matrix
DisplayMatrix($matrix, (2 * $N - 1));

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to print the magical pattern

    function overLapping(N,matrix)
    {
        let max, inc = 0, dec, start;

        // The size of matrix
        max = 2 * N - 1;

        // Fixing the range
        dec = max;

        // Overlapping value
        start = N;

        while (start != 0) {
            for (let row = 0; row < max; row++) {
                for (let col = 0; col < max; col++) {
                    if (row == inc
                            || row == dec - 1
                            || col == dec - 1
                            || col == inc) {

                        matrix[row][col] = start;
                    }
                }
            }
            start--;
            inc++;
            dec--;
        }

        // return matrix;
    }

    function DisplayMatrix(matrix,max)
    {
        // To display the overlapping matrix
        for (let row = 0; row < max; row++) {
            for (let col = 0; col < max; col++) {
                document.write( matrix[row][col]+" ");
            }
            document.write("<br>");
        }
    }

    // Driver code
    let N = 3;
    // Declaring the overlapping matrix
    let matrix = new Array(100);
    for(let i=0;i<100;i++)
    {
        matrix[i]=new Array(100);
    }

    // Create the magical matrix
    overLapping(N, matrix);

    // Print the magical matrix
    DisplayMatrix(matrix, (2 * N - 1));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
3 2 1 2 3 
2 2 1 2 2 
1 1 1 1 1 
2 2 1 2 2 
3 2 1 2 3
```