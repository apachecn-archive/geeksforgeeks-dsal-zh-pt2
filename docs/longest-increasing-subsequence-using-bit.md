# 使用位的最长递增子序列

> 原文:[https://www . geesforgeks . org/最长递增子序列使用位/](https://www.geeksforgeeks.org/longest-increasing-subsequence-using-bit/)

给定一个数组 **arr** ，任务是使用[二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) (BIT)找到最长递增序列的长度

**例:**

```
Input: arr = {6, 5, 1, 3, 2, 4, 8, 7}
Output: 4
Explanantion:
The possible subsequences are 
{1 2 4 7}, {1 2 4 8}, 
{1 3 4 8}, {1 3 4 7}  

Now insert the elements one by one from left to right:

6 is inserted: max length till 5 = 0, ans for 6 is 1
5 is inserted: max length till 4 = 0, ans for 5 is 1
1 is inserted: max length till 0 = 2, ans for 1 is 1
3 is inserted: max length till 2 = 1, ans for 3 is 2
2 is inserted: max length till 1 = 1, ans for 2 is 2
4 is inserted: max length till 3 = 2, ans for 4 is 3
8 is inserted: max length till 7 = 3, ans for 8 is 4
7 is inserted: max length till 6 = 3, ans for 7 is 4

Input: arr = {1, 2, 3, 4, 1, 5}
Output: 5
```

这篇文章的先决条件:[二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)

**进场:**

*   首先，使用坐标压缩(将数组的所有值替换为从 1 到 N 的数字)。这将减少数组中的最大数量，并帮助我们在 NlogN 时间内解决上述问题。还有，这将有助于我们减少记忆。
*   制作一个长度为 N + 1 的新数组 BIT。
*   现在，从左到右遍历数组，并将当前元素添加到位中。
*   当第一个元素(A[i])插入到位中时，检查可以形成的最长子序列的长度，直到 A[I]–1。设此值为 x。如果 x + 1 大于 BIT 中的当前元素，则更新 BIT。

下面是上述方法的实现:

## c++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to map
// numbers using coordinate
// compression
void coordinateCompression(int arr[], int n)
{

    // Set will store
    // all unique numbers
    set<int> s;
    for (int i = 0; i < n; i++) {
        s.insert(arr[i]);
    }

    // Map will store
    // the new elements
    int index = 0;
    map<int, int> mp;
    set<int>::iterator itr;

    for (itr = s.begin(); itr != s.end(); itr++) {
        // For every new number in the set,
        index++;
        // Increment the index of the
        // current number and store it
        // in a hashmap. Here index
        // for every element is the
        // new value with with the
        // current element is replaced
        mp[*itr] = index;
    }
    for (int i = 0; i < n; i++) {
        // now change the current element
        // to range 1 to N.
        arr[i] = mp[arr[i]];
    }
}

// Function to calculate
// length of maximum
// increasing sequence till
// i'th index
int query(int BIT[], int index, int n)
{

    int ans = 0;
    while (index > 0) {
        ans = max(ans, BIT[index]);
        // Go to parent node
        index -= index & (-index);
    }
    return ans;
}

// Function for updating
// BIT array for maximum
// increasing sequence till
// i'th index
void update(int BIT[], int index, int n)
{

    // If 4 is inserted in BIT,
    // check for maximum length
    // subsequence till element 3.
    // Let this subsequence length be x.
    // If x + 1 is greater than
    // the current element in BIT,
    // update the BIT array
    int x = query(BIT, index - 1, n);
    int value = x + 1;
    while (index <= n) {

        // Store maximum length subsequence length till index
        // Here index is the
        // coordinate compressed element
        BIT[index] = max(BIT[index], value);

        // Go to child node and update that node
        index += index & (-index);
    }
}

// Function to calculate
// maximum Longest Increasing
// Sequence length
int findLISLength(int arr[], int n)
{

    coordinateCompression(arr, n);
    int BIT[n + 1];

    // Initialising BIT array
    for (int i = 0; i <= n; i++) {
        BIT[i] = 0;
    }

    for (int i = 0; i < n; i++) {
        // Add elements
        // from left to right
        // in BIT
        update(BIT, arr[i], n);
    }

    int ans = query(BIT, n, n);
    return ans;
}

// Driver code
int main()
{

    int arr[] = { 6, 5, 1, 3, 2, 4, 8, 7 };
    int n = sizeof(arr) / sizeof(int);
    int ans = findLISLength(arr, n);

    cout << ans << endl;

    return 0;
}
```

## Java

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to map numbers using
// coordinate compression
static void coordinateCompression(int arr[],
                                  int n)
{

    // Set will store
    // all unique numbers
    Set<Integer> s = new HashSet<>();
    for (int i = 0; i < n; i++)
    {
        s.add(arr[i]);
    }

    // Map will store
    // the new elements
    int index = 0;
    HashMap<Integer, Integer> mp =
         new HashMap<Integer, Integer>();

    for (int itr : s)
    {
        // For every new number in the set,
        index++;

        // Increment the index of the
        // current number and store it
        // in a hashmap. Here index
        // for every element is the
        // new value with with the
        // current element is replaced
        mp.put(itr, index);
    }
    for (int i = 0; i < n; i++)
    {
        // now change the current element
        // to range 1 to N.
        arr[i] = mp.get(arr[i]);
    }
}

// Function to calculate length of maximum
// increasing sequence till i'th index
static int query(int BIT[], int index, int n)
{
    int ans = 0;
    while (index > 0)
    {
        ans = Math.max(ans, BIT[index]);

        // Go to parent node
        index -= index & (-index);
    }
    return ans;
}

// Function for updating BIT array for
// maximum increasing sequence till
// i'th index
static void update(int BIT[],
                   int index, int n)
{

    // If 4 is inserted in BIT,
    // check for maximum length
    // subsequence till element 3.
    // Let this subsequence length be x.
    // If x + 1 is greater than
    // the current element in BIT,
    // update the BIT array
    int x = query(BIT, index - 1, n);
    int value = x + 1;
    while (index <= n)
    {

        // Store maximum length subsequence length
        // till index. Here index is the
        // coordinate compressed element
        BIT[index] = Math.max(BIT[index], value);

        // Go to child node and update that node
        index += index & (-index);
    }
}

// Function to calculate maximum
// Longest Increasing Sequence length
static int findLISLength(int arr[], int n)
{

    coordinateCompression(arr, n);
    int []BIT = new int[n + 1];

    // Initialising BIT array
    for (int i = 0; i <= n; i++)
    {
        BIT[i] = 0;
    }

    for (int i = 0; i < n; i++)
    {
        // Add elements from left to right
        // in BIT
        update(BIT, arr[i], n);
    }

    int ans = query(BIT, n, n);
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 5, 1, 3, 2, 4, 8, 7 };
    int n = arr.length;
    int ans = findLISLength(arr, n);

    System.out.println(ans);
}
}

// This code is contributed by Rajput-Ji
```

## python 3

```
# Python3 program for the above approach

# Function to map
# numbers using coordinate
# compression
def coordinateCompression(arr, n):

    # Set will store
    # all unique numbers
    s = dict()
    for i in range(n):
        s[arr[i]] = 1

    # Map will store
    # the new elements
    index = 0
    mp = dict()

    for itr in sorted(s):

        # For every new number in the set,
        index += 1

        # Increment the index of the
        # current number and store it
        # in a hashmap. Here index
        # for every element is the
        # new value with with the
        # current element is replaced
        mp[itr] = index
    for i in range(n):

        # now change the current element
        # to range 1 to N.
        arr[i] = mp[arr[i]]

# Function to calculate
# length of maximum
# increasing sequence till
# i'th index
def query(BIT, index, n):

    ans = 0
    while (index > 0):
        ans = max(ans, BIT[index])

        # Go to parent node
        index -= index & (-index)
    return ans

# Function for updating
# BIT array for maximum
# increasing sequence till
# i'th index
def update(BIT, index, n):

    # If 4 is inserted in BIT,
    # check for maximum length
    # subsequence till element 3.
    # Let this subsequence length be x.
    # If x + 1 is greater than
    # the current element in BIT,
    # update the BIT array
    x = query(BIT, index - 1, n)
    value = x + 1
    while (index <= n):

        # Store maximum length subsequence length till index
        # Here index is the
        # coordinate compressed element
        BIT[index] = max(BIT[index], value)

        # Go to child node and update that node
        index += index & (-index)

# Function to calculate
# maximum Longest Increasing
# Sequence length
def findLISLength(arr, n):

    coordinateCompression(arr, n)
    BIT = [0]*(n + 1)

    for i in range(n):

        # Add elements
        # from left to right
        # in BIT
        update(BIT, arr[i], n)

    ans = query(BIT, n, n)
    return ans

# Driver code
arr=[6, 5, 1, 3, 2, 4, 8, 7]
n = len(arr)
ans = findLISLength(arr, n)

print(ans)

# This code is contributed mohit kumar 29
```

## c#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG{

// Function to map numbers using
// coordinate compression
static void coordinateCompression(int []arr,
                                  int n)
{
  // Set will store
  // all unique numbers
  HashSet<int> s = new HashSet<int>();
  for (int i = 0; i < n; i++)
  {
    s.Add(arr[i]);
  }

  // Map will store
  // the new elements
  int index = 0;
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();

  foreach (int itr in s)
  {
    // For every new number in the set,
    index++;

    // Increment the index of the
    // current number and store it
    // in a hashmap. Here index
    // for every element is the
    // new value with with the
    // current element is replaced
    mp.Add(itr, index);
  }

  for (int i = 0; i < n; i++)
  {
    // now change the current element
    // to range 1 to N.
    arr[i] = mp[arr[i]];
  }
}

// Function to calculate
// length of maximum increasing
// sequence till i'th index
static int query(int []BIT,
                 int index, int n)
{
  int ans = 0;
  while (index > 0)
  {
    ans = Math.Max(ans,
                   BIT[index]);

    // Go to parent node
    index -= index & (-index);
  }
  return ans;
}

// Function for updating BIT array for
// maximum increasing sequence till
// i'th index
static void update(int []BIT,
                   int index, int n)
{
  // If 4 is inserted in BIT,
  // check for maximum length
  // subsequence till element 3.
  // Let this subsequence length be x.
  // If x + 1 is greater than
  // the current element in BIT,
  // update the BIT array
  int x = query(BIT, index - 1, n);
  int value = x + 1;
  while (index <= n)
  {
    // Store maximum length subsequence length
    // till index. Here index is the
    // coordinate compressed element
    BIT[index] = Math.Max(BIT[index], value);

    // Go to child node and update that node
    index += index & (-index);
  }
}

// Function to calculate maximum
// longest Increasing Sequence length
static int findLISLength(int []arr,
                         int n)
{
  coordinateCompression(arr, n);
  int []BIT = new int[n + 1];

  // Initialising BIT array
  for (int i = 0; i <= n; i++)
  {
    BIT[i] = 0;
  }

  for (int i = 0; i < n; i++)
  {
    // Add elements from
    // left to right in BIT
    update(BIT, arr[i], n);
  }

  int ans = query(BIT, n, n) / 2;
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {6, 5, 1, 3,
               2, 4, 8, 7};
  int n = arr.Length;
  int ans = findLISLength(arr, n);
  Console.WriteLine(ans);
}
}

