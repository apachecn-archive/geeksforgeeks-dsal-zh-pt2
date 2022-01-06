# 按位异或为 K 的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最长子数组的长度-按位异或是-k/](https://www.geeksforgeeks.org/length-of-the-longest-subarray-whose-bitwise-xor-is-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找到最长的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的长度，该子数组的所有元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **K** 。

**示例:**

> **输入:** arr[] = { 1，2，4，7，2 }，K = 1
> **输出:** 3
> **解释:**
> 位异或等于 K(= 1)的子阵列为{ { 1 }、{ 2，4，7 }、{ 1 }。
> 因此，按位异或等于 K(= 1)的最长子阵列的长度为 3
> 
> **输入:** arr[] = { 2，5，6，1，0，3，5，6 }，K = 4
> **输出:** 6
> **解释:**
> 位异或等于 K(= 4)的子阵列为{ { 6，1，0，3 }，{ 5，6，1，0，3，5 } }。
> 因此，按位异或等于 K(= 4)的最长子阵列的长度为 6。

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)和[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)可以解决这个问题。以下是观察结果:

> a<sub>1</sub>^ a<sub>2</sub>^ a<sub>3</sub>^…..^ a <sub>n</sub> = K
> 
> => a <sub>2</sub> ^ a <sub>3</sub> ^ …..^ a <sub>n</sub> ^ K = a <sub>1</sub>

按照以下步骤解决问题:

*   初始化一个变量，比如说**前缀异或**，以存储所有元素的按位异或，直到给定数组的第 **i <sup>第</sup>T5】个索引。**
*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **mp** ，来存储数组的计算前缀 xor 的索引。
*   初始化一个变量，比如 **maxLen** ，存储最长子阵列的长度，其[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **K** 。
*   [使用变量 **i** 遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。对于每个 **i <sup>th</sup>** 索引，更新**prefix xor = prefix xor ^ arr[I]**并检查地图中是否存在 **(prefixXOR ^ K)** 。如果发现为真，则更新 **maxLen = max(maxLen，I–MP[prefixxor ^ k])**。
*   如果地图中不存在**前缀**，则[将](https://www.geeksforgeeks.org/map-insert-in-c-stl/) **前缀**插入到地图中。
*   最后打印 **maxLen** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the longest
// subarray whose bitwise XOR is equal to K
int LongestLenXORK(int arr[], int N, int K)
{

    // Stores prefix XOR
    // of the array
    int prefixXOR = 0;

    // Stores length of longest subarray
    // having bitwise XOR equal to K
    int maxLen = 0;

    // Stores index of prefix
    // XOR of the array
    map<int, int> mp;

    // Insert 0 into the map
    mp[0] = -1;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update prefixXOR
        prefixXOR ^= arr[i];

        // If (prefixXOR ^ K) present
        // in the map
        if (mp.count(prefixXOR ^ K)) {

            // Update maxLen
            maxLen = max(maxLen,
               (i - mp[prefixXOR ^ K]));
        }

        // If prefixXOR not present
        // in the Map
        if (!mp.count(prefixXOR)) {

            // Insert prefixXOR
            // into the map
            mp[prefixXOR] = i;
        }
    }

    return maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 7, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 1;
    cout<< LongestLenXORK(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the length of the longest
// subarray whose bitwise XOR is equal to K
static int LongestLenXORK(int arr[],
                          int N, int K)
{

    // Stores prefix XOR
    // of the array
    int prefixXOR = 0;

    // Stores length of longest subarray
    // having bitwise XOR equal to K
    int maxLen = 0;

    // Stores index of prefix
    // XOR of the array
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Insert 0 into the map
    mp.put(0, -1);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update prefixXOR
        prefixXOR ^= arr[i];

        // If (prefixXOR ^ K) present
        // in the map
        if (mp.containsKey(prefixXOR ^ K))
        {

            // Update maxLen
            maxLen = Math.max(maxLen,
               (i - mp.get(prefixXOR ^ K)));
        }

        // If prefixXOR not present
        // in the Map
        if (!mp.containsKey(prefixXOR))
        {

            // Insert prefixXOR
            // into the map
            mp.put(prefixXOR, i);
        }
    }
    return maxLen;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 7, 2 };
    int N = arr.length;
    int K = 1;

    System.out.print(LongestLenXORK(arr, N, K));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the length of the longest
# subarray whose bitwise XOR is equal to K
def LongestLenXORK(arr, N, K):

    # Stores prefix XOR
    # of the array
    prefixXOR = 0

    # Stores length of longest subarray
    # having bitwise XOR equal to K
    maxLen = 0

    # Stores index of prefix
    # XOR of the array
    mp = {}

    # Insert 0 into the map
    mp[0] = -1

    # Traverse the array
    for i in range(N):

        # Update prefixXOR
        prefixXOR ^= arr[i]

        # If (prefixXOR ^ K) present
        # in the map
        if (prefixXOR ^ K) in mp:

            # Update maxLen
            maxLen = max(maxLen,
                        (i - mp[prefixXOR ^ K]))

        # If prefixXOR not present
        # in the Map
        else:

            # Insert prefixXOR
            # into the map
            mp[prefixXOR] = i

    return maxLen

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 4, 7, 2 ]
    N = len(arr)
    K = 1

    print(LongestLenXORK(arr, N, K))

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to find the length of the longest
// subarray whose bitwise XOR is equal to K
static int longestLenXORK(int []arr,
                          int N, int K)
{

    // Stores prefix XOR
    // of the array
    int prefixXOR = 0;

    // Stores length of longest subarray
    // having bitwise XOR equal to K
    int maxLen = 0;

    // Stores index of prefix
    // XOR of the array
    Dictionary<int,
            int> mp = new Dictionary<int,
                                      int>();

    // Insert 0 into the map
    mp.Add(0, -1);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update prefixXOR
        prefixXOR ^= arr[i];

        // If (prefixXOR ^ K) present
        // in the map
        if (mp.ContainsKey(prefixXOR ^ K))
        {

            // Update maxLen
            maxLen = Math.Max(maxLen,
               (i - mp[prefixXOR ^ K]));
        }

        // If prefixXOR not present
        // in the Map
        if (!mp.ContainsKey(prefixXOR))
        {

            // Insert prefixXOR
            // into the map
            mp.Add(prefixXOR, i);
        }
    }
    return maxLen;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {1, 2, 4, 7, 2};
    int N = arr.Length;
    int K = 1;

    Console.Write(longestLenXORK(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the length of the longest
// subarray whose bitwise XOR is equal to K
function LongestLenXORK(arr, N, K)
{

    // Stores prefix XOR
    // of the array
    var prefixXOR = 0;

    // Stores length of longest subarray
    // having bitwise XOR equal to K
    var maxLen = 0;

    // Stores index of prefix
    // XOR of the array
    var mp = new Map();

    // Insert 0 into the map
    mp.set(0, -1);

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update prefixXOR
        prefixXOR ^= arr[i];

        // If (prefixXOR ^ K) present
        // in the map
        if (mp.has(prefixXOR ^ K)) {

            // Update maxLen
            maxLen = Math.max(maxLen,
               (i - mp.get(prefixXOR ^ K)));
        }

        // If prefixXOR not present
        // in the Map
        if (!mp.has(prefixXOR)) {

            // Insert prefixXOR
            // into the map
            mp.set(prefixXOR, i);
        }
    }

    return maxLen;
}

// Driver Code
var arr = [1, 2, 4, 7, 2];
var N =  arr.length;
var K = 1;
document.write( LongestLenXORK(arr, N, K));

</script>
```

**输出:**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)