# 最小化要添加到给定数组的元素，使其包含另一个给定数组作为子序列|集合 2

> 原文:[https://www . geesforgeks . org/最小化要添加到给定数组中的元素，使其包含另一个给定数组作为其子序列集-2/](https://www.geeksforgeeks.org/minimize-elements-to-be-added-to-a-given-array-such-that-it-contains-another-given-array-as-its-subsequence-set-2/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和另一个由 **M** 个整数组成的数组**B【】**，任务是找到要添加到数组**B【】**中的元素的最小数量，使得数组**A【】**成为数组**B【】**的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> ***输入:** N = 5，M = 6，A[] = {1，2，3，4，5}，B[] = {2，5，6，4，9，12}*
> ***输出:** 3*
> ***说明:***
> *以下是需要添加的元素:*
> *1)在 B[*的元素 2 前添加 1
> *因此，得到的数组 B[]为{1，2，5，6，3，4，9，12，5}。*
> *因此，A[]是 B[]在加上 3 个元素后的子序列。*
> 
> ***输入:** N = 5，M = 5，A[] = {3，4，5，2，7}，B[] = {3，4，7，9，2}*
> ***输出:** 2*
> ***说明:***
> *以下是需要添加的元素:*
> *1)在元素 4 后添加 5。*
> *2)在元素 5 后增加 2。*
> *因此，得到的数组 B[]为{3，4，5，2，7，9，2}。*
> *因此，需要添加 2 个元素。*

**天真的做法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/minimize-elements-to-be-added-to-a-given-array-such-that-it-contains-another-given-array-as-its-subsequence/)了解解决问题最简单的方法。

***时间复杂度:**O(N * 2<sup>M</sup>)*
***辅助空间:** O(M + N)*

[**【动态规划】**](https://www.geeksforgeeks.org/dynamic-programming/) **方法:**基于最长公共子序列的方法参见本文[前一篇文章](https://www.geeksforgeeks.org/minimize-elements-to-be-added-to-a-given-array-such-that-it-contains-another-given-array-as-its-subsequence/)。

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*

**高效方法:**这个想法类似于从数组 **B[]** 中找到[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/) ( **LIS** )。按照以下步骤解决问题:

*   考虑存在于数组**A【】**中的数组**B【】**的元素，并将数组**A【】**的每个元素的索引存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中
*   然后，使用二分搜索法找到 [LIS 数组**sub q[]**，该数组由递增顺序的索引组成。](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)
*   最后，要插入到数组中的元素的最小数量 **B[]** 等于**N–len(LIS)**，其中 **len(LIS)** 在上述步骤中使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)计算。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// element to be added in array
// B so that array A become
// subsequence of array B
int minElements(int A[], int B[],
                int N, int M)
{
  // Stores indices of the
  // array elements
  map<int, int> map;

  // Iterate over the array
  for (int i = 0; i < N; i++)
  {
    // Store the indices of
    // the array elements
    map[A[i]] = i;
  }

  // Stores the LIS
  vector<int> subseq;

  int l = 0, r = -1;

  for (int i = 0; i < M; i++)
  {
    // Check if element B[i]
    // is in array A[]
    if (map.find(B[i]) !=
        map.end())
    {
      int e = map[B[i]];

      // Perform Binary Search
      while (l <= r)
      {
        // Find the value of
        // mid m
        int m = l + (r - l) / 2;

        // Update l and r
        if (subseq[m] < e)
          l = m + 1;
        else
          r = m - 1;
      }

      // If found better element
      // 'e' for pos r + 1
      if (r + 1 < subseq.size())
      {
        subseq[r + 1] = e;
      }

      // Otherwise, extend the
      // current subsequence
      else
      {
        subseq.push_back(e);
      }

      l = 0;
      r = subseq.size() - 1;
    }
  }

  // Return the answer
  return N - subseq.size();
}

