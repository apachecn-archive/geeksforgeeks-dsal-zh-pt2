# 最大和交替子阵列

> 原文:[https://www . geesforgeks . org/maximum-sum-alternative-subarray/](https://www.geeksforgeeks.org/maximum-sum-alternating-subarray/)

给定一个大小为 **N、**的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定阵列的[子阵列](https://www.geeksforgeeks.org/tag/subarray/)的最大交替和。

> **交替子阵和:**考虑一个子阵 **{arr[i]，arr[j]}，**子阵**的交替和是 arr[I]–arr[I+1]+arr[I+2]–……..(+ / -) arr[j]。**

**示例:**

> **输入:** arr[] = {-4，-10，3，5}
> **输出:** 9
> **解释:**斯巴瑞{arr[0]，arr[2]} = {-4，-10，3}。因此，这个子阵列的总和是 9。
> 
> **输入:** arr[] = {-1，2，-1，4，7}
> 输出: 7

***逼近*** **:** 使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个变量，比如说 **sum** 为 **0** ，它将保存一个最大交替子阵和一个变量，比如说 **sumSoFar** ，将从 1 <sup>st</sup> 循环中的偶数索引开始的子阵和以及从奇数索引开始的和存储在 2 <sup>nd</sup> 循环中。
*   在两个循环的每次迭代中，将**和**更新为**最大值(和，sumSoFar)** 。
*   最后，返回存储在 **sum** 变量中的最大交替和。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum alternating
// sum of a subarray for the given array
int alternatingSum(int arr[],int n)
{
  int sum = 0;
  int sumSoFar = 0;

  // Traverse the array
  for (int i = 0; i < n; i++) {

    // Store sum of subarrays
    // starting at even indices
    if (i % 2 == 1) {

      sumSoFar -= arr[i];
    }
    else {

      sumSoFar = max(
        sumSoFar + arr[i], arr[i]);
    }

    // Update sum
    sum = max(sum, sumSoFar);
  }

  sumSoFar = 0;

  // Traverse the array
  for (int i = 1; i < n; i++) {

    // Store sum of subarrays
    // starting at odd indices
    if (i % 2 == 0) {
      sumSoFar -= arr[i];
    }
    else {
      sumSoFar = max(
        sumSoFar + arr[i], arr[i]);
    }

    // Update sum
    sum = max(sum, sumSoFar);
  }
  return sum;
}

// Driver code
int main()
{

  // Given Input
  int arr[] ={ -4, -10, 3, 5 };
  int n = sizeof(arr)/sizeof(arr[0]);

  // Function call
  int ans = alternatingSum(arr,n);

  cout<<ans<<endl;
  return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;

class GFG {

    // Function to find the maximum alternating
    // sum of a subarray for the given array
    public static int alternatingSum(int[] arr)
    {
        int sum = 0;
        int sumSoFar = 0;

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {

            // Store sum of subarrays
            // starting at even indices
            if (i % 2 == 1) {

                sumSoFar -= arr[i];
            }
            else {

                sumSoFar = Math.max(
                    sumSoFar + arr[i], arr[i]);
            }

            // Update sum
            sum = Math.max(sum, sumSoFar);
        }

        sumSoFar = 0;

        // Traverse the array
        for (int i = 1; i < arr.length; i++) {

            // Store sum of subarrays
            // starting at odd indices
            if (i % 2 == 0) {
                sumSoFar -= arr[i];
            }
            else {
                sumSoFar = Math.max(
                    sumSoFar + arr[i], arr[i]);
            }

            // Update sum
            sum = Math.max(sum, sumSoFar);
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given Input
        int arr[] = new int[] { -4, -10, 3, 5 };

        // Function call
        int ans = alternatingSum(arr);

        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to find the maximum alternating
# sum of a subarray for the given array
def alternatingSum(arr, n):
    sum_ = 0
    sumSoFar = 0

    # Traverse the array
    for i in range(n):

      # Store sum of subarrays
       # starting at even indices
        if i % 2 == 1:
            sumSoFar -= arr[i]
        else:
            sumSoFar = max(arr[i], sumSoFar + arr[i])

            # Update sum
        sum_ = max(sum_, sumSoFar)

    sumSoFar = 0

    # Traverse array
    for i in range(1, n):

      # Store sum of subarrays
      # starting at odd indices
        if i % 2 == 0:
            sumSoFar -= arr[i]
        else:
            sumSoFar = max(arr[i], sumSoFar + arr[i])
        sum_ = max(sum_, sumSoFar)

        # update sum
    return sum_

# given array
arr = [-4, -10, 3, 5]
n = len(arr)

# return sum
ans = alternatingSum(arr, n)
print(ans)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum alternating
// sum of a subarray for the given array
static int alternatingSum(int []arr,int n)
{
    int sum = 0;
    int sumSoFar = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Store sum of subarrays
        // starting at even indices
        if (i % 2 == 1)
        {
            sumSoFar -= arr[i];
        }
        else
        {
            sumSoFar = Math.Max(
            sumSoFar + arr[i], arr[i]);
        }

        // Update sum
        sum = Math.Max(sum, sumSoFar);
    }

    sumSoFar = 0;

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // Store sum of subarrays
        // starting at odd indices
        if (i % 2 == 0)
        {
            sumSoFar -= arr[i];
        }
        else
        {
            sumSoFar = Math.Max(
            sumSoFar + arr[i], arr[i]);
        }

        // Update sum
        sum = Math.Max(sum, sumSoFar);
    }
    return sum;
}

// Driver code
public static void Main()
{

    // Given Input
    int []arr = { -4, -10, 3, 5 };
    int n = arr.Length;

    // Function call
    int ans = alternatingSum(arr,n);

    Console.Write(ans);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// JavaScript implementation for the above approach
    // Function to find the maximum alternating
    // sum of a subarray for the given array
    function alternatingSum(arr)
    {
        var sum = 0;
        var sumSoFar = 0;

        // Traverse the array
        for (var i = 0; i < arr.length; i++) {

            // Store sum of subarrays
            // starting at even indices
            if (i % 2 == 1) {

                sumSoFar -= arr[i];
            }
            else {

                sumSoFar = Math.max(
                    sumSoFar + arr[i], arr[i]);
            }

            // Update sum
            sum = Math.max(sum, sumSoFar);
        }

        sumSoFar = 0;

        // Traverse the array
        for (var i = 1; i < arr.length; i++) {

            // Store sum of subarrays
            // starting at odd indices
            if (i % 2 == 0) {
                sumSoFar -= arr[i];
            }
            else {
                sumSoFar = Math.max(
                    sumSoFar + arr[i], arr[i]);
            }

            // Update sum
            sum = Math.max(sum, sumSoFar);
        }
        return sum;
    }

    // Driver code
        // Given Input
        var arr = new Array ( -4, -10, 3, 5 );

        // Function call
        var ans = alternatingSum(arr);
        document.write(ans);

    // This code is contributed by  shivanisinghss2110
</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)