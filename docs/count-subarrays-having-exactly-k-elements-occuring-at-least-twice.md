# 计算至少出现两次的精确 K 元素的子阵列

> 原文:[https://www . geeksforgeeks . org/count-subarray-具有-恰好-k-元素-出现-至少-两次/](https://www.geeksforgeeks.org/count-subarrays-having-exactly-k-elements-occuring-at-least-twice/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是计算至少两次**出现精确 **K** 个元素的子数组数量**。

**示例:**

> **输入:** arr[] = {1，1，1，2，2}，K = 1
> **输出:** 7
> **解释:**至少出现两次恰好一个元素的子阵是:
> 
> 1.  {1, 1}.1 的频率是 2。
> 2.  {1, 1, 1}.1 的频率是 3。
> 3.  {1, 1, 1, 2}.1 的频率是 3。
> 4.  {1, 1}.1 的频率是 2。
> 5.  {1, 1, 2}.1 的频率是 2。
> 6.  {1, 2, 2}.2 的频率是 2。
> 7.  {2, 2}.2 的频率是 2。
> 
> 因此，所需的输出为 7。
> 
> **输入:** arr[] = {1，2，1，2，3}，K = 3
> 
> **输出:** 0

**天真方法:**解决这个问题最简单的方法是 [<u>从给定的数组</u>](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/) 中生成所有可能的子数组，并对那些至少出现两次**的子数组进行计数。检查完所有[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)后，打印获得的子阵列总数。**

*****时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)***

****高效方法:**上述方法可以通过使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)和[两个指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)进行优化。按照以下步骤解决问题:**

