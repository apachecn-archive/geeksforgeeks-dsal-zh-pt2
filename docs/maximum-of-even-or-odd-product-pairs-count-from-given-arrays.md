# 给定数组中偶数或奇数乘积对的最大计数

> 原文:[https://www . geeksforgeeks . org/给定数组中偶数或奇数乘积对的最大数量/](https://www.geeksforgeeks.org/maximum-of-even-or-odd-product-pairs-count-from-given-arrays/)

给定由 **N** 个整数组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是用偶数和奇数乘积对 **(A[i]，B[j])** 进行计数，并打印两个计数的最大值。

**示例:**

> **输入:** A[] = {1，2，3}，B[] = {4，5，6}
> **输出:** 7
> **说明:**
> 奇数积计数的对为:(1，5) (3，5)。因此，奇数乘积的对数= 2。
> 产品计数为偶数的对是:(1，4) (1，6) (2，4) (2，5) (2，6) (3，4) (3，6)。因此，偶数乘积的对数= 7
> 因此，两个计数的最大值为 7。因此，输出 7。
> 
> **输入:** A[] = {1，5，9}，B[] = {1，7，3}
> **输出:** 9
> **说明:**
> 奇数乘积计数的对为:(1，1) (1，7) (1，3) (5，1) (5，7) (5，3) (9，1) (9，7) (9，3)。因此，奇数乘积的对数= 9
> 不存在偶数乘积计数的对。
> 因此，输出 9。

**天真方法:**最简单的方法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)和[检查它们的乘积是偶数还是奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，并相应地增加它们各自的计数。检查所有对后，打印这两个计数的最大值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效解:**上述方法可以通过观察到只有一对奇数相乘才会产生奇数来优化。否则，将生成一个偶数。按照以下步骤解决问题:

*   初始化变量 **oddcount** 、**event count**、**T5】和 **oddCountB** 至 **0** 分别存储数组 **B[]** 中奇数对、偶数对的计数。**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **B[]** ，如果元素为奇数，则递增**奇数**。现在**(N–odd countb)**的值给出数组 **B[]** 中偶数元素的个数。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【A】并执行以下操作:
    *   如果当前元素是偶数，则用 **N** 来增加**偶数**，因为在 **B[]** 中乘以任何数字都会得到偶数乘积对。
    *   否则，将**B【】**中的偶数与**A【】**中的奇数相乘，得出**(N-odd count B)**对，将 **oddcount** 增加 **oddCountB** ，因为**B【】**中的奇数与**A【】**中的奇数相乘
*   完成以上步骤后，打印**奇数**和**偶数**的最大计数作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// count of odd count pair or
// even count pair
int maxcountpair(int A[], int B[], int N)
{
    // Stores odd count, even count
    // pairs and odd numbers in B[]
    int oddcount = 0, evencount = 0;
    int oddCountB = 0;

    // Traverse the array B[]
    for (int i = 0; i < N; i++) {

        // If B[i] is an odd number
        if (B[i] & 1)

            // Increment oddCountB by 1
            oddCountB += 1;
    }

    // Traverse the array A[]
    for (int i = 0; i < N; i++) {

        // If A[i] is an odd number
        if (A[i] & 1) {
            oddcount += oddCountB;
            evencount += (N - oddCountB);
        }

        // If A[i] is even
        else
            evencount += N;
    }

    // Return maximum count of odd
    // and even pairs
    return max(oddcount, evencount);
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3 };
    int B[] = { 4, 5, 6 };

    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << maxcountpair(A, B, N);

    return 0;
}
```

## C

```
// C program for above approach
#include <stdio.h>

// Function to return the
// maximum of two numbers
int max(int num1, int num2)
{
    return (num1 > num2) ? num1 : num2;
}

// Function to return the maximum count of
// odd count pair or even count pair
int maxcountpair(int A[], int B[], int N)
{

    // Stores odd count, even count
    // pairs and odd numbers in B[]
    int oddcount = 0, evencount = 0;
    int oddCountB = 0;

    // Traverse the array B[]
    for(int i = 0; i < N; i++)
    {

        // If B[i] is an odd number
        if (B[i] & 1)

            // Increment oddCountB by 1
            oddCountB += 1;
    }

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
    {

        // If A[i] is an odd number
        if (A[i] & 1)
        {
            oddcount += oddCountB;
            evencount += (N - oddCountB);
        }

        // If A[i] is even
        else
            evencount += N;
    }

    // Return maximum count of odd
    // and even pairs
    return max(oddcount, evencount);
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3 };
    int B[] = { 4, 5, 6 };

    int N = sizeof(A) / sizeof(A[0]);

    printf("%d", maxcountpair(A, B, N));

    return 0;
}

