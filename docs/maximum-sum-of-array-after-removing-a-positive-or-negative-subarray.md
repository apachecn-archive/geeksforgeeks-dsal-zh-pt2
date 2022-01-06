# 去除正负子阵列后的阵列最大和

> 原文:[https://www . geeksforgeeks . org/移除正或负子阵列后的最大阵列总和/](https://www.geeksforgeeks.org/maximum-sum-of-array-after-removing-a-positive-or-negative-subarray/)

给定一个非零整数的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr[]****N**，任务是通过移除恰好一组连续的正元素或负元素来找到数组的[最大和。](https://www.geeksforgeeks.org/maximum-subarray-sum-using-divide-and-conquer-algorithm/)

**示例:**

> **输入:** arr[] = {-2，-3，4，-1，-2，1，5，-3}
> **输出:** 4
> **说明:**由于 arr[0，1]具有相同类型的元素，即负元素，因此可以通过移除子阵列 arr[0，1]来获得最大阵列和。因此，所需的总和是 4。
> 
> **输入:** arr[] = {2，-10，4，2，-8，-7}
> **输出:** -2
> **解释:**由于 arr[4，5]具有相同类型的元素，即负元素，因此可以通过移除子阵列 arr[4，5]来获得最大阵列和。因此，所需的总和为-2。

**方法:**给定的问题可以基于以下观察来解决，即为了获得最大和，要移除一组连续的负元素，因为移除正元素将减少数组和。但是，如果没有负元素，则移除数组中的[最小元素。按照以下步骤解决问题:](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)， **arr[]** 并将**T5[数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的总和存储在变量中，比如说**总和**。**
*   将最大连续负和存储在一个变量中，比如 **max_neg** 。
*   如果数组中没有负元素，则将 **max_neg** 更新为数组中最小的[元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)。
*   将 **sum** 的值更新为**(sum–max _ neg)**。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// array after removing either the contiguous
// positive or negative elements
void maxSum(int arr[], int n)
{
    // Store the total sum of array
    int sum = 0;

    // Store the maximum contiguous
    // negative sum
    int max_neg = INT_MAX;

    // Store the sum of current
    // contiguous negative elements
    int tempsum = 0;

    // Store the minimum element of array
    int small = INT_MAX;

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {

        // Update the overall sum
        sum += arr[i];

        // Store minimum element of array
        small = min(small, arr[i]);

        // If arr[i] is positive
        if (arr[i] > 0) {

            // Update temp_sum to 0
            tempsum = 0;
        }

        else {

            // Add arr[i] to temp_sum
            tempsum += arr[i];
        }

        // Update max_neg
        max_neg = min(max_neg, tempsum);
    }

    // If no negative element in array
    // then remove smallest positive element
    if (max_neg == 0) {
        max_neg = small;
    }

    // Print the required sum
    cout << sum - max_neg;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the maximum sum of
// array after removing either the contiguous
// positive or negative elements
static void maxSum(int arr[], int n)
{

    // Store the total sum of array
    int sum = 0;

    // Store the maximum contiguous
    // negative sum
    int max_neg = Integer.MAX_VALUE;

    // Store the sum of current
    // contiguous negative elements
    int tempsum = 0;

    // Store the minimum element of array
    int small = Integer.MAX_VALUE;

    // Traverse the array, arr[]
    for(int i = 0; i < n; i++)
    {

        // Update the overall sum
        sum += arr[i];

        // Store minimum element of array
        small = Math.min(small, arr[i]);

        // If arr[i] is positive
        if (arr[i] > 0)
        {

            // Update temp_sum to 0
            tempsum = 0;
        }
        else
        {

            // Add arr[i] to temp_sum
            tempsum += arr[i];
        }

        // Update max_neg
        max_neg = Math.min(max_neg, tempsum);
    }

    // If no negative element in array
    // then remove smallest positive element
    if (max_neg == 0)
    {
        max_neg = small;
    }

    // Print the required sum
    System.out.println(sum - max_neg);
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
    int n = arr.length;

    // Function Call
    maxSum(arr, n);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python 3 program for the above approach

import sys
# Function to find the maximum sum of
# array after removing either the contiguous
# positive or negative elements
def maxSum(arr, n):

    # Store the total sum of array
    sum = 0

    # Store the maximum contiguous
    # negative sum
    max_neg = sys.maxsize

    # Store the sum of current
    # contiguous negative elements
    tempsum = 0

    # Store the minimum element of array
    small = sys.maxsize

    # Traverse the array, arr[]
    for i in range(n):
        # Update the overall sum
        sum += arr[i]

        # Store minimum element of array
        small = min(small, arr[i])

        # If arr[i] is positive
        if (arr[i] > 0):
            # Update temp_sum to 0
            tempsum = 0

        else:

            # Add arr[i] to temp_sum
            tempsum += arr[i]

        # Update max_neg
        max_neg = min(max_neg, tempsum)

    # If no negative element in array
    # then remove smallest positive element
    if (max_neg == 0):
        max_neg = small

    # Print the required sum
    print(sum - max_neg)

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [-2, -3, 4, -1, -2, 1, 5, -3]
    n = len(arr)

    # Function Call
    maxSum(arr, n)

    # This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum sum of
// array after removing either the contiguous
// positive or negative elements
function maxSum(arr, n) {
    // Store the total sum of array
    let sum = 0;

    // Store the maximum contiguous
    // negative sum
    let max_neg = Number.MAX_SAFE_INTEGER;

    // Store the sum of current
    // contiguous negative elements
    let tempsum = 0;

    // Store the minimum element of array
    let small = Number.MAX_SAFE_INTEGER;

    // Traverse the array, arr[]
    for (let i = 0; i < n; i++) {

        // Update the overall sum
        sum += arr[i];

        // Store minimum element of array
        small = Math.min(small, arr[i]);

        // If arr[i] is positive
        if (arr[i] > 0) {

            // Update temp_sum to 0
            tempsum = 0;
        }

        else {

            // Add arr[i] to temp_sum
            tempsum += arr[i];
        }

        // Update max_neg
        max_neg = Math.min(max_neg, tempsum);
    }

    // If no negative element in array
    // then remove smallest positive element
    if (max_neg == 0) {
        max_neg = small;
    }

    // Print the required sum
    document.write(sum - max_neg);
}

// Driver Code

// Given Input
let arr = [-2, -3, 4, -1, -2, 1, 5, -3];
let n = arr.length;

// Function Call
maxSum(arr, n);

// This code is contributed by gfgking.
</script>
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// array after removing either the contiguous
// positive or negative elements
static void maxSum(int []arr, int n)
{

    // Store the total sum of array
    int sum = 0;

    // Store the maximum contiguous
    // negative sum
    int max_neg = Int32.MaxValue;

    // Store the sum of current
    // contiguous negative elements
    int tempsum = 0;

    // Store the minimum element of array
    int small = Int32.MaxValue;

    // Traverse the array, arr[]
    for(int i = 0; i < n; i++)
    {

        // Update the overall sum
        sum += arr[i];

        // Store minimum element of array
        small = Math.Min(small, arr[i]);

        // If arr[i] is positive
        if (arr[i] > 0)
        {

            // Update temp_sum to 0
            tempsum = 0;
        }
        else
        {

            // Add arr[i] to temp_sum
            tempsum += arr[i];
        }

        // Update max_neg
        max_neg = Math.Min(max_neg, tempsum);
    }

    // If no negative element in array
    // then remove smallest positive element
    if (max_neg == 0)
    {
        max_neg = small;
    }

    // Print the required sum
    Console.Write(sum - max_neg);
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int []arr = { -2, -3, 4, -1, -2, 1, 5, -3 };
    int n = arr.Length;

    // Function Call
    maxSum(arr, n);
}
}

// This code is contributed by shivanisinghss2110
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)