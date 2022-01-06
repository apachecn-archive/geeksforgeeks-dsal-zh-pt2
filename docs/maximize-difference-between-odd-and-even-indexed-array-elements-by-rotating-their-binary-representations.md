# 通过旋转奇数和偶数索引数组元素的二进制表示来最大化它们之间的差异

> 原文:[https://www . geeksforgeeks . org/通过旋转它们的二进制表示来最大化奇数和偶数索引数组元素之间的差异/](https://www.geeksforgeeks.org/maximize-difference-between-odd-and-even-indexed-array-elements-by-rotating-their-binary-representations/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过将数组元素的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)旋转任意多次，找到位于偶数索引处的数组元素的[和位于奇数索引处的数组元素的](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)之间的最大绝对差。仅考虑 **8 位**表示。

**示例:**

> **输入:** arr[] = {123，86，234，189}
> **输出:** 326
> **解释:**
> 以下是元素的旋转:
> 
> 1.  ***为 arr[0](= 123):**arr[0]=(123)<sub>10</sub>=(1111011)<sub>2</sub>。向右旋转钻头两次，使 arr[0]=(11111100)<sub>2</sub>=(246)<sub>10</sub>。*
> 2.  ***为 arr[1](= 86):**arr[1]=(86)<sub>10</sub>=(1010110)<sub>2</sub>。向右旋转钻头一次，使 arr[1]=(0101011)<sub>2</sub>=(43)<sub>10</sub>。*
> 3.  ***为元素 arr[3](= 189):**arr[3]=(189)<sub>10</sub>=(10111101)<sub>2</sub>。向左旋转钻头一次，使 arr[3]=(011111011)<sub>2</sub>=(111)<sub>10</sub>。*
> 
> *因此，数组 arr[]修改为{246，43，234，111}。最大绝对差值=(246+234)–(43+111)= 326。*
> 
> **输入:** arr[] = {211，122，212，222}，N = 4
> **输出:** 376

**方法:**通过旋转每个数组元素的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)并找到最大差值，可以通过最小化偶数或奇数索引处的元素和最大化其他索引处的元素来解决给定的问题。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)说**旋转(X，f)** 在旋转任意数的二进制表示中的位后，找到一个数可能的最大值和最小值。
    *   初始化两个变量，比如 **maxi = X** 和 **mini = X** 来存储数字 **X** 的最大值和最小值。
    *   迭代数字 **X** 的位，然后通过执行以下操作旋转 **X** 的位:
        *   [如果 **X** 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则更新 **X** 的值为**X>T11】1**和 **X = X | (1 < < 7)** 。
        *   否则，将 **X** 的值更新为**X>T5】1**。
    *   将 **maxi** 的值更新为 **maxi** 和 **X** 的最大值。
    *   将 **mini** 的值更新为 **mini** 和 **X** 的最小值。
    *   如果 **f** 的值为 **1** ，则返回 **maxi** 。否则，返回 **mini。**
*   现在，找出通过最大化放置在偶数索引处的元素和最小化放置在奇数索引处的元素而获得的差异，并将该差异存储在变量中，比如**案例一**。
*   现在，找出通过最小化放置在偶数索引处的元素和最大化放置在奇数索引处的元素获得的差异，并将该差异存储在变量中，比如**情况二**。
*   完成以上步骤后，打印最大**案例一**和**案例二**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum and
// minimum value of a number that
// can be obtained by rotating bits
int Rotate(int n, int f)
{

    // Stores the value of N
    int temp = n;

    // Stores the maximum value
    int maxi = n;

    // Stores the minimum value
    int mini = n;

    for (int idx = 0; idx < 7; idx++) {

        // If temp is odd
        if (temp & 1) {
            temp >>= 1;
            temp += pow(2, 7);
        }

        else
            temp >>= 1;

        // Update the maximum
        // and the minimum value
        mini = min(mini, temp);
        maxi = max(maxi, temp);
    }

    // If flag is 1, then
    // return the maximum value
    if (f)
        return (maxi);

    // Otherwise, return
    // the maximum value
    else
        return (mini);
}

// Function to find the maximum difference
// between the sum of odd and even-indexed
// array elements possible by rotating bits
int calcMinDiff(int arr[], int n)
{

    // Stores the maximum difference
    int caseOne = 0;

    // Stores the sum of elements
    // present at odd indices
    int sumOfodd = 0;

    // Stores the sum of elements
    // present at even indices
    int sumOfeven = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If the index is even
        if (i % 2)
            sumOfodd += Rotate(arr[i], 0);
        else
            sumOfeven += Rotate(arr[i], 1);
    }

    // Update the caseOne
    caseOne = abs(sumOfodd - sumOfeven);

    // Stores the maximum difference
    int caseTwo = 0;

    // Stores the sum of elements
    // placed at odd positions
    sumOfodd = 0;

    // Stores the sum of elements
    // placed at even positions
    sumOfeven = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // If the index is even
        if (i % 2)
            sumOfodd += Rotate(arr[i], 1);
        else
            sumOfeven += Rotate(arr[i], 0);
    }

    // Update the caseTwo
    caseTwo = abs(sumOfodd - sumOfeven);

    // Return the maximum of caseOne
    // and caseTwo
    return max(caseOne, caseTwo);
}