// This code is contributed by sourav singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

class GFG{

// Function to return the maximum count of
// odd count pair or even count pair
static int maxcountpair(int A[], int B[],
                        int N)
{

    // Stores odd count, even count
    // pairs and odd numbers in B[]
    int oddcount = 0, evencount = 0;
    int oddCountB = 0;

    // Traverse the array B[]
    for(int i = 0; i < N; i++)
    {

        // If B[i] is an odd number
        if (B[i] % 2 == 1)

            // Increment oddCountB by 1
            oddCountB += 1;
    }

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
    {

        // If A[i] is an odd number
        if (A[i] % 2 == 1)
        {
            oddcount += oddCountB;
            evencount += (N - oddCountB);
        }

        // If A[i] is even
        else
            evencount += N;
    }

    // Return maximum count of odd
    // and even pairs
    return (oddcount > evencount) ? oddcount
                                  : evencount;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 2, 3 };
    int B[] = { 4, 5, 6 };
    int N = A.length;

    System.out.print(maxcountpair(A, B, N));
}
}

// This code is contributed by sourav singh
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to return the maximum count of
# odd count pair or even count pair
def maxcountpair(A, B, N):

    # Function to return the maximum count of
    # odd count pair or even count pair
    oddcount = 0
    evencount = 0
    oddCountB = 0

    # Traverse the array, B[]
    for i in range(0, N):

        # If B[i] is an odd number
        if B[i] % 2 == 1:
            oddCountB += 1

    # Traverse the array, A[]
    for i in range(0, N):

        # If A[i] is an odd number
        if A[i] % 2 == 1:
            oddcount += oddCountB
            evencount += (N - oddCountB)
        else:
            evencount += N

    # Return maximum count of odd
    # and even pairs
    return max(oddcount, evencount)

# Driver Code
A = [ 1, 2, 3 ]
B = [ 4, 5, 6 ]
N = len(A)

print(maxcountpair(A, B, N))

# This code is contributed by sourav singh
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the maximum count of
// odd count pair or even count pair
static int maxcountpair(int[] A, int[] B,
                        int N)
{

    // Stores odd count, even count
    // pairs and odd numbers in B[]
    int oddcount = 0, evencount = 0;
    int oddCountB = 0;

    // Traverse the array B[]
    for(int i = 0; i < N; i++)
    {

        // If B[i] is an odd number
        if (B[i] % 2 == 1)

            // Increment oddCountB by 1
            oddCountB += 1;
    }

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
    {

        // If A[i] is an odd number
        if (A[i] % 2 == 1)
        {
            oddcount += oddCountB;
            evencount += (N - oddCountB);
        }

        // If A[i] is even
        else
            evencount += N;
    }

    // Return maximum count of odd
    // and even pairs
    return (oddcount > evencount) ? oddcount
                                  : evencount;
}

// Driver Code
public static void Main(String[] args)
{
    int[] A = { 1, 2, 3 };
    int[] B = { 4, 5, 6 };
    int N = A.Length;

    // Function call
    Console.Write(maxcountpair(A, B, N));
}
}

// This code is contributed by sourav singh
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to return the maximum
// count of odd count pair or
// even count pair
function maxcountpair(A, B, N)
{
    // Stores odd count, even count
    // pairs and odd numbers in B[]
    let oddcount = 0, evencount = 0;
    let oddCountB = 0;

    // Traverse the array B[]
    for (let i = 0; i < N; i++) {

        // If B[i] is an odd number
        if (B[i] & 1)

            // Increment oddCountB by 1
            oddCountB += 1;
    }

    // Traverse the array A[]
    for (let i = 0; i < N; i++) {

        // If A[i] is an odd number
        if (A[i] & 1) {
            oddcount += oddCountB;
            evencount += (N - oddCountB);
        }

        // If A[i] is even
        else
            evencount += N;
    }

    // Return maximum count of odd
    // and even pairs
    return Math.max(oddcount, evencount);
}

// Driver Code

    let A = [ 1, 2, 3 ];
    let B = [ 4, 5, 6 ];

    let N = A.length;

    // Function Call
    document.write(maxcountpair(A, B, N));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)