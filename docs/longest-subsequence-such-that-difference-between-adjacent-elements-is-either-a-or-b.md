# 最长的子序列，使得相邻元素之间的差异为 A 或 B

> 原文:[https://www . geesforgeks . org/最长子序列-这样-相邻元素之间的差异-不是-a 就是-b/](https://www.geeksforgeeks.org/longest-subsequence-such-that-difference-between-adjacent-elements-is-either-a-or-b/)

给定一个大小为 **N** 的数组 **arr** ，以及两个整数 **A** 和 **B** 。任务是找出最长子序列的长度，相邻元素之间的差值为 **A** 或 **B** 。

**示例:**

> **输入** : arr[]={ 5，5，5，10，8，6，12，13 }，A=0，B=1
> **输出** : 4
> **解释**:最大长度子序列为{ 5，5，5，6}
> 
> **输入** : arr[] = {4，6，7，8，9，8，12，14，17，15}，A=2，B=1
> **输出** : 6

**逼近**:仔细看问题，问题类似于[最长连续子序列](https://www.geeksforgeeks.org/longest-consecutive-subsequence/)。它们之间唯一的区别是现在我们要计算有差异的元素 **A** 或 **B** 而不是 **1** 。现在，要解决这个问题，请遵循以下步骤:

1.  创建一个映射，将每个元素存储为关键字，以 **arr[i]** 结束的最长子序列的长度为值。
2.  现在，遍历数组 arr，对于每个元素**arr【I】**:
    *   在地图中搜索**arr【I】-A**、**arr【I】+A**、**arr【I】-B**、**arr【I】+B**。
    *   如果它们存在，找出所有的最大值和其中的 **+1** ，以获得子序列的最大长度。
3.  在地图中找到最大值，并将其作为答案返回

下面是上述方法的实现。

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// longest common subsequence with
// difference between the consecutive
// element is either A or B
int maxSubsequence(vector<int>& arr, int A, int B)
{
    int N = arr.size();

    int ans = 1;

    // Map to store the length of longest subsequence
    // ending with arr[i]
    unordered_map<int, int> mp;

    for (int i = 0; i < N; ++i) {
        int aa = 1;

        // If arr[i]-A exists
        if (mp.count(arr[i] - A)) {
            aa = mp[arr[i] - A] + 1;
        }

        // If arr[i]+A exists
        if (mp.count(arr[i] + A)) {
            aa = max(aa, mp[arr[i] + A] + 1);
        }

        // If arr[i]-B exists
        if (mp.count(arr[i] - B)) {
            aa = max(aa, mp[arr[i] - B] + 1);
        }

        // If arr[i]+B exists
        if (mp.count(arr[i] + B)) {
            aa = max(aa, mp[arr[i] + B] + 1);
        }

        mp[arr[i]] = aa;
        ans = max(ans, mp[arr[i]]);
    }

    return ans;
}

// Driver Code
int main()
{

    vector<int> arr = { 5, 5, 5, 10, 8, 6, 12, 13 };
    int A = 0, B = 1;
    cout << maxSubsequence(arr, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find the length of
// longest common subsequence with
// difference between the consecutive
// element is either A or B
static int maxSubsequence(int []arr, int A, int B)
{
    int N = arr.length;

    int ans = 1;

    // Map to store the length of longest subsequence
    // ending with arr[i]
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    for (int i = 0; i < N; ++i) {
        int aa = 1;

        // If arr[i]-A exists
        if (mp.containsKey(arr[i] - A)) {
            aa = mp.get(arr[i] - A) + 1;
        }

        // If arr[i]+A exists
        if (mp.containsKey(arr[i] + A)) {
            aa = Math.max(aa, mp.get(arr[i] + A) + 1);
        }

        // If arr[i]-B exists
        if (mp.containsKey(arr[i] - B)) {
            aa = Math.max(aa, mp.get(arr[i] - B) + 1);
        }

        // If arr[i]+B exists
        if (mp.containsKey(arr[i] + B)) {
            aa = Math.max(aa, mp.get(arr[i] + B) + 1);
        }
        mp.put(arr[i], aa);
        ans = Math.max(ans, mp.get(arr[i]));
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{

    int []arr = { 5, 5, 5, 10, 8, 6, 12, 13 };
    int A = 0, B = 1;
    System.out.print(maxSubsequence(arr, A, B));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python code for the above approach

# Function to find the length of
# longest common subsequence with
# difference between the consecutive
# element is either A or B
def maxSubsequence(arr, A, B):
    N = len(arr)
    ans = 1

    # Map to store the length of longest subsequence
    # ending with arr[i]
    mp = {}

    for i in range(0, N):
        aa = 1

        # If arr[i]-A exists
        if ((arr[i] - A) in mp):
            aa = mp[arr[i] - A] + 1

        # If arr[i]+A exists
        if ((arr[i] + A) in mp):
            aa = max(aa, mp[arr[i] + A] + 1)

        # If arr[i]-B exists
        if ((arr[i] - B) in mp):
            aa = max(aa, mp[arr[i] - B] + 1)

        # If arr[i]+B exists
        if ((arr[i] + B) in mp):
            aa = max(aa, mp[arr[i] + B] + 1)

        mp[arr[i]] = aa
        ans = max(ans, mp[arr[i]])

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [5, 5, 5, 10, 8, 6, 12, 13]

    A = 0
    B = 1

    print(maxSubsequence(arr, A, B))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find the length of
  // longest common subsequence with
  // difference between the consecutive
  // element is either A or B
  static int maxSubsequence(int[] arr, int A, int B)
  {
    int N = arr.Length;

    int ans = 1;

    // Map to store the length of longest subsequence
    // ending with arr[i]
    Dictionary<int, int> mp
      = new Dictionary<int, int>();

    for (int i = 0; i < N; ++i) {
      int aa = 1;

      // If arr[i]-A exists
      if (mp.ContainsKey(arr[i] - A)) {
        aa = mp[arr[i] - A] + 1;
      }

      // If arr[i]+A exists
      if (mp.ContainsKey(arr[i] + A)) {
        aa = Math.Max(aa, mp[arr[i] + A] + 1);
      }

      // If arr[i]-B exists
      if (mp.ContainsKey(arr[i] - B)) {
        aa = Math.Max(aa, mp[arr[i] - B] + 1);
      }

      // If arr[i]+B exists
      if (mp.ContainsKey(arr[i] + B)) {
        aa = Math.Max(aa, mp[arr[i] + B] + 1);
      }
      mp[arr[i]] = aa;
      ans = Math.Max(ans, mp[arr[i]]);
    }

    return ans;
  }

  // Driver Code
  public static void Main(string[] args)
  {

    int[] arr = { 5, 5, 5, 10, 8, 6, 12, 13 };
    int A = 0, B = 1;
    Console.WriteLine(maxSubsequence(arr, A, B));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach

        // Function to find the length of
        // longest common subsequence with
        // difference between the consecutive
        // element is either A or B
        function maxSubsequence(arr, A, B) {
            let N = arr.length;

            let ans = 1;

            // Map to store the length of longest subsequence
            // ending with arr[i]
            let mp = new Map();

            for (let i = 0; i < N; ++i) {
                let aa = 1;

                // If arr[i]-A exists
                if (mp.has(arr[i] - A)) {
                    aa = mp.get(arr[i] - A) + 1;
                }

                // If arr[i]+A exists
                if (mp.has(arr[i] + A)) {
                    aa = Math.max(aa, mp.get(arr[i] + A) + 1);
                }

                // If arr[i]-B exists
                if (mp.has(arr[i] - B)) {
                    aa = Math.max(aa, mp.get(arr[i] - B) + 1);
                }

                // If arr[i]+B exists
                if (mp.has(arr[i] + B)) {
                    aa = Math.max(aa, mp.get(arr[i] + B) + 1);
                }

                mp.set(arr[i], aa);
                ans = Math.max(ans, mp.get(arr[i]));
            }

            return ans;
        }

        // Driver Code
        let arr = [5, 5, 5, 10, 8, 6, 12, 13]
        let A = 0, B = 1;
        document.write(maxSubsequence(arr, A, B));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)