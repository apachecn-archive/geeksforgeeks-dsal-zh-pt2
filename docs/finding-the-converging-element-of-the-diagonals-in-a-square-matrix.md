# 求方阵对角线的收敛元素

> 原文:[https://www . geesforgeks . org/find-正方形矩阵中对角线的收敛元素/](https://www.geeksforgeeks.org/finding-the-converging-element-of-the-diagonals-in-a-square-matrix/)

给定一个正方形矩阵，任务是找到这个正方形矩阵的左右对角线收敛的矩阵元素。
**例:**

```
Input: n = 5, matrix = 
[ 1 2 3 4 5
  5 6 7 8 6
  9 5 6 8 7
  2 3 5 6 8
  1 2 3 4 5 ]
Output: 6

Input: n = 4, matrix = 
[ 1 2 3 4
  5 6 7 8
  9 0 1 2 
  4 5 6 1 ]
Output: NULL
Here there no converging element at all. 
Hence the answer is null.
```

**进场:**

*   如果矩阵的行数和列数是偶数，那么我们只打印 NULL，因为在行数和列数都是偶数的情况下不会有收敛元素。
*   如果矩阵的行数和列数为奇数，求 n 的中间值为

```
mid = n/2
```

*   arr[mid][mid]本身就是收敛的对角元素。

以下是上述方法的实现:

## C++

```
// C++ program to find the converging element
// of the diagonals in a square matrix

#include <malloc.h>
#include <stdio.h>
#include <stdlib.h>

// Driver code
int main()
{
    int n = 5;
    int a[][5] = { { 1, 2, 3, 4, 5 },
                   { 5, 6, 7, 8, 6 },
                   { 9, 5, 6, 8, 7 },
                   { 2, 3, 5, 6, 8 },
                   { 1, 2, 3, 4, 5 } };

    int convergingele, mid;
    int i, j;

    // If n is even, then convergence
    // element will be null.
    if (n % 2 == 0) {
        printf("NULL\n");
    }

    else {
        // finding the mid
        mid = n / 2;

        // finding the converging element
        convergingele = a[mid][mid];

        printf("%d\n", convergingele);
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the converging element
// of the diagonals in a square matrix
class GFG
{

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        int a[][] = {{1, 2, 3, 4, 5},
                     {5, 6, 7, 8, 6},
                     {9, 5, 6, 8, 7},
                     {2, 3, 5, 6, 8},
                     {1, 2, 3, 4, 5}};

        int convergingele, mid;
        int i, j;

        // If n is even, then convergence
        // element will be null.
        if (n % 2 == 0)
        {
            System.out.printf("NULL\n");
        }
        else
        {
            // finding the mid
            mid = n / 2;

            // finding the converging element
            convergingele = a[mid][mid];

            System.out.printf("%d\n", convergingele);
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the converging element
# of the diagonals in a square matrix

# Driver code
n = 5
a = [[ 1, 2, 3, 4, 5 ],
     [ 5, 6, 7, 8, 6 ],
     [ 9, 5, 6, 8, 7 ],
     [ 2, 3, 5, 6, 8 ],
     [ 1, 2, 3, 4, 5 ]]

# If n is even, then convergence
# element will be null.
if (n % 2 == 0):
    print("NULL")
else :

    # finding the mid
    mid = n // 2

    # finding the converging element
    convergingele = a[mid][mid]

    print(convergingele)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# iprogram to find the converging element
// of the diagonals in a square matrix
using System;

class GFG
{

    // Driver code
    public static void Main(String []args)
    {
        int n = 5;
        int [,]a = {{1, 2, 3, 4, 5},
                    {5, 6, 7, 8, 6},
                    {9, 5, 6, 8, 7},
                    {2, 3, 5, 6, 8},
                    {1, 2, 3, 4, 5}};

        int convergingele, mid;

        // If n is even, then convergence
        // element will be null.
        if (n % 2 == 0)
        {
            Console.Write("NULL\n");
        }
        else
        {
            // finding the mid
            mid = n / 2;

            // finding the converging element
            convergingele = a[mid,mid];

            Console.Write("{0}\n", convergingele);
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the converging element
// of the diagonals in a square matrix

// Driver code
    let n = 5;
    let a = [ [ 1, 2, 3, 4, 5 ],
                   [ 5, 6, 7, 8, 6 ],
                   [ 9, 5, 6, 8, 7 ],
                   [ 2, 3, 5, 6, 8 ],
                   [ 1, 2, 3, 4, 5 ] ];

    let convergingele, mid;
    let i, j;

    // If n is even, then convergence
    // element will be null.
    if (n % 2 == 0) {
        document.write("NULL<br>");
    }

    else
    {

        // finding the mid
        mid = parseInt(n / 2);

        // finding the converging element
        convergingele = a[mid][mid];

        document.write(convergingele + "<br>");
    }

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
6
```