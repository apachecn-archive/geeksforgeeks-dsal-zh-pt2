# 需要在任一端减去的最小数组元素，以将 K 减少到 0

> 原文:[https://www . geeksforgeeks . org/最小数组元素-要求从任意一端减去以将 k 减少到 0/](https://www.geeksforgeeks.org/minimum-array-elements-required-to-be-subtracted-from-either-end-to-reduce-k-to-0/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过从数组的任一端移除一个数组元素并从 **K** 中减去它来将 **K** 减少到 **0** 。如果无法将 **K** 降为 **0** ，则打印**-1”**。否则，打印所需的最小操作次数。

**示例:**

> ***输入:** a* rr[] = {1，3，1，1，2}，K = 4
> ***输出:*** 2
> ***解释:***
> *给定数组为{1，3，1，1，2}*
> **操作 1:** 移除 arr[0] (= 1)将 arr[]修改为{3，1，2 从 K 中减去 arr[0]将 K 减少到 4–1 = 3。
> **操作 2:** 移除 arr[0] (= 1)会将 arr[]修改为{1，1，2}。从 K 中减去 arr[0]将 K 减少到 3–3 = 0。
> 因此，所需步骤总数为 2。
> 
> ***输入:*** arr[] = {1，1，3，4}，K = 3
> ***输出:*** -1

**方法:**给定的问题可以基于以下观察来解决:

*   考虑需要分别从给定阵列的正面和背面移除 **X** 和 **Y** 元素，以将 **K** 减少到 **0** 。
*   因此，剩余阵元之和必须等于 **(** [**阵元之和**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**–K)**。

因此，从上面的观察来看，思路是求和等于 **(** [**)阵元之和**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**–K)**的子阵(说 **L** )的最大长度。因此，打印**(N–L)**的值，作为将 **K** 减少到 **0** 必须移除的最小元素。如果没有这样的子阵列，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// longest subarray having sum K
int longestSubarray(int arr[],
                    int N, int K)
{
    // Stores the index of
    // the prefix sum
    unordered_map<int, int> um;

    int sum = 0, maxLen = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Update sum
        sum += arr[i];

        // If the subarray starts
        // from index 0
        if (sum == K)
            maxLen = i + 1;

        // Add the current prefix sum
        // with index if it is not
        // present in the map um
        if (um.find(sum) == um.end())
            um[sum] = i;

        // Check if sum - K is
        // present in Map um or not
        if (um.find(sum - K) != um.end()) {

            // Update the maxLength
            if (maxLen < (i - um[sum - K]))
                maxLen = i - um[sum - K];
        }
    }

    // Return the required maximum length
    return maxLen;
}

// Function to find the minimum removal of
// array elements required to reduce K to 0
void minRequiredOperation(int arr[],
                          int N, int K)
{
    // Stores the sum of the array
    int TotalSum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)

        // Update sum of the array
        TotalSum += arr[i];

    // Find maxLen
    int maxLen = longestSubarray(
        arr, N, TotalSum - K);

    // If the subarray with
    // sum doesn't exist
    if (maxLen == -1) {
        cout << -1;
    }

    // Otherwise, print the
    // required maximum length
    else
        cout << N - maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 1, 1, 2 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    minRequiredOperation(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the length of
// longest subarray having sum K
static int longestSubarray(int[] arr, int N, int K)
{

    // Stores the index of
    // the prefix sum
    HashMap<Integer,
            Integer> um = new HashMap<Integer,
                                      Integer>();

    int sum = 0, maxLen = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Update sum
        sum += arr[i];

        // If the subarray starts
        // from index 0
        if (sum == K)
            maxLen = i + 1;

        // Add the current prefix sum
        // with index if it is not
        // present in the map um
        if (!um.containsKey(sum))
            um.put(sum, i);

        // Check if sum - K is
        // present in Map um or not
        if (um.containsKey(sum - K))
        {

            // Update the maxLength
            if (maxLen < (i - um.get(sum - K)))
                maxLen = i - um.get(sum - K);
        }
    }

    // Return the required maximum length
    return maxLen;
}

// Function to find the minimum removal of
// array elements required to reduce K to 0
static void minRequiredOperation(int[] arr, int N,
                                 int K)
{

    // Stores the sum of the array
    int TotalSum = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)

        // Update sum of the array
        TotalSum += arr[i];

    // Find maxLen
    int maxLen = longestSubarray(arr, N, TotalSum - K);

    // If the subarray with
    // sum doesn't exist
    if (maxLen == -1)
    {
        System.out.println(-1);
    }

    // Otherwise, print the
    // required maximum length
    else
        System.out.println(N - maxLen);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 3, 1, 1, 2 };
    int K = 4;
    int N = arr.length;

    minRequiredOperation(arr, N, K);
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of
# longest subarray having sum K
def longestSubarray(arr, N, K):

  # Stores the index of
    # the prefix sum
    um = {}
    sum , maxLen = 0, 0

    # Traverse the given array
    for i in range(N):

        # Update sum
        sum += arr[i]

        # If the subarray starts
        # from index 0
        if (sum == K):
            maxLen = i + 1

        # Add the current prefix sum
        # with index if it is not
        # present in the map um
        if (sum not in um):
            um[sum] = i

        # Check if sum - K is
        # present in Map um or not
        if ((sum - K) in um):

            # Update the maxLength
            if (maxLen < (i - um[sum - K])):
                maxLen = i - um[sum - K]

    # Return the required maximum length
    return maxLen

# Function to find the minimum removal of
# array elements required to reduce K to 0
def minRequiredOperation(arr, N, K):

    # Stores the sum of the array
    TotalSum = 0

    # Traverse the array arr[]
    for i in range(N):

      # Update sum of the array
        TotalSum += arr[i]

    # Find maxLen
    maxLen = longestSubarray(arr, N, TotalSum - K)

    # If the subarray with
    # sum doesn't exist
    if (maxLen == -1):
        print (-1,end="")

    # Otherwise, print the
    # required maximum length
    else:
        print (N - maxLen,end="")

# Driver Code
if __name__ == '__main__':
    arr = [1, 3, 1, 1, 2]
    K = 4
    N = len(arr)

    minRequiredOperation(arr, N, K)

    # this code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to find the length of
  // longest subarray having sum K
  static int longestSubarray(int []arr,
                             int N, int K)
  {
    // Stores the index of
    // the prefix sum
    Dictionary<int,int> um = new Dictionary<int,int>();

    int sum = 0, maxLen = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

      // Update sum
      sum += arr[i];

      // If the subarray starts
      // from index 0
      if (sum == K)
        maxLen = i + 1;

      // Add the current prefix sum
      // with index if it is not
      // present in the map um
      if (!um.ContainsKey(sum))
        um[sum] = i;

      // Check if sum - K is
      // present in Map um or not
      if (um.ContainsKey(sum - K)) {

        // Update the maxLength
        if (maxLen < (i - um[sum - K]))
          maxLen = i - um[sum - K];
      }
    }

    // Return the required maximum length
    return maxLen;
  }

  // Function to find the minimum removal of
  // array elements required to reduce K to 0
  static void minRequiredOperation(int []arr,
                                   int N, int K)
  {

    // Stores the sum of the array
    int TotalSum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)

      // Update sum of the array
      TotalSum += arr[i];

    // Find maxLen
    int maxLen = longestSubarray(
      arr, N, TotalSum - K);

    // If the subarray with
    // sum doesn't exist
    if (maxLen == -1) {
      Console.WriteLine(-1);
    }

    // Otherwise, print the
    // required maximum length
    else
      Console.WriteLine(N - maxLen);
  }

  // Driver Code
  public static void Main()
  {
    int []arr = { 1, 3, 1, 1, 2 };
    int K = 4;
    int N = arr.Length;
    minRequiredOperation(arr, N, K);
  }
}

