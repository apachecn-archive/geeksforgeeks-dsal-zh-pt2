# 从给定的三个数组中选择元素后最小化总和

> 原文:[https://www . geeksforgeeks . org/从给定的三个数组中选择元素后最小化总和/](https://www.geeksforgeeks.org/minimize-the-sum-after-choosing-elements-from-the-given-three-arrays/)

给定相同大小 N 的三个数组**A【】**、**B【】**和**C【】**,任务是在从这些数组中选择 N 个元素之后最小化总和，使得在每个索引处 **i** 可以从数组**A【I】**、**B【I】**或**C【I】**中的任何一个中选择一个元素，并且不能从同一数组中选择两个连续的元素。
**举例:**

> **输入:** A[] = {1，100，1}，B[] = {100，100，100}，C[] = {100，100， 100 }
> T3】输出:102
> A[0]+B[1]+A[2]= 1+100+100 = 201
> A[0]+B[1]+C[2]= 1+100+100 = 201
> A[0]+C[1]+B[2]= 1+100+100 = 201
> T9】A[0]+C[1] +A[1]+C[2]= 100+100+100 = 300
> B[0]+C[1]+A[2]= 100+100+1 = 201
> B[0]+C[1]+B[2]= 100+100+100 = 300
> C[0]+A[1]+B[2]= 100+100+100 = 300 = 100+100+1 = 201
> C[0]+B[1]+C[2]= 100+100+100 = 300
> **输入:** A[] = {1，1，1}，B[] = {1，1，1}，C[] = {1，1，1}
> **输出:** 3

**方法:**问题是寻找最小成本的一个简单变型。额外的限制是，如果我们从一个特定的数组中取出一个元素，那么我们就不能从同一个数组中取出下一个元素。使用递归可以很容易地解决这个问题，但是它会给时间带来复杂性，就像 **O(3^n)** 一样，因为对于每个元素，我们有三个数组作为选择。
为了提高时间复杂度，我们可以轻松地将预先计算的值存储在 dp 数组中。
由于在每个索引处有三个数组可供选择，因此在这种情况下会出现三种情况:

*   **情况 1:** 如果从第 I 个元素中选择了数组 A[]，那么对于第(i + 1)个元素，我们要么选择数组 B[]，要么选择数组 C[]。
*   **情况 2:** 如果从第 I 个元素中选择了数组 B[]，那么对于第(i + 1)个元素，我们要么选择数组 A[]，要么选择数组 C[]。
*   **情况 3:** 如果从第 I 个元素中选择了数组 C[]，那么我们要么为第(i + 1)个元素选择数组 A[]，要么选择数组 B[]。

上述状态可以使用递归来解决，并且中间结果可以存储在 dp 数组中。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;
#define SIZE 3
const int N = 3;

// Function to return the minimized sum
int minSum(int A[], int B[], int C[], int i,
        int n, int curr, int dp[SIZE][N])
{

    // If all the indices have been used
    if (n <= 0)
        return 0;

    // If this value is pre-calculated
    // then return its value from dp array
    // instead of re-computing it
    if (dp[n][curr] != -1)
        return dp[n][curr];

    // Here curr is the array chosen
    // for the (i - 1)th element
    // 0 for A[], 1 for B[] and 2 for C[]

    // If A[i - 1] was chosen previously then
    // only B[i] or C[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    if (curr == 0) {
        return dp[n][curr]
                = min(B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp),
                      C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));
    }

    // If B[i - 1] was chosen previously then
    // only A[i] or C[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    if (curr == 1)
        return dp[n][curr]
                = min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                      C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));

    // If C[i - 1] was chosen previously then
    // only A[i] or B[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    return dp[n][curr]
                = min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                      B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp));
}

