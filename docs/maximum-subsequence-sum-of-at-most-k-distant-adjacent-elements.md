# 最多 K 个远邻元素的最大子序列和

> 原文:[https://www . geeksforgeeks . org/最大子序列-k 个最远相邻元素之和/](https://www.geeksforgeeks.org/maximum-subsequence-sum-of-at-most-k-distant-adjacent-elements/)

给定一个由长度为 **N** 的整数和一个整数 **K** (1 < = K < = N)组成的数组**arr【】**，任务是找到数组中最大的子序列和，使得该子序列中的相邻元素在原始数组中的索引中最多有 **K** 的差异。换句话说，如果 **i** 和 **j** 是原始数组中子序列的两个连续元素的索引，那么 **|i-j| < = K** 。

**示例:**

> ***输入:** arr[] = {1，2，-2，4，3，1}，K = 2*
> ***输出:** 11*
> ***说明:**最大和的子*–*序列为{1，2，4，3，1}(指数间的差< =2)*
> 
> ***输入:** arr[] = {4，-2，-2，-1，3，-1}，K = 2*
> ***输出:** 5*
> ***说明:**最大和的子序列为{4，-2，3}(指数间的差< =2)*

**天真方法:** [生成数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，并检查每个子集是否满足两个相邻元素的索引最多相差 K 的条件。如果是，则将它的总和与迄今为止获得的最大总和进行比较，如果它大于迄今为止获得的总和，则更新总和。

**有效途径:**这个问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

创建一个表 **dp[]** ，其中 **dp[i]** 存储子序列的最大可能和，直到 **i <sup>第</sup>** 个索引。

*   如果当前元素是子序列的第一个元素，则:

> dp[i] =疤痕[i]

*   否则，我们必须检查以前的结果，并在该指数后面的 **K** 窗口中检查 dp 的最大结果是多少:

> dp[i] = max(arr[i] + dp[x])，其中 x 来自[i-k，i-1]

*   对于每个指数，选择给出该指数最大和的条件，因此最终[递推关系](https://www.geeksforgeeks.org/different-types-recurrence-relations-solutions/)将为:

> dp[i] = max(arr[i]，arr[i] + dp[x])，其中 i-k <= x <= i-1

因此，为了在 **K** 的窗口中检查该索引后面的最大值是什么，我们可以从 dp[i-1]迭代到 dp[i-k]并找到最大值，在这种情况下，时间复杂度将是 **O(N*K)** ，或者可以通过获取有序映射并保持每个索引的计算的 dp[i]值来降低时间复杂度。这降低了 **O(N*log(K))** 的复杂性。

下面是上述方法的实现。

## C++

```
// C++ implementation to
// C++ program to
// find the maximum sum
// subsequence such that
// two adjacent element
// have atmost difference
// of K in their indices

#include <iostream>
#include <iterator>
#include <map>
using namespace std;

int max_sum(int arr[], int N,
            int K)
{

    // DP Array to store the
    // maximum sum obtained
    // till now
    int dp[N];

    // Ordered map to store DP
    // values in a window ok K
    map<int, int> mp;

    // Initializing dp[0]=arr[0]
    dp[0] = arr[0];

    // Inserting value of DP[0]
    // in map
    mp[dp[0]]++;

    // Initializing final answer
    // with dp[0]
    int ans = dp[0];

    for (int i = 1;
         i < N; i++) {

        // when i<k there is no
        // need to delete elements
        // from map as window is
        // less than K
        if (i < K) {

            // Initializing iterator
            // to end af map
            auto it = mp.end();

            // Decreasing iterator to
            // get maximum key
            it--;

            // Evaluating DP[i]
            // from recurrence
            dp[i] = max(it->first
                            + arr[i],
                        arr[i]);

            // Inserting dp value in map
            mp[dp[i]]++;
        }
        else {

            auto it = mp.end();
            it--;
            dp[i] = max(it->first
                            + arr[i],
                        arr[i]);

            mp[dp[i]]++;

            // Deleting dp[i-k] from
            // map because window size
            // has become K+1
            mp[dp[i - K]]--;

            // Erase the key from if
            // count of dp[i-K] becomes
            // zero
            if (mp[dp[i - K]] == 0) {

                mp.erase(dp[i - K]);
            }
        }

        // Calculating final answer
        ans = max(ans, dp[i]);
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, -2,
                  4, 3, 1 };
    int N = sizeof(arr) / sizeof(int);
    int K = 2;
    cout << max_sum(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// find the maximum sum
// subsequence such that
// two adjacent element
// have atmost difference
// of K in their indices
import java.util.*;
class GFG
{
  static int max_sum(int[] arr, int N, int K)
  {

    // DP Array to store the
    // maximum sum obtained
    // till now
    int[] dp = new int[N];

    // Ordered map to store DP
    // values in a window ok K
    HashMap<Integer, Integer> mp = new HashMap<>();

    // Initializing dp[0]=arr[0]
    dp[0] = arr[0];

    // Inserting value of DP[0]
    // in map
    if(mp.containsKey(dp[0]))
    {
      mp.put(dp[0], mp.get(dp[0]) + 1);  
    }
    else{
      mp.put(dp[0], 1);
    }

    // Initializing final answer
    // with dp[0]
    int ans = dp[0];    
    for (int i = 1; i < N; i++)
    {

      // when i<k there is no
      // need to delete elements
      // from map as window is
      // less than K
      if (i < K)
      {

        // Evaluating DP[i]
        // from recurrence
        Set<Integer> keySet = mp.keySet();
        ArrayList<Integer> Keys = new ArrayList<Integer>(keySet);
        dp[i] = Math.max(Keys.get(Keys.size()-1) + arr[i], arr[i]);

        // Inserting dp value in map

        if(mp.containsKey(dp[i]))
        {
          mp.put(dp[i], mp.get(dp[i]) + 1);
        }
        else{
          mp.put(dp[i], 1);
        }
      }
      else {
        Set<Integer> keySet = mp.keySet();
        ArrayList<Integer> Keys = new ArrayList<Integer>(keySet);
        dp[i] = Math.max(Keys.get(Keys.size()-1) + arr[i], arr[i]);

        if(mp.containsKey(dp[i]))
        {
          mp.put(dp[i], mp.get(dp[i]) + 1);  
        }
        else{
          mp.put(dp[i], 1);
        }

        // Deleting dp[i-k] from
        // map because window size
        // has become K+1
        if(mp.containsKey(dp[i - K]))
        {
          mp.put(dp[i - K], mp.get(dp[i - K]) - 1);
        }
        else{
          mp.put(dp[i - K], - 1);
        }

        // Erase the key from if
        // count of dp[i-K] becomes
        // zero
        if (mp.get(dp[i - K]) == 0)
        {  
          mp.remove(dp[i - K]);
        }
      }

      // Calculating final answer
      ans = Math.max(ans, dp[i]);
    }
    return ans;
  }

  // Driver code
  public static void main(String[] args) {
    int[] arr = { 1, 2, -2,
                 4, 3, 1 };
    int N = arr.length;
    int K = 2;
    System.out.println(max_sum(arr, N, K));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program to
# find the maximum sum
# subsequence such that
# two adjacent element
# have atmost difference
# of K in their indices

def max_sum(arr, N, K):

    # DP Array to store the
    # maximum sum obtained
    # till now
    dp = [0 for i in range(N)]

    # Ordered map to store DP
    # values in a window ok K
    mp = dict()

    # Initializing dp[0]=arr[0]
    dp[0] = arr[0];

    # Inserting value of DP[0]
    # in map
    mp[dp[0]] = 1

    # Initializing final answer
    # with dp[0]
    ans = dp[0];

    for i in range(1, N):

        # when i<k there is no
        # need to delete elements
        # from map as window is
        # less than K
        if (i < K):

            # Initializing iterator
            # to end af map
            it = list(mp)[-1]

            # Evaluating DP[i]
            # from recurrence
            dp[i] = max(it + arr[i], arr[i])

            # Inserting dp value in map
            if dp[i] in mp:
                mp[dp[i]] += 1
            else:
                mp[dp[i]] = 1

        else:

            it = list(mp)[-1]

            dp[i] = max(it + arr[i],arr[i]);

            if dp[i] in mp:
                mp[dp[i]] += 1
            else:
                mp[dp[i]] = 1

            # Deleting dp[i-k] from
            # map because window size
            # has become K+1
            if mp[dp[i - K]] == 0:
                mp[dp[i - K]] -= 1

        # Calculating final answer
        ans = max(ans, dp[i]);

    return ans;

# Driver code
if __name__=='__main__':

    arr = [ 1, 2, -2, 4, 3, 1 ]
    N = len(arr)
    K = 2;

    print(max_sum(arr, N, K))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to
// find the maximum sum
// subsequence such that
// two adjacent element
// have atmost difference
// of K in their indices
using System;
using System.Collections.Generic; 
using System.Linq;
class GFG
{

  static int max_sum(int[] arr, int N, int K)
  {

    // DP Array to store the
    // maximum sum obtained
    // till now
    int[] dp = new int[N];

    // Ordered map to store DP
    // values in a window ok K
    Dictionary<int, int> mp = new Dictionary<int, int>();

    // Initializing dp[0]=arr[0]
    dp[0] = arr[0];

    // Inserting value of DP[0]
    // in map
    if(mp.ContainsKey(dp[0]))
    {
      mp[dp[0]]++;  
    }
    else{
      mp[dp[0]] = 1;
    }

    // Initializing final answer
    // with dp[0]
    int ans = dp[0];    
    for (int i = 1; i < N; i++)
    {

      // when i<k there is no
      // need to delete elements
      // from map as window is
      // less than K
      if (i < K)
      {

        // Evaluating DP[i]
        // from recurrence
        dp[i] = Math.Max(mp.Keys.Last() + arr[i], arr[i]);

        // Inserting dp value in map

        if(mp.ContainsKey(dp[i]))
        {
          mp[dp[i]]++;  
        }
        else{
          mp[dp[i]] = 1;
        }
      }
      else {

        dp[i] = Math.Max(mp.Keys.Last() + arr[i], arr[i]);

        if(mp.ContainsKey(dp[i]))
        {
          mp[dp[i]]++;  
        }
        else{
          mp[dp[i]] = 1;
        }

        // Deleting dp[i-k] from
        // map because window size
        // has become K+1
        if(mp.ContainsKey(dp[i - K]))
        {
          mp[dp[i - K]]--;  
        }
        else{
          mp[dp[i - K]] = -1;
        }

        // Erase the key from if
        // count of dp[i-K] becomes
        // zero
        if (mp[dp[i - K]] == 0)
        {  
          mp.Remove(dp[i - K]);
        }
      }

      // Calculating final answer
      ans = Math.Max(ans, dp[i] + 1);
    }
    return ans;
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 2, -2,
                 4, 3, 1 };
    int N = arr.Length;
    int K = 2;
    Console.Write(max_sum(arr, N, K));
  }
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
11
```

**时间复杂度:** *O(N*log(K))*