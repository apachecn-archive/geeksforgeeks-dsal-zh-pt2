# 在矩阵中找到最大和的列

> 原文:[https://www . geeksforgeeks . org/find-带矩阵最大和的列/](https://www.geeksforgeeks.org/find-column-with-maximum-sum-in-a-matrix/)

给定一个 N*N 矩阵。任务是找到和最大的列的索引。这是元素总和最大的列。
**例** :

```
Input : mat[][] = {
        { 1, 2, 3, 4, 5 },
        { 5, 3, 1, 4, 2 },
        { 5, 6, 7, 8, 9 },
        { 0, 6, 3, 4, 12 },
        { 9, 7, 12, 4, 3 },
    };
Output : Column 5 has max sum 31

Input : mat[][] = {
        { 1, 2, 3 },
        { 4, 2, 1 },
        { 5, 6, 7 },
    };
Output : Column 3 has max sum 11
```

思路是[逐列遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)找到每一列的元素之和，检查每一列当前之和是否大于直到当前列得到的最大和，并相应更新 maximum_sum。
以下是上述办法的实施情况:

## C++

```
// C++ program to find column with
// max sum in a matrix
#include <bits/stdc++.h>
using namespace std;

#define N 5 // No of rows and column

// Function to find the column with max sum
pair<int, int> colMaxSum(int mat[N][N])
{
    // Variable to store index of column
    // with maximum
    int idx = -1;

    // Variable to store max sum
    int maxSum = INT_MIN;

    // Traverse matrix column wise
    for (int i = 0; i < N; i++) {
        int sum = 0;

        // calculate sum of column
        for (int j = 0; j < N; j++) {
            sum += mat[j][i];
        }

        // Update maxSum if it is less than
        // current sum
        if (sum > maxSum) {
            maxSum = sum;

            // store index
            idx = i;
        }
    }

    pair<int, int> res;

    res = make_pair(idx, maxSum);

    // return result
    return res;
}

// driver code
int main()
{

    int mat[N][N] = {
        { 1, 2, 3, 4, 5 },
        { 5, 3, 1, 4, 2 },
        { 5, 6, 7, 8, 9 },
        { 0, 6, 3, 4, 12 },
        { 9, 7, 12, 4, 3 },
    };

    pair<int, int> ans = colMaxSum(mat);

    cout << "Column " << ans.first + 1 << " has max sum "
         << ans.second;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find column
// with max sum in a matrix
import java.util.*;

class GFG
{
// No of rows and column
static final int N = 5;

// structure for pair
static class Pair
{
    int first , second;

    Pair(int f, int s)
    {
        first = f;
        second = s;
    }
}

// Function to find the column
// with max sum
static Pair colMaxSum(int mat[][])
{
    // Variable to store index of
    // column with maximum
    int idx = -1;

    // Variable to store max sum
    int maxSum = Integer.MIN_VALUE;

    // Traverse matrix column wise
    for (int i = 0; i < N; i++)
    {
        int sum = 0;

        // calculate sum of column
        for (int j = 0; j < N; j++)
        {
            sum += mat[j][i];
        }

        // Update maxSum if it is
        // less than current sum
        if (sum > maxSum)
        {
            maxSum = sum;

            // store index
            idx = i;
        }
    }

    Pair res;

    res = new Pair(idx, maxSum);

    // return result
    return res;
}

// Driver code
public static void main(String args[])
{
    int mat[][] = { { 1, 2, 3, 4, 5 },
                    { 5, 3, 1, 4, 2 },
                    { 5, 6, 7, 8, 9 },
                    { 0, 6, 3, 4, 12 },
                    { 9, 7, 12, 4, 3 }};

    Pair ans = colMaxSum(mat);

    System.out.println("Column " + (int)(ans.first + 1) +
                           " has max sum " + ans.second);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find column with
# max Sum in a matrix

N = 5

# Function to find the column with max Sum
def colMaxSum(mat):

    # Variable to store index of column
    # with maximum
    idx = -1

    # Variable to store max Sum
    maxSum = -10**9

    # Traverse matrix column wise
    for i in range(N):

        Sum = 0

        # calculate Sum of column
        for j in range(N):
            Sum += mat[j][i]

        # Update maxSum if it is less
        # than current Sum
        if (Sum > maxSum):
            maxSum = Sum

            # store index
            idx = i

    # return result
    return idx, maxSum

# Driver Code

mat = [[ 1, 2, 3, 4, 5 ],
       [ 5, 3, 1, 4, 2 ],
       [ 5, 6, 7, 8, 9 ],
       [ 0, 6, 3, 4, 12 ],
       [ 9, 7, 12, 4, 3 ]]

ans, ans0 = colMaxSum(mat)

print("Column", ans + 1,   
      "has max Sum", ans0)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to find column
// with max sum in a matrix
using System;

class GFG
{

// No of rows and column
static readonly int N = 5;

// structure for pair
public class Pair
{
    public int first , second;

    public Pair(int f, int s)
    {
        first = f;
        second = s;
    }
}

// Function to find the column
// with max sum
static Pair colMaxSum(int [,]mat)
{
    // Variable to store index of
    // column with maximum
    int idx = -1;

    // Variable to store max sum
    int maxSum = int.MinValue;

    // Traverse matrix column wise
    for (int i = 0; i < N; i++)
    {
        int sum = 0;

        // calculate sum of column
        for (int j = 0; j < N; j++)
        {
            sum += mat[j, i];
        }

        // Update maxSum if it is
        // less than current sum
        if (sum > maxSum)
        {
            maxSum = sum;

            // store index
            idx = i;
        }
    }

    Pair res;

    res = new Pair(idx, maxSum);

    // return result
    return res;
}

// Driver code
public static void Main(String []args)
{
    int [,]mat = { { 1, 2, 3, 4, 5 },
                    { 5, 3, 1, 4, 2 },
                    { 5, 6, 7, 8, 9 },
                    { 0, 6, 3, 4, 12 },
                    { 9, 7, 12, 4, 3 }};

    Pair ans = colMaxSum(mat);

    Console.WriteLine("Column " + (int)(ans.first + 1) +
                        " has max sum " + ans.second);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find column
// with max sum in a matrix

// No of rows and column
let N = 5;

// Function to find the column
// with max sum
function colMaxSum(mat)
{
    // Variable to store index of
    // column with maximum
    let idx = -1;

    // Variable to store max sum
    let maxSum = Number.MIN_VALUE;

    // Traverse matrix column wise
    for (let i = 0; i < N; i++)
    {
        let sum = 0;

        // calculate sum of column
        for (let j = 0; j < N; j++)
        {
            sum += mat[j][i];
        }

        // Update maxSum if it is
        // less than current sum
        if (sum > maxSum)
        {
            maxSum = sum;

            // store index
            idx = i;
        }
    }

    let res;

    res = [idx, maxSum];

    // return result
    return res;
}

// Driver code
let mat = [[ 1, 2, 3, 4, 5 ],
       [ 5, 3, 1, 4, 2 ],
       [ 5, 6, 7, 8, 9 ],
       [ 0, 6, 3, 4, 12 ],
       [ 9, 7, 12, 4, 3 ]];

let ans = colMaxSum(mat);
document.write("Column " + (ans[0] + 1) +
                           " has max sum " + ans[1]);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Column 5 has max sum 31
```