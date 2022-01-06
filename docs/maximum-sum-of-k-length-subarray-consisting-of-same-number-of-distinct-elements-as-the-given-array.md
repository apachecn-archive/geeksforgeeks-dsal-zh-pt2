# 由与给定阵列相同数量的不同元素组成的 K 长度子阵列的最大和

> 原文:[https://www . geeksforgeeks . org/k 长度最大和子数组-由相同数量的不同元素组成-作为给定数组/](https://www.geeksforgeeks.org/maximum-sum-of-k-length-subarray-consisting-of-same-number-of-distinct-elements-as-the-given-array/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到一个**大小为 K** 的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其中不同元素的最大和与计数与原始数组相同。

**示例:**

> **输入:** arr[] = {7，7，2，4，2，7，4，6，6，6}，K = 6
> **输出:** 31
> **解释:**给定数组由 4 个不同的元素组成，即{2，4，6，7}。由所有这些元素组成且最大和为{2，7，4，6，6，6}的大小为 **K** 的子阵列，从原始阵列的第 5 个<sup>索引( *1 基索引*)开始。
> 因此，子阵之和= 2 + 7 + 4 + 6 + 6 + 6 = 31。</sup>
> 
> **输入:** arr[] = {1，2，5，5，19，2，1}，K = 4
> **输出:** 27

**天真方法:**简单的方法是[生成所有可能的大小为 K 的**子阵列**](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查它是否具有与原始阵列相同的独特元素。如果是，那么求这个子阵的和。检查完所有子阵列后，打印所有这些子阵列的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// distinct elements present in the array
int distinct(int arr[], int n)
{
    map<int,int> mpp;

    // Insert all elements into the Set
    for (int i = 0; i < n; i++)
    {
        mpp[arr[i]] = 1;
    }

    // Return the size of set
    return mpp.size();
}

// Function that finds the maximum
// sum of K-length subarray having
// same unique elements as arr[]
int maxSubSum(int arr[], int n,int k, int totalDistinct)
{

    // Not possible to find a
    // subarray of size K
    if (k > n)
        return 0;
    int maxm = 0, sum = 0;
    for (int i = 0; i < n - k + 1; i++)
    {
        sum = 0;

        // Initialize Set
        set<int> st;

        // Calculate sum of the distinct elements
        for (int j = i; j < i + k; j++)
        {
            sum += arr[j];
            st.insert(arr[j]);
        }

        // If the set size is same as the
        // count of distinct elements
        if ((int) st.size() == totalDistinct)

            // Update the maximum value
            maxm = max(sum, maxm);
    }
    return maxm;
}

// Driver code
int main()
{
  int arr[] = { 7, 7, 2, 4, 2,
                7, 4, 6, 6, 6 };
  int K = 6;
  int N = sizeof(arr)/sizeof(arr[0]);

  // Stores the count of distinct elements
  int totalDistinct = distinct(arr, N);
  cout << (maxSubSum(arr, N, K, totalDistinct));

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to count the number of
    // distinct elements present in the array
    static int distinct(int arr[], int n)
    {
        Set<Integer> set = new HashSet<>();

        // Insert all elements into the Set
        for (int i = 0; i < n; i++) {
            set.add(arr[i]);
        }

        // Return the size of set
        return set.size();
    }

    // Function that finds the maximum
    // sum of K-length subarray having
    // same unique elements as arr[]
    static int maxSubSum(int arr[], int n,
                         int k,
                         int totalDistinct)
    {
        // Not possible to find a
        // subarray of size K
        if (k > n)
            return 0;

        int max = 0, sum = 0;

        for (int i = 0; i < n - k + 1; i++) {
            sum = 0;

            // Initialize Set
            Set<Integer> set = new HashSet<>();

            // Calculate sum of the distinct elements
            for (int j = i; j < i + k; j++) {
                sum += arr[j];
                set.add(arr[j]);
            }

            // If the set size is same as the
            // count of distinct elements
            if (set.size() == totalDistinct)

                // Update the maximum value
                max = Math.max(sum, max);
        }
        return max;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 7, 7, 2, 4, 2,
                      7, 4, 6, 6, 6 };
        int K = 6;
        int N = arr.length;

        // Stores the count of distinct elements
        int totalDistinct = distinct(arr, N);

        System.out.println(
            maxSubSum(arr, N, K, totalDistinct));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# distinct elements present in the array
def distinct(arr, n):

    mpp = {}

    # Insert all elements into the Set
    for i in range(n):
        mpp[arr[i]] = 1

    # Return the size of set
    return len(mpp)

# Function that finds the maximum
# sum of K-length subarray having
# same unique elements as arr[]
def maxSubSum(arr, n, k, totalDistinct):

    # Not possible to find a
    # subarray of size K
    if (k > n):
        return 0

    maxm = 0
    sum = 0

    for i in range(n - k + 1):
        sum = 0

        # Initialize Set
        st = set()

        # Calculate sum of the distinct elements
        for j in range(i, i + k, 1):
            sum += arr[j]
            st.add(arr[j])

        # If the set size is same as the
        # count of distinct elements
        if (len(st) == totalDistinct):

            # Update the maximum value
            maxm = max(sum, maxm)

    return maxm

# Driver code
if __name__ == '__main__':

    arr = [ 7, 7, 2, 4, 2, 7, 4, 6, 6, 6 ]
    K = 6
    N = len(arr)

    # Stores the count of distinct elements
    totalDistinct = distinct(arr, N)
    print(maxSubSum(arr, N, K, totalDistinct))

# This code is contributed by ipg2016107
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to count the number of
  // distinct elements present in the array
  static int distinct(int[] arr, int n)
  {
    HashSet<int> set = new HashSet<int>();

    // Insert all elements into the Set
    for (int i = 0; i < n; i++) {
      set.Add(arr[i]);
    }

    // Return the size of set
    return set.Count;
  }

  // Function that finds the maximum
  // sum of K-length subarray having
  // same unique elements as arr[]
  static int maxSubSum(int[] arr, int n,
                       int k,
                       int totalDistinct)
  {
    // Not possible to find a
    // subarray of size K
    if (k > n)
      return 0;

    int max = 0, sum = 0;

    for (int i = 0; i < n - k + 1; i++) {
      sum = 0;

      // Initialize Set
      HashSet<int> set = new HashSet<int>();

      // Calculate sum of the distinct elements
      for (int j = i; j < i + k; j++) {
        sum += arr[j];
        set.Add(arr[j]);
      }

      // If the set size is same as the
      // count of distinct elements
      if (set.Count == totalDistinct)

        // Update the maximum value
        max = Math.Max(sum, max);
    }
    return max;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 7, 7, 2, 4, 2,
                 7, 4, 6, 6, 6 };
    int K = 6;
    int N = arr.Length;

    // Stores the count of distinct elements
    int totalDistinct = distinct(arr, N);

    Console.WriteLine(
      maxSubSum(arr, N, K, totalDistinct));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// distinct elements present in the array
function distinct(arr, n)
{
    var mpp = new Map();

    // Insert all elements into the Set
    for (var i = 0; i < n; i++)
    {
        mpp.set(arr[i], 1);
    }

    // Return the size of set
    return mpp.size;
}

// Function that finds the maximum
// sum of K-length subarray having
// same unique elements as arr[]
function maxSubSum(arr, n,k, totalDistinct)
{

    // Not possible to find a
    // subarray of size K
    if (k > n)
        return 0;
    var maxm = 0, sum = 0;
    for (var i = 0; i < n - k + 1; i++)
    {
        sum = 0;

        // Initialize Set
        var st = new Set();

        // Calculate sum of the distinct elements
        for (var j = i; j < i + k; j++)
        {
            sum += arr[j];
            st.add(arr[j]);
        }

        // If the set size is same as the
        // count of distinct elements
        if ( st.size == totalDistinct)

            // Update the maximum value
            maxm = Math.max(sum, maxm);
    }
    return maxm;
}

// Driver code
var arr = [7, 7, 2, 4, 2,
              7, 4, 6, 6, 6];
var K = 6;
var N = arr.length;

// Stores the count of distinct elements
var totalDistinct = distinct(arr, N);
document.write(maxSubSum(arr, N, K, totalDistinct));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
31
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**高效途径:**优化上述途径，思路是利用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)一次，持续更新**地图**中数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
2.  检查地图的[大小是否等于原始数组中不同元素的总数。如果发现为真，则更新最大和。](https://www.geeksforgeeks.org/mapsize-c-stl/)
3.  遍历原始数组时，如果第**I**遍历与数组中的 **K** 元素交叉，则通过删除第**(I–K)**元素的出现来更新**映射**。
4.  完成上述步骤后，打印获得的最大总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the number of
// distinct elements present in the array
int distinct(vector<int>arr, int N)
{
    set<int> st;

    // Insert array elements into set
    for(int i = 0; i < N; i++)
    {
        st.insert(arr[i]);
    }

    // Return the st size
    return st.size();
}

// Function to calculate maximum
// sum of K-length subarray having
// same unique elements as arr[]
int maxSubarraySumUtil(vector<int>arr, int N,
                       int K, int totalDistinct)
{

    // Not possible to find an
    // subarray of length K from
    // an N-sized array, if K > N
    if (K > N)
        return 0;

    int mx = 0;
    int sum = 0;

    map<int, int> mp;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update the mp
        mp[arr[i]] += 1;
        sum += arr[i];

        // If i >= K, then decrement
        // arr[i-K] element's one
        // occurence
        if (i >= K)
        {
            mp[arr[i - K]] -= 1;
            sum -= arr[i - K];

            // If frequency of any
            // element is 0 then
            // remove the element
            if (mp[arr[i - K]] == 0)
                mp.erase(arr[i - K]);
        }

        // If mp size is same as the
        // count of distinct elements
        // of array arr[] then update
        // maximum sum
        if (mp.size() == totalDistinct)
            mx = max(mx, sum);
    }
    return mx;
}

// Function that finds the maximum
// sum of K-length subarray having
// same number of distinct elements
// as the original array
void maxSubarraySum(vector<int>arr,
                           int K)
{
    // Size of array
    int N = arr.size();

    // Stores count of distinct elements
    int totalDistinct = distinct(arr, N);

    // Print maximum subarray sum
    cout<<maxSubarraySumUtil(arr, N, K, totalDistinct);
}

// Driver Code
int main()
{
    vector<int>arr { 7, 7, 2, 4, 2,
                     7, 4, 6, 6, 6 };
    int K = 6;

    // Function Call
    maxSubarraySum(arr, K);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
class GFG {

    // Function to count the number of
    // distinct elements present in the array
    static int distinct(int arr[], int N)
    {
        Set<Integer> set = new HashSet<>();

        // Insert array elements into Set
        for (int i = 0; i < N; i++) {
            set.add(arr[i]);
        }

        // Return the Set size
        return set.size();
    }

    // Function to calculate maximum
    // sum of K-length subarray having
    // same unique elements as arr[]
    static int maxSubarraySumUtil(
        int arr[], int N, int K,
        int totalDistinct)
    {
        // Not possible to find an
        // subarray of length K from
        // an N-sized array, if K > N
        if (K > N)
            return 0;

        int max = 0;
        int sum = 0;

        Map<Integer, Integer> map
            = new HashMap<>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update the map
            map.put(arr[i],
                    map.getOrDefault(arr[i], 0) + 1);
            sum += arr[i];

            // If i >= K, then decrement
            // arr[i-K] element's one
            // occurence
            if (i >= K) {
                map.put(arr[i - K],
                        map.get(arr[i - K]) - 1);
                sum -= arr[i - K];

                // If frequency of any
                // element is 0 then
                // remove the element
                if (map.get(arr[i - K]) == 0)
                    map.remove(arr[i - K]);
            }

            // If map size is same as the
            // count of distinct elements
            // of array arr[] then update
            // maximum sum
            if (map.size() == totalDistinct)
                max = Math.max(max, sum);
        }
        return max;
    }

    // Function that finds the maximum
    // sum of K-length subarray having
    // same number of distinct elements
    // as the original array
    static void maxSubarraySum(int arr[],
                               int K)
    {
        // Size of array
        int N = arr.length;

        // Stores count of distinct elements
        int totalDistinct = distinct(arr, N);

        // Print maximum subarray sum
        System.out.println(
            maxSubarraySumUtil(arr, N, K,
                               totalDistinct));
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 7, 7, 2, 4, 2,
                      7, 4, 6, 6, 6 };
        int K = 6;

        // Function Call
        maxSubarraySum(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count the number of
# distinct elements present in the array
def distinct(arr, N):
    st = set()

    # Insert array elements into set
    for i in range(N):
        st.add(arr[i])

    # Return the st size
    return len(st)

# Function to calculate maximum
# sum of K-length subarray having
# same unique elements as arr[]
def maxSubarraySumUtil(arr, N, K, totalDistinct):
    # Not possible to find an
    # subarray of length K from
    # an N-sized array, if K > N
    if (K > N):
        return 0

    mx = 0
    sum = 0

    mp = {}

    # Traverse the array
    for i in range(N):
        # Update the mp
        if(arr[i] in mp):
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1
        sum += arr[i]

        # If i >= K, then decrement
        # arr[i-K] element's one
        # occurence
        if (i >= K):
            if(arr[i-K] in mp):
                mp[arr[i - K]] -= 1
                sum -= arr[i - K]

            # If frequency of any
            # element is 0 then
            # remove the element
            if (arr[i-K] in mp and mp[arr[i - K]] == 0):
                mp.remove(arr[i - K])

        # If mp size is same as the
        # count of distinct elements
        # of array arr[] then update
        # maximum sum
        if (len(mp) == totalDistinct):
            mx = max(mx, sum)
    return mx

# Function that finds the maximum
# sum of K-length subarray having
# same number of distinct elements
# as the original array
def maxSubarraySum(arr, K):

    # Size of array
    N = len(arr)

    # Stores count of distinct elements
    totalDistinct = distinct(arr, N)

    # Print maximum subarray sum
    print(maxSubarraySumUtil(arr, N, K, totalDistinct))

# Driver Code
if __name__ == '__main__':
    arr  =  [7, 7, 2, 4, 2,7, 4, 6, 6, 6]
    K = 6

    # Function Call
    maxSubarraySum(arr, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to count the number of
// distinct elements present in the array
static int distinct(List<int>arr, int N)
{
    HashSet<int> st = new HashSet<int>();

    // Insert array elements into set
    for(int i = 0; i < N; i++)
    {
        st.Add(arr[i]);
    }

    // Return the st size
    return st.Count;
}

// Function to calculate maximum
// sum of K-length subarray having
// same unique elements as arr[]
static int maxSubarraySumUtil(List<int>arr, int N,
                       int K, int totalDistinct)
{

    // Not possible to find an
    // subarray of length K from
    // an N-sized array, if K > N
    if (K > N)
        return 0;
    int mx = 0;
    int sum = 0; 
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update the mp
        if(mp.ContainsKey(arr[i]))
            mp[arr[i]] += 1;
        else
            mp[arr[i]] = 1;
        sum += arr[i];

        // If i >= K, then decrement
        // arr[i-K] element's one
        // occurence
        if (i >= K)
        {
           if(mp.ContainsKey(arr[i - K]))
              mp[arr[i - K]] -= 1;
           else
              mp[arr[i - K]] = 1;
            sum -= arr[i - K];

            // If frequency of any
            // element is 0 then
            // remove the element
            if (mp[arr[i - K]] == 0)
                mp.Remove(arr[i - K]);
        }

        // If mp size is same as the
        // count of distinct elements
        // of array arr[] then update
        // maximum sum
        if (mp.Count == totalDistinct)
            mx = Math.Max(mx, sum);
    }
    return mx;
}

// Function that finds the maximum
// sum of K-length subarray having
// same number of distinct elements
// as the original array
static void maxSubarraySum(List<int>arr,
                           int K)
{

    // Size of array
    int N = arr.Count;

    // Stores count of distinct elements
    int totalDistinct = distinct(arr, N);

    // Print maximum subarray sum
    Console.WriteLine(maxSubarraySumUtil(arr, N, K, totalDistinct));
}

// Driver Code
public static void Main()
{
    List<int>arr = new List<int>{ 7, 7, 2, 4, 2,
                     7, 4, 6, 6, 6 };
    int K = 6;

    // Function Call
    maxSubarraySum(arr, K);
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of
// distinct elements present in the array
function distinct(arr, N)
{
    var st = new Set();

    // Insert array elements into set
    for(var i = 0; i < N; i++)
    {
        st.add(arr[i]);
    }

    // Return the st size
    return st.size;
}

// Function to calculate maximum
// sum of K-length subarray having
// same unique elements as arr[]
function maxSubarraySumUtil(arr, N, K, totalDistinct)
{

    // Not possible to find an
    // subarray of length K from
    // an N-sized array, if K > N
    if (K > N)
        return 0;

    var mx = 0;
    var sum = 0;

    var mp = new Map();

    // Traverse the array
    for(var i=0; i<N; i++) 
    {

        // Update the mp
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else   
            mp.set(arr[i], 1)

        sum += arr[i];

        // If i >= K, then decrement
        // arr[i-K] element's one
        // occurence
        if (i >= K)
        {
            if(mp.has(arr[i-K]))
                mp.set(arr[i-K], mp.get(arr[i-K])-1)

            sum -= arr[i - K];

            // If frequency of any
            // element is 0 then
            // remove the element
            if (mp.has(arr[i - K]) &&  mp.get(arr[i - K])== 0)
                mp.delete(arr[i - K]);
        }

        // If mp size is same as the
        // count of distinct elements
        // of array arr[] then update
        // maximum sum
        if (mp.size == totalDistinct)
            mx = Math.max(mx, sum);
    }
    return mx;
}

// Function that finds the maximum
// sum of K-length subarray having
// same number of distinct elements
// as the original array
function maxSubarraySum(arr, K)
{
    // Size of array
    var N = arr.length;

    // Stores count of distinct elements
    var totalDistinct = distinct(arr, N);

    // Print maximum subarray sum
    document.write( maxSubarraySumUtil(arr, N, K, totalDistinct));
}

// Driver Code

var arr = [7, 7, 2, 4, 2,
           7, 4, 6, 6, 6 ];
var K = 6;

// Function Call
maxSubarraySum(arr, K);

</script>
```

**Output:** 

```
31
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)