# 统计列和大于行和的对的数量

> 原文:[https://www . geesforgeks . org/count-列和大于行和的对数/](https://www.geeksforgeeks.org/count-the-number-of-pairs-that-have-column-sum-greater-than-row-sum/)

给定一个大小为 **NxN** 的矩阵。任务是计算指数对(I，j)的数量，使得第 **j 列的总和大于第 **i 行的总和。
**举例:****** 

```
Input : N = 2, mat[][] = {{1, 2},
                          {3, 4}}
Output : 2
The 2 valid pairs are (1, 1) and (1, 2).

Input : N = 3, mat[][] = { { 1, 2, 3 }, 
                       { 4, 5, 6 },
                       { 7, 8, 9 } }; 
Output : 4
```

**方法:**
想法是分别预先计算每行和每列的行和与列和，然后计算可能的有效对(I，j)的数量，使得第 j 列的列和大于第 I 行的行和。
以下是上述办法的实施:

## C++

```
// C++ program to count the number of pairs
// (i,j) such that sum of elements in j-th column
// is greater than sum of elements in i-th row

#include <bits/stdc++.h>
using namespace std;
#define N 3

// Function to count the number of pairs
// (i,j) such that sum of elements in j-th column
// is greater than sum of elements in i-th row
int countPairs(int a[N][N])
{
    // Initialize row sum and column
    // sum to zero
    int sumr[N] = { 0 }, sumc[N] = { 0 };

    // Calculate row sum and column sum
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++) {
            sumr[i] += a[i][j];
            sumc[j] += a[i][j];
        }

    int count = 0;

    // Count the number of pairs that are valid
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            if (sumc[i] > sumr[j])
                count++;

    return count;
}

// Driver Code
int main()
{
    int a[][N] = { { 1, 2, 3 },
                   { 4, 5, 6 },
                   { 7, 8, 9 } };

    cout << countPairs(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of pairs
// (i,j) such that sum of elements in j-th column
// is greater than sum of elements in i-th row
import java.io.*;

class GFG
{

static int N = 3;

// Function to count the number of pairs
// (i,j) such that sum of elements in j-th column
// is greater than sum of elements in i-th row
static int countPairs(int a[][])
{
    // Initialize row sum and column
    // sum to zero
    int sumr[] = new int[N] ;
    int sumc[] = new int [N] ;

    // Calculate row sum and column sum
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
        {
            sumr[i] += a[i][j];
            sumc[j] += a[i][j];
        }

    int count = 0;

    // Count the number of pairs that are valid
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            if (sumc[i] > sumr[j])
                count++;

    return count;
}

    // Driver Code
    public static void main (String[] args)
    {

    int a[][] = { { 1, 2, 3 },
                { 4, 5, 6 },
                { 7, 8, 9 } };

    System.out.println (countPairs(a));
    }
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python 3 program to count the number of pairs
# (i,j) such that sum of elements in j-th column
# is greater than sum of elements in i-th row

N = 3

# Function to count the number of pairs
# (i,j) such that sum of elements in j-th column
# is greater than sum of elements in i-th row
def countPairs(a):

    # Initialize row sum and column
    # sum to zero
    sumr = [0 for i in range(N)]
    sumc = [0 for i in range(N)]

    # Calculate row sum and column sum
    for i in range(N):
        for j in range(N):
            sumr[i] += a[i][j]
            sumc[j] += a[i][j]

    count = 0

    # Count the number of pairs that are valid
    for i in range(N):
        for j in range(N):
            if (sumc[i] > sumr[j]):
                count += 1

    return count

# Driver Code
if __name__ == '__main__':
    a = [[1, 2, 3],[4, 5, 6], [7, 8, 9]]

    print(countPairs(a))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count the number of pairs
// (i,j) such that sum of elements in j-th column
// is greater than sum of elements in i-th row
using System;

class GFG
{

static int N = 3;

// Function to count the number
// of pairs (i,j) such that sum
// of elements in j-th column is
// greater than sum of elements in i-th row
static int countPairs(int [,]a)
{
    // Initialize row sum and column
    // sum to zero
    int []sumr = new int[N] ;
    int []sumc = new int [N] ;

    // Calculate row sum and column sum
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
        {
            sumr[i] += a[i, j];
            sumc[j] += a[i, j];
        }

    int count = 0;

    // Count the number of pairs that are valid
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            if (sumc[i] > sumr[j])
                count++;

    return count;
}

// Driver Code
public static void Main()
{

    int [,]a = { { 1, 2, 3 },
                { 4, 5, 6 },
                { 7, 8, 9 } };

    Console.WriteLine(countPairs(a));
}
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

    // Javascript program to count the number of pairs
    // (i,j) such that sum of elements in j-th column
    // is greater than sum of elements in i-th row

    let N = 3;

    // Function to count the number of pairs
    // (i,j) such that sum of elements in j-th column
    // is greater than sum of elements in i-th row
    function countPairs(a)
    {
        // Initialize row sum and column
        // sum to zero
        let sumr = new Array(N);
        sumr.fill(0);
        let sumc = new Array(N);
        sumc.fill(0);

        // Calculate row sum and column sum
        for (let i = 0; i < N; i++)
            for (let j = 0; j < N; j++)
            {
                sumr[i] += a[i][j];
                sumc[j] += a[i][j];
            }

        let count = 0;

        // Count the number of pairs that are valid
        for (let i = 0; i < N; i++)
            for (let j = 0; j < N; j++)
                if (sumc[i] > sumr[j])
                    count++;

        return count;
    }

    let a = [ [ 1, 2, 3 ],
               [ 4, 5, 6 ],
               [ 7, 8, 9 ] ];

    document.write(countPairs(a));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N <sup>2</sup> )