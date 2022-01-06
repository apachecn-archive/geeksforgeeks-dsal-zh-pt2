# 从双数组中找到原数组的元素

> 原文:[https://www . geeksforgeeks . org/从双数组中查找原始数组元素/](https://www.geeksforgeeks.org/find-elements-of-original-array-from-doubled-array/)

*   给定一个由 **2*N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，它由所有元素以及另一个数组的两倍值组成，比如说 **A[]** ，任务是找到数组 **A[]** 。

**示例:**

> **输入:** arr[] = {4，1，18，2，9，8}
> **输出:** 1 4 9
> **解释:**
> 取 1，4，9 的双值后再加到原数组中，得到给定数组 arr[]的所有元素
> 
> **输入:** arr[] = {4，1，2，2，8，2，4，4 }
> T3】输出: 1 2 2 4

**方法:**给定的问题可以通过计算 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 数组元素中的数组元素的频率来解决，并且可以观察到，数组中的[最小元素将始终是原始数组的一部分，因此它可以包含在结果列表**RES【】**中。具有最小元素两倍值的元素将是不属于原始数组的重复元素，因此其频率可以从映射中减少。可以遵循以下步骤来解决问题:](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

*   [按升序排列给定的数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) **arr[]**
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)元素，并将数字及其频率存储在散列表中
*   创建结果列表 **res[]** 以存储原始列表中存在的元素
*   在结果列表中添加第一个元素，并减少具有第一个元素两倍值的元素的频率。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查地图中每个元素的频率:
    *   如果频率大于 0，则在结果列表中添加元素并减少频率。
    *   否则，跳过该元素并向前移动，因为它是一个双精度值，而不是原始数组的一部分。
*   完成以上步骤后，打印列表**RES【】**中的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the original array
// from the doubled array
vector<int> findOriginal(vector<int>& arr)
{

    // Stores the numbers and
    // their frequency
    map<int, int> numFreq;

    // Add number with their frequencies
    // in the hashmap
    for (int i = 0; i < arr.size(); i++) {
        numFreq[arr[i]]++;
    }

    // Sort the array
    sort(arr.begin(), arr.end());

    // Initialize an arraylist
    vector<int> res;

    for (int i = 0; i < arr.size(); i++) {

        // Get the frequency of the number
        int freq = numFreq[arr[i]];
        if (freq > 0) {

            // Element is of original array
            res.push_back(arr[i]);

            // Decrement the frequency of
            // the number
            numFreq[arr[i]]--;

            int twice = 2 * arr[i];

            // Decrement the frequency of
            // the number having double value
            numFreq[twice]--;
        }
    }

    // Return the resultant string
    return res;
}

// Driver Code
int main()
{

    vector<int> arr = { 4, 1, 2, 2, 2, 4, 8, 4 };
    vector<int> res = findOriginal(arr);

    // Print the result list
    for (int i = 0; i < res.size(); i++) {
        cout << res[i] << " ";
    }

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to find the original array
    // from the doubled array
    public static List<Integer>
    findOriginal(int[] arr)
    {

        // Stores the numbers and
        // their frequency
        Map<Integer, Integer> numFreq
            = new HashMap<>();

        // Add number with their frequencies
        // in the hashmap
        for (int i = 0; i < arr.length; i++) {
            numFreq.put(
                arr[i],
                numFreq.getOrDefault(arr[i], 0)
                    + 1);
        }

        // Sort the array
        Arrays.sort(arr);

        // Initialize an arraylist
        List<Integer> res = new ArrayList<>();

        for (int i = 0; i < arr.length; i++) {

            // Get the frequency of the number
            int freq = numFreq.get(arr[i]);
            if (freq > 0) {

                // Element is of original array
                res.add(arr[i]);

                // Decrement the frequency of
                // the number
                numFreq.put(arr[i], freq - 1);

                int twice = 2 * arr[i];

                // Decrement the frequency of
                // the number having double value
                numFreq.put(
                    twice,
                    numFreq.get(twice) - 1);
            }
        }

        // Return the resultant string
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {

        List<Integer> res = findOriginal(
            new int[] { 4, 1, 2, 2, 2, 4, 8, 4 });

        // Print the result list
        for (int i = 0; i < res.size(); i++) {
            System.out.print(
                res.get(i) + " ");
        }
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the original array
# from the doubled array
def findOriginal(arr):

    # Stores the numbers and
    # their frequency
    numFreq = {}

    # Add number with their frequencies
    # in the hashmap
    for i in range(0, len(arr)):
        if (arr[i] in numFreq):
            numFreq[arr[i]] += 1
        else:
            numFreq[arr[i]] = 1

    # Sort the array
    arr.sort()

    # Initialize an arraylist
    res = []

    for i in range(0, len(arr)):

        # Get the frequency of the number
        freq = numFreq[arr[i]]
        if (freq > 0):

            # Element is of original array
            res.append(arr[i])

            # Decrement the frequency of
            # the number
            numFreq[arr[i]] -= 1

            twice = 2 * arr[i]

            # Decrement the frequency of
            # the number having double value
            numFreq[twice] -= 1

    # Return the resultant string
    return res

# Driver Code
arr = [4, 1, 2, 2, 2, 4, 8, 4]
res = findOriginal(arr)

# Print the result list
for i in range(0, len(res)):
    print(res[i], end=" ")

# This code is contributed by _Saurabh_Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the original array
    // from the doubled array
    public static List<int> findOriginal(int[] arr)
    {

        // Stores the numbers and
        // their frequency
        Dictionary<int, int> numFreq = new Dictionary<int, int>();

        // Add number with their frequencies
        // in the hashmap
        for (int i = 0; i < arr.Length; i++) {
             if(numFreq.ContainsKey(arr[i])){
                numFreq[arr[i]] = numFreq[arr[i]] + 1;
            }else{
                numFreq.Add(arr[i], 1);
            }
        }

        // Sort the array
        Array.Sort(arr);

        // Initialize an arraylist
        List<int> res = new List<int>();

        for (int i = 0; i < arr.Length; i++) {

            // Get the frequency of the number
            int freq = numFreq[arr[i]];
            if (freq > 0) {

                // Element is of original array
                res.Add(arr[i]);

                // Decrement the frequency of
                // the number
                numFreq[arr[i]] = freq - 1;

                int twice = 2 * arr[i];

                // Decrement the frequency of
                // the number having double value
                numFreq[twice] = numFreq[twice] - 1;
            }
        }

        // Return the resultant string
        return res;
    }

    // Driver Code
    public static void Main()
    {

        List<int> res = findOriginal(new int[] { 4, 1, 2, 2, 2, 4, 8, 4 });

        // Print the result list
        for (int i = 0; i < res.Count; i++) {
            Console.Write(res[i] + " ");
        }
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the original array
// from the doubled array
function findOriginal(arr)
{

  // Stores the numbers and
  // their frequency
  let numFreq = new Map();

  // Add number with their frequencies
  // in the hashmap
  for (let i = 0; i < arr.length; i++) {
    if (numFreq.has(arr[i])) {
      numFreq.set(arr[i], numFreq.get(arr[i]) + 1);
    } else {
      numFreq.set(arr[i], 1);
    }
  }

  // Sort the array
  arr.sort((a, b) => a - b);

  // Initialize an arraylist
  let res = [];

  for (let i = 0; i < arr.length; i++) {
    // Get the frequency of the number
    let freq = numFreq.get(arr[i]);
    if (freq > 0) {
      // Element is of original array
      res.push(arr[i]);

      // Decrement the frequency of
      // the number
      numFreq.set(arr[i], numFreq.get(arr[i]) - 1);

      let twice = 2 * arr[i];

      // Decrement the frequency of
      // the number having double value
      numFreq.set(twice, numFreq.get(twice) - 1);
    }
  }

  // Return the resultant string
  return res;
}

// Driver Code

let arr = [4, 1, 2, 2, 2, 4, 8, 4];
let res = findOriginal(arr);

// Print the result list
for (let i = 0; i < res.length; i++) {
  document.write(res[i] + " ");
}

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
1 2 2 4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*