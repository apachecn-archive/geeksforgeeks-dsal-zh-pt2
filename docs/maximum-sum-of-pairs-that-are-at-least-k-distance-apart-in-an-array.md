# 一个数组中至少相距 K 距离的对的最大和

> 原文:[https://www . geesforgeks . org/阵列中距离至少为 k 的最大对和/](https://www.geeksforgeeks.org/maximum-sum-of-pairs-that-are-at-least-k-distance-apart-in-an-array/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出至少由 **K** 个索引分隔的元素对的最大和。

**示例:**

> **输入:** arr[] = {2，4，1，6，8}，K = 2
> **输出:** 12
> **解释:**
> 元素{1，4}相距 K(= 2)距离。对{4，8}的总和为 4 + 8 = 12，这是最大值。
> 
> **输入:** arr[] = {1，2，3}，K = 1
> T3】输出: 4

**天真方法:**解决给定问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，这些对相距**K**，并打印所有形成的可能对中的最大和。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**可以通过预计算每个数组元素的前缀[最大值](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)来优化上述方法。按照以下步骤解决给定的问题:

*   初始化一个变量，比如 **res** 为 [**INT_MIN**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，它存储给定数组中相距 K 的有效对的最大和。
*   初始化一个[数组，比如](https://www.geeksforgeeks.org/array-data-structure/)**preMax[]**，它存储数组元素的最大值直到每个索引 **i** 。
*   初始化 **preMax[0]** 等于 **arr[0]** 。
*   [在**【1，N–1】**范围内遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，并将**preMax【I】**的值更新为**preMax【I–1】**和**arr【I】**的最大值。
*   现在，[遍历范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【K，N–1】**，对于每个索引 **i** ，更新 **res** 的值作为 **res** 和**的最大值(arr[I]+preMax[I–K])**。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest sum
// pair that are K distant apart
int getMaxPairSum(int arr[], int N,
                  int K)
{
    // Stores the prefix maximum array
    int preMax[N];

    // Base Case
    preMax[0] = arr[0];

    // Traverse the array and update
    // the maximum value upto index i
    for (int i = 1; i < N; i++) {
        preMax[i] = max(preMax[i - 1],
                        arr[i]);
    }

    // Stores the maximum sum of pairs
    int res = INT_MIN;

    // Iterate over the range [K, N]
    for (int i = K; i < N; i++) {
        // Find the maximum value of
        // the sum of valid pairs
        res = max(res, arr[i]
                           + preMax[i - K]);
    }

    // Return the resultant sum
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 8, 6, 3 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getMaxPairSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to find the largest sum
    // pair that are K distant apart
    static int getMaxPairSum(int[] arr, int N, int K)
    {

        // Stores the prefix maximum array
        int[] preMax = new int[N];

        // Base Case
        preMax[0] = arr[0];

        // Traverse the array and update
        // the maximum value upto index i
        for (int i = 1; i < N; i++) {
            preMax[i] = Math.max(preMax[i - 1], arr[i]);
        }

        // Stores the maximum sum of pairs
        int res = Integer.MIN_VALUE;

        // Iterate over the range [K, N]
        for (int i = K; i < N; i++) {

            // Find the maximum value of
            // the sum of valid pairs
            res = Math.max(res, arr[i] + preMax[i - K]);
        }

        // Return the resultant sum
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 1, 2, 4, 8, 6, 3 };
        int K = 3;
        int N = arr.length;
        System.out.print(getMaxPairSum(arr, N, K));
    }
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3` program for the above approach

# Function to find the largest sum
# pair that are K distant apart
def getMaxPairSum(arr, N, K):

    # Stores the prefix maximum array
    preMax = [0]*N

    # Base Case
    preMax[0] = arr[0]

    # Traverse the array and update
    # the maximum value upto index i
    for i in range(1, N):
        preMax[i] = max(preMax[i - 1], arr[i])

    # Stores the maximum sum of pairs
    res = -10**8

    # Iterate over the range [K, N]
    for i in range(K, N):

        # Find the maximum value of
        # the sum of valid pairs
        res = max(res, arr[i] + preMax[i - K])

    # Return the resultant sum
    return res

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 4, 8, 6, 3]
    K = 3
    N = len(arr)
    print (getMaxPairSum(arr, N, K))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the largest sum
    // pair that are K distant apart
    static int getMaxPairSum(int[] arr, int N, int K)
    {

        // Stores the prefix maximum array
        int[] preMax = new int[N];

        // Base Case
        preMax[0] = arr[0];

        // Traverse the array and update
        // the maximum value upto index i
        for (int i = 1; i < N; i++) {
            preMax[i] = Math.Max(preMax[i - 1], arr[i]);
        }

        // Stores the maximum sum of pairs
        int res = Int32.MinValue;

        // Iterate over the range [K, N]
        for (int i = K; i < N; i++)
        {

            // Find the maximum value of
            // the sum of valid pairs
            res = Math.Max(res, arr[i] + preMax[i - K]);
        }

        // Return the resultant sum
        return res;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 4, 8, 6, 3 };
        int K = 3;
        int N = arr.Length;
        Console.Write(getMaxPairSum(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the largest sum
// pair that are K distant apart
function getMaxPairSum(arr, N, K)
{
    // Stores the prefix maximum array
    var preMax = Array(N);

    // Base Case
    preMax[0] = arr[0];

    // Traverse the array and update
    // the maximum value upto index i
    for (var i = 1; i < N; i++) {
        preMax[i] = Math.max(preMax[i - 1],
                        arr[i]);
    }

    // Stores the maximum sum of pairs
    var res = -1000000000;

    // Iterate over the range [K, N]
    for (var i = K; i < N; i++) {
        // Find the maximum value of
        // the sum of valid pairs
        res = Math.max(res, arr[i]
                           + preMax[i - K]);
    }

    // Return the resultant sum
    return res;
}

// Driver Code
var arr = [1, 2, 4, 8, 6, 3];
var K = 3;
var N = arr.length;
document.write( getMaxPairSum(arr, N, K));

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)