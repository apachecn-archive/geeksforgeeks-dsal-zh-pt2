# 找出与给定数组中元素的索引相同的非负幂的最高频率

> 原文:[https://www . geeksforgeeks . org/find-与给定数组中元素的索引相同的非负幂的最高频率/](https://www.geeksforgeeks.org/find-highest-frequency-of-non-negative-powers-that-are-same-as-indices-of-elements-in-given-array/)

给定一个具有非负整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】****N**，求与其指数相同的非负幂的元素的最大数量。

> **arr[i] = i <sup>X</sup> ，**其中 X 是非负数。

任务是返回 x 的最大频率。

**示例:**

> **输入:**arr =【1，1，4，17】
> **输出:** 2
> **解释:**
> 指数 0 处的元素 1 是 0 的幂
> 指数 1 处的元素 1 是 0 的幂
> 指数 2 处的元素 4 是 2 的幂
> 指数 3 处的元素 17 不是其指数的幂，因此不考虑
> 因此最大频率是 0 的幂
> 
> **输入:**arr =【0，1，1，9，1，25】
> **输出:** 4
> **解释:**
> 索引 0 处的元素 0 是 2 的幂
> 索引 1 处的元素 1 是 2 的幂
> 索引 2 处的元素 1 是 0 的幂
> 索引 3 处的元素 9 是 2 的幂
> 索引 4 处的元素 1， 是 0 的幂
> 索引 5 处的元素 25 是 2 的幂
> 因此最大频率是 2 的幂，也就是 4

**方法:**给定的问题可以通过找到每个索引的[幂](https://www.geeksforgeeks.org/powers-2-required-sum/)并检查它们是否等于该索引中存在的元素来解决。

按照以下步骤解决问题:

*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 从索引 2 到结束，在每个索引:
    *   使用循环将索引本身相乘，直到该值小于整数的[最大值，并且小于或等于该索引处的元素](https://www.geeksforgeeks.org/integer-max_value-and-integer-min_value-in-java-with-examples/)
        *   如果幂等于元素，那么检查它是否存在于散列表中:
            *   如果不存在幂，则将其添加到值为 1 的哈希映射中
            *   否则，如果电源已经存在，则将其频率增加 1
*   如果 **arr[0] = 1，**则将散列表中 0 的频率增加 1
*   [迭代 HashMap](https://www.geeksforgeeks.org/iterate-map-java/) 找到频率最高的值:
    *   如果 **arr[0] = 1，**则除 0 之外的所有值的频率增加 1
*   如果 **arr[1] = 1，**则返回， **maxFreq +1，**否则返回 **maxFreq**

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of elements which
// are a non-negative power of their indices
int indPowEqualsEle(vector<int> arr)
{

    // Length of the array
    int len = arr.size();

    // Initialize the hashmap to store
    // the frequency of elements
    unordered_map<int, int> map;

    // Initialize maximum value
    // of integer into long
    long limit = INT_MAX;

    // Iterate the array arr from index 2
    for (int i = 2; i < len; i++)
    {

        // If current element is equal to 1
        // then its equal to index power 0
        if (arr[i] == 1)
        {

            // Increment the frequency of 0 by 1
            map[0]++;
            continue;
        }

        // Initialize a variable to index
        // which is to be multiplied
        // by the index
        long indPow = i;

        // Initialize a variable to
        // store the power of the index
        int p = 1;

        while (indPow <= limit && indPow <= arr[i])
        {

            // Element is equal to
            // a power of its index
            if (arr[i] == indPow)
            {

                // Increment the frequency
                // of p by 1
                map[p]++;

                break;
            }

            // Increment power
            p++;

            // Multiply current value with
            // index to get the next power
            indPow *= i;
        }
    }

    // If arr[0] == 1, then increment
    // the frequency of 0 in the hashmap
    map[0]++;

    // Initialize maxFreq to 0 to calculate
    // maximum frequency of powers
    int maxFreq = 0;

    // Iterate the hashmap
    for (auto it = map.begin(); it != map.end(); it++)
    {
        int power = it->second;
        // If arr[0] == 0, then increment the
        // frequency of all powers except 0
        if (arr[0] == 0 && power != 0)
        {

            maxFreq = max(maxFreq,
                          map[power] + 1);
        }
        else
        {

            maxFreq = max(maxFreq,
                          map[power]);
        }
    }

    // Increment the maximum frequency by 1
    // If arr[1] is equal to 1
    return arr[1] == 1
               ? maxFreq + 1
               : maxFreq;
}

// Driver function
int main()
{

    // Initialize an array
    vector<int> arr = {0, 1, 1, 9, 1, 25};

    // Call the function
    // and print the answer
    cout << (indPowEqualsEle(arr));
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find count of elements which
    // are a non-negative power of their indices
    public static int indPowEqualsEle(int[] arr)
    {

        // Length of the array
        int len = arr.length;

        // Initialize the hashmap to store
        // the frequency of elements
        Map<Integer, Integer> map
            = new HashMap<>();

        // Initialize maximum value
        // of integer into long
        long limit = (long)Integer.MAX_VALUE;

        // Iterate the array arr from index 2
        for (int i = 2; i < len; i++) {

            // If current element is equal to 1
            // then its equal to index power 0
            if (arr[i] == 1) {

                // Increment the frequency of 0 by 1
                map.put(0,
                        map.getOrDefault(0, 0) + 1);
                continue;
            }

            // Initialize a variable to index
            // which is to be multiplied
            // by the index
            long indPow = i;

            // Initialize a variable to
            // store the power of the index
            int p = 1;

            while (indPow <= limit
                   && indPow <= arr[i]) {

                // Element is equal to
                // a power of its index
                if (arr[i] == indPow) {

                    // Increment the frequency
                    // of p by 1
                    map
                        .put(p,
                             map.getOrDefault(p, 0) + 1);

                    break;
                }

                // Increment power
                p++;

                // Multiply current value with
                // index to get the next power
                indPow *= i;
            }
        }

        // If arr[0] == 1, then increment
        // the frequency of 0 in the hashmap
        map.put(0, map.getOrDefault(0, 0) + 1);

        // Initialize maxFreq to 0 to calculate
        // maximum frequency of powers
        int maxFreq = 0;

        // Iterate the hashmap
        for (int power : map.keySet()) {

            // If arr[0] == 0, then increment the
            // frequency of all powers except 0
            if (arr[0] == 0 && power != 0) {

                maxFreq
                    = Math.max(maxFreq,
                               map.get(power) + 1);
            }
            else {

                maxFreq = Math.max(maxFreq,
                                   map.get(power));
            }
        }

        // Increment the maximum frequency by 1
        // If arr[1] is equal to 1
        return arr[1] == 1
            ? maxFreq + 1
            : maxFreq;
    }

    // Driver function
    public static void main(String[] args)
    {

        // Initialize an array
        int[] arr = { 0, 1, 1, 9, 1, 25 };

        // Call the function
        // and print the answer
        System.out.println(indPowEqualsEle(arr));
    }
}
```

## 蟒蛇 3

```
# Python 3 code for the above approach
from collections import defaultdict
import sys

# Function to find count of elements which
# are a non-negative power of their indices
def indPowEqualsEle(arr):

    # Length of the array
    length = len(arr)

    # Initialize the hashmap to store
    # the frequency of elements
    map = defaultdict(int)

    # Initialize maximum value
    # of integer into long
    limit = sys.maxsize

    # Iterate the array arr from index 2
    for i in range(2, length):

        # If current element is equal to 1
        # then its equal to index power 0
        if (arr[i] == 1):

            # Increment the frequency of 0 by 1
            map[0] += 1
            continue

        # Initialize a variable to index
        # which is to be multiplied
        # by the index
        indPow = i

        # Initialize a variable to
        # store the power of the index
        p = 1

        while (indPow <= limit and indPow <= arr[i]):

            # Element is equal to
            # a power of its index
            if (arr[i] == indPow):

                # Increment the frequency
                # of p by 1
                map[p] += 1

                break

            # Increment power
            p += 1

            # Multiply current value with
            # index to get the next power
            indPow *= i

    # If arr[0] == 1, then increment
    # the frequency of 0 in the hashmap
    map[0] += 1

    # Initialize maxFreq to 0 to calculate
    # maximum frequency of powers
    maxFreq = 0

    # Iterate the hashmap
    for it in range(len(map)):

        power = map[it]
        # If arr[0] == 0, then increment the
        # frequency of all powers except 0
        if (arr[0] == 0 and power != 0):

            maxFreq = max(maxFreq,
                          map[power] + 1)
        else:

            maxFreq = max(maxFreq,
                          map[power])

    # Increment the maximum frequency by 1
    # If arr[1] is equal to 1
    if(arr[1] == 1):
        return maxFreq + 1
    return maxFreq

# Driver function
if __name__ == "__main__":

    # Initialize an array
    arr = [0, 1, 1, 9, 1, 25]

    # Call the function
    # and print the answer
    print(indPowEqualsEle(arr))

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to find count of elements which
    // are a non-negative power of their indices
    public static int indPowEqualsEle(int[] arr)
    {

        // Length of the array
        int len = arr.Length;

        // Initialize the hashmap to store
        // the frequency of elements
        Dictionary<int, int> map
            = new Dictionary<int, int>();

        // Initialize maximum value
        // of integer into long
        long limit = (long)int.MaxValue;

        // Iterate the array arr from index 2
        for (int i = 2; i < len; i++) {

            // If current element is equal to 1
            // then its equal to index power 0
            if (arr[i] == 1) {

                // Increment the frequency of 0 by 1
                if(map.ContainsKey(0))
                    map[0] = map[0]+1;
                else
                    map.Add(0, 1);
                continue;
            }

            // Initialize a variable to index
            // which is to be multiplied
            // by the index
            long indPow = i;

            // Initialize a variable to
            // store the power of the index
            int p = 1;

            while (indPow <= limit
                   && indPow <= arr[i]) {

                // Element is equal to
                // a power of its index
                if (arr[i] == indPow) {

                    // Increment the frequency
                    // of p by 1
                    if(map.ContainsKey(p))
                    map[p] = map[p]+1;
                else
                    map.Add(p, 1);

                    break;
                }

                // Increment power
                p++;

                // Multiply current value with
                // index to get the next power
                indPow *= i;
            }
        }

        // If arr[0] == 1, then increment
        // the frequency of 0 in the hashmap
        if(map.ContainsKey(0))
            map[0] = map[0]+1;
        else
            map.Add(0, 1);

        // Initialize maxFreq to 0 to calculate
        // maximum frequency of powers
        int maxFreq = 0;

        // Iterate the hashmap
        foreach (int power in map.Keys) {

            // If arr[0] == 0, then increment the
            // frequency of all powers except 0
            if (arr[0] == 0 && power != 0) {

                maxFreq
                    = Math.Max(maxFreq,
                               map[power] + 1);
            }
            else {

                maxFreq = Math.Max(maxFreq,
                                   map[power]);
            }
        }

        // Increment the maximum frequency by 1
        // If arr[1] is equal to 1
        return arr[1] == 1
            ? maxFreq + 1
            : maxFreq;
    }

    // Driver function
    public static void Main(String[] args)
    {

        // Initialize an array
        int[] arr = { 0, 1, 1, 9, 1, 25 };

        // Call the function
        // and print the answer
        Console.WriteLine(indPowEqualsEle(arr));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to find count of elements which
// are a non-negative power of their indices
function indPowEqualsEle(arr) {

  // Length of the array
  let len = arr.length;

  // Initialize the hashmap to store
  // the frequency of elements
  let map = new Map();

  // Initialize maximum value
  // of integer into long
  let limit = Number.MAX_SAFE_INTEGER;

  // Iterate the array arr from index 2
  for (let i = 2; i < len; i++) {

    // If current element is equal to 1
    // then its equal to index power 0
    if (arr[i] == 1) {

      // Increment the frequency of 0 by 1
      if (map.has(0)) {
        map.set(0, map.get(0) + 1)
      } else {
        map.set(0, 1)
      }
      continue;
    }

    // Initialize a variable to index
    // which is to be multiplied
    // by the index
    let indPow = i;

    // Initialize a variable to
    // store the power of the index
    let p = 1;

    while (indPow <= limit && indPow <= arr[i]) {

      // Element is equal to
      // a power of its index
      if (arr[i] == indPow) {

        // Increment the frequency
        // of p by 1
        if (map.has(p)) {
          map.set(p, map.get(p) + 1)
        } else {
          map.set(p, 1)
        }

        break;
      }

      // Increment power
      p++;

      // Multiply current value with
      // index to get the next power
      indPow *= i;
    }
  }

  // If arr[0] == 1, then increment
  // the frequency of 0 in the hashmap
  if (map.has(0)) {
    map.set(0, map.get(0) + 1)
  } else {
    map.set(0, 1)
  }

  // Initialize maxFreq to 0 to calculate
  // maximum frequency of powers
  let maxFreq = 0;

  // Iterate the hashmap
  for (let power of map.keys()) {

    // If arr[0] == 0, then increment the
    // frequency of all powers except 0
    if (arr[0] == 0 && power != 0) {

      maxFreq = Math.max(maxFreq,
        map.get(power) + 1);
    }
    else {

      maxFreq = Math.max(maxFreq,
        map.get(power));
    }
  }

  // Increment the maximum frequency by 1
  // If arr[1] is equal to 1
  return arr[1] == 1
    ? maxFreq + 1
    : maxFreq;
}

// Driver function
// Initialize an array
let arr = [0, 1, 1, 9, 1, 25];

// Call the function
// and print the answer
document.write((indPowEqualsEle(arr)))

// This code is contributed by gfgking.
</script>
```

**Output**

```
4
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(1)