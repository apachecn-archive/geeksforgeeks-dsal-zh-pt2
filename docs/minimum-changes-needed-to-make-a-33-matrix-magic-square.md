# 制作 3*3 矩阵幻方所需的最小改动

> 原文:[https://www . geeksforgeeks . org/制作 33 矩阵幻方所需的最小改动/](https://www.geeksforgeeks.org/minimum-changes-needed-to-make-a-33-matrix-magic-square/)

给定一个 3*3 的矩阵，找到需要对其进行的**最小改变次数**，以便将其变成一个幻方。幻方是所有行的和相同，所有列的和相同，两条对角线的和相同的方阵。

**示例:**

```
Input :  8 5 6 
         3 8 7 
         4 9 2 
Output : 2
5 in row 1 col 2 should be changed to 1
8 in row 2 col 2 should be changed to 5
Total 2 changes are required.

Input : 8 9 4 
        5 9 3 
        6 1 8 
Output : 3
8 in row 1 col 1 should be changed to 2
5 in row 2 col 1 should be changed to 7
9 in row 2 col 2 should be changed to 5
Total 3 changes are required.
```

有 3*3 维的 **8** 可能的[幻方](https://www.geeksforgeeks.org/magic-square/)，分别是
8 1 6
3 5 7
4 9 2

6 1 8
7 5 3
2 9 4

4 9 2
3 5 7
8 1 6

2 9 4
7 5 3
6 1 8

8 3 4
1 5 9
6 7 2

4 3 8
9 5 1
2 7 6

6 7 2
1 5 9
8 3 4

2 7 6
9 5 1
4 3 8

我们创建一个三维数组来存储这 8 个矩阵。现在，我们检查这 8 个矩阵中每一个的输入矩阵，找出变化次数最少**的矩阵。**

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

// This program takes in two 2D arrays as
// input and compares them to find out the
// minimum number of changes that needs to
// be made to convert arr to ms.
int findMinimumFromMS(int arr[][3], int ms[][3])
{
    int count = 0;

    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            if (arr[i][j] != ms[i][j])
                count++;
        }
    }
    return count;
}

int findMinimum(int arr[][3])
{
    int ms[][3][3] = {
        { { 8, 1, 6 }, { 3, 5, 7 }, { 4, 9, 2 } },
        { { 6, 1, 8 }, { 7, 5, 3 }, { 2, 9, 4 } },
        { { 4, 9, 2 }, { 3, 5, 7 }, { 8, 1, 6 } },
        { { 2, 9, 4 }, { 7, 5, 3 }, { 6, 1, 8 } },
        { { 8, 3, 4 }, { 1, 5, 9 }, { 6, 7, 2 } },
        { { 4, 3, 8 }, { 9, 5, 1 }, { 2, 7, 6 } },
        { { 6, 7, 2 }, { 1, 5, 9 }, { 8, 3, 4 } },
        { { 2, 7, 6 }, { 9, 5, 1 }, { 4, 3, 8 } }, };

    // If all the elements need to be changed,
    // there would be 9 changes, so we take the
    // max as 9
    int min = 9;

    for(int i = 0; i < 8; i++)
    {
        int x = findMinimumFromMS(arr, ms[i]);
        if (x < min)
            min = x;
    }
    return min;
}

// Driver code   
int main()
{
    int arr[][3] = { { 8, 5, 6 },
                     { 3, 8, 7 }, 
                     { 4, 9, 2 } };

    cout << findMinimum(arr) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
class GfG {

    // this program takes in two 2D arrays as
    // input and compares them to find out the
    // minimum number of changes that needs to
    // be made to convert arr to ms.
    public static int findMinimumFromMS(int[][] arr,
                                        int[][] ms)
    {
        int count = 0;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (arr[i][j] != ms[i][j])
                    count++;
            }
        }
        return count;
    }

    public static int findMinimum(int[][] arr)
    {
        int[][][] ms = {
            { { 8, 1, 6 }, { 3, 5, 7 }, { 4, 9, 2 } },
            { { 6, 1, 8 }, { 7, 5, 3 }, { 2, 9, 4 } },
            { { 4, 9, 2 }, { 3, 5, 7 }, { 8, 1, 6 } },
            { { 2, 9, 4 }, { 7, 5, 3 }, { 6, 1, 8 } },
            { { 8, 3, 4 }, { 1, 5, 9 }, { 6, 7, 2 } },
            { { 4, 3, 8 }, { 9, 5, 1 }, { 2, 7, 6 } },
            { { 6, 7, 2 }, { 1, 5, 9 }, { 8, 3, 4 } },
            { { 2, 7, 6 }, { 9, 5, 1 }, { 4, 3, 8 } },
        };

        // If all the elements need to be changed,
        // there would be 9 changes, so we take the
        // max as 9
        int min = 9;
        for (int i = 0; i < 8; i++) {
            int x = findMinimumFromMS(arr, ms[i]);
            if (x < min)
                min = x;
        }
        return min;
    }

    public static void main(String[] args)
    {
        int[][] arr = { { 8, 5, 6 }, { 3, 8, 7 },
                                     { 4, 9, 2 } };
        System.out.println(findMinimum(arr));
    }
}
```

## **蟒蛇 3**

```
# This program takes in two 2D arrays as
# input and compares them to find out the
# minimum number of changes that needs to
# be made to convert arr to ms.
def findMinimumFromMS(arr, ms):

    count = 0
    for i in range(0, 3):
        for j in range(0, 3):
            if arr[i][j] != ms[i][j]:
                count += 1

    return count

