# 给定数组前缀和后缀总和相等的索引计数

> 原文:[https://www . geeksforgeeks . org/给定数组的前缀和后缀之和等于哪个索引计数/](https://www.geeksforgeeks.org/count-of-indices-up-to-which-prefix-and-suffix-sum-is-equal-for-given-array/)

给定一个整数的[数组](https://www.geeksforgeeks.org/array-class-c/) **arr[]** ，任务是找出[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)与[后缀和](https://www.geeksforgeeks.org/tag/suffix/)相等的索引数。

**示例:**

> **输入:** arr = [9，0，0，-1，11，-1]
> **输出:** 2
> **说明:**前缀和后缀总和相等的索引如下:
> At 索引 1 前缀和后缀总和为 9
> At 索引 2 前缀和后缀总和为 9
> 
> **输入:** arr = [5，0，4，-1，-3，0，2，-2，0，3，2]
> **输出:** 3
> **说明:**前缀子阵和后缀子阵的和相等如下:
> At 索引 1 前缀和后缀和为 5
> At 索引 5 前缀和后缀和为 5
> At 索引 8 前缀和后缀和为 5

**天真方法:**给定的问题可以通过以下方式解决:[从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr** 并计算前缀和直到该索引，然后[从右到左迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 并计算后缀和，然后检查前缀和后缀和是否相等。
**时间复杂度:** O(N^2)

**方法:**上述方法可以通过[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 两次来优化。想法是预先计算[后缀和](https://www.geeksforgeeks.org/tag/suffix-sum/)作为总的子阵列和。然后第二次迭代数组，在每个索引处计算[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，然后比较前缀和后缀和并更新后缀和。按照以下步骤解决问题:

*   初始化一个变量**将**重置为零来计算答案
*   初始化一个变量 **sufSum** 来存储[后缀 sum](https://www.geeksforgeeks.org/index-with-minimum-sum-of-prefix-and-suffix-sums-in-an-array/)
*   初始化一个变量**假设**存储[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr** 并将每个元素**arr【I】**添加到 **sufSum**
*   [在每次迭代中再次迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** :
    *   将当前元素**arr【I】**添加到**设定**中
    *   如果**假定**和**的总和**相等，则将 **res** 的值增加 1
    *   从**苏富姆**中减去当前元素**arr【I】**
*   返回存储在 **res** 中的答案

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate number of
// equal prefix and suffix sums
// till the same indices
int equalSumPreSuf(int arr[], int n)
{

    // Initialize a variable
    // to store the result
    int res = 0;

    // Initialize variables to
    // calculate prefix and suffix sums
    int preSum = 0, sufSum = 0;

    // Length of array arr
    int len = n;

    // Traverse the array from right to left
    for (int i = len - 1; i >= 0; i--)
    {

        // Add the current element
        // into sufSum
        sufSum += arr[i];
    }

    // Iterate the array from left to right
    for (int i = 0; i < len; i++)
    {

        // Add the current element
        // into preSum
        preSum += arr[i];

        // If prefix sum is equal to
        // suffix sum then increment res by 1
        if (preSum == sufSum)
        {

            // Increment the result
            res++;
        }

        // Subtract the value of current
        // element arr[i] from suffix sum
        sufSum -= arr[i];
    }

    // Return the answer
    return res;
}

// Driver code
int main()
{

    // Initialize the array
    int arr[] = {5, 0, 4, -1, -3, 0,
                 2, -2, 0, 3, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    // Call the function and
    // print its result
    cout << (equalSumPreSuf(arr, n));
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to calculate number of
    // equal prefix and suffix sums
    // till the same indices
    public static int equalSumPreSuf(int[] arr)
    {

        // Initialize a variable
        // to store the result
        int res = 0;

        // Initialize variables to
        // calculate prefix and suffix sums
        int preSum = 0, sufSum = 0;

        // Length of array arr
        int len = arr.length;

        // Traverse the array from right to left
        for (int i = len - 1; i >= 0; i--) {

            // Add the current element
            // into sufSum
            sufSum += arr[i];
        }

        // Iterate the array from left to right
        for (int i = 0; i < len; i++) {

            // Add the current element
            // into preSum
            preSum += arr[i];

            // If prefix sum is equal to
            // suffix sum then increment res by 1
            if (preSum == sufSum) {

                // Increment the result
                res++;
            }

            // Subtract the value of current
            // element arr[i] from suffix sum
            sufSum -= arr[i];
        }

        // Return the answer
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the array
        int[] arr = { 5, 0, 4, -1, -3, 0,
                      2, -2, 0, 3, 2 };

        // Call the function and
        // print its result
        System.out.println(equalSumPreSuf(arr));
    }
}
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to calculate number of
# equal prefix and suffix sums
# till the same indices
from builtins import range

def equalSumPreSuf(arr):

    # Initialize a variable
    # to store the result
    res = 0;

    # Initialize variables to
    # calculate prefix and suffix sums
    preSum = 0;
    sufSum = 0;

    # Length of array arr
    length = len(arr);

    # Traverse the array from right to left
    for i in range(length - 1,-1,-1):

        # Add the current element
        # into sufSum
        sufSum += arr[i];

    # Iterate the array from left to right
    for i in range(length):

        # Add the current element
        # into preSum
        preSum += arr[i];

        # If prefix sum is equal to
        # suffix sum then increment res by 1
        if (preSum == sufSum):

            # Increment the result
            res += 1;

        # Subtract the value of current
        # element arr[i] from suffix sum
        sufSum -= arr[i];

    # Return the answer
    return res;

# Driver code
if __name__ == '__main__':

    # Initialize the array
    arr = [5, 0, 4, -1, -3, 0, 2, -2, 0, 3, 2];

    # Call the function and
    # prits result
    print(equalSumPreSuf(arr));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

    // Function to calculate number of
    // equal prefix and suffix sums
    // till the same indices
    static int equalSumPreSuf(int[] arr)
    {

        // Initialize a variable
        // to store the result
        int res = 0;

        // Initialize variables to
        // calculate prefix and suffix sums
        int preSum = 0, sufSum = 0;

        // Length of array arr
        int len = arr.Length;

        // Traverse the array from right to left
        for (int i = len - 1; i >= 0; i--) {

            // Add the current element
            // into sufSum
            sufSum += arr[i];
        }

        // Iterate the array from left to right
        for (int i = 0; i < len; i++) {

            // Add the current element
            // into preSum
            preSum += arr[i];

            // If prefix sum is equal to
            // suffix sum then increment res by 1
            if (preSum == sufSum) {

                // Increment the result
                res++;
            }

            // Subtract the value of current
            // element arr[i] from suffix sum
            sufSum -= arr[i];
        }

        // Return the answer
        return res;
    }

    // Driver code
    public static void Main()
    {

        // Initialize the array
        int[] arr = { 5, 0, 4, -1, -3, 0,
                      2, -2, 0, 3, 2 };

        // Call the function and
        // print its result
        Console.Write(equalSumPreSuf(arr));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to calculate number of
// equal prefix and suffix sums
// till the same indices
function equalSumPreSuf(arr, n)
{

    // Initialize a variable
    // to store the result
    let res = 0;

    // Initialize variables to
    // calculate prefix and suffix sums
    let preSum = 0, sufSum = 0;

    // Length of array arr
    let len = n;

    // Traverse the array from right to left
    for (let i = len - 1; i >= 0; i--)
    {

        // Add the current element
        // into sufSum
        sufSum += arr[i];
    }

    // Iterate the array from left to right
    for (let i = 0; i < len; i++)
    {

        // Add the current element
        // into preSum
        preSum += arr[i];

        // If prefix sum is equal to
        // suffix sum then increment res by 1
        if (preSum == sufSum)
        {

            // Increment the result
            res++;
        }

        // Subtract the value of current
        // element arr[i] from suffix sum
        sufSum -= arr[i];
    }

    // Return the answer
    return res;
}

// Driver code

// Initialize the array
let arr = [5, 0, 4, -1, -3, 0,
             2, -2, 0, 3, 2];

let n = arr.length

// Call the function and
// print its result
document.write(equalSumPreSuf(arr, n));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)