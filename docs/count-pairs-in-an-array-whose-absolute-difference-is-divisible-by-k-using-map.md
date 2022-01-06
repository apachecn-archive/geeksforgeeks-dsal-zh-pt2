# 对绝对差可被 K 整除的数组中的对进行计数|使用映射

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-array-of-absolute-division-k-use-map/](https://www.geeksforgeeks.org/count-pairs-in-an-array-whose-absolute-difference-is-divisible-by-k-using-map/)

给定一个由 **N** 元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** 和一个整数 **K** ，任务是找到对 **(i，j)** 的数量，使得**(arr[I]–arr[j])的绝对值为**的倍数 **K** 。

**示例:**

> **输入:** N = 4，K = 2，arr[] = {1，2，3，4}
> **输出:** 2
> **说明:** *数组中总共存在 2 对绝对差可被 2 整除。这两对是:(1，3)，(2，4)。*
> 
> **输入:** N = 3， *K = 3，arr[] = {3，3，3}*
> **输出:** 3
> ***说明:**这个数组中共有 3 对，绝对差可被 3 整除。这两对是:(3，3)，(3，3)，(3，3)。*

**天真方法:**最简单的方法是遍历数组中每一个可能的对，如果数字的绝对差是 **K** 的倍数，那么将**计数**增加 **1** 。处理完所有对后，打印计数值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**频率阵列方法:**使用频率阵列解决该问题的方法在本文的[第 1 集中讨论。在这种方法中，我们讨论了使用地图解决它的方法。](https://www.geeksforgeeks.org/count-pairs-in-an-array-whose-absolute-difference-is-divisible-by-k/)

**高效途径:**优化上述途径，思路是观察两个数字**a【I】**和**a【j】**如果**a【I】% K = a【j】% K**，那么**ABS(a【I】–a【j】)**就是 **K** 的倍数。按照以下步骤解决问题:

*   将变量**和**初始化为 **0** 来存储答案。
*   [声明一个**无序 _ 映射< int，int>**](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)**count _ map【】**用 **K** 存储数组元素的余数。
*   [使用变量**索引**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并为每个索引将 **count_map** 中的值 **arr【索引】%k** 增加 **1** 。
*   [迭代 count_map](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) 中的所有键值对。对于每个键值对:
    *   值**count _ map【rem】**是其与 **K** 的余数等于“ **rem** 的元素数。
    *   要形成有效的配对，请从**count _ map【rem】**号码中选择任意两个号码。
    *   从 **N** 个数字中选择两个数字的方式数为**Nc2 = N *(N–1)/2**。
*   添加所有键值对的答案，打印**和**。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of pairs
// (i, j) such that abs(arr[i] - arr[j])
// is divisible by k.
void countOfPairs(int* arr, int N, int K)
{

    // Frequency Map to keep count of
    // remainders of array elements with K.
    unordered_map<int, int> count_map;

    for (int index = 0; index < N; ++index) {
        count_map[arr[index] % K]++;
    }

    // To store the final answer.
    int ans = 0;
    for (auto it : count_map) {

        // Number of ways of selecting any two
        // numbers from all numbers having the
        // same remainder is Nc2 = N
        // * (N - 1) / 2
        ans += (it.second * (it.second - 1)) / 2;
    }

    // Output the answer.
    cout << ans << endl;
}

// Driver Code
int main()
{
    int K = 2;

    // Input array
    int arr[] = { 1, 2, 3, 4 };

    // Size of array
    int N = sizeof arr / sizeof arr[0];

    countOfPairs(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to count number of pairs
    // (i, j) such that Math.abs(arr[i] - arr[j])
    // is divisible by k.
    static void countOfPairs(int[] arr, int N, int K) {

        // Frequency Map to keep count of
        // remainders of array elements with K.
        HashMap<Integer, Integer> count_map =
                new HashMap<Integer, Integer>();

        for (int index = 0; index < N; ++index) {
            if (count_map.containsKey(arr[index] % K)) {
                count_map.put(arr[index] % K,
                        count_map.get(arr[index] % K) + 1);
            } else {
                count_map.put(arr[index] % K, 1);
            }
        }

        // To store the final answer.
        int ans = 0;
        for (Map.Entry<Integer, Integer> it : count_map.entrySet()) {

            // Number of ways of selecting any two
            // numbers from all numbers having the
            // same remainder is Nc2 = N
            // * (N - 1) / 2
            ans += (it.getValue() * (it.getValue() - 1)) / 2;
        }

        // Output the answer.
        System.out.print(ans + "\n");
    }

    // Driver Code
    public static void main(String[] args) {
        int K = 2;

        // Input array
        int arr[] = { 1, 2, 3, 4 };

        // Size of array
        int N = arr.length;

        countOfPairs(arr, N, K);

    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to count number of pairs
# (i, j) such that abs(arr[i] - arr[j])
# is divisible by k.
def countOfPairs(arr, N, K):

    # Frequency Map to keep count of
    # remainders of array elements with K.
    count_map = {}

    for index in range(N):

        if (not arr[index] % K in count_map):
            count_map[arr[index] % K] = 1
        else:
            count_map[arr[index] % K] += 1

    # To store the final answer.
    ans = 0
    for val in count_map.values():

        # Number of ways of selecting any two
        # numbers from all numbers having the
        # same remainder is Nc2 = N
        # * (N - 1) / 2
        ans += (val * (val - 1)) // 2

    # Output the answer.
    print(ans)

# Driver Code
K = 2

# Input array
arr = [1, 2, 3, 4]

# Size of array
N = len(arr)

countOfPairs(arr, N, K)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to count number of pairs
    // (i, j) such that Math.Abs(arr[i] - arr[j])
    // is divisible by k.
    static void countOfPairs(int[] arr, int N, int K) {

        // Frequency Map to keep count of
        // remainders of array elements with K.
        Dictionary<int, int> count_map =
                new Dictionary<int, int>();

        for (int index = 0; index < N; ++index) {
            if (count_map.ContainsKey(arr[index] % K)) {
                count_map[arr[index] % K] =
                        count_map[arr[index] % K] + 1;
            } else {
                count_map.Add(arr[index] % K, 1);
            }
        }

        // To store the readonly answer.
        int ans = 0;
        foreach (KeyValuePair<int, int> it in count_map) {

            // Number of ways of selecting any two
            // numbers from all numbers having the
            // same remainder is Nc2 = N
            // * (N - 1) / 2
            ans += (it.Value * (it.Value - 1)) / 2;
        }

        // Output the answer.
        Console.Write(ans + "\n");
    }

    // Driver Code
    public static void Main(String[] args) {
        int K = 2;

        // Input array
        int []arr = { 1, 2, 3, 4 };

        // Size of array
        int N = arr.Length;

        countOfPairs(arr, N, K);

    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach

      // Function to count number of pairs
      // (i, j) such that abs(arr[i] - arr[j])
      // is divisible by k.
      function countOfPairs(arr, N, K) {

          // Frequency Map to keep count of
          // remainders of array elements with K.
          let count_map = new Map();

          for (let index = 0; index < N; ++index) {

              if (!count_map.has(arr[index] % K))
                  count_map.set(arr[index] % K, 1);
              else
                  count_map.set(arr[index] % K, count_map.get(arr[index] % K) + 1)
          }

          // To store the final answer.
          let ans = 0;
          for (let [key, value] of count_map) {

              // Number of ways of selecting any two
              // numbers from all numbers having the
              // same remainder is Nc2 = N
              // * (N - 1) / 2
              ans += (value * (value - 1)) / 2;
          }

          // Output the answer.
          document.write(ans + '<br>');
      }

      // Driver Code
      let K = 2;

      // Input array
      let arr = [1, 2, 3, 4];

      // Size of array
      let N = arr.length;

      countOfPairs(arr, N, K);

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*