*   **初始化一个变量，比如说 **cntSub** 为 **0** ，以存储所有可能的子阵列的计数，这些子阵列具有至少出现两次**的 **K 元素**。****
*   ****初始化两个变量，说 **l** 为 **0** ，说 **r** 为 **0** ，分别存储每个子阵列左右边界的索引。****
*   ****初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，说 **mp** ，一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，说 **S** 分别存储子阵中的元素个数和子阵中频率至少为 **2** 的元素。****
*   ****迭代直到 **r** 小于 **N** 并执行以下操作:

    *   当 **r** 小于 **N** 且集合的[大小最多为**K**时迭代:](https://www.geeksforgeeks.org/setsize-c-stl/)
        *   增加 **mp** 中**arr【r】**的计数，如果**MP【arr【r】**等于 **2** ，则[将元素推入设置](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)T6】S。
        *   将 **r** 增加 **1** 。
        *   如果设置的 **S** 的大小是 **K** ，那么将 **cntSub** 增加 **1** 。
    *   当 **l < r** 且集合的[大小大于 **K** 时迭代:](https://www.geeksforgeeks.org/setsize-c-stl/)
        *   如果 **mp[arr[r]]** 等于 **1** ，则递减 **mp** 中 **arr[l]** 的计数，然后[从 set](https://www.geeksforgeeks.org/seterase-c-stl/) **S** 中擦除该元素。
        *   将 **cntSub** 和 **l** 增加 **1** 。**** 
*   ****现在在 **l < N** 和[的同时迭代，集合](https://www.geeksforgeeks.org/setsize-c-stl/)的大小为 **K** ，将**arr【l】**的计数减少 **1** ，如果**arr【l】**的频率为 **1** ，则从集合中删除**arr【l】**。****
*   ****完成上述步骤后，打印 **cntSub** 的值作为子阵列的结果计数。****

****下面是上述方法的实现:****

## ****C++14****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the subarrays with
// exactly K elements occurring twice
int cntSubarrays(int A[], int K, int n)
{
    // Stores the count of subarrays
    // having exactly K elements
    // occurring at least twice
    int cntSub = 0;

    // Stores the count of
    // integers in the subarray
    map<int, int> mp;

    // Stores the indices of left
    // boundary and right boundary
    int l = 0, r = 0;

    // Store the elements which occurs
    // atleast twice between [l, r]
    set<int> st;

    // Iterate while r < n
    while (r < n) {

        // Iterate while r < n
        // and size of st <= K
        while (r < n && st.size() <= K) {

            // If mp[A[r]] >= 1
            if (mp[A[r]]) {
                st.insert(A[r]);
            }

            // Increment count of A[r]
            mp[A[r]]++;

            // Increment r by 1
            r++;

            // If st.size() is K
            if (st.size() == K)
                cntSub++;
        }

        // Iterate while l < r
        // and st.size() > K
        while (l < r && st.size() > K) {

            // Increment cntSub by 1
            cntSub++;

            // Decrement cntSub by 1
            mp[A[l]]--;

            // If mp[A[l]] = 1
            if (mp[A[l]] == 1) {
                st.erase(st.find(A[l]));
            }

            // Increment l by 1
            l++;
        }
    }

    // Iterate while l < n  and
    // st.size() == K
    while (l < n && st.size() == K) {

        // Increment cntSub by 1
        cntSub++;

        mp[A[l]]--;

        // If Mp[A[l]] is equal to 1
        if (mp[A[l]] == 1) {
            st.erase(st.find(A[l]));
        }

        // Increment l by 1
        l++;
    }

    // Return cntSub
    return cntSub;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 1, 2, 2 };
    int K = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << cntSubarrays(arr, K, N);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;
class GFG {

  // Function to count the subarrays with
  // exactly K elements occurring twice
  static int cntSubarrays(int[] A, int K, int n)
  {

    // Stores the count of subarrays
    // having exactly K elements
    // occurring at least twice
    int cntSub = 0;

    // Stores the count of
    // integers in the subarray
    HashMap<Integer, Integer> mp
      = new HashMap<Integer, Integer>();

    // Stores the indices of left
    // boundary and right boundary
    int l = 0, r = 0;

    // Store the elements which occurs
    // atleast twice between [l, r]
    HashSet<Integer> st = new HashSet<Integer>();

    // Iterate while r < n
    while (r < n) {

      // Iterate while r < n
      // and size of st <= K
      while (r < n && st.size() <= K) {

        // If mp[A[r]] >= 1
        if (mp.containsKey(A[r])) {
          st.add(A[r]);
        }

        // Increment count of A[r]
        if (mp.containsKey(A[r]))
          mp.put(A[r], mp.get(A[r]) + 1);
        else
          mp.put(A[r], 1);

        // Increment r by 1
        r++;

        // If st.size() is K
        if (st.size() == K)
          cntSub++;
      }

      // Iterate while l < r
      // and st.size() > K
      while (l < r && st.size() > K) {

        // Increment cntSub by 1
        cntSub++;

        // Decrement cntSub by 1
        if (mp.containsKey(A[l]))
          mp.put(A[l], mp.get(A[l]) - 1);

        // If mp[A[l]] = 1
        if (mp.get(A[l]) == 1) {
          st.remove(A[l]);
        }

        // Increment l by 1
        l++;
      }
    }

    // Iterate while l < n  and
    // st.size() == K
    while (l < n && st.size() == K) {

      // Increment cntSub by 1
      cntSub++;
      if (mp.containsKey(A[l]))
        mp.put(A[l], mp.get(A[l]) - 1);

      // If Mp[A[l]] is equal to 1
      if (mp.get(A[l]) == 1) {
        st.remove(A[l]);
      }

      // Increment l by 1
      l++;
    }

    // Return cntSub
    return cntSub;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 1, 1, 1, 2, 2 };
    int K = 1;
    int N = arr.length;

    System.out.println(cntSubarrays(arr, K, N));
  }
}

// This code is contributed by ukasp.**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to count the subarrays with
# exactly K elements occurring twice
def cntSubarrays(A, K, n):

    # Stores the count of subarrays
    # having exactly K elements
    # occurring at least twice
    cntSub = 0

    # Stores the count of
    # integers in the subarray
    mp = {}

    # Stores the indices of left
    # boundary and right boundary
    l = 0
    r = 0

    # Store the elements which occurs
    # atleast twice between [l, r]
    st = set()

    # Iterate while r < n
    while (r < n):

        # Iterate while r < n
        # and size of st <= K
        while (r < n and len(st) <= K):

            # If mp[A[r]] >= 1
            if (A[r] in mp):
                st.add(A[r])

            # Increment count of A[r]
            if (A[r] in mp):
                mp[A[r]] += 1
            else:
                mp[A[r]] = 1

            # Increment r by 1
            r += 1

            # If st.size() is K
            if (len(st) == K):
                cntSub += 1

        # Iterate while l < r
        # and st.size() > K
        while (l < r and len(st) > K):

            # Increment cntSub by 1
            cntSub += 1

            # Decrement cntSub by 1
            if (A[l] in mp):
                mp[A[l]] -= 1
            else:
                mp[A[l]] = 1

            # If mp[A[l]] = 1
            if (mp[A[l]] == 1):
                st.remove(A[l])

            # Increment l by 1
            l += 1

    # Iterate while l < n  and
    # st.size() == K
    while (l < n and len(st) == K):

        # Increment cntSub by 1
        cntSub += 1

        mp[A[l]] -= 1

        # If Mp[A[l]] is equal to 1
        if (mp[A[l]] == 1):
            st.remove(A[l])

        # Increment l by 1
        l += 1

    # Return cntSub
    return cntSub

# Driver Code
if __name__ == '__main__':

    arr =  [1, 1, 1, 2, 2]
    K = 1
    N = len(arr)

    print(cntSubarrays(arr, K, N))

# This code is contributed by ipg2016107**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to count the subarrays with
  // exactly K elements occurring twice
  static int cntSubarrays(int []A, int K, int n)
  {

    // Stores the count of subarrays
    // having exactly K elements
    // occurring at least twice
    int cntSub = 0;

    // Stores the count of
    // integers in the subarray
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Stores the indices of left
    // boundary and right boundary
    int l = 0, r = 0;

    // Store the elements which occurs
    // atleast twice between [l, r]
    HashSet<int> st = new HashSet<int>();

    // Iterate while r < n
    while (r < n) {

      // Iterate while r < n
      // and size of st <= K
      while (r < n && st.Count <= K) {

        // If mp[A[r]] >= 1
        if (mp.ContainsKey(A[r])) {
          st.Add(A[r]);
        }

        // Increment count of A[r]
        if (mp.ContainsKey(A[r]))
          mp[A[r]]++;
        else
          mp[A[r]] = 1;

        // Increment r by 1
        r++;

        // If st.size() is K
        if (st.Count == K)
          cntSub++;
      }

      // Iterate while l < r
      // and st.size() > K
      while (l < r && st.Count > K) {

        // Increment cntSub by 1
        cntSub++;

        // Decrement cntSub by 1
        if (mp.ContainsKey(A[l]))
          mp[A[l]]--;

        // If mp[A[l]] = 1
        if (mp[A[l]] == 1) {
          st.Remove(A[l]);
        }

        // Increment l by 1
        l++;
      }
    }

    // Iterate while l < n  and
    // st.size() == K
    while (l < n && st.Count == K) {

      // Increment cntSub by 1
      cntSub++;
      if (mp.ContainsKey(A[l]))
        mp[A[l]]--;

      // If Mp[A[l]] is equal to 1
      if (mp[A[l]] == 1) {
        st.Remove(A[l]);
      }

      // Increment l by 1
      l++;
    }

    // Return cntSub
    return cntSub;
  }

  // Driver Code
  public static void Main()
  {
    int []arr = { 1, 1, 1, 2, 2 };
    int K = 1;
    int N = arr.Length;

    Console.WriteLine(cntSubarrays(arr, K, N));
  }
}

// This code is contributed by ipg2016107.**
```

## ****java 描述语言****

```
**<script>

// JavaScript program for the above approach

// Function to count the subarrays with
// exactly K elements occurring twice
function cntSubarrays(A,K,n)
{
    // Stores the count of subarrays
    // having exactly K elements
    // occurring at least twice
    let cntSub = 0;

    // Stores the count of
    // integers in the subarray
    let mp = new Map();

    // Stores the indices of left
    // boundary and right boundary
    let l = 0, r = 0;

    // Store the elements which occurs
    // atleast twice between [l, r]
    let st = new Set();

    // Iterate while r < n
    while (r < n) {

      // Iterate while r < n
      // and size of st <= K
      while (r < n && st.size <= K) {

        // If mp[A[r]] >= 1
        if (mp.has(A[r])) {
          st.add(A[r]);
        }

        // Increment count of A[r]
        if (mp.has(A[r]))
          mp.set(A[r], mp.get(A[r]) + 1);
        else
          mp.set(A[r], 1);

        // Increment r by 1
        r++;

        // If st.size() is K
        if (st.size == K)
          cntSub++;
      }

      // Iterate while l < r
      // and st.size() > K
      while (l < r && st.size > K) {

        // Increment cntSub by 1
        cntSub++;

        // Decrement cntSub by 1
        if (mp.has(A[l]))
          mp.set(A[l], mp.get(A[l]) - 1);

        // If mp[A[l]] = 1
        if (mp.get(A[l]) == 1) {
          st.delete(A[l]);
        }

        // Increment l by 1
        l++;
      }
    }

    // Iterate while l < n  and
    // st.size() == K
    while (l < n && st.size == K) {

      // Increment cntSub by 1
      cntSub++;
      if (mp.has(A[l]))
        mp.set(A[l], mp.get(A[l]) - 1);

      // If Mp[A[l]] is equal to 1
      if (mp.get(A[l]) == 1) {
        st.delete(A[l]);
      }

      // Increment l by 1
      l++;
    }

    // Return cntSub
    return cntSub;
}

 // Driver Code
let arr=[1, 1, 1, 2, 2 ];
let K = 1;
let N = arr.length;
document.write(cntSubarrays(arr, K, N));

// This code is contributed by avanitrachhadiya2155

</script>**
```

******Output:** 

```
7
```**** 

*******时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*****