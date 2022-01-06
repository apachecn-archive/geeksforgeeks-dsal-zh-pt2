# 使用循环旋转最大化给定排列中相应相同元素的计数

> 原文:[https://www . geeksforgeeks . org/最大化给定排列中对应的相同元素的数量-使用循环旋转/](https://www.geeksforgeeks.org/maximize-count-of-corresponding-same-elements-in-given-permutations-using-cyclic-rotations/)

给定从 **1 到 N** 的数字的两个排列 **P1** 和 **P2** ，任务是通过在 **P1** 上执行[循环左移或右移](https://www.geeksforgeeks.org/array-rotation/)来找到给定排列中对应的相同元素的最大计数。
**示例:**

> **输入:** P1 = [5 4 3 2 1]，P2 = [1 2 3 4 5]
> **输出:** 1
> **解释:**
> 元素 3 在索引 2 处有一个匹配对。
> **输入:** P1 = [1 3 5 2 4 6]，P2 = [1 5 2 4 3 6]
> **输出:** 3
> **解释:**
> 第二次置换向右循环移位会给出 6 1 5 2 4 3，我们得到 5，2，4 的匹配。因此，答案是 3 对匹配。

**天真方法:**天真方法是检查左右两个方向上的每一个可能的移位，通过循环所有形成的置换来计算匹配对的数量。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效进场:**以上幼稚进场可以优化。这个想法是让每个元素**在单独的数组中存储这个元素从左侧到右侧的位置之间的较小距离**。因此，问题的解决方案将被计算为来自两个分离阵列的元素的**最大频率**。以下是步骤:

1.  将排列 **P2** 的所有元素的位置存储在一个数组中(比如说**存储[]** )。
2.  对于排列 **P1** 中的每个元素，执行以下操作:
    *   找出当前元素在 **P2** 的位置与在 **P1** 的位置之间的差异(比如 **diff** )。
    *   如果差值小于 0，则将差值更新为**(N–差值)**。
    *   将电流差差的频率存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
3.  经过以上步骤，地图中存储的最大频率为 **P1** 上旋转后的最大等元数。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the matching
// pairs between two permutation
// using left and right rotation
int maximumMatchingPairs(int perm1[],
                         int perm2[],
                         int n)
{
    // Left array store distance of element
    // from left side and right array store
    // distance of element from right side
    int left[n], right[n];

    // Map to store index of elements
    map<int, int> mp1, mp2;
    for (int i = 0; i < n; i++) {
        mp1[perm1[i]] = i;
    }
    for (int j = 0; j < n; j++) {
        mp2[perm2[j]] = j;
    }

    for (int i = 0; i < n; i++) {

        // idx1 is index of element
        // in first permutation

        // idx2 is index of element
        // in second permutation
        int idx2 = mp2[perm1[i]];
        int idx1 = i;

        if (idx1 == idx2) {

            // If element if present on same
            // index on both permutations then
            // distance is zero
            left[i] = 0;
            right[i] = 0;
        }
        else if (idx1 < idx2) {

            // Calculate distance from left
            // and right side
            left[i] = (n - (idx2 - idx1));
            right[i] = (idx2 - idx1);
        }
        else {

            // Calculate distance from left
            // and right side
            left[i] = (idx1 - idx2);
            right[i] = (n - (idx1 - idx2));
        }
    }

    // Maps to store frequencies of elements
    // present in left and right arrays
    map<int, int> freq1, freq2;
    for (int i = 0; i < n; i++) {
        freq1[left[i]]++;
        freq2[right[i]]++;
    }

    int ans = 0;

    for (int i = 0; i < n; i++) {

        // Find maximum frequency
        ans = max(ans, max(freq1[left[i]],
                           freq2[right[i]]));
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    // Given permutations P1 and P2
    int P1[] = { 5, 4, 3, 2, 1 };
    int P2[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(P1) / sizeof(P1[0]);

    // Function Call
    cout << maximumMatchingPairs(P1, P2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to maximize the matching
// pairs between two permutation
// using left and right rotation
static int maximumMatchingPairs(int perm1[],
                                int perm2[],
                                int n)
{
  // Left array store distance of element
  // from left side and right array store
  // distance of element from right side
  int []left = new int[n];
  int []right = new int[n];

  // Map to store index of elements
  HashMap<Integer,
          Integer> mp1 =  new HashMap<>();
  HashMap<Integer,
          Integer> mp2 =  new HashMap<>();

  for (int i = 0; i < n; i++)
  {
    mp1.put(perm1[i], i);
  }
  for (int j = 0; j < n; j++)
  {
    mp2.put(perm2[j], j);
  }

  for (int i = 0; i < n; i++)
  {
    // idx1 is index of element
    // in first permutation
    // idx2 is index of element
    // in second permutation
    int idx2 = mp2.get(perm1[i]);
    int idx1 = i;

    if (idx1 == idx2)
    {
      // If element if present on same
      // index on both permutations then
      // distance is zero
      left[i] = 0;
      right[i] = 0;
    }
    else if (idx1 < idx2)
    {
      // Calculate distance from left
      // and right side
      left[i] = (n - (idx2 - idx1));
      right[i] = (idx2 - idx1);
    }
    else
    {
      // Calculate distance from left
      // and right side
      left[i] = (idx1 - idx2);
      right[i] = (n - (idx1 - idx2));
    }
  }

  // Maps to store frequencies of elements
  // present in left and right arrays
  HashMap<Integer,
          Integer> freq1 = new HashMap<>();
  HashMap<Integer,
          Integer> freq2 = new HashMap<>();

  for (int i = 0; i < n; i++)
  {
    if(freq1.containsKey(left[i]))
      freq1.put(left[i],
      freq1.get(left[i]) + 1);
    else
      freq1.put(left[i], 1);
    if(freq2.containsKey(right[i]))
      freq2.put(right[i],
      freq2.get(right[i]) + 1);
    else
      freq2.put(right[i], 1);
  }

  int ans = 0;

  for (int i = 0; i < n; i++)
  {
    // Find maximum frequency
    ans = Math.max(ans,
          Math.max(freq1.get(left[i]),
                   freq2.get(right[i])));
  }

  // Return the result
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  // Given permutations P1 and P2
  int P1[] = {5, 4, 3, 2, 1};
  int P2[] = {1, 2, 3, 4, 5};
  int n = P1.length;

  // Function Call
  System.out.print(maximumMatchingPairs(P1, P2, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to maximize the matching
# pairs between two permutation
# using left and right rotation
def maximumMatchingPairs(perm1, perm2, n):

    # Left array store distance of element
    # from left side and right array store
    # distance of element from right side
    left = [0] * n
    right = [0] * n

    # Map to store index of elements
    mp1 = {}
    mp2 = {}
    for i in range (n):
        mp1[perm1[i]] = i

    for j in range (n):
        mp2[perm2[j]] = j

    for i in range (n):

        # idx1 is index of element
        # in first permutation

        # idx2 is index of element
        # in second permutation
        idx2 = mp2[perm1[i]]
        idx1 = i

        if (idx1 == idx2):

            # If element if present on same
            # index on both permutations then
            # distance is zero
            left[i] = 0
            right[i] = 0

        elif (idx1 < idx2):

            # Calculate distance from left
            # and right side
            left[i] = (n - (idx2 - idx1))
            right[i] = (idx2 - idx1)

        else :

            # Calculate distance from left
            # and right side
            left[i] = (idx1 - idx2)
            right[i] = (n - (idx1 - idx2))

    # Maps to store frequencies of elements
    # present in left and right arrays
    freq1 = defaultdict (int)
    freq2 = defaultdict (int)
    for i in range (n):
        freq1[left[i]] += 1
        freq2[right[i]] += 1

    ans = 0

    for i in range( n):

        # Find maximum frequency
        ans = max(ans, max(freq1[left[i]],
                           freq2[right[i]]))

    # Return the result
    return ans

# Driver Code
if __name__ == "__main__":

    # Given permutations P1 and P2
    P1 = [ 5, 4, 3, 2, 1 ]
    P2 = [ 1, 2, 3, 4, 5 ]
    n = len(P1)

    # Function Call
    print(maximumMatchingPairs(P1, P2, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to maximize the matching
// pairs between two permutation
// using left and right rotation
static int maximumMatchingPairs(int []perm1,
                                int []perm2,
                                int n)
{
  // Left array store distance of element
  // from left side and right array store
  // distance of element from right side
  int []left = new int[n];
  int []right = new int[n];

  // Map to store index of elements
  Dictionary<int,
             int> mp1=new Dictionary<int,
                                     int>();
  Dictionary<int,
             int> mp2=new Dictionary<int,
                                     int>();

  for (int i = 0; i < n; i++)
  {
    mp1[perm1[i]] = i;
  }
  for (int j = 0; j < n; j++)
  {
    mp2[perm2[j]] = j;
  }

  for (int i = 0; i < n; i++)
  {
    // idx1 is index of element
    // in first permutation
    // idx2 is index of element
    // in second permutation
    int idx2 = mp2[perm1[i]];
    int idx1 = i;

    if (idx1 == idx2)
    {
      // If element if present on same
      // index on both permutations then
      // distance is zero
      left[i] = 0;
      right[i] = 0;
    }
    else if (idx1 < idx2)
    {
      // Calculate distance from left
      // and right side
      left[i] = (n - (idx2 - idx1));
      right[i] = (idx2 - idx1);
    }
    else
    {
      // Calculate distance from left
      // and right side
      left[i] = (idx1 - idx2);
      right[i] = (n - (idx1 - idx2));
    }
  }

  // Maps to store frequencies of elements
  // present in left and right arrays
  Dictionary<int,
             int> freq1=new Dictionary <int,
                                        int>();
  Dictionary<int,
             int> freq2=new Dictionary <int,
                                        int>();

  for (int i = 0; i < n; i++)
  {
    if(freq1.ContainsKey(left[i]))
      freq1[left[i]]++;
    else
      freq1[left[i]] = 1;

    if(freq2.ContainsKey(right[i]))
      freq2[right[i]]++;
    else
      freq2[right[i]] = 1;
  }

  int ans = 0;

  for (int i = 0; i < n; i++)
  {
    // Find maximum frequency
    ans = Math.Max(ans,
          Math.Max(freq1[left[i]],
                   freq2[right[i]]));
  }

  // Return the result
  return ans;
}

// Driver Code
public static void Main(string[] args)
{
  // Given permutations P1 and P2
  int []P1 = {5, 4, 3, 2, 1};
  int []P2 = {1, 2, 3, 4, 5};
  int n = P1.Length;

  // Function Call
  Console.Write(maximumMatchingPairs(P1, P2, n));
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to maximize the matching
// pairs between two permutation
// using left and right rotation
function maximumMatchingPairs(perm1, perm2, n)
{
    // Left array store distance of element
    // from left side and right array store
    // distance of element from right side
    var left = Array(n);
    var right = Array(n);

    // Map to store index of elements
    var mp1 = new Map(), mp2 = new Map();
    for (var i = 0; i < n; i++) {
        mp1.set(perm1[i], i);
    }
    for (var j = 0; j < n; j++) {
        mp2.set(perm2[j], j);
    }

    for (var i = 0; i < n; i++) {

        // idx1 is index of element
        // in first permutation

        // idx2 is index of element
        // in second permutation
        var idx2 = mp2.get(perm1[i]);
        var idx1 = i;

        if (idx1 == idx2) {

            // If element if present on same
            // index on both permutations then
            // distance is zero
            left[i] = 0;
            right[i] = 0;
        }
        else if (idx1 < idx2) {

            // Calculate distance from left
            // and right side
            left[i] = (n - (idx2 - idx1));
            right[i] = (idx2 - idx1);
        }
        else {

            // Calculate distance from left
            // and right side
            left[i] = (idx1 - idx2);
            right[i] = (n - (idx1 - idx2));
        }
    }

    // Maps to store frequencies of elements
    // present in left and right arrays
    var freq1 = new Map(), freq2 = new Map();
    for (var i = 0; i < n; i++) {
        if(freq1.has(left[i]))
            freq1.set(left[i], freq1.get(left[i])+1)
        else
            freq1.set(left[i], 1)

        if(freq2.has(right[i]))
            freq2.set(right[i], freq2.get(right[i])+1)
        else
            freq2.set(right[i], 1)
    }

    var ans = 0;

    for (var i = 0; i < n; i++) {

        // Find maximum frequency
        ans = Math.max(ans, Math.max(freq1.get(left[i]),
                           freq2.get(right[i])));
    }

    // Return the result
    return ans;
}

// Driver Code
// Given permutations P1 and P2
var P1 = [5, 4, 3, 2, 1];
var P2 = [1, 2, 3, 4, 5];
var n = P1.length;
// Function Call
document.write( maximumMatchingPairs(P1, P2, n));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)