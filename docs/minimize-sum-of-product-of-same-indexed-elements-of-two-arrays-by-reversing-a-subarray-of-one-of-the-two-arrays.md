# 通过反转两个阵列之一的子阵列来最小化两个阵列的相同索引元素的乘积之和

> 原文:[https://www . geesforgeks . org/通过反转两个数组中的一个子数组来最小化两个数组中相同索引元素的乘积之和/](https://www.geeksforgeeks.org/minimize-sum-of-product-of-same-indexed-elements-of-two-arrays-by-reversing-a-subarray-of-one-of-the-two-arrays/)

给定仅由正整数组成的两个等长[阵列](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是反转第一个阵列的任何[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得两个阵列的相同索引元素的乘积之和，即 **(A[i] * B[i])** 最小。

**示例:**

> **输入:** N = 4，A[] = {2，3，1，5}，B[] = {8，2，4，3 }
> T3】输出:T5】A[]= 1 3 2 5
> B[]= 8 2 4 3
> 最小积为 37
> 
> **说明:**反转子阵{A[0]，A[2]}。相同索引元素的乘积之和是 37，这是可能的最小值。
> 
> **输入:** N = 3，A[] = {3，1，1}，B[] = {4，5，6 }
> T3】输出:T5】A[]= 3 1
> B[]= 4 5 6
> 最小积为 23

**方法:**给定的问题可以通过使用[两点技巧](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决问题:

*   声明一个变量，比如 **total** ，来存储两个数组的初始乘积。
*   声明一个变量，说 **min** ，存储需要的答案。
*   声明两个变量，比如**第一个**和**第二个**，来存储需要反转以最小化产品的子阵列的开始和结束索引。
*   通过以下操作计算**奇数长度子阵列**的最小可能乘积:
    *   [使用变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，说 **i** 。
    *   检查所有奇数长度的子阵列，通过设置**I–1**，说**左**，和 **i + 1** ，说**右**作为子阵列的开始和结束索引。
    *   通过减去【total 左]* b[左]+a[右]* b[右] 并加上 a[左]* b[右]+a[右]* b[左]来更新**总计**。
    *   对于每个子阵列，在更新**总数**后，检查它是否是获得的最小值。相应地更新和存储最小产品。
*   同样，检查所有偶数长度的子阵列并计算总和。
*   最后，打印得到的数组和最小和。

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print1 the arrays
void print1(vector<int> &a, vector<int> &b)
{
    int minProd = 0;

    for(int i = 0; i < a.size(); ++i)
    {
        cout << a[i] << " ";
    }
    cout << endl;

    for(int i = 0; i < b.size(); ++i)
    {
        cout << b[i] << " ";
        minProd += a[i] * b[i];
    }
    cout << endl;
    cout << minProd;
}

// Function to reverse1 the subarray
void reverse1(int left, int right,
                 vector<int> &arr)
{
    while (left < right)
    {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        ++left;
        --right;
    }
}

// Function to calculate the
// minimum product of same-indexed
// elements of two given arrays
void minimumProdArray(vector<int> &a,
                      vector<int> &b, int l)
{
    int total = 0;

    // Calculate initial product
    for(int i = 0; i < a.size(); ++i)
    {
        total += a[i] * b[i];
    }

    int min = INT_MAX;
    int first = 0;
    int second = 0;

    // Traverse all odd length subarrays
    for(int i = 0; i < a.size(); ++i)
    {
        int left = i - 1;
        int right = i + 1;
        int total1 = total;

        while (left >= 0 && right < a.size())
        {

            // Remove the previous product
            total1 -= a[left] * b[left] +
                     a[right] * b[right];

            // Add the current product
            total1 += a[left] * b[right] +
                     a[right] * b[left];

            // Check if current product
            // is minimum or not
            if (min >= total1)
            {
                min = total1;
                first = left;
                second = right;
            }
            --left;
            ++right;
        }
    }

    // Traverse all even length subarrays
    for(int i = 0; i < a.size(); ++i)
    {
        int left = i;
        int right = i + 1;
        int total1 = total;

        while (left >= 0 && right < a.size())
        {

            // Remove the previous product
            total1 -= a[left] * b[left] +
                     a[right] * b[right];

            // Add to the current product
            total1 += a[left] * b[right] +
                     a[right] * b[left];

            // Check if current product
            // is minimum or not
            if (min >= total1)
            {
                min = total1;
                first = left;
                second = right;
            }

            // Update the pointers
            --left;
            ++right;
        }
    }

    // reverse1 the subarray
    if (min < total)
    {
        reverse1(first, second, a);

        // print1 the subarray
        print1(a, b);
    }
    else
    {
        print1(a, b);
    }
}

// Driver Code
int main()
{
    int n = 4;
    vector<int> a{ 2, 3, 1, 5 };
    vector<int> b{ 8, 2, 4, 3 };

    minimumProdArray(a, b, n);
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the above approach

import java.io.*;
import java.util.*;

public class Main {

    // Function to calculate the
    // minimum product of same-indexed
    // elements of two given arrays
    static void minimumProdArray(long a[],
                                 long b[], int l)
    {
        long total = 0;

        // Calculate initial product
        for (int i = 0; i < a.length; ++i) {
            total += a[i] * b[i];
        }

        long min = Integer.MAX_VALUE;

        int first = 0;
        int second = 0;

        // Traverse all odd length subarrays
        for (int i = 0; i < a.length; ++i) {

            int left = i - 1;
            int right = i + 1;
            long total1 = total;
            while (left >= 0 && right < a.length) {

                // Remove the previous product
                total1 -= a[left] * b[left]
                          + a[right] * b[right];

                // Add the current product
                total1 += a[left] * b[right]
                          + a[right] * b[left];

                // Check if current product
                // is minimum or not
                if (min >= total1) {

                    min = total1;
                    first = left;
                    second = right;
                }

                --left;
                ++right;
            }
        }

        // Traverse all even length subarrays
        for (int i = 0; i < a.length; ++i) {

            int left = i;
            int right = i + 1;
            long total1 = total;

            while (left >= 0 && right < a.length) {

                // Remove the previous product
                total1 -= a[left] * b[left]
                          + a[right] * b[right];

                // Add to the current product
                total1 += a[left] * b[right]
                          + a[right] * b[left];

                // Check if current product
                // is minimum or not
                if (min >= total1) {
                    min = total1;
                    first = left;
                    second = right;
                }

                // Update the pointers
                --left;
                ++right;
            }
        }

        // Reverse the subarray
        if (min < total) {

            reverse(first, second, a);

            // Print the subarray
            print(a, b);
        }

        else {
            print(a, b);
        }
    }

    // Function to reverse the subarray
    static void reverse(int left, int right,
                        long arr[])
    {
        while (left < right) {
            long temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            ++left;
            --right;
        }
    }

    // Function to print the arrays
    static void print(long a[], long b[])
    {
        int minProd = 0;

        for (int i = 0; i < a.length; ++i) {
            System.out.print(a[i] + " ");
        }
        System.out.println();
        for (int i = 0; i < b.length; ++i) {
            System.out.print(b[i] + " ");
            minProd += a[i] * b[i];
        }
        System.out.println();
        System.out.println(minProd);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        long a[] = { 2, 3, 1, 5 };
        long b[] = { 8, 2, 4, 3 };

        minimumProdArray(a, b, n);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement the above approach

# Function to calculate the
# minimum product of same-indexed
# elements of two given arrays
def minimumProdArray(a, b, l) :

    total = 0

    # Calculate initial product
    for i in range(len(a)):
        total += a[i] * b[i]

    Min = 2147483647
    first = 0;
    second = 0;

    # Traverse all odd length subarrays
    for i in range(len(a)):

        left = i - 1;
        right = i + 1;
        total1 = total;
        while (left >= 0 and right < len(a)) :

            # Remove the previous product
            total1 -= a[left] * b[left] + a[right] * b[right];

            # Add the current product
            total1 += a[left] * b[right] + a[right] * b[left];

            # Check if current product
            # is minimum or not
            if (Min >= total1) :

                Min = total1
                first = left
                second = right

            left -= 1
            right += 1

    # Traverse all even length subarrays
    for i in range(len(a)):

        left = i
        right = i + 1
        total1 = total

        while (left >= 0 and right < len(a)) :

            # Remove the previous product
            total1 -= a[left] * b[left] + a[right] * b[right]

            # Add to the current product
            total1 += a[left] * b[right] + a[right] * b[left]

            # Check if current product
            # is minimum or not
            if (Min >= total1) :
                Min = total1
                first = left
                second = right

            # Update the pointers
            left -= 1
            right += 1

    # Reverse the subarray
    if (Min < total) :

        reverse(first, second, a)

        # Print the subarray
        Print(a, b)

    else :
        Print(a, b)

# Function to reverse the subarray
def reverse(left, right, arr) :

    while (left < right) :
        temp = arr[left]
        arr[left] = arr[right]
        arr[right] = temp
        left += 1
        right -= 1

# Function to print the arrays
def Print(a, b):

    minProd = 0

    for i in range(len(a)):
        print(a[i], end = " ")

    print();
    for i in range(len(b)):
        print(b[i], end = " ")
        minProd += a[i] * b[i]

    print()
    print(minProd)

n = 4;
a = [ 2, 3, 1, 5 ]
b = [ 8, 2, 4, 3 ]

minimumProdArray(a, b, n)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# Program to implement the above approach
using System;
public class GFG {

    // Function to calculate the
    // minimum product of same-indexed
    // elements of two given arrays
    static void minimumProdArray(long[] a, long[] b, int l)
    {
        long total = 0;

        // Calculate initial product
        for (int i = 0; i < a.Length; ++i) {
            total += a[i] * b[i];
        }

        long min = Int32.MaxValue;
        int first = 0;
        int second = 0;

        // Traverse all odd length subarrays
        for (int i = 0; i < a.Length; ++i) {

            int left = i - 1;
            int right = i + 1;
            long total1 = total;
            while (left >= 0 && right < a.Length) {

                // Remove the previous product
                total1 -= a[left] * b[left]
                          + a[right] * b[right];

                // Add the current product
                total1 += a[left] * b[right]
                          + a[right] * b[left];

                // Check if current product
                // is minimum or not
                if (min >= total1) {

                    min = total1;
                    first = left;
                    second = right;
                }

                --left;
                ++right;
            }
        }

        // Traverse all even length subarrays
        for (int i = 0; i < a.Length; ++i) {

            int left = i;
            int right = i + 1;
            long total1 = total;

            while (left >= 0 && right < a.Length) {

                // Remove the previous product
                total1 -= a[left] * b[left]
                          + a[right] * b[right];

                // Add to the current product
                total1 += a[left] * b[right]
                          + a[right] * b[left];

                // Check if current product
                // is minimum or not
                if (min >= total1) {
                    min = total1;
                    first = left;
                    second = right;
                }

                // Update the pointers
                --left;
                ++right;
            }
        }

        // Reverse the subarray
        if (min < total) {

            reverse(first, second, a);

            // Print the subarray
            print(a, b);
        }

        else {
            print(a, b);
        }
    }

    // Function to reverse the subarray
    static void reverse(int left, int right, long[] arr)
    {
        while (left < right) {
            long temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            ++left;
            --right;
        }
    }

    // Function to print the arrays
    static void print(long[] a, long[] b)
    {
        long minProd = 0;

        for (int i = 0; i < a.Length; ++i) {
            Console.Write(a[i] + " ");
        }
        Console.WriteLine();
        for (int i = 0; i < b.Length; ++i) {
            Console.Write(b[i] + " ");
            minProd += a[i] * b[i];
        }
        Console.WriteLine();
        Console.WriteLine(minProd);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int n = 4;
        long[] a = { 2, 3, 1, 5 };
        long[] b = { 8, 2, 4, 3 };

        minimumProdArray(a, b, n);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to print1 the arrays
function print1(a, b) {
    let minProd = 0;

    for (let i = 0; i < a.length; ++i) {
        document.write(a[i] + " ");
    }
    document.write("<br>");

    for (let i = 0; i < b.length; ++i) {
        document.write(b[i] + " ");
        minProd += a[i] * b[i];

    }
    document.write("<br>");
    document.write(minProd);
}

// Function to reverse1 the subarray
function reverse1(left, right, arr) {
    while (left < right) {
        let temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        ++left;
        --right;
    }
}

// Function to calculate the
// minimum product of same-indexed
// elements of two given arrays
function minimumProdArray(a, b, l) {
    let total = 0;

    // Calculate initial product
    for (let i = 0; i < a.length; ++i) {
        total += a[i] * b[i];
    }

    let min = Number.MAX_SAFE_INTEGER;
    let first = 0;
    let second = 0;

    // Traverse all odd length subarrays
    for (let i = 0; i < a.length; ++i) {
        let left = i - 1;
        let right = i + 1;
        let total1 = total;

        while (left >= 0 && right < a.length) {

            // Remove the previous product
            total1 -= a[left] * b[left] +
                a[right] * b[right];

            // Add the current product
            total1 += a[left] * b[right] +
                a[right] * b[left];

            // Check if current product
            // is minimum or not
            if (min >= total1) {
                min = total1;
                first = left;
                second = right;
            }
            --left;
            ++right;
        }
    }

    // Traverse all even length subarrays
    for (let i = 0; i < a.length; ++i) {
        let left = i;
        let right = i + 1;
        let total1 = total;

        while (left >= 0 && right < a.length) {

            // Remove the previous product
            total1 -= a[left] * b[left] +
                a[right] * b[right];

            // Add to the current product
            total1 += a[left] * b[right] +
                a[right] * b[left];

            // Check if current product
            // is minimum or not
            if (min >= total1) {
                min = total1;
                first = left;
                second = right;
            }

            // Update the pointers
            --left;
            ++right;
        }
    }

    // reverse1 the subarray
    if (min < total) {
        reverse1(first, second, a);

        // print1 the subarray
        print1(a, b);
    }
    else {
        print1(a, b);
    }
}

// Driver Code

let n = 4;
let a = [2, 3, 1, 5];
let b = [8, 2, 4, 3];

minimumProdArray(a, b, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
1 3 2 5 
8 2 4 3 
37
```

***时间复杂度:** O(N <sup>2</sup> )。*
***辅助空间:** O(1)*