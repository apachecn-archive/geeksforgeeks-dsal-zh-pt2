# 计算行/列的总和等于对角线总和

> 原文:[https://www . geesforgeks . org/count-rowscolumns-with-sum-equal-to-对角线-sum/](https://www.geeksforgeeks.org/count-rowscolumns-with-sum-equals-to-diagonal-sum/)

给定一个 n×n 的方阵，计算其和等于任何主对角线或次对角线之和的所有行和列。

示例:

```
Input : n = 3   
arr[][] = { {1, 2, 3},
            {4, 5, 2},
            {7, 9, 10}};
Output : 2
In first example sum of principal diagonal 
= (1 + 5 + 10) = 16  and sum of secondary 
diagonal = (3 + 5 + 7) = 15.

Input:  n = 4
 arr[][] =  { { 7, 2, 3, 5 },
              { 4, 5, 6, 3 },
              { 7, 9, 10, 12 },
              { 1, 5, 4, 3 } };
Output: 1      

```

我们需要计算总和等于 16 或 15 的行数或列数。所以求所有行和列的和，如果它们的和等于 16 或 15，那么增加计数。
因此，列{2，5，9}的和= 16，列{3，2，10}的和= 15。因此，计数等于 **2。**

## C++

```
// C++ program to Count number of rows and
// columns having sum is equal to sum of 
// any diagonal in matrix
#include <iostream>
#define n 4
using namespace std;

// function to count number of rows countnd columns
// whose sum is equal to sum of any diagonal
int count(int arr[][n])
{
    int diag1 = 0, diag2 = 0;
    int row = 0, col = 0, count = 0;

    for (int i = 0, j = n - 1; i < n; i++, j--)
    {
        // sum of principle diagonal
        diag1 += arr[i][i];

        // sum of secondary diagonal
        diag2 += arr[i][j];
    }

    // Find the sum of individual
    // row and column
    for (int i = 0; i < n; i++) {
        row = 0, col = 0;

        for (int j = 0; j < n; j++) {
            row = row + arr[i][j];
        }
        for (int j = 0; j < n; j++) {
            col = col + arr[j][i];
        }
        if ((row == diag1) || (row == diag2)) {
            count++;
        }
        if ((col == diag1) || (col == diag2))
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int arr[n][n] = { { 7, 2, 3, 5 },
                    { 4, 5, 6, 3 },
                    { 7, 9, 10, 12 },
                    { 1, 5, 4, 3 } };    
    cout << count(arr) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count number of rows and
// columns having sum is equal to sum of
// any diagonal in matrix

import java.io.*;

class GFG {

    static int n = 4;

    // function to count number of rows countnd 
    // columns whose sum is equal to sum of any
    // diagonal
    static int count(int arr[][])
    {

        int diag1 = 0, diag2 = 0;
        int row = 0, col = 0, count = 0;

        for (int i = 0, j = n - 1; i < n; i++, j--) 
        {

            // sum of principle diagonal
            diag1 += arr[i][i];

            // sum of secondary diagonal
            diag2 += arr[i][j];
        }

        // Find the sum of individual
        // row and column
        for (int i = 0; i < n; i++) {
            row = 0;
            col = 0;

            for (int j = 0; j < n; j++) {
                row = row + arr[i][j];
            }

            for (int j = 0; j < n; j++) {
                col = col + arr[j][i];
            }

            if ((row == diag1) || (row == diag2)) 
                count++;

            if ((col == diag1) || (col == diag2))
                count++;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[][] = {{7, 2, 3, 5},
                        {4, 5, 6, 3},
                        {7, 9, 10, 12},
                        {1, 5, 4, 3}};

        System.out.println(count(arr));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to Count number of rows 
# and columns having sum is equal to sum  
# of any diagonal in matrix
n = 4

# Function to count number of rows
# countnd columns whose sum is equal
# to sum of any diagonal
def count(arr):
    diag1 = 0; diag2 = 0; row = 0
    col = 0; count = 0; j = n - 1

    for i in range(n):

        # sum of principle diagonal
        diag1 += arr[i][i]

        # sum of secondary diagonal
        diag2 += arr[i][j]
        j -= 1

    # Find the sum of individual
    # row and column
    for i in range(n):
        row = 0; col = 0

        for j in range(n):
            row += arr[i][j]

        for j in range(n):
            col +=  arr[j][i]

        if ((row == diag1) or (row == diag2)):
            count += 1

        if ((col == diag1) or (col == diag2)):
            count += 1

    return count

# Driver code

arr = [[ 7, 2, 3, 5 ],
      [ 4, 5, 6, 3 ],
      [ 7, 9, 10, 12 ],
      [ 1, 5, 4, 3 ] ] 
print(count(arr))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to Count number of rows and
// columns having sum is equal to sum of
// any diagonal in matrix
using System;

namespace Matrix
{
public class GFG
{     

static int n = 4;

    // Function to count number of rows  
    // countnd columns whose sum is equal 
    // to sum of any diagonal
    static int count(int [,]arr)
    {

        int diag1 = 0, diag2 = 0;
        int row = 0, col = 0, count = 0;

        for (int i = 0, j = n - 1; i < n; i++, j--) 
        {

            // sum of principle diagonal
            diag1 += arr[i,i];

            // sum of secondary diagonal
            diag2 += arr[i,j];
        }

        // Find the sum of individual
        // row and column
        for (int i = 0; i < n; i++) {
            row = 0;
            col = 0;

            for (int j = 0; j < n; j++) {
                row = row + arr[i,j];
            }

            for (int j = 0; j < n; j++) {
                col = col + arr[j,i];
            }

            if ((row == diag1) || (row == diag2)) 
                count++;

            if ((col == diag1) || (col == diag2))
                count++;
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int [,]arr = {  { 7, 2, 3, 5 },
                        { 4, 5, 6, 3 },
                        { 7, 9, 10, 12 },
                        { 1, 5, 4, 3 } }; 
        Console.Write(count(arr));
    }
} 
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Count number of rows and
// columns having sum is equal to sum of 
// any diagonal in matrix

// function to count number of 
// rows countnd columns whose 
// sum is equal to sum of any diagonal
function countt($arr)
{
    $diag1 = 0; $diag2 = 0;
    $row = 0; $col = 0;
    $count = 0;$n = 4;

    for ($i = 0, $j = $n - 1; $i < $n; $i++, $j--)
    {

        // sum of principle diagonal
        $diag1 += $arr[$i][$i];

        // sum of secondary diagonal
        $diag2 += $arr[$i][$j];
    }

    // Find the sum of individual
    // row and column
    for ($i = 0; $i < $n; $i++) {
        $row = 0; $col = 0;

        for ($j = 0; $j < $n; $j++) {
            $row = $row + $arr[$i][$j];
        }
        for ($j = 0; $j < $n; $j++) {
            $col = $col + $arr[$j][$i];
        }
        if (($row == $diag1) || ($row == $diag2)) {
            $count++;
        }
        if (($col == $diag1) || ($col == $diag2))
            $count++;
    }

    return $count;
}

// Driver code
{
    $arr = array(array(7, 2, 3, 5),
                 array(4, 5, 6, 3),
                 array(7, 9, 10, 12),
                 array(1, 5, 4, 3)); 
    echo countt($arr) ;
}

// This code is contributed by nitin mittal.
?>
```

输出:

```
1
```