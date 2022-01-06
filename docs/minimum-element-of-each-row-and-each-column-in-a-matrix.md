# 矩阵中每行每列的最小元素

> 原文:[https://www . geesforgeks . org/矩阵中每行每列的最小元素/](https://www.geeksforgeeks.org/minimum-element-of-each-row-and-each-column-in-a-matrix/)

给定一个矩阵，任务是找到每行和每列的最小元素。
**例:**

```
Input: [1, 2, 3]
        [1, 4, 9]
        [76, 34, 21]
Output: Minimum element of each row is {1, 1, 21}
Minimum element of each column is {1, 2, 3}

Input: [1, 2, 3, 21]
       [12, 1, 65, 9]
       [11, 56, 34, 2]
Output: Minimum element of each row is {1, 1, 21}
Minimum element of each column is {1, 2, 3}
```

**逼近**:思路是对 no _ of _ rows 运行循环。检查行内的每个元素，查找最小元素。最后，打印元素。同样，检查列中的每个元素，并查找最小元素。最后，打印元素。
以下是上述办法的实施情况:

## C++

```
// C++ program to find the minimum
// element of each row and each column
#include<bits/stdc++.h>
using namespace std;
const int MAX = 100;

// function to find the minimum
// element of each row.
void smallestInRow(int mat[][MAX], int n, int m)
{
    cout << " { ";
    for (int i = 0; i < n; i++) {

        // initialize the minimum element
        // as first element
        int minm = mat[i][0];

        for (int j = 1; j < m; j++) {

            // check if any element is smaller
            // than the minimum element of the row
            // and replace it
            if (mat[i][j] < minm)
                minm = mat[i][j];
        }

        // print the smallest element of the row
        cout << minm << ", ";
    }
    cout << "}";
}

// function to find the minimum
// element of each column.
void smallestInCol(int mat[][MAX], int n, int m)
{

    cout << " { ";
    for (int i = 0; i < m; i++) {

        // initialize the minimum element
        // as first element
        int minm = mat[0][i];

        // Run the inner loop for columns
        for (int j = 1; j < n; j++) {

            // check if any element is smaller
            // than the minimum element of the column
            // and replace it
            if (mat[j][i] < minm)
                minm = mat[j][i];
        }

        // print the smallest element of the row
        cout << minm << ", ";
    }

    cout << "}";
}

// Driver code
int main()
{

    int n = 3, m = 3;
    int mat[][MAX] = { { 2, 1, 7 },
                       { 3, 7, 2 },
                       { 5, 4, 9 } };

    cout << "Minimum element of each row is ";
    smallestInRow(mat, n, m);

    cout << "\nMinimum element of each column is ";
    smallestInCol(mat, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// element of each row and each column

public class GFG {

    final static int MAX = 100;

// function to find the minimum
// element of each row.
    static void smallestInRow(int mat[][], int n, int m) {
        System.out.print(" { ");
        for (int i = 0; i < n; i++) {

            // initialize the minimum element
            // as first element
            int minm = mat[i][0];

            for (int j = 1; j < m; j++) {

                // check if any element is smaller
                // than the minimum element of the row
                // and replace it
                if (mat[i][j] < minm) {
                    minm = mat[i][j];
                }
            }

            // print the smallest element of the row
            System.out.print(minm + ", ");
        }
        System.out.println("}");
    }

// function to find the minimum
// element of each column.
    static void smallestInCol(int mat[][], int n, int m) {

        System.out.print(" { ");
        for (int i = 0; i < m; i++) {

            // initialize the minimum element
            // as first element
            int minm = mat[0][i];

            // Run the inner loop for columns
            for (int j = 1; j < n; j++) {

                // check if any element is smaller
                // than the minimum element of the column
                // and replace it
                if (mat[j][i] < minm) {
                    minm = mat[j][i];
                }
            }

            // print the smallest element of the row
            System.out.print(minm + ", ");
        }

        System.out.print("}");
    }

// Driver code
    public static void main(String args[]) {
        int n = 3, m = 3;
        int mat[][] = {{2, 1, 7},
        {3, 7, 2},
        {5, 4, 9}};

        System.out.print("Minimum element of each row is ");
        smallestInRow(mat, n, m);

        System.out.print("\nMinimum element of each column is ");
        smallestInCol(mat, n, m);
    }
}

/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 program to find the minimum

MAX = 100

# function to find the minimum
# element of each row.
def smallestInRow(mat, n, m):
    print("{", end = "")
    for i in range(n):

        # initialize the minimum element
        # as first element
        minm = mat[i][0]

        for j in range(1, m, 1):

            # check if any element is smaller
            # than the minimum element of the
            # row and replace it
            if (mat[i][j] < minm):
                minm = mat[i][j]

        # print the smallest element
        # of the row
        print(minm, end = ",")

    print("}")

# function to find the minimum
# element of each column.
def smallestInCol(mat, n, m):
    print("{", end = "")
    for i in range(m):

        # initialize the minimum element
        # as first element
        minm = mat[0][i]

        # Run the inner loop for columns
        for j in range(1, n, 1):

            # check if any element is smaller
            # than the minimum element of the
            # column and replace it
            if (mat[j][i] < minm):
                minm = mat[j][i]

        # print the smallest element
        # of the row
        print(minm, end = ",")

    print("}")

# Driver code
if __name__ == '__main__':
    n = 3
    m = 3
    mat = [[2, 1, 7],
           [3, 7, 2 ],
           [ 5, 4, 9 ]];

    print("Minimum element of each row is",
                                 end = " ")
    smallestInRow(mat, n, m)

    print("Minimum element of each column is",
                                    end = " ")
    smallestInCol(mat, n, m)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find the minimum
// element of each row and each column
using System;

class GFG
{

readonly static int MAX = 100;

// function to find the minimum
// element of each row.
static void smallestInRow(int [,]mat,
                          int n, int m)
{
    Console.Write(" { ");

    for (int i = 0; i < n; i++)
    {

        // initialize the minimum element
        // as first element
        int minm = mat[i, 0];

        for (int j = 1; j < m; j++)
        {

            // check if any element is smaller
            // than the minimum element of the
            // row and replace it
            if (mat[i, j] < minm)
            {
                minm = mat[i, j];
            }
        }

        // print the smallest element
        // of the row
        Console.Write(minm + ", ");
    }
    Console.WriteLine("}");
}

// function to find the minimum
// element of each column.
static void smallestInCol(int [,]mat,
                          int n, int m)
{

    Console.Write(" { ");
    for (int i = 0; i < m; i++)
    {

        // initialize the minimum element
        // as first element
        int minm = mat[0, i];

        // Run the inner loop for columns
        for (int j = 1; j < n; j++)
        {

            // check if any element is smaller
            // than the minimum element of the
            // column and replace it
            if (mat[j, i] < minm)
            {
                minm = mat[j, i];
            }
        }

        // print the smallest element
        // of the row
        Console.Write(minm + ", ");
    }

    Console.Write("}");
}

// Driver code
public static void Main()
{
    int n = 3, m = 3;
    int [,]mat = {{2, 1, 7},
                   {3, 7, 2},
                  {5, 4, 9}};

    Console.Write("Minimum element of " +
                         "each row is ");
    smallestInRow(mat, n, m);

    Console.Write("\nMinimum element of " +
                        "each column is ");
    smallestInCol(mat, n, m);
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// element of each row and each column
$MAX = 100;

// function to find the minimum
// element of each row.
function smallestInRow(&$mat, $n, $m)
{
    echo " { ";
    for ($i = 0; $i < $n; $i++)
    {

        // initialize the minimum element
        // as first element
        $minm = $mat[$i][0];

        for ($j = 1; $j < $m; $j++)
        {

            // check if any element is smaller
            // than the minimum element of the
            // row and replace it
            if ($mat[$i][$j] < $minm)
                $minm = $mat[$i][$j];
        }

        // print the smallest element
        // of the row
        echo $minm . ", ";
    }
    echo "}";
}

// function to find the minimum
// element of each column.
function smallestInCol(&$mat, $n, $m)
{
    echo " { ";
    for ($i = 0; $i < $m; $i++)
    {

        // initialize the minimum element
        // as first element
        $minm = $mat[0][$i];

        // Run the inner loop for columns
        for ($j = 1; $j < $n; $j++)
        {

            // check if any element is smaller
            // than the minimum element of the column
            // and replace it
            if ($mat[$j][$i] < $minm)
                $minm = $mat[$j][$i];
        }

        // print the smallest element of the row
        echo $minm . ", ";
    }

    echo "}";
}

// Driver code
$n = 3;
$m = 3;
$mat = array(array( 2, 1, 7 ),
             array( 3, 7, 2 ),
             array( 5, 4, 9 ));

echo "Minimum element of each row is ";
smallestInRow($mat, $n, $m);

echo "\nMinimum element of each column is ";
smallestInCol($mat, $n, $m);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Java script program to find the minimum
// element of each row and each column

let MAX = 100;

// function to find the minimum
// element of each row.
    function smallestInRow(mat,n,m) {
        document.write(" { ");
        for (let i = 0; i < n; i++) {

            // initialize the minimum element
            // as first element
            let minm = mat[i][0];

            for (let j = 1; j < m; j++) {

                // check if any element is smaller
                // than the minimum element of the row
                // and replace it
                if (mat[i][j] < minm) {
                    minm = mat[i][j];
                }
            }

            // print the smallest element of the row
            document.write(minm + ", ");
        }
        document.write("}"+"<br>");
    }

// function to find the minimum
// element of each column.
    function smallestInCol(mat,n,m) {

        document.write(" { ");
        for (let i = 0; i < m; i++) {

            // initialize the minimum element
            // as first element
            let minm = mat[0][i];

            // Run the inner loop for columns
            for (let j = 1; j < n; j++) {

                // check if any element is smaller
                // than the minimum element of the column
                // and replace it
                if (mat[j][i] < minm) {
                    minm = mat[j][i];
                }
            }

            // print the smallest element of the row
            document.write(minm + ", ");
        }

        document.write("}");
    }

// Driver code

        let n = 3, m = 3;
        let mat = [[2, 1, 7],
        [3, 7, 2],
        [5, 4, 9]];

        document.write("Minimum element of each row is ");
        smallestInRow(mat, n, m);

        document.write("\nMinimum element of each column is ");
        smallestInCol(mat, n, m);

// This code is contributed by Bobby
</script>
```

**Output:** 

```
Minimum element of each row is  { 1, 2, 4, }
Minimum element of each column is  { 2, 1, 2, }
```

**时间复杂度:** O(n*m)