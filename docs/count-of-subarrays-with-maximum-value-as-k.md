# 最大值为 K 的子阵列计数

> 原文:[https://www . geeksforgeeks . org/最大值为 k 的子阵列计数/](https://www.geeksforgeeks.org/count-of-subarrays-with-maximum-value-as-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。任务是找到**最大值**等于 **K 的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量**

**示例:**

> **输入:** arr[ ] = {2，1，3，4}，K = 3
> **输出:** 3
> **解释:**
> 最大值等于 K 的子阵为{2，1，3 }、{ 1，3 }、{ 3 }，因此答案为 3。
> 
> **输入:** arr[ ] = {1，2，3}，K = 1。
> T3】输出: 1

**方式:**在[阵](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量等于最大不大于 **K** 的[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量减去最大不大于 **K-1 的[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。**参考此处统计最大值大于 **K 的[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)个数**按照以下步骤解决问题:

*   初始化变量 say，**计数 1** 为 **0** 计算最大不大于 **K-1 的[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)个数。**
*   初始化变量 say，**计数 2** 为 **0** 计算最大不大于 **K.** 的[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)数量
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，比如**total subarray(arr，N，K)** 来计算最大不大于 **K** 的[subarray](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的个数，并执行以下步骤:
    *   初始化变量 say， **ans 为 0** 存储[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的计数，最大值不大于 **K.**
    *   [在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**范围内迭代，执行以下步骤。
        *   如果**arr【I】**的值大于 **K，**则将 **i** 的值增加**1**[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
        *   将变量**计数**初始化为 **0** ，以存储可能的总计数[子阵列。](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)
        *   [在](https://www.geeksforgeeks.org/range-based-loop-c/)范围内迭代，直到 **i** 小于 **N** 且**arr【I】**小于等于**k**
            *   将**I****的数值增加 **1 计算**。**
        *   将**(计数*(计数+1))/2** 的值加到 **ans 的值上。**
    *   返回 **ans 的值。**
*   通过调用函数**计算最大不大于 **K-1** 的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，总计子阵列(arr，N，K-1)** 并存储在 **count1 中。**
*   通过调用函数**计算最大不大于 **K** 的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，总计子阵列(arr，N，K)** 并存储在**计数 2 中。**
*   将**(count 2–count 1)**的值存储在**和**的最终值中并打印出来。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the subarrays with maximum
// not greater than K
int totalSubarrays(int arr[], int n, int k)
{
    int ans = 0, i = 0;

    while (i < n) {
        // If arr[i]>k then arr[i] cannot be
        // a part of any subarray.
        if (arr[i] > k) {
            i++;
            continue;
        }

        int count = 0;
        // Count the number of elements where
        // arr[i] is not greater than k.
        while (i < n && arr[i] <= k) {
            i++;
            count++;
        }

        // Summation of all possible subarrays
        // in the variable ans.
        ans += ((count * (count + 1)) / 2);
    }

    return ans;
}

// Function to count the subarrays with
// maximum value is equal to K
int countSubarrays(int arr[], int n, int k)
{
    // Stores count of subarrays with max <= k - 1.
    int count1 = totalSubarrays(arr, n, k - 1);

    // Stores count of subarrays with max >= k + 1.
    int count2 = totalSubarrays(arr, n, k);

    // Stores count of subarrays with max = k.
    int ans = count2 - count1;

    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int n = 4, k = 3;
    int arr[] = { 2, 1, 3, 4 };

    // Function Call
    cout << countSubarrays(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    // Function to count the subarrays with maximum
    // not greater than K
    static int totalSubarrays(int arr[], int n, int k)
    {
        int ans = 0, i = 0;

        while (i < n) {
            // If arr[i]>k then arr[i] cannot be
            // a part of any subarray.
            if (arr[i] > k) {
                i++;
                continue;
            }

            int count = 0;
            // Count the number of elements where
            // arr[i] is not greater than k.
            while (i < n && arr[i] <= k) {
                i++;
                count++;
            }

            // Summation of all possible subarrays
            // in the variable ans.
            ans += ((count * (count + 1)) / 2);
        }

        return ans;
    }

    // Function to count the subarrays with
    // maximum value is equal to K
    static int countSubarrays(int arr[], int n, int k)
    {
        // Stores count of subarrays with max <= k - 1.
        int count1 = totalSubarrays(arr, n, k - 1);

        // Stores count of subarrays with max >= k + 1.
        int count2 = totalSubarrays(arr, n, k);

        // Stores count of subarrays with max = k.
        int ans = count2 - count1;

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int n = 4, k = 3;
        int arr[] = { 2, 1, 3, 4 };

        // Function Call

        System.out.println(countSubarrays(arr, n, k));
      // This code is contributed by Potta Lokesh
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count the subarrays with maximum
# not greater than K
def totalSubarrays(arr, n, k):

    ans = 0
    i = 0

    while (i < n):

        # If arr[i]>k then arr[i] cannot be
        # a part of any subarray.
        if (arr[i] > k):
            i += 1
            continue

        count = 0

        # Count the number of elements where
        # arr[i] is not greater than k.
        while (i < n and arr[i] <= k):
            i += 1
            count += 1

        # Summation of all possible subarrays
        # in the variable ans.
        ans += ((count * (count + 1)) // 2)

    return ans

# Function to count the subarrays with
# maximum value is equal to K
def countSubarrays(arr, n, k):

    # Stores count of subarrays with max <= k - 1.
    count1 = totalSubarrays(arr, n, k - 1)

    # Stores count of subarrays with max >= k + 1.
    count2 = totalSubarrays(arr, n, k)

    # Stores count of subarrays with max = k.
    ans = count2 - count1

    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 4
    k = 3
    arr = [ 2, 1, 3, 4 ]

    # Function Call
    print(countSubarrays(arr, n, k))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG
{
    // Function to count the subarrays with maximum
    // not greater than K
    static int totalSubarrays(int[] arr, int n, int k)
    {
        int ans = 0, i = 0;

        while (i < n)
        {

            // If arr[i]>k then arr[i] cannot be
            // a part of any subarray.
            if (arr[i] > k) {
                i++;
                continue;
            }

            int count = 0;

            // Count the number of elements where
            // arr[i] is not greater than k.
            while (i < n && arr[i] <= k) {
                i++;
                count++;
            }

            // Summation of all possible subarrays
            // in the variable ans.
            ans += ((count * (count + 1)) / 2);
        }

        return ans;
    }

    // Function to count the subarrays with
    // maximum value is equal to K
    static int countSubarrays(int[] arr, int n, int k)
    {
        // Stores count of subarrays with max <= k - 1.
        int count1 = totalSubarrays(arr, n, k - 1);

        // Stores count of subarrays with max >= k + 1.
        int count2 = totalSubarrays(arr, n, k);

        // Stores count of subarrays with max = k.
        int ans = count2 - count1;

        return ans;
    }
    static void Main()
    {
        // Given Input
        int n = 4, k = 3;
        int[] arr = { 2, 1, 3, 4 };

        // Function Call

        Console.WriteLine(countSubarrays(arr, n, k));
    }
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to count the subarrays with maximum
       // not greater than K
       function totalSubarrays(arr, n, k) {
           let ans = 0, i = 0;

           while (i < n) {
               // If arr[i]>k then arr[i] cannot be
               // a part of any subarray.
               if (arr[i] > k) {
                   i++;
                   continue;
               }

               let count = 0;
               // Count the number of elements where
               // arr[i] is not greater than k.
               while (i < n && arr[i] <= k) {
                   i++;
                   count++;
               }

               // Summation of all possible subarrays
               // in the variable ans.
               ans += (Math.floor((count * (count + 1)) / 2));
           }

           return ans;
       }

       // Function to count the subarrays with
       // maximum value is equal to K
       function countSubarrays(arr, n, k) {
           // Stores count of subarrays with max <= k - 1.
           let count1 = totalSubarrays(arr, n, k - 1);

           // Stores count of subarrays with max >= k + 1.
           let count2 = totalSubarrays(arr, n, k);

           // Stores count of subarrays with max = k.
           let ans = count2 - count1;

           return ans;
       }

       // Driver Code

       // Given Input
       let n = 4, k = 3;
       let arr = [2, 1, 3, 4];

       // Function Call
       document.write(countSubarrays(arr, n, k));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)