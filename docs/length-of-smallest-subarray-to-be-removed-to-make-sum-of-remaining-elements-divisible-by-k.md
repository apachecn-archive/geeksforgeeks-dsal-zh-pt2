# 要移除的最小子阵列的长度，以使剩余元素的总和可被 K 整除

> 原文:[https://www . geeksforgeeks . org/要移除的最小子阵列长度-剩余元素之和-可被 k 整除/](https://www.geeksforgeeks.org/length-of-smallest-subarray-to-be-removed-to-make-sum-of-remaining-elements-divisible-by-k/)

给定一个整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找到需要移除的最小子数组的长度，使得剩余数组元素的总和可以被 **K** 整除。不允许移除整个数组。如果不可能，那么打印**-1”**。

**示例:**

> **输入:** arr[] = {3，1，4，2}，K = 6
> **输出:** 1
> **说明:**数组元素之和= 10，不能被 6 整除。移除子阵列{4}后，剩余元素的总和为 6。因此，移除的子阵列的长度为 1。
> 
> **输入:** arr[] = {3，6，7，1}，K = 9
> **输出:** 2
> **说明:**数组元素之和= 17，不能被 9 整除。移除子阵列{7，1}和后，其余元素的总和为 9。因此，移除的子阵列的长度为 2。

**天真方法:**最简单的方法是[从给定的阵列中生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/) **arr[]** 排除长度为 **N** 的子阵列。现在，求子阵列的最小长度，使得阵列中所有元素的[之和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)与该子阵列中元素之和之差可被 **K** 整除。如果不存在这样的子阵列，则打印**-1”**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路基于以下观察:

> ((total _ sum–subarray _ sum)% K+subarray _ sum % K)必须等于 total_sum % K.
> 但是，(total _ sum–subarray _ sum)% K = = 0 应该为真。
> 
> 因此，total_sum % K == subarray_sum % K，所以 subarray_sum 和 total_sum 在除以 K 时都应该留下相同的余数。因此，任务是找到元素之和将留下(total_sum % K)余数的最小子阵列的长度。

按照以下步骤解决此问题:

*   将变量 **res** 初始化为 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，以存储要移除的子阵列的最小长度。
*   计算**总和**以及除以 **K** 后剩下的余数。
*   创建一个辅助数组 **modArr[]** ，当每个**arr【I】**被 **K** 除时，存储其剩余部分，如下所示:

> **modArr[i] = (arr[i] + K) % K** 。
> 其中，
> K 在计算余数的时候加了，用来处理负整数的情况。

*   [遍历给定阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并维护一个[无序 _ 地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)以存储遇到的余数的最近位置，并跟踪具有与**目标 _ 余数**相同的**余数的最小所需子阵列。**
*   如果在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中存在等于**(curr _ 余数–target _ 余数+ K) % K** 的任何键，那么将该子阵列长度存储在可变 res 中，作为 **res** 和找到的当前长度的最小值。
*   在上述之后，如果 **res** 不变，则打印**-1”**否则打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is divisible by K
void removeSmallestSubarray(int arr[],
                            int n, int k)
{
    // Stores the remainder of each
    // arr[i] when divided by K
    int mod_arr[n];

    // Stores total sum of elements
    int total_sum = 0;

    // K has been added to each arr[i]
    // to handle -ve integers
    for (int i = 0; i < n; i++) {
        mod_arr[i] = (arr[i] + k) % k;

        // Update the total sum
        total_sum += arr[i];
    }

    // Remainder when total_sum
    // is divided by K
    int target_remainder
        = total_sum % k;

    // If given array is already
    // divisible by K
    if (target_remainder == 0) {
        cout << "0";
        return;
    }

    // Stores curr_remainder and the
    // most recent index at which
    // curr_remainder has occurred
    unordered_map<int, int> map1;
    map1[0] = -1;

    int curr_remainder = 0;

    // Stores required answer
    int res = INT_MAX;

    for (int i = 0; i < n; i++) {

        // Add current element to
        // curr_sum and take mod
        curr_remainder = (curr_remainder
                          + arr[i] + k)
                         % k;

        // Update current remainder index
        map1[curr_remainder] = i;

        int mod
            = (curr_remainder
               - target_remainder
               + k)
              % k;

        // If mod already exists in map
        // the subarray exists
        if (map1.find(mod) != map1.end())
            res = min(res, i - map1[mod]);
    }

    // If not possible
    if (res == INT_MAX || res == n) {
        res = -1;
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 1, 4, 2 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 6;

    // Function Call
    removeSmallestSubarray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is divisible by K
static void removeSmallestSubarray(int arr[],
                                   int n, int k)
{
  // Stores the remainder of each
  // arr[i] when divided by K
  int []mod_arr = new int[n];

  // Stores total sum of
  // elements
  int total_sum = 0;

  // K has been added to each
  // arr[i] to handle -ve integers
  for (int i = 0; i < n; i++)
  {
    mod_arr[i] = (arr[i] +
                  k) % k;

    // Update the total sum
    total_sum += arr[i];
  }

  // Remainder when total_sum
  // is divided by K
  int target_remainder =
      total_sum % k;

  // If given array is already
  // divisible by K
  if (target_remainder == 0)
  {
    System.out.print("0");
    return;
  }

  // Stores curr_remainder and the
  // most recent index at which
  // curr_remainder has occurred
  HashMap<Integer,
          Integer> map1 =
          new HashMap<>();
  map1.put(0, -1);

  int curr_remainder = 0;

  // Stores required answer
  int res = Integer.MAX_VALUE;

  for (int i = 0; i < n; i++)
  {
    // Add current element to
    // curr_sum and take mod
    curr_remainder = (curr_remainder +
                      arr[i] + k) % k;

    // Update current remainder
    // index
    map1.put(curr_remainder, i);

    int mod = (curr_remainder -
               target_remainder +
               k) % k;

    // If mod already exists in
    // map the subarray exists
    if (map1.containsKey(mod))
      res = Math.min(res, i -
                     map1.get(mod));
  }

  // If not possible
  if (res == Integer.MAX_VALUE ||
      res == n)
  {
    res = -1;
  }

  // Print the result
  System.out.print(res);
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {3, 1, 4, 2};

  // Size of array
  int N = arr.length;

  // Given K
  int K = 6;

  // Function Call
  removeSmallestSubarray(arr, N, K);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the length of the
# smallest subarray to be removed such
# that sum of elements is divisible by K
def removeSmallestSubarray(arr, n, k):

    # Stores the remainder of each
    # arr[i] when divided by K
    mod_arr = [0] * n

    # Stores total sum of elements
    total_sum = 0

    # K has been added to each arr[i]
    # to handle -ve integers
    for i in range(n) :
        mod_arr[i] = (arr[i] + k) % k

        # Update the total sum
        total_sum += arr[i]

    # Remainder when total_sum
    # is divided by K
    target_remainder = total_sum % k

    # If given array is already
    # divisible by K
    if (target_remainder == 0):
        print("0")
        return

    # Stores curr_remainder and the
    # most recent index at which
    # curr_remainder has occurred
    map1 = {}
    map1[0] = -1

    curr_remainder = 0

    # Stores required answer
    res = sys.maxsize

    for i in range(n):

        # Add current element to
        # curr_sum and take mod
        curr_remainder = (curr_remainder +
                             arr[i] + k) % k

        # Update current remainder index
        map1[curr_remainder] = i

        mod = (curr_remainder -
             target_remainder + k) % k

        # If mod already exists in map
        # the subarray exists
        if (mod in map1.keys()):
            res = min(res, i - map1[mod])

    # If not possible
    if (res == sys.maxsize or res == n):
        res = -1

    # Print the result
    print(res)

# Driver Code

# Given array arr[]
arr = [ 3, 1, 4, 2 ]

# Size of array
N = len(arr)

# Given K
K = 6

# Function Call
removeSmallestSubarray(arr, N, K)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is divisible by K
static void removeSmallestSubarray(int []arr,
                                   int n, int k)
{

  // Stores the remainder of each
  // arr[i] when divided by K
  int []mod_arr = new int[n];

  // Stores total sum of
  // elements
  int total_sum = 0;

  // K has been added to each
  // arr[i] to handle -ve integers
  for(int i = 0; i < n; i++)
  {
    mod_arr[i] = (arr[i] + k) % k;

    // Update the total sum
    total_sum += arr[i];
  }

  // Remainder when total_sum
  // is divided by K
  int target_remainder = total_sum % k;

  // If given array is already
  // divisible by K
  if (target_remainder == 0)
  {
    Console.Write("0");
    return;
  }

  // Stores curr_remainder and the
  // most recent index at which
  // curr_remainder has occurred
  Dictionary<int,
             int> map1 = new Dictionary<int,
                                        int>();

  map1.Add(0, -1);

  int curr_remainder = 0;

  // Stores required answer
  int res = int.MaxValue;

  for(int i = 0; i < n; i++)
  {

    // Add current element to
    // curr_sum and take mod
    curr_remainder = (curr_remainder +
                      arr[i] + k) % k;

    // Update current remainder
    // index
    map1[curr_remainder] = i;

    int mod = (curr_remainder -
               target_remainder +
               k) % k;

    // If mod already exists in
    // map the subarray exists
    if (map1.ContainsKey(mod))
      res = Math.Min(res, i -
                     map1[mod]);
  }

  // If not possible
  if (res == int.MaxValue ||
      res == n)
  {
    res = -1;
  }

  // Print the result
  Console.Write(res);
}

// Driver Code
public static void Main(String[] args)
{

  // Given array []arr
  int []arr = { 3, 1, 4, 2 };

  // Size of array
  int N = arr.Length;

  // Given K
  int K = 6;

  // Function Call
  removeSmallestSubarray(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is divisible by K
function removeSmallestSubarray(arr, n, k) {
    // Stores the remainder of each
    // arr[i] when divided by K
    let mod_arr = new Array(n);

    // Stores total sum of elements
    let total_sum = 0;

    // K has been added to each arr[i]
    // to handle -ve integers
    for (let i = 0; i < n; i++) {
        mod_arr[i] = (arr[i] + k) % k;

        // Update the total sum
        total_sum += arr[i];
    }

    // Remainder when total_sum
    // is divided by K
    let target_remainder
        = total_sum % k;

    // If given array is already
    // divisible by K
    if (target_remainder == 0) {
        document.write("0");
        return;
    }

    // Stores curr_remainder and the
    // most recent index at which
    // curr_remainder has occurred
    let map1 = new Map();
    map1.set(0, -1);

    let curr_remainder = 0;

    // Stores required answer
    let res = Number.MAX_SAFE_INTEGER;

    for (let i = 0; i < n; i++) {

        // Add current element to
        // curr_sum and take mod
        curr_remainder = (curr_remainder
            + arr[i] + k)
            % k;

        // Update current remainder index
        map1.set(curr_remainder, i);

        let mod
            = (curr_remainder
                - target_remainder
                + k)
            % k;

        // If mod already exists in map
        // the subarray exists
        if (map1.has(mod))
            res = Math.min(res, i - map1.get(mod));
    }

    // If not possible
    if (res == Number.MAX_SAFE_INTEGER || res == n) {
        res = -1;
    }

    // Print the result
    document.write(res);
}

// Driver Code

// Given array arr[]
let arr = [3, 1, 4, 2];

// Size of array
let N = arr.length;

// Given K
let K = 6;

// Function Call
removeSmallestSubarray(arr, N, K);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)