// Driver Code
int main()
{
    int arr[] = { 123, 86, 234, 189 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << (calcMinDiff(arr, n));
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find maximum and
// minimum value of a number that
// can be obtained by rotating bits
static int Rotate(int n, int f)
{

    // Stores the value of N
    int temp = n;

    // Stores the maximum value
    int maxi = n;

    // Stores the minimum value
    int mini = n;

    for (int idx = 0; idx < 7; idx++) {

        // If temp is odd
        if (temp %2 == 1) {
            temp >>= 1;
            temp += Math.pow(2, 7);
        }

        else
            temp >>= 1;

        // Update the maximum
        // and the minimum value
        mini = Math.min(mini, temp);
        maxi = Math.max(maxi, temp);
    }

    // If flag is 1, then
    // return the maximum value
    if (f==1)
        return (maxi);

    // Otherwise, return
    // the maximum value
    else
        return (mini);
}

// Function to find the maximum difference
// between the sum of odd and even-indexed
// array elements possible by rotating bits
static int calcMinDiff(int arr[], int n)
{

    // Stores the maximum difference
    int caseOne = 0;

    // Stores the sum of elements
    // present at odd indices
    int sumOfodd = 0;

    // Stores the sum of elements
    // present at even indices
    int sumOfeven = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If the index is even
        if (i % 2==0)
            sumOfodd += Rotate(arr[i], 0);
        else
            sumOfeven += Rotate(arr[i], 1);
    }

    // Update the caseOne
    caseOne = Math.abs(sumOfodd - sumOfeven);

    // Stores the maximum difference
    int caseTwo = 0;

    // Stores the sum of elements
    // placed at odd positions
    sumOfodd = 0;

    // Stores the sum of elements
    // placed at even positions
    sumOfeven = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // If the index is even
        if (i % 2==0)
            sumOfodd += Rotate(arr[i], 1);
        else
            sumOfeven += Rotate(arr[i], 0);
    }

    // Update the caseTwo
    caseTwo = Math.abs(sumOfodd - sumOfeven);

    // Return the maximum of caseOne
    // and caseTwo
    return Math.max(caseOne, caseTwo);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 123, 86, 234, 189 };
    int n = arr.length;
    System.out.print((calcMinDiff(arr, n)));
}
}

// This code contributed by umadevi9616.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find maximum and
# minimum value of a number that
# can be obtained by rotating bits
def Rotate(n, f):

    # Stores the value of N
    temp = n

    # Stores the maximum value
    maxi = n

    # Stores the minimum value
    mini = n

    for idx in range(7):

        # If temp is odd
        if temp & 1:
            temp >>= 1
            temp += 2**7

        else:
            temp >>= 1

        # Update the maximum
        # and the minimum value
        mini = min(mini, temp)
        maxi = max(maxi, temp)

    # If flag is 1, then
    # return the maximum value
    if(f):
        return (maxi)

    # Otherwise, return
    # the maximum value
    else:
        return (mini)

# Function to find the maximum difference
# between the sum of odd and even-indexed
# array elements possible by rotating bits
def calcMinDiff(arr):

    # Stores the maximum difference
    caseOne = 0

    # Stores the sum of elements
    # present at odd indices
    sumOfodd = 0

    # Stores the sum of elements
    # present at even indices
    sumOfeven = 0

    # Traverse the given array
    for i in range(len(arr)):

        # If the index is even
        if i % 2:
            sumOfodd += Rotate(arr[i], 0)
        else:
            sumOfeven += Rotate(arr[i], 1)

    # Update the caseOne
    caseOne = abs(sumOfodd - sumOfeven)

    # Stores the maximum difference
    caseTwo = 0

    # Stores the sum of elements
    # placed at odd positions
    sumOfodd = 0

    # Stores the sum of elements
    # placed at even positions
    sumOfeven = 0

    # Traverse the array
    for i in range(len(arr)):

        # If the index is even
        if i % 2:
            sumOfodd += Rotate(arr[i], 1)
        else:
            sumOfeven += Rotate(arr[i], 0)

    # Update the caseTwo
    caseTwo = abs(sumOfodd - sumOfeven)

    # Return the maximum of caseOne
    # and caseTwo
    return max(caseOne, caseTwo)

# Driver Code

