# 非负和最长的子序列

> 原文:[https://www . geesforgeks . org/最长子序列-带非负和/](https://www.geeksforgeeks.org/longest-sub-sequence-with-non-negative-sum/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到具有非负和的最大子序列的长度。
**例:**

> **输入:** arr[] = {1，2，-3}
> **输出:** 3
> 完整数组有一个非负和。
> **输入:** arr[] = {1，2，-4}
> **输出:** 2
> {1，2}为所需子序列。

**方法:**思想是所有非负数都必须包含在子序列中，因为这样的数只会增加总和的值。
现在，在负数中不难看出，必须先选大的。因此，只要负数不使总和的值降低到 0 以下，就继续按这些值的非递增顺序相加。这可以在[整理](https://www.geeksforgeeks.org/sorting-algorithms/)阵列后完成。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the largest subsequence
// with non-negative sum
int maxLen(int* arr, int n)
{
    // To store the current sum
    int c_sum = 0;

    // Sort the input array in
    // non-increasing order
    sort(arr, arr + n, greater<int>());

    // Traverse through the array
    for (int i = 0; i < n; i++) {

        // Add the current element to the sum
        c_sum += arr[i];

        // Condition when c_sum falls
        // below zero
        if (c_sum < 0)
            return i;
    }

    // Complete array has a non-negative sum
    return n;
}

// Driver code
int main()
{
    int arr[] = { 3, 5, -6 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxLen(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the length of
// the largest subsequence
// with non-negative sum
static int maxLen(int[] arr, int n)
{
    // To store the current sum
    int c_sum = 0;

    // Sort the input array in
    // non-increasing order
    Arrays.sort(arr);

    // Traverse through the array
    for (int i = n-1; i >=0; i--)
    {

        // Add the current element to the sum
        c_sum += arr[i];

        // Condition when c_sum falls
        // below zero
        if (c_sum < 0)
            return i;
    }

    // Complete array has a non-negative sum
    return n;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 3, 5, -6 };
    int n = arr.length;

    System.out.println(maxLen(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of
# the largest subsequence
# with non-negative sum
def maxLen(arr, n) :

    # To store the current sum
    c_sum = 0;

    # Sort the input array in
    # non-increasing order
    arr.sort(reverse = True);

    # Traverse through the array
    for i in range(n) :

        # Add the current element to the sum
        c_sum += arr[i];

        # Condition when c_sum falls
        # below zero
        if (c_sum < 0) :
            return i;

    # Complete array has a non-negative sum
    return n;

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 5, -6 ];
    n = len(arr);

    print(maxLen(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the length of
// the largest subsequence
// with non-negative sum
static int maxLen(int[] arr, int n)
{
    // To store the current sum
    int c_sum = 0;

    // Sort the input array in
    // non-increasing order
    Array.Sort(arr);

    // Traverse through the array
    for (int i = n - 1; i >= 0; i--)
    {

        // Add the current element to the sum
        c_sum += arr[i];

        // Condition when c_sum falls
        // below zero
        if (c_sum < 0)
            return i;
    }

    // Complete array has a non-negative sum
    return n;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, 5, -6 };
    int n = arr.Length;

    Console.WriteLine(maxLen(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length of
// the largest subsequence
// with non-negative sum
function maxLen(arr, n)
{
    // To store the current sum
    var c_sum = 0;

    // Sort the input array in
    // non-increasing order
    arr.sort((a,b)=> b-a)

    // Traverse through the array
    for (var i = 0; i < n; i++) {

        // Add the current element to the sum
        c_sum += arr[i];

        // Condition when c_sum falls
        // below zero
        if (c_sum < 0)
            return i;
    }

    // Complete array has a non-negative sum
    return n;
}

// Driver code
var arr = [3, 5, -6];
var n = arr.length;
document.write( maxLen(arr, n));

</script>
```

**Output:** 

```
3
```