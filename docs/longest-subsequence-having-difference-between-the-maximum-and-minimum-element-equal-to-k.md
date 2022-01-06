# 最大和最小元素之差等于 K 的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列最大和最小元素差值等于 k/](https://www.geeksforgeeks.org/longest-subsequence-having-difference-between-the-maximum-and-minimum-element-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到给定数组的最长[子序列，使得子序列中最大和最小元素之间的差正好是 **K** 。](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)

**示例:**

> **输入:** arr[] = {1，3，2，2，5，2，3，7}，K = 1
> **输出:** 5
> **解释:**
> 最大和最小元素之差为 K(= 1)的最长子序列为{3，2，2，2，3}。
> 因此，长度为 5。
> 
> **输入:** arr [] = {4，3，3，4}，K = 4
> T3】输出: 0

**朴素方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，对于每个子序列，找到子序列中最大值和最小值之间的差异。如果它等于 **K** ，更新结果最长子序列长度。检查所有子序列后，打印获得的最大长度。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是基于这样的观察:在所需的子序列中，只能存在两个唯一的元素，它们的区别应该是 **K** 。这个问题可以通过[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来解决，存储每个数组元素的[频率。按照以下步骤解决问题:](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)

*   初始化一个变量，比如**和**，来存储最长子序列的长度。
*   初始化一个 [hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如说 **M** ，那个[存储数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素 **arr[i]** ，将 **M** 中 **arr[]** 的频率增加 **1** 。
*   现在[遍历 hashmap](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，对于 **M** 中的每个键(比如说 **X** ，如果 **(X + K)** 也存在于 **M** 中，那么将 **ans** 的值更新为 **ans** 和两个键的值之和的最大值。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find longest subsequence
// having absolute difference between
// maximum and minimum element K
void longestSubsequenceLength(int arr[],
                              int N, int K)
{
    // Stores the frequency of each
    // array element
    unordered_map<int, int> um;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)

        // Increment um[arr[i]] by 1
        um[arr[i]]++;

    // Store the required answer
    int ans = 0;

    // Traverse the hashmap
    for (auto it : um) {

        // Check if it.first + K
        // exists in the hashmap
        if (um.find(it.first + K)
            != um.end()) {

            // Update the answer
            ans = max(ans,
                      it.second
                          + um[it.first + K]);
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 2, 2, 5, 2, 3, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 1;

    longestSubsequenceLength(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find longest subsequence
// having absolute difference between
// maximum and minimum element K
static void longestSubsequenceLength(int []arr,
                                     int N, int K)
{

    // Stores the frequency of each
    // array element
    Map<Integer,
        Integer> um = new HashMap<Integer,
                                  Integer>();

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        if (um.containsKey(arr[i]))
            um.put(arr[i], um.get(arr[i]) + 1);
        else
            um.put(arr[i], 1);
    }

    // Store the required answer
    int ans = 0;

    // Traverse the hashmap
    for(Map.Entry<Integer, Integer> e : um.entrySet())
    {

        // Check if it.first + K
        // exists in the hashmap
        if (um.containsKey(e.getKey() + K))
        {

            // Update the answer
            ans = Math.max(ans, e.getValue() +
                           um.get(e.getKey() + K));
        }
    }

    // Print the result
    System.out.println(ans);
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 3, 2, 2, 5, 2, 3, 7 };
    int N = arr.length;
    int K = 1;

    longestSubsequenceLength(arr, N, K);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find longest subsequence
# having absolute difference between
# maximum and minimum element K
def longestSubsequenceLength(arr, N, K):

    # Stores the frequency of each
    # array element
    um = defaultdict(int)

    # Traverse the array arr[]
    for i in range(N):

        # Increment um[arr[i]] by 1
        um[arr[i]] += 1

    # Store the required answer
    ans = 0

    # Traverse the hashmap
    for it in um.keys():

        # Check if it.first + K
        # exists in the hashmap
        if (it + K) in um:

            # Update the answer
            ans = max(ans,
                      um[it]
                      + um[it + K])

    # Print the result
    print(ans)

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 2, 2, 5, 2, 3, 7]
    N = len(arr)
    K = 1

    longestSubsequenceLength(arr, N, K)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to find longest subsequence
// having absolute difference between
// maximum and minimum element K
static void longestSubsequenceLength(int[] arr,
                              int N, int K)
{

    // Stores the frequency of each
    // array element
    Dictionary<int, int> um = new Dictionary<int, int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Increase the counter of
        // the array element by 1
        int count = um.ContainsKey(arr[i]) ? um[arr[i]] : 0;
        if (count == 0)
        {
            um.Add(arr[i], 1);
        }
        else
        {
            um[arr[i]] = count + 1;
        }
    }

    // Store the required answer
    int ans = 0;

    // Traverse the hashmap
    foreach(KeyValuePair<int, int> it in um)
    {

        // Check if it.first + K
        // exists in the hashmap
        if (um.ContainsKey(it.Key + K))
        {

            // Update the answer
            ans = Math.Max(ans, (it.Value + um[it.Key + K]));
        }
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 3, 2, 2, 5, 2, 3, 7 };
    int N = arr.Length;
    int K = 1;

    longestSubsequenceLength(arr, N, K);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find longest subsequence
// having absolute difference between
// maximum and minimum element K
function longestSubsequenceLength(arr, N, K)
{
    // Stores the frequency of each
    // array element
    var um = new Map();

    // Traverse the array arr[]
    for (var i = 0; i < N; i++)

        // Increment um[arr[i]] by 1
        if(um.has(arr[i]))
        {
            um.set(arr[i], um.get(arr[i])+1);
        }
        else
        {
            um.set(arr[i], 1);
        }

    // Store the required answer
    var ans = 0;

    // Traverse the hashmap
    um.forEach((value, key) => {

        // Check if it.first + K
        // exists in the hashmap
        if (um.has(key+K)) {

            // Update the answer
            ans = Math.max(ans,
                      value
                          + um.get(key+K));
        }
    });

    // Print the result
    document.write( ans);
}

// Driver Code
var arr = [ 1, 3, 2, 2, 5, 2, 3, 7 ];
var N = arr.length;
var K = 1;
longestSubsequenceLength(arr, N, K);

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)