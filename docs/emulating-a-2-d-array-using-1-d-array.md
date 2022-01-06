# 使用一维阵列模拟二维阵列

> 原文:[https://www . geesforgeks . org/仿真-a-2-d-array-使用-1-d-array/](https://www.geeksforgeeks.org/emulating-a-2-d-array-using-1-d-array/)

如何将大小为(m x n)的二维数组转换为一维数组，以及如何将二维数组的元素存储在一维数组中的[i，j]位置？显然，一维数组的大小是二维数组中元素的数量，即(m×n)。如果二维数组中的元素按行主顺序存储。然后，二维数组中索引[i，j]处的元素将存储在索引 k 处的一维数组中，如下所示:

**k = j+(I * total _ no _ of _ columns _ in _ matrix)**

如果二维数组中的元素以列主顺序存储，则索引 k 的值将为

**k = I+(j * total _ no _ of _ rows _ in _ matrix)**

关于行主和列主顺序的更多信息，请参考:[https://en.wikipedia.org/wiki/Row-major_order](https://en.wikipedia.org/wiki/Row-major_order)

**示例:**

```
Given 2-d array:

// array is formed in row-major order
    __________________________
   |                          |
   |1(0,0)    2(0,1)    3(0,2)|
   |                          |
   |4(1,0)    5(1,1)    6(1,2)|
   |__________________________|

// The elements in parenthesis represents the
// index of the particular element in 2-d array.

Index of element at (0,1) in 1-d array will be:
k(0,1) = 1 + 0 * 3 = 1

Index of element at (1,1) in 1-d array will be:
k(1,1) = 1 + 1 * 3 = 4 
```

## C++

```
// C++ program to emulate 2-d array using
// 1-d array
#include<stdio.h>
#define n 3
#define m 3
#define max_size 100
int main()
{

    // Initialising a 2-d array
    int grid[n][m] = {{1, 2, 3},
                      {4, 5, 6},
                      {7, 8, 9}};

    // storing elements in 1-d array
    int i, j, k = 0;
    int array[max_size];
    for (i=0; i<n; i++)
    {
        for (j=0; j<m; j++)
        {
            k = i*m + j;
            array[k] = grid[i][j];
            k++;
        }
    }

    // displaying elements in 1-d array
    for (i=0; i<n; i++)
    {
        for (j=0; j<m; j++)
            printf("%d ", *(array + i*m + j));
        printf("\n");
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to emulate 2-d array using
// 1-d array

class GFG
{
    // Driver program
    public static void main(String arg[])
    {
    // Declaring number of rows and columns
        int n = 3, m = 3;
        int array[]=new int[100];

        // Initialising a 2-d array
        int grid[][] = {{1, 2, 3},
                        {4, 5, 6},
                        {7, 8, 9}};

        // storing elements in 1-d array
        int i, j, k = 0;
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
            {
                k = i * m + j;
                array[k] = grid[i][j];
                k++;
            }
        }

        // displaying elements in 1-d array
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
                System.out.print((array[i * m + j])+" ");
            System.out.print("\n");
        }

    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to emulate 2-d
# array using 1-d array

# Declaring number of rows and columns
n = 3; m = 3

array = [0 for i in range(100)]

# Initialising a 2-d array
grid = [[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]];

# storing elements in 1-d array
k = 0

for i in range(n):
    for j in range(m):

        k = i*m + j
        array[k] = grid[i][j]
        k += 1

# displaying elements in 1-d array
for i in range(n):
    for j in range(m):
        print((array[i*m + j]), " ", end = "")
    print()

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to emulate 2-d array using
// 1-d array
using System;

class GFG
{
    // Driver program
    public static void Main()
    {
    // Declaring number of rows and columns
        int n = 3, m = 3;
        int []array=new int[100];

        // Initialising a 2-d array
        int [,]grid = {{1, 2, 3},
                        {4, 5, 6},
                        {7, 8, 9}};

        // storing elements in 1-d array
        int i, j, k = 0;
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
            {
                k = i * m + j;
                array[k] = grid[i, j];
                k++;
            }
        }

        // displaying elements in 1-d array
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < m; j++)
                Console.Write((array[i * m + j])+" ");
            Console.Write("\n");
        }

    }
}

// This code is contributed by nitin mittal
```

## java 描述语言

```
<script>

// Javascript program to emulate 2-d array using
// 1-d array

// Declaring number of rows and columns
let n = 3, m = 3;
let array = new Array(100);

// Initialising a 2-d array
let grid = [ [ 1, 2, 3 ],
             [ 4, 5, 6 ],
             [ 7, 8, 9 ] ];

// Storing elements in 1-d array
let i, j, k = 0;
for(i = 0; i < n; i++)
{
    for(j = 0; j < m; j++)
    {
        k = i * m + j;
        array[k] = grid[i][j];
        k++;
    }
}

// Displaying elements in 1-d array
for(i = 0; i < n; i++)
{
    for(j = 0; j < m; j++)
        document.write((array[i * m + j]) + " ");

    document.write("<br>");
}

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1  2  3  
4  5  6  
7  8  9 
```

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。