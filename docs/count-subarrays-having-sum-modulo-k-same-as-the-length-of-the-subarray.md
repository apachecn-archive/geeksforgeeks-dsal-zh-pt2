# 计数与子阵列长度具有相同模 K 的和的子阵列

> 原文:[https://www . geeksforgeeks . org/count-subarray-having-sum-mod-k-与子阵列的长度相同/](https://www.geeksforgeeks.org/count-subarrays-having-sum-modulo-k-same-as-the-length-of-the-subarray/)

给定一个整数 **K** 和一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出[个子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量，其和[模](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/) **K** 等于子阵列的大小。

**示例:**

> **输入:** arr[] = {1，4，3，2}，K = 3
> **输出:** 4
> **解释:**
> 1% 3 = 1
> (1+4)% 3 = 2
> 4% 3 = 1
> (3+2)% 3 = 2
> 因此，子阵列{1}、{1，4}、{4}、{3，2}满足要求的条件。
> 
> **输入:** arr[] = {2，3，5，3，1，5}，K = 4
> **输出:** 5
> **说明:**
> 子阵(5)、(1)、(5)、(1，5)、(3，5，3)满足要求条件。

**天真法:**最简单的方法是找到给定数组的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，然后[生成](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的所有子数组，并对那些具有与该子数组长度相等的**和** [**模**](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/) **K** 的子数组进行计数。打印获得的子阵列的最终计数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that counts the subarrays
// having sum modulo k equal to the
// length of subarray

long long int countSubarrays(
    int a[], int n, int k)
{

    // Stores the count
    // of subarrays
    int ans = 0;

    // Stores prefix sum
    // of the array
    vector<int> pref;
    pref.push_back(0);

    // Calculate prefix sum array
    for (int i = 0; i < n; i++)
        pref.push_back((a[i]
                        + pref[i])
                       % k);

    // Generate all the subarrays
    for (int i = 1; i <= n; i++) {
        for (int j = i; j <= n; j++) {

            // Check if this subarray is
            // a valid subarray or not
            if ((pref[j] - pref[i - 1] + k) % k
                == j - i + 1) {
                ans++;
            }
        }
    }

    // Total count of subarrays
    cout << ans << ' ';
}

// Driver Code
int main()
{
    // Given arr[]
    int arr[] = { 2, 3, 5, 3, 1, 5 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 4;

    // Function Call
    countSubarrays(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function that counts the subarrays
// having sum modulo k equal to the
// length of subarray
static void countSubarrays(int a[], int n,
                           int k)
{

    // Stores the count
    // of subarrays
    int ans = 0;

    // Stores prefix sum
    // of the array
    ArrayList<Integer> pref = new ArrayList<>();
    pref.add(0);

    // Calculate prefix sum array
    for(int i = 0; i < n; i++)
        pref.add((a[i] + pref.get(i)) % k);

    // Generate all the subarrays
    for(int i = 1; i <= n; i++)
    {
        for(int j = i; j <= n; j++)
        {

            // Check if this subarray is
            // a valid subarray or not
            if ((pref.get(j) -
                 pref.get(i - 1) + k) %
                     k == j - i + 1)
            {
                ans++;
            }
        }
    }

    // Total count of subarrays
    System.out.println(ans);
}

// Driver Code
public static void main (String[] args)
throws java.lang.Exception
{

    // Given arr[]
    int arr[] = { 2, 3, 5, 3, 1, 5 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 4;

    // Function call
    countSubarrays(arr, N, K);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the subarrays
# having sum modulo k equal to the
# length of subarray
def countSubarrays(a, n, k):

    # Stores the count
    # of subarrays
    ans = 0

    # Stores prefix sum
    # of the array
    pref = []
    pref.append(0)

    # Calculate prefix sum array
    for i in range(n):
        pref.append((a[i] + pref[i]) % k)

    # Generate all the subarrays
    for i in range(1, n + 1, 1):
        for j in range(i, n + 1, 1):

            # Check if this subarray is
            # a valid subarray or not
            if ((pref[j] -
                 pref[i - 1] + k) %
                      k == j - i + 1):
                ans += 1

    # Total count of subarrays
    print(ans, end = ' ')

# Driver Code

# Given arr[]
arr = [ 2, 3, 5, 3, 1, 5 ]

# Size of the array
N = len(arr)

# Given K
K = 4

# Function call
countSubarrays(arr, N, K)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach 
using System;
using System.Collections.Generic;

class GFG{

// Function that counts the subarrays
// having sum modulo k equal to the
// length of subarray
static void countSubarrays(int[] a, int n,
                            int k)
{

    // Stores the count
    // of subarrays
    int ans = 0;

    // Stores prefix sum
    // of the array
    List<int> pref = new List<int>();
    pref.Add(0);

    // Calculate prefix sum array
    for(int i = 0; i < n; i++)
        pref.Add((a[i] + pref[i]) % k);

    // Generate all the subarrays
    for(int i = 1; i <= n; i++)
    {
        for(int j = i; j <= n; j++)
        {

            // Check if this subarray is
            // a valid subarray or not
            if ((pref[j] -
                 pref[i - 1] + k) %
                      k == j - i + 1)
            {
                ans++;
            }
        }
    }

    // Total count of subarrays
    Console.WriteLine(ans);
}

// Driver Code
public static void Main ()
{

    // Given arr[]
    int[] arr = { 2, 3, 5, 3, 1, 5 };

    // Size of the array
    int N = arr.Length;

    // Given K
    int K = 4;

    // Function call
    countSubarrays(arr, N, K);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function that counts the subarrays
// having sum modulo k equal to the
// length of subarray

function countSubarrays( a, n, k)
{

    // Stores the count
    // of subarrays
    var ans = 0;

    // Stores prefix sum
    // of the array
    var pref = [];
    pref.push(0);

    // Calculate prefix sum array
    for (var i = 0; i < n; i++)
        pref.push((a[i]
                        + pref[i])
                       % k);

    // Generate all the subarrays
    for (var i = 1; i <= n; i++) {
        for (var j = i; j <= n; j++) {

            // Check if this subarray is
            // a valid subarray or not
            if ((pref[j] - pref[i - 1] + k) % k
                == j - i + 1) {
                ans++;
            }
        }
    }

    // Total count of subarrays
    document.write( ans + ' ');
}

// Driver Code

// Given arr[]
var arr = [ 2, 3, 5, 3, 1, 5 ];

// Size of the array
var N = arr.length;

// Given K
var K = 4;

// Function Call
countSubarrays(arr, N, K);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**思想是生成给定数组的[前缀和，然后将问题简化为子数组的计数，使得**(pref[j]–pref[I])% K**等于**(j–I)**，其中 **j > i** 和**(j-I)≤K .**下面是步骤:](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)

*   创建一个辅助数组 **pref[]** ，存储给定数组的前缀和。
*   为了计算满足上述方程的子阵列，该方程可以写成:

> (pref[j]—j)% K =(pref[I]—I)% K，其中 **j > i** 和**(j—I)≤K**

*   [遍历前缀数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**pref【】**并为每个索引 **j** 将计数**(pref[j]–j)% K**存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)T10m 中
*   对于上述步骤中的每个元素 **pref[i]** ，更新计数为**M[(pref[I]–I % K+K)% K]**，并增加地图**M**中**(pref[I]–I % K+K)% K**的频率
*   完成上述步骤后，打印子阵列的计数值。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that counts the subarrays
// s.t. sum of elements in the subarray
// modulo k is equal to size of subarray
long long int countSubarrays(
    int a[], int n, int k)
{
    // Stores the count of (pref[i] - i) % k
    unordered_map<int, int> cnt;

    // Stores the count of subarray
    long long int ans = 0;

    // Stores prefix sum of the array
    vector<int> pref;
    pref.push_back(0);

    // Find prefix sum array
    for (int i = 0; i < n; i++)
        pref.push_back((a[i]
                        + pref[i])
                       % k);

    // Base Condition
    cnt[0] = 1;

    for (int i = 1; i <= n; i++) {

        // Remove the index at present
        // after K indices from the
        // current index
        int remIdx = i - k;

        if (remIdx >= 0) {
            cnt[(pref[remIdx]
                 - remIdx % k + k)
                % k]--;
        }

        // Update the answer for subarrays
        // ending at the i-th index
        ans += cnt[(pref[i]
                    - i % k + k)
                   % k];

        // Add the calculated value of
        // current index to count
        cnt[(pref[i] - i % k + k) % k]++;
    }

    // Print the count of subarrays
    cout << ans << ' ';
}

// Driver Code
int main()
{
    // Given arr[]
    int arr[] = { 2, 3, 5, 3, 1, 5 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 4;

    // Function Call
    countSubarrays(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function that counts the subarrays
// having sum modulo k equal to the
// length of subarray

static void countSubarrays(int a[], int n,
                                    int k)
{

    // Stores the count of (pref[i] - i) % k
    HashMap<Integer, Integer> cnt = new HashMap<>();

    // Stores the count of subarray
    long  ans = 0;

    // Stores prefix sum of the array
    ArrayList<Integer> pref = new ArrayList<>();
    pref.add(0);

    // Find prefix sum array
    for(int i = 0; i < n; i++)
        pref.add((a[i] + pref.get(i)) % k);

    // Base Condition
    cnt.put(0, 1);

    for(int i = 1; i <= n; i++)
    {

        // Remove the index at present
        // after K indices from the
        // current index
        int remIdx = i - k;

        if (remIdx >= 0)
        {
            if (cnt.containsKey((pref.get(remIdx) -
                                   remIdx % k + k) % k))
                cnt.put((pref.get(remIdx) -
                          remIdx % k + k) % k,
                cnt.get((pref.get(remIdx) -
                          remIdx % k + k) % k) - 1);

            else
                cnt.put((pref.get(remIdx) -
                          remIdx % k + k) % k, -1);
        }

        // Update the answer for subarrays
        // ending at the i-th index
        if (cnt.containsKey((pref.get(i) -
                              i % k + k) % k))
            ans += cnt.get((pref.get(i) -
                             i % k + k) % k);

        // Add the calculated value of
        // current index to count
        if (cnt.containsKey((pref.get(i) -
                           i % k + k) % k))
            cnt.put((pref.get(i) -
                      i % k + k) % k,
            cnt.get((pref.get(i) -
                 i % k + k) % k) + 1);
        else
            cnt.put((pref.get(i) -
                      i % k + k) % k, 1);
    }

    // Print the count of subarrays
    System.out.println(ans);
}

// Driver Code
public static void main (String[] args)
throws java.lang.Exception
{

    // Given arr[]
    int arr[] = { 2, 3, 5, 3, 1, 5 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 4;

    // Function call
    countSubarrays(arr, N, K);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function that counts the subarrays
# s.t. sum of elements in the subarray
# modulo k is equal to size of subarray
def countSubarrays(a, n, k):

    # Stores the count of (pref[i] - i) % k
    cnt = {}

    # Stores the count of subarray
    ans = 0

    # Stores prefix sum of the array
    pref = []
    pref.append(0)

    # Find prefix sum array
    for i in range(n):
        pref.append((a[i] + pref[i]) % k)

    # Base Condition
    cnt[0] = 1

    for i in range(1, n + 1):

        # Remove the index at present
        # after K indices from the
        # current index
        remIdx = i - k

        if (remIdx >= 0):
            if ((pref[remIdx] -
                   remIdx % k + k) % k in cnt):
                cnt[(pref[remIdx] -
                       remIdx % k + k) % k] -= 1
            else:
                cnt[(pref[remIdx] -
                       remIdx % k + k) % k] = -1

        # Update the answer for subarrays
        # ending at the i-th index
        if (pref[i] - i % k + k) % k in cnt:
            ans += cnt[(pref[i] - i % k + k) % k]

        # Add the calculated value of
        # current index to count
        if (pref[i] - i % k + k) % k in cnt:
            cnt[(pref[i] - i % k + k) % k] += 1
        else:
            cnt[(pref[i] - i % k + k) % k] = 1

    # Print the count of subarrays
    print(ans, end = ' ')

# Driver code 

# Given arr[]
arr = [ 2, 3, 5, 3, 1, 5 ]

# Size of the array
N = len(arr)

# Given K
K = 4

# Function call
countSubarrays(arr, N, K)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function that counts the subarrays
// having sum modulo k equal to the
// length of subarray
static void countSubarrays(int []a, int n,
                           int k)
{
  // Stores the count of
  // (pref[i] - i) % k
  Dictionary<int,
             int> cnt = new Dictionary<int,
                                       int>();

  // Stores the count of subarray
  long ans = 0;

  // Stores prefix sum of the array
  List<int> pref = new List<int>();
  pref.Add(0);

  // Find prefix sum array
  for(int i = 0; i < n; i++)
    pref.Add((a[i] + pref[i]) % k);

  // Base Condition
  cnt.Add(0, 1);

  for(int i = 1; i <= n; i++)
  {
    // Remove the index at present
    // after K indices from the
    // current index
    int remIdx = i - k;

    if (remIdx >= 0)
    {
      if (cnt.ContainsKey((pref[remIdx] -
                           remIdx % k + k) % k))
        cnt[(pref[remIdx] -
             remIdx % k + k) % k] = cnt[(pref[remIdx] -
                                    remIdx % k + k) % k] - 1;

      else
        cnt.Add((pref[remIdx] -
                 remIdx % k + k) % k, -1);
    }

    // Update the answer for subarrays
    // ending at the i-th index
    if (cnt.ContainsKey((pref[i] -
                         i % k + k) % k))
      ans += cnt[(pref[i] -
                  i % k + k) % k];

    // Add the calculated value of
    // current index to count
    if (cnt.ContainsKey((pref[i] -
                         i % k + k) % k))
      cnt[(pref[i] -
           i % k + k) % k] = cnt[(pref[i] -
                                  i % k + k) % k] + 1;
    else
      cnt.Add((pref[i] -
               i % k + k) % k, 1);
  }

  // Print the count of subarrays
  Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)

{
  // Given []arr
  int []arr = {2, 3, 5, 3, 1, 5};

  // Size of the array
  int N = arr.Length;

  // Given K
  int K = 4;

  // Function call
  countSubarrays(arr, N, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function that counts the subarrays
    // having sum modulo k equal to the
    // length of subarray
    function countSubarrays(a , n , k) {

        // Stores the count of (pref[i] - i) % k
        var cnt = new Map();

        // Stores the count of subarray
        var ans = 0;

        // Stores prefix sum of the array
        var pref = [];
        pref.push(0);

        // Find prefix sum array
        for (i = 0; i < n; i++)
            pref.push((a[i] + pref[i]) % k);

        // Base Condition
        cnt.set(0, 1);

        for (i = 1; i <= n; i++) {

            // Remove the index at present
            // after K indices from the
            // current index
            var remIdx = i - k;

            if (remIdx >= 0) {
                if (cnt.has((pref[remIdx] - remIdx % k + k) % k))
                    cnt.set((pref[remIdx] - remIdx % k + k) % k,
                            cnt.get((pref[remIdx] - remIdx % k + k) % k) - 1);

                else
                    cnt.set((pref.get(remIdx) - remIdx % k + k) % k, -1);
            }

            // Update the answer for subarrays
            // ending at the i-th index
            if (cnt.has((pref[i] - i % k + k) % k))
                ans += cnt.get((pref[i] - i % k + k) % k);

            // Add the calculated value of
            // current index to count
            if (cnt.has((pref[i] - i % k + k) % k))
                cnt.set((pref[i] - i % k + k) % k, cnt.get((pref[i] - i % k + k) % k) + 1);
            else
                cnt.set((pref[i] - i % k + k) % k, 1);
        }

        // Prvar the count of subarrays
        document.write(ans);
    }

    // Driver Code

        // Given arr
        var arr = [ 2, 3, 5, 3, 1, 5 ];

        // Size of the array
        var N = arr.length;

        // Given K
        var K = 4;

        // Function call
        countSubarrays(arr, N, K);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)