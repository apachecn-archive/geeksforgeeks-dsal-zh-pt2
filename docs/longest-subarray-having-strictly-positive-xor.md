# 具有严格正异或的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长子数组-具有-严格正-xor/](https://www.geeksforgeeks.org/longest-subarray-having-strictly-positive-xor/)

给定非负整数的数组**arr[]****N**。任务是找到最长子阵列的长度，使得这个子阵列的所有元素的异或是严格正的。如果不存在这样的子阵列，则打印 **-1**
**示例:**

> **输入:** arr[] = {1，1，1，1}
> **输出:** 3
> 取子阵【0:2】= { 1，1，1}
> 此子阵的 Xor 等于 1。
> **输入:** arr[] = {0，1，5，19}
> **输出:** 4

**进场:**

*   如果完整数组的异或为正，则答案等于 **N** 。
*   如果所有元素都是零，那么答案是 **-1** ，因为不可能得到严格的正异或。
*   否则，假设第一个正数的指数为 **l** ，最后一个正数为 **r** 。
*   现在，索引范围**【l，r】**的所有元素的异或必须为零，因为在 **l** 之前和 **r** 之后的元素是 **0s** ，它们不会对异或值产生影响，并且原始数组的异或是 **0** 。
*   考虑子阵列 **A <sub>1</sub> 、A <sub>1</sub> 、…、A <sub>r-1</sub>** 和 **A <sub>l+1</sub> 、A <sub>l+2</sub> 、…、A <sub>N</sub>** 。
*   第一个子阵列的异或值等于**A【r】**，第二个子阵列的异或值为**A【l】**正。
*   返回这两个子数组中较大子数组的长度。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the
// longest sub-array having positive XOR
int StrictlyPositiveXor(int A[], int N)
{

    // To store the XOR
    // of all the elements
    int allxor = 0;

    // To check if all the
    // elements of the array are 0s
    bool checkallzero = true;

    for (int i = 0; i < N; i += 1) {

        // Take XOR of all the elements
        allxor ^= A[i];

        // If any positive value is found
        // the make the checkallzero false
        if (A[i] > 0)
            checkallzero = false;
    }

    // If complete array is the answer
    if (allxor != 0)
        return N;

    // If all elements are equal to zero
    if (checkallzero)
        return -1;

    // Initialize l and r
    int l = N, r = -1;

    for (int i = 0; i < N; i += 1) {

        // First positive value of the array
        if (A[i] > 0) {
            l = i + 1;
            break;
        }
    }
    for (int i = N - 1; i >= 0; i -= 1) {

        // Last positive value of the array
        if (A[i] > 0) {
            r = i + 1;
            break;
        }
    }

    // Maximum length among
    // these two subarrays
    return max(N - l, r - 1);
}

