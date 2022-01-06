# 尽量减少插入或删除，使每个数组元素的频率等于其值

> 原文:[https://www . geeksforgeeks . org/最小化-插入-或-删除-使每个数组元素的频率等于其值/](https://www.geeksforgeeks.org/minimize-insertions-or-deletions-to-make-frequency-of-each-array-element-equal-to-its-value/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到使每个元素的频率等于其值所需的最小插入或删除操作。

**示例:**

> **输入:** arr = {3，2，3，1，2}
> **输出:** 1
> **解释:**最初，数组中整数的频率是 freq[3] = 2，freq[2] = 2，freq[1] = 1。在第一个操作中，将 3 插入数组。因此，数组变成 arr[] = {3，2，3，1，2，3}，每个元素的频率等于它的值。
> 
> **输入:**【3，3，4，3，1，2】
> **输出:** 2
> **说明:**在第一次操作中，从数组中删除 4。在第二个操作中，将 2 插入数组。因此，数组变成 arr[] = {3，3，3，1，2，2}，每个元素的频率等于它的值。

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。按照以下步骤解决给定的问题:

*   创建一个[散列图](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) **频率**，以存储数组所有元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   使用变量**键**迭代地图的所有值。如果 **freq【键】>键**，将贡献 **(freq【键】–键)**到总操作数，否则，将贡献 **min(freq【键】，键–freq【键】)**到总操作数。
*   创建一个变量**计数**，它存储所有可能的键值的操作计数，这些键值将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find minimum insertions or
// deletions required to make frequency
// of each element equal to its value
int minOperations(int arr[], int n)
{

    // Initializing Hash Map for making
    // freaquency map
    map<int, int> mp;

    // Making frequency map
    for (int i = 0; i < n; i++) {
        mp[arr[i]]++;
    }

    // Stores the final count of operations
    int count = 0;

    // Traversing Hash Map
    for (auto it : mp) {

        // Updating the operation count
        if (it.second >= it.first)
            count += (it.second - it.first);
        else
            count += min(it.first - it.second, it.second);
    }

    // Return Answer
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 3, 4, 3, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int count = minOperations(arr, n);
    cout << count;
    return 0;
}

// This code is contributed by kdheraj.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;

class GFG {

    // Function to find minimum insertions or
    // deletions required to make frequency
    // of each element equal to its value
    public static int minOperations(int[] arr, int n)
    {
        // Initializing Hash Map for making
        // freaquency map
        Map<Integer, Integer> freq = new HashMap<>();

        // Making frequency map
        for (int val : arr)
            freq.put(val, freq.getOrDefault(val, 0) + 1);

        // Stores the final count of operations
        int count = 0;

        // Traversing Hash Map
        for (Map.Entry mp : freq.entrySet()) {

            int key = (int)mp.getKey();
            int val = (int)mp.getValue();

            // Updating the operation count
            if (val >= key)
                count += val - key;
            else
                count += Math.min(key - val, val);
        }

        // Return Answer
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 3, 3, 4, 3, 1, 2 };
        int n = arr.length;
        System.out.println(minOperations(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach
from collections import defaultdict

# Function to find minimum insertions or
# deletions required to make frequency
# of each element equal to its value
def minOperations(arr, n):

    # Initializing Hash Map for making
    # freaquency map
    mp = defaultdict(int)

    # Making frequency map
    for i in range(n):
        mp[arr[i]] += 1

    # Stores the final count of operations
    count = 0

    # Traversing Hash Map
    for it in mp:

        # Updating the operation count
        if (mp[it] >= it):
            count += (mp[it] - it)

        else:
            count += min(it - mp[it], mp[it])

    # Return Answer
    return count

# Driver Code
if __name__ == "__main__":

    arr = [3, 3, 4, 3, 1, 2]
    n = len(arr)
    count = minOperations(arr, n)
    print(count)

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation of the above approach

using System;
using System.Collections;
using System.Collections.Generic;

class GFG {

// Function to find minimum insertions or
// deletions required to make frequency
// of each element equal to its value
static int minOperations(int []arr, int n)
{

    // Initializing Hash Map for making
    // freaquency map
    Dictionary<int, int> mp =
          new Dictionary<int, int>();

    // Making frequency map
    for (int i = 0; i < n; i++) {
        if (mp.ContainsKey(arr[i])) {
              int val = mp[arr[i]];
              mp.Remove(arr[i]);
              mp.Add(arr[i], val + 1);
        }
        else {
          mp.Add(arr[i], 1);
        }
    }

    // Stores the final count of operations
    int count = 0;

    // Traversing Hash Map
    foreach(KeyValuePair<int, int> it in mp) {

        // Updating the operation count
        if (it.Value >= it.Key)
            count += (it.Value - it.Key);
        else
            count += Math.Min(it.Key - it.Value, it.Value);
    }

    // Return Answer
    return count;
}

// Driver code
public static void Main()
{
    int[] arr = { 3, 3, 4, 3, 1, 2 };
    int n = arr.Length;
    Console.Write(minOperations(arr, n));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find minimum insertions or
// deletions required to make frequency
// of each element equal to its value
function minOperations(arr, n)
{

    // Initializing Hash Map for making
    // freaquency map
    var mp = new Map();

    // Traverse through array elements and
    // count frequencies
    for (var i = 0; i < n; i++)
    {
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1)
    }

    // Stores the final count of operations
    var count = 0;
    var keys = [];

    mp.forEach((value, key) => {
        keys.push(key);
    });
    // Traversing Hash Map
    keys.forEach((key) => {

        // Updating the operation count
        if (mp.get(key) >= key)
            count += (mp.get(key) - key);
        else
            count += Math.min(key - mp.get(key), mp.get(key));
    });

    // Return Answer
    return count;
}

// Driver Code
var arr = [ 3, 3, 4, 3, 1, 2 ];
var n = arr.length;
var count = minOperations(arr, n);
document.write(count);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)