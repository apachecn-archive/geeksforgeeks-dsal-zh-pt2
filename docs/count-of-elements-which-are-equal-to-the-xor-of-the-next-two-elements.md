# 等于后两个元素异或的元素计数

> 原文:[https://www . geesforgeks . org/元素计数等于下两个元素的异或数/](https://www.geeksforgeeks.org/count-of-elements-which-are-equal-to-the-xor-of-the-next-two-elements/)

给定一个由 **n** 个元素组成的数组 **arr[]** 。任务是找出等于接下来两个元素异或的元素数。
**例:**

> **输入:** arr[] = {4，2，1，3，7，8}
> **输出:** 1
> 2 是唯一有效的元素，因为 1 ^ 3 = 2
> **输入:** arr[] = {23，1，7，8，6}
> **输出:** 0

**方法:**初始化**计数= 0** 对于数组中的每个元素，至少有两个元素出现在数组中，如果它等于接下来两个元素的异或，则增加**计数**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of elements
// which are equal to the XOR
// of the next two elements
int cntElements(int arr[], int n)
{

    // To store the required count
    int cnt = 0;

    // For every element of the array such that
    // it has at least two elements appearing
    // after it in the array
    for (int i = 0; i < n - 2; i++) {

        // If current element is equal to the XOR
        // of the next two elements in the array
        if (arr[i] == (arr[i + 1] ^ arr[i + 2])) {
            cnt++;
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 4, 2, 1, 3, 7, 8 };
    int n = sizeof(arr) / sizeof(int);

    cout << cntElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the count of elements
// which are equal to the XOR
// of the next two elements
static int cntElements(int arr[], int n)
{

    // To store the required count
    int cnt = 0;

    // For every element of the array such that
    // it has at least two elements appearing
    // after it in the array
    for (int i = 0; i < n - 2; i++)
    {

        // If current element is equal to the XOR
        // of the next two elements in the array
        if (arr[i] == (arr[i + 1] ^ arr[i + 2]))
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 4, 2, 1, 3, 7, 8 };
    int n = arr.length;

    System.out.println (cntElements(arr, n));
}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of elements
# which are equal to the XOR
# of the next two elements
def cntElements(arr, n):

    # To store the required count
    cnt = 0

    # For every element of the array such that
    # it has at least two elements appearing
    # after it in the array
    for i in range(n - 2):

        # If current element is equal to the XOR
        # of the next two elements in the array
        if (arr[i] == (arr[i + 1] ^ arr[i + 2])):
            cnt += 1

    return cnt

# Driver code
arr = [4, 2, 1, 3, 7, 8]
n = len(arr)

print(cntElements(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count of elements
// which are equal to the XOR
// of the next two elements
static int cntElements(int []arr, int n)
{

    // To store the required count
    int cnt = 0;

    // For every element of the array such that
    // it has at least two elements appearing
    // after it in the array
    for (int i = 0; i < n - 2; i++)
    {

        // If current element is equal to the XOR
        // of the next two elements in the array
        if (arr[i] == (arr[i + 1] ^ arr[i + 2]))
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 4, 2, 1, 3, 7, 8 };
    int n = arr.Length;

    Console.WriteLine(cntElements(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of elements
// which are equal to the XOR
// of the next two elements
function cntElements(arr, n)
{

    // To store the required count
    let cnt = 0;

    // For every element of the array such that
    // it has at least two elements appearing
    // after it in the array
    for (let i = 0; i < n - 2; i++) {

        // If current element is equal to the XOR
        // of the next two elements in the array
        if (arr[i] == (arr[i + 1] ^ arr[i + 2]))
        {
            cnt++;
        }
    }

    return cnt;
}

// Driver code
    let arr = [ 4, 2, 1, 3, 7, 8 ];
    let n = arr.length;

    document.write(cntElements(arr, n));

</script>
```

**Output:** 

```
1
```