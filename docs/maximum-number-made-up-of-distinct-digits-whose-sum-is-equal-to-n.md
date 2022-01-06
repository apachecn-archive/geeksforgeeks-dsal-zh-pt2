# 由不同数字组成的最大数字，其和等于 N

> 原文:[https://www . geesforgeks . org/最大数字-由不同数字组成-其和等于-n/](https://www.geeksforgeeks.org/maximum-number-made-up-of-distinct-digits-whose-sum-is-equal-to-n/)

给定一个正整数 **N** ，任务是找到由不同数字组成的最大正数，其数字的[和等于 **N** 。如果没有，打印**-1”**。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)

**示例:**

> **输入:** N = 25
> **输出:** 98710
> **说明:**
> 数字 98710 是只包含唯一数字的最大数字，其数字之和(9 + 8 + 7 + 1 + 0)为 N(= 25)。
> 
> **输入:** N = 50
> **输出:** -1

**方法:**给定的问题可以基于以下观察来解决:

*   **如果 N 的值至少为 45:** 则需要的结果为 **-1** ，因为使用非重复数字可以做的最大数字是 **9876543210** ，其数字之和为 **45** 。
*   **对于 N 的所有其他值:**要获得最大的数字，从最大的数字开始，即 **9** ，并不断递减，并将其添加到所需的数字中。要求的数字必须在其末尾包含一个 **0** ，因为它增加了数值而不改变数字的总和。

按照以下步骤解决问题:

*   如果给定的数字 **N** 大于 **45** ，则打印**-1”**。
*   否则，请执行以下步骤:
    *   初始化一个变量，说 **num** 为 **0** 存储需要的结果，一个变量，说**数字**，为 **9** 。
    *   [循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)直到 **N** 和**数字**的值为正并执行以下步骤:
        *   如果一个**数字**的值最多为**N**，那么将**数**乘以 **10** ，然后将**数字**的值加到**数**上，将 **N** 的值减去**数字**。
        *   另外，将**数字**的值递减 **1** 。
    *   将变量**数**乘以 **10** ，并在末尾追加数字 **0** 。
*   完成上述步骤后，打印 **num** 的值作为结果数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest positive
// number made up of distinct digits
// having the sum of its digits as N
long largestNumber(int N)
{
    // If given number is greater
    // than 45, print -1
    if (N > 45)
        return -1;

    // Store the required number and
    // the digit to be considered
    int num = 0, digit = 9;

    // Loop until N > 0 and digit > 0
    while (N > 0 && digit > 0) {

        // If the current digit is
        // at most N then, add it
        // to number num
        if (digit <= N) {

            // Update the value of
            // num
            num *= 10;
            num += digit;

            // Decrement N by digit
            N -= digit;
        }

        // Consider the next lower
        // digit
        digit -= 1;
    }

    // Add 0 at the end and return
    // the number num
    return num * 10;
}

// Driver Code
int main()
{
    int N = 25;
    cout << largestNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the largest positive
// number made up of distinct digits
// having the sum of its digits as N
static long largestNumber(int N)
{

    // If given number is greater
    // than 45, print -1
    if (N > 45)
        return -1;

    // Store the required number and
    // the digit to be considered
    int num = 0, digit = 9;

    // Loop until N > 0 and digit > 0
    while (N > 0 && digit > 0)
    {

        // If the current digit is
        // at most N then, add it
        // to number num
        if (digit <= N)
        {

            // Update the value of
            // num
            num *= 10;
            num += digit;

            // Decrement N by digit
            N -= digit;
        }

        // Consider the next lower
        // digit
        digit -= 1;
    }

    // Add 0 at the end and return
    // the number num
    return num * 10;
}

// Driver Code
public static void main (String[] args)
{
    int N = 25;

    System.out.print(largestNumber(N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the largest positive
# number made up of distinct digits
# having the sum of its digits as N
def largestNumber(N):

    # If given number is greater
    # than 45, print -1
    if (N > 45):
        return -1

    # Store the required number and
    # the digit to be considered
    num = 0
    digit = 9

    # Loop until N > 0 and digit > 0
    while (N > 0 and digit > 0):

        # If the current digit is
        # at most N then, add it
        # to number num
        if (digit <= N):

            # Update the value of
            # num
            num *= 10
            num += digit

            # Decrement N by digit
            N -= digit

        # Consider the next lower
        # digit
        digit -= 1

    # Add 0 at the end and return
    # the number num
    return num * 10

# Driver Code
N = 25
print(largestNumber(N))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the largest positive
// number made up of distinct digits
// having the sum of its digits as N
static long largestNumber(int N)
{

    // If given number is greater
    // than 45, print -1
    if (N > 45)
        return -1;

    // Store the required number and
    // the digit to be considered
    int num = 0, digit = 9;

    // Loop until N > 0 and digit > 0
    while (N > 0 && digit > 0)
    {

        // If the current digit is
        // at most N then, add it
        // to number num
        if (digit <= N)
        {

            // Update the value of
            // num
            num *= 10;
            num += digit;

            // Decrement N by digit
            N -= digit;
        }

        // Consider the next lower
        // digit
        digit -= 1;
    }

    // Add 0 at the end and return
    // the number num
    return num * 10;
}

// Driver Code
public static void Main()
{
    int N = 25;

    Console.Write(largestNumber(N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the largest positive
// number made up of distinct digits
// having the sum of its digits as N
function largestNumber(N)
{

    // If given number is greater
    // than 45, print -1
    if (N > 45)
        return -1;

    // Store the required number and
    // the digit to be considered
    let num = 0, digit = 9;

    // Loop until N > 0 and digit > 0
    while (N > 0 && digit > 0)
    {

        // If the current digit is
        // at most N then, add it
        // to number num
        if (digit <= N)
        {

            // Update the value of
            // num
            num *= 10;
            num += digit;

            // Decrement N by digit
            N -= digit;
        }

        // Consider the next lower
        // digit
        digit -= 1;
    }

    // Add 0 at the end and return
    // the number num
    return num * 10;
}

// Driver Code
     let N = 25;

    document.write(largestNumber(N));

</script>
```

**Output:** 

```
98710
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)