arr = [123, 86, 234, 189]
print(calcMinDiff(arr))
```

## C#

```
// C# program for the above approach

using System;

public class GFG {

// Function to find maximum and
// minimum value of a number that
// can be obtained by rotating bits
static int Rotate(int n, int f)
{

    // Stores the value of N
    int temp = n;

    // Stores the maximum value
    int maxi = n;

    // Stores the minimum value
    int mini = n;

    for (int idx = 0; idx < 7; idx++) {

        // If temp is odd
        if (temp %2 == 1) {
            temp >>= 1;
            temp += (int)Math.Pow(2, 7);
        }

        else
            temp >>= 1;

        // Update the maximum
        // and the minimum value
        mini = Math.Min(mini, temp);
        maxi = Math.Max(maxi, temp);
    }

    // If flag is 1, then
    // return the maximum value
    if (f==1)
        return (maxi);

    // Otherwise, return
    // the maximum value
    else
        return (mini);
}

// Function to find the maximum difference
// between the sum of odd and even-indexed
// array elements possible by rotating bits
static int calcMinDiff(int[] arr, int n)
{

    // Stores the maximum difference
    int caseOne = 0;

    // Stores the sum of elements
    // present at odd indices
    int sumOfodd = 0;

    // Stores the sum of elements
    // present at even indices
    int sumOfeven = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If the index is even
        if (i % 2==0)
            sumOfodd += Rotate(arr[i], 0);
        else
            sumOfeven += Rotate(arr[i], 1);
    }

    // Update the caseOne
    caseOne = Math.Abs(sumOfodd - sumOfeven);

    // Stores the maximum difference
    int caseTwo = 0;

    // Stores the sum of elements
    // placed at odd positions
    sumOfodd = 0;

    // Stores the sum of elements
    // placed at even positions
    sumOfeven = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // If the index is even
        if (i % 2==0)
            sumOfodd += Rotate(arr[i], 1);
        else
            sumOfeven += Rotate(arr[i], 0);
    }

    // Update the caseTwo
    caseTwo = Math.Abs(sumOfodd - sumOfeven);

    // Return the maximum of caseOne
    // and caseTwo
    return Math.Max(caseOne, caseTwo);
}

    // Driver Code
    public static void Main(string[] args)
    {

        int[] arr = { 123, 86, 234, 189 };
    int n = arr.Length;
     Console.WriteLine((calcMinDiff(arr, n)));
    }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find maximum and
// minimum value of a number that
// can be obtained by rotating bits
function Rotate(n, f)
{

    // Stores the value of N
    let temp = n;

    // Stores the maximum value
    let maxi = n;

    // Stores the minimum value
    let mini = n;

    for (let idx = 0; idx < 7; idx++) {

        // If temp is odd
        if (temp %2 == 1) {
            temp >>= 1;
            temp += Math.pow(2, 7);
        }

        else
            temp >>= 1;

        // Update the maximum
        // and the minimum value
        mini = Math.min(mini, temp);
        maxi = Math.max(maxi, temp);
    }

    // If flag is 1, then
    // return the maximum value
    if (f==1)
        return (maxi);

    // Otherwise, return
    // the maximum value
    else
        return (mini);
}

// Function to find the maximum difference
// between the sum of odd and even-indexed
// array elements possible by rotating bits
function calcMinDiff(arr, n)
{

    // Stores the maximum difference
    let caseOne = 0;

    // Stores the sum of elements
    // present at odd indices
    let sumOfodd = 0;

    // Stores the sum of elements
    // present at even indices
    let sumOfeven = 0;

    // Traverse the given array
    for (let i = 0; i < n; i++) {

        // If the index is even
        if (i % 2==0)
            sumOfodd += Rotate(arr[i], 0);
        else
            sumOfeven += Rotate(arr[i], 1);
    }

    // Update the caseOne
    caseOne = Math.abs(sumOfodd - sumOfeven);

    // Stores the maximum difference
    let caseTwo = 0;

    // Stores the sum of elements
    // placed at odd positions
    sumOfodd = 0;

    // Stores the sum of elements
    // placed at even positions
    sumOfeven = 0;

    // Traverse the array
    for (let i = 0; i < n; i++)
    {

        // If the index is even
        if (i % 2==0)
            sumOfodd += Rotate(arr[i], 1);
        else
            sumOfeven += Rotate(arr[i], 0);
    }

    // Update the caseTwo
    caseTwo = Math.abs(sumOfodd - sumOfeven);

    // Return the maximum of caseOne
    // and caseTwo
    return Math.max(caseOne, caseTwo);
}

// Driver code

    let arr = [ 123, 86, 234, 189 ];
    let n = arr.length;
     document.write((calcMinDiff(arr, n)));

</script>
```

**Output:** 

```
326
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)