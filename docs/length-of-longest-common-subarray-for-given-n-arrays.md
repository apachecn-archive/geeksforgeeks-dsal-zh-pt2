# 给定 N 个阵列的最长公共子阵列的长度

> 原文:[https://www . geeksforgeeks . org/给定 n 阵列的最长公共子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-common-subarray-for-given-n-arrays/)

给定包含 **N** 阵列的二维阵列**阵列[][]** ，任务是在 **N** 阵列中找到最长的普通[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) (LCS)。

**示例:**

> **输入** : N = 3，
> 数组[][] = { { 0，1，2，3，4 }，
> { 2，3，4 }，
> { 4，0，1，2，3 } }
> **输出** : 2
> **解释**:最长的普通子路径是{ 2，3 }。
> 
> **输入** : N = 2，
> 数组[][] = {{0，1，2，3，4}，
> {4，3，2，1，0}}
> **输出** : 1
> **解释**:可能最长的常用子路径有【0】、【1】、【2】、【3】和【4】。都有 1 的长度。

**进场:**很明显 LCS 的长度可以是[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。也就是说，如果有一个长度为 **L** 的公共子阵列，总会有一个长度小于 **L** 的公共子阵列。因此，二分搜索法框架如下:

> lower = 0，upper = max length+1；// LCS 在[下，上]。
> 而(下+ 1 <上){
> 中=(下+上)/2；
> if(有一些长度中间的常见子串){
> lower = middle；
> else {
> upper = middle；
> }
> }
> LCS =更低；

所以，这里的重点是检查是否有一些长度居中的常见子数组。通常的方法是采用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)，即[拉宾卡普哈希](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)。

> **哈希(S[0..n-1])=(s[n-1]* magic^0+s[n-2]* magic^1+..+ S[n-1-i] * MAGIC^i + … ) % MOD**

这里最方便的一点是 **Hash(S[0…i])** 可以用来计算 **O(1)** 时间内的 **Hash(S[l…r])** ，有 **O(N)** 准备。也就是说，

> **哈希(S[l..r]) =(哈希(S[0..r])–哈希(S[0..l-1]) * MAGIC^(r-l+1)) % MOD**

因此，可以找到两个给定数组中长度中间的子数组的所有哈希值，然后检查是否有重叠。这个过程可以通过 O(|S|)中的[散列表](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)或者 O(|S|log|S|)中的[设置](https://www.geeksforgeeks.org/multiset-in-cpp-stl/) ( [平衡二叉查找树](https://www.geeksforgeeks.org/convert-normal-bst-balanced-bst/))来完成。因此，二分搜索法+哈希可以在 O(|S| log|S|)时间内解决这个问题。按照以下步骤解决此问题:

*   将变量 **min_len** 初始化为最大可能长度，即 **INT_MAX** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   将 **min_len** 的值设置为 **min_len** 或**数组【I】的最小值。大小()。**
*   初始化变量**开始**为 **0，结束**为 **min_len** ，中间**为 **0** ，执行长度二分搜索法。**
*   [遍历 while 循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**开始**小于等于**结束**，并执行以下步骤:
    *   将**中间**的值设置为**开始**和**结束的平均值。**
    *   调用[功能](https://www.geeksforgeeks.org/functions-in-c/) **检查(数组，中间)**检查长度**中间**是否可以作为答案，或者不使用[拉宾-卡普哈希](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)。
    *   如果函数返回**为真，**则将**开始**的值设置为**中间+1** ，否则**结束**为**中间-1。**
*   执行上述步骤后，打印**结束**的值作为答案。

下面是上述方法的实现

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const long long p = 1299827;
const long long mod = 1e11 + 7;
long long M;

// Function to implement rabin - carp
// hashing to check whether the given length
// is possible or not
bool check(vector<vector<int> >& array, int len)
{
    if (len == 0)
        return true;
    map<long long, int> freq;
    for (int i = 0; i < M; i++) {
        long long curr_hash = 0, pow = 1;
        set<long long> found_hashes;
        for (int j = 0; j < len; j++) {
            curr_hash = (curr_hash * p) % mod;
            curr_hash += array[i][j];
            if (j != len - 1)
                pow = (pow * p) % mod;
        }
        found_hashes.insert(curr_hash);
        for (int j = len; j < array[i].size(); j++) {
            curr_hash += mod;
            curr_hash -= (array[i][j - len] * pow) % mod;
            curr_hash %= mod;
            curr_hash = curr_hash * p;
            curr_hash %= mod;
            curr_hash += array[i][j];
            curr_hash %= mod;
            found_hashes.insert(curr_hash);
        }
        while (found_hashes.size()) {
            long long h = *(found_hashes.begin());
            found_hashes.erase(found_hashes.begin());
            freq[h]++;
            if (freq[h] == M)
                return true;
        }
    }
    return false;
}

// Function to find the longest common sub-array
// from the given N arrays
int longestCommonSubpath(long long N,
                         vector<vector<int> >& array)
{

    M = N;

    // Find the maximum length possible
    int minlen = INT_MAX;
    for (int i = 0; i < array.size(); i++) {
        minlen = min(minlen, (int)array[i].size());
    }

    // Binary search on the length
    int start = 0, end = minlen, mid = 0;
    while (start <= end) {
        int mid = (start + end) / 2;

        // Function Call to check whether
        // it is possible or not
        if (check(array, mid)) {
            start = mid + 1;
        }
        else {
            end = mid - 1;
        }
    }
    return end;
}

// Driver Code
int main()
{
    vector<vector<int> > arr{ { 0, 1, 2, 3, 4 },
                              { 2, 3, 4 },
                              { 4, 0, 1, 2, 3 } };

    long long N = arr.size();

    cout << longestCommonSubpath(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
import java.util.HashSet;

class GFG {

  static long p = 1299827;
  static long mod = (long) 1E11 + 7;
  static long M;

  // Function to implement rabin - carp
  // hashing to check whether the given length
  // is possible or not
  static boolean check(int[][] array, int len) {
    if (len == 0)
      return true;
    HashMap<Long, Integer> freq = new HashMap<Long, Integer>();
    for (int i = 0; i < M; i++) {
      long curr_hash = 0, pow = 1;
      HashSet<Long> found_hashes = new HashSet<Long>();
      for (int j = 0; j < len; j++) {
        curr_hash = (curr_hash * p) % mod;
        curr_hash += array[i][j];
        if (j != len - 1)
          pow = (pow * p) % mod;
      }
      found_hashes.add(curr_hash);
      for (int j = len; j < array[i].length; j++) {
        curr_hash += mod;
        curr_hash -= (array[i][j - len] * pow) % mod;
        curr_hash %= mod;
        curr_hash = curr_hash * p;
        curr_hash %= mod;
        curr_hash += array[i][j];
        curr_hash %= mod;
        found_hashes.add(curr_hash);
      }
      while (found_hashes.size() > 0) {
        long h = found_hashes.iterator().next();
        found_hashes.remove(h);
        if (freq.containsKey(h)) {
          freq.put(h, freq.get(h) + 1);
        } else {
          freq.put(h, 1);
        }
        if (freq.get(h) == M)
          return true;
      }
    }
    return false;
  }

  // Function to find the longest common sub-array
  // from the given N arrays
  public static int longestCommonSubpath(long N, int[][] array) {

    M = N;

    // Find the maximum length possible
    int minlen = Integer.MAX_VALUE;
    for (int i = 0; i < array.length; i++) {
      minlen = Math.min(minlen, (int) array[i].length);
    }

    // Binary search on the length
    int start = 0, end = minlen, mid = 0;
    while (start <= end) {
      mid = (start + end) / 2;

      // Function Call to check whether
      // it is possible or not
      if (check(array, mid)) {
        start = mid + 1;
      } else {
        end = mid - 1;
      }
    }
    return end;
  }

  // Driver Code
  public static void main(String args[]) {
    int[][] arr = { { 0, 1, 2, 3, 4 }, { 2, 3, 4 }, { 4, 0, 1, 2, 3 } };

    long N = arr.length;

    System.out.println(longestCommonSubpath(N, arr));
  }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
p = 1299827
mod = 1e11 + 7
M = None

# Function to implement rabin - carp
# hashing to check whether the given length
# is possible or not
def check(array, _len, M):
    if (_len == 0):
        return True
    freq = {}

    for i in range(M):
        curr_hash = 0
        pow = 1
        found_hashes = set()
        for j in range(_len):
            curr_hash = (curr_hash * p) % mod
            curr_hash = curr_hash + array[i][j]
            if (j != _len - 1):
                pow = (pow * p) % mod

        found_hashes.add(curr_hash)
        for j in range(_len, len(array[i])):
            curr_hash = curr_hash + mod
            curr_hash = curr_hash - (array[i][j - _len] * pow) % mod
            curr_hash = curr_hash % mod
            curr_hash = curr_hash * p
            curr_hash = curr_hash % mod
            curr_hash = curr_hash + array[i][j]
            curr_hash = curr_hash % mod
            found_hashes.add(curr_hash)
        while (len(found_hashes) != 0):
            it = list(found_hashes)

            # get first entry:
            h = it[0]
            found_hashes.remove(h)

            if (h not in freq):
                freq[h] = 1
            else:
                freq[h] += 1

            if (h in freq and freq[h] == M):
                return True
    return False

# Function to find the longest common sub-array
# from the given N arrays
def longestCommonSubpath(N, array):
    M = N

    # Find the maximum length possible
    minlen = 10 ** 9
    for i in range(len(array)):
        minlen = min(minlen, len(array[i]))

    # Binary search on the length
    start = 0
    end = minlen
    mid = 0
    while (start <= end):
        mid = (start + end) // 2

        # Function Call to check whether
        # it is possible or not
        if (check(array, mid, M)):
            start = mid + 1
        else:
            end = mid - 1
    return end

# Driver Code
arr = [[0, 1, 2, 3, 4], [2, 3, 4], [4, 0, 1, 2, 3]]

N = len(arr)
print(longestCommonSubpath(N, arr))

# This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach
      let p = 1299827;
      let mod = 1e11 + 7;
      var M;

      // Function to implement rabin - carp
      // hashing to check whether the given length
      // is possible or not
      function check(array, len, M) {
          if (len == 0)
              return true;
          let freq = new Map();

          for (let i = 0; i < M; i++) {
              let curr_hash = 0, pow = 1;
              let found_hashes = new Set();
              for (let j = 0; j < len; j++) {
                  curr_hash = (curr_hash * p) % mod;
                  curr_hash = curr_hash + array[i][j];
                  if (j != len - 1)
                      pow = (pow * p) % mod;
              }
              found_hashes.add(curr_hash);
              for (let j = len; j < array[i].length; j++) {
                  curr_hash = curr_hash + mod;
                  curr_hash = curr_hash - (array[i][j - len] * pow) % mod;
                  curr_hash = curr_hash % mod;
                  curr_hash = curr_hash * p;
                  curr_hash = curr_hash % mod;
                  curr_hash = curr_hash + array[i][j];
                  curr_hash = curr_hash % mod;
                  found_hashes.add(curr_hash);
              }

              while (found_hashes.size != 0)
              {
                  var it = found_hashes.values();

                  // get first entry:
                  var first = it.next();

                  // get value out of the iterator entry:
                  var h = first.value;

                  found_hashes.delete(h);

                  if (freq.has(h) == false) {
                      freq.set(h, 1)
                  }
                  else {
                      freq.set(h, freq.get(h) + 1)
                  }

                  if (freq.has(h) && freq.get(h) == M)
                      return true;
              }
          }
          return false;
      }

      // Function to find the longest common sub-array
      // from the given N arrays
      function longestCommonSubpath(N,
          array) {

          M = N;

          // Find the maximum length possible
          let minlen = Number.MAX_SAFE_INTEGER;
          for (let i = 0; i < array.length; i++) {
              minlen = Math.min(minlen, array[i].length);
          }

          // Binary search on the length
          let start = 0, end = minlen, mid = 0;
          while (start <= end) {
              let mid = Math.floor((start + end) / 2);

              // Function Call to check whether
              // it is possible or not
              if (check(array, mid, M)) {
                  start = mid + 1;
              }
              else {
                  end = mid - 1;
              }
          }
          return end;
      }

      // Driver Code
      let arr = [[0, 1, 2, 3, 4],
      [2, 3, 4],
      [4, 0, 1, 2, 3]];

      let N = arr.length;

      document.write(longestCommonSubpath(N, arr));

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*