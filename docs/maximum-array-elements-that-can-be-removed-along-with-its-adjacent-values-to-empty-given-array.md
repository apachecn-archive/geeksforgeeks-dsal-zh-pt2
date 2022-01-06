# 可移除的最大数组元素及其相邻值，以清空给定数组

> 原文:[https://www . geeksforgeeks . org/最大数组-可移除元素-及其相邻值-空给定数组/](https://www.geeksforgeeks.org/maximum-array-elements-that-can-be-removed-along-with-its-adjacent-values-to-empty-given-array/)

给定一个 **N** 大小的[阵](https://www.geeksforgeeks.org/array-data-structure/)T2【arr】。在每个操作中，选择一个数组元素 **X** ，并移除范围**【X–1，X+1】**中的所有数组元素。任务是找到所需的最大步数，这样数组中就没有硬币了。

**示例:**

> **输入:**硬币[] = {5，1，3，2，6，7，4}
> **输出:** 4
> **解释:**
> 拾取硬币硬币[1]修改数组 arr[] = {5，3，6，7，4}。
> 拾取硬币[1]修改数组 arr[] = {5，6，7}
> 拾取硬币[0]修改数组 arr[] = {7}
> 拾取硬币[0]修改数组 arr[] = {}。因此，所需的输出为 4。
> 
> **输入:**硬币[] = {6，7，5，1}
> **输出:** 3

**天真方法:**解决这个问题最简单的方法是[生成给定数组的所有可能的排列](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)，对于数组的每个排列，通过在所有可能的步骤中只挑选数组的第一个元素，找到移除数组所有元素所需的步骤数。最后，打印移除所有元素所需的最大步骤数。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是从数组中选取一个元素，在每一步中最多移除数组中的两个元素。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntSteps** 来存储从**arr【】**数组中移除所有硬币所需的最大步数。
*   创建一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说**图**以升序存储**arr【】**数组元素的频率。
*   初始化一个变量，说 **Min** 存储**地图**的最小元素。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，在每次遍历中，从**地图**中移除 **Min** 和 **(Min + 1)** ，并将 **cntSteps** 的值增加 **1** 。
*   最后，打印 **cntSteps** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum steps to
// remove all coins from the arr[]
int maximumSteps(int arr[], int N)
{

    // Store the frequency of array
    // elements in ascending order
    map<int, int> Map;

    // Traverse the arr[] array
    for (int i = 0; i < N; i++) {
        Map[arr[i]]++;
    }

    // Stores count of steps required
    // to remove all the array elements
    int cntSteps = 0;

    // Traverse the map
    for (auto i : Map) {

        // Stores the smallest element
        // of Map
        int X = i.first;

        // If frequency if X
        // greater than 0
        if (i.second > 0) {

            // Update cntSteps
            cntSteps++;

            // Mark X as
            // removed element
            Map[X] = 0;

            // If frequency of (X + 1)
            // greater than  0
            if (Map[X + 1])

                // Mark (X + 1) as
                // removed element
                Map[X + 1] = 0;
        }
    }
    return cntSteps;
}

// Driver Code
int main()
{
    int arr[] = { 5, 1, 3, 2, 6, 7, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumSteps(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find maximum steps to
// remove all coins from the arr[]
static int maximumSteps(int arr[], int N)
{

    // Store the frequency of array
    // elements in ascending order
    Map<Integer,
        Integer> mp = new HashMap<Integer,
                                  Integer>();

    // Traverse the arr[] array
    for(int i = 0; i < N; i++)
    {
        mp.put(arr[i],
               mp.getOrDefault(arr[i], 0) + 1);
    }

    // Stores count of steps required
    // to remove all the array elements
    int cntSteps = 0;

    // Traverse the mp
    for(Map.Entry<Integer, Integer> it : mp.entrySet())
    {

        // Stores the smallest element
        // of mp
        int X = it.getKey();

        // If frequency if X
        // greater than 0
        if (it.getValue() > 0)
        {

            // Update cntSteps
            cntSteps++;

            // Mark X as
            // removed element
            mp.replace(X, 0);

            // If frequency of (X + 1)
            // greater than  0
            if (mp.getOrDefault(X + 1, 0) != 0)

                // Mark (X + 1) as
                // removed element
                mp.replace(X + 1, 0);
        }
    }
    return cntSteps;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 5, 1, 3, 2, 6, 7, 4 };
    int N = arr.length;

    System.out.print(maximumSteps(arr, N));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find maximum steps to
# remove all coins from the arr[]
def maximumSteps(arr, N):

    # Store the frequency of array
    # elements in ascending order
    Map = {}

    # Traverse the arr[] array
    for i in range(N):
        Map[arr[i]] = Map.get(arr[i], 0) + 1

    # Stores count of steps required
    # to remove all the array elements
    cntSteps = 0

    # Traverse the map
    for i in Map:

        # Stores the smallest element
        # of Map
        X = i

        # If frequency if X
        # greater than 0
        if (Map[i] > 0):

            # Update cntSteps
            cntSteps += 1

            # Mark X as
            # removed element
            Map[X] = 0

            # If frequency of (X + 1)
            # greater than  0
            if (X + 1 in Map):

                # Mark (X + 1) as
                # removed element
                Map[X + 1] = 0

    return cntSteps

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 1, 3, 2, 6, 7, 4 ]
    N = len(arr)

    print(maximumSteps(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum steps to
// remove all coins from the []arr
static int maximumSteps(int []arr, int N)
{

    // Store the frequency of array
    // elements in ascending order
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the []arr array
    for(int i = 0; i < N; i++)
    {
        if (mp.ContainsKey(arr[i]))
        {
            mp[arr[i]]++;   
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Stores count of steps required
    // to remove all the array elements
    int cntSteps = 0;

    // Traverse the mp
    foreach(KeyValuePair<int, int> it in mp)
    {

        // Stores the smallest element
        // of mp
        int X = it.Key;

        // If frequency if X
        // greater than 0
        if (it.Value > 0)
        {

            // Update cntSteps
            cntSteps++;

        }
    }
    return (cntSteps + 1) / 2;
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 5, 1, 3, 2, 6, 7, 4 };
    int N = arr.Length;

    Console.Write(maximumSteps(arr, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find maximum steps to
// remove all coins from the arr[]
function maximumSteps(arr, N)
{

    // Store the frequency of array
    // elements in ascending order
    var map = new Map();

    // Traverse the arr[] array
    for (var i = 0; i < N; i++) {
        if(map.has(arr[i]))
        {
            map.set(arr[i], map.get(arr[i])+1);
        }
        else
        {
            map.set(arr[i], 1);
        }
    }

    // Stores count of steps required
    // to remove all the array elements
    var cntSteps = 0;

    // Traverse the map
    map.forEach((value, key) => {

        // Stores the smallest element
        // of map
        var X = key;

        // If frequency if X
        // greater than 0
        if (value > 0) {

            // Update cntSteps
            cntSteps++;

            // Mark X as
            // removed element
            map.set(X, 0);

            // If frequency of (X + 1)
            // greater than  0
            if (map.has(X + 1))

                // Mark (X + 1) as
                // removed element
                map.set(X+1, 0);
        }
    });

    return cntSteps;
}

// Driver Code
var arr = [5, 1, 3, 2, 6, 7, 4];
var N = arr.length;
document.write( maximumSteps(arr, N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * Log(N))*
***空间复杂度:** O(N)*