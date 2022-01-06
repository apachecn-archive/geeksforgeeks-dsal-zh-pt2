# 将给定矩阵转换为对角占优矩阵的最小步数

> 原文:[https://www . geesforgeks . org/将给定矩阵转换为对角占优矩阵的最小步骤数/](https://www.geeksforgeeks.org/minimum-number-of-steps-to-convert-a-given-matrix-into-diagonally-dominant-matrix/)

给定一个有序的矩阵 **NxN** ，任务是找到将给定矩阵转换成[对角占优矩阵](https://www.geeksforgeeks.org/diagonally-dominant-matrix/)的最小步数。在每个步骤中，唯一允许的操作是将任何元素减少或增加 1。
**例:**

> **输入:** mat[][] = {{3，2，4}，{1，4，4}，{2，3，4}}
> **输出:** 5
> 第 1 行元素绝对值之和除了
> 对角线元素比 abs 多 3(arr[0][0])。
> 第二排比 abs(arr[1][1])多 1 个
> 第三排比 abs(arr[2][2])多 1 个。
> 因此，3 + 1 + 1 = 5
> **输入:** mat[][] = {{1，2，4，0}，{1，3，4，2}，{3，3，4，2}，{-1，0，1，4}}
> **输出:** 13

**进场:**

*   如果对于矩阵的每一行，一行中对角线条目的大小大于或等于该行中所有其他(非对角线)条目的大小之和，则称正方形矩阵为对角占优矩阵。
*   将给定矩阵转换成对角占优矩阵所需的最小步数可以根据两种情况来计算:
    1.  如果一行中除对角线元素之外的所有元素的绝对值之和**大于对角线元素的绝对值**，那么这两个值之间的差值将被加到结果中。
    2.  否则不需要在结果中添加任何东西，因为在这种情况下，行满足对角占优矩阵的条件。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 3

// Function to return the minimum steps
// required to convert the given matrix
// to a Diagonally Dominant Matrix
int findStepsForDDM(int arr[][N])
{
    int result = 0;

    // For each row
    for (int i = 0; i < N; i++) {

        // To store the sum of the current row
        int sum = 0;
        for (int j = 0; j < N; j++)
            sum += abs(arr[i][j]);

        // Remove the element of the current row
        // which lies on the main diagonal
        sum -= abs(arr[i][i]);

        // Checking if the diagonal element is less
        // than the sum of non-diagonal element
        // then add their difference to the result
        if (abs(arr[i][i]) < abs(sum))
            result += abs(abs(arr[i][i]) - abs(sum));
    }

    return result;
}

// Driven code
int main()
{
    int arr[N][N] = { { 3, -2, 1 },
                      { 1, -3, 2 },
                      { -1, 2, 4 } };

    cout << findStepsForDDM(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    final static int N = 3 ;

    // Function to return the minimum steps
    // required to convert the given matrix
    // to a Diagonally Dominant Matrix
    static int findStepsForDDM(int arr[][])
    {
        int result = 0;

        // For each row
        for (int i = 0; i < N; i++)
        {

            // To store the sum of the current row
            int sum = 0;
            for (int j = 0; j < N; j++)
                sum += Math.abs(arr[i][j]);

            // Remove the element of the current row
            // which lies on the main diagonal
            sum -= Math.abs(arr[i][i]);

            // Checking if the diagonal element is less
            // than the sum of non-diagonal element
            // then add their difference to the result
            if (Math.abs(arr[i][i]) < Math.abs(sum))
                result += Math.abs(Math.abs(arr[i][i]) - Math.abs(sum));
        }

        return result;
    }

    // Driven code
    public static void main (String[] args)
    {

        int arr[][] = { { 3, -2, 1 },
                        { 1, -3, 2 },
                        { -1, 2, 4 } };

        System.out.println(findStepsForDDM(arr));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

N = 3

# Function to return the minimum steps
# required to convert the given matrix
# to a Diagonally Dominant Matrix
def findStepsForDDM(arr):

    result = 0

    # For each row
    for i in range(N):

        # To store the sum of the current row
        sum = 0
        for j in range(N):
            sum += abs(arr[i][j])

        # Remove the element of the current row
        # which lies on the main diagonal
        sum -= abs(arr[i][i])

        # Checking if the diagonal element is less
        # than the sum of non-diagonal element
        # then add their difference to the result
        if (abs(arr[i][i]) < abs(sum)):
            result += abs(abs(arr[i][i]) - abs(sum))

    return result

# Driver code

arr= [ [ 3, -2, 1 ],
    [ 1, -3, 2 ],
    [ -1, 2, 4 ] ]

print(findStepsForDDM(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int N = 3 ;

    // Function to return the minimum steps
    // required to convert the given matrix
    // to a Diagonally Dominant Matrix
    static int findStepsForDDM(int [,]arr)
    {
        int result = 0;

        // For each row
        for (int i = 0; i < N; i++)
        {

            // To store the sum of the current row
            int sum = 0;
            for (int j = 0; j < N; j++)
                sum += Math.Abs(arr[i,j]);

            // Remove the element of the current row
            // which lies on the main diagonal
            sum -= Math.Abs(arr[i,i]);

            // Checking if the diagonal element is less
            // than the sum of non-diagonal element
            // then add their difference to the result
            if (Math.Abs(arr[i,i]) < Math.Abs(sum))
                result += Math.Abs(Math.Abs(arr[i,i]) - Math.Abs(sum));
        }

        return result;
    }

    // Driven code
    static public void Main ()
    {

        int [,]arr = { { 3, -2, 1 },
                        { 1, -3, 2 },
                        { -1, 2, 4 } };

        Console.WriteLine(findStepsForDDM(arr));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
// Java script implementation of the approach
let N = 3 ;

    // Function to return the minimum steps
    // required to convert the given matrix
    // to a Diagonally Dominant Matrix
    function findStepsForDDM(arr)
    {
        let result = 0;

        // For each row
        for (let i = 0; i < N; i++)
        {

            // To store the sum of the current row
            let sum = 0;
            for (let j = 0; j < N; j++)
                sum += Math.abs(arr[i][j]);

            // Remove the element of the current row
            // which lies on the main diagonal
            sum -= Math.abs(arr[i][i]);

            // Checking if the diagonal element is less
            // than the sum of non-diagonal element
            // then add their difference to the result
            if (Math.abs(arr[i][i]) < Math.abs(sum))
                result += Math.abs(Math.abs(arr[i][i]) - Math.abs(sum));
        }

        return result;
    }

    // Driven code
        let arr = [[ 3, -2, 1 ],
                        [ 1, -3, 2 ],
                        [ -1, 2, 4 ]];

        document.write(findStepsForDDM(arr));

// This code is contributed by mohan pavan

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(N <sup>2</sup> )