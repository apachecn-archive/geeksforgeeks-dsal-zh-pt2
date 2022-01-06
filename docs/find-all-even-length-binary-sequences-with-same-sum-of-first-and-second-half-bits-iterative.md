# 找出所有第一半位和第二半位和相同的偶数长度二进制序列|迭代

> 原文:[https://www . geeksforgeeks . org/find-所有偶数长度的二进制序列-具有相同的第一和第二半比特之和-迭代/](https://www.geeksforgeeks.org/find-all-even-length-binary-sequences-with-same-sum-of-first-and-second-half-bits-iterative/)

给定一个数字 **N** ，找出所有长度为 **2*N** 的二进制序列，使得第一个 **N** 位的总和与最后一个 **N** 位的总和相同。
**举例:**

> **输入:** N = 2
> **输出:**
> 0000
> 0101
> 0110
> 1001
> 1010
> 1111
> **输入:** N = 1
> **输出:**
> 00
> 11

**注:**这个问题的递归方法可以在[这里](https://www.geeksforgeeks.org/find-all-even-length-binary-sequences-with-same-sum-of-first-and-second-half-bits/)找到。
**方法:**
一种简单的方法，从 **0** 到 **2 <sup>2*N</sup>** 运行一个循环，转换成二进制形式，检查前半部分的和是否等于后半部分的和。
如果上述条件成立，则打印该号码，否则检查下一个号码。
以下是上述方法的实施:

## C++

```
// C++ implementation
#include <iostream>
#include <malloc.h>
#include <math.h>
using namespace std;

// Function to convert the
// number into binary and
// store the number into
// an array
void convertToBinary(int num, int a[], int n)
{

    int pointer = n - 1;
    while (num > 0) {
        a[pointer] = num % 2;
        num = num / 2;
        pointer--;
    }
}

// Function to check if the
// sum of the digits till
// the mid of the array and
// the sum of the digits
// from mid till n is the
// same, if they are same
// then print that binary
void checkforsum(int a[], int n)
{

    int sum1 = 0;
    int sum2 = 0;
    int mid = n / 2;

    // Calculating the sum from
    // 0 till mid and store
    // in sum1
    for (int i = 0; i < mid; i++)
        sum1 = sum1 + a[i];

    // Calculating the sum
    // from mid till n and
    // store in sum2
    for (int j = mid; j < n; j++)
        sum2 = sum2 + a[j];

    // If sum1 is same as
    // sum2 print the binary
    if (sum1 == sum2) {
        for (int i = 0; i < n; i++)
            cout << a[i];
        cout << "\n";
    }
}

// Function to print sequence
void print_seq(int m)
{

    int n = (2 * m);

    // Creating the array
    int a[n];

    // Initialize the array
    // with 0 to store the
    // binary nnumbers
    for (int j = 0; j < n; j++) {
        a[j] = 0;
    }

    for (int i = 0; i < (int)pow(2, n); i++) {

        // Converting the number
        // into binary first
        convertToBinary(i, a, n);

        // Checking if the sum of
        // the first half of the
        // array is same as the
        // sum of the next half
        checkforsum(a, n);
    }
}

// Driver Code
int main()
{
    int m = 2;

    print_seq(m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code implementation for above approach
class GFG
{

    // Function to convert the
    // number into binary and
    // store the number into
    // an array
    static void convertToBinary(int num,
                                int a[], int n)
    {
        int pointer = n - 1;
        while (num > 0)
        {
            a[pointer] = num % 2;
            num = num / 2;
            pointer--;
        }
    }

    // Function to check if the
    // sum of the digits till
    // the mid of the array and
    // the sum of the digits
    // from mid till n is the
    // same, if they are same
    // then print that binary
    static void checkforsum(int a[], int n)
    {
        int sum1 = 0;
        int sum2 = 0;
        int mid = n / 2;

        // Calculating the sum from
        // 0 till mid and store
        // in sum1
        for (int i = 0; i < mid; i++)
            sum1 = sum1 + a[i];

        // Calculating the sum
        // from mid till n and
        // store in sum2
        for (int j = mid; j < n; j++)
            sum2 = sum2 + a[j];

        // If sum1 is same as
        // sum2 print the binary
        if (sum1 == sum2)
        {
            for (int i = 0; i < n; i++)
                System.out.print(a[i]);
            System.out.println();
        }
    }

    // Function to print sequence
    static void print_seq(int m)
    {

        int n = (2 * m);

        // Creating the array
        int a[] = new int[n];

        // Initialize the array
        // with 0 to store the
        // binary nnumbers
        for (int j = 0; j < n; j++)
        {
            a[j] = 0;
        }

        for (int i = 0; i < (int)Math.pow(2, n); i++)
        {

            // Converting the number
            // into binary first
            convertToBinary(i, a, n);

            // Checking if the sum of
            // the first half of the
            // array is same as the
            // sum of the next half
            checkforsum(a, n);
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int m = 2;

        print_seq(m);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to convert the number into binary
# and store the number into an array
def convertToBinary(num, a, n):

    pointer = n - 1
    while (num > 0):
        a[pointer] = num % 2
        num = num // 2
        pointer -= 1

# Function to check if the sum of the digits till
# the mid of the array and the sum of the digits
# from mid till n is the same, if they are same
# then print that binary
def checkforsum(a, n):

    sum1 = 0
    sum2 = 0
    mid = n // 2

    # Calculating the sum from 0 till mid
    # and store in sum1
    for i in range(mid):
        sum1 = sum1 + a[i]

    # Calculating the sum from mid till n
    # and store in sum2
    for j in range(mid, n):
        sum2 = sum2 + a[j]

    # If sum1 is same as sum2 print the binary
    if (sum1 == sum2):
        for i in range(n):
            print(a[i], end = "")
        print()

# Function to prsequence
def print_seq(m):

    n = (2 * m)

    # Creating the array
    a = [0 for i in range(n)]

    for i in range(pow(2, n)):

        # Converting the number
        # into binary first
        convertToBinary(i, a, n)

        # Checking if the sum of the first half
        # of the array is same as the sum of
        # the next half
        checkforsum(a, n)

# Driver Code
m = 2

print_seq(m)

# This code is contributed by mohit kumar
```

## C#

```
// C# code implementation for above approach
using System;

class GFG
{

    // Function to convert the
    // number into binary and
    // store the number into
    // an array
    static void convertToBinary(int num,
                                int []a, int n)
    {
        int pointer = n - 1;
        while (num > 0)
        {
            a[pointer] = num % 2;
            num = num / 2;
            pointer--;
        }
    }

    // Function to check if the
    // sum of the digits till
    // the mid of the array and
    // the sum of the digits
    // from mid till n is the
    // same, if they are same
    // then print that binary
    static void checkforsum(int []a, int n)
    {
        int sum1 = 0;
        int sum2 = 0;
        int mid = n / 2;

        // Calculating the sum from
        // 0 till mid and store
        // in sum1
        for (int i = 0; i < mid; i++)
            sum1 = sum1 + a[i];

        // Calculating the sum
        // from mid till n and
        // store in sum2
        for (int j = mid; j < n; j++)
            sum2 = sum2 + a[j];

        // If sum1 is same as
        // sum2 print the binary
        if (sum1 == sum2)
        {
            for (int i = 0; i < n; i++)
                Console.Write(a[i]);
            Console.WriteLine();
        }
    }

    // Function to print sequence
    static void print_seq(int m)
    {

        int n = (2 * m);

        // Creating the array
        int []a = new int[n];

        // Initialize the array
        // with 0 to store the
        // binary nnumbers
        for (int j = 0; j < n; j++)
        {
            a[j] = 0;
        }

        for (int i = 0; i < (int)Math.Pow(2, n); i++)
        {

            // Converting the number
            // into binary first
            convertToBinary(i, a, n);

            // Checking if the sum of
            // the first half of the
            // array is same as the
            // sum of the next half
            checkforsum(a, n);
        }
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int m = 2;

        print_seq(m);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation

// Function to convert the
// number into binary and
// store the number into
// an array
function convertToBinary(num, a, n)
{

    let pointer = n - 1;
    while (num > 0) {
        a[pointer] = num % 2;
        num = parseInt(num / 2);
        pointer--;
    }
}

// Function to check if the
// sum of the digits till
// the mid of the array and
// the sum of the digits
// from mid till n is the
// same, if they are same
// then print that binary
function checkforsum(a, n)
{

    let sum1 = 0;
    let sum2 = 0;
    let mid = parseInt(n / 2);

    // Calculating the sum from
    // 0 till mid and store
    // in sum1
    for (let i = 0; i < mid; i++)
        sum1 = sum1 + a[i];

    // Calculating the sum
    // from mid till n and
    // store in sum2
    for (let j = mid; j < n; j++)
        sum2 = sum2 + a[j];

    // If sum1 is same as
    // sum2 print the binary
    if (sum1 == sum2) {
        for (let i = 0; i < n; i++)
            document.write(a[i]);
        document.write("<br>");
    }
}

// Function to print sequence
function print_seq(m)
{

    let n = (2 * m);

    // Creating the array
    let a = new Array(n);

    // Initialize the array
    // with 0 to store the
    // binary nnumbers
    for (let j = 0; j < n; j++) {
        a[j] = 0;
    }

    for (let i = 0; i < Math.pow(2, n); i++) {

        // Converting the number
        // into binary first
        convertToBinary(i, a, n);

        // Checking if the sum of
        // the first half of the
        // array is same as the
        // sum of the next half
        checkforsum(a, n);
    }
}

// Driver Code
    let m = 2;

    print_seq(m);

</script>
```

**Output:** 

```
0000
0101
0110
1001
1010
1111
```