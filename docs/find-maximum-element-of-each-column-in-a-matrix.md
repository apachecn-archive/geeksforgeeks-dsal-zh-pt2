# 求矩阵中每列的最大元素

> 原文:[https://www . geeksforgeeks . org/find-矩阵中每列的最大元素数/](https://www.geeksforgeeks.org/find-maximum-element-of-each-column-in-a-matrix/)

给定一个矩阵，任务是找到每列的最大元素。
**例:**

```
Input:  [1, 2, 3]
         [1, 4, 9]
         [76, 34, 21]

Output:
76
34
21

Input: [1, 2, 3, 21]
        [12, 1, 65, 9]
        [1, 56, 34, 2]
Output:
12
56
65
21
```

**方法:**想法是运行 no_of_cols 的循环。检查列内的每个元素，找到最大元素。最后，打印元素。

以下是上述办法的实施:

## C++

```
// C++ program to find the maximum
// element of each column.
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100;

// Function to find the maximum
// element of each column.
void largestInColumn(int mat[][MAX], int rows, int cols)
{
    for (int i = 0; i < cols; i++) {
        // initialize the maximum element
        // with 0
        int maxm = mat[0][i];

        // Run the inner loop for rows
        for (int j = 1; j < rows; j++) {
            // check if any element is greater
            // than the maximum element
            // of the column and replace it
            if (mat[j][i] > maxm)
                maxm = mat[j][i];
        }

        // print the largest element of the column
        cout << maxm << endl;
    }
}

// Driver code
int main()
{
    int n = 4, m = 4;
    int mat[][MAX] = { { 3, 4, 1, 8 },
                       { 1, 4, 9, 11 },
                       { 76, 34, 21, 1 },
                       { 2, 1, 4, 5 } };

    largestInColumn(mat, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// element of each column in a matrix
public class GFG {

    // Function to find the maximum
    // element of each column.
    public static void largestInColumn(int cols, int[][] arr)
    {

        for (int i = 0; i < cols; i++) {

            // Initialize max to 0 at beginning
            // of finding max element of each column
            int maxm = arr[0][i];
            for (int j = 1; j < arr[i].length; j++)
                if (arr[j][i] > maxm)
                    maxm = arr[j][i];

            System.out.println(maxm);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[][] arr = new int[][] { { 3, 4, 1, 8 },
                                    { 1, 4, 9, 11 },
                                    { 76, 34, 21, 1 },
                                    { 2, 1, 4, 5 } };
        // Calling the function
        largestInColumn(4, arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# element of each column
MAX = 100

# function to find the maximum
# elements of each column
def largestInColumn(mat, rows, cols):
    for i in range(cols):

        # initialize the maximum element with 0
        maxm = mat[0][i]
        # run the inner loop for news
        for j in range(rows):

            # check if any elements is greater
            # than the maximum elements
            # of the column and replace it
            if mat[j][i] > maxm:
                maxm = mat[j][i]

        # print the largest element
        # of the column
        print(maxm)

# Driver code
n, m = 4, 4
mat = [[3, 4, 1, 8],
       [1, 4, 9, 11],
       [76, 34, 21, 1],
       [2, 1, 4, 5]]

largestInColumn(mat, n, m);

# This code is contributed
# by Mohit kumar 29 (IIIT gwalior)
```

## C#

```
// C# program to find maximum
// element of each column in a matrix
using System;

class GFG
{

// Function to find the maximum
// element of each column.
public static void largestInColumn(int cols,
                                   int[, ] arr)
{
    for (int i = 0; i < cols; i++)
    {

        // Initialize max to 0 at beginning
        // of finding max element of each column
        int maxm = arr[0, i];
        for (int j = 1; j < arr.GetLength(0); j++)
            if (arr[j, i] > maxm)
                maxm = arr[j, i];

        Console.WriteLine(maxm);
    }
}

// Driver code
public static void Main()
{
    int[, ] arr = new int[, ] { { 3, 4, 1, 8 },
                                { 1, 4, 9, 11 },
                                { 76, 34, 21, 1 },
                                { 2, 1, 4, 5 } };
    // Calling the function
    largestInColumn(4, arr);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// element of each column.
$MAX = 100;

// Function to find the maximum
// element of each column.
function largestInColumn($mat, $rows, $cols)
{
    for ($i = 0; $i < $cols; $i++)
    {
        // initialize the maximum element
        // with 0
        $maxm = $mat[0][$i];

        // Run the inner loop for rows
        for ($j = 1; $j < $rows; $j++)
        {
            // check if any element is greater
            // than the maximum element
            // of the column and replace it
            if ($mat[$j][$i] > $maxm)
                $maxm = $mat[$j][$i];
        }

        // print the largest element
        // of the column
        echo $maxm, "\n";
    }
}

// Driver code
$n = 4;
$m = 4;
$mat = array(array( 3, 4, 1, 8 ),
             array( 1, 4, 9, 11 ),
             array( 76, 34, 21, 1 ),
             array( 2, 1, 4, 5 ));

largestInColumn($mat, $n, $m);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// element of each column in a matrix

    // Function to find the maximum
    // element of each column.
    function largestInColumn(cols,arr)
    {

        for (let i = 0; i < cols; i++)
        {

            // Initialize max to 0 at beginning
            // of finding max element of each column
            let maxm = arr[0][i];
            for (let j = 1; j < arr[i].length; j++)
                if (arr[j][i] > maxm)
                    maxm = arr[j][i];

            document.write(maxm+"<br>");
        }
    }

    // Driver code
    let arr = [[ 3, 4, 1, 8 ],
               [ 1, 4, 9, 11 ],
               [ 76, 34, 21, 1 ],
               [ 2, 1, 4, 5 ]];
        // Calling the function
        largestInColumn(4, arr);

// This code is contributed by sravan kumar G

</script>
```

**Output:** 

```
76
34
21
11
```

**时间复杂度:** O(n * m)，这里 n 为行数，m 为列数。