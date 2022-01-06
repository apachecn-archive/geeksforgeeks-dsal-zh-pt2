# 将阵列分割成具有同素乘积的子阵列的最小指数

> 原文:[https://www . geeksforgeeks . org/最小索引-将数组拆分为子数组-具有同素乘积/](https://www.geeksforgeeks.org/minimum-index-to-split-array-into-subarrays-with-co-prime-products/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到最大索引 **K** ，使得[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)T10】{ arr[0]，arr[K]} 和 **{arr[K + 1]，arr[N–1]}**的乘积为[同素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。如果没有这样的索引，则打印【T16 "-" 1 "。

**示例:**

> **输入:** arr[] = {2，3，4，5}
> **输出:** 2
> **说明:**
> 分区最小索引为 2。
> 左子阵的乘积为= 2 * 3 * 4 = 24。
> 右子阵列的乘积= 5。
> 由于 24 和 5 是同素的，所以要求的答案是 2。
> 
> **输入:** arr[] = {23，41，52，83，7，13}
> **输出:** 0
> **说明:**
> 分区最小索引为 0。
> 左子阵列的乘积= 23。
> 右子阵积= 41 * 52 * 83 * 7 * 13 = 16102996。
> 由于 23 和 16102996 是同素的，所以答案是 0。

**天真方法:**最简单的方法是从数组开始检查分区的所有可能索引，并检查所形成的子数组的[乘积是否为同素。如果存在任何这样的索引，那么打印该索引。否则，打印**-1”**。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/product-of-all-subarrays-of-an-array/)

**高效法:**对上述方法进行优化，思路是使用[前缀积数组](https://www.geeksforgeeks.org/prefix-product-array/)和**后缀积数组**，找到可能的索引。按照以下步骤解决问题:

*   创建两个辅助数组，**前缀[]** 和**后缀[]** 来存储前缀和后缀数组乘积。将**前缀【0】**初始化为**arr【0】**，将**后缀【N–1】**初始化为**arr【N–1】**。
*   [使用变量 **i** 在范围**【2，N】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将前缀数组更新为**前缀【I】=前缀【I–1】* arr【I】**。
*   使用变量 **i** 在范围**【N–2，0】**内从后面遍历给定数组，并将后缀数组更新为**后缀[i] =后缀[i + 1]*arr[i]** 。
*   使用变量 **i** 和[在范围**【0，N–1】**内循环，检查**前缀【I】**和**后缀【I+1】**是否同素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。如果发现为真，打印当前索引并[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   如果上述步骤中没有这样的索引，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the GCD of 2 numbers
int GCD(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Find the GCD recursively
    return GCD(b, a % b);
}

// Function to find the minimum partition
// index K s.t. product of both subarrays
// around that partition are co-prime
int findPartition(int nums[], int N)
{

    // Stores the prefix and suffix
    // array product
    int prefix[N], suffix[N], i, k;

    prefix[0] = nums[0];

    // Update the prefix array
    for (i = 1; i < N; i++) {
        prefix[i] = prefix[i - 1]
                    * nums[i];
    }

    suffix[N - 1] = nums[N - 1];

    // Update the suffix array
    for (i = N - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1]
                    * nums[i];
    }

    // Iterate the given array
    for (k = 0; k < N - 1; k++) {
        // Check if prefix[k] and
        // suffix[k+1] are co-prime
        if (GCD(prefix[k],
                suffix[k + 1])
            == 1) {
            return k;
        }
    }

    // If no index for partition
    // exists, then return -1
    return -1;
}

// Driver Code
int main()
{

    int arr[] = { 2, 3, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << findPartition(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class solution{

// Function to find the
// GCD of 2 numbers
static int GCD(int a,
               int b)
{
  // Base Case
  if (b == 0)
    return a;

  // Find the GCD
  // recursively
  return GCD(b, a % b);
}

// Function to find the minimum
// partition index K s.t. product
// of both subarrays around that
// partition are co-prime
static int findPartition(int nums[],
                         int N)
{
  // Stores the prefix and
  // suffix array product
  int []prefix = new int[N];
  int []suffix = new int[N];
  int i, k;

  prefix[0] = nums[0];

  // Update the prefix array
  for (i = 1; i < N; i++)
  {
    prefix[i] = prefix[i - 1] *
                nums[i];
  }

  suffix[N - 1] = nums[N - 1];

  // Update the suffix array
  for (i = N - 2; i >= 0; i--)
  {
    suffix[i] = suffix[i + 1] *
                nums[i];
  }

  // Iterate the given array
  for (k = 0; k < N - 1; k++)
  {
    // Check if prefix[k] and
    // suffix[k+1] are co-prime
    if (GCD(prefix[k],
            suffix[k + 1]) == 1)
    {
      return k;
    }
  }

  // If no index for partition
  // exists, then return -1
  return -1;
}

// Driver Code
public static void main(String args[])
{
  int arr[] = {2, 3, 4, 5};
  int N = arr.length;

  // Function call
  System.out.println(findPartition(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the
# GCD of 2 numbers
def GCD(a, b):

    # Base Case
    if (b == 0):
        return a

    # Find the GCD recursively
    return GCD(b, a % b)

# Function to find the minimum
# partition index K s.t. product
# of both subarrays around that
# partition are co-prime
def findPartition(nums, N):

    #Stores the prefix and
    # suffix array product
    prefix=[0] * N
    suffix=[0] * N

    prefix[0] = nums[0]

    # Update the prefix
    # array
    for i in range(1, N):
        prefix[i] = (prefix[i - 1] *
                     nums[i])

    suffix[N - 1] = nums[N - 1]

    # Update the suffix array
    for i in range(N - 2, -1, -1):
        suffix[i] = (suffix[i + 1] *
                     nums[i])

    # Iterate the given array
    for k in range(N - 1):

        # Check if prefix[k] and
        # suffix[k+1] are co-prime
        if (GCD(prefix[k],
                suffix[k + 1]) == 1):
            return k

    # If no index for partition
    # exists, then return -1
    return -1

# Driver Code
if __name__ == '__main__':

    arr = [2, 3, 4, 5]
    N = len(arr)

    # Function call
    print(findPartition(arr, N))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the
// GCD of 2 numbers
static int GCD(int a, int b)
{
  // Base Case
  if (b == 0)
    return a;

  // Find the GCD
  // recursively
  return GCD(b, a % b);
}

// Function to find the minimum
// partition index K s.t. product
// of both subarrays around that
// partition are co-prime
static int findPartition(int[] nums,
                         int N)
{
  // Stores the prefix and
  // suffix array product
  int[] prefix = new int[N];
  int[] suffix = new int[N];
  int i, k;

  prefix[0] = nums[0];

  // Update the prefix array
  for (i = 1; i < N; i++)
  {
    prefix[i] = prefix[i - 1] *
                nums[i];
  }

  suffix[N - 1] = nums[N - 1];

  // Update the suffix array
  for (i = N - 2; i >= 0; i--)
  {
    suffix[i] = suffix[i + 1] *
                nums[i];
  }

  // Iterate the given array
  for (k = 0; k < N - 1; k++)
  {
    // Check if prefix[k] and
    // suffix[k+1] are co-prime
    if (GCD(prefix[k],
            suffix[k + 1]) == 1)
    {
      return k;
    }
  }

  // If no index for partition
  // exists, then return -1
  return -1;
}

// Driver code
static void Main()
{
  int[] arr = {2, 3, 4, 5};
  int N = arr.Length;

  // Function call
  Console.WriteLine(findPartition(arr, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the GCD of 2 numbers
function GCD(a, b)
{
    // Base Case
    if (b == 0)
        return a;

    // Find the GCD recursively
    return GCD(b, a % b);
}

// Function to find the minimum partition
// index K s.t. product of both subarrays
// around that partition are co-prime
function findPartition(nums, N)
{

    // Stores the prefix and suffix
    // array product
    var prefix = Array(N), suffix = Array(N), i, k;

    prefix[0] = nums[0];

    // Update the prefix array
    for (i = 1; i < N; i++) {
        prefix[i] = prefix[i - 1]
                    * nums[i];
    }

    suffix[N - 1] = nums[N - 1];

    // Update the suffix array
    for (i = N - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1]
                    * nums[i];
    }

    // Iterate the given array
    for (k = 0; k < N - 1; k++) {
        // Check if prefix[k] and
        // suffix[k+1] are co-prime
        if (GCD(prefix[k],
                suffix[k + 1])
            == 1) {
            return k;
        }
    }

    // If no index for partition
    // exists, then return -1
    return -1;
}

// Driver Code
var arr = [2, 3, 4, 5];
var N = arr.length;
// Function call
document.write( findPartition(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N log(N))*
***辅助空间:** O(N)*