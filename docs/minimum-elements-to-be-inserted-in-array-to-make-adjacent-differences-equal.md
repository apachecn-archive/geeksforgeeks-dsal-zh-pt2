# 要插入数组中的最小元素，以使相邻的差异相等

> 原文:[https://www . geesforgeks . org/待插入数组中的最小元素使相邻差相等/](https://www.geeksforgeeks.org/minimum-elements-to-be-inserted-in-array-to-make-adjacent-differences-equal/)

给定整数数组 **Arr[]** 。数组的元素按升序排序。任务是找到要插入数组中的最小元素数，以便任意两个连续元素之间的差异相同。

**示例:**

> **输入:** Arr[] = {1，4，13，19，25}
> **输出:** 4
> **解释:**
> 一种可能的解决方案是:Arr[] = {1，4，7，10，13，16，19，22，25}。这里所有连续的元素相差 3，为此插入了 4 个元素。
> 
> **输入:** Arr[] = {1，5，8，10，12，16 }；
> **输出:** 10
> **说明:**
> 需要插入 10 个元素才能使差异相等。

**方法:**想法是计算所有连续元素之间的**差异**。数组中有 **N** 元素，所以会有**N–1**这样的区别。

*   求所有这些差的 [GCD(最大公约数)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。这个 GCD 将是插入新元素后数组中任意两个连续元素之间的差值。
*   假设第一个元素和第二个元素的区别是 **diff** 。将答案初始化为 0，并在答案中添加**((diff/GCD)–1)**，因为需要**(diff/GCD–1)**元素来使差异等于 **GCD** 。
*   对给定数组的所有连续元素执行相同的操作，并将其添加到答案中，以找到要插入的最小元素数，从而使数组的任意两个连续元素之间的差异相等。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find gcd of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to calculate minimum
// numbers to be inserted to make
// equal differences between
// two consecutive elements
int minimum_elements(int n, int arr[])
{
    // Check if there is only one
    // element in the array
    // then answer will be 0
    if (n < 3)
        return 0;

    int g, ans = 0, diff, cnt;

    // Calculate difference
    // between first and second
    // element of array
    diff = arr[1] - arr[0];

    // If there is only two elements
    // in the array then gcd of
    // differences of consecutive
    // elements of array will be
    // equal to difference of first
    // and second element of the array
    g = diff;

    // Loop to calculate the gcd
    // of the differences between
    // consecutive elements of the array
    for (int i = 2; i < n; i++) {
        diff = arr[i] - arr[i - 1];

        g = gcd(g, diff);
    }

    // Loop to calculate the
    // elements to be inserted
    for (int i = 1; i < n; i++) {
        diff = arr[i] - arr[i - 1];

        cnt = diff / g;

        ans += (cnt - 1);
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 8, 10, 12, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minimum_elements(n, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to calculate minimum
// numbers to be inserted to make
// equal differences between
// two consecutive elements
static int minimum_elements(int n, int arr[])
{

    // Check if there is only one
    // element in the array
    // then answer will be 0
    if (n < 3)
        return 0;

    int g, ans = 0, diff, cnt;

    // Calculate difference
    // between first and second
    // element of array
    diff = arr[1] - arr[0];

    // If there is only two elements
    // in the array then gcd of
    // differences of consecutive
    // elements of array will be
    // equal to difference of first
    // and second element of the array
    g = diff;

    // Loop to calculate the gcd
    // of the differences between
    // consecutive elements of the array
    for(int i = 2; i < n; i++)
    {
        diff = arr[i] - arr[i - 1];
        g = gcd(g, diff);
    }

    // Loop to calculate the
    // elements to be inserted
    for(int i = 1; i < n; i++)
    {
        diff = arr[i] - arr[i - 1];
        cnt = diff / g;
        ans += (cnt - 1);
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 5, 8, 10, 12, 16 };
    int n = arr.length;

    System.out.println(minimum_elements(n, arr));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find gcd of two numbers
def gcd(a, b):

    if (b == 0):
        return a

    return gcd(b, a % b)

# Function to calculate minimum
# numbers to be inserted to make
# equal differences between
# two consecutive elements
def minimum_elements(n, arr):

    # Check if there is only one
    # element in the array
    # then answer will be 0
    if (n < 3):
        return 0

    ans = 0

    # Calculate difference
    # between first and second
    # element of array
    diff = arr[1] - arr[0]

    # If there is only two elements
    # in the array then gcd of
    # differences of consecutive
    # elements of array will be
    # equal to difference of first
    # and second element of the array
    g = diff

    # Loop to calculate the gcd
    # of the differences between
    # consecutive elements of the array
    for i in range(2, n):
        diff = arr[i] - arr[i - 1]

        g = gcd(g, diff)

    # Loop to calculate the
    # elements to be inserted
    for i in range(1, n):
        diff = arr[i] - arr[i - 1]
        cnt = diff // g
        ans += (cnt - 1)

    # Return the answer
    return ans

# Driver code
arr = [ 1, 5, 8, 10, 12, 16 ]
n = len(arr)

print(minimum_elements(n, arr))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to calculate minimum
// numbers to be inserted to make
// equal differences between
// two consecutive elements
static int minimum_elements(int n, int[] arr)
{

    // Check if there is only one
    // element in the array
    // then answer will be 0
    if (n < 3)
        return 0;

    int g, ans = 0, diff, cnt;

    // Calculate difference
    // between first and second
    // element of array
    diff = arr[1] - arr[0];

    // If there is only two elements
    // in the array then gcd of
    // differences of consecutive
    // elements of array will be
    // equal to difference of first
    // and second element of the array
    g = diff;

    // Loop to calculate the gcd
    // of the differences between
    // consecutive elements of the array
    for(int i = 2; i < n; i++)
    {
        diff = arr[i] - arr[i - 1];
        g = gcd(g, diff);
    }

    // Loop to calculate the
    // elements to be inserted
    for(int i = 1; i < n; i++)
    {
        diff = arr[i] - arr[i - 1];
        cnt = diff / g;
        ans += (cnt - 1);
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main ()
{
    int[] arr = { 1, 5, 8, 10, 12, 16 };
    int n = arr.Length;

    Console.WriteLine(minimum_elements(n, arr));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find gcd of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to calculate minimum
// numbers to be inserted to make
// equal differences between
// two consecutive elements
function minimum_elements(n, arr)
{
    // Check if there is only one
    // element in the array
    // then answer will be 0
    if (n < 3)
        return 0;

    let g, ans = 0, diff, cnt;

    // Calculate difference
    // between first and second
    // element of array
    diff = arr[1] - arr[0];

    // If there is only two elements
    // in the array then gcd of
    // differences of consecutive
    // elements of array will be
    // equal to difference of first
    // and second element of the array
    g = diff;

    // Loop to calculate the gcd
    // of the differences between
    // consecutive elements of the array
    for (let i = 2; i < n; i++) {
        diff = arr[i] - arr[i - 1];

        g = gcd(g, diff);
    }

    // Loop to calculate the
    // elements to be inserted
    for (let i = 1; i < n; i++) {
        diff = arr[i] - arr[i - 1];

        cnt = parseInt(diff / g);

        ans += (cnt - 1);
    }

    // Return the answer
    return ans;
}

// Driver code
    let arr = [ 1, 5, 8, 10, 12, 16 ];
    let n = arr.length;

    document.write(minimum_elements(n, arr));

</script>
```

**Output:** 

```
10
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(1)