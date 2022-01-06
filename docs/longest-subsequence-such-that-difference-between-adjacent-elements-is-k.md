# 最长的子序列，使得相邻元素之间的差异为 K

> 原文:[https://www . geeksforgeeks . org/最长子序列相邻元素之间的差异为-k/](https://www.geeksforgeeks.org/longest-subsequence-such-that-difference-between-adjacent-elements-is-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是找到最长的[子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得相邻子序列之间的差值为 **K** 。

**示例:**

> **输入:** arr[]={1，2，3，4，5，3，2}，K=1
> **输出:** 6
> **解释:**相邻元素之差为 1 的最长子序列为:{1，2，3，4，3，2}
> 
> **输入:** arr[]={1，2，3，2，3，7，2，1}，K=2
> **输出:** 3

**方法:**给定的问题可以使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)来解决。的想法是存储最长的[子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，该子序列在包括当前元素之后结束的相邻子序列之间具有差异 **K** 。创建一个[无序映射](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **mp** ，其中**MP【I】**表示包含整数 **i** 的子序列的最大长度。
因此，得到最大长度子序列的关系可以写成:

> **mp[i] = 1 +最大值(MP[I–K]，mp[i + K])**

地图 **mp** 中存储的最大整数就是所需答案。下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest
// subsequence such that difference
// between adjacent elements is K
int longestSubsequence(vector<int>& arr, int K)
{
    // Stores length of longest
    // subsequence in a map
    unordered_map<int, int> mp;

    // Variable to store the maximum
    // length of subsequence
    int mx = 1;

    // Loop to iterate through the
    // given array
    for (auto x : arr) {
        mp[x] = 1;

        // If (x - K) exists
        if (mp.count(x - K)) {
            mp[x] = 1 + mp[x - K];
        }

        // if (x + K) exists
        if (mp.count(x + K)) {
            mp[x] = max(mp[x], 1 + mp[x + K]);
        }

        mx = max(mx, mp[x]);
    }

    // Return Answer
    return mx;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 4, 5, 3, 2 };
    int K = 1;

    cout << longestSubsequence(arr, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.HashMap;

class GFG {

    // Function to find the longest
    // subsequence such that difference
    // between adjacent elements is K
    public static int longestSubsequence(int[] arr, int K) {

        // Stores length of longest
        // subsequence in a map
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Variable to store the maximum
        // length of subsequence
        int mx = 1;

        // Loop to iterate through the
        // given array
        for (int x : arr) {
            mp.put(x, 1);

            // If (x - K) exists
            if (mp.containsKey(x - K)) {
                mp.put(x, 1 + mp.get(x - K));
            }

            // If (x + K) exists
            if (mp.containsKey(x + K)) {
                mp.put(x, Math.max(mp.get(x), 1 + mp.get(x + K)));
            }
            mx = Math.max(mx, mp.get(x));
        }

        // Return Answer
        return mx;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 1, 2, 3, 4, 5, 3, 2 };
        int K = 1;

        System.out.print(longestSubsequence(arr, K));
    }
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# python code for the above approach

# Function to find the longest
# subsequence such that difference
# between adjacent elements is K
def longestSubsequence(arr, K):

    # Stores length of longest
    # subsequence in a map
    mp = {}

    # Variable to store the maximum
    # length of subsequence
    mx = 1

    # Loop to iterate through the
    # given array
    for x in arr:
        mp[x] = 1

        # If (x - K) exists
        if ((x - K) in mp):
            mp[x] = 1 + mp[x - K]

        # if (x + K) exists
        if ((x+K) in mp):
            mp[x] = max(mp[x], 1 + mp[x + K])

        mx = max(mx, mp[x])

    # Return Answer
    return mx

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5, 3, 2]
    K = 1

    print(longestSubsequence(arr, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the longest
// subsequence such that difference
// between adjacent elements is K
static int longestSubsequence(List<int> arr, int K)
{

    // Stores length of longest
    // subsequence in a map
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Variable to store the maximum
    // length of subsequence
    int mx = 1;

    // Loop to iterate through the
    // given array
    foreach(int x in arr)
    {
        mp[x] = 1;

        // If (x - K) exists
        if (mp.ContainsKey(x - K))
        {
            mp[x] = 1 + mp[x - K];
        }

        // If (x + K) exists
        if (mp.ContainsKey(x + K))
        {
            mp[x] = Math.Max(mp[x], 1 + mp[x + K]);
        }
        mx = Math.Max(mx, mp[x]);
    }

    // Return Answer
    return mx;
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 1, 2, 3, 4, 5, 3, 2 };
    int K = 1;

    Console.Write(longestSubsequence(arr, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
  <script>
      // JavaScript code for the above approach

      // Function to find the longest
      // subsequence such that difference
      // between adjacent elements is K
      function longestSubsequence(arr, K)
      {

          // Stores length of longest
          // subsequence in a map
          let mp = new Map();

          // Variable to store the maximum
          // length of subsequence
          let mx = 1;

          // Loop to iterate through the
          // given array
          for (let x of arr) {
              mp.set(x, 1)

              // If (x - K) exists
              if (mp.has(x - K)) {
                  mp.set(x, 1 + mp.get(x - K));
              }

              // if (x + K) exists
              if (mp.has(x + K)) {
                  mp.set(x, 1 + mp.get(x + K));
              }

              mx = Math.max(mx, mp.get(x));
          }

          // Return Answer
          return mx;
      }

      // Driver Code
      let arr = [1, 2, 3, 4, 5, 3, 2];
      let K = 1;

      document.write(longestSubsequence(arr, K));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)