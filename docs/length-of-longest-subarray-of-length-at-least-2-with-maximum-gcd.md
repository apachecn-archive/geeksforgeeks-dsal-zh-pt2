# 长度至少为 2 的最长子阵列的长度，最大 GCD

> 原文:[https://www . geeksforgeeks . org/最长长度子阵列最大长度至少 2/gcd/](https://www.geeksforgeeks.org/length-of-longest-subarray-of-length-at-least-2-with-maximum-gcd/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到长度至少为 2 的最长子数组[长度以及最大可能的](https://www.geeksforgeeks.org/length-largest-subarray-contiguous-elements-set-1/) [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 值。
**举例:**

> **输入:** arr[] = {1，2，2}
> **输出:** 2
> **解释:**
> 尺寸大于 2 的可能子阵列，并且存在 GCD 的有:
> 1) {1，2} - > 1
> 2) {2，2} - > 2
> 3) {1，2，3} - > 1
> 这里，最大 GCD 值为 2 和
> 因此答案是{2，2}。
> **输入:** arr[] = {18，3，6，9}
> **输出:** 4
> **解释:**
> 这里，最大 GCD 值为 3，GCD = 3 的最长子数组为{18，3，6，9}。
> 因此答案是{18，3，6，9}。

**天真方法:**想法是[生成所有可能的大小至少为 2 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并分别找到其中每个子阵列的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。那么，具有最大 GCD 值的子阵列的长度就是所需的长度。
***时间复杂度:**O(N<sup>2</sup>)*
**高效途径:**

1.  使用[这篇](https://www.geeksforgeeks.org/maximum-gcd-of-all-subarrays-of-length-at-least-2/)文章中讨论的方法，找到长度至少为 2 的所有子阵列的最大 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) (比如 **g** )。
2.  遍历给定数组并[计算可被 **GCD g** 整除的连续元素的最大数量](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find maximum size subarray
// having maximum GCD
int maximumGcdSubarray(int arr[], int n)
{
    // Base Case
    if (n == 1)
        return 0;

    // Let the maximum GCD be 1 initially
    int k = 1;

    // Loop thourgh array to find maximum
    // GCD of subarray with size 2
    for (int i = 1; i < n; ++i) {
        k = max(k, gcd(arr[i], arr[i - 1]));
    }

    int cnt = 0;
    int maxLength = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Is a multiple of k, increase cnt
        if (arr[i] % k == 0) {
            cnt++;
        }

        // Else update maximum length with
        // consecutive element divisible by k
        // Set cnt to 0
        else {
            maxLength = max(maxLength, cnt);
            cnt = 0;
        }
    }

    // Update the maxLength
    maxLength = max(maxLength, cnt);

    // Return the maxLength
    return maxLength;
}

// Driver Code
int main()
{
    int arr[] = { 18, 3, 6, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << maximumGcdSubarray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate GCD of
// two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find maximum size 
// subarray having maximum GCD
static int maximumGcdSubarray(int arr[], int n)
{

    // Base case
    if (n == 1)
        return 0;

    // Let the maximum GCD be 1 initially
    int k = 1;

    // Loop through array to find maximum
    // GCD of subarray with size 2
    for(int i = 1; i < n; i++)
    {
       k = Math.max(k, gcd(arr[i], arr[i - 1]));
    }

    int cnt = 0;
    int maxLength = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

       // Is a multiple of k, increase cnt
       if(arr[i] % k == 0)
       {
           cnt++;
       }

       // Else update maximum length with
       // consecutive element divisible by k
       // Set cnt to 0
       else
       {
           maxLength = Math.max(maxLength, cnt);
           cnt = 0;
       }
    }

    // Update the maxLength
    maxLength = Math.max(maxLength, cnt);

    // Return the maxLength
    return maxLength;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 18, 3, 6, 9 };
    int n = arr.length;

    // Function call
    System.out.println(maximumGcdSubarray(arr, n));
}
}

// This code is contributed by stutipathak31jan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate GCD of
# two numbers
def gcd(a, b):

    if b == 0:
        return a
    return gcd(b, a % b)

# Function to find maximum size
# subarray having maximum GCD
def maxGcdSubarray(arr, n):

    # Base case
    if n == 1:
        return 0

    # Let the maximum GCD be 1 initially
    k = 1

    # Loop through array to find maximum
    # GCD of subarray with size 2
    for i in range(1, n):
        k = max(k, gcd(arr[i], arr[i - 1]))

    cnt = 0
    maxLength = 0

    # Traverse the array
    for i in range(n):

        # Is a multiple of k, increase cnt
        if arr[i] % k == 0:
            cnt += 1

        # Else update maximum length with
        # consecutive element divisible by k
        # Set cnt to 0
        else:
            maxLength = max(maxLength, cnt)
            cnt = 0

    # Update the maxLength
    maxLength = max(maxLength, cnt)

    # Return the maxLength
    return maxLength

# Driver Code
arr = [ 18, 3, 6, 9 ]
n = len(arr)

# Function call
print(maxGcdSubarray(arr, n))

# This code is contributed by stutipathak31jan
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate GCD of
// two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find maximum size
// subarray having maximum GCD
static int maximumGcdSubarray(int[] arr, int n)
{

    // Base case
    if (n == 1)
        return 0;

    // Let the maximum GCD be 1 initially
    int k = 1;

    // Loop through array to find maximum
    // GCD of subarray with size 2
    for(int i = 1; i < n; i++)
    {
        k = Math.Max(k, gcd(arr[i], arr[i - 1]));
    }

    int cnt = 0;
    int maxLength = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Is a multiple of k, increase cnt
        if(arr[i] % k == 0)
        {
            cnt++;
        }

        // Else update maximum length with
        // consecutive element divisible by k
        // Set cnt to 0
        else
        {
            maxLength = Math.Max(maxLength, cnt);
            cnt = 0;
        }
    }

    // Update the maxLength
    maxLength = Math.Max(maxLength, cnt);

    // Return the maxLength
    return maxLength;
}

// Driver code   
static void Main()
{
    int[] arr = { 18, 3, 6, 9 };
    int n = arr.Length;

    // Function call
    Console.WriteLine(maximumGcdSubarray(arr, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate GCD of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find maximum size subarray
// having maximum GCD
function maximumGcdSubarray(arr, n)
{
    // Base Case
    if (n == 1)
        return 0;

    // Let the maximum GCD be 1 initially
    let k = 1;

    // Loop thourgh array to find maximum
    // GCD of subarray with size 2
    for (let i = 1; i < n; ++i) {
        k = Math.max(k, gcd(arr[i], arr[i - 1]));
    }

    let cnt = 0;
    let maxLength = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // Is a multiple of k, increase cnt
        if (arr[i] % k == 0) {
            cnt++;
        }

        // Else update maximum length with
        // consecutive element divisible by k
        // Set cnt to 0
        else {
            maxLength = Math.max(maxLength, cnt);
            cnt = 0;
        }
    }

    // Update the maxLength
    maxLength = Math.max(maxLength, cnt);

    // Return the maxLength
    return maxLength;
}

// Driver Code

    let arr = [ 18, 3, 6, 9 ];
    let n = arr.length;

    // Function Call
    document.write(maximumGcdSubarray(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。

***辅助空间:** O(log(max(a，b)))*