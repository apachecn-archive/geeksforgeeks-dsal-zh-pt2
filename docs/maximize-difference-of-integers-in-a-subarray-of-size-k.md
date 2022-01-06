# 最大化大小为 K 的子阵列中整数的差值

> 原文:[https://www . geeksforgeeks . org/最大化大小为 k 的子数组中的整数差/](https://www.geeksforgeeks.org/maximize-difference-of-integers-in-a-subarray-of-size-k/)

给定一个长度为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出大小为 **K.** 的子数组中整数的最大差值

> **输入:** arr = [2，3，-1，-5，4，0]，K = 3
> **输出:** 9
> **说明:**斯巴瑞[-1，-5，4]包含-5 和-4 之间的最大差值为 9
> 
> **输入:** arr = [-2，-4，0，1，5，-6，9]，K =4
> **输出:** 15
> **说明:**斯巴瑞【1，5，-6，9】包含-6 和 9 之间的最大差值为 15

**方法:**给定的问题可以使用[两点技巧](https://www.geeksforgeeks.org/two-pointers-technique/)和[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)方法以及[树形图](https://www.geeksforgeeks.org/treemap-in-java/)数据结构来解决。可以遵循以下步骤来解决问题:

*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 直到**K–1**并将元素插入**树形图，**
    *   如果整数已经出现在**树形图中，**则将其频率增加 1
*   [使用指针**向右**迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 从 **K** 直到数组结束，每次迭代:
    *   如果元素不存在，则在**树形图**中插入该元素，否则将其频率增加 1
    *   如果滑动窗口的频率为 1，则移除滑动窗口最左边的元素，否则将其频率减少 1
    *   通过从**树形图**中检索第一个和最后一个元素来计算最大和最小元素之间的差异，并更新结果 **res**
*   返回结果 **res**

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum difference in integers
// of subarray of size K
int maxDiffK(
    vector<int> arr, int K)
{

    // Initialize length of the array
    int N = arr.size();

    // Initialize a TreeMap
    map<int, int> tm;

    // Iterate the array arr till K - 1
    for (int i = 0; i < K; i++)
    {

        // Get the frequency of the
        // arr[i] from the treemap
        int f = tm[arr[i]];

        // If freq is null
        if (f == 0)
        {

            // Add the integer in the
            // treemap with frequency 1
            tm[arr[i]] = 1;
        }
        else
        {

            // Increment the frequency
            // of the element
            tm[arr[i]] = f + 1;
        }
    }

    // Initialize MaxDiff to the absolute
    // Difference between greatest and
    // smallest element in the treemap
    int maxDiff = abs(
        tm.begin()->first - tm.rbegin()->first);

    // Iterate the array arr
    // from K till the end
    for (int i = K; i < N; i++)
    {

        // Get the frequency of the
        // current element from the treemap
        int f = tm[arr[i]];

        // If freq is null then add the
        // integer in the treemap
        // with frequency 1
        if (f == 0)
        {

            tm[arr[i]] = 1;
        }
        else
        {

            // Increment the frequency
            // of the element
            tm[arr[i]] = f + 1;
        }

        int freq = tm[arr[i - K]];

        // If freq is 1 then remove the
        // value from the treemap
        if (freq == 1)
            tm.erase(tm.find(arr[i - K]));

        // Else reduce the frequency
        // of that element by 1
        else
            tm[arr[i - K]] = freq - 1;

        // Update maxDiff with the maximum
        // of difference between smallest
        // and greatest element in treemap
        // and maxDiff
        maxDiff = max(
            maxDiff,
            abs(
                tm.begin()->first - tm.rbegin()->first));
    }

    // Return the answer as maxDiff
    return maxDiff;
}

// Driver code
int main()
{

    // Initialize the array
    vector<int> arr = {2, 3, -1, -5, 4, 0};

    // Initialize the value of K
    int K = 3;

    // Call the function and
    // print the result
    cout << (maxDiffK(arr, K));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the
    // maximum difference in integers
    // of subarray of size K
    public static int maxDiffK(
        int arr[], int K)
    {

        // Initialize length of the array
        int N = arr.length;

        // Initialize a TreeMap
        TreeMap<Integer, Integer> tm
            = new TreeMap<>();

        // Iterate the array arr till K - 1
        for (int i = 0; i < K; i++) {

            // Get the frequency of the
            // arr[i] from the treemap
            Integer f = tm.get(arr[i]);

            // If freq is null
            if (f == null) {

                // Add the integer in the
                // treemap with frequency 1
                tm.put(arr[i], 1);
            }
            else {

                // Increment the frequency
                // of the element
                tm.put(arr[i], f + 1);
            }
        }

        // Initialize MaxDiff to the absolute
        // Difference between greatest and
        // smallest element in the treemap
        int maxDiff = Math.abs(
            tm.firstKey() - tm.lastKey());

        // Iterate the array arr
        // from K till the end
        for (int i = K; i < N; i++) {

            // Get the frequency of the
            // current element from the treemap
            Integer f = tm.get(arr[i]);

            // If freq is null then add the
            // integer in the treemap
            // with frequency 1
            if (f == null) {

                tm.put(arr[i], 1);
            }
            else {

                // Increment the frequency
                // of the element
                tm.put(arr[i], f + 1);
            }

            int freq = tm.get(arr[i - K]);

            // If freq is 1 then remove the
            // value from the treemap
            if (freq == 1)
                tm.remove(arr[i - K]);

            // Else reduce the frequency
            // of that element by 1
            else
                tm.put(arr[i - K], freq - 1);

            // Update maxDiff with the maximum
            // of difference between smallest
            // and greatest element in treemap
            // and maxDiff
            maxDiff = Math.max(
                maxDiff,
                Math.abs(
                    tm.firstKey()
                    - tm.lastKey()));
        }

        // Return the answer as maxDiff
        return maxDiff;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the array
        int[] arr = { 2, 3, -1, -5, 4, 0 };

        // Initialize the value of K
        int K = 3;

        // Call the function and
        // print the result
        System.out.println(maxDiffK(arr, K));
    }
}
```

## 蟒蛇 3

```
# python code for the above approach

# Function to find the
# maximum difference in integers
# of subarray of size K
def maxDiffK(arr, K):

    # Initialize length of the array
    N = len(arr)

    # Initialize a TreeMap
    tm = {}

    # Iterate the array arr till K - 1
    for i in range(0, K):

        # If freq is null
        if (not (arr[i] in tm)):

            # Add the integer in the
            # treemap with frequency 1
            tm[arr[i]] = 1
        else:

             # Increment the frequency
             # of the element
            tm[arr[i]] += 1

        # Initialize MaxDiff to the absolute
        # Difference between greatest and
        # smallest element in the treemap
    maxDiff = max(list(tm)) - min(list(tm))

    # Iterate the array arr
    # from K till the end
    for i in range(K, N):

         # If freq is null then add the
         # integer in the treemap
         # with frequency 1
        if (not (arr[i] in tm)):
            tm[arr[i]] = 1

        else:

             # Increment the frequency
             # of the element
            tm[arr[i]] += 1

        freq = tm[arr[i - K]]

        # If freq is 1 then remove the
        # value from the treemap
        if (freq == 1):
            del tm[arr[i - K]]

            # Else reduce the frequency
            # of that element by 1
        else:
            tm[arr[i - K]] -= 1

            # Update maxDiff with the maximum
            # of difference between smallest
            # and greatest element in treemap
            # and maxDiff
        maxDiff = max(maxDiff, max(list(tm)) - min(list(tm)))

    # Return the answer as maxDiff
    return maxDiff

# Driver code
if __name__ == "__main__":

    # Initialize the array
    arr = [2, 3, -1, -5, 4, 0]

    # Initialize the value of K
    K = 3

    # Call the function and
    # print the result
    print(maxDiffK(arr, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

    // Function to find the
    // maximum difference in ints
    // of subarray of size K
    public static int maxDiffK(int[] arr, int K)
    {

        // Initialize length of the array
        int N = arr.Length;

        // Initialize a TreeMap
        Dictionary<int, int> tm = new Dictionary<int, int>();

        // Iterate the array arr till K - 1
        for (int i = 0; i < K; i++)
        {

            // Get the frequency of the
            // arr[i] from the treemap
            if (!tm.ContainsKey(arr[i]))
            {

                // Add the int in the
                // treemap with frequency 1
                tm[arr[i]] = 1;
            }
            else
            {

                // Increment the frequency
                // of the element
                tm[arr[i]] += 1;
            }
        }

        // Initialize MaxDiff to the absolute
        // Difference between greatest and
        // smallest element in the treemap
        int[] keys = tm.Keys.ToArray();
        Array.Sort(keys);
        int maxDiff = Math.Abs(keys.First() - keys.Last());

        // Iterate the array arr
        // from K till the end
        for (int i = K; i < N; i++)
        {

            // Get the frequency of the
            // current element from the treemap

            if (!tm.ContainsKey(arr[i]))
            {
                tm[arr[i]] = 1;
            }
            else
            {
                // Increment the frequency
                // of the element
                tm[arr[i]] += 1;
            }

            int freq = tm[arr[i - K]];

            // If freq is 1 then remove the
            // value from the treemap
            if (freq == 1)
                tm.Remove(arr[i - K]);

            // Else reduce the frequency
            // of that element by 1
            else
                tm[arr[i - K]] = freq - 1;

            // Update maxDiff with the maximum
            // of difference between smallest
            // and greatest element in treemap
            // and maxDiff
            keys = tm.Keys.ToArray();
            Array.Sort(keys);
            maxDiff = Math.Max(maxDiff, Math.Abs(keys.First() - keys.Last()));
        }

        // Return the answer as maxDiff
        return maxDiff;
    }

    // Driver code
    public static void Main()
    {

        // Initialize the array
        int[] arr = { 2, 3, -1, -5, 4, 0 };

        // Initialize the value of K
        int K = 3;

        // Call the function and
        // print the result
        Console.Write(maxDiffK(arr, K));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to find the
// maximum difference in integers
// of subarray of size K
function maxDiffK(arr, K) {

  // Initialize length of the array
  let N = arr.length;

  // Initialize a TreeMap
  let tm = new Map();

  // Iterate the array arr till K - 1
  for (let i = 0; i < K; i++) {

    // Get the frequency of the
    // arr[i] from the treemap
    let f = tm.get(arr[i]);

    // If freq is null
    if (!f) {

      // Add the integer in the
      // treemap with frequency 1
      tm.set(arr[i], 1);
    }
    else {

      // Increment the frequency
      // of the element
      tm.set(arr[i], f + 1);
    }
  }

  // Initialize MaxDiff to the absolute
  // Difference between greatest and
  // smallest element in the treemap
  let maxDiff = Math.abs([...tm.keys()].sort((a, b) => a - b)[0] - [...tm.keys()].sort((a, b) => b - a)[0]);

  // Iterate the array arr
  // from K till the end
  for (let i = K; i < N; i++) {

    // Get the frequency of the
    // current element from the treemap
    let f = tm.get(arr[i]);

    // If freq is null then add the
    // integer in the treemap
    // with frequency 1
    if (!f) {

      tm.set(arr[i], 1);
    }
    else {

      // Increment the frequency
      // of the element
      tm.set(arr[i], f + 1);
    }

    let freq = tm.get(arr[i - K]);

    // If freq is 1 then remove the
    // value from the treemap
    if (freq == 1)
      tm.delete((arr[i - K]));

    // Else reduce the frequency
    // of that element by 1
    else
      tm.set(arr[i - K], freq - 1);

    // Update maxDiff with the maximum
    // of difference between smallest
    // and greatest element in treemap
    // and maxDiff
    maxDiff = Math.max(
      maxDiff,
      Math.abs([...tm.keys()].sort((a, b) => a - b)[0] - [...tm.keys()].sort((a, b) => b - a)[0]));
  }

  // Return the answer as maxDiff
  return maxDiff;
}

// Driver code

// Initialize the array
let arr = [2, 3, -1, -5, 4, 0];

// Initialize the value of K
let K = 3;

// Call the function and
// print the result
document.write((maxDiffK(arr, K)))

// This code is contributed by Saurabh Jaiswal

</script>
```

**Output**

```
9
```

**时间复杂度:**O(N * log K)
T3】辅助空间: O(N)