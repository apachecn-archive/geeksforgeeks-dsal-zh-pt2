# 通过翻转单个子阵列所有元素的符号来最大化阵列的总和

> 原文:[https://www . geesforgeks . org/通过翻转单个子阵列所有元素的符号来最大化阵列总和/](https://www.geeksforgeeks.org/maximize-sum-of-an-array-by-flipping-sign-of-all-elements-of-a-single-subarray/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过最多一次翻转给定数组的任意[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的**符号**得到数组的**最大和**。

**示例:**

> **输入:** arr[] = {-2，3，-1，-4，-2}
> **输出:** 8
> **解释:**
> 翻转子阵的符号{-1，-4，-2}将数组修改为{-2，3，1，4，2}。因此，数组的和= -2 + 3 + 1 + 4 + 2 = 8，这是最大可能。
> 
> **输入:** arr[] = {1，2，-10，2，-20}
> **输出:** 31
> **解释:**
> 翻转子阵的符号{-10，2，-20}将数组修改为{1，2，10，-2，20}。因此，数组的和= 1+2+10–2+20 = 31，这是最大可能值。

**天真法:**最简单的方法是计算阵列的[总和，然后](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。现在，对于每个子阵列{ **A[i]，… A[j]** }，从总和中减去其总和， **sum(A[i]，…，A[j])** ，并翻转子阵列元素的符号。翻转子阵列后，将翻转后的子阵列之和，即 **(-1 * sum(A[i]，…，A[j])**)加到总和上。以下是步骤:

1.  求原数组的总和(比如 **total_sum** )并存储。
2.  现在，对于所有可能的子阵列，求**total _ sum–2 * sum(I，j)** 的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// after flipping a subarray
int maxSumFlip(int a[], int n)
{

    // Stores the total sum of array
    int total_sum = 0;
    for (int i = 0; i < n; i++)
        total_sum += a[i];

    // Initialize the maximum sum
    int max_sum = INT_MIN;

    // Iterate over all possible subarrays
    for (int i = 0; i < n; i++)
    {
        // Initialize sum of the subarray
        // before flipping sign
        int sum = 0;

        for (int j = i; j < n; j++)
        {
            // Calculate the sum of
            // original subarray
            sum += a[j];

            // Subtract the original
            // subarray sum and add
            // the flipped subarray
            // sum to the total sum
            max_sum = max(max_sum, total_sum - 2 * sum);
        }
    }

    // Return the max_sum
    return max(max_sum, total_sum);
}

// Driver Code
int main()
{
    int arr[] = { -2, 3, -1, -4, -2 };
    int N = sizeof(arr) / sizeof(int);

    cout << maxSumFlip(arr, N);
}

// This code is contributed by sanjoy_62
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

public class GFG
{
    // Function to find the maximum sum
    // after flipping a subarray
    public static int maxSumFlip(int a[], int n)
    {
        // Stores the total sum of array
        int total_sum = 0;
        for (int i = 0; i < n; i++)
            total_sum += a[i];

        // Initialize the maximum sum
        int max_sum = Integer.MIN_VALUE;

        // Iterate over all possible subarrays
        for (int i = 0; i < n; i++)
        {
            // Initialize sum of the subarray
            // before flipping sign
            int sum = 0;

            for (int j = i; j < n; j++)
            {
                // Calculate the sum of
                // original subarray
                sum += a[j];

                // Subtract the original
                // subarray sum and add
                // the flipped subarray
                // sum to the total sum
                max_sum = Math.max(max_sum,
                                   total_sum - 2 * sum);
            }
        }

        // Return the max_sum
        return Math.max(max_sum, total_sum);
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { -2, 3, -1, -4, -2 };
        int N = arr.length;

        // Function call
        System.out.println(maxSumFlip(arr, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the maximum sum
# after flipping a subarray

def maxSumFlip(a, n):

    # Stores the total sum of array
    total_sum = 0
    for i in range(n):
        total_sum += a[i]

    # Initialize the maximum sum
    max_sum = -sys.maxsize - 1

    # Iterate over all possible subarrays
    for i in range(n):

        # Initialize sum of the subarray
        # before flipping sign
        sum = 0

        for j in range(i, n):

            # Calculate the sum of
            # original subarray
            sum += a[j]

            # Subtract the original
            # subarray sum and add
            # the flipped subarray
            # sum to the total sum
            max_sum = max(max_sum,
                          total_sum - 2 * sum)

    # Return the max_sum
    return max(max_sum, total_sum)

# Driver Code
arr = [-2, 3, -1, -4, -2]
N = len(arr)

print(maxSumFlip(arr, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the maximum sum
    // after flipping a subarray
    public static int maxSumFlip(int[] a, int n)
    {

        // Stores the total sum of array
        int total_sum = 0;
        for (int i = 0; i < n; i++)
            total_sum += a[i];

        // Initialize the maximum sum
        int max_sum = int.MinValue;

        // Iterate over all possible subarrays
        for (int i = 0; i < n; i++)
        {
            // Initialize sum of the subarray
            // before flipping sign
            int sum = 0;

            for (int j = i; j < n; j++)
            {
                // Calculate the sum of
                // original subarray
                sum += a[j];

                // Subtract the original
                // subarray sum and add
                // the flipped subarray
                // sum to the total sum
                max_sum = Math.Max(max_sum,
                                   total_sum - 2 * sum);
            }
        }

        // Return the max_sum
        return Math.Max(max_sum, total_sum);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { -2, 3, -1, -4, -2 };
        int N = arr.Length;

        // Function call
        Console.WriteLine(maxSumFlip(arr, N));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find the maximum sum
    // after flipping a subarray
    function maxSumFlip(a, n)
    {
        // Find the total sum of array
        let total_sum = 0;
        for (let i = 0; i < n; i++)
            total_sum += a[i];

        // Using Kadane's Algorithm
        let max_ending_here = -a[0] - a[0];
        let curr_sum = -a[0] - a[0];

        for (let i = 1; i < n; i++)
        {
            // Either extend previous
            // sub_array or start
            // new subarray
            curr_sum = Math.max(curr_sum + (-a[i] - a[i]),
                                (-a[i] - a[i]));

            // Keep track of max_sum array
            max_ending_here
                = Math.max(max_ending_here, curr_sum);
        }

        // Add the sum to the total_sum
        let max_sum = total_sum + max_ending_here;

        // Check max_sum was maximum
        // with flip or without flip
        max_sum = Math.max(max_sum, total_sum);

        // Return max_sum
        return max_sum;
    }

// Driver Code

        let arr = [ -2, 3, -1, -4, -2 ];
        let N = arr.length;

        // Function Call
        document.write(maxSumFlip(arr, N));

</script>
```

**Output**

```
8
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**有效途径:**从上述途径可以观察到，为了获得最大阵列和， **(2 *子阵列和)**需要对所有子阵列最大化。这可以通过使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来完成。以下是步骤:

1.  使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)从**l【】**找到最小和子阵
2.  这最大化了 **(2 * sum)** 对所有子阵列的贡献。
3.  将最大贡献与数组的总和相加。

下面是上述方法的实现:

## 蟒蛇 3

```
def maxsum(l,n):
  total_sum=sum(l)
  #kadane's algorithm to find the minimum subarray sum
  current_sum=0
  minimum_sum=0
  for i in l:
    current_sum+=i
    minimum_sum=min(minimum_sum,current_sum)
    current_sum=min(current_sum,0)
  return max(total_sum,total_sum-2*minimum_sum)
l=[-2,3,-1,-4,-2]
n=len(l)
print(maxsum(l,n))
```

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// after flipping a subarray
int maxSumFlip(int a[], int n)
{

    // Stores the total sum of array
    int total_sum = 0;
    for (int i = 0; i < n; i++)
        total_sum += a[i];

      // Kadane's algorithm to find the minimum subarray sum
    int b,a=2e9;
    for (int i = 0; i < n; i++)
    {
        b+=ar[i];
          if(a>b)
          a=b;
          if(b>0)
          b=0;
    }

    // Return the max_sum
    return max(total_sum,total_sum-2*a);
}

// Driver Code
int main()
{
    int arr[] = { -2, 3, -1, -4, -2 };
    int N = sizeof(arr) / sizeof(int);

    cout << maxSumFlip(arr, N);
}
```

**Output**

```
8

```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
注:也可以通过求最小子阵和并打印 max(TotalSum，TotalSum-2 *(minsubaraysum))