# 左边可被当前元素整除的元素数

> 原文:[https://www . geeksforgeeks . org/左侧可被当前元素整除的元素计数/](https://www.geeksforgeeks.org/count-of-elements-on-the-left-which-are-divisible-by-current-element/)

给定一个 **N** 整数的数组 **A[]** ，任务是生成一个数组 **B[]** ，使得 **B[i]** 包含 **A[]** 中的索引 **j** 的计数，使得 **j < i** 和 **A[j] % A[i] = 0**
**示例:**

> **输入:** arr[] = {3，5，1}
> **输出:** 0 0 2
> 3 和 5 不除
> 左侧的任何元素，但 1 除 3 和 5。
> **输入:** arr[] = {8，1，28，4，2，6，7}
> **输出:** 0 1 0 2 3 0 1

**方法:**从数组的第一个元素到最后一个元素运行一个循环，对于当前元素，对它左边的元素运行另一个循环，检查它左边有多少元素可以被它整除。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// elements of the array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to generate and print
// the required array
void generateArr(int A[], int n)
{
    int B[n];

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // To store the count of elements
        // on the left that the current
        // element divides
        int cnt = 0;
        for (int j = 0; j < i; j++) {
            if (A[j] % A[i] == 0)
                cnt++;
        }
        B[i] = cnt;
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
int main()
{
    int A[] = { 3, 5, 1 };
    int n = sizeof(A) / sizeof(A[0]);

    generateArr(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Utility function to print the
// elements of the array
static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to generate and print
// the required array
static void generateArr(int A[], int n)
{
    int []B = new int[n];

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // To store the count of elements
        // on the left that the current
        // element divides
        int cnt = 0;
        for (int j = 0; j < i; j++)
        {
            if (A[j] % A[i] == 0)
                cnt++;
        }
        B[i] = cnt;
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
public static void main(String args[])
{
    int A[] = { 3, 5, 1 };
    int n = A.length;

    generateArr(A, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print the
# elements of the array
def printArr(arr, n):

    for i in arr:
        print(i, end = " ")

# Function to generate and print
# the required array
def generateArr(A, n):
    B = [0 for i in range(n)]

    # For every element of the array
    for i in range(n):

        # To store the count of elements
        # on the left that the current
        # element divides
        cnt = 0
        for j in range(i):
            if (A[j] % A[i] == 0):
                cnt += 1

        B[i] = cnt

    # Print the generated array
    printArr(B, n)

# Driver code
A = [3, 5, 1]
n = len(A)

generateArr(A, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Utility function to print the
// elements of the array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to generate and print
// the required array
static void generateArr(int []A, int n)
{
    int []B = new int[n];

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // To store the count of elements
        // on the left that the current
        // element divides
        int cnt = 0;
        for (int j = 0; j < i; j++)
        {
            if (A[j] % A[i] == 0)
                cnt++;
        }
        B[i] = cnt;
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
public static void Main(String []args)
{
    int []A = { 3, 5, 1 };
    int n = A.Length;

    generateArr(A, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to print the
// elements of the array
function printArr(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to generate and print
// the required array
function generateArr(A, n)
{
    let B = new Array(n);

    // For every element of the array
    for (let i = 0; i < n; i++) {

        // To store the count of elements
        // on the left that the current
        // element divides
        let cnt = 0;
        for (let j = 0; j < i; j++) {
            if (A[j] % A[i] == 0)
                cnt++;
        }
        B[i] = cnt;
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
    let A = [ 3, 5, 1 ];
    let n = A.length;

    generateArr(A, n);

</script>
```

**Output:** 

```
0 0 2
```