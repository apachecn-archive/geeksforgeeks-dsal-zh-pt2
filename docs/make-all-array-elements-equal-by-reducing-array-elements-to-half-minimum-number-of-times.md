# 通过将数组元素减少到最小次数的一半

使所有数组元素相等

> 原文:[https://www . geesforgeks . org/通过将数组元素减少到最小次数的一半来使所有数组元素相等/](https://www.geeksforgeeks.org/make-all-array-elements-equal-by-reducing-array-elements-to-half-minimum-number-of-times/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过将**A<sub>I</sub>T9】转换为**A<sub>I</sub>2/2，将使所有数组元素相等所需的操作次数降至最低。**在每次操作中**

**示例:**

> **输入:** arr[] = {3，1，1，3}
> **输出:** 2
> **解释:**
> 将 A <sub>0</sub> 减少为 A <sub>0</sub> / 2 将 arr[]修改为{1，1，1，3}。
> 将 A <sub>3</sub> 减少到 A <sub>3</sub> / 2 将 arr[]修改为{1，1，1，1}。
> 因此，所有数组元素相等，因此，所需的最小运算量为 2。
> 
> **输入:** arr[] = {2，2，2 }
> T3】输出: 0

**进场:**解决这个问题的思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。以下是步骤:

*   初始化一个辅助[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp。**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，将元素除以 **2** 直到减少到 **1** ，并将结果数存储在地图**中。**
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)找到频率等于 **N** 的最大元素，比如 **mx** 。
*   再次，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，将元素除以 **2** ，直到它等于 **mx** 并递增计数。
*   打印计数作为所需操作的最小数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of operations
int minOperations(int arr[], int N)
{
    // Initialize map
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        int res = arr[i];

        // Divide current array
        // element until it reduces to 1
        while (res) {

            mp[res]++;
            res /= 2;
        }
    }

    int mx = 1;
    // Traverse the map
    for (auto it : mp) {
        // Find the maximum element
        // having frequency equal to N
        if (it.second == N) {
            mx = it.first;
        }
    }

    // Stores the minimum number
    // of operations required
    int ans = 0;

    for (int i = 0; i < N; i++) {
        int res = arr[i];

        // Count operations required to
        // convert current element to mx
        while (res != mx) {

            ans++;

            res /= 2;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 3, 1, 1, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    minOperations(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

  // Function to find minimum number of operations
  static void minOperations(int[] arr, int N)
  {
    // Initialize map
    HashMap<Integer,
    Integer> mp = new HashMap<Integer,
    Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++) {
      int res = arr[i];

      // Divide current array
      // element until it reduces to 1
      if (mp.containsKey(res))
        mp.put(res, mp.get(res) + 1);
      else
        mp.put(res, 1);

      res /= 2;
    }   
    int mx = 1;

    for(Map.Entry<Integer, Integer> it : mp.entrySet())
    {

      // Find the maximum element
      // having frequency equal to N
      if (it.getValue() == N)
      {
        mx = it.getKey();
      }
    }

    // Stores the minimum number
    // of operations required
    int ans = 0;

    for (int i = 0; i < N; i++)
    {
      int res = arr[i];

      // Count operations required to
      // convert current element to mx
      while (res != mx)
      {
        ans++;
        res /= 2;
      }
    }

    // Print the answer
    System.out.println(ans);
  }      

  // Driver Code
  public static void main(String[] args)
  {
    // Given array
    int arr[] = { 3, 1, 1, 3 };

    // Size of the array
    int N = arr.length;
    minOperations(arr, N);
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to find minimum number of operations
def minOperations(arr, N):

  # Initialize map
  mp = {}

  # Traverse the array
  for i in range(N):
    res = arr[i]

    # Divide current array
    # element until it reduces to 1
    while (res):
      if res in mp:
        mp[res] += 1
      else:
        mp[res] = 1
      res //= 2
  mx = 1

  # Traverse the map
  for it in mp:

    # Find the maximum element
    # having frequency equal to N
    if (mp[it] == N):
      mx = it

  # Stores the minimum number
  # of operations required
  ans = 0
  for i in range(N):
    res = arr[i]

    # Count operations required to
    # convert current element to mx
    while (res != mx):
      ans += 1
      res //= 2

  # Print the answer
  print(ans)

# Driver Code
# Given array
arr = [ 3, 1, 1, 3 ]

# Size of the array
N = len(arr)
minOperations(arr, N)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find minimum number of operations
    static void minOperations(int[] arr, int N)
    {
        // Initialize map
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Traverse the array
        for (int i = 0; i < N; i++) {
            int res = arr[i];

            // Divide current array
            // element until it reduces to 1
            while (res > 0) {
                if(mp.ContainsKey(res))
                {
                    mp[res]++;
                }
                else{
                    mp[res] = 1;
                }
                res /= 2;
            }
        }   
        int mx = 1;

        foreach(KeyValuePair<int, int> it in mp)
        {

            // Find the maximum element
            // having frequency equal to N
            if (it.Value == N)
            {
                mx = it.Key;
            }
        }

        // Stores the minimum number
        // of operations required
        int ans = 0;

        for (int i = 0; i < N; i++)
        {
            int res = arr[i];

            // Count operations required to
            // convert current element to mx
            while (res != mx)
            {
                ans++;
                res /= 2;
            }
        }

        // Print the answer
        Console.Write(ans);
    }

  // Driver code
  static void Main()
  {

    // Given array
    int[] arr = { 3, 1, 1, 3 };

    // Size of the array
    int N = arr.Length;

    minOperations(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum number of operations
function minOperations(arr, N)
{
    // Initialize map
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {
        var res = arr[i];

        // Divide current array
        // element until it reduces to 1
        while (res) {

            if(mp.has(res))
            {
                mp.set(res, mp.get(res)+1);
            }
            else
            {
                mp.set(res, 1);
            }
            res = parseInt(res/2);
        }
    }

    var mx = 1;
    // Traverse the map
    mp.forEach((value, key) => {
        // Find the maximum element
        // having frequency equal to N
        if (value == N) {
            mx = key;
        }
    });

    // Stores the minimum number
    // of operations required
    var ans = 0;

    for (var i = 0; i < N; i++) {
        var res = arr[i];

        // Count operations required to
        // convert current element to mx
        while (res != mx) {

            ans++;

            res = parseInt(res/2);
        }
    }

    // Print the answer
    document.write( ans);
}

// Driver Code

// Given array
var arr = [3, 1, 1, 3];

// Size of the array
var N = arr.length;
minOperations(arr, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N * log(max(arr[I])*
***辅助空间:** O(N)*