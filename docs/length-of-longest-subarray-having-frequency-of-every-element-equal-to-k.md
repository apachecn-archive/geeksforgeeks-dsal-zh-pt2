# 每个元素的频率等于 K 的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/每元素频率等于 k 的最长子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-having-frequency-of-every-element-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到最长子数组的长度，使得每个元素出现 **K** 次。

**示例:**

> **输入:** **arr[]** = {3，5，2，2，4，6，4，6，5}， **K** = 2
> **输出:** 8
> **解释:**长度为 8 的子阵列:{5，2，2，4，6，4，6，5}每个元素的频率为 2。
> 
> **输入:** **arr[]** = {5，5，5，5}， **K** = 3
> **输出:** 3
> **说明:**长度为 3 的子阵:{5，5，5}每个元素的频率为 3。

**方法:**按照以下步骤解决问题:

1.  [从给定的阵列中生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。
2.  对于每个子阵列，初始化两个 [**无序映射**](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **映射 1** 和**映射 2** ，以存储每个元素的[频率，并存储具有各自频率的元素计数。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
3.  如果对于任何一个子阵来说 **map2** 的大小等于 **1** ，当前元素的频率为 **K** ，这意味着每个元素在当前子阵中单独出现 **K** 次。
4.  最后，返回所有这些子阵列的最大大小。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// required maximum subarray
int max_subarray_len(int arr[],
                     int N, int K)
{
    // Initialize answer to 0
    int ans = 0;

    // Generate all subarrays having i as the
    // starting index and j as the ending index
    for (int i = 0; i < N; i++) {

        // Stores frequency of subarray elements
        unordered_map<int, int> map1;

        // Stores subarray elements with
        // respective frequencies
        unordered_map<int, int> map2;

        for (int j = i; j < N; j++) {

            // Stores previous
            // frequency of arr[j]
            int prev_freq;

            // If arr[j] hasn't
            // occurred previously
            if (map1.find(arr[j])
                == map1.end()) {

                // Set frequency as 0
                prev_freq = 0;
            }

            else {

                // Update previous frequency
                prev_freq = map1[arr[j]];
            }

            // Increasing frequency
            // of arr[j] by 1
            map1[arr[j]]++;

            // If frequency is stored
            if (map2.find(prev_freq)
                != map2.end()) {

                // If previous frequency is 1
                if (map2[prev_freq] == 1) {

                    // Rove previous frequency
                    map2.erase(prev_freq);
                }
                else {

                    // Decrease previous frequency
                    map2[prev_freq]--;
                }
            }

            int new_freq = prev_freq + 1;

            // Increment new frequency
            map2[new_freq]++;

            // If updated frequency is equal to K
            if (map2.size() == 1
                && (new_freq) == K) {
                ans = max(
                    ans, j - i + 1);
            }
        }
    }

    // Return the maximum size
    // of the subarray
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 5, 2, 2, 4,
                  6, 4, 6, 5 };

    int K = 2;

    // Size of Array
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function Call
    cout << max_subarray_len(
        arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the length of
// required maximum subarray
static int max_subarray_len(int arr[],
                     int N, int K)
{
    // Initialize answer to 0
    int ans = 0;

    // Generate all subarrays having i as the
    // starting index and j as the ending index
    for (int i = 0; i < N; i++)
    {

        // Stores frequency of subarray elements
        HashMap<Integer,Integer> map1 = new HashMap<>();

        // Stores subarray elements with
        // respective frequencies
        HashMap<Integer,Integer> map2 = new HashMap<>();

        for (int j = i; j < N; j++)
        {

            // Stores previous
            // frequency of arr[j]
            int prev_freq = 0;

            // If arr[j] hasn't
            // occurred previously
            if (!map1.containsKey(arr[j]))
            {

                // Set frequency as 0
                prev_freq = 0;
            }

            else
            {

                // Update previous frequency
                prev_freq = map1.get(arr[j]);
            }

            // Increasing frequency
            // of arr[j] by 1
            if(map1.containsKey(arr[j]))
            {
                map1.put(arr[j], map1.get(arr[j]) + 1);
            }
            else
            {
                map1.put(arr[j], 1);
            }

            // If frequency is stored
            if (map2.containsKey(prev_freq))
            {

                // If previous frequency is 1
                if (map2.get(prev_freq) == 1)
                {

                    // Rove previous frequency
                    map2.remove(prev_freq);
                }
                else
                {

                    // Decrease previous frequency
                    map2.put(prev_freq, map2.get(prev_freq)-1);

                }
            }

            int new_freq = prev_freq + 1;

            // Increment new frequency
            if(map2.containsKey(new_freq))
            {
                map2.put(new_freq, map2.get(new_freq) + 1);
            }
            else{
                map2.put(new_freq, 1);
            }

            // If updated frequency is equal to K
            if (map2.size() == 1
                && (new_freq) == K) {
                ans = Math.max(
                    ans, j - i + 1);
            }
        }
    }

    // Return the maximum size
    // of the subarray
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 3, 5, 2, 2, 4,
                  6, 4, 6, 5 };

    int K = 2;

    // Size of Array
    int N = arr.length;

    // Function Call
    System.out.print(max_subarray_len(
        arr, N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above
# approach
from collections import defaultdict

# Function to find the length of
# required maximum subarray
def max_subarray_len(arr, N, K):

    # Initialize answer to 0
    ans = 0

    # Generate all subarrays having
    # i as the starting index and j
    # as the ending index
    for i in range(N):

        # Stores frequency of subarray
        # elements
        map1 = defaultdict(int)

        # Stores subarray elements with
        # respective frequencies
        map2 = defaultdict(int)

        for j in range(i, N):

            # If arr[j] hasn't
            # occurred previously
            if (arr[j] not in map1):

                # Set frequency as 0
                prev_freq = 0

            else:

                # Update previous frequency
                prev_freq = map1[arr[j]]

            # Increasing frequency
            # of arr[j] by 1
            map1[arr[j]] += 1

            # If frequency is stored
            if prev_freq in map2:

                # If previous frequency is 1
                if (map2[prev_freq] == 1):

                    # Rove previous frequency
                    del map2[prev_freq]

                else:

                    # Decrease previous frequency
                    map2[prev_freq] -= 1

            new_freq = prev_freq + 1

            # Increment new frequency
            map2[new_freq] += 1

            # If updated frequency is equal
            # to K
            if (len(map2) == 1 and
               (new_freq) == K):
                ans = max(ans, j - i + 1)

    # Return the maximum size
    # of the subarray
    return ans

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [3, 5, 2, 2, 4,
           6, 4, 6, 5]

    K = 2

    # Size of Array
    N = len(arr)

    # Function Call
    print(max_subarray_len(
          arr, N, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the length of
// required maximum subarray
static int max_subarray_len(int []arr,
                     int N, int K)
{
    // Initialize answer to 0
    int ans = 0;

    // Generate all subarrays having i as the
    // starting index and j as the ending index
    for (int i = 0; i < N; i++)
    {

        // Stores frequency of subarray elements
        Dictionary<int,int> map1 = new Dictionary<int,int>();

        // Stores subarray elements with
        // respective frequencies
        Dictionary<int,int> map2 = new Dictionary<int,int>();

        for (int j = i; j < N; j++)
        {

            // Stores previous
            // frequency of arr[j]
            int prev_freq = 0;

            // If arr[j] hasn't
            // occurred previously
            if (!map1.ContainsKey(arr[j]))
            {

                // Set frequency as 0
                prev_freq = 0;
            }

            else
            {

                // Update previous frequency
                prev_freq = map1[arr[j]];
            }

            // Increasing frequency
            // of arr[j] by 1
            if(map1.ContainsKey(arr[j]))
            {
                map1[arr[j]] = map1[arr[j]] + 1;
            }
            else
            {
                map1.Add(arr[j], 1);
            }

            // If frequency is stored
            if (map2.ContainsKey(prev_freq))
            {

                // If previous frequency is 1
                if (map2[prev_freq] == 1)
                {

                    // Rove previous frequency
                    map2.Remove(prev_freq);
                }
                else
                {

                    // Decrease previous frequency
                    map2[prev_freq]= map2[prev_freq]-1;

                }
            }

            int new_freq = prev_freq + 1;

            // Increment new frequency
            if(map2.ContainsKey(new_freq))
            {
                map2[new_freq] = map2[new_freq] + 1;
            }
            else{
                map2.Add(new_freq, 1);
            }

            // If updated frequency is equal to K
            if (map2.Count == 1
                && (new_freq) == K) {
                ans = Math.Max(
                    ans, j - i + 1);
            }
        }
    }

    // Return the maximum size
    // of the subarray
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []arr = { 3, 5, 2, 2, 4,
                  6, 4, 6, 5 };

    int K = 2;

    // Size of Array
    int N = arr.Length;

    // Function Call
    Console.Write(max_subarray_len(
        arr, N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the length of
// required maximum subarray
function max_subarray_len(arr,N,K)
{
    // Initialize answer to 0
    let ans = 0;

    // Generate all subarrays having i as the
    // starting index and j as the ending index
    for (let i = 0; i < N; i++)
    {

        // Stores frequency of subarray elements
        let map1 = new Map();

        // Stores subarray elements with
        // respective frequencies
        let map2 = new Map();

        for (let j = i; j < N; j++)
        {

            // Stores previous
            // frequency of arr[j]
            let prev_freq = 0;

            // If arr[j] hasn't
            // occurred previously
            if (!map1.has(arr[j]))
            {

                // Set frequency as 0
                prev_freq = 0;
            }

            else
            {

                // Update previous frequency
                prev_freq = map1.get(arr[j]);
            }

            // Increasing frequency
            // of arr[j] by 1
            if(map1.has(arr[j]))
            {
                map1.set(arr[j], map1.get(arr[j]) + 1);
            }
            else
            {
                map1.set(arr[j], 1);
            }

            // If frequency is stored
            if (map2.has(prev_freq))
            {

                // If previous frequency is 1
                if (map2.get(prev_freq) == 1)
                {

                    // Rove previous frequency
                    map2.delete(prev_freq);
                }
                else
                {

                    // Decrease previous frequency
                    map2.set(prev_freq, map2.get(prev_freq)-1);

                }
            }

            let new_freq = prev_freq + 1;

            // Increment new frequency
            if(map2.has(new_freq))
            {
                map2.set(new_freq, map2.get(new_freq) + 1);
            }
            else
            {
                map2.set(new_freq, 1);
            }

            // If updated frequency is equal to K
            if (map2.size == 1
                && (new_freq) == K)
            {
                ans = Math.max(
                    ans, j - i + 1);
            }
        }
    }

    // Return the maximum size
    // of the subarray
    return ans;
}

// Driver Code
let arr=[ 3, 5, 2, 2, 4,
                  6, 4, 6, 5 ];

let K = 2;
// Size of Array
let N = arr.length;

// Function Call
document.write(max_subarray_len(
arr, N, K));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*