# 填充对角线，使每一行、每一列、每一对角线之和等于 3×3 矩阵

> 原文:[https://www . geeksforgeeks . org/filling-对角线对每行列和对角线之和等于 3×3 矩阵/](https://www.geeksforgeeks.org/filling-diagonal-to-make-the-sum-of-every-row-column-and-diagonal-equal-of-3x3-matrix/)

给定一个**3×3**矩阵中的 9 个元素，其中对角线的值为 **0** 。我们需要找到对角线上的值，使每行、每列和对角线的总和相等。
**例:**

```
Input: 
0 3 6 
5 0 5
4 7 0
Output: 
6 3 6
5 5 5
4 7 4
Explanation: 
    Now the value of the sum of 
    any row or column is 15

Input: 
0 4 4
4 0 4
4 4 0
Output: 
4 4 4
4 4 4
4 4 4
```

**进场:**

*   假设对角线是 x，y 和 z。
*   x 的值为 **( x <sub>2，3</sub> + x <sub>3，2</sub> ) / 2。**
*   z 值为 **( x <sub>1，2</sub> + x <sub>2，1</sub> ) / 2。**
*   y 的值将是 **( x + z ) / 2。**

以下是上述方法的实施:
**程序:**

## C++

```
// C++ program to implement
// the above problem

#include <bits/stdc++.h>
using namespace std;

// Function to print the matrix
void print(int arr[3][3])
{
    int i = 0, j = 0;

    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++)
            cout << arr[i][j] << " ";
        cout << endl;
    }
}

// Function to find the diagonal values
void find(int arr[3][3])
{
    arr[0][0] = (arr[1][2] + arr[2][1]) / 2;
    arr[2][2] = (arr[0][1] + arr[1][0]) / 2;
    arr[1][1] = (arr[0][0] + arr[1][1]) / 2;

    // Print the new matrix with diagonals
    cout << "Matrix with diagonals:\n";
    print(arr);
}

// Driver code
int main()
{
    // Initialize all the elements of a matrix
    int arr[3][3] = { { 0, 54, 48 },
                      { 36, 0, 78 },
                      { 66, 60, 0 } };

    cout << "Matrix initially:\n";
    print(arr);

    find(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above problem
class GFG
{

// Function to print the matrix
static void print(int arr[][])
{
    int i = 0, j = 0;

    for (i = 0; i < 3; i++)
    {
        for (j = 0; j < 3; j++)
            System.out.print( arr[i][j] + " ");
        System.out.println();
    }
}

// Function to find the diagonal values
static void find(int arr[][])
{
    arr[0][0] = (arr[1][2] + arr[2][1]) / 2;
    arr[2][2] = (arr[0][1] + arr[1][0]) / 2;
    arr[1][1] = (arr[0][0] + arr[1][1]) / 2;

    // Print the new matrix with diagonals
    System.out.print( "Matrix with diagonals:\n");
    print(arr);
}

// Driver code
public static void main(String args[])
{
    // Initialize all the elements of a matrix
    int arr[][] = { { 0, 54, 48 },
                    { 36, 0, 78 },
                    { 66, 60, 0 } };

    System.out.print( "Matrix initially:\n");
    print(arr);

    find(arr);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to implement
# the above problem

# Function to print the matrix
def print_(arr, n):
    for i in range(n):
        for j in range(n):
            print(arr[i][j], end = " ")
        print("\n", end= "")

# Function to find the diagonal values
def find(arr, n):
    arr[0][0] = (arr[1][2] + arr[2][1]) // 2
    arr[2][2] = (arr[0][1] + arr[1][0]) // 2
    arr[1][1] = (arr[0][0] + arr[1][1]) // 2
    print("\nMatrix with diagonals:")
    print_(arr, n)

# Driver code
arr = [[0, 54, 48],
       [36, 0, 78],
       [66, 60, 0]]

n = 3
print("Matrix initially:")
print_(arr, n)
find(arr, n)

# This code is contributed by Shrikant13
```

## C#

```
// C# program to implement
// the above problem
using System;

class GFG
{

    // Function to print the matrix
    static void print(int [,]arr)
    {
        int i = 0, j = 0;

        for (i = 0; i < 3; i++)
        {
            for (j = 0; j < 3; j++)
                Console.Write( arr[i, j] + " ");

            Console.WriteLine();
        }
    }

    // Function to find the diagonal values
    static void find(int [,]arr)
    {
        arr[0, 0] = (arr[1, 2] + arr[2, 1]) / 2;
        arr[2, 2] = (arr[0, 1] + arr[1, 0]) / 2;
        arr[1, 1] = (arr[0, 0] + arr[1, 1]) / 2;

        // Print the new matrix with diagonals
        Console.Write( "Matrix with diagonals:\n");
        print(arr);
    }

    // Driver code
    public static void Main()
    {
        // Initialize all the elements of a matrix
        int [,]arr = { { 0, 54, 48 },
                        { 36, 0, 78 },
                        { 66, 60, 0 } };

        Console.Write( "Matrix initially:\n");
        print(arr);

        find(arr);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above problem Function
// to print the matrix
function printt( $arr)
{
    $i = 0;
    $j = 0;

    for ($i = 0; $i < 3; $i++)
    {
        for ($j = 0; $j < 3; $j++)
            echo $arr[$i][$j], " ";
        echo "\n";
    }
}

// Function to find the diagonal values
function find( $arr)
{
    $arr[0][0] = ($arr[1][2] + $arr[2][1]) / 2;
    $arr[2][2] = ($arr[0][1] + $arr[1][0]) / 2;
    $arr[1][1] = ($arr[0][0] + $arr[1][1]) / 2;

    // Print the new matrix with diagonals
    echo "Matrix with diagonals:\n";
    printt($arr);
}

// Driver code

// Initialize all the elements of a matrix
$arr =array(array( 0, 54, 48 ),
        array( 36, 0, 78 ),
        array( 66, 60, 0 ));

echo "Matrix initially:\n";
printt($arr);

find($arr);

#This Code is contributed by ajit..
?>
```

## java 描述语言

```
<script>
// Java script program to implement
// the above problem

// Function to print the matrix
function print(arr)
{
    let i = 0, j = 0;

    for (i = 0; i < 3; i++)
    {
        for (j = 0; j < 3; j++)
            document.write( parseInt(arr[i][j]) + " ");
        document.write("<br>");
    }
}

// Function to find the diagonal values
function find(arr)
{
    arr[0][0] = (arr[1][2] + arr[2][1]) / 2;
    arr[2][2] = (arr[0][1] + arr[1][0]) / 2;
    arr[1][1] = (arr[0][0] + arr[1][1]) / 2;

    // Print the new matrix with diagonals
    document.write( "Matrix with diagonals:<br>");
    print(arr);
}

// Driver code

    // Initialize all the elements of a matrix
    let arr = [[ 0, 54, 48 ],
                    [36, 0, 78 ],
                    [ 66, 60, 0 ]];

    document.write( "Matrix initially:<br>");
    print(arr);

    find(arr);

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
Matrix initially:
0 54 48 
36 0 78 
66 60 0 

Matrix with diagonals:
69 54 48 
36 34 78 
66 60 45
```