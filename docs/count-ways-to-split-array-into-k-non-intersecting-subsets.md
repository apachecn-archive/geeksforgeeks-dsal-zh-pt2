# 计数将数组拆分为 K 个不相交子集的方式

> 原文:[https://www . geeksforgeeks . org/count-way-to-split-array-in-k-non-crossing-subset/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-k-non-intersecting-subsets/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** 和一个整数 **K** ，任务是将数组拆分为 **K** 个不相交的子集，使得所有 **K** 个子集的并集等于给定的数组。

**示例:**

> **输入:** arr[]= {2，3}，K=2
> **输出:** 4
> **解释:**
> 将数组划分为 K(=2)个子集的可能方式有:{ {{}、{2，3}}、{{2}、{3}}、{{3}、{2}、{ { 2 }、{ { 2 }、{ { 2 }、{ { 3 } } }。
> 因此，要求输出为 4。
> 
> **输入:** arr[] = {2，2，3，3}，K = 3
> T3】输出 : 9

**接近**:根据以下观察可以解决问题:

> 将元素放入 K 个子集的方法总数= K。
> 因此，将给定数组的所有不同元素放入 K 个子集的方法总数= K × K × …..× K(M 次)= K<sup>M</sup>T3【其中 M =给定数组中不同元素的总数。

按照以下步骤解决问题:

*   [计算不同的元素](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)，比如给定数组中的 M。
*   打印[功率(K，M)](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/) 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get
// the value of pow(K, M)
int power(int K, int M)
{
    // Stores value of pow(K, M)
    int res = 1;

    // Calculate value of pow(K, N)
    while (M > 0) {

        // If N is odd, update
        // res
        if ((M & 1) == 1) {
            res = (res * K);
        }

        // Update M to M / 2
        M = M >> 1;

        // Update K
        K = (K * K);
    }
    return res;
}

// Function to print total ways
// to split the array that
// satisfies the given condition
int cntWays(int arr[], int N,
            int K)
{
    // Stores total ways that
    // satisfies the given
    // condition
    int cntways = 0;

    // Stores count of distinct
    // elements in the given arr
    int M = 0;

    // Store distinct elements
    // of the given array
    unordered_set<int> st;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Insert current element
        // into set st.
        st.insert(arr[i]);
    }

    // Update M
    M = st.size();

    // Update cntways
    cntways = power(K, M);

    return cntways;
}

// Driver Code
int main()
{

    int arr[] = { 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;
    cout << cntWays(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to get
// the value of pow(K, M)
static int power(int K, int M)
{

    // Stores value of pow(K, M)
    int res = 1;

    // Calculate value of pow(K, N)
    while (M > 0)
    {

        // If N is odd, update
        // res
        if ((M & 1) == 1)
        {
            res = (res * K);
        }

        // Update M to M / 2
        M = M >> 1;

        // Update K
        K = (K * K);
    }
    return res;
}

// Function to print total ways
// to split the array that
// satisfies the given condition
static int cntWays(int arr[], int N,
                   int K)
{

    // Stores total ways that
    // satisfies the given
    // condition
    int cntways = 0;

    // Stores count of distinct
    // elements in the given arr
    int M = 0;

    // Store distinct elements
    // of the given array
    Set<Integer> st = new HashSet<Integer>(); 

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Insert current element
        // into set st.
        st.add(arr[i]);
    }

    // Update M
    M = st.size();

    // Update cntways
    cntways = power(K, M);

    return cntways;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 2, 3 };
    int N = arr.length;
    int K = 2;

    System.out.println(cntWays(arr, N, K));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to get
# the value of pow(K, M)
def power(K, M):

    # Stores value of pow(K, M)
    res = 1

    # Calculate value of pow(K, N)
    while (M > 0):

        # If N is odd, update
        # res
        if ((M & 1) == 1):
            res = (res * K)

        # Update M to M / 2
        M = M >> 1

        # Update K
        K = (K * K)

    return res

# Function to print total ways
# to split the array that
# satisfies the given condition
def cntWays(arr, N, K):

    # Stores total ways that
    # satisfies the given
    # condition
    cntways = 0

    # Stores count of distinct
    # elements in the given arr
    M = 0

    # Store distinct elements
    # of the given array
    st = set()

    # Traverse the given array
    for i in range(N):

        # Insert current element
        # into set st.
        st.add(arr[i])

    # Update M
    M = len(st)

    # Update cntways
    cntways = power(K, M)

    return cntways

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 3 ]
    N = len(arr)
    K = 2

    print(cntWays(arr, N, K))

# This code is contributed by math_lover
```

## C#

```
// C# program to implement
// the above approach 
using System;
using System.Collections.Generic;

class GFG{

// Function to get
// the value of pow(K, M)
static int power(int K, int M)
{

    // Stores value of pow(K, M)
    int res = 1;

    // Calculate value of pow(K, N)
    while (M > 0)
    {

        // If N is odd, update
        // res
        if ((M & 1) == 1)
        {
            res = (res * K);
        }

        // Update M to M / 2
        M = M >> 1;

        // Update K
        K = (K * K);
    }
    return res;
}

// Function to print total ways
// to split the array that
// satisfies the given condition
static int cntWays(int[] arr, int N,
                   int K)
{

    // Stores total ways that
    // satisfies the given
    // condition
    int cntways = 0;

    // Stores count of distinct
    // elements in the given arr
    int M = 0;

    // Store distinct elements
    // of the given array
    HashSet<int> st = new HashSet<int>();

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Insert current element
        // into set st.
        st.Add(arr[i]);
    }

    // Update M
    M = st.Count;

    // Update cntways
    cntways = power(K, M);

    return cntways;
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 3 };
    int N = arr.Length;
    int K = 2;

    Console.WriteLine(cntWays(arr, N, K));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to get
// the value of pow(K, M)
function power(K, M)
{
    // Stores value of pow(K, M)
    var res = 1;

    // Calculate value of pow(K, N)
    while (M > 0) {

        // If N is odd, update
        // res
        if ((M & 1) == 1) {
            res = (res * K);
        }

        // Update M to M / 2
        M = M >> 1;

        // Update K
        K = (K * K);
    }
    return res;
}

// Function to print total ways
// to split the array that
// satisfies the given condition
function cntWays( arr, N, K)
{
    // Stores total ways that
    // satisfies the given
    // condition
    var cntways = 0;

    // Stores count of distinct
    // elements in the given arr
    var M = 0;

    // Store distinct elements
    // of the given array
    var st = new Set();

    // Traverse the given array
    for (var i = 0; i < N; i++) {

        // Insert current element
        // into set st.
        st.add(arr[i]);
    }

    // Update M
    M = st.size;

    // Update cntways
    cntways = power(K, M);

    return cntways;
}

// Driver Code
var arr = [ 2, 3 ];
var N = arr.length;
var K = 2;
document.write( cntWays(arr, N, K));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*