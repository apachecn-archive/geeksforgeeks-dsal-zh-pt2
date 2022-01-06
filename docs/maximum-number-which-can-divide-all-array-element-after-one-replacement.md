# 一次替换后可以分割所有数组元素的最大个数

> 原文:[https://www . geeksforgeeks . org/最大值-可对所有数组元素进行一次替换后的除数/](https://www.geeksforgeeks.org/maximum-number-which-can-divide-all-array-element-after-one-replacement/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr** ，用任何其他整数替换数组中的任何一个元素。任务是返回这个数组中所有元素的最大除数。

示例:

> **输入:** arr = [15，9，3]
> **输出:** 3
> **解释:**这里用 3 代替 15，这样数组就变成了 arr = [3，9，3]，现在数组中的所有元素都可以被 3 整除，所以 3 就是我们的答案
> 
> **输入:** arr = [16，5，10，25]
> **输出:** 5

方法:为解决上述问题:

*   [在整数 I 上迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，从零到小于其长度
*   每次，从数组中移除第 I 个元素并[找到最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)并将 **gcd** 存储在变量中
*   如果当前 **gcd** 大于**maxGcd**T6，则更新 **maxGcd**

下面是上述方法的实现:

## C++14

```
// C++ Implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of two numbers
int gcdOfTwoNos(int num1, int num2)
{

    // If one of numbers is 0
    // then gcd is other number
    if (num1 == 0)
        return num2;
    if (num2 == 0)
        return num1;

    // If both are equal
    // then that value is gcd
    if (num1 == num2)
        return num1;

    // One is greater
    if (num1 > num2)
        return gcdOfTwoNos(num1 - num2, num2);
    return gcdOfTwoNos(num1, num2 - num1);
}

// Function to return minimum sum
int Min_sum(int arr[], int N)
{
    // Initialize min_sum with large value
    int min_sum = 1000000, maxGcd = 1;
    for (int i = 0; i < N; i++) {

        // Initialize variable gcd
        int gcd;
        if (i == 0)
            gcd = arr[1];
        else {
            gcd = arr[i - 1];
        }
        for (int j = 0; j < N; j++) {
            if (j != i)
                gcd = gcdOfTwoNos(gcd, arr[j]);
        }

        // Storing value of arr[i] in c
        int c = arr[i];

        // Update maxGcd if gcd is greater
        // than maxGcd
        if (gcd > maxGcd)
            maxGcd = gcd;
    }

    // returning the maximum divisor
    // of all elements
    return maxGcd;
}
// Driver code
int main()
{
    int arr[] = { 16, 5, 10, 25 };
    int N = sizeof(arr) / sizeof(int);
    cout << Min_sum(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to return gcd of two numbers
static int gcdOfTwoNos(int num1, int num2)
{

    // If one of numbers is 0
    // then gcd is other number
    if (num1 == 0)
        return num2;
    if (num2 == 0)
        return num1;

    // If both are equal
    // then that value is gcd
    if (num1 == num2)
        return num1;

    // One is greater
    if (num1 > num2)
        return gcdOfTwoNos(num1 - num2, num2);
    return gcdOfTwoNos(num1, num2 - num1);
}

// Function to return minimum sum
static int Min_sum(int arr[], int N)
{
    // Initialize min_sum with large value
    int min_sum = 1000000, maxGcd = 1;
    for (int i = 0; i < N; i++) {

        // Initialize variable gcd
        int gcd;
        if (i == 0)
            gcd = arr[1];
        else {
            gcd = arr[i - 1];
        }
        for (int j = 0; j < N; j++) {
            if (j != i)
                gcd = gcdOfTwoNos(gcd, arr[j]);
        }

        // Storing value of arr[i] in c
        int c = arr[i];

        // Update maxGcd if gcd is greater
        // than maxGcd
        if (gcd > maxGcd)
            maxGcd = gcd;
    }

    // returning the maximum divisor
    // of all elements
    return maxGcd;
}

// Driver code
    public static void main (String[] args) {
      int arr[] = { 16, 5, 10, 25 };
      int N = arr.length;

        System.out.println( Min_sum(arr, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 Implementation for the above approach

# Function to return gcd1 of two numbers
def gcd1OfTwoNos(num1, num2):
    # If one of numbers is 0
    # then gcd1 is other number
    if (num1 == 0):
        return num2
    if (num2 == 0):
        return num1

    # If both are equal
    # then that value is gcd1
    if (num1 == num2):
        return num1

    # One is greater
    if (num1 > num2):
        return gcd1OfTwoNos(num1 - num2, num2)
    return gcd1OfTwoNos(num1, num2 - num1)

# Function to return minimum sum
def Min_sum(arr, N):
    # Initialize min_sum with large value
    min_sum = 1000000
    maxgcd1 = 1
    for i in range(N):
        # Initialize variable gcd1
        gcd1 = 1
        if (i == 0):
            gcd1 = arr[1]
        else:
            gcd1 = arr[i - 1]
        for j in range(N):
            if (j != i):
                gcd1 = gcd1OfTwoNos(gcd1, arr[j])

        # Storing value of arr[i] in c
        c = arr[i]

        # Update maxgcd1 if gcd1 is greater
        # than maxgcd1
        if (gcd1 > maxgcd1):
            maxgcd1 = gcd1

    # returning the maximum divisor
    # of all elements
    return maxgcd1

# Driver code
if __name__ == '__main__':
    arr = [16, 5, 10, 25]
    N = len(arr)
    print(Min_sum(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach

using System;

public class GFG
{

  // Function to return gcd of two numbers
static int gcdOfTwoNos(int num1, int num2)
{

    // If one of numbers is 0
    // then gcd is other number
    if (num1 == 0)
        return num2;
    if (num2 == 0)
        return num1;

    // If both are equal
    // then that value is gcd
    if (num1 == num2)
        return num1;

    // One is greater
    if (num1 > num2)
        return gcdOfTwoNos(num1 - num2, num2);
    return gcdOfTwoNos(num1, num2 - num1);
}

// Function to return minimum sum
static int Min_sum(int []arr, int N)
{
    // Initialize min_sum with large value
    int min_sum = 1000000, maxGcd = 1;
    for (int i = 0; i < N; i++) {

        // Initialize variable gcd
        int gcd;
        if (i == 0)
            gcd = arr[1];
        else {
            gcd = arr[i - 1];
        }
        for (int j = 0; j < N; j++) {
            if (j != i)
                gcd = gcdOfTwoNos(gcd, arr[j]);
        }

        // Update maxGcd if gcd is greater
        // than maxGcd
        if (gcd > maxGcd)
            maxGcd = gcd;
    }

    // returning the maximum divisor
    // of all elements
    return maxGcd;
}

// Driver code
    public static void Main (string[] args) {
      int []arr = { 16, 5, 10, 25 };
      int N = arr.Length;

        Console.WriteLine(Min_sum(arr, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
  <script>
        // JavaScript Program to implement
        // the above approach

  // Function to return gcd of two numbers
function gcdOfTwoNos(num1, num2)
{

    // If one of numbers is 0
    // then gcd is other number
    if (num1 == 0)
        return num2;
    if (num2 == 0)
        return num1;

    // If both are equal
    // then that value is gcd
    if (num1 == num2)
        return num1;

    // One is greater
    if (num1 > num2)
        return gcdOfTwoNos(num1 - num2, num2);
    return gcdOfTwoNos(num1, num2 - num1);
}

// Function to return minimum sum
function Min_sum(arr, N)
{
    // Initialize min_sum with large value
    let min_sum = 1000000, maxGcd = 1;
    for (let i = 0; i < N; i++) {

        // Initialize variable gcd
        let gcd;
        if (i == 0)
            gcd = arr[1];
        else {
            gcd = arr[i - 1];
        }
        for (let j = 0; j < N; j++) {
            if (j != i)
                gcd = gcdOfTwoNos(gcd, arr[j]);
        }

        // Storing value of arr[i] in c
        let c = arr[i];

        // Update maxGcd if gcd is greater
        // than maxGcd
        if (gcd > maxGcd)
            maxGcd = gcd;
    }

    // returning the maximum divisor
    // of all elements
    return maxGcd;
}

 // Driver Code

      let arr = [ 16, 5, 10, 25 ];
      let N = arr.length;

      document.write( Min_sum(arr, N));

// This code is contributed by sanjoy_62.
    </script>
```

**Output:** 

```
5
```

**时间复杂度:** O((N^2) * Log(M))，其中 m 为数组
中的最小值**辅助空间:** O(1)