// This code is contributed by SUREDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the length of
// longest subarray having sum K
function longestSubarray(arr, N, K)
{

    // Stores the index of
    // the prefix sum
    let um = new Map();

    let sum = 0, maxLen = 0;

    // Traverse the given array
    for(let i = 0; i < N; i++)
    {

        // Update sum
        sum += arr[i];

        // If the subarray starts
        // from index 0
        if (sum == K)
            maxLen = i + 1;

        // Add the current prefix sum
        // with index if it is not
        // present in the map um
        if (!um.has(sum))
            um.set(sum, i);

        // Check if sum - K is
        // present in Map um or not
        if (um.has(sum - K))
        {

            // Update the maxLength
            if (maxLen < (i - um.get(sum - K)))
                maxLen = i - um.get(sum - K);
        }
    }

    // Return the required maximum length
    return maxLen;
}

// Function to find the minimum removal of
// array elements required to reduce K to 0
function minRequiredOperation(arr, N, K)
{

    // Stores the sum of the array
    let TotalSum = 0;

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)

        // Update sum of the array
        TotalSum += arr[i];

    // Find maxLen
    let maxLen = longestSubarray(
            arr, N, TotalSum - K);

    // If the subarray with
    // sum doesn't exist
    if (maxLen == -1)
    {
        document.write(-1);
    }

    // Otherwise, print the
    // required maximum length
    else
        document.write(N - maxLen);
}

// Driver Code
let arr = [ 1, 3, 1, 1, 2 ];
let K = 4;
let N = arr.length

minRequiredOperation(arr, N, K);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)