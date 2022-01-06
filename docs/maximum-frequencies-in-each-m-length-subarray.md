# 每个 M 长度子阵列中的最大频率

> 原文:[https://www . geesforgeks . org/每米长度最大频率-subarray/](https://www.geeksforgeeks.org/maximum-frequencies-in-each-m-length-subarray/)

给定一个由 **N** 个整数和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为每个 **M** 长度子数组( *0 < M ≤ N* )找到[最大频率](https://www.geeksforgeeks.org/frequent-element-array/)。

**示例:**

> **输入:** arr[] = {1，2，3，1，2，4，1，4，4}，M = 4
> **输出:** 2 2 1 2 2 3
> **说明:**
> 任意元素频率最大的所有 M 长度子阵列为:
> 
> 1.  {1，2，3，1}，一个元素的最大频率是 2。
> 2.  {2，3，1，2}，一个元素的最大频率是 2。
> 3.  {3，1，2，4}，一个元素的最大频率是 1。
> 4.  {1，2，4，1}，一个元素的最大频率是 2。
> 5.  {2，4，1，4}，一个元素的最大频率是 2。
> 6.  {4，1，4，4}，一个元素的最大频率是 3。
> 
> **输入:** arr[] = {1，1，2，2，3，5}，M = 4
> T3】输出: 2 2 英寸

**方法:**给定的问题可以通过找到每个 **M 尺寸子阵列的频率来解决**打印所有子阵列中的最大频率。按照以下步骤解决给定的问题:

*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)，比如说 **M** 到[存储数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率。
*   初始化变量，将**值**设为 **0** 来存储子阵列某个元素的最大频率。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   如果**(I–M)**的值大于等于 **0** ，则从地图 **M** 中减少**A【I–M】**的值。
    *   在地图 **M** 中添加**arr【I】**的值。
    *   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，将**值**更新为**值**或 **x 秒**的最大值。
    *   将**值**打印为当前 M 尺寸子阵列的最大值。

下面是上述方法的一个实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the frequency of
// the most common element in each M
// length subarrays
void maxFrequencySubarrayUtil(
    vector<int> A, int N, int M)
{
    int i = 0;

    // Stores frequency of array element
    unordered_map<int, int> m;

    // Stores the maximum frequency
    int val = 0;

    // Iterate for the first sub-array
    // and store the maximum
    for (; i < M; i++) {
        m[A[i]]++;
        val = max(val, m[A[i]]);
    }

    // Print the maximum frequency for
    // the first subarray
    cout << val << " ";

    // Iterate over the range [M, N]
    for (i = M; i < N; i++) {

        // Subtract the A[i - M] and
        // add the A[i] in the map
        m[A[i - M]]--;
        m[A[i]]++;

        val = 0;

        // Find the maximum frequency
        for (auto x : m) {
            val = max(val, x.second);
        }

        // Print the maximum frequency
        // for the current subarray
        cout << val << " ";
    }
}

// Driver Code
int main()
{
    vector<int> A = { 1, 1, 2, 2, 3, 5 };
    int N = A.size();
    int M = 4;
    maxFrequencySubarrayUtil(A, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the frequency of
    // the most common element in each M
    // length subarrays
    static void maxFrequencySubarrayUtil(int[] A, int N, int M) {
        int i = 0;

        // Stores frequency of array element
        HashMap<Integer, Integer> m = new HashMap<Integer, Integer>();

        // Stores the maximum frequency
        int val = 0;

        // Iterate for the first sub-array
        // and store the maximum
        for (; i < M; i++) {
            if (m.containsKey(A[i])) {
                m.put(A[i], m.get(A[i]) + 1);
            } else {
                m.put(A[i], 1);
            }
            val = Math.max(val, m.get(A[i]));
        }

        // Print the maximum frequency for
        // the first subarray
        System.out.print(val + " ");

        // Iterate over the range [M, N]
        for (i = M; i < N; i++) {

            // Subtract the A[i - M] and
            // add the A[i] in the map
            if (m.containsKey(i - M)) {
                m.put(i - M, m.get(i - M) - 1);
            }
            if (m.containsKey(A[i])) {
                m.put(A[i], m.get(A[i]) + 1);
            } else {
                m.put(A[i], 1);
            }

            val = 0;

            // Find the maximum frequency
            for (Map.Entry<Integer, Integer> x : m.entrySet()) {
                val = Math.max(val, x.getValue());
            }

            // Print the maximum frequency
            // for the current subarray
            System.out.print(val + " ");
        }
    }

    // Driver Code
    public static void main(String[] args) {
        int[] A = { 1, 1, 2, 2, 3, 5 };
        int N = A.length;
        int M = 4;
        maxFrequencySubarrayUtil(A, N, M);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the frequency of
# the most common element in each M
# length subarrays
def maxFrequencySubarrayUtil(A,N,M):
    i = 0

    # Stores frequency of array element
    m = {}

    # Stores the maximum frequency
    val = 0

    # Iterate for the first sub-array
    # and store the maximum
    while(i < M):
        if A[i] in m:
            m[A[i]] += 1
        else:
            m[A[i]] = 1
        val = max(val, m[A[i]])
        i += 1

    # Print the maximum frequency for
    # the first subarray
    print(val,end = " ")

    # Iterate over the range [M, N]
    for i in range(M,N,1):
        # Subtract the A[i - M] and
        # add the A[i] in the map
        if A[i - M] in m:
            m[A[i - M]] -= 1
        else:
            m[A[i - M]] = 0
        if A[i] in m:
            m[A[i]] += 1

        val = 0

        # Find the maximum frequency
        for key,value in m.items():
            val = max(val, value)

        # Print the maximum frequency
        # for the current subarray
        print(val,end=" ")

# Driver Code
if __name__ == '__main__':
    A = [1, 1, 2, 2, 3, 5]
    N = len(A)
    M = 4
    maxFrequencySubarrayUtil(A, N, M)

    # This code is contributed by ipg2016107.
```

## C#

```
using System;
using System.Collections.Generic;
public class GFG {

    // Function to find the frequency of
    // the most common element in each M
    // length subarrays
    static void maxFrequencySubarrayUtil(int[] A, int N,
                                         int M)
    {
        int i = 0;

        // Stores frequency of array element
        Dictionary<int, int> m = new Dictionary<int, int>();
        // Stores the maximum frequency
        int val = 0;

        // Iterate for the first sub-array
        // and store the maximum
        for (; i < M; i++) {
            if (m.ContainsKey(A[i])) {
                val = m[A[i]];
                m.Remove(A[i]);
                m.Add(A[i], val + 1);
            }
            else {
                m.Add(A[i], 1);
            }
            val = Math.Max(val, m[A[i]]);
        }

        // Print the maximum frequency for
        // the first subarray
        Console.Write(val + " ");

        // Iterate over the range [M, N]
        for (i = M; i < N; i++) {

            // Subtract the A[i - M] and
            // add the A[i] in the map
            if (m.ContainsKey(i - M)) {
                val = i - M;
                m.Remove(i - M);
                m.Add(i - M, val - 1);
            }
           if (m.ContainsKey(A[i])) {
                val = m[A[i]];
                m.Remove(A[i]);
                m.Add(A[i], val + 1);
            }
            else {
                m.Add(A[i], 1);
            }

            val = Math.Max(val, m[A[i]]);

        val = 0;

        // Find the maximum frequency
        foreach(KeyValuePair<int, int> x in m)
        {

            val = Math.Max(val, x.Value);
        }

        // Print the maximum frequency
        // for the current subarray
        Console.Write(val + " ");
        }
}

// Driver Code

static public void Main()
{
    int[] A = { 1, 1, 2, 2, 3, 5 };
    int N = 6;
    int M = 4;
    maxFrequencySubarrayUtil(A, N, M);
}
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the frequency of
        // the most common element in each M
        // length subarrays
        function maxFrequencySubarrayUtil(A, N, M)
        {

            // Stores frequency of array element
            let m = new Map();

            // Stores the maximum frequency
            let val = 0;

            // Iterate for the first sub-array
            // and store the maximum
            for (let i = 0; i < M; i++) {

                if (m.has(A[i])) {
                    m.set(m.get(A[i]), m.get(A[i]) + 1);
                }
                else {
                    m.set(A[i], 1);
                }
                val = Math.max(val, m.get(A[i]));
            }

            // Print the maximum frequency for
            // the first subarray
            document.write(val + " ");

            // Iterate over the range [M, N]
            for (i = M; i < N; i++) {

                // Subtract the A[i - M] and
                // add the A[i] in the map
                if (m.has(A[i - m]))
                    m.set(m.get(A[i - M]), m.get(A[i - M]) - 1);
                if (m.has(A[i]))
                    m.set(m.get(A[i]), m.get(A[i]) + 1);

                val = 0;

                // Find the maximum frequency
                for (let [key, value] of m) {
                    val = Math.max(val, value);
                }

                // Print the maximum frequency
                // for the current subarray
                document.write(val + " ");
            }
        }

        // Driver Code
        let A = [1, 1, 2, 2, 3, 5];
        let N = A.length;
        let M = 4;
        maxFrequencySubarrayUtil(A, N, M);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2 2 2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(M)*