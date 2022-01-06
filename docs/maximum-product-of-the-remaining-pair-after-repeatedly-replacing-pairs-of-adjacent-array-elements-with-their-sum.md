# 用相邻数组元素对的和重复替换后剩余对的最大乘积

> 原文:[https://www . geeksforgeeks . org/重复用其和替换相邻数组元素对后剩余对的最大乘积/](https://www.geeksforgeeks.org/maximum-product-of-the-remaining-pair-after-repeatedly-replacing-pairs-of-adjacent-array-elements-with-their-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在用它们的和重复替换一对相邻数组元素后，找到剩余对的最大乘积。

***注:**将阵势缩小为 2。*

**示例:**

> **输入:** arr[] = {2，3，5，6，7}
> **输出:** 130
> **解释:**
> 用 arr[1]和 arr[2]的和(即 3 + 5 = 8)替换 arr[1]和 arr[2]将 arr[]修改为{2，8，6，7}
> 用 arr[2]和 arr[3]的和(即 6 + 7 = 13)替换 arr[2]将 arr[]修改为{2，8，13}
> 
> **输入:** arr[] = {5，6 }
> T3】输出: 30

**方法:**给定的问题可以通过观察来解决。可以观察到，对于一个索引 **i** ， **X** 必须等于第一个 **i** 元素的和，即 arr[1] + arr[2] + arr[3] + … + arr[i]和 **Y** 必须等于其余元素的和，即 arr[i + 1] + arr[i + 2] +…+ arr[N]。现在，这个问题可以通过使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)并在每个索引处找到它与其余元素之和的乘积来解决。按照以下步骤解决问题:

*   将 **ans** 初始化为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 存储所需答案， **prefixSum** 初始化为 **0** 存储数组前缀和。
*   将数组元素的总和存储在一个变量中，比如说 **S** 。
*   [使用变量 **i** 在索引**【0，N–2】**的范围内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下操作:
    *   将**arr【I】**的值加到**前缀**上。
    *   将**前缀**的值存储在变量 **X** 中，将**(sum–前缀)**存储在变量 **Y** 中。
    *   如果 **(X * Y)** 的值大于 **ans** ，则更新 **ans** 为 **(X * Y)** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum product
// possible after repeatedly replacing
// pairs of adjacent array elements
// with their sum
void maxProduct(int arr[], int N)
{
    // Store the maximum product
    int max_product = INT_MIN;

    // Store the prefix sum
    int prefix_sum = 0;

    // Store the total sum of array
    int sum = 0;

    // Traverse the array to find
    // the total sum
    for (int i = 0; i < N; i++) {
        sum += arr[i];
    }

    // Iterate in the range [0, N-2]
    for (int i = 0; i < N - 1; i++) {

        // Add arr[i] to prefix_sum
        prefix_sum += arr[i];

        // Store the value of prefix_sum
        int X = prefix_sum;

        // Store the value of
        // (total sum - prefix sum)
        int Y = sum - prefix_sum;

        // Update the maximum product
        max_product = max(max_product,
                          X * Y);
    }

    // Print the answer
    cout << max_product;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 5, 6, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maxProduct(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{
  // Function to find the maximum product
  // possible after repeatedly replacing
  // pairs of adjacent array elements
  // with their sum
  static void maxProduct(int[] arr, int N)
  {
    // Store the maximum product
    int max_product = Integer.MIN_VALUE;

    // Store the prefix sum
    int prefix_sum = 0;

    // Store the total sum of array
    int sum = 0;

    // Traverse the array to find
    // the total sum
    for (int i = 0; i < N; i++)
    {
      sum += arr[i];
    }

    // Iterate in the range [0, N-2]
    for (int i = 0; i < N - 1; i++)
    {

      // Add arr[i] to prefix_sum
      prefix_sum += arr[i];

      // Store the value of prefix_sum
      int X = prefix_sum;

      // Store the value of
      // (total sum - prefix sum)
      int Y = sum - prefix_sum;

      // Update the maximum product
      max_product = Math.max(max_product, X * Y);
    }

    // Print the answer
    System.out.print(max_product);
  }

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 5, 6, 7 };
    int N = arr.length;
    maxProduct(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach
import sys

# Function to find the maximum product
# possible after repeatedly replacing
# pairs of adjacent array elements
# with their sum
def maxProduct(arr, N):

    # Store the maximum product
    max_product = -sys.maxsize;

    # Store the prefix sum
    prefix_sum = 0;

    # Store the total sum of array
    sum = 0;

    # Traverse the array to find
    # the total sum
    for i in range(N):
        sum += arr[i];

    # Iterate in the range [0, N-2]
    for i in range(N - 1):

        # Add arr[i] to prefix_sum
        prefix_sum += arr[i];

        # Store the value of prefix_sum
        X = prefix_sum;

        # Store the value of
        # (total sum - prefix sum)
        Y = sum - prefix_sum;

        # Update the maximum product
        max_product = max(max_product, X * Y);

    # Print the answer
    print(max_product);

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 5, 6, 7];
    N = len(arr);
    maxProduct(arr, N);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the maximum product
  // possible after repeatedly replacing
  // pairs of adjacent array elements
  // with their sum
  static void maxProduct(int[] arr, int N)
  {
    // Store the maximum product
    int max_product = Int32.MinValue;

    // Store the prefix sum
    int prefix_sum = 0;

    // Store the total sum of array
    int sum = 0;

    // Traverse the array to find
    // the total sum
    for (int i = 0; i < N; i++)
    {
      sum += arr[i];
    }

    // Iterate in the range [0, N-2]
    for (int i = 0; i < N - 1; i++)
    {

      // Add arr[i] to prefix_sum
      prefix_sum += arr[i];

      // Store the value of prefix_sum
      int X = prefix_sum;

      // Store the value of
      // (total sum - prefix sum)
      int Y = sum - prefix_sum;

      // Update the maximum product
      max_product = Math.Max(max_product, X * Y);
    }

    // Print the answer
    Console.WriteLine(max_product);
  } 

  // Driver code
  static void Main()
  {
    int[] arr = { 2, 3, 5, 6, 7 };
    int N = arr.Length;
    maxProduct(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the maximum product
    // possible after repeatedly replacing
    // pairs of adjacent array elements
    // with their sum
    function maxProduct(arr , N) {
        // Store the maximum product
        var max_product = Number.MIN_VALUE;

        // Store the prefix sum
        var prefix_sum = 0;

        // Store the total sum of array
        var sum = 0;

        // Traverse the array to find
        // the total sum
        for (i = 0; i < N; i++) {
            sum += arr[i];
        }

        // Iterate in the range [0, N-2]
        for (i = 0; i < N - 1; i++) {

            // Add arr[i] to prefix_sum
            prefix_sum += arr[i];

            // Store the value of prefix_sum
            var X = prefix_sum;

            // Store the value of
            // (total sum - prefix sum)
            var Y = sum - prefix_sum;

            // Update the maximum product
            max_product = Math.max(max_product, X * Y);
        }

        // Print the answer
        document.write(max_product);
    }

    // Driver Code

        var arr = [ 2, 3, 5, 6, 7 ];
        var N = arr.length;
        maxProduct(arr, N);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
130
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)