// Driver code
int main()
{
    int A[] = { 1, 50, 1 };
    int B[] = { 50, 50, 50 };
    int C[] = { 50, 50, 50 };

    // Initialize the dp[][] array
    int dp[SIZE][N];
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < N; j++)
            dp[i][j] = -1;

    // min(start with A[0], start with B[0], start with C[0])
    cout << min(A[0] + minSum(A, B, C, 1, SIZE - 1, 0, dp),
                min(B[0] + minSum(A, B, C, 1, SIZE - 1, 1, dp),
                    C[0] + minSum(A, B, C, 1, SIZE - 1, 2, dp)));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

static int SIZE = 3;
static int N = 3;

// Function to return the minimized sum
static int minSum(int A[], int B[], int C[], int i,
                    int n, int curr, int [][]dp)
{

    // If all the indices have been used
    if (n <= 0)
        return 0;

    // If this value is pre-calculated
    // then return its value from dp array
    // instead of re-computing it
    if (dp[n][curr] != -1)
        return dp[n][curr];

    // Here curr is the array chosen
    // for the (i - 1)th element
    // 0 for A[], 1 for B[] and 2 for C[]

    // If A[i - 1] was chosen previously then
    // only B[i] or C[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    if (curr == 0)
    {
        return dp[n][curr]
                = Math.min(B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp),
                    C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));
    }

    // If B[i - 1] was chosen previously then
    // only A[i] or C[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    if (curr == 1)
        return dp[n][curr]
                = Math.min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                    C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));

    // If C[i - 1] was chosen previously then
    // only A[i] or B[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    return dp[n][curr]
                = Math.min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                    B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp));
}

// Driver code
public static void main (String[] args)
{
    int A[] = { 1, 50, 1 };
    int B[] = { 50, 50, 50 };
    int C[] = { 50, 50, 50 };

    // Initialize the dp[][] array
    int dp[][] = new int[SIZE][N];
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < N; j++)
            dp[i][j] = -1;

    // min(start with A[0], start with B[0], start with C[0])
    System.out.println(Math.min(A[0] + minSum(A, B, C, 1, SIZE - 1, 0, dp),
                Math.min(B[0] + minSum(A, B, C, 1, SIZE - 1, 1, dp),
                    C[0] + minSum(A, B, C, 1, SIZE - 1, 2, dp))));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

import numpy as np

SIZE = 3;
N = 3;

# Function to return the minimized sum
def minSum(A, B, C, i, n, curr, dp) :

    # If all the indices have been used
    if (n <= 0) :
        return 0;

    # If this value is pre-calculated
    # then return its value from dp array
    # instead of re-computing it
    if (dp[n][curr] != -1) :
        return dp[n][curr];

    # Here curr is the array chosen
    # for the (i - 1)th element
    # 0 for A[], 1 for B[] and 2 for C[]

    # If A[i - 1] was chosen previously then
    # only B[i] or C[i] can chosen now
    # choose the one which leads
    # to the minimum sum
    if (curr == 0) :
        dp[n][curr] = min( B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp),
        C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));
        return dp[n][curr]

    # If B[i - 1] was chosen previously then
    # only A[i] or C[i] can chosen now
    # choose the one which leads
    # to the minimum sum
    if (curr == 1) :
        dp[n][curr] = min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
        C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));
        return dp[n][curr]

    # If C[i - 1] was chosen previously then
    # only A[i] or B[i] can chosen now
    # choose the one which leads
    # to the minimum sum
    dp[n][curr] = min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
    B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp));

    return dp[n][curr]

# Driver code
if __name__ == "__main__" :

    A = [ 1, 50, 1 ];
    B = [ 50, 50, 50 ];
    C = [ 50, 50, 50 ];

    # Initialize the dp[][] array
    dp = np.zeros((SIZE,N));

    for i in range(SIZE) :
        for j in range(N) :
            dp[i][j] = -1;

    # min(start with A[0], start with B[0], start with C[0])
    print(min(A[0] + minSum(A, B, C, 1, SIZE - 1, 0, dp),
                min(B[0] + minSum(A, B, C, 1, SIZE - 1, 1, dp),
                C[0] + minSum(A, B, C, 1, SIZE - 1, 2, dp))));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static int SIZE = 3;