// Driver code
int main()
{
  // Given arrays
  int A[] = {1, 2, 3, 4, 5};
  int B[] = {2, 5, 6, 4, 9, 12};

  int M = sizeof(A) /
          sizeof(A[0]);
  int N = sizeof(B) /
          sizeof(B[0]);

  // Function Call
  cout << minElements(A, B,
                      M, N);

  return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to return minimum element
    // to be added in array B so that array
    // A become subsequence of array B
    static int minElements(
        int[] A, int[] B, int N, int M)
    {

        // Stores indices of the
        // array elements
        Map<Integer, Integer> map
            = new HashMap<>();

        // Iterate over the array
        for (int i = 0;
             i < A.length; i++) {

            // Store the indices of
            // the array elements
            map.put(A[i], i);
        }

        // Stores the LIS
        ArrayList<Integer> subseq
            = new ArrayList<>();

        int l = 0, r = -1;

        for (int i = 0; i < M; i++) {

            // Check if element B[i]
            // is in array A[]
            if (map.containsKey(B[i])) {

                int e = map.get(B[i]);

                // Perform Binary Search
                while (l <= r) {

                    // Find the value of
                    // mid m
                    int m = l + (r - l) / 2;

                    // Update l and r
                    if (subseq.get(m) < e)
                        l = m + 1;
                    else
                        r = m - 1;
                }

                // If found better element
                // 'e' for pos r + 1
                if (r + 1 < subseq.size()) {
                    subseq.set(r + 1, e);
                }

                // Otherwise, extend the
                // current subsequence
                else {
                    subseq.add(e);
                }

                l = 0;
                r = subseq.size() - 1;
            }
        }

        // Return the answer
        return N - subseq.size();
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given arrays
        int[] A = { 1, 2, 3, 4, 5 };
        int[] B = { 2, 5, 6, 4, 9, 12 };

        int M = A.length;
        int N = B.length;

        // Function Call
        System.out.println(
            minElements(A, B, M, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return minimum element
# to be added in array B so that array
# A become subsequence of array B
def minElements(A, B, N, M):

    # Stores indices of the
    # array elements
    map = {}

    # Iterate over the array
    for i in range(len(A)):

        # Store the indices of
        # the array elements
        map[A[i]] = i

    # Stores the LIS
    subseq = []

    l = 0
    r = -1

    for i in range(M):

        # Check if element B[i]
        # is in array A[]
        if B[i] in map:
            e = map[B[i]]

            # Perform Binary Search
            while (l <= r):

                # Find the value of
                # mid m
                m = l + (r - l) // 2

                # Update l and r
                if (subseq[m] < e):
                    l = m + 1
                else:
                    r = m - 1

            # If found better element
            # 'e' for pos r + 1
            if (r + 1 < len(subseq)):
                subseq[r + 1]= e

            # Otherwise, extend the
            # current subsequence
            else:
                subseq.append(e)

            l = 0
            r = len(subseq) - 1

    # Return the answer
    return N - len(subseq)

# Driver Code
if __name__ == '__main__':

    # Given arrays
    A = [ 1, 2, 3, 4, 5 ]
    B = [ 2, 5, 6, 4, 9, 12 ]

    M = len(A)
    N = len(B)

    # Function call
    print(minElements(A, B, M, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return minimum element
// to be added in array B so that array
// A become subsequence of array B
static int minElements(int[] A, int[] B,
                       int N, int M)
{
  // Stores indices of the
  // array elements
  Dictionary<int,
             int> map = new Dictionary<int,
                                       int>();

  // Iterate over the array
  for (int i = 0;
           i < A.Length; i++)
  {
    // Store the indices of
    // the array elements
    map.Add(A[i], i);
  }

  // Stores the LIS
  List<int> subseq = new List<int>();

  int l = 0, r = -1;

  for (int i = 0; i < M; i++)
  {
    // Check if element B[i]
    // is in array []A
    if (map.ContainsKey(B[i]))
    {
      int e = map[B[i]];

      // Perform Binary Search
      while (l <= r)
      {
        // Find the value of
        // mid m
        int m = l + (r - l) / 2;

        // Update l and r
        if (subseq[m] < e)
          l = m + 1;
        else
          r = m - 1;
      }

      // If found better element
      // 'e' for pos r + 1
      if (r + 1 < subseq.Count)
      {
        subseq[r + 1] = e;
      }

      // Otherwise, extend the
      // current subsequence
      else
      {
        subseq.Add(e);
      }

      l = 0;
      r = subseq.Count - 1;
    }
  }

  // Return the answer
  return N - subseq.Count;
}

// Driver Code
public static void Main(String[] args)
{
  // Given arrays
  int[] A = {1, 2, 3, 4, 5};
  int[] B = {2, 5, 6, 4, 9, 12};

  int M = A.Length;
  int N = B.Length;

  // Function Call
  Console.WriteLine(minElements(A, B,
                                M, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach

// Function to return minimum
// element to be added in array
// B so that array A become
// subsequence of array B
function minElements(A, B, N, M)
{
  // Stores indices of the
  // array elements
  var map = new Map();

  // Iterate over the array
  for (var i = 0; i < N; i++)
  {
    // Store the indices of
    // the array elements
    map.set(A[i], i);
  }

  // Stores the LIS
  var subseq = [];

  var l = 0, r = -1;

  for (var i = 0; i < M; i++)
  {
    // Check if element B[i]
    // is in array A[]
    if (map.has(B[i]))
    {
      var e = map.get(B[i]);

      // Perform Binary Search
      while (l <= r)
      {
        // Find the value of
        // mid m
        var m = l + parseInt((r - l) / 2);

        // Update l and r
        if (subseq[m] < e)
          l = m + 1;
        else
          r = m - 1;
      }

      // If found better element
      // 'e' for pos r + 1
      if (r + 1 < subseq.length)
      {
        subseq[r + 1] = e;
      }

      // Otherwise, extend the
      // current subsequence
      else
      {
        subseq.push(e);
      }

      l = 0;
      r = subseq.length - 1;
    }
  }

  // Return the answer
  return N - subseq.length;
}

// Driver code
// Given arrays
var A = [1, 2, 3, 4, 5];
var B = [2, 5, 6, 4, 9, 12];
var M = A.length;
var N = B.length;
// Function Call
document.write( minElements(A, B,
                    M, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N logN)*
***辅助空间:** O(N)*