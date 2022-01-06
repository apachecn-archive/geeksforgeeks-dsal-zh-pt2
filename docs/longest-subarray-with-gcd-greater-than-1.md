# GCD 大于 1 的最长子阵列

> 原文:[https://www . geesforgeks . org/long-subarray-with-gcd-大于-1/](https://www.geeksforgeeks.org/longest-subarray-with-gcd-greater-than-1/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出子数组的最大[长度，该子数组具有大于 **1** 的所有元素的](https://www.geeksforgeeks.org/size-subarray-maximum-sum/)[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) (GCD)。

**示例:**

> **输入:** arr[] = {4，3，2，2}
> **输出:** 2
> **解释:**
> 考虑子阵列{2，2}具有最大长度的 GCD 为 2( > 1)。
> 
> **输入:** arr[] = {410，52，51，180，222，33，33 }
> T3】输出: 5

**天真方法:**给定问题可以通过[生成给定阵列的所有可能子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并跟踪 GCD 大于 1 的子阵列的最大长度来解决。检查所有子阵列后，打印获得的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum length of
// the subarray having GCD > one
void maxSubarrayLen(int arr[], int n)
{
    // Stores maximum length of subarray
    int maxLen = 0;

    // Loop to iterate over all subarrays
    // starting from index i
    for (int i = 0; i < n; i++) {

        // Find the GCD of subarray
        // from i to j
        int gcd = 0;
        for (int j = i; j < n; j++) {

            // Calculate GCD
            gcd = __gcd(gcd, arr[j]);

            // Update maximum length
            // of the subarray
            if (gcd > 1)
                maxLen = max(maxLen, j - i + 1);
            else
                break;
        }
    }

    // Print maximum length
    cout << maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 410, 52, 51, 180,
                  222, 33, 33 };
    int N = sizeof(arr) / sizeof(int);
    maxSubarrayLen(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

// Function to find maximum length of
// the subarray having GCD > one
static void maxSubarrayLen(int arr[], int n)
{
    // Stores maximum length of subarray
    int maxLen = 0;

    // Loop to iterate over all subarrays
    // starting from index i
    for (int i = 0; i < n; i++) {

        // Find the GCD of subarray
        // from i to j
        int gcd = 0;
        for (int j = i; j < n; j++) {

            // Calculate GCD
            gcd = __gcd(gcd, arr[j]);

            // Update maximum length
            // of the subarray
            if (gcd > 1)
                maxLen = Math.max(maxLen, j - i + 1);
            else
                break;
        }
    }

    // Print maximum length
    System.out.print(maxLen);
}

// Driver Code
public static void main(String[] args)

{
    int arr[] = { 410, 52, 51, 180,
                  222, 33, 33 };
    int N = arr.length;
    maxSubarrayLen(arr, N);
}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python program of the above approach
def __gcd(a, b):
  if (b == 0): return a;
  return __gcd(b, a % b);

# Function to find maximum length of
# the subarray having GCD > one
def maxSubarrayLen(arr, n) :

  # Stores maximum length of subarray
  maxLen = 0;

  # Loop to iterate over all subarrays
  # starting from index i
  for i in range(n):

    # Find the GCD of subarray
    # from i to j
    gcd = 0;
    for j in range(i, n):

      # Calculate GCD
      gcd = __gcd(gcd, arr[j]);

      # Update maximum length
      # of the subarray
      if (gcd > 1):
           maxLen = max(maxLen, j - i + 1);
      else: break;

  # Print maximum length
  print(maxLen);

# Driver Code
arr = [410, 52, 51, 180, 222, 33, 33];
N = len(arr)
maxSubarrayLen(arr, N);

# This code is contributed by gfgking.
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to find maximum length of
  // the subarray having GCD > one
  static int __gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return __gcd(a - b, b);

    return __gcd(a, b - a);
  }
  static void maxSubarrayLen(int []arr, int n)
  {

    // Stores maximum length of subarray
    int maxLen = 0;

    // Loop to iterate over all subarrays
    // starting from index i
    for (int i = 0; i < n; i++) {

      // Find the GCD of subarray
      // from i to j
      int gcd = 0;
      for (int j = i; j < n; j++) {

        // Calculate GCD
        gcd = __gcd(gcd, arr[j]);

        // Update maximum length
        // of the subarray
        if (gcd > 1)
          maxLen = Math.Max(maxLen, j - i + 1);
        else
          break;
      }
    }

    // Print maximum length
    Console.Write(maxLen);
  }

  // Driver Code
  static public void Main (){
    int []arr = { 410, 52, 51, 180,
                 222, 33, 33 };
    int N = arr.Length;
    maxSubarrayLen(arr, N);
  }
}

// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>
// Javascript program of the above approach
function __gcd(a, b) {
  if (b == 0) return a;
  return __gcd(b, a % b);
}

// Function to find maximum length of
// the subarray having GCD > one
function maxSubarrayLen(arr, n)
{

  // Stores maximum length of subarray
  let maxLen = 0;

  // Loop to iterate over all subarrays
  // starting from index i
  for (let i = 0; i < n; i++)
  {

    // Find the GCD of subarray
    // from i to j
    let gcd = 0;
    for (let j = i; j < n; j++)
    {

      // Calculate GCD
      gcd = __gcd(gcd, arr[j]);

      // Update maximum length
      // of the subarray
      if (gcd > 1) maxLen = Math.max(maxLen, j - i + 1);
      else break;
    }
  }

  // Print maximum length
  document.write(maxLen);
}

// Driver Code
let arr = [410, 52, 51, 180, 222, 33, 33];
let N = arr.length;
maxSubarrayLen(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*

**高效方法:**以上也可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)和[T5】段树 T7】进行优化。假设 **L** 表示第一个索引， **R** 表示最后一个索引， **X** 表示当前窗口的大小，那么有两种可能的情况，如下所述:](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

*   当前窗口的 GCD 为 **1** 。在这种情况下，移动到下一个大小为 **X** 的窗口(即 **L + 1** 到 **R + 1** )。
*   当前窗口的 GCD 大于 **1** 。在这种情况下，将当前窗口的大小增加一(即 **L** 到 **R + 1** )。

因此，为了实现上述思想，可以使用分段树来有效地找到数组的给定索引范围的 [GCD。](https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/)

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to build the Segment Tree
// from the given array to process
// range queries in log(N) time
void build_tree(int* b, vector<int>& seg_tree,
                int l, int r, int vertex)
{
    // Termination Condition
    if (l == r) {
        seg_tree[vertex] = b[l];
        return;
    }

    // Find the mid value
    int mid = (l + r) / 2;

    // Left and Right  Recursive Call
    build_tree(b, seg_tree, l, mid,
               2 * vertex);
    build_tree(b, seg_tree, mid + 1,
               r, 2 * vertex + 1);

    // Update the Segment Tree Node
    seg_tree[vertex] = __gcd(seg_tree[2 * vertex],
                             seg_tree[2 * vertex + 1]);
}

// Function to return the GCD of the
// elements of the Array from index
// l to index r
int range_gcd(vector<int>& seg_tree, int v,
              int tl, int tr,
              int l, int r)
{
    // Base Case
    if (l > r)
        return 0;
    if (l == tl && r == tr)
        return seg_tree[v];

    // Find the middle range
    int tm = (tl + tr) / 2;

    // Find the GCD and return
    return __gcd(
        range_gcd(seg_tree, 2 * v, tl,
                  tm, l, min(tm, r)),

        range_gcd(seg_tree, 2 * v + 1,
                  tm + 1, tr,
                  max(tm + 1, l), r));
}

// Function to print maximum length of
// the subarray having GCD > one
void maxSubarrayLen(int arr[], int n)
{
    // Stores the Segment Tree
    vector<int> seg_tree(4 * (n) + 1, 0);

    // Function call to build the
    // Segment tree from array arr[]
    build_tree(arr, seg_tree, 0, n - 1, 1);

    // Store maximum length of subarray
    int maxLen = 0;

    // Starting and ending pointer of
    // the current window
    int l = 0, r = 0;

    while (r < n && l < n) {

        // Case where the GCD of the
        // current window is 1
        if (range_gcd(seg_tree, 1, 0,
                      n - 1, l, r)
            == 1) {
            l++;
        }

        // Update the maximum length
        maxLen = max(maxLen, r - l + 1);
        r++;
    }

    // Print answer
    cout << maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 410, 52, 51, 180, 222, 33, 33 };
    int N = sizeof(arr) / sizeof(int);
    maxSubarrayLen(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG{

// Function to build the Segment Tree
// from the given array to process
// range queries in log(N) time
static void build_tree(int[] b, int [] seg_tree,
                int l, int r, int vertex)
{

    // Termination Condition
    if (l == r) {
        seg_tree[vertex] = b[l];
        return;
    }

    // Find the mid value
    int mid = (l + r) / 2;

    // Left and Right  Recursive Call
    build_tree(b, seg_tree, l, mid,
               2 * vertex);
    build_tree(b, seg_tree, mid + 1,
               r, 2 * vertex + 1);

    // Update the Segment Tree Node
    seg_tree[vertex] = __gcd(seg_tree[2 * vertex],
                             seg_tree[2 * vertex + 1]);
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Function to return the GCD of the
// elements of the Array from index
// l to index r
static int range_gcd(int [] seg_tree, int v,
              int tl, int tr,
              int l, int r)
{
    // Base Case
    if (l > r)
        return 0;
    if (l == tl && r == tr)
        return seg_tree[v];

    // Find the middle range
    int tm = (tl + tr) / 2;

    // Find the GCD and return
    return __gcd(
        range_gcd(seg_tree, 2 * v, tl,
                  tm, l, Math.min(tm, r)),

        range_gcd(seg_tree, 2 * v + 1,
                  tm + 1, tr,
                  Math.max(tm + 1, l), r));
}

// Function to print maximum length of
// the subarray having GCD > one
static void maxSubarrayLen(int arr[], int n)
{
    // Stores the Segment Tree
    int []seg_tree = new int[4 * (n) + 1];

    // Function call to build the
    // Segment tree from array arr[]
    build_tree(arr, seg_tree, 0, n - 1, 1);

    // Store maximum length of subarray
    int maxLen = 0;

    // Starting and ending pointer of
    // the current window
    int l = 0, r = 0;

    while (r < n && l < n) {

        // Case where the GCD of the
        // current window is 1
        if (range_gcd(seg_tree, 1, 0,
                      n - 1, l, r)
            == 1) {
            l++;
        }

        // Update the maximum length
        maxLen = Math.max(maxLen, r - l + 1);
        r++;
    }

    // Print answer
    System.out.print(maxLen);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 410, 52, 51, 180, 222, 33, 33 };
    int N = arr.length;
    maxSubarrayLen(arr, N);

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to build the Segment Tree
# from the given array to process
# range queries in log(N) time
def build_tree(b, seg_tree, l, r, vertex):
    # Termination Condition
    if (l == r):
        seg_tree[vertex] = b[l]
        return

    # Find the mid value
    mid = int((l + r) / 2)

    # Left and Right  Recursive Call
    build_tree(b, seg_tree, l, mid, 2 * vertex)
    build_tree(b, seg_tree, mid + 1, r, 2 * vertex + 1)

    # Update the Segment Tree Node
    seg_tree[vertex] = __gcd(seg_tree[2 * vertex], seg_tree[2 * vertex + 1])

def __gcd(a, b):
    if b == 0:
        return b
    else:
        return __gcd(b, a % b)

# Function to return the GCD of the
# elements of the Array from index
# l to index r
def range_gcd(seg_tree, v, tl, tr, l, r):
    # Base Case
    if (l > r):
        return 0
    if (l == tl and r == tr):
        return seg_tree[v]

    # Find the middle range
    tm = int((tl + tr) / 2)

    # Find the GCD and return
    return __gcd(range_gcd(seg_tree, 2 * v, tl, tm, l, min(tm, r)),
        range_gcd(seg_tree, 2 * v + 1, tm + 1, tr, max(tm + 1, l), r))

# Function to print maximum length of
# the subarray having GCD > one
def maxSubarrayLen(arr, n):
    # Stores the Segment Tree
    seg_tree = [0]*(4*n + 1)

    # Function call to build the
    # Segment tree from array []arr
    build_tree(arr, seg_tree, 0, n - 1, 1)

    # Store maximum length of subarray
    maxLen = 0

    # Starting and ending pointer of
    # the current window
    l, r = 0, 0

    while (r < n and l < n):
        # Case where the GCD of the
        # current window is 1
        if (range_gcd(seg_tree, 1, 0, n - 1, l, r) == 1):
            l+=1

        # Update the maximum length
        maxLen = max(maxLen, r - l - 1)
        r+=1

    # Print answer
    print(maxLen, end = "")

arr = [ 410, 52, 51, 180, 222, 33, 33 ]
N = len(arr)
maxSubarrayLen(arr, N)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program of the above approach
using System;
public class GFG
{

// Function to build the Segment Tree
// from the given array to process
// range queries in log(N) time
static void build_tree(int[] b, int [] seg_tree,
                int l, int r, int vertex)
{

    // Termination Condition
    if (l == r) {
        seg_tree[vertex] = b[l];
        return;
    }

    // Find the mid value
    int mid = (l + r) / 2;

    // Left and Right  Recursive Call
    build_tree(b, seg_tree, l, mid,
               2 * vertex);
    build_tree(b, seg_tree, mid + 1,
               r, 2 * vertex + 1);

    // Update the Segment Tree Node
    seg_tree[vertex] = __gcd(seg_tree[2 * vertex],
                             seg_tree[2 * vertex + 1]);
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Function to return the GCD of the
// elements of the Array from index
// l to index r
static int range_gcd(int [] seg_tree, int v,
              int tl, int tr,
              int l, int r)
{
    // Base Case
    if (l > r)
        return 0;
    if (l == tl && r == tr)
        return seg_tree[v];

    // Find the middle range
    int tm = (tl + tr) / 2;

    // Find the GCD and return
    return __gcd(
        range_gcd(seg_tree, 2 * v, tl,
                  tm, l, Math.Min(tm, r)),

        range_gcd(seg_tree, 2 * v + 1,
                  tm + 1, tr,
                  Math.Max(tm + 1, l), r));
}

// Function to print maximum length of
// the subarray having GCD > one
static void maxSubarrayLen(int []arr, int n)
{
    // Stores the Segment Tree
    int []seg_tree = new int[4 * (n) + 1];

    // Function call to build the
    // Segment tree from array []arr
    build_tree(arr, seg_tree, 0, n - 1, 1);

    // Store maximum length of subarray
    int maxLen = 0;

    // Starting and ending pointer of
    // the current window
    int l = 0, r = 0;

    while (r < n && l < n) {

        // Case where the GCD of the
        // current window is 1
        if (range_gcd(seg_tree, 1, 0,
                      n - 1, l, r)
            == 1) {
            l++;
        }

        // Update the maximum length
        maxLen = Math.Max(maxLen, r - l + 1);
        r++;
    }

    // Print answer
    Console.Write(maxLen);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 410, 52, 51, 180, 222, 33, 33 };
    int N = arr.Length;
    maxSubarrayLen(arr, N);

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program of the above approach

function __gcd(a, b) {
  if (b == 0) return a;
  return __gcd(b, a % b);
}

// Function to build the Segment Tree
// from the given array to process
// range queries in log(N) time
function build_tree(b, seg_tree, l, r, vertex) {
  // Termination Condition
  if (l == r) {
    seg_tree[vertex] = b[l];
    return;
  }

  // Find the mid value
  let mid = Math.floor((l + r) / 2);

  // Left and Right  Recursive Call
  build_tree(b, seg_tree, l, mid, 2 * vertex);
  build_tree(b, seg_tree, mid + 1, r, 2 * vertex + 1);

  // Update the Segment Tree Node
  seg_tree[vertex] = __gcd(seg_tree[2 * vertex], seg_tree[2 * vertex + 1]);
}

// Function to return the GCD of the
// elements of the Array from index
// l to index r
function range_gcd(seg_tree, v, tl, tr, l, r) {
  // Base Case
  if (l > r) return 0;
  if (l == tl && r == tr) return seg_tree[v];

  // Find the middle range
  let tm = Math.floor((tl + tr) / 2);

  // Find the GCD and return
  return __gcd(
    range_gcd(seg_tree, 2 * v, tl, tm, l, Math.min(tm, r)),

    range_gcd(seg_tree, 2 * v + 1, tm + 1, tr, Math.max(tm + 1, l), r)
  );
}

// Function to print maximum length of
// the subarray having GCD > one
function maxSubarrayLen(arr, n) {
  // Stores the Segment Tree
  let seg_tree = new Array(4 * n + 1).fill(0);

  // Function call to build the
  // Segment tree from array arr[]
  build_tree(arr, seg_tree, 0, n - 1, 1);

  // Store maximum length of subarray
  let maxLen = 0;

  // Starting and ending pointer of
  // the current window
  let l = 0,
    r = 0;

  while (r < n && l < n) {
    // Case where the GCD of the
    // current window is 1
    if (range_gcd(seg_tree, 1, 0, n - 1, l, r) == 1) {
      l++;
    }

    // Update the maximum length
    maxLen = Math.max(maxLen, r - l + 1);
    r++;
  }

  // Print answer
  document.write(maxLen);
}

// Driver Code

let arr = [410, 52, 51, 180, 222, 33, 33];
let N = arr.length;
maxSubarrayLen(arr, N);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*