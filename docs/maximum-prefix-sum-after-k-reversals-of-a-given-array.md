# 给定数组 K 次反转后的最大前缀和

> 原文:[https://www . geesforgeks . org/max-prefix-sum-after-k-reverses-of-a-给定数组/](https://www.geeksforgeeks.org/maximum-prefix-sum-after-k-reversals-of-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是在给定数组的 **K** 次反转后找到最大[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

**示例:**

> **输入:** arr[] = {1，5，8，9，11，2}，K = 1
> **输出:** 36
> **说明:**反阵一次。因此，数组变成了{2，11，9，8，5，1}。最大前缀总和= 2 + 11 + 9 + 8 + 5 + 1 = 36。
> 
> **输入:** arr[] = {5，6，-4，3，-2，-10}，K = 2
> **输出:** 11
> **说明:**反阵两次。因此，数组变成{5，6，-4，3，-2，-10}。最大前缀总和= 5 + 6=11。

**天真法:**最简单的方法是[反转数组](https://www.geeksforgeeks.org/reverse-an-array-in-java/) **K 次**，在 **K 次反转**后，通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到[最大前缀和](https://www.geeksforgeeks.org/maximum-prefix-sum-given-range/)可能，打印最大和。
***时间复杂度:** O(N * K)*
***辅助空间:** O(1)*

**高效进场:**优化上述进场，思路是基于观察[如果 **K 为奇数**](Maximum prefix sum after K reversals of the given array) ，那么阵变反。否则，数组保持不变。所以如果 **K 为奇数**，求最大后缀和。否则，求最大前缀和。按照以下步骤解决问题:

*   将**求和**初始化为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 存储所需答案。
*   [若 **K** 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，[反阵](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/) **arr[]** 。
*   将 **currSum** 初始化为 **0** 来存储元素的前缀和。
*   使用变量 **i** 遍历数组 **arr[]** ，并执行以下操作:
    *   将**arr【I】**添加到变量 **currSum** 中。
    *   如果 **currSum** 的值大于**之和**，则将**之和**更新为 **currSum** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum prefix
// sum after K reversals of the array
int maxSumAfterKReverse(int arr[],
                        int K, int N)
{
    // Stores the required sum
    int sum = INT_MIN;

    // If K is odd, reverse the array
    if (K & 1)
        reverse(arr, arr + N);

    // Store current prefix sum of array
    int currsum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Add arr[i] to currsum
        currsum += arr[i];

        // Update maximum prefix sum
        // till now
        sum = max(sum, currsum);
    }

    // Print the answer
    cout << sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 8, 9, 11, 2 };
    int K = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxSumAfterKReverse(arr, K, N);

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

  // Function to find the maximum prefix
  // sum after K reversals of the array
  static void maxSumAfterKReverse(Integer arr[], int K, int N)
  {

    // Stores the required sum
    int sum = Integer.MIN_VALUE;

    // If K is odd, reverse the array
    if (K % 2 != 0)
      Collections.reverse(Arrays.asList(arr));

    // Store current prefix sum of array
    int currsum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

      // Add arr[i] to currsum
      currsum += arr[i];

      // Update maximum prefix sum
      // till now
      sum = Math.max(sum, currsum);
    }

    // Print the answer
    System.out.print(sum);
  }

  // Driver Code
  public static void main(String[] args)
  {
    Integer[] arr = { 1, 5, 8, 9, 11, 2 };
    int K = 1;
    int N = arr.length;

    // Function Call
    maxSumAfterKReverse(arr, K, N);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the maximum prefix
# sum after K reversals of the array
def maxSumAfterKReverse(arr, K, N) :

    # Stores the required sum
    sum = -sys.maxsize - 1

    # If K is odd, reverse the array
    if (K & 1) :
        arr.reverse()

    # Store current prefix sum of array
    currsum = 0

    # Traverse the array arr[]
    for i in range(N):

        # Add arr[i] to currsum
        currsum += arr[i]

        # Update maximum prefix sum
        # till now
        sum = max(sum, currsum)

    # Prthe answer
    print(sum)

# Driver Code
arr = [ 1, 5, 8, 9, 11, 2 ]
K = 1
N = len(arr)

# Function Call
maxSumAfterKReverse(arr, K, N)

# This code is contributed by code_hunt.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find the maximum prefix
  // sum after K reversals of the array
  static void maxSumAfterKReverse(int[] arr, int K, int N)
  {

    // Stores the required sum
    int sum = Int32.MinValue;

    // If K is odd, reverse the array
    if (K % 2 != 0)
      Array.Reverse(arr);

    // Store current prefix sum of array
    int currsum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

      // Add arr[i] to currsum
      currsum += arr[i];

      // Update maximum prefix sum
      // till now
      sum = Math.Max(sum, currsum);
    }

    // Print the answer
    Console.Write(sum);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 1, 5, 8, 9, 11, 2 };
    int K = 1;
    int N = arr.Length;

    // Function Call
    maxSumAfterKReverse(arr, K, N);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

  // Function to find the maximum prefix
  // sum after K reversals of the array
  function maxSumAfterKReverse(arr, K, N)
  {

    // Stores the required sum
    let sum = Number.MIN_VALUE;

    // If K is odd, reverse the array
    if (K % 2 != 0)
      arr.reverse();

    // Store current prefix sum of array
    let currsum = 0;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++)
    {

      // Add arr[i] to currsum
      currsum += arr[i];

      // Update maximum prefix sum
      // till now
      sum = Math.max(sum, currsum);
    }

    // Print the answer
    document.write(sum);
  }

// Driver Code

      let arr = [ 1, 5, 8, 9, 11, 2 ];
    let K = 1;
    let N = arr.length;

    // Function Call
    maxSumAfterKReverse(arr, K, N);

</script>
```

**Output:** 

```
36
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)