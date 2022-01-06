# 计数具有相等按位“与”和按位“或”值的对

> 原文:[https://www . geesforgeks . org/count-pairs-with-equal-bitwise-and-bitwise-or-value/](https://www.geeksforgeeks.org/count-pairs-with-equal-bitwise-and-and-bitwise-or-value/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是计算无序对的数量，使得每对的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)相等。

**示例:**

> **输入:** arr[] = {1，2，1}
> **输出:** 1
> **解释:**
> 按位 AND 值和按位 OR 值所有可能的对是:
> 对的按位 AND(arr[0]，arr[1])是(arr[0] & arr[1]) = (1 & 2) = 0 对的按位 AND(arr[0]，arr[1])是(arr[0] | arr arr[2])是(arr[0]&arr[2])=(1&2)= 1
> 对(arr[0]，arr[1])的位与是(arr[0] | arr[1]) = (1 | 2) = 1
> 对(arr[1]，arr[2])的位与是(arr[1]&arr[2])=(2&1)= 0
> 对(arr[2]
> 
> **输入:** arr[] = {1，2，3，1，2，2 }
> T3】输出: 4

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/array-data-structure/)和[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对。对于每对，检查该对的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)是否等于该对的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。如果发现为真，则递增计数器。最后，打印计数器的值。

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 0 & 0 = 0 和 0 | 0 = 0
> 0 & 1 = 0 和 0 | 1 = 1
> 1 & 0 = 0 和 1 | 0 = 1
> 1 & 1 = 1 和 1 | 1 = 1
> 
> 因此，如果一对中的两个元素相等，则该对的按位 AND(&)和按位 OR(|)才相等。

按照以下步骤解决问题:

*   初始化一个变量，比如 **cntPairs** 来存储位“与”(&)值和位“或”(|)值相等的对的计数。
*   创建一个地图，比如说 **mp** 来存储给定数组中所有不同元素的频率。
*   [遍历给定数组](https://www.geeksforgeeks.org/array-data-structure/)，并将给定数组中所有不同元素的频率存储在 **mp** 中。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)检查频率，说 **freq** 大于 **1** 然后更新**cntPairs+=(freq *(freq–1))/2。**
*   最后，打印 **cntPairs 的值。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs in an array
// whose bitwise AND equal to bitwise OR
int countPairs(int arr[], int N)
{

    // Store count of pairs whose
    // bitwise AND equal to bitwise OR
    int cntPairs = 0;

    // Stores frequency of
    // distinct elements of array
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Increment the frequency
        // of arr[i]
        mp[arr[i]]++;
    }

    // Traverse map
    for (auto freq: mp) {
        cntPairs += (freq.second *
                   (freq.second - 1)) / 2;
    }

    return cntPairs;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 1, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout<<countPairs(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count pairs in an array
// whose bitwise AND equal to bitwise OR
static int countPairs(int[] arr, int N)
{

    // Store count of pairs whose
    // bitwise AND equal to bitwise OR
    int cntPairs = 0;

    // Stores frequency of
    // distinct elements of array
    HashMap<Integer, Integer> mp = new HashMap<>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Increment the frequency
        // of arr[i]
        mp.put(arr[i],
               mp.getOrDefault(arr[i], 0) + 1);
    }

    // Traverse map
    for(Map.Entry<Integer, Integer> freq : mp.entrySet())
    {
        cntPairs += (freq.getValue() *
                    (freq.getValue() - 1)) / 2;
    }

    return cntPairs;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 1, 2, 2 };
    int N = arr.length;

    System.out.println(countPairs(arr, N));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count pairs in an array
# whose bitwise AND equal to bitwise OR
def countPairs(arr, N):

    # Store count of pairs whose
    # bitwise AND equal to bitwise OR
    cntPairs = 0

    # Stores frequency of
    # distinct elements of array
    mp = {}

    # Traverse the array
    for i in range(0, N):

        # Increment the frequency
        # of arr[i]
        if arr[i] in mp:
            mp[arr[i]] = mp[arr[i]] + 1
        else:
            mp[arr[i]] = 1

    # Traverse map
    for freq in mp:
        cntPairs += int((mp[freq] *
                        (mp[freq] - 1)) / 2)

    return cntPairs

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 1, 2, 2 ]
    N = len(arr)

    print(countPairs(arr, N))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count pairs in an array
// whose bitwise AND equal to bitwise OR
static int countPairs(int[] arr, int N)
{

    // Store count of pairs whose
    // bitwise AND equal to bitwise OR
    int cntPairs = 0;

    // Stores frequency of
    // distinct elements of array
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Increment the frequency
        // of arr[i]
        if (!mp.ContainsKey(arr[i]))
            mp.Add(arr[i], 1);
        else
            mp[arr[i]] = mp[arr[i]] + 1;
    }

    // Traverse map
    foreach(KeyValuePair<int, int> freq in mp)
    {
        cntPairs += (freq.Value *
                    (freq.Value - 1)) / 2;
    }

    return cntPairs;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 1, 2, 2 };
    int N = arr.Length;

    Console.WriteLine(countPairs(arr, N));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count pairs in an array
// whose bitwise AND equal to bitwise OR
function countPairs(arr, N)
{

    // Store count of pairs whose
    // bitwise AND equal to bitwise OR
    var cntPairs = 0;

    // Stores frequency of
    // distinct elements of array
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Increment the frequency
        // of arr[i]
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1);
    }

    // Traverse map
    mp.forEach((value, key) => {

        cntPairs += parseInt((value *
                   (value - 1)) / 2);
    });

    return cntPairs;
}

// Driver Code
var arr = [1, 2, 3, 1, 2, 2 ];
var N = arr.length;
document.write( countPairs(arr, N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)