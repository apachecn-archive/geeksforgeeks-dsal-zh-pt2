# 在最多 C 次分裂给定数组后最大化第 k 个最大元素

> 原文:[https://www . geeksforgeeks . org/maximize-kth-最大元素-拆分后-给定数组-最多 c 次/](https://www.geeksforgeeks.org/maximize-kth-largest-element-after-splitting-the-given-array-at-most-c-times/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和两个正整数 **K** 和 **C** ，任务是将数组元素 **arr[]** 拆分为两部分**(不一定是整数)** **C** 后得到的最大元素个数最大化。打印 **-1** 如果不存在 **K <sup>th</sup>** 最大元素。

**注意:**必须进行拆分操作，直到数组**arr【】**的大小为 **≥ K** 。

**示例:**

> **输入:** arr[] = {5，8}，K = 1，C = 1
> **输出:** 8.0
> **说明:**无需执行任何操作。最终数组将是{8，5}，因此 8.0 是最大可实现值。
> 
> **输入:** arr[] = {5，9}，K = 3，C = 1
> **输出:** 4.5
> **说明:**值 9 可以拆分为 4.5 和 4.5。最终的数组将是{5，4.5，4.5}，其中第三个值是 4.5，这是最大可达到的值。

**方法:**给定的问题可以用答案上的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决。按照以下步骤解决给定的问题。

*   初始化两个变量，分别说**低**和**高**为 **0** 和 **10 <sup>9</sup>** ，代表二分搜索法可以执行的范围。
*   使用以下步骤执行二分搜索法:
    *   求**中间**的值为**(低+高)*0.5** 。
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将至少为**的元素计数**存储在变量中 **mid** 的值，比如说 **A** ，还可以找到变量中执行的操作数，比如说 **B** 。
    *   如果**(A≥K)****(b+ C≥K)**的值，则更新**低**的值为**中**。否则，将**高值**更新为**中值**。
*   完成上述步骤后，变量 **low** 中存储的值是合成的最大化**K<sup>th</sup>T5【最大化】元素。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the K-th maximum
// element after upto C operations
double maxKth(int arr[], int N,
              int C, int K)
{
    // Check for the base case
    if (N + C < K) {
        return -1;
    }
    // Stores the count iterations of BS
    int iter = 300;

    // Create the left and right bounds
    // of binary search
    double l = 0, r = 1000000000.0;

    // Perform binary search
    while (iter--) {

        // Find the value of mid
        double mid = (l + r) * 0.5;
        double a = 0;
        double b = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {
            a += int((double)arr[i] / mid);
            if ((double)arr[i] >= mid) {
                b++;
            }
        }

        // Update the ranges
        if (a >= K && b + C >= K) {
            l = mid;
        }
        else {
            r = mid;
        }
    }

    // Return the maximum value obtained
    return l;
}

// Driver Code
int main()
{
    int arr[] = { 5, 8 };
    int K = 1, C = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxKth(arr, N, C, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the K-th maximum
    // element after upto C operations
    static double maxKth(int arr[], int N, int C, int K)
    {

        // Check for the base case
        if (N + C < K) {
            return -1;
        }

        // Stores the count iterations of BS
        int iter = 300;

        // Create the left and right bounds
        // of binary search
        double l = 0, r = 1000000000.0;

        // Perform binary search
        while (iter-- > 0) {

            // Find the value of mid
            double mid = (l + r) * 0.5;
            double a = 0;
            double b = 0;

            // Traverse the array
            for (int i = 0; i < N; i++) {
                a += (int)((double)arr[i] / mid);
                if ((double)arr[i] >= mid) {
                    b++;
                }
            }

            // Update the ranges
            if (a >= K && b + C >= K) {
                l = mid;
            }
            else {
                r = mid;
            }
        }

        // Return the maximum value obtained
        return l;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 5, 8 };
        int K = 1, C = 1;
        int N = arr.length;

        System.out.println(maxKth(arr, N, C, K));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the K-th maximum
# element after upto C operations
def maxKth(arr, N, C, K):

    # Check for the base case
    if (N + C < K):
        return -1

    # Stores the count iterations of BS
    iter = 300

    # Create the left and right bounds
    # of binary search
    l = 0
    r = 1000000000.0

    # Perform binary search
    while (iter):
        iter = iter - 1
        # Find the value of mid
        mid = (l + r) * 0.5
        a = 0
        b = 0

        # Traverse the array
        for i in range(N) :
            a += arr[i] // mid
            if (arr[i] >= mid) :
                b += 1

        # Update the ranges
        if (a >= K and b + C >= K) :
                l = mid

        else :
                r = mid

    # Return the maximum value obtained
    return int(l)

# Driver Code
arr = [5, 8]
K = 1
C = 1
N = len(arr)

print(maxKth(arr, N, C, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find the K-th maximum
    // element after upto C operations
    static double maxKth(int []arr, int N, int C, int K)
    {

        // Check for the base case
        if (N + C < K) {
            return -1;
        }

        // Stores the count iterations of BS
        int iter = 300;

        // Create the left and right bounds
        // of binary search
        double l = 0, r = 1000000000.0;

        // Perform binary search
        while (iter-- > 0) {

            // Find the value of mid
            double mid = (l + r) * 0.5;
            double a = 0;
            double b = 0;

            // Traverse the array
            for (int i = 0; i < N; i++) {
                a += (int)((double)arr[i] / mid);
                if ((double)arr[i] >= mid) {
                    b++;
                }
            }

            // Update the ranges
            if (a >= K && b + C >= K) {
                l = mid;
            }
            else {
                r = mid;
            }
        }

        // Return the maximum value obtained
        return l;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 5, 8 };
        int K = 1, C = 1;
        int N = arr.Length;

        Console.Write(maxKth(arr, N, C, K));
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the K-th maximum
       // element after upto C operations
       function maxKth(arr, N,
           C, K)
       {

           // Check for the base case
           if (N + C < K) {
               return -1;
           }
           // Stores the count iterations of BS
           let iter = 300;

           // Create the left and right bounds
           // of binary search
           let l = 0, r = 1000000000.0;

           // Perform binary search
           while (iter--) {

               // Find the value of mid
               let mid = (l + r) * 0.5;
               let a = 0;
               let b = 0;

               // Traverse the array
               for (let i = 0; i < N; i++) {
                   a += Math.floor(arr[i] / mid);
                   if (arr[i] >= mid) {
                       b++;
                   }
               }

               // Update the ranges
               if (a >= K && b + C >= K) {
                   l = mid;
               }
               else {
                   r = mid;
               }
           }

           // Return the maximum value obtained
           return l;
       }

       // Driver Code
       let arr = [5, 8];
       let K = 1, C = 1;
       let N = arr.length;

       document.write(maxKth(arr, N, C, K));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N*log M)*
***辅助空间:** O(1)*