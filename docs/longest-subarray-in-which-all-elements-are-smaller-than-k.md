# 所有元素都小于 K 的最长子阵列

> 原文:[https://www . geesforgeks . org/最长子阵列，其中所有元素都小于 k/](https://www.geeksforgeeks.org/longest-subarray-in-which-all-elements-are-smaller-than-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出所有元素都小于 **K** 的最长子数组的长度。

约束:
0 < = arr[i] < = 10^5

**示例:**

> **输入:** arr[] = {1，8，3，5，2，2，1，13}，K = 6
> **输出:** 5
> **解释:**
> 存在一个长度为 5 的可能最长子阵列，即{3，5，2，2，1}。
> 
> **输入:** arr[] = {8，12，15，1，3，9，2，10}，K = 10
> **输出:** 4
> **解释:**
> 最长的子阵是{1，3，9，2}。

**天真方法:**最简单的方法是[生成给定阵列的所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并打印最长子阵列的长度，其中所有元素都小于 K 。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方式:**对上述方式进行优化，思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对小于 **K** 的连续数组元素进行计数。打印获得的最大计数。按照以下步骤解决问题:

*   初始化两个变量**计数**和 **C** 分别存储所有元素**小于 K** 的子阵列最大长度和所有元素**小于 K** 的当前子阵列长度。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
    *   如果当前元素小于 **K** ，则增加 **C** 。
    *   否则，将**计数**的值更新为**计数**和 **C** 的最大值，并将 **C** 重置为 **0** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest subarray with all elements
// smaller than K
int largestSubarray(int arr[], int N,
                    int K)
{
    // Stores the length of maximum
    // consecutive sequence
    int count = 0;

    // Stores maximum length of subarray
    int len = 0;

    // Iterate through the array
    for (int i = 0; i < N; i++) {

        // Check if array element
        // smaller than K
        if (arr[i] < K) {
            count += 1;
        }
        else {

            // Store the maximum
            // of length and count
            len = max(len, count);

            // Reset the counter
            count = 0;
        }
    }

    if (count) {
        len = max(len, count);
    }

    // Print the maximum length
    cout << len;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 8, 3, 5, 2, 2, 1, 13 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 6;

    // Function Call
    largestSubarray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the length of the
// longest subarray with all elements
// smaller than K
static void largestSubarray(int[] arr, int N,
                            int K)
{

    // Stores the length of maximum
    // consecutive sequence
    int count = 0;

    // Stores maximum length of subarray
    int len = 0;

    // Iterate through the array
    for(int i = 0; i < N; i++)
    {

        // Check if array element
        // smaller than K
        if (arr[i] < K)
        {
            count += 1;
        }
        else
        {

            // Store the maximum
            // of length and count
            len = Math.max(len, count);

            // Reset the counter
            count = 0;
        }
    }

    if (count != 0)
    {
        len = Math.max(len, count);
    }

    // Print the maximum length
    System.out.println(len);
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int[] arr = { 1, 8, 3, 5, 2, 2, 1, 13 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 6;

    // Function Call
    largestSubarray(arr, N, K);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# longest subarray with all elements
# smaller than K
def largestSubarray(arr, N, K):

    # Stores the length of maximum
    # consecutive sequence
    count = 0

    # Stores maximum length of subarray
    length = 0

    # Iterate through the array
    for i in range(N):

      # Check if array element
      # smaller than K
      if (arr[i] < K):
        count += 1
      else:

        # Store the maximum
        # of length and count
        length = max(length, count)

        # Reset the counter
        count = 0

    if (count):
        length = max(length, count)

    # Print the maximum length
    print(length, end = "")

# Driver Code
if __name__ == "__main__" :

    # Given array arr[]
    arr = [ 1, 8, 3, 5, 2, 2, 1, 13 ]

    # Size of the array
    N = len(arr)

    # Given K
    K = 6

    # Function Call
    largestSubarray(arr, N, K)

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the length of the
    // longest subarray with all elements
    // smaller than K
    static void largestSubarray(int[] arr, int N, int K)
    {

        // Stores the length of maximum
        // consecutive sequence
        int count = 0;

        // Stores maximum length of subarray
        int len = 0;

        // Iterate through the array
        for (int i = 0; i < N; i++)
        {

            // Check if array element
            // smaller than K
            if (arr[i] < K)
            {
                count += 1;
            }
            else
            {

                // Store the maximum
                // of length and count
                len = Math.Max(len, count);

                // Reset the counter
                count = 0;
            }
        }

        if (count != 0)
        {
            len = Math.Max(len, count);
        }

        // Print the maximum length
        Console.WriteLine(len);
    }

  // Driver code
  static void Main()
  {

        // Given array arr[]
        int[] arr = { 1, 8, 3, 5, 2, 2, 1, 13 };

        // Size of the array
        int N = arr.Length;

        // Given K
        int K = 6;

        // Function Call
        largestSubarray(arr, N, K);
  }
}

// This code is contributed by diveshrabadiya07
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to find the length of the
// longest subarray with all elements
// smaller than K
function largestSubarray(arr, N,
                            K)
{

    // Stores the length of maximum
    // consecutive sequence
    let count = 0;

    // Stores maximum length of subarray
    let len = 0;

    // Iterate through the array
    for(let i = 0; i < N; i++)
    {

        // Check if array element
        // smaller than K
        if (arr[i] < K)
        {
            count += 1;
        }
        else
        {

            // Store the maximum
            // of length and count
            len = Math.max(len, count);

            // Reset the counter
            count = 0;
        }
    }

    if (count != 0)
    {
        len = Math.max(len, count);
    }

    // Prlet the maximum length
    document.write(len);
}

// Driver code

    // Given array arr[]
    let arr = [ 1, 8, 3, 5, 2, 2, 1, 13 ];

    // Size of the array
    let N = arr.length;

    // Given K
    let K = 6;

    // Function Call
    largestSubarray(arr, N, K);

    // This code is contributed by target_2.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)