// This code is contributed by gauravrajput1
```

## Javascript

```
<script>

// JavaScript implementation of the approach

// Function to map numbers using
// coordinate compression
function coordinateCompression(arr, n) {

    // Set will store
    // all unique numbers
    let s = new Set();
    for (let i = 0; i < n; i++) {
        s.add(arr[i]);
    }

    // Map will store
    // the new elements
    let index = 0;
    let mp = new Map();

    for (let itr of s) {
        // For every new number in the set,
        index++;

        // Increment the index of the
        // current number and store it
        // in a hashmap. Here index
        // for every element is the
        // new value with with the
        // current element is replaced
        mp.set(itr, index);
    }
    for (let i = 0; i < n; i++) {
        // now change the current element
        // to range 1 to N.
        arr[i] = mp.get(arr[i]);
    }
}

// Function to calculate length of maximum
// increasing sequence till i'th index
function query(BIT, index, n) {
    let ans = 0;
    while (index > 0) {
        ans = Math.max(ans, BIT[index]);

        // Go to parent node
        index -= index & (-index);
    }
    return ans;
}

// Function for updating BIT array for
// maximum increasing sequence till
// i'th index
function update(BIT, index, n) {

    // If 4 is inserted in BIT,
    // check for maximum length
    // subsequence till element 3.
    // Let this subsequence length be x.
    // If x + 1 is greater than
    // the current element in BIT,
    // update the BIT array
    let x = query(BIT, index - 1, n);
    let value = x + 1;
    while (index <= n) {

        // Store maximum length subsequence length
        // till index. Here index is the
        // coordinate compressed element
        BIT[index] = Math.max(BIT[index], value);

        // Go to child node and update that node
        index += index & (-index);
    }
}

// Function to calculate maximum
// Longest Increasing Sequence length
function findLISLength(arr, n) {

    coordinateCompression(arr, n);
    let BIT = new Array(n + 1);

    // Initialising BIT array
    for (let i = 0; i <= n; i++) {
        BIT[i] = 0;
    }

    for (let i = 0; i < n; i++) {
        // Add elements from left to right
        // in BIT
        update(BIT, arr[i], n);
    }

    let ans = query(BIT, n, n) / 2;
    return ans;
}

// Driver code

let arr = [6, 5, 1, 3, 2, 4, 8, 7];
let n = arr.length;
let ans = findLISLength(arr, n);

document.write(ans);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(N*log(N))

**辅助空间:** O(N)