# 长度 K 的最大和子序列|集合 2

> 原文:[https://www . geesforgeks . org/maximum-sum-subsequence-of-length-k-set-2/](https://www.geeksforgeeks.org/maximum-sum-subsequence-of-length-k-set-2/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)序列**arr【】**即**【A<sub>1</sub>、A<sub>2</sub>…A<sub>n</sub>】**和一个整数 **k** ，任务是找到长度为 **k** 的子序列 S 的**最大**可能**和**

**示例:**

> **输入:** arr[] = {-1，3，4，2，5}，K = 3
> **输出:** 3 4 5
> **解释:**求和为 12 的子序列 3 4 5 是最大可能求和的子序列。
> 
> **输入:** arr[] = {6，3，4，1，1，8，7，-4，2}
> **输出:** 6 3 4 8 7

**进场:**使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决任务。想法是从子序列中的**arr【】**中获取**最大**可能的元素。按照以下步骤解决问题。

*   声明一个向量对容器，比如说**使用[]** 来存储元素及其索引。
*   遍历**arr【】**并使用【】及其索引推送**中的所有元素。**
*   [排序**使用[]** 按照非递减顺序](https://www.geeksforgeeks.org/sort-c-stl/)。
*   声明一个向量 **ans[]** 来存储最终的子序列。
*   用 I 遍历**使用[]** ，从使用中取出最后一个 **K** 元素，并推它们的索引(**使用【I】)。第二**)变成 **ans[]** 。
*   按非递减顺序对**和**进行排序，以使索引按递增顺序排列。
*   现在用 I 遍历 **ans[]** ，并用**arr【ans[I]】**替换每个元素。
*   返回**ans【】**作为后续的最终最大和。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the subsequence
// with maximum sum of length K
vector<int> maxSumSubsequence(vector<int>& arr, int N,
                              int K)
{

    // Use an extra array to keep
    // track of indices while sorting
    vector<pair<int, int> > use;

    for (int i = 0; i < N; i++) {
        use.push_back({ arr[i], i });
    }

    // Sorting in non-decreasing order
    sort(use.begin(), use.end());

    // To store the final subsequence
    vector<int> ans;

    // Pushing last K elements in ans
    for (int i = N - 1; i >= N - K; i--) {

        // Pushing indices of elements
        // which are part of final subsequence
        ans.push_back(use[i].second);
    }

    // Sorting the indices
    sort(ans.begin(), ans.end());

    // Storing elements corresponding to each indices
    for (int i = 0; i < int(ans.size()); i++)
        ans[i] = arr[ans[i]];

    // Return ans as the final result
    return ans;
}

// Driver Code
int main()
{

    int N = 9;
    vector<int> arr = { 6, 3, 4, 1, 1, 8, 7, -4, 2 };

    int K = 5;

    // Storing answer in res
    vector<int> res = maxSumSubsequence(arr, N, K);

    // Printing the result
    for (auto i : res)
        cout << i << ' ';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG {

    static class Pair {
        int first;
        int second;

        Pair(int i, int j) {
            this.first = i;
            this.second = j;
        }
    }

    // Function to find the subsequence
    // with maximum sum of length K
    static ArrayList<Integer> maxSumSubsequence(int[] arr, int N, int K) {

        // Use an extra array to keep
        // track of indices while sorting
        ArrayList<Pair> use = new ArrayList<Pair>();

        for (int i = 0; i < N; i++) {
            use.add(new Pair(arr[i], i));
        }

        // Sorting in non-decreasing order
        Collections.sort(use, new Comparator<Pair>() {
            @Override
            public int compare(Pair i, Pair j) {
                return i.first - j.first;
            }
        });

        // To store the final subsequence
        ArrayList<Integer> ans = new ArrayList<Integer>();

        // Pushing last K elements in ans
        for (int i = N - 1; i >= N - K; i--) {

            // Pushing indices of elements
            // which are part of final subsequence
            ans.add(use.get(i).second);
        }

        // Sorting the indices
        Collections.sort(ans);

        // Storing elements corresponding to each indices
        for (int i = 0; i < ans.size(); i++)
            ans.set(i, arr[ans.get(i)]);

        // Return ans as the final result
        return ans;
    }

    // Driver Code
    public static void main(String args[]) {

        int N = 9;
        int[] arr = { 6, 3, 4, 1, 1, 8, 7, -4, 2 };

        int K = 5;

        // Storing answer in res
        ArrayList<Integer> res = maxSumSubsequence(arr, N, K);

        // Printing the result
        for (int i : res)
            System.out.print(i + " ");
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for above approach

# Function to find the subsequence
# with maximum sum of length K
def maxSumSubsequence(arr, N, K):

    # Use an extra array to keep
    # track of indices while sorting
    use = []

    for i in range(0, N):
        use.append([arr[i], i])

    # Sorting in non-decreasing order
    use.sort()

    # To store the final subsequence
    ans = []

    # Pushing last K elements in ans
    for i in range(N - 1, N - K - 1, -1):

        # Pushing indices of elements
        # which are part of final subsequence
        ans.append(use[i][1])

    # Sorting the indices
    ans.sort()

    # Storing elements corresponding to each indices
    for i in range(0, len(ans)):
        ans[i] = arr[ans[i]]

    # Return ans as the final result
    return ans

# Driver Code
if __name__ == "__main__":

    N = 9
    arr = [6, 3, 4, 1, 1, 8, 7, -4, 2]

    K = 5

    # Storing answer in res
    res = maxSumSubsequence(arr, N, K)

    # Printing the result
    for i in res:
        print(i, end=' ')

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

public class GFG {

  class Pair {
    public int first;
    public int second;

    public Pair(int i, int j) {
      this.first = i;
      this.second = j;
    }
  }

  // Function to find the subsequence
  // with maximum sum of length K
  static List<int> maxSumSubsequence(int[] arr, int N, int K) {

    // Use an extra array to keep
    // track of indices while sorting
    List<Pair> use = new List<Pair>();

    for (int i = 0; i < N; i++) {
      use.Add(new Pair(arr[i], i));
    }

    // Sorting in non-decreasing order
    use.Sort((i, j) => i.first - j.first);

    // To store the readonly subsequence
    List<int> ans = new List<int>();

    // Pushing last K elements in ans
    for (int i = N - 1; i >= N - K; i--) {

      // Pushing indices of elements
      // which are part of readonly subsequence
      ans.Add(use[i].second);
    }

    // Sorting the indices
    ans.Sort();

    // Storing elements corresponding to each indices
    for (int i = 0; i < ans.Count; i++)
      ans[i] = arr[ans[i]];

    // Return ans as the readonly result
    return ans;
  }

  // Driver Code
  public static void Main(String []args) {

    int N = 9;
    int[] arr = { 6, 3, 4, 1, 1, 8, 7, -4, 2 };

    int K = 5;

    // Storing answer in res
    List<int> res = maxSumSubsequence(arr, N, K);

    // Printing the result
    foreach (int i in res)
      Console.Write(i + " ");
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the subsequence
      // with maximum sum of length K
      function maxSumSubsequence(arr, N,
          K) {

          // Use an extra array to keep
          // track of indices while sorting
          let use = [];

          for (let i = 0; i < N; i++) {
              use.push({ first: arr[i], second: i });
          }

          // Sorting in non-decreasing order
          use.sort(function (a, b) { return a.first - b.first; });

          // To store the final subsequence
          let ans = [];

          // Pushing last K elements in ans
          for (let i = N - 1; i >= N - K; i--) {

              // Pushing indices of elements
              // which are part of final subsequence
              ans.push(use[i].second);
          }

          // Sorting the indices
          ans.sort(function (a, b) { return a - b; });

          // Storing elements corresponding to each indices
          for (let i = 0; i < ans.length; i++)
              ans[i] = arr[ans[i]];

          // Return ans as the final result
          return ans;
      }

      // Driver Code

      let N = 9;
      let arr = [6, 3, 4, 1, 1, 8, 7, -4, 2]

      let K = 5;

      // Storing answer in res
      let res = maxSumSubsequence(arr, N, K);

      // Printing the result
      for (let i = 0; i < res.length; i++)
          document.write(res[i] + ' ');

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
6 3 4 8 7 
```

***时间复杂度*** **:** O(NlogN)，其中 N 是数组的大小
***辅助空间*** **:** O(N)，其中 N 是数组的大小