// Driver code
int main()
{

    int A[] = { 1, 0, 0, 1 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << StrictlyPositiveXor(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the length of the
// longest sub-array having positive XOR
static int StrictlyPositiveXor(int []A, int N)
{

    // To store the XOR
    // of all the elements
    int allxor = 0;

    // To check if all the
    // elements of the array are 0s
    boolean checkallzero = true;

    for (int i = 0; i < N; i += 1)
    {

        // Take XOR of all the elements
        allxor ^= A[i];

        // If any positive value is found
        // the make the checkallzero false
        if (A[i] > 0)
            checkallzero = false;
    }

    // If complete array is the answer
    if (allxor != 0)
        return N;

    // If all elements are equal to zero
    if (checkallzero)
        return -1;

    // Initialize l and r
    int l = N, r = -1;

    for (int i = 0; i < N; i += 1)
    {

        // First positive value of the array
        if (A[i] > 0)
        {
            l = i + 1;
            break;
        }
    }
    for (int i = N - 1; i >= 0; i -= 1)
    {

        // Last positive value of the array
        if (A[i] > 0)
        {
            r = i + 1;
            break;
        }
    }

    // Maximum length among
    // these two subarrays
    return Math.max(N - l, r - 1);
}

// Driver code
public static void main (String[] args)
{
    int A[] = { 1, 0, 0, 1 };

    int N = A.length;

    System.out.print(StrictlyPositiveXor(A, N));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of the
# longest sub-array having positive XOR
def StrictlyPositiveXor(A, N) :

    # To store the XOR
    # of all the elements
    allxor = 0;

    # To check if all the
    # elements of the array are 0s
    checkallzero = True;

    for i in range(N) :

        # Take XOR of all the elements
        allxor ^= A[i];

        # If any positive value is found
        # the make the checkallzero false
        if (A[i] > 0) :
            checkallzero = False;

    # If complete array is the answer
    if (allxor != 0) :
        return N;

    # If all elements are equal to zero
    if (checkallzero) :
        return -1;

    # Initialize l and r
    l = N; r = -1;

    for i in range(N) :

        # First positive value of the array
        if (A[i] > 0) :
            l = i + 1;
            break;

    for i in range(N - 1, -1, -1) :

        # Last positive value of the array
        if (A[i] > 0) :
            r = i + 1;
            break;

    # Maximum length among
    # these two subarrays
    return max(N - l, r - 1);

# Driver code
if __name__ == "__main__" :

    A= [ 1, 0, 0, 1 ];
    N = len(A);
    print(StrictlyPositiveXor(A, N));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the length of the
// longest sub-array having positive XOR
static int StrictlyPositiveXor(int []A, int N)
{

    // To store the XOR
    // of all the elements
    int allxor = 0;

    // To check if all the
    // elements of the array are 0s
    bool checkallzero = true;

    for (int i = 0; i < N; i += 1)
    {

        // Take XOR of all the elements
        allxor ^= A[i];

        // If any positive value is found
        // the make the checkallzero false
        if (A[i] > 0)
            checkallzero = false;
    }

    // If complete array is the answer
    if (allxor != 0)
        return N;

    // If all elements are equal to zero
    if (checkallzero)
        return -1;

    // Initialize l and r
    int l = N, r = -1;

    for (int i = 0; i < N; i += 1)
    {

        // First positive value of the array
        if (A[i] > 0)
        {
            l = i + 1;
            break;
        }
    }
    for (int i = N - 1; i >= 0; i -= 1)
    {

        // Last positive value of the array
        if (A[i] > 0)
        {
            r = i + 1;
            break;
        }
    }

    // Maximum length among
    // these two subarrays
    return Math.Max(N - l, r - 1);
}

// Driver code
public static void Main ()
{
    int []A = { 1, 0, 0, 1 };

    int N = A.Length;

    Console.WriteLine(StrictlyPositiveXor(A, N));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length of the
// longest sub-array having positive XOR
function StrictlyPositiveXor(A, N)
{

    // To store the XOR
    // of all the elements
    let allxor = 0;

    // To check if all the
    // elements of the array are 0s
    let checkallzero = true;

    for (let i = 0; i < N; i += 1) {

        // Take XOR of all the elements
        allxor ^= A[i];

        // If any positive value is found
        // the make the checkallzero false
        if (A[i] > 0)
            checkallzero = false;
    }

    // If complete array is the answer
    if (allxor != 0)
        return N;

    // If all elements are equal to zero
    if (checkallzero)
        return -1;

    // Initialize l and r
    let l = N, r = -1;

    for (let i = 0; i < N; i += 1) {

        // First positive value of the array
        if (A[i] > 0) {
            l = i + 1;
            break;
        }
    }
    for (let i = N - 1; i >= 0; i -= 1) {

        // Last positive value of the array
        if (A[i] > 0) {
            r = i + 1;
            break;
        }
    }

    // Maximum length among
    // these two subarrays
    return Math.max(N - l, r - 1);
}

// Driver code

    let A = [ 1, 0, 0, 1 ];

    let N = A.length;

    document.write(StrictlyPositiveXor(A, N));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)