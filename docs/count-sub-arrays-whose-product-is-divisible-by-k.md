# 计数乘积可被 k 整除的子阵列

> 原文:[https://www . geesforgeks . org/count-子数组-其乘积可被 k 整除/](https://www.geeksforgeeks.org/count-sub-arrays-whose-product-is-divisible-by-k/)

给定一个整数 **K** 和一个数组**arr【】**，任务是计算其乘积可被 **K** 整除的所有子数组。
**举例:**

> **输入:** arr[] = {6，2，8}，K = 4
> **输出:** 4
> 所需的子阵列为{6，2}、{6，2，8}、{2，8}和{8}。
> **输入:** arr[] = {9，1，14}，K = 6
> **输出:** 1

**简单方法:**运行嵌套循环，检查每个子数组是否**乘积% k == 0** 。当子阵列的条件为真时，更新**计数=计数+ 1** 。该方法的时间复杂度为 **O(n <sup>3</sup> )** 。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to count sub-arrays whose
// product is divisible by K
int countSubarrays(const int* arr, int n, int K)
{
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // Calculate the product of the
            // current sub-array
            ll product = 1;
            for (int x = i; x <= j; x++)
                product *= arr[x];

            // If product of the current sub-array
            // is divisible by K
            if (product % K == 0)
                count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 6, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 4;
    cout << countSubarrays(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to count sub-arrays whose
// product is divisible by K
static int countSubarrays(int []arr, int n, int K)
{
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {

            // Calculate the product of the
            // current sub-array
            long product = 1;
            for (int x = i; x <= j; x++)
                product *= arr[x];

            // If product of the current sub-array
            // is divisible by K
            if (product % K == 0)
                count++;
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 2, 8 };
    int n = arr.length;
    int K = 4;
    System.out.println(countSubarrays(arr, n, K));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to count sub-arrays whose
# product is divisible by K
def countSubarrays(arr, n, K):

    count = 0
    for i in range( n):
        for j in range(i, n):

            # Calculate the product of
            # the current sub-array
            product = 1
            for x in range(i, j + 1):
                product *= arr[x]

            # If product of the current
            # sub-array is divisible by K
            if (product % K == 0):
                count += 1
    return count

# Driver code
if __name__ == "__main__":

    arr = [ 6, 2, 8 ]
    n = len(arr)
    K = 4
    print(countSubarrays(arr, n, K))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to count sub-arrays whose
    // product is divisible by K
    static int countSubarrays(int []arr, int n, int K)
    {
        int count = 0;
        for (int i = 0; i < n; i++)
        {
            for (int j = i; j < n; j++)
            {

                // Calculate the product of the
                // current sub-array
                long product = 1;
                for (int x = i; x <= j; x++)
                    product *= arr[x];

                // If product of the current sub-array
                // is divisible by K
                if (product % K == 0)
                    count++;
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 6, 2, 8 };
        int n = arr.Length;
        int K = 4;

        Console.WriteLine(countSubarrays(arr, n, K));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to count sub-arrays whose
// product is divisible by K
function countSubarrays($arr, $n, $K)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i; $j < $n; $j++)
        {

            // Calculate the product of the
            // current sub-array
            $product = 1;
            for ($x = $i; $x <= $j; $x++)
                $product *= $arr[$x];

            // If product of the current
            // sub-array is divisible by K
            if ($product % $K == 0)
                $count++;
        }
    }
    return $count;
}

// Driver code
$arr = array( 6, 2, 8 );
$n = count($arr);
$K = 4;
echo countSubarrays($arr, $n, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to count sub-arrays whose
    // product is divisible by K
    function countSubarrays(arr, n, K)
    {
        let count = 0;
        for (let i = 0; i < n; i++)
        {
            for (let j = i; j < n; j++)
            {

                // Calculate the product of the
                // current sub-array
                let product = 1;
                for (let x = i; x <= j; x++)
                    product *= arr[x];

                // If product of the current sub-array
                // is divisible by K
                if (product % K == 0)
                    count++;
            }
        }
        return count;
    }

    // Driver code
    let arr = [ 6, 2, 8 ];
    let n = arr.length;
    let K = 4;
    document.write(countSubarrays(arr, n, K));

    // This ode is contributed by mukesh07.
</script>
```

**Output:** 

```
4
```

更好的方法是使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)或者使用[分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)快速找到子数组的乘积。
**分段树:**天真解的复杂度是三次的。这是因为遍历每个子数组来查找产品。代替遍历每个子数组，产品可以存储在一个段树中，并且可以查询该树以获得 **O(log n)** 时间内的**产品% k** 值。因此，该方法的时间复杂度将是 **O(n <sup>2</sup> log n)** 。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define MAX 100002

// Segment tree implemented as an array
ll tree[4 * MAX];

// Function to build the segment tree
void build(int node, int start, int end, const int* arr, int k)
{
    if (start == end) {
        tree[node] = (1LL * arr[start]) % k;
        return;
    }
    int mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
}

// Function to query product of
// sub-array[l..r] in O(log n) time
ll query(int node, int start, int end, int l, int r, int k)
{
    if (start > end || start > r || end < l) {
        return 1;
    }
    if (start >= l && end <= r) {
        return tree[node] % k;
    }
    int mid = (start + end) >> 1;
    ll q1 = query(2 * node, start, mid, l, r, k);
    ll q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
}

// Function to count sub-arrays whose
// product is divisible by K
ll countSubarrays(const int* arr, int n, int k)
{
    ll count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // Query segment tree to find product % k
            // of the sub-array[i..j]
            ll product_mod_k = query(1, 0, n - 1, i, j, k);
            if (product_mod_k == 0) {
                count++;
            }
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 6, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    // Build the segment tree
    build(1, 0, n - 1, arr, k);

    cout << countSubarrays(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
    // Java implementation for above approach
class GFG
{

static int MAX = 100002;

// Segment tree implemented as an array
static long tree[] = new long[4 * MAX];

// Function to build the segment tree
static void build(int node, int start, int end,
                            int []arr, int k)
{
    if (start == end)
    {
        tree[node] = (1L * arr[start]) % k;
        return;
    }
    int mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
}

// Function to query product of
// sub-array[l..r] in O(log n) time
static long query(int node, int start, int end,
                            int l, int r, int k)
{
    if (start > end || start > r || end < l)
    {
        return 1;
    }
    if (start >= l && end <= r)
    {
        return tree[node] % k;
    }
    int mid = (start + end) >> 1;
    long q1 = query(2 * node, start, mid, l, r, k);
    long q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
}

// Function to count sub-arrays whose
// product is divisible by K
static long countSubarrays(int []arr, int n, int k)
{
    long count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {

            // Query segment tree to find product % k
            // of the sub-array[i..j]
            long product_mod_k = query(1, 0, n - 1, i, j, k);
            if (product_mod_k == 0)
            {
                count++;
            }
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 2, 8 };
    int n = arr.length;
    int k = 4;

    // Build the segment tree
    build(1, 0, n - 1, arr, k);

    System.out.println(countSubarrays(arr, n, k));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 100002

# Segment tree implemented as an array
tree = [0 for  i in range(4 * MAX)];

# Function to build the segment tree
def build(node, start, end, arr, k):

    if (start == end):
        tree[node] = (arr[start]) % k;
        return;

    mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;

# Function to query product of
# sub-array[l..r] in O(log n) time
def query(node, start, end, l, r, k):
    if (start > end or start > r or end < l):
        return 1;
    if (start >= l and end <= r):
        return tree[node] % k;

    mid = (start + end) >> 1;
    q1 = query(2 * node, start, mid, l, r, k);
    q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;

# Function to count sub-arrays whose
# product is divisible by K
def countSubarrays(arr, n, k):
    count = 0;
    for i in range(n):
        for j in range(i, n):

            # Query segment tree to find product % k
            # of the sub-array[i..j]
            product_mod_k = query(1, 0, n - 1, i, j, k);
            if (product_mod_k == 0):
                count += 1

    return count;

# Driver code
if __name__=='__main__':

    arr = [ 6, 2, 8 ]
    n = len(arr)
    k = 4;

    # Build the segment tree
    build(1, 0, n - 1, arr, k);
    print(countSubarrays(arr, n, k))

# This code is contributed by pratham76.
```

## C#

```
// C# implementation for above approach
using System;

class GFG
{

static int MAX = 100002;

// Segment tree implemented as an array
static long []tree = new long[4 * MAX];

// Function to build the segment tree
static void build(int node, int start, int end,
                            int []arr, int k)
{
    if (start == end)
    {
        tree[node] = (1L * arr[start]) % k;
        return;
    }
    int mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
}

// Function to query product of
// sub-array[l..r] in O(log n) time
static long query(int node, int start, int end,
                            int l, int r, int k)
{
    if (start > end || start > r || end < l)
    {
        return 1;
    }
    if (start >= l && end <= r)
    {
        return tree[node] % k;
    }
    int mid = (start + end) >> 1;
    long q1 = query(2 * node, start, mid, l, r, k);
    long q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
}

// Function to count sub-arrays whose
// product is divisible by K
static long countSubarrays(int []arr, int n, int k)
{
    long count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {

            // Query segment tree to find product % k
            // of the sub-array[i..j]
            long product_mod_k = query(1, 0, n - 1, i, j, k);
            if (product_mod_k == 0)
            {
                count++;
            }
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 6, 2, 8 };
    int n = arr.Length;
    int k = 4;

    // Build the segment tree
    build(1, 0, n - 1, arr, k);

    Console.WriteLine(countSubarrays(arr, n, k));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation for above approach

let MAX = 100002;

// Segment tree implemented as an array
let tree = new Array(4 * MAX);

// Function to build the segment tree
function build(node,start,end,arr,k)
{
    if (start == end)
    {
        tree[node] = (1 * arr[start]) % k;
        return;
    }
    let mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
}

// Function to query product of
// sub-array[l..r] in O(log n) time
function query(node,start,end,l,r,k)
{
    if (start > end || start > r || end < l)
    {
        return 1;
    }
    if (start >= l && end <= r)
    {
        return tree[node] % k;
    }
    let mid = (start + end) >> 1;
    let q1 = query(2 * node, start, mid, l, r, k);
    let q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
}

// Function to count sub-arrays whose
// product is divisible by K
function countSubarrays(arr,n,k)
{
    let count = 0;
    for (let i = 0; i < n; i++)
    {
        for (let j = i; j < n; j++)
        {

            // Query segment tree to find product % k
            // of the sub-array[i..j]
            let product_mod_k = query(1, 0, n - 1, i, j, k);
            if (product_mod_k == 0)
            {
                count++;
            }
        }
    }
    return count;
}

// Driver code
let arr=[ 6, 2, 8];
let n = arr.length;
let k = 4;

// Build the segment tree
build(1, 0, n - 1, arr, k);

document.write(countSubarrays(arr, n, k));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
4
```

**进一步优化解:**可以理解，如果子阵列的乘积[i..j]可以被 k 整除，那么所有子阵的**积【I..使得 j < t < n 也可以被 k** 整除。因此[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以应用于从特定索引 i 开始计数子阵列**，并且其乘积可以被 k
整除**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 100005
typedef long long ll;

// Segment tree implemented as an array
ll tree[MAX << 2];

// Function to build segment tree
void build(int node, int start, int end, const int* arr, int k)
{
    if (start == end) {
        tree[node] = arr[start] % k;
        return;
    }
    int mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
}

// Function to query product % k
// of sub-array[l..r]
ll query(int node, int start, int end, int l, int r, int k)
{
    if (start > end || start > r || end < l)
        return 1;
    if (start >= l && end <= r)
        return tree[node] % k;
    int mid = (start + end) >> 1;
    ll q1 = query(2 * node, start, mid, l, r, k);
    ll q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
}

// Function to return the count of sub-arrays
// whose product is divisible by K
ll countSubarrays(int* arr, int n, int k)
{

    ll ans = 0;

    for (int i = 0; i < n; i++) {

        int low = i, high = n - 1;

        // Binary search
        // Check if sub-array[i..mid] satisfies the constraint
        // Adjust low and high accordingly
        while (low <= high) {
            int mid = (low + high) >> 1;
            if (query(1, 0, n - 1, i, mid, k) == 0)
                high = mid - 1;
            else
                low = mid + 1;
        }
        ans += n - low;
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 6, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    // Build the segment tree
    build(1, 0, n - 1, arr, k);

    cout << countSubarrays(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
  static int MAX = 100005;

  // Segment tree implemented as an array
  static int tree[] = new int[MAX << 2];

  // Function to build segment tree
  static void build(int node, int start,
                    int end, int arr[], int k)
  {
    if (start == end) {
      tree[node] = arr[start] % k;
      return;
    }
    int mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
  }

  // Function to query product % k
  // of sub-array[l..r]
  static int query(int node, int start, int end, int l, int r, int k)
  {
    if (start > end || start > r || end < l)
      return 1;
    if (start >= l && end <= r)
      return tree[node] % k;
    int mid = (start + end) >> 1;
    int q1 = query(2 * node, start, mid, l, r, k);
    int q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
  }

  // Function to return the count of sub-arrays
  // whose product is divisible by K
  static int countSubarrays(int arr[], int n, int k)
  {      
    int ans = 0;      
    for (int i = 0; i < n; i++)
    {
      int low = i, high = n - 1;

      // Binary search
      // Check if sub-array[i..mid] satisfies the constraint
      // Adjust low and high accordingly
      while (low <= high)
      {
        int mid = (low + high) >> 1;
        if (query(1, 0, n - 1, i, mid, k) == 0)
          high = mid - 1;
        else
          low = mid + 1;
      }
      ans += n - low;
    }
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 6, 2, 8 };
    int n = arr.length;
    int k = 4;

    // Build the segment tree
    build(1, 0, n - 1, arr, k);
    System.out.println(countSubarrays(arr, n, k));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100005

# Segment tree implemented as an array
tree = [0 for i in range(MAX << 2)];

# Function to build segment tree
def build(node, start, end,  arr, k):
    if (start == end):
        tree[node] = arr[start] % k;
        return;   
    mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;

# Function to query product % k
# of sub-array[l..r]
def query(node, start, end, l, r, k):
    if (start > end or start > r or end < l):
        return 1;
    if (start >= l and end <= r):
        return tree[node] % k;
    mid = (start + end) >> 1;
    q1 = query(2 * node, start, mid, l, r, k);
    q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;

# Function to return the count of sub-arrays
# whose product is divisible by K
def countSubarrays(arr, n, k):
    ans = 0;
    for i in range(n):
        low = i
        high = n - 1;

        # Binary search
        # Check if sub-array[i..mid] satisfies the constraint
        # Adjust low and high accordingly
        while (low <= high):
            mid = (low + high) >> 1;
            if (query(1, 0, n - 1, i, mid, k) == 0):
                high = mid - 1;
            else:
                low = mid + 1;       
        ans += n - low;   
    return ans;

# Driver code
if __name__=='__main__':

    arr = [ 6, 2, 8 ]
    n = len(arr)
    k = 4;

    # Build the segment tree
    build(1, 0, n - 1, arr, k);
    print(countSubarrays(arr, n, k))

    # This code is contributed by rutvik_56.
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

    static int MAX = 100005;

  // Segment tree implemented as an array
  static int[] tree = new int[MAX << 2];

  // Function to build segment tree
  static void build(int node, int start,
                    int end, int[] arr, int k)
  {
    if (start == end)
    {
      tree[node] = arr[start] % k;
      return;
    }
    int mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
  }

  // Function to query product % k
  // of sub-array[l..r]
  static int query(int node, int start, int end,
                   int l, int r, int k)
  {
    if (start > end || start > r || end < l)
      return 1;
    if (start >= l && end <= r)
      return tree[node] % k;
    int mid = (start + end) >> 1;
    int q1 = query(2 * node, start, mid, l, r, k);
    int q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
  }

  // Function to return the count of sub-arrays
  // whose product is divisible by K
  static int countSubarrays(int[] arr, int n, int k)
  {      
    int ans = 0;      
    for (int i = 0; i < n; i++)
    {
      int low = i, high = n - 1;

      // Binary search
      // Check if sub-array[i..mid] satisfies the constraint
      // Adjust low and high accordingly
      while (low <= high)
      {
        int mid = (low + high) >> 1;
        if (query(1, 0, n - 1, i, mid, k) == 0)
          high = mid - 1;
        else
          low = mid + 1;
      }
      ans += n - low;
    }
    return ans;
  }

  // Driver code
  static void Main() {
    int[] arr = { 6, 2, 8 };
    int n = arr.Length;
    int k = 4;

    // Build the segment tree
    build(1, 0, n - 1, arr, k);
    Console.Write(countSubarrays(arr, n, k));
  }
}

// This code is contributed by divyeshrbadiya07
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let MAX = 100005;

// Segment tree implemented as an array
let tree = new Array(MAX << 2);

// Function to build segment tree
function build(node, start, end, arr, k)
{
    if (start == end)
    {
      tree[node] = arr[start] % k;
      return;
    }
    let mid = (start + end) >> 1;
    build(2 * node, start, mid, arr, k);
    build(2 * node + 1, mid + 1, end, arr, k);
    tree[node] = (tree[2 * node] * tree[2 * node + 1]) % k;
}

// Function to query product % k
  // of sub-array[l..r]
function query(node,start,end,l,r,k)
{
    if (start > end || start > r || end < l)
      return 1;
    if (start >= l && end <= r)
      return tree[node] % k;
    let mid = (start + end) >> 1;
    let q1 = query(2 * node, start, mid, l, r, k);
    let q2 = query(2 * node + 1, mid + 1, end, l, r, k);
    return (q1 * q2) % k;
}

 // Function to return the count of sub-arrays
  // whose product is divisible by K
function countSubarrays(arr,n,k)
{
    let ans = 0;     
    for (let i = 0; i < n; i++)
    {
      let low = i, high = n - 1;

      // Binary search
      // Check if sub-array[i..mid] satisfies the constraint
      // Adjust low and high accordingly
      while (low <= high)
      {
        let mid = (low + high) >> 1;
        if (query(1, 0, n - 1, i, mid, k) == 0)
          high = mid - 1;
        else
          low = mid + 1;
      }
      ans += n - low;
    }
    return ans;
}

 // Driver code
let arr = [6, 2, 8];
let n = arr.length;
let k = 4;

// Build the segment tree
build(1, 0, n - 1, arr, k);
document.write(countSubarrays(arr, n, k));

// This code is contributed by avanitrachhadiya2155.
</script>
```

**Output:** 

```
4
```

**双指针技术:**类似于二进制搜索的讨论，很明显如果子数组[i..j]的乘积可被 **k** 整除，则所有子数组[i..这样 j < t < n 也将拥有可被 **k** 整除的产品。
因此，对应于上述事实，这里也可以应用双指针技术。取两个指针 **l，r** ，其中 **l** 指向**电流**子阵的开始， **r** 指向**电流**子阵的结束。如果子阵列[l..r]的乘积可被 k 整除，则所有子阵列[l..s]使得 r < s < n 将具有可被 k 整除的乘积，因此执行**count = count+n–r .**由于需要在当前子阵列中添加和移除元素，因此不能简单地从整个子阵列中获取乘积，因为以这种方式添加和移除元素会很麻烦。
取而代之的是， **k** 在 **O(sqrt(n))** 时间内进行素因子分解，其素因子存储在 STL 图中。另一个图用于保持当前子阵列中素数的计数，在本文中该图可以称为**当前图**。然后每当需要在当前子阵列中添加元素时，这些素数的计数被添加到**当前图**中，这发生在 **k** 的素数分解中。每当需要从**当前图**中移除一个元素时，类似地减去素数。
以下是上述办法的实施情况。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define MAX 100002
#define pb push_back

// Vector to store primes
vector<int> primes;

// k_cnt stores count of prime factors of k
// current_map stores the count of primes
// in the current sub-array
// cnts[] is an array of maps which stores
// the count of primes for element at index i
unordered_map<int, int> k_cnt, current_map, cnts[MAX];

// Function to store primes in
// the vector primes
void sieve()
{

    int prime[MAX];
    prime[0] = prime[1] = 1;
    for (int i = 2; i < MAX; i++) {
        if (prime[i] == 0) {
            for (int j = i * 2; j < MAX; j += i) {
                if (prime[j] == 0) {
                    prime[j] = i;
                }
            }
        }
    }

    for (int i = 2; i < MAX; i++) {
        if (prime[i] == 0) {
            prime[i] = i;
            primes.pb(i);
        }
    }
}

// Function to count sub-arrays whose product
// is divisible by k
ll countSubarrays(int* arr, int n, int k)
{

    // Special case
    if (k == 1) {
        cout << (1LL * n * (n + 1)) / 2;
        return 0;
    }

    vector<int> k_primes;

    for (auto p : primes) {
        while (k % p == 0) {
            k_primes.pb(p);
            k /= p;
        }
    }

    // If k is prime and is more than 10^6
    if (k > 1) {
        k_primes.pb(k);
    }

    for (auto num : k_primes) {
        k_cnt[num]++;
    }

    // Two pointers initialized
    int l = 0, r = 0;

    ll ans = 0;

    while (r < n) {

        // Add rth element to the current segment
        for (auto& it : k_cnt) {

            // p = prime factor of k
            int p = it.first;

            while (arr[r] % p == 0) {
                current_map[p]++;
                cnts[r][p]++;
                arr[r] /= p;
            }
        }

        // Check if current sub-array's product
        // is divisible by k
        int flag = 0;
        for (auto& it : k_cnt) {
            int p = it.first;
            if (current_map[p] < k_cnt[p]) {
                flag = 1;
                break;
            }
        }

        // If for all prime factors p of k,
        // current_map[p] >= k_cnt[p]
        // then current sub-array is divisible by k

        if (!flag) {

            // flag = 0 means that after adding rth element
            // segment's product is divisible by k
            ans += n - r;

            // Eliminate 'l' from the current segment
            for (auto& it : k_cnt) {
                int p = it.first;
                current_map[p] -= cnts[l][p];
            }

            l++;
        }
        else {
            r++;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 6, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    sieve();

    cout << countSubarrays(arr, n, k);

    return 0;
}
```

**Output:** 

```
4
```