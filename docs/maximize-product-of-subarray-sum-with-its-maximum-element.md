# 最大化子阵和与其最大元素的乘积

> 原文:[https://www . geeksforgeeks . org/subarray 的最大乘积与其最大元素之和/](https://www.geeksforgeeks.org/maximize-product-of-subarray-sum-with-its-maximum-element/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出[子数组和](https://www.geeksforgeeks.org/sum-of-all-subarrays/)与该子数组的[个最大元素的最大乘积。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** arr[] = {2，-3，8，-2，5}
> **输出:** 88
> **解释:**
> 使用子阵{8，-2，5}
> 可以得到所需的最大乘积因此，最大乘积= (8 + (-2) + 5) * (8) = 88。
> 
> **输入:** arr[] = {-4，1，-5，3，5 }
> T3】输出: 40

**天真法:**解决问题最简单的方法是[生成给定阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有子阵列，对于每个子阵列，计算子阵列的[和，并与子阵列中的最大元素相乘。通过与计算的产品进行比较，更新最大产品。检查所有子阵列后，打印处理所有子阵列后获得的最大产品。](https://www.geeksforgeeks.org/sum-of-all-subarrays/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过修改[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来优化，得到最终的最大值。按照以下步骤解决问题:

*   按照以下步骤执行卡丹算法:
    *   将三个变量初始化为**最大值**、**最大值**、**最大值**为 **0** 。
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下步骤；
        *   将 **currSum** 更新为 **currSum + arr[i]** ，将 **currMax** 更新为 **max(currMax，arr[i])** 。
        *   将**最大总和**的值更新为**最大值(最大总和，当前*当前)**。
        *   如果 **currSum** 的值小于 **0** ，则将 **currMax** 和 **currSum** 的值更新为 **0** 。
    *   完成上述步骤后，返回 **largestSum** 的值，作为子阵列与其最大元素之和的合成最大乘积。
*   初始化一个变量，将**最大值**设为 **0** ，该变量存储子阵列与其最大元素的[和的最大乘积。](https://www.geeksforgeeks.org/find-subarray-with-given-sum/)
*   对给定数组执行更新的卡丹算法，并将返回值存储在**最大值**中。
*   现在，通过将每个元素乘以 **(-1)** 来更新每个数组元素，并用更新后的数组再次执行更新后的卡丹算法，以便如果任何子数组的最大元素为负，则必须考虑该组合。
*   将**最大值**的值更新为**最大值**的最大值和上一步返回的值。
*   完成上述步骤后，打印**最大值**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum product
// of the sum of the subarray with its
// maximum element
int Kadane(int arr[], int n)
{

    int largestSum = 0, currMax = 0;
    int currSum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Increment currSum by a[i]
        currSum += arr[i];

        // Maximize the value of currMax
        currMax = max(currMax, arr[i]);

        // Maximize the value of
        // largestSum
        largestSum = max(largestSum,
                         currMax * currSum);

        // If currSum goes less than 0
        // then update currSum = 0
        if (currSum < 0) {
            currMax = 0;
            currSum = 0;
        }
    }

    // Return the resultant value
    return largestSum;
}

// Function to maximize the product of
// the sum of the subarray with its
// maximum element
int maximumWeight(int arr[], int n)
{
    // Find the largest sum of the
    // subarray
    int largestSum = Kadane(arr, n);

    // Multiply each array element
    // with -1
    for (int i = 0; i < n; i++) {
        arr[i] = -arr[i];
    }

    // Find the largest sum of the
    // subarray with negation of all
    // array element
    largestSum = max(largestSum,
                     Kadane(arr, n));

    // Return the resultant maximum
    // value
    return largestSum;
}

// Driver Code
int main()
{
    int arr[] = { 2, -3, 8, -2, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumWeight(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    // Function to find the maximum product
    // of the sum of the subarray with its
    // maximum element
    static int Kadane(int arr[], int n)
    {

        int largestSum = 0, currMax = 0;
        int currSum = 0;

        // Traverse the array arr[]
        for (int i = 0; i < n; i++) {

            // Increment currSum by a[i]
            currSum += arr[i];

            // Maximize the value of currMax
            currMax = Math.max(currMax, arr[i]);

            // Maximize the value of
            // largestSum
            largestSum
                = Math.max(largestSum, currMax * currSum);

            // If currSum goes less than 0
            // then update currSum = 0
            if (currSum < 0) {
                currMax = 0;
                currSum = 0;
            }
        }

        // Return the resultant value
        return largestSum;
    }

    // Function to maximize the product of
    // the sum of the subarray with its
    // maximum element
    static int maximumWeight(int arr[], int n)
    {
        // Find the largest sum of the
        // subarray
        int largestSum = Kadane(arr, n);

        // Multiply each array element
        // with -1
        for (int i = 0; i < n; i++) {
            arr[i] = -arr[i];
        }

        // Find the largest sum of the
        // subarray with negation of all
        // array element
        largestSum = Math.max(largestSum, Kadane(arr, n));

        // Return the resultant maximum
        // value
        return largestSum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, -3, 8, -2, 5 };
        int N = arr.length;
        System.out.println(maximumWeight(arr, N));
        // This code is contributed by Potta Lokesh
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum product
# of the sum of the subarray with its
# maximum element
def Kadane(arr, n):

    largestSum = 0
    currMax = 0
    currSum = 0

    # Traverse the array arr[]
    for i in range(n):

        # Increment currSum by a[i]
        currSum += arr[i]

        # Maximize the value of currMax
        currMax = max(currMax, arr[i])

        # Maximize the value of
        # largestSum
        largestSum = max(largestSum,
                         currMax * currSum)

        # If currSum goes less than 0
        # then update currSum = 0
        if (currSum < 0):
            currMax = 0
            currSum = 0

    # Return the resultant value
    return largestSum

# Function to maximize the product of
# the sum of the subarray with its
# maximum element
def maximumWeight(arr, n):

    # Find the largest sum of the
    # subarray
    largestSum = Kadane(arr, n)

    # Multiply each array element
    # with -1
    for i in range(n):
        arr[i] = -arr[i]

    # Find the largest sum of the
    # subarray with negation of all
    # array element
    largestSum = max(largestSum,
                     Kadane(arr, n))

    # Return the resultant maximum
    # value
    return largestSum

# Driver Code
if __name__ == '__main__':

    arr = [ 2, -3, 8, -2, 5 ]
    N = len(arr)

    print(maximumWeight(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum product
// of the sum of the subarray with its
// maximum element
static int Kadane(int []arr, int n)
{
    int largestSum = 0, currMax = 0;
    int currSum = 0;

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Increment currSum by a[i]
        currSum += arr[i];

        // Maximize the value of currMax
        currMax = Math.Max(currMax, arr[i]);

        // Maximize the value of
        // largestSum
        largestSum = Math.Max(largestSum,
                              currMax * currSum);

        // If currSum goes less than 0
        // then update currSum = 0
        if (currSum < 0)
        {
            currMax = 0;
            currSum = 0;
        }
    }

    // Return the resultant value
    return largestSum;
}

// Function to maximize the product of
// the sum of the subarray with its
// maximum element
static int maximumWeight(int []arr, int n)
{

    // Find the largest sum of the
    // subarray
    int largestSum = Kadane(arr, n);

    // Multiply each array element
    // with -1
    for(int i = 0; i < n; i++)
    {
        arr[i] = -arr[i];
    }

    // Find the largest sum of the
    // subarray with negation of all
    // array element
    largestSum = Math.Max(largestSum,
                          Kadane(arr, n));

    // Return the resultant maximum
    // value
    return largestSum;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, -3, 8, -2, 5 };
    int N = arr.Length;

    Console.Write(maximumWeight(arr, N));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to find the maximum product
       // of the sum of the subarray with its
       // maximum element
       function Kadane(arr, n) {

           let largestSum = 0, currMax = 0;
           let currSum = 0;

           // Traverse the array arr[]
           for (let i = 0; i < n; i++) {

               // Increment currSum by a[i]
               currSum += arr[i];

               // Maximize the value of currMax
               currMax = Math.max(currMax, arr[i]);

               // Maximize the value of
               // largestSum
               largestSum = Math.max(largestSum,
                   currMax * currSum);

               // If currSum goes less than 0
               // then update currSum = 0
               if (currSum < 0) {
                   currMax = 0;
                   currSum = 0;
               }
           }

           // Return the resultant value
           return largestSum;
       }

       // Function to maximize the product of
       // the sum of the subarray with its
       // maximum element
       function maximumWeight(arr, n) {
           // Find the largest sum of the
           // subarray
           let largestSum = Kadane(arr, n);

           // Multiply each array element
           // with -1
           for (let i = 0; i < n; i++) {
               arr[i] = -arr[i];
           }

           // Find the largest sum of the
           // subarray with negation of all
           // array element
           largestSum = Math.max(largestSum,
               Kadane(arr, n));

           // Return the resultant maximum
           // value
           return largestSum;
       }

       // Driver Code

       let arr = [2, -3, 8, -2, 5];
       let N = arr.length;
       document.write(maximumWeight(arr, N));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
88
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*