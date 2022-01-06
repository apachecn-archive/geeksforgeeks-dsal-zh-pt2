# 奇数长度子阵列中奇数索引元素的最小翻转，以使两个给定阵列相等

> 原文:[https://www . geeksforgeeks . org/从奇数长度子数组到两个给定数组的最小奇数索引元素翻转数-相等/](https://www.geeksforgeeks.org/minimum-flips-of-odd-indexed-elements-from-odd-length-subarrays-to-make-two-given-arrays-equal/)

给定两个大小为 **N** 的二进制[阵列](https://www.geeksforgeeks.org/array-data-structure/) **X[]** 和 **Y[]** ，任务是通过选择任意奇数长度的子阵列并从该子阵列翻转所有奇数索引元素的最小操作数，将阵列 **X[]** 转换为阵列 **Y[]** 。

**示例:**

> **输入:** X[] = {1，0，0，0，0，1}，Y[] = {1，1，0，1，1}
> **输出:** 2
> **解释:**
> 最初，X[]是{1，0，0，0，0，1}。
> **操作 1:** 从数组 X[]中选择子数组{0，0，0}，更改第 2 <sup>nd</sup> 和第 4 <sup>th</sup> 字符，将其转换为{1，0，1}。
> 现在 X 变成了{1，1，0，1，0，1}。
> **操作 2:** 选择仅包含第 5 个<sup>T21 字符的子数组{0}，并将其转换为 1。
> 最后 X 变成{1，1，0，1，1，1}，等于 y
> 因此，运算次数为 2。</sup>
> 
> **输入:** X[] = {0，1，0}，Y[] = {0，1，0}
> **输出:** 0
> **解释:**
> 由于数组 X 和 Y 相等，因此最小运算量为 0。

**方法:**想法是分别计算偶数和奇数位置的操作。按照以下步骤解决问题:

*   初始化一个变量 **C** 为 **0** 来存储操作数。
*   [遍历奇数位置的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**【X】**元素，取一个计数器**计数** = 0。
    *   检查 **X[i]** 和 **Y[i]** 之间是否有连续的不等元素，每次将计数器**计数**增加 **1** 。
    *   当 **X[i]** 和 **Y[i]** 相等时，增加一个全局 **C** 使操作增加 1，因为在一个操作中，所有奇数位置可以与 **Y** 相等。
*   同样地，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **X[]** 元素越过偶数位置，再次取一个计数器**计数** = 0。
    *   检查 **X[i]** 和 **Y[i]** 之间是否有连续的不等元素，每次将计数器**计数**增加 **1** 。
    *   当 **X[i]** 和 **Y[i]** 相等时，增加一个全局计数器 **C** ，通过 **1** 增加操作。
*   完成上述步骤后，打印 **C** 的值作为所需操作的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum flip
// of subarrays required at alternate
// index to make binary arrays equals
void minOperation(int X[], int Y[],
                  int n)
{
    // Stores count of total operations
    int C = 0;

    // Stores count of consecutive
    // unequal elements
    int count = 0;

    // Loop to run on odd positions
    for (int i = 1; i < n; i = i + 2) {

        if (X[i] != Y[i]) {
            count++;
        }
        else {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    // If all last elements are equal
    if (count != 0)
        C++;

    count = 0;

    // Loop to run on even positions
    for (int i = 0; i < n; i = i + 2) {

        if (X[i] != Y[i]) {
            count++;
        }
        else {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    if (count != 0)
        C++;

    // Print the minimum operations
    cout << C;
}

// Driver Code
int main()
{
    int X[] = { 1, 0, 0, 0, 0, 1 };
    int Y[] = { 1, 1, 0, 1, 1, 1 };
    int N = sizeof(X) / sizeof(X[0]);

    // Function Call
    minOperation(X, Y, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum flip
// of subarrays required at alternate
// index to make binary arrays equals
static void minOperation(int X[], int Y[],
                         int n)
{

    // Stores count of total operations
    int C = 0;

    // Stores count of consecutive
    // unequal elements
    int count = 0;

    // Loop to run on odd positions
    for(int i = 1; i < n; i = i + 2)
    {

        if (X[i] != Y[i])
        {
            count++;
        }
        else
        {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    // If all last elements are equal
    if (count != 0)
        C++;

    count = 0;

    // Loop to run on even positions
    for(int i = 0; i < n; i = i + 2)
    {
        if (X[i] != Y[i])
        {
            count++;
        }
        else
        {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    if (count != 0)
        C++;

    // Print the minimum operations
    System.out.print(C);
}

// Driver Code
public static void main(String[] args)
{
    int X[] = { 1, 0, 0, 0, 0, 1 };
    int Y[] = { 1, 1, 0, 1, 1, 1 };
    int N = X.length;

    // Function Call
    minOperation(X, Y, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum flip
# of subarrays required at alternate
# index to make binary arrays equals
def minOperation(X, Y, n):

    # Stores count of total operations
    C = 0;

    # Stores count of consecutive
    # unequal elements
    count = 0;

    # Loop to run on odd positions
    for i in range(1, n, 2):

        if (X[i] != Y[i]):
            count += 1;
        else:

            # Incrementing the
            # global counter
            if (count != 0):
                C += 1;

            # Change count to 0
            count = 0;

    # If all last elements are equal
    if (count != 0):
        C += 1;

    count = 0;

    # Loop to run on even positions
    for i in range(0, n, 2):
        if (X[i] != Y[i]):
            count += 1;
        else:

            # Incrementing the
            # global counter
            if (count != 0):
                C += 1;

            # Change count to 0
            count = 0;

    if (count != 0):
        C += 1;

    # Print minimum operations
    print(C);

# Driver Code
if __name__ == '__main__':
    X = [1, 0, 0, 0, 0, 1];
    Y = [1, 1, 0, 1, 1, 1];
    N = len(X);

    # Function Call
    minOperation(X, Y, N);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum flip
// of subarrays required at alternate
// index to make binary arrays equals
static void minOperation(int []X, int []Y,
                         int n)
{

    // Stores count of total operations
    int C = 0;

    // Stores count of consecutive
    // unequal elements
    int count = 0;

    // Loop to run on odd positions
    for(int i = 1; i < n; i = i + 2)
    {
        if (X[i] != Y[i])
        {
            count++;
        }
        else
        {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    // If all last elements are equal
    if (count != 0)
        C++;

    count = 0;

    // Loop to run on even positions
    for(int i = 0; i < n; i = i + 2)
    {
        if (X[i] != Y[i])
        {
            count++;
        }
        else
        {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    if (count != 0)
        C++;

    // Print the minimum operations
    Console.Write(C);
}

// Driver Code
public static void Main(String[] args)
{
    int []X = { 1, 0, 0, 0, 0, 1 };
    int []Y = { 1, 1, 0, 1, 1, 1 };
    int N = X.Length;

    // Function Call
    minOperation(X, Y, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to find the minimum flip
// of subarrays required at alternate
// index to make binary arrays equals
function minOperation(X, Y,
                         n)
{

    // Stores count of total operations
    let C = 0;

    // Stores count of consecutive
    // unequal elements
    let count = 0;

    // Loop to run on odd positions
    for(let i = 1; i < n; i = i + 2)
    {

        if (X[i] != Y[i])
        {
            count++;
        }
        else
        {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    // If all last elements are equal
    if (count != 0)
        C++;

    count = 0;

    // Loop to run on even positions
    for(let i = 0; i < n; i = i + 2)
    {
        if (X[i] != Y[i])
        {
            count++;
        }
        else
        {

            // Incrementing the
            // global counter
            if (count != 0)
                C++;

            // Change count to 0
            count = 0;
        }
    }

    if (count != 0)
        C++;

    // Print the minimum operations
    document.write(C);
}

// Driver code

    let X = [ 1, 0, 0, 0, 0, 1 ];
    let Y = [ 1, 1, 0, 1, 1, 1 ];
    let N = X.length;

    // Function Call
    minOperation(X, Y, N);

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)