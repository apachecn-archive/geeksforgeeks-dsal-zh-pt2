# 最多移除一个子阵列后可能的最大子阵列总和

> 原文:[https://www . geeksforgeeks . org/max-subarray-最多移除一个 subarray 后的可能总和/](https://www.geeksforgeeks.org/maximum-subarray-sum-possible-after-removing-at-most-one-subarray/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在从给定数组中最多移除一个[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)后，找到任意子数组的[最大可能和。](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

**示例:**

> **输入:** arr[] = {-1，5，2，-1，6}
> **输出:** 13
> **解释:**
> 选择子阵{5，2，-1，6}并去掉子阵{-1}即可得到最大和。
> 
> **输入:** arr[] = {7，6，-1，-4，-5，7，1，-2，-3}
> **输出:** 21

**方法:**按照步骤解决问题:

*   初始化一个数组，比如说**设定[]** ，这样**设定【I】**存储范围**【0，I】**内任何子阵列的[最大子阵列和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。
*   初始化一个数组，比如说 **suffSum[]** ，这样 **suffSum[i]** 存储范围**【I，N–1】**内任何子阵列的[最大子阵列和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。
*   初始化一个变量，比如说**和**，在从给定阵列中移除任何子阵列后，存储[最大子阵列和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。
*   [从头开始遍历给定数组](https://www.geeksforgeeks.org/traverse-through-arraylist-in-forward-direction-in-java/)并使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)更新**假定[]** 。
*   [从头到尾遍历给定的数组](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/)，并使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)更新**后缀[]** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**并更新 **ans** 的值 **ans** 和**的最大值(假定[i] + postSum[i + 1])** 。
*   完成上述步骤后，打印**和**的值作为结果的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum
// subarray sum possible after
// removing at most one subarray
void maximumSum(int arr[], int n)
{
    int preSum[n];
    int sum = 0;
    int maxSum = 0;

    // Calculate the preSum[] array
    for(int i = 0; i < n; i++)
    {

        // Update the value of sum
        sum = max(arr[i], sum + arr[i]);

        // Update the value of maxSum
        maxSum = max(maxSum, sum);

        // Update the value of preSum[i]
        preSum[i] = maxSum;
    }

    sum = 0;
    maxSum = 0;

    int postSum[n + 1];

    // Calculate the postSum[] array
    for(int i = n - 1; i >= 0; i--)
    {

        // Update the value of sum
        sum = max(arr[i], sum + arr[i]);

        // Update the value of maxSum
        maxSum = max(maxSum, sum);

        // Update the value of postSum[i]
        postSum[i] = maxSum;
    }

    // Stores the resultant maximum
    // sum of subarray
    int ans = 0;

    for(int i = 0; i < n; i++)
    {

        // Update the value of ans
        ans = max(ans, preSum[i] + postSum[i]);
    }

    // Print the resultant sum
    cout << (ans);
}

// Driver Code
int main()
{
    int arr[] = { 7, 6, -1, -4, -5, 7, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    maximumSum(arr, n);

    return 0;
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find maximum
    // subarray sum possible after
    // removing at most one subarray
    public static void maximumSum(
        int arr[], int n)
    {
        long[] preSum = new long[n];

        long sum = 0;
        long maxSum = 0;

        // Calculate the preSum[] array
        for (int i = 0; i < n; i++) {

            // Update the value of sum
            sum = Math.max(arr[i],
                           sum + arr[i]);

            // Update the value of maxSum
            maxSum = Math.max(maxSum,
                              sum);

            // Update the value of preSum[i]
            preSum[i] = maxSum;
        }

        sum = 0;
        maxSum = 0;

        long[] postSum = new long[n + 1];

        // Calculate the postSum[] array
        for (int i = n - 1; i >= 0; i--) {

            // Update the value of sum
            sum = Math.max(arr[i],
                           sum + arr[i]);

            // Update the value of maxSum
            maxSum = Math.max(maxSum,
                              sum);

            // Update the value of postSum[i]
            postSum[i] = maxSum;
        }

        // Stores the resultant maximum
        // sum of subarray
        long ans = 0;

        for (int i = 0; i < n; i++) {

            // Update the value of ans
            ans = Math.max(ans,
                           preSum[i]
                               + postSum[i + 1]);
        }

        // Print the resultant sum
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 7, 6, -1, -4, -5, 7, 1 };
        maximumSum(arr, arr.length);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find maximum
# subarray sum possible after
# removing at most one subarray
def maximumSum(arr, n) :

    preSum = [0] * n

    sum = 0
    maxSum = 0

    # Calculate the preSum[] array
    for i in range(n):

        # Update the value of sum
        sum = max(arr[i], sum + arr[i])

        # Update the value of maxSum
        maxSum = max(maxSum,
                          sum)

        # Update the value of preSum[i]
        preSum[i] = maxSum

    sum = 0
    maxSum = 0

    postSum = [0] * (n + 1)

    # Calculate the postSum[] array
    for i in range(n-1, -1, -1):

        # Update the value of sum
        sum = max(arr[i],
                       sum + arr[i])

        # Update the value of maxSum
        maxSum = max(maxSum,
                          sum)

        # Update the value of postSum[i]
        postSum[i] = maxSum

    # Stores the resultant maximum
    # sum of subarray
    ans = 0

    for i in range(n):

        # Update the value of ans
        ans = max(ans,
                       preSum[i]
                           + postSum[i + 1])

    # Print resultant sum
    print(ans)

# Driver code
arr = [ 7, 6, -1, -4, -5, 7, 1]
N = len(arr)
maximumSum(arr, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find maximum
// subarray sum possible after
// removing at most one subarray
public static void maximumSum(int[] arr, int n)
{
    long[] preSum = new long[n];
    long sum = 0;
    long maxSum = 0;

    // Calculate the preSum[] array
    for(int i = 0; i < n; i++)
    {

        // Update the value of sum
        sum = Math.Max(arr[i], sum + arr[i]);

        // Update the value of maxSum
        maxSum = Math.Max(maxSum, sum);

        // Update the value of preSum[i]
        preSum[i] = maxSum;
    }

    sum = 0;
    maxSum = 0;

    long[] postSum = new long[n + 1];

    // Calculate the postSum[] array
    for(int i = n - 1; i >= 0; i--)
    {

        // Update the value of sum
        sum = Math.Max(arr[i], sum + arr[i]);

        // Update the value of maxSum
        maxSum = Math.Max(maxSum, sum);

        // Update the value of postSum[i]
        postSum[i] = maxSum;
    }

    // Stores the resultant maximum
    // sum of subarray
    long ans = 0;

    for(int i = 0; i < n; i++)
    {

        // Update the value of ans
        ans = Math.Max(ans, preSum[i] +
                            postSum[i + 1]);
    }

    // Print the resultant sum
    Console.WriteLine(ans);
}

// Driver code
static void Main()
{
    int[] arr = { 7, 6, -1, -4, -5, 7, 1 };
    maximumSum(arr, arr.Length);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    // Function to find maximum
    // subarray sum possible after
    // removing at most one subarray
    function maximumSum(
        arr, n)
    {
        let preSum = Array.from({length: n}, (_, i) => 0);

        let sum = 0;
        let maxSum = 0;

        // Calculate the preSum[] array
        for (let i = 0; i < n; i++) {

            // Update the value of sum
            sum = Math.max(arr[i],
                           sum + arr[i]);

            // Update the value of maxSum
            maxSum = Math.max(maxSum,
                              sum);

            // Update the value of preSum[i]
            preSum[i] = maxSum;
        }

        sum = 0;
        maxSum = 0;

        let postSum = Array.from({length: n+1}, (_, i) => 0);

        // Calculate the postSum[] array
        for (let i = n - 1; i >= 0; i--) {

            // Update the value of sum
            sum = Math.max(arr[i],
                           sum + arr[i]);

            // Update the value of maxSum
            maxSum = Math.max(maxSum,
                              sum);

            // Update the value of postSum[i]
            postSum[i] = maxSum;
        }

        // Stores the resultant maximum
        // sum of subarray
        let ans = 0;

        for (let i = 0; i < n; i++) {

            // Update the value of ans
            ans = Math.max(ans,
                           preSum[i]
                               + postSum[i + 1]);
        }

        // Print the resultant sum
        document.write(ans);
    }

  // Driver Code

    let arr = [ 7, 6, -1, -4, -5, 7, 1 ];
    maximumSum(arr, arr.length);

</script>
```

**Output:** 

```
21
```

***时间复杂度:*** *O(N)*
***辅助空间:*** *O(N)*