static int N = 3;

// Function to return the minimized sum
static int minSum(int []A, int []B, int []C, int i,
                    int n, int curr, int [,]dp)
{

    // If all the indices have been used
    if (n <= 0)
        return 0;

    // If this value is pre-calculated
    // then return its value from dp array
    // instead of re-computing it
    if (dp[n,curr] != -1)
        return dp[n,curr];

    // Here curr is the array chosen
    // for the (i - 1)th element
    // 0 for A[], 1 for B[] and 2 for C[]

    // If A[i - 1] was chosen previously then
    // only B[i] or C[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    if (curr == 0)
    {
        return dp[n,curr]
                = Math.Min(B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp),
                    C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));
    }

    // If B[i - 1] was chosen previously then
    // only A[i] or C[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    if (curr == 1)
        return dp[n,curr]
                = Math.Min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                    C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));

    // If C[i - 1] was chosen previously then
    // only A[i] or B[i] can chosen now
    // choose the one which leads
    // to the minimum sum
    return dp[n,curr]
                = Math.Min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                    B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp));
}

// Driver code
public static void Main ()
{
    int []A = { 1, 50, 1 };
    int []B = { 50, 50, 50 };
    int []C = { 50, 50, 50 };

    // Initialize the dp[][] array
    int [,]dp = new int[SIZE,N];
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < N; j++)
            dp[i,j] = -1;

    // min(start with A[0], start with B[0], start with C[0])
    Console.WriteLine(Math.Min(A[0] + minSum(A, B, C, 1, SIZE - 1, 0, dp),
                Math.Min(B[0] + minSum(A, B, C, 1, SIZE - 1, 1, dp),
                    C[0] + minSum(A, B, C, 1, SIZE - 1, 2, dp))));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let SIZE = 3;
    let N = 3;

    // Function to return the minimized sum
    function minSum(A, B, C, i, n, curr, dp)
    {

        // If all the indices have been used
        if (n <= 0)
            return 0;

        // If this value is pre-calculated
        // then return its value from dp array
        // instead of re-computing it
        if (dp[n][curr] != -1)
            return dp[n][curr];

        // Here curr is the array chosen
        // for the (i - 1)th element
        // 0 for A[], 1 for B[] and 2 for C[]

        // If A[i - 1] was chosen previously then
        // only B[i] or C[i] can chosen now
        // choose the one which leads
        // to the minimum sum
        if (curr == 0)
        {
            return dp[n][curr]
                    = Math.min(B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp),
                        C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));
        }

        // If B[i - 1] was chosen previously then
        // only A[i] or C[i] can chosen now
        // choose the one which leads
        // to the minimum sum
        if (curr == 1)
            return dp[n][curr]
                    = Math.min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                        C[i] + minSum(A, B, C, i + 1, n - 1, 2, dp));

        // If C[i - 1] was chosen previously then
        // only A[i] or B[i] can chosen now
        // choose the one which leads
        // to the minimum sum
        return dp[n][curr]
                    = Math.min(A[i] + minSum(A, B, C, i + 1, n - 1, 0, dp),
                        B[i] + minSum(A, B, C, i + 1, n - 1, 1, dp));
    }

    let A = [ 1, 50, 1 ];
    let B = [ 50, 50, 50 ];
    let C = [ 50, 50, 50 ];

    // Initialize the dp[][] array
    let dp = new Array(SIZE);
    for (let i = 0; i < SIZE; i++)
    {
        dp[i] = new Array(N);
        for (let j = 0; j < N; j++)
        {
            dp[i][j] = -1;
        }
    }

    // min(start with A[0], start with B[0], start with C[0])
    document.write(Math.min(A[0] + minSum(A, B, C, 1, SIZE - 1, 0, dp),
                Math.min(B[0] + minSum(A, B, C, 1, SIZE - 1, 1, dp),
                    C[0] + minSum(A, B, C, 1, SIZE - 1, 2, dp))));

</script>
```

**Output:** 

```
52
```