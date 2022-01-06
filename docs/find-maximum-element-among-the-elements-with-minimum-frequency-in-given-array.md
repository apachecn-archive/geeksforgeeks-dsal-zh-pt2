# 在给定数组中频率最小的元素中找到最大元素

> 原文:[https://www . geesforgeks . org/find-给定数组中具有最小频率的元素中的最大元素/](https://www.geeksforgeeks.org/find-maximum-element-among-the-elements-with-minimum-frequency-in-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到[个最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，最小频率为。

**示例:**

> **输入:** arr[] = {2，2，5，50，1}
> **输出:** 50
> **解释:**
> 最小频率的元素为{1，5，50}。这些元素中最大元素是 50。
> 
> **输入:** arr[] = {3，2，5，6，1}
> **输出:** 6

**方法:**给定的问题可以通过将数组元素的[频率存储在](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中，然后找到具有最小频率的最大值来解决。按照以下步骤解决给定的问题:

*   [将每个元素的频率存储在一个 HashMap 中，比如**M**T3。](https://www.geeksforgeeks.org/find-frequency-of-each-element-in-a-limited-range-array-in-less-than-on-time/)
*   初始化两个变量，将 **maxValue** 表示为 [**INT_MIN**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 和 **minFreq** 表示为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，它们存储合成的最大元素并存储所有频率中的最小频率。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** 并执行以下步骤:
    *   如果当前元素的频率小于 **minFreq** ，则将 **minFreq** 的值更新为当前频率，将 **maxValue** 的值更新为当前元素。
    *   如果当前元素的频率等于 **minFreq** 并且**最大值**的值小于当前值，则更新**最大值**的值到当前元素。
*   完成上述步骤后，打印**最大值**的值作为结果元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum element
// with the minimum frequency
int maxElementWithMinFreq(int* arr, int N)
{
    // Stores the frequency of array
    // elements
    unordered_map<int, int> mp;

    // Find the frequency and store
    // in the map
    for (int i = 0; i < N; i++) {
        mp[arr[i]]++;
    }

    // Initialize minFreq to the maximum
    // value and minValue to the minimum
    int minFreq = INT_MAX;
    int maxValue = INT_MIN;

    // Traverse the map mp
    for (auto x : mp) {

        int num = x.first;
        int freq = x.second;

        // If freq < minFreq, then update
        // minFreq to freq and maxValue
        // to the current element
        if (freq < minFreq) {
            minFreq = freq;
            maxValue = num;
        }

        // If freq is equal to the minFreq
        // and current element > maxValue
        // then update maxValue to the
        // current element
        else if (freq == minFreq
                 && maxValue < num) {
            maxValue = num;
        }
    }

    // Return the resultant maximum value
    return maxValue;
}

// Driver Code
int main()
{
    int arr[] = { 2, 2, 5, 50, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maxElementWithMinFreq(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum element
// with the minimum frequency
static int maxElementWithMinFreq(int[] arr, int N)
{

    // Stores the frequency of array
    // elements
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Find the frequency and store
    // in the map
    for (int i = 0; i < N; i++) {
        if(mp.containsKey(arr[i])){
            mp.put(arr[i], mp.get(arr[i])+1);
        }else{
            mp.put(arr[i], 1);
    }
    }

    // Initialize minFreq to the maximum
    // value and minValue to the minimum
    int minFreq = Integer.MAX_VALUE;
    int maxValue = Integer.MIN_VALUE;

    // Traverse the map mp
    for (Map.Entry<Integer,Integer> x : mp.entrySet()){

        int num = x.getKey();
        int freq = x.getValue();

        // If freq < minFreq, then update
        // minFreq to freq and maxValue
        // to the current element
        if (freq < minFreq) {
            minFreq = freq;
            maxValue = num;
        }

        // If freq is equal to the minFreq
        // and current element > maxValue
        // then update maxValue to the
        // current element
        else if (freq == minFreq
                 && maxValue < num) {
            maxValue = num;
        }
    }

    // Return the resultant maximum value
    return maxValue;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 2, 5, 50, 1 };
    int N = arr.length;
    System.out.print(maxElementWithMinFreq(arr, N));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys
from collections import defaultdict

# Function to find the maximum element
# with the minimum frequency
def maxElementWithMinFreq(arr, N):

    # Stores the frequency of array
    # elements
    mp = defaultdict(int)

    # Find the frequency and store
    # in the map
    for i in range(N):
        mp[arr[i]] += 1

    # Initialize minFreq to the maximum
    # value and minValue to the minimum
    minFreq = sys.maxsize
    maxValue = -sys.maxsize-1

    # Traverse the map mp
    for x in mp:

        num = x
        freq = mp[x]

        # If freq < minFreq, then update
        # minFreq to freq and maxValue
        # to the current element
        if (freq < minFreq):
            minFreq = freq
            maxValue = num

        # If freq is equal to the minFreq
        # and current element > maxValue
        # then update maxValue to the
        # current element
        elif (freq == minFreq
              and maxValue < num):
            maxValue = num

    # Return the resultant maximum value
    return maxValue

# Driver Code
if __name__ == "__main__":

    arr = [2, 2, 5, 50, 1]
    N = len(arr)
    print(maxElementWithMinFreq(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum element
// with the minimum frequency
static int maxElementWithMinFreq(int []arr, int N)
{

    // Stores the frequency of array
    // elements
    Dictionary<int, int> mp = new Dictionary<int,int>();

    // Find the frequency and store
    // in the map
    for (int i = 0; i < N; i++) {
        if(mp.ContainsKey(arr[i]))
        mp[arr[i]]++;
        else
          mp.Add(arr[i],1);
    }

    // Initialize minFreq to the maximum
    // value and minValue to the minimum
    int minFreq = Int32.MaxValue;
    int maxValue = Int32.MinValue;

    // Traverse the map mp
    foreach(KeyValuePair<int,int> x in mp) {

        int num = x.Key;
        int freq = x.Value;

        // If freq < minFreq, then update
        // minFreq to freq and maxValue
        // to the current element
        if (freq < minFreq) {
            minFreq = freq;
            maxValue = num;
        }

        // If freq is equal to the minFreq
        // and current element > maxValue
        // then update maxValue to the
        // current element
        else if (freq == minFreq
                 && maxValue < num) {
            maxValue = num;
        }
    }

    // Return the resultant maximum value
    return maxValue;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 2, 5, 50, 1 };
    int N = arr.Length;
    Console.Write(maxElementWithMinFreq(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the maximum element
        // with the minimum frequency
        function maxElementWithMinFreq(arr, N) {
            // Stores the frequency of array
            // elements
            let mp = new Map();

            // Find the frequency and store
            // in the map
            for (let i = 0; i < N; i++) {
                if (mp.has(arr[i])) {
                    mp.set(arr[i], mp.get(arr[i]) + 1);
                }
                else {
                    mp.set(arr[i], 1);
                }

            }

            // Initialize minFreq to the maximum
            // value and minValue to the minimum
            let minFreq = Number.MAX_VALUE
            let maxValue = Number.MIN_VALUE;

            // Traverse the map mp
            for (let [key, value] of mp) {

                let num = key;
                let freq = value;

                // If freq < minFreq, then update
                // minFreq to freq and maxValue
                // to the current element
                if (freq < minFreq) {
                    minFreq = freq;
                    maxValue = num;
                }

                // If freq is equal to the minFreq
                // and current element > maxValue
                // then update maxValue to the
                // current element
                else if (freq == minFreq
                    && maxValue < num) {
                    maxValue = num;
                }
            }

            // Return the resultant maximum value
            return maxValue;
        }

        // Driver Code

        let arr = [2, 2, 5, 50, 1];
        let N = arr.length;
        document.write(maxElementWithMinFreq(arr, N));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
50
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)