# 将一个阵列分割成三个具有递增总和的连续子阵列的方法计数

> 原文:[https://www . geeksforgeeks . org/将一个数组拆分为三个连续子数组的方法计数-具有递增总和/](https://www.geeksforgeeks.org/count-of-ways-to-split-an-array-into-three-contiguous-subarrays-having-increasing-sum/)

给定一个由非负整数组成的数组**arr【】**，任务是找出将数组拆分为三个非空的连续子数组的方法，使它们各自的元素之和按递增顺序排列。

**示例:**

> **输入:** arr[] = {2，3，1，7}
> **输出:** 2
> **解释:**
> {{2}、{3，1}、{7}}、{{2}、{3}、{1，7}}是可能的拆分。
> 
> **输入:** arr[] = {1，2，0 }
> T3】输出: 0

**方法:**思路是使用[前缀后缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)技术。按照以下步骤解决问题:

*   生成[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和后缀和数组。
*   初始化两个指针 **s** 和 **e** 求第二个子阵列的和。
*   迭代数组，当 **curr_subarray_sum** 小于**prefix _ sum【s–1】**时，用**arr【e】**递增 **curr_subarray_sum** ，并继续递增 **e** 。
*   每当 **curr_subarray_sum** 为≥ **前缀 _ sum[s–1]**时，检查 **curr_subarray_sum** 是否为≤ **后缀 _sum[e]** 。如果发现为真，增加**计数**。
*   将 **curr_subarray_sum** 减少**arr**，增加 **s** 。
*   重复以上步骤，最后打印**计数**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the number of ways
// to split array into three contiguous
// subarrays of the required type
int findCount(int arr[], int n)
{

    // Stores the prefix sums
    int prefix_sum[n];

    prefix_sum[0] = arr[0];

    for(int i = 1; i < n; i++)
        prefix_sum[i] = prefix_sum[i - 1] + arr[i];

    // Stores the suffix sums
    int suffix_sum[n];

    suffix_sum[n - 1] = arr[n - 1];

    for(int i = n - 2; i >= 0; i--)
        suffix_sum[i] = suffix_sum[i + 1] + arr[i];

    int s = 1, e = 1;
    int curr_subarray_sum = 0, count = 0;

    // Traverse the given array
    while (s < n - 1 && e < n - 1)
    {

        // Updating curr_subarray_sum until
        // it is less than prefix_sum[s-1]
        while (e < n - 1 && curr_subarray_sum <
               prefix_sum[s - 1])
        {
            curr_subarray_sum += arr[e++];
        }

        if (curr_subarray_sum <= suffix_sum[e])
        {

            // Increase count
            count++;
        }

        // Decrease curr_subarray_sum by arr[s[]
        curr_subarray_sum -= arr[s++];
    }

    // Return count
    return count;
}

// Driver code
int32_t main()
{
    int arr[] = { 2, 3, 1, 7 };
    int n = sizeof arr / sizeof arr[0];

    cout << (findCount(arr, n));
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to count the number of ways
    // to split array into three contiguous
    // subarrays of the required type
    static int findCount(int arr[], int n)
    {

        // Stores the prefix sums
        int[] prefix_sum = new int[n];

        prefix_sum[0] = arr[0];

        for (int i = 1; i < n; i++)
            prefix_sum[i]
                = prefix_sum[i - 1] + arr[i];

        // Stores the suffix sums
        int[] suffix_sum = new int[n];

        suffix_sum[n - 1] = arr[n - 1];

        for (int i = n - 2; i >= 0; i--)
            suffix_sum[i]
                = suffix_sum[i + 1] + arr[i];

        int s = 1, e = 1;
        int curr_subarray_sum = 0, count = 0;

        // Traverse the given array
        while (s < n - 1 && e < n - 1) {

            // Updating curr_subarray_sum until
            // it is less than prefix_sum[s-1]
            while (e < n - 1
                   && curr_subarray_sum
                          < prefix_sum[s - 1]) {
                curr_subarray_sum += arr[e++];
            }

            if (curr_subarray_sum <= suffix_sum[e]) {
                // Increase count
                count++;
            }

            // Decrease curr_subarray_sum by arr[s[]
            curr_subarray_sum -= arr[s++];
        }

        // Return count
        return count;
    }

    // Driver Code
    public static void main(String args[])
    {

        int[] arr = { 2, 3, 1, 7 };
        int n = arr.length;
        System.out.println(findCount(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number of ways
# to split array into three contiguous
# subarrays of the required type
def findCount(arr, n):

    # Stores the prefix sums
    prefix_sum = [0 for x in range(n)]
    prefix_sum[0] = arr[0]

    for i in range(1, n):
        prefix_sum[i] = prefix_sum[i - 1] + arr[i]

    # Stores the suffix sums
    suffix_sum = [0 for x in range(n)]

    suffix_sum[n - 1] = arr[n - 1]

    for i in range(n - 2, -1, -1):
        suffix_sum[i] = suffix_sum[i + 1] + arr[i]

    s = 1
    e = 1
    curr_subarray_sum = 0
    count = 0

    #Traverse the given array
    while (s < n - 1 and e < n - 1):

        # Updating curr_subarray_sum until
        # it is less than prefix_sum[s-1]
        while (e < n - 1 and
               curr_subarray_sum < prefix_sum[s - 1]):
            curr_subarray_sum += arr[e]
            e += 1

        if (curr_subarray_sum <= suffix_sum[e]):

            # Increase count
            count += 1

        # Decrease curr_subarray_sum by arr[s[]
        curr_subarray_sum -= arr[s]
        s += 1

    # Return count
    return count

# Driver code
arr = [ 2, 3, 1, 7 ]
n = len(arr)

print(findCount(arr, n))

# This code is contributed by Stream_Cipher
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to count the number of ways
  // to split array into three contiguous
  // subarrays of the required type
  static int findCount(int []arr, int n)
  {

    // Stores the prefix sums
    int[] prefix_sum = new int[n];

    prefix_sum[0] = arr[0];

    for (int i = 1; i < n; i++)
      prefix_sum[i] = prefix_sum[i - 1] + arr[i];

    // Stores the suffix sums
    int[] suffix_sum = new int[n];

    suffix_sum[n - 1] = arr[n - 1];

    for (int i = n - 2; i >= 0; i--)
      suffix_sum[i] = suffix_sum[i + 1] + arr[i];

    int s = 1, e = 1;
    int curr_subarray_sum = 0, count = 0;

    // Traverse the given array
    while (s < n - 1 && e < n - 1)
    {

      // Updating curr_subarray_sum until
      // it is less than prefix_sum[s-1]
      while (e < n - 1 &&
             curr_subarray_sum < prefix_sum[s - 1])
      {
        curr_subarray_sum += arr[e++];
      }

      if (curr_subarray_sum <= suffix_sum[e])
      {
        // Increase count
        count++;
      }

      // Decrease curr_subarray_sum by arr[s[]
      curr_subarray_sum -= arr[s++];
    }

    // Return count
    return count;
  }

  // Driver Code
  public static void Main(String []args)
  {

    int[] arr = { 2, 3, 1, 7 };
    int n = arr.Length;
    Console.WriteLine(findCount(arr, n));
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

   // Function to count the number of ways
    // to split array into three contiguous
    // subarrays of the required type
    function findCount(arr, n)
    {

        // Stores the prefix sums
        let prefix_sum = Array.from({length: n},
        (_, i) => 0);

        prefix_sum[0] = arr[0];

        for (let i = 1; i < n; i++)
            prefix_sum[i]
                = prefix_sum[i - 1] + arr[i];

        // Stores the suffix sums
        let suffix_sum = Array.from({length: n},
        (_, i) => 0);

        suffix_sum[n - 1] = arr[n - 1];

        for (let i = n - 2; i >= 0; i--)
            suffix_sum[i]
                = suffix_sum[i + 1] + arr[i];

        let s = 1, e = 1;
        let curr_subarray_sum = 0, count = 0;

        // Traverse the given array
        while (s < n - 1 && e < n - 1) {

            // Updating curr_subarray_sum until
            // it is less than prefix_sum[s-1]
            while (e < n - 1
                   && curr_subarray_sum
                          < prefix_sum[s - 1]) {
                curr_subarray_sum += arr[e++];
            }

            if (curr_subarray_sum <= suffix_sum[e]) {
                // Increase count
                count++;
            }

            // Decrease curr_subarray_sum by arr[s[]
            curr_subarray_sum -= arr[s++];
        }

        // Return count
        return count;
    }

// Driver Code

        let arr = [ 2, 3, 1, 7 ];
        let n = arr.length;
        document.write(findCount(arr, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)