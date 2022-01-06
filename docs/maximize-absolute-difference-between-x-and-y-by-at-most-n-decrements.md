# 将 X 和 Y 之间的绝对差值最大化最多 N 次递减

> 原文:[https://www . geeksforgeeks . org/最大化 x 和 y 之间的绝对差值最多 n 次递减/](https://www.geeksforgeeks.org/maximize-absolute-difference-between-x-and-y-by-at-most-n-decrements/)

给定五个整数 **X** 、 **Y** 、 **A** 、 **B** 和 **N** ，任务是通过精确地执行以下操作 **N** 次来找到 **X** 和 **Y** 之间最大可能的绝对差:

*   将 **X** 的值递减 **1** 至 **A** 。
*   将 **Y** 的值递减 **1** 至 **B** 。

**注意:**的值**(X–A+Y–B)**必须大于等于 **N**

**示例:**

> **输入:** X = 12，Y = 8，A = 8，B = 7，N = 2
> **输出:** 4
> **说明:**
> 将 X 的值减 1。因此，X = X–1 = 11
> 将 Y 的值减 1。因此，Y = Y–1 = 7
> 因此，X 和 Y 的最大绝对差值= ABS(X–Y)= ABS(11–7)= 4
> 
> **输入:** X = 10，Y = 10，A = 8，B = 5，N = 3
> **输出:** 3
> **说明:**
> 将 Y 的值递减 1 三次。因此，Y = Y–3 = 7
> 因此，X 和 Y 的最大绝对差值= ABS(X–Y)= ABS(10–7)= 3

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如说 **n1** 来存储在 **X** 上执行的操作的最大计数。
*   更新 **n1 = min(N，X–A)**。
*   初始化一个变量，比如说 **n2** 来存储在 **Y** 上执行的操作的最大计数。
*   更新 **n2 = min(N，Y–B)**。
*   初始化一个变量，比如 **diff_X_Y_1** 来存储 **X** 和 **Y** 的绝对差值，首先将 **X** 的值递减 **1** 正好 **min(N，n1)** 次，然后将 **Y** 的值递减剩余的运算次数。
*   初始化一个变量，比如 **diff_X_Y_2** 来存储 **X** 和 **Y** 的绝对差值，首先将 Y 的值递减 **1** 正好 **min(N，n2)** 次，然后将 **X** 的值递减剩余的运算次数。
*   最后打印 **max(diff_X_Y_1，diff_X_Y_2)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the absolute difference
// between X and Y with given operations
int AbsDiff(int X, int Y, int A, int B, int N)
{
    // Stores maximum absolute difference
    // between X and Y with given operations
    int maxDiff = 0;

    // Stores maximum number of operations
    // performed on X
    int n1 = X - A;

    // Update X
    X = X - min(N, n1);

    // Decrementing N at most N times
    N = N - min(N, n1);

    // Stores maximum number of operations
    // performed on Y
    int n2 = Y - B;

    // Update Y
    Y = Y - min(N, n2);

    // Update maxDiff
    maxDiff = abs(X - Y);

    return maxDiff;
}

// Function to find the max absolute difference
// between X and Y with given operations
int maxAbsDiff(int X, int Y, int A, int B, int N)
{
    // Stores absolute difference between
    // X and Y by first decrementing X and then Y
    int diffX_Y_1;

    // Stores absolute difference between X
    // and Y first decrementing Y and then X
    int diffX_Y_2;

    // Update diffX_Y_1
    diffX_Y_1 = AbsDiff(X, Y, A, B, N);

    // Swap X, Y and A, B
    swap(X, Y);
    swap(A, B);

    // Update diffX_Y_2
    diffX_Y_2 = AbsDiff(X, Y, A, B, N);

    return max(diffX_Y_1, diffX_Y_2);
}

// Driver Code
int main()
{
    int X = 10;
    int Y = 10;
    int A = 8;
    int B = 5;
    int N = 3;
    cout << maxAbsDiff(X, Y, A, B, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the absolute difference
// between X and Y with given operations
public static int AbsDiff(int X, int Y, int A,
                          int B, int N)
{

    // Stores maximum absolute difference
    // between X and Y with given operations
    int maxDiff = 0;

    // Stores maximum number of operations
    // performed on X
    int n1 = X - A;

    // Update X
    X = X - Math.min(N, n1);

    // Decrementing N at most N times
    N = N - Math.min(N, n1);

    // Stores maximum number of operations
    // performed on Y
    int n2 = Y - B;

    // Update Y
    Y = Y - Math.min(N, n2);

    // Update maxDiff
    maxDiff = Math.abs(X - Y);

    return maxDiff;
}

// Function to find the max absolute difference
// between X and Y with given operations
public static int maxAbsDiff(int X, int Y, int A,
                             int B, int N)
{

    // Stores absolute difference between
    // X and Y by first decrementing X and then Y
    int diffX_Y_1;

    // Stores absolute difference between X
    // and Y first decrementing Y and then X
    int diffX_Y_2;

    // Update diffX_Y_1
    diffX_Y_1 = AbsDiff(X, Y, A, B, N);

    // Swap X, Y and A, B
    int temp1 = X;
    X = Y;
    Y = temp1;

    int temp2 = A;
    A = B;
    B = temp2;

    // Update diffX_Y_2
    diffX_Y_2 = AbsDiff(X, Y, A, B, N);

    return Math.max(diffX_Y_1, diffX_Y_2);
}

// Driver code
public static void main(String[] args)
{
    int X = 10;
    int Y = 10;
    int A = 8;
    int B = 5;
    int N = 3;

    System.out.println(maxAbsDiff(X, Y, A, B, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the absolute difference
# between X and Y with given operations
def AbsDiff(X, Y, A, B, N):

    # Stores maximum absolute difference
    # between X and Y with given operations
    maxDiff = 0

    # Stores maximum number of operations
    # performed on X
    n1 = X - A

    # Update X
    X = X - min(N, n1)

    # Decrementing N at most N times
    N = N - min(N, n1)

    # Stores maximum number of operations
    # performed on Y
    n2 = Y - B

    # Update Y
    Y = Y - min(N, n2)

    # Update maxDiff
    maxDiff = abs(X - Y)

    return maxDiff

# Function to find the max absolute difference
# between X and Y with given operations
def maxAbsDiff(X, Y, A, B, N):

    # Stores absolute difference between
    # X and Y by first decrementing X and then Y
    diffX_Y_1 = AbsDiff(X, Y, A, B, N)

    # Swap X, Y and A, B
    temp1 = X
    X = Y
    Y = temp1

    temp2 = A
    A = B
    B = temp2

    # Stores absolute difference between X
    # and Y first decrementing Y and then X
    diffX_Y_2 = AbsDiff(X, Y, A, B, N)

    return max(diffX_Y_1, diffX_Y_2)

# Driver Code
X = 10
Y = 10
A = 8
B = 5
N = 3

print(maxAbsDiff(X, Y, A, B, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the absolute difference
// between X and Y with given operations
public static int AbsDiff(int X, int Y, int A,
                          int B, int N)
{

    // Stores maximum absolute difference
    // between X and Y with given operations
    int maxDiff = 0;

    // Stores maximum number of operations
    // performed on X
    int n1 = X - A;

    // Update X
    X = X - Math.Min(N, n1);

    // Decrementing N at most N times
    N = N - Math.Min(N, n1);

    // Stores maximum number of operations
    // performed on Y
    int n2 = Y - B;

    // Update Y
    Y = Y - Math.Min(N, n2);

    // Update maxDiff
    maxDiff = Math.Abs(X - Y);

    return maxDiff;
}

// Function to find the max absolute difference
// between X and Y with given operations
public static int maxAbsDiff(int X, int Y, int A,
                             int B, int N)
{

    // Stores absolute difference between
    // X and Y by first decrementing X and then Y
    int diffX_Y_1;

    // Stores absolute difference between X
    // and Y first decrementing Y and then X
    int diffX_Y_2;

    // Update diffX_Y_1
    diffX_Y_1 = AbsDiff(X, Y, A, B, N);

    // Swap X, Y and A, B
    int temp1 = X;
    X = Y;
    Y = temp1;

    int temp2 = A;
    A = B;
    B = temp2;

    // Update diffX_Y_2
    diffX_Y_2 = AbsDiff(X, Y, A, B, N);

    return Math.Max(diffX_Y_1, diffX_Y_2);
}

// Driver code
public static void Main(String[] args)
{
    int X = 10;
    int Y = 10;
    int A = 8;
    int B = 5;
    int N = 3;

    Console.WriteLine(maxAbsDiff(X, Y, A, B, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the absolute difference
// between X and Y with given operations
function AbsDiff(X, Y, A, B, N)
{

    // Stores maximum absolute difference
    // between X and Y with given operations
    let maxDiff = 0;

    // Stores maximum number of operations
    // performed on X
    let n1 = X - A;

    // Update X
    X = X - Math.min(N, n1);

    // Decrementing N at most N times
    N = N - Math.min(N, n1);

    // Stores maximum number of operations
    // performed on Y
    let n2 = Y - B;

    // Update Y
    Y = Y - Math.min(N, n2);

    // Update maxDiff
    maxDiff = Math.abs(X - Y);

    return maxDiff;
}

// Function to find the max absolute difference
// between X and Y with given operations
function maxAbsDiff(X, Y, A, B, N)
{

    // Stores absolute difference between
    // X and Y by first decrementing X and then Y
    let diffX_Y_1;

    // Stores absolute difference between X
    // and Y first decrementing Y and then X
    let diffX_Y_2;

    // Update diffX_Y_1
    diffX_Y_1 = AbsDiff(X, Y, A, B, N);

    // Swap X, Y and A, B
    let temp1 = X;
    X = Y;
    Y = temp1;

    let temp2 = A;
    A = B;
    B = temp2;

    // Update diffX_Y_2
    diffX_Y_2 = AbsDiff(X, Y, A, B, N);

    return Math.max(diffX_Y_1, diffX_Y_2);
}
    // Driver Code

     let  X = 10;
    let Y = 10;
    let A = 8;
    let B = 5;
    let N = 3;

    document.write(maxAbsDiff(X, Y, A, B, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)