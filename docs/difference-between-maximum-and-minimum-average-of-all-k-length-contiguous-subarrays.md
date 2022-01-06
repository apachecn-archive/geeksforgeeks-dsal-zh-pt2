# 所有 K 长度连续子阵列的最大和最小平均值之差

> 原文:[https://www . geeksforgeeks . org/所有 k 长度连续子阵列的最大和最小平均值之差/](https://www.geeksforgeeks.org/difference-between-maximum-and-minimum-average-of-all-k-length-contiguous-subarrays/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**和一个整数 **K，**的任务是打印长度为 **K** 的相邻[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大值和最小值[平均值之间的差值。](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)

**示例:**

> **输入:** arr[ ] = {3，8，9，15}，K = 2
> **输出:** 6.5
> **解释:**
> 长度为 2 的所有子阵分别为{3，8}、{8，9}、{9，15}，它们的平均值分别为(3+8)/2 = 5.5、(8+9)/2 = 8.5 和(9+15)/2 = 12.0。
> 因此，最大值(=12.0)和最小值(=5.5)之差为 12.0 -5.5 = 6.5。
> 
> **输入:** arr[] = {17，6.2，19，3.4}，K = 3
> T3】输出: 4.533

**天真法:**最简单的方法是求出大小为 **K** 的每个相邻[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)，然后求出这些值的最大值和最小值，并打印出它们的差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// averages of the maximum and the minimum
// subarrays of length k
double Avgdifference(double arr[], int N, int K)
{

    // Stores min and max sum
    double min = 1000000, max = -1;

    // Iterate through starting points
    for (int i = 0; i <= N - K; i++) {
        double sum = 0;

        // Sum up next K elements
        for (int j = 0; j < K; j++) {
            sum += arr[i + j];
        }

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return the difference between max
    // and min average
    return (max - min) / K;
}

// Driver Code
int main()
{
    // Given Input
    double arr[] = { 3, 8, 9, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    // Function Call
    cout << Avgdifference(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

  // Function to find the difference between
  // averages of the maximum and the minimum
  // subarrays of length k
  static double Avgdifference(double arr[], int N, int K)
  {

    // Stores min and max sum
    double min = 1000000, max = -1;

    // Iterate through starting points
    for (int i = 0; i <= N - K; i++) {
      double sum = 0;

      // Sum up next K elements
      for (int j = 0; j < K; j++) {
        sum += arr[i + j];
      }

      // Update max and min moving sum
      if (min > sum)
        min = sum;
      if (max < sum)
        max = sum;
    }

    // Return the difference between max
    // and min average
    return (max - min) / K;
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given Input
    double arr[] = { 3, 8, 9, 15 };
    int N =arr.length;
    int K = 2;

    // Function Call

    System.out.println( Avgdifference(arr, N, K));
  }
}

// This code is contribiuted by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the difference between
# averages of the maximum and the minimum
# subarrays of length k
def Avgdifference(arr, N, K):

    # Stores min and max sum
    min = 1000000;
    max = -1;

    # Iterate through starting points
    for i in range(N - K + 1):
        sum = 0;

        # Sum up next K elements
        for j in range(K):
            sum += arr[i + j];

        # Update max and min moving sum
        if (min > sum):
            min = sum;
        if (max < sum):
            max = sum;

    # Return the difference between max
    # and min average
    return (max - min) / K;

# Driver Code

# Given Input
arr = [3, 8, 9, 15];
N = len(arr);
K = 2;

# Function Call
print(Avgdifference(arr, N, K));

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the difference between
// averages of the maximum and the minimum
// subarrays of length k
static double Avgdifference(double []arr, int N, int K)
{

    // Stores min and max sum
    double min = 1000000, max = -1;

    // Iterate through starting points
    for(int i = 0; i <= N - K; i++)
    {
        double sum = 0;

        // Sum up next K elements
        for(int j = 0; j < K; j++)
        {
            sum += arr[i + j];
        }

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return the difference between max
    // and min average
    return(max - min) / K;
}

// Driver Code
public static void Main (String[] args)
{

    // Given Input
    double []arr = { 3, 8, 9, 15 };
    int N = arr.Length;
    int K = 2;

    // Function Call
    Console.Write(Avgdifference(arr, N, K));
}
}

// This code is contribiuted by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the difference between
// averages of the maximum and the minimum
// subarrays of length k
function Avgdifference(arr, N, K) {

    // Stores min and max sum
    let min = 1000000, max = -1;

    // Iterate through starting points
    for (let i = 0; i <= N - K; i++) {
        let sum = 0;

        // Sum up next K elements
        for (let j = 0; j < K; j++) {
            sum += arr[i + j];
        }

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return the difference between max
    // and min average
    return (max - min) / K;
}

// Driver Code

// Given Input
let arr = [3, 8, 9, 15];
let N = arr.length;
let K = 2;

// Function Call
document.write(Avgdifference(arr, N, K));

</script>
```

**Output**

```
6.5
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化。按照以下步骤解决问题:

*   找出范围**【0，K-1】**内子阵列的和，并将其存储在一个变量中，比如**和**。
*   初始化两个变量，比如**最大**和**最小**，以存储任何大小的子阵列的最大和最小和 **K.**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【K，N-K+1】**，并执行以下步骤:
    *   移除元素**arr【I-K】**并将元素**arr【I】**添加到大小为 **K.** 的窗口中，即将 **sum** 更新为**sum+arr【I】-arr【I-K】。**
    *   将 **min** 更新为 **min** 和**之和的最小值，**并将 **max** 更新为 **max** 和**之和**的最大值。
*   最后，完成以上步骤后，将答案打印为 **(max-min)/K.**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// the maximum and minimum subarrays of
// length K
double Avgdifference(double arr[], int N, int K)
{

    // Stores the sum of subarray over the
    // range [0, K]
    double sum = 0;
    // Iterate over the range [0, K]
    for (int i = 0; i < K; i++)
        sum += arr[i];

    // Store min and max sum
    double min = sum;
    double max = sum;

    // Iterate over the range [K, N-K]
    for (int i = K; i <= N - K + 1; i++) {

        // Increment sum by arr[i]-arr[i-K]
        sum += arr[i] - arr[i - K];

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return difference between max and min
    // average
    return (max - min) / K;
}
// Driver Code
int main()
{
    // Given Input
    double arr[] = { 3, 8, 9, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    // Function Call
    cout << Avgdifference(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the difference between
// the maximum and minimum subarrays of
// length K
static double Avgdifference(double arr[], int N, int K)
{

    // Stores the sum of subarray over the
    // range [0, K]
    double sum = 0;

    // Iterate over the range [0, K]
    for(int i = 0; i < K; i++)
        sum += arr[i];

    // Store min and max sum
    double min = sum;
    double max = sum;

    // Iterate over the range [K, N-K]
    for(int i = K; i <= N - K + 1; i++)
    {

        // Increment sum by arr[i]-arr[i-K]
        sum += arr[i] - arr[i - K];

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return difference between max and min
    // average
    return(max - min) / K;
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    double arr[] = { 3, 8, 9, 15 };
    int N = arr.length;
    int K = 2;

    // Function Call
    System.out.println(Avgdifference(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find the difference between
# the maximum and minimum subarrays of
# length K
def Avgdifference(arr, N, K):

    # Stores the sum of subarray over the
    # range [0, K]
    sum = 0
    # Iterate over the range [0, K]
    for i in range(K):
        sum += arr[i]

    # Store min and max sum
    min = sum
    max = sum

    # Iterate over the range [K, N-K]
    for i in range(K,N - K + 2,1):

        # Increment sum by arr[i]-arr[i-K]
        sum += arr[i] - arr[i - K]

        # Update max and min moving sum
        if (min > sum):
            min = sum
        if (max < sum):
            max = sum

    # Return difference between max and min
    # average
    return (max - min) / K

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [3, 8, 9, 15]
    N = len(arr)
    K = 2

    # Function Call
    print(Avgdifference(arr, N, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the difference between
// the maximum and minimum subarrays of
// length K
static double Avgdifference(double []arr, int N, int K)
{

    // Stores the sum of subarray over the
    // range [0, K]
    double sum = 0;

    // Iterate over the range [0, K]
    for(int i = 0; i < K; i++)
        sum += arr[i];

    // Store min and max sum
    double min = sum;
    double max = sum;

    // Iterate over the range [K, N-K]
    for(int i = K; i <= N - K + 1; i++)
    {

        // Increment sum by arr[i]-arr[i-K]
        sum += arr[i] - arr[i - K];

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return difference between max and min
    // average
    return(max - min) / K;
}

// Driver Code
public static void Main (String[] args)
{

    // Given Input
    double []arr = { 3, 8, 9, 15 };
    int N = arr.Length;
    int K = 2;

    // Function Call
    Console.Write(Avgdifference(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to find the difference between
// the maximum and minimum subarrays of
// length K
function Avgdifference(arr, N, K)
{

    // Stores the sum of subarray over the
    // range [0, K]
    let sum = 0;

    // Iterate over the range [0, K]
    for(let i = 0; i < K; i++)
        sum += arr[i];

    // Store min and max sum
    let min = sum;
    let max = sum;

    // Iterate over the range [K, N-K]
    for(let i = K; i <= N - K + 1; i++)
    {

        // Increment sum by arr[i]-arr[i-K]
        sum += arr[i] - arr[i - K];

        // Update max and min moving sum
        if (min > sum)
            min = sum;
        if (max < sum)
            max = sum;
    }

    // Return difference between max and min
    // average
    return(max - min) / K;
}

// Driver Code

    // Given Input
    let arr = [ 3, 8, 9, 15 ];
    let N = arr.length;
    let K = 2;

    // Function Call
    document.write(Avgdifference(arr, N, K));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
6.5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)