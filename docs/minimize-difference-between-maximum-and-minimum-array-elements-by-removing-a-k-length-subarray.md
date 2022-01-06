# 通过移除 K 长度子阵列

来最小化最大和最小阵列元素之间的差异

> 原文:[https://www . geeksforgeeks . org/通过移除长度为 k 的子数组来最小化最大和最小数组元素之间的差异/](https://www.geeksforgeeks.org/minimize-difference-between-maximum-and-minimum-array-elements-by-removing-a-k-length-subarray/)

给定一个由 **N** 整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是在移除任何大小为 **K** 的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)后，找出数组中存在的最大元素和[最小元素之间的最小差异。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

**示例:**

> **输入:** arr[] = {4，5，8，9，1，2}，K = 2
> **输出:** 4
> **说明:**移除子阵列{8，9}。最大和最小数组元素之间的最小差值变为(5–1)= 4。
> 
> **输入:** arr[] = {1，2，2}，K = 1
> **输出:** 0
> **说明:**移除子阵列{1}。最大和最小数组元素之间的最小差值变为(2–2)= 0。

**天真法:**最简单的方法是将[所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的大小 **K** 一个个去掉，计算剩余元素中最大值和最小值的差值。最后，打印得到的最小差值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过将**最大值**和**最小前缀**存储到任意索引并从任意索引开始存储**最大值和最小值**来优化。一旦计算出上面的**四个值**，在**不变的计算复杂度中去掉一个 **K** 长度的子阵后，找到最大和最小的数组元素。**

按照以下步骤解决问题:

*   初始化数组 **maxSufix[]和 minsufix[]**。使得 maxSuffix[]和 minSuffix[]数组的第 **i <sup>个</sup>元素**表示分别出现在第 **i <sup>个</sup>个**索引右侧的最大和最小元素。
*   初始化两个变量，比如 **maxPrefix** 和 **minPrefix，**来存储前缀子数组中存在的最大和最小元素。
*   [将数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)遍历索引**【1，N】**并检查 **i + K < = N** 是否存在。如果发现为真，则执行以下步骤:
    *   从第**I<sup>th</sup>T5】索引开始移除大小为 **K** 的子阵列后，阵列中出现的最大值为**max(max 后缀[i + k]，maxPrefix)。****
    *   从**I<sup>th</sup>T5】索引开始移除大小为 **K** 的子阵列后，阵列中出现的最小值为 **min(minSuffix[i + k]，minPrefix)。****
    *   将 **minDiff** 更新为 **min( minDiff，最大–最小)**，以存储最小差值。
*   打印 **minDiff** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize difference
// between maximum and minimum array
// elements by removing a K-length subarray
void minimiseDifference(vector<int>& arr, int K)
{
    // Size of array
    int N = arr.size();

    // Stores the maximum and minimum
    // in the suffix subarray [i .. N-1]
    int maxSuffix[N + 1], minSuffix[N + 1];

    maxSuffix[N] = -1e9;
    minSuffix[N] = 1e9;
    maxSuffix[N - 1] = arr[N - 1];
    minSuffix[N - 1] = arr[N - 1];

    // Constructing the maxSuffix and
    // minSuffix arrays

    // Traverse the array
    for (int i = N - 2; i >= 0; --i) {

        maxSuffix[i] = max(
maxSuffix[i + 1],
 arr[i]);
        minSuffix[i] = min(
minSuffix[i + 1],
 arr[i]);
    }

    // Stores the maximum and minimum
    // in the prefix subarray [0 .. i-1]
    int maxPrefix = arr[0];
    int minPrefix = arr[0];

    // Store the minimum difference
    int minDiff = maxSuffix[K] - minSuffix[K];

    // Traverse the array
    for (int i = 1; i < N; ++i) {

        // If the suffix doesn't exceed
        // the end of the array
        if (i + K <= N) {

            // Store the maximum element
            // in array after removing
            // subarray of size K
            int maximum = max(maxSuffix[i + K], maxPrefix);

            // Stores the maximum element
            // in array after removing
            // subarray of size K
            int minimum = min(minSuffix[i + K], minPrefix);

            // Update minimum difference
            minDiff = min(minDiff, maximum - minimum);
        }

        // Updating the maxPrefix and
        // minPrefix with current element
        maxPrefix = max(maxPrefix, arr[i]);
        minPrefix = min(minPrefix, arr[i]);
    }

    // Print the minimum difference
    cout << minDiff << "\n";
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 5, 8, 9, 1, 2 };
    int K = 2;
    minimiseDifference(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to minimize difference
  // between maximum and minimum array
  // elements by removing a K-length subarray
  static void minimiseDifference(int[] arr, int K)
  {
    // Size of array
    int N = arr.length;

    // Stores the maximum and minimum
    // in the suffix subarray [i .. N-1]
    int[] maxSuffix = new int[N + 1];
    int[] minSuffix = new int[N + 1];

    maxSuffix[N] = -1000000000;
    minSuffix[N] = 1000000000;
    maxSuffix[N - 1] = arr[N - 1];
    minSuffix[N - 1] = arr[N - 1];

    // Constructing the maxSuffix and
    // minSuffix arrays

    // Traverse the array
    for (int i = N - 2; i >= 0; --i) {

      maxSuffix[i]
        = Math.max(maxSuffix[i + 1], arr[i]);
      minSuffix[i]
        = Math.min(minSuffix[i + 1], arr[i]);
    }

    // Stores the maximum and minimum
    // in the prefix subarray [0 .. i-1]
    int maxPrefix = arr[0];
    int minPrefix = arr[0];

    // Store the minimum difference
    int minDiff = maxSuffix[K] - minSuffix[K];

    // Traverse the array
    for (int i = 1; i < N; ++i) {

      // If the suffix doesn't exceed
      // the end of the array
      if (i + K <= N) {

        // Store the maximum element
        // in array after removing
        // subarray of size K
        int maximum
          = Math.max(maxSuffix[i + K], maxPrefix);

        // Stores the maximum element
        // in array after removing
        // subarray of size K
        int minimum
          = Math.min(minSuffix[i + K], minPrefix);

        // Update minimum difference
        minDiff
          = Math.min(minDiff, maximum - minimum);
      }

      // Updating the maxPrefix and
      // minPrefix with current element
      maxPrefix = Math.max(maxPrefix, arr[i]);
      minPrefix = Math.min(minPrefix, arr[i]);
    }

    // Print the minimum difference
    System.out.print(minDiff);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 4, 5, 8, 9, 1, 2 };
    int K = 2;
    minimiseDifference(arr, K);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to minimize difference
# between maximum and minimum array
# elements by removing a K-length subarray
def minimiseDifference(arr, K):

    # Size of array
    N = len(arr)

    # Stores the maximum and minimum
    # in the suffix subarray [i .. N-1]
    maxSuffix = [0 for i in range(N + 1)]
    minSuffix = [0 for i in range(N + 1)]

    maxSuffix[N] = -1e9
    minSuffix[N] = 1e9
    maxSuffix[N - 1] = arr[N - 1]
    minSuffix[N - 1] = arr[N - 1]

    # Constructing the maxSuffix and
    # minSuffix arrays

    # Traverse the array
    i = N - 2
    while(i >= 0):
        maxSuffix[i] = max(maxSuffix[i + 1],arr[i])
        minSuffix[i] = min(minSuffix[i + 1], arr[i])
        i -= 1

    # Stores the maximum and minimum
    # in the prefix subarray [0 .. i-1]
    maxPrefix = arr[0]
    minPrefix = arr[0]

    # Store the minimum difference
    minDiff = maxSuffix[K] - minSuffix[K]

    # Traverse the array
    for i in range(1, N):

        # If the suffix doesn't exceed
        # the end of the array
        if (i + K <= N):

            # Store the maximum element
            # in array after removing
            # subarray of size K
            maximum = max(maxSuffix[i + K], maxPrefix)

            # Stores the maximum element
            # in array after removing
            # subarray of size K
            minimum = min(minSuffix[i + K], minPrefix)

            # Update minimum difference
            minDiff = min(minDiff, maximum - minimum)

        # Updating the maxPrefix and
        # minPrefix with current element
        maxPrefix = max(maxPrefix, arr[i])
        minPrefix = min(minPrefix, arr[i])

    # Print the minimum difference
    print(minDiff)

# Driver Code
if __name__ == '__main__':
    arr =  [4, 5, 8, 9, 1, 2]
    K = 2
    minimiseDifference(arr, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFg {

  // Function to minimize difference
  // between maximum and minimum array
  // elements by removing a K-length subarray
  static void minimiseDifference(List<int> arr, int K)
  {
    // Size of array
    int N = arr.Count;

    // Stores the maximum and minimum
    // in the suffix subarray [i .. N-1]
    int[] maxSuffix = new int[N + 1];
    int[] minSuffix = new int[N + 1];

    maxSuffix[N] = -1000000000;
    minSuffix[N] = 1000000000;
    maxSuffix[N - 1] = arr[N - 1];
    minSuffix[N - 1] = arr[N - 1];

    // Constructing the maxSuffix and
    // minSuffix arrays

    // Traverse the array
    for (int i = N - 2; i >= 0; --i) {

      maxSuffix[i]
        = Math.Max(maxSuffix[i + 1], arr[i]);
      minSuffix[i]
        = Math.Min(minSuffix[i + 1], arr[i]);
    }

    // Stores the maximum and minimum
    // in the prefix subarray [0 .. i-1]
    int maxPrefix = arr[0];
    int minPrefix = arr[0];

    // Store the minimum difference
    int minDiff = maxSuffix[K] - minSuffix[K];

    // Traverse the array
    for (int i = 1; i < N; ++i) {

      // If the suffix doesn't exceed
      // the end of the array
      if (i + K <= N) {

        // Store the maximum element
        // in array after removing
        // subarray of size K
        int maximum
          = Math.Max(maxSuffix[i + K], maxPrefix);

        // Stores the maximum element
        // in array after removing
        // subarray of size K
        int minimum
          = Math.Min(minSuffix[i + K], minPrefix);

        // Update minimum difference
        minDiff
          = Math.Min(minDiff, maximum - minimum);
      }

      // Updating the maxPrefix and
      // minPrefix with current element
      maxPrefix = Math.Max(maxPrefix, arr[i]);
      minPrefix = Math.Min(minPrefix, arr[i]);
    }

    // Print the minimum difference
    Console.WriteLine(minDiff);
  }

  // Driver Code
  public static void Main()
  {
    List<int> arr
      = new List<int>() { 4, 5, 8, 9, 1, 2 };
    int K = 2;
    minimiseDifference(arr, K);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript  program for the above approach

// Function to minimize difference
// between maximum and minimum array
// elements by removing a K-length subarray
function minimiseDifference(arr, K)
{
    // Size of array
    var N = arr.length;

    // Stores the maximum and minimum
    // in the suffix subarray [i .. N-1]
    var maxSuffix = new Array(N + 1);
    var minSuffix = new Array(N + 1);

    maxSuffix[N] = -1e9;
    minSuffix[N] = 1e9;
    maxSuffix[N - 1] = arr[N - 1];
    minSuffix[N - 1] = arr[N - 1];

    // Constructing the maxSuffix and
    // minSuffix arrays

    // Traverse the array
    for (var i = N - 2; i >= 0; --i) {

        maxSuffix[i] = Math.max(maxSuffix[i + 1], arr[i]);
        minSuffix[i] = Math.min(minSuffix[i + 1], arr[i]);
    }

    // Stores the maximum and minimum
    // in the prefix subarray [0 .. i-1]
    var maxPrefix = arr[0];
    var minPrefix = arr[0];

    // Store the minimum difference
    var minDiff = maxSuffix[K] - minSuffix[K];

    // Traverse the array
    for (var i = 1; i < N; ++i) {

        // If the suffix doesn't exceed
        // the end of the array
        if (i + K <= N) {

            // Store the maximum element
            // in array after removing
            // subarray of size K
            var maximum =
            Math.max(maxSuffix[i + K], maxPrefix);

            // Stores the maximum element
            // in array after removing
            // subarray of size K
            var minimum =
            Math.min(minSuffix[i + K], minPrefix);

            // Update minimum difference
            minDiff =
            Math.min(minDiff, maximum - minimum);
        }

        // Updating the maxPrefix and
        // minPrefix with current element
        maxPrefix = Math.max(maxPrefix, arr[i]);
        minPrefix = Math.min(minPrefix, arr[i]);
    }

    // Print the minimum difference
   document.write( minDiff + "<br>");
}

var arr = [ 4, 5, 8, 9, 1, 2 ];
var K = 2;
minimiseDifference(arr, K);

// This code is contributed by SoumikMondal

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)