def findMinimum(arr):

    ms = [
            [ [ 8, 1, 6 ], [ 3, 5, 7 ], [ 4, 9, 2 ] ],
            [ [ 6, 1, 8 ], [ 7, 5, 3 ], [ 2, 9, 4 ] ],
            [ [ 4, 9, 2 ], [ 3, 5, 7 ], [ 8, 1, 6 ] ],
            [ [ 2, 9, 4 ], [ 7, 5, 3 ], [ 6, 1, 8 ] ],
            [ [ 8, 3, 4 ], [ 1, 5, 9 ], [ 6, 7, 2 ] ],
            [ [ 4, 3, 8 ], [ 9, 5, 1 ], [ 2, 7, 6 ] ],
            [ [ 6, 7, 2 ], [ 1, 5, 9 ], [ 8, 3, 4 ] ],
            [ [ 2, 7, 6 ], [ 9, 5, 1 ], [ 4, 3, 8 ] ],
        ]

    # If all the elements need to be changed, there
    # would be 9 changes, so we take the max as 9
    Min = 9
    for i in range(0, 8):
        x = findMinimumFromMS(arr, ms[i])
        if x < Min:
            Min = x

    return Min

if __name__ == "__main__":

    arr = [ [ 8, 5, 6 ], [ 3, 8, 7 ], [ 4, 9, 2 ] ]
    print(findMinimum(arr))

# This code is contributed by Rituraj Jain
```

## **C#**

```
using System;

class GFG{

// This program takes in two 2D arrays as
// input and compares them to find out the
// minimum number of changes that needs to
// be made to convert arr to ms.
static int findMinimumFromMS(int[,] arr, int[,,] ms,
                             int row)
{
    int count = 0;
    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            if (arr[i, j] != ms[row, i, j])
            {
                count++;
            }
        }
    }
    return count;
}

static int findMinimum(int[,] arr)
{
    int[,,] ms = {
        { { 8, 1, 6 }, { 3, 5, 7 }, { 4, 9, 2 } },
        { { 6, 1, 8 }, { 7, 5, 3 }, { 2, 9, 4 } },
        { { 4, 9, 2 }, { 3, 5, 7 }, { 8, 1, 6 } },
        { { 2, 9, 4 }, { 7, 5, 3 }, { 6, 1, 8 } },
        { { 8, 3, 4 }, { 1, 5, 9 }, { 6, 7, 2 } },
        { { 4, 3, 8 }, { 9, 5, 1 }, { 2, 7, 6 } },
        { { 6, 7, 2 }, { 1, 5, 9 }, { 8, 3, 4 } },
        { { 2, 7, 6 }, { 9, 5, 1 }, { 4, 3, 8 } },
    };

    // If all the elements need to be changed,
    // there would be 9 changes, so we take the
    // max as 9
    int min = 9;

    for(int i = 0; i < 8; i++)
    {
        int x = findMinimumFromMS(arr, ms, i);

        if (x < min)
        {
            min = x;
        }
    }
    return min;
}

// Driver Code
static public void Main()
{
    int[,] arr = { { 8, 5, 6 },
                   { 3, 8, 7 },
                   { 4, 9, 2 } };

    Console.WriteLine(findMinimum(arr));
}
}

// This code is contributed by avanitrachhadiya2155
```

## **java 描述语言**

```
<script>
// this program takes in two 2D arrays as
// input and compares them to find out the
// minimum number of changes that needs to
// be made to convert arr to ms.

function findMinimumFromMS(arr,ms)
{
    let count = 0;
        for (let i = 0; i < 3; i++) {
            for (let j = 0; j < 3; j++) {
                if (arr[i][j] != ms[i][j])
                    count++;
            }
        }
        return count;
}

function findMinimum(arr)
{

let ms = [
            [ [ 8, 1, 6 ], [ 3, 5, 7 ], [ 4, 9, 2 ] ],
            [ [ 6, 1, 8 ], [ 7, 5, 3 ], [ 2, 9, 4 ] ],
            [ [ 4, 9, 2 ], [ 3, 5, 7 ], [ 8, 1, 6 ] ],
            [ [ 2, 9, 4 ], [ 7, 5, 3 ], [ 6, 1, 8 ] ],
            [ [ 8, 3, 4 ], [ 1, 5, 9 ], [ 6, 7, 2 ] ],
            [ [ 4, 3, 8 ], [ 9, 5, 1 ], [ 2, 7, 6 ] ],
            [ [ 6, 7, 2 ], [ 1, 5, 9 ], [ 8, 3, 4 ] ],
            [ [ 2, 7, 6 ], [ 9, 5, 1 ], [ 4, 3, 8 ] ],
        ];
        // If all the elements need to be changed,
        // there would be 9 changes, so we take the
        // max as 9
        let min = 9;
        for (let i = 0; i < 8; i++) {
            let x = findMinimumFromMS(arr, ms[i]);
            if (x < min)
                min = x;
        }
        return min;
}

let arr=[[ 8, 5, 6 ], [ 3, 8, 7 ],[ 4, 9, 2 ] ];
document.write(findMinimum(arr));

// This code is contributed by ab2127
</script>
```

****Output:** 

```
2
```**