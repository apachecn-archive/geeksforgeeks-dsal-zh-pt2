# 在一个数字的二进制表示中找到长度为> = n 的连续 1

> 原文:[https://www . geeksforgeeks . org/find-长度为 1 的 n 进制数字表示法/](https://www.geeksforgeeks.org/find-consecutive-1s-of-length-n-in-binary-representation-of-a-number/)

给定两个整数 *x* 和 *n* ，任务是搜索长度大于或等于 *n* 的第一个连续的 1 流(在 *x 的* 32 位二进制表示中)，并返回其位置。如果不存在这样的字符串，则返回-1。
**举例:**

> **输入:** x = 35，n = 2
> **输出:**31
> 35 的二进制表示为 0000000000000000000000000010000011，在位置 31 存在两个连续的 1。
> **输入:** x = 32，n = 3
> **输出:**-1
> 32 = 000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

**方法:**使用按位运算计算数字中前导零的数量，然后使用它找到我们需要开始搜索连续 1 的位置。跳过搜索前导零。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the
// number of leading zeros
int countLeadingZeros(int x)
{
    unsigned y;
    int n;
    n = 32;
    y = x >> 16;
    if (y != 0) {
        n = n - 16;
        x = y;
    }
    y = x >> 8;
    if (y != 0) {
        n = n - 8;
        x = y;
    }
    y = x >> 4;
    if (y != 0) {
        n = n - 4;
        x = y;
    }
    y = x >> 2;
    if (y != 0) {
        n = n - 2;
        x = y;
    }
    y = x >> 1;
    if (y != 0)
        return n - 2;
    return n - x;
}

// Function to find the string
// of n consecutive 1's
int FindStringof1s(unsigned x, int n)
{
    int k, p;

    // Initialize position to return.
    p = 0;
    while (x != 0) {

        // Skip leading 0's
        k = countLeadingZeros(x);
        x = x << k;

        // Set position after leading 0's
        p = p + k;

        // Count first group of 1's.
        k = countLeadingZeros(~x);

        // If length of consecutive 1's
        // is greater than or equal to n
        if (k >= n)
            return p + 1;

        // Not enough 1's
        // skip over to next group
        x = x << k;

        // Update the position
        p = p + k;
    }

    // if no string is found
    return -1;
}

// Driver code
int main()
{
    int x = 35;
    int n = 2;
    cout << FindStringof1s(x, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  implementation of above approach

import java.io.*;

class GFG {
// Function to count the
// number of leading zeros
static int countLeadingZeros(int x)
{
    int y;
    int n;
    n = 32;
    y = x >> 16;
    if (y != 0) {
        n = n - 16;
        x = y;
    }
    y = x >> 8;
    if (y != 0) {
        n = n - 8;
        x = y;
    }
    y = x >> 4;
    if (y != 0) {
        n = n - 4;
        x = y;
    }
    y = x >> 2;
    if (y != 0) {
        n = n - 2;
        x = y;
    }
    y = x >> 1;
    if (y != 0)
        return n - 2;
    return n - x;
}

// Function to find the string
// of n consecutive 1's
static int FindStringof1s(int x, int n)
{
    int k, p;

    // Initialize position to return.
    p = 0;
    while (x != 0) {

        // Skip leading 0's
        k = countLeadingZeros(x);
        x = x << k;

        // Set position after leading 0's
        p = p + k;

        // Count first group of 1's.
        k = countLeadingZeros(~x);

        // If length of consecutive 1's
        // is greater than or equal to n
        if (k >= n)
            return p + 1;

        // Not enough 1's
        // skip over to next group
        x = x << k;

        // Update the position
        p = p + k;
    }

    // if no string is found
    return -1;
}

// Driver code

    public static void main (String[] args) {

    int x = 35;
    int n = 2;
    System.out.println(FindStringof1s(x, n));
    }
}
```

## C#

```
// C# implementation of above approach

using System;

public class GFG{

// Function to count the
// number of leading zeros
static int countLeadingZeros(int x)
{
    int y;
    int n;
    n = 32;
    y = x >> 16;
    if (y != 0) {
        n = n - 16;
        x = y;
    }
    y = x >> 8;
    if (y != 0) {
        n = n - 8;
        x = y;
    }
    y = x >> 4;
    if (y != 0) {
        n = n - 4;
        x = y;
    }
    y = x >> 2;
    if (y != 0) {
        n = n - 2;
        x = y;
    }
    y = x >> 1;
    if (y != 0)
        return n - 2;
    return n - x;
}

// Function to find the string
// of n consecutive 1's
static int FindStringof1s(int  x, int n)
{
    int k, p;

    // Initialize position to return.
    p = 0;
    while (x != 0) {

        // Skip leading 0's
        k = countLeadingZeros(x);
        x = x << k;

        // Set position after leading 0's
        p = p + k;

        // Count first group of 1's.
        k = countLeadingZeros(~x);

        // If length of consecutive 1's
        // is greater than or equal to n
        if (k >= n)
            return p + 1;

        // Not enough 1's
        // skip over to next group
        x = x << k;

        // Update the position
        p = p + k;
    }

    // if no string is found
    return -1;
}

// Driver code

    static public void Main (){
    int x = 35;
    int n = 2;
    Console.WriteLine (FindStringof1s(x, n));
    }
}
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to count the
// number of leading zeros
function countLeadingZeros(x) {
    let y;
    let n;
    n = 32;
    y = x >> 16;
    if (y != 0) {
        n = n - 16;
        x = y;
    }
    y = x >> 8;
    if (y != 0) {
        n = n - 8;
        x = y;
    }
    y = x >> 4;
    if (y != 0) {
        n = n - 4;
        x = y;
    }
    y = x >> 2;
    if (y != 0) {
        n = n - 2;
        x = y;
    }
    y = x >> 1;
    if (y != 0)
        return n - 2;
    return n - x;
}

// Function to find the string
// of n consecutive 1's
function FindStringof1s(x, n) {
    let k, p;

    // Initialize position to return.
    p = 0;
    while (x != 0) {

        // Skip leading 0's
        k = countLeadingZeros(x);
        x = x << k;

        // Set position after leading 0's
        p = p + k;

        // Count first group of 1's.
        k = countLeadingZeros(~x);

        // If length of consecutive 1's
        // is greater than or equal to n
        if (k >= n)
            return p + 1;

        // Not enough 1's
        // skip over to next group
        x = x << k;

        // Update the position
        p = p + k;
    }

    // if no string is found
    return -1;
}

// Driver code
let x = 35;
let n = 2;
document.write(FindStringof1s(x, n));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
31
```