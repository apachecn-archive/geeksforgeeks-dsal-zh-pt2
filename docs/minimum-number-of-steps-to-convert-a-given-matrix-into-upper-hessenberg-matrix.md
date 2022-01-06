# 将给定矩阵转换为上赫森伯格矩阵的最小步数

> 原文:[https://www . geeksforgeeks . org/将给定矩阵转换为上赫森伯格矩阵的最小步骤数/](https://www.geeksforgeeks.org/minimum-number-of-steps-to-convert-a-given-matrix-into-upper-hessenberg-matrix/)

给定一个有序矩阵 **NxN** ，找到将给定矩阵转换成[上赫森伯格矩阵](https://www.geeksforgeeks.org/print-upper-hessenberg-matrix-of-order-n/)的最小步数。在每个步骤中，唯一允许的操作是将任何元素值减少或增加 1。
**例:**

> **输入:**N = 3
> 1 2 8
> 1 3 4
> 2 3 4
> T6】输出: 2
> 减少元素 a[2][0] 2 次。
> 现在矩阵是上赫森伯格
> **输入:**N = 4
> 1 2 2 3
> 1 3 4 2
> 3 3 4 2
> -1 0 1 4
> **输出:** 4

**进场:**

*   一个矩阵要成为上赫森伯格矩阵，它在次对角线以下的所有元素都必须等于零，即对于所有 i > j+1，A <sub>ij</sub> = 0。。
*   转换上赫森伯格矩阵中给定矩阵所需的最小步数等于所有 i > j + 1 的所有 A <sub>ij</sub> 的**绝对值之和。**
*   考虑了元件的模数值，因为元件数量的增加和减少都是一个步骤。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#define N 4
using namespace std;

// Function to count steps in
// conversion of matrix into upper
// Hessenberg matrix
int stepsRequired(int arr[][N])
{
    int result = 0;
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // if element is below sub-diagonal
            // add abs(element) into result
            if (i > j + 1)
                result += abs(arr[i][j]);
        }
    }
    return result;
}

// Driver code
int main()
{
    int arr[N][N] = { 1, 2, 3, 4,
                      3, 1, 0, 3,
                      3, 2, 1, 3,
                     -3, 4, 2, 1 };

    // Function call
    cout << stepsRequired(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

    static int N = 4;

    // Function to count steps in
    // conversion of matrix into upper
    // Hessenberg matrix
    static int stepsRequired(int arr[][])
    {
        int result = 0;
        for (int i = 0; i < N; i++)
        {

            for (int j = 0; j < N; j++)
            {

                // if element is below sub-diagonal
                // add abs(element) into result
                if (i > j + 1)
                    result += Math.abs(arr[i][j]);
            }
        }
        return result;
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr [][] = new int [][] {{1, 2, 3, 4},
                        {3, 1, 0, 3},
                        {3, 2, 1, 3},
                        {-3, 4, 2, 1 }};

        // Function call
        System.out.println(stepsRequired(arr));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above approach
N = 4;

# Function to count steps in
# conversion of matrix into upper
# Hessenberg matrix
def stepsRequired(arr):
    result = 0;
    for i in range(N):

        for j in range(N):

            # if element is below sub-diagonal
            # add abs(element) into result
            if (i > j + 1):
                result += abs(arr[i][j]);

    return result;

# Driver code
arr =   [[1, 2, 3, 4],
         [3, 1, 0, 3],
         [3, 2, 1, 3],
         [-3, 4, 2, 1]];

# Function call
print(stepsRequired(arr));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    static int N = 4;

    // Function to count steps in
    // conversion of matrix into upper
    // Hessenberg matrix
    static int stepsRequired(int [, ] arr)
    {
        int result = 0;
        for (int i = 0; i < N; i++)
        {

            for (int j = 0; j < N; j++)
            {

                // if element is below sub-diagonal
                // add abs(element) into result
                if (i > j + 1)
                    result += Math.Abs(arr[i, j]);
            }
        }
        return result;
    }

    // Driver code
    public static void Main ()
    {

        int [ , ] arr = new int [, ] { {1, 2, 3, 4},
                        {3, 1, 0, 3},
                        {3, 2, 1, 3},
                        {-3, 4, 2, 1}};

        // Function call
        Console.WriteLine(stepsRequired(arr));

    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
// Java script implementation of above approach
let N = 4;

    // Function to count steps in
    // conversion of matrix into upper
    // Hessenberg matrix
    function stepsRequired(arr)
    {
        let result = 0;
        for (let i = 0; i < N; i++)
        {

            for (let j = 0; j < N; j++)
            {

                // if element is below sub-diagonal
                // add abs(element) into result
                if (i > j + 1)
                    result += Math.abs(arr[i][j]);
            }
        }
        return result;
    }

    // Driver code   
        let arr =[[1, 2, 3, 4],
                        [3, 1, 0, 3],
                        [3, 2, 1, 3],
                        [-3, 4, 2, 1 ]];

        // Function call
        document.write(stepsRequired(arr));

// This code is contributed by mohan pavan

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N*N)