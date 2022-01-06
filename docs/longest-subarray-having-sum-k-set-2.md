# 总和为 K 的最长子阵列|集合 2

> 原文:[https://www . geesforgeks . org/long-subarray-having-sum-k-set-2/](https://www.geeksforgeeks.org/longest-subarray-having-sum-k-set-2/)

给定一个包含整数的 **N** 大小的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到和等于给定值 **K** 的最长子阵列的长度。

**示例:**

> **输入:** arr[] = {2，3，4，2，1，1}，K = 10
> **输出:** 4
> **解释:**
> 子阵{3，4，2，1}求和为 10。
> 
> **输入:** arr[] = {6，8，14，9，4，11，10}，K = 13
> **输出:** 2
> **解释:**
> 子阵{9，4}给出求和为 13。

**天真做法:**请参考[这篇](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)文章。
**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(1)*

**高效方法:**思路是利用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到最大长度有和的子阵 **K** 。以下是步骤:

1.  从给定数组 **arr[]** 中创建一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)(比如说 **pref[]** )。
2.  对于前缀数组中的每个元素 **pref[]** 做二分搜索法:
    *   将 **ans** 、 **start** 和 **end** 变量分别初始化为 **-1、0** 、**T9】和 **N** 。**
    *   找到中间指数(说**中间**)。
    *   如果**优先选择【中】–val≤K**，那么将起始变量更新为**中+ 1** 和 **ans** 至**中**。
    *   否则将结束变量更新为**中间–1**。
3.  从上面的二分搜索法返回**和**的值。
4.  如果当前子阵列长度小于**(ans–I)**，则将最大长度更新为**(ans–I)**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// To store the prefix sum array
vector<int> v;

// Function for searching the
// lower bound of the subarray
int bin(int val, int k, int n)
{
    int lo = 0;
    int hi = n;
    int mid;
    int ans = -1;

    // Iterate until low less
    // than equal to high
    while (lo <= hi) {
        mid = lo + (hi - lo) / 2;

        // For each mid finding sum
        // of sub array less than
        // or equal to k
        if (v[mid] - val <= k) {
            lo = mid + 1;
            ans = mid;
        }
        else
            hi = mid - 1;
    }

    // Return the final answer
    return ans;
}

// Function to find the length of
// subarray with sum K
void findSubarraySumK(int arr[], int N, int K)
{

    // Initialize sum to 0
    int sum = 0;
    v.push_back(0);

    // Push the prefix sum of the
    // array arr[] in prefix[]
    for (int i = 0; i < N; i++) {

        sum += arr[i];
        v.push_back(sum);
    }

    int l = 0, ans = 0, r;

    for (int i = 0; i < N; i++) {

        // Search r for each i
        r = bin(v[i], K, N);

        // Update ans
        ans = max(ans, r - i);
    }

    // Print the length of subarray
    // found in the array
    cout << ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 6, 8, 14, 9, 4, 11, 10 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Given sum K
    int K = 13;

    // Function Call
    findSubarraySumK(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // To store the prefix sum array
    static Vector<Integer> v = new Vector<Integer>();

    // Function for searching the
    // lower bound of the subarray
    static int bin(int val, int k, int n)
    {
        int lo = 0;
        int hi = n;
        int mid;
        int ans = -1;

        // Iterate until low less
        // than equal to high
        while (lo <= hi) {
            mid = lo + (hi - lo) / 2;

            // For each mid finding sum
            // of sub array less than
            // or equal to k
            if (v.get(mid) - val <= k) {
                lo = mid + 1;
                ans = mid;
            }
            else
                hi = mid - 1;
        }

        // Return the final answer
        return ans;
    }

    // Function to find the length of
    // subarray with sum K
    static void findSubarraySumK(int arr[], int N, int K)
    {

        // Initialize sum to 0
        int sum = 0;
        v.add(0);

        // Push the prefix sum of the
        // array arr[] in prefix[]
        for (int i = 0; i < N; i++) {
            sum += arr[i];
            v.add(sum);
        }

        int l = 0, ans = 0, r;

        for (int i = 0; i < v.size(); i++) {

            // Search r for each i
            r = bin(v.get(i), K, N);

            // Update ans
            ans = Math.max(ans, r - i);
        }

        // Print the length of subarray
        // found in the array
        System.out.print(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array arr[]
        int arr[] = { 6, 8, 14, 9, 4, 11, 10 };

        int N = arr.length;

        // Given sum K
        int K = 13;

        // Function call
        findSubarraySumK(arr, N, K);
    }
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To store the prefix sum1 array
v = []

# Function for searching the
# lower bound of the subarray

def bin1(val, k, n):

    global v
    lo = 0
    hi = n
    mid = 0
    ans = -1

    # Iterate until low less
    # than equal to high
    while (lo <= hi):
        mid = lo + ((hi - lo) // 2)

        # For each mid finding sum1
        # of sub array less than
        # or equal to k
        if (v[mid] - val <= k):
            lo = mid + 1
            ans = mid
        else:
            hi = mid - 1

    # Return the final answer
    return ans

# Function to find the length of
# subarray with sum1 K

def findSubarraysum1K(arr, N, K):

    global v

    # Initialize sum1 to 0
    sum1 = 0
    v.append(0)

    # Push the prefix sum1 of the
    # array arr[] in prefix[]
    for i in range(N):
        sum1 += arr[i]
        v.append(sum1)

    l = 0
    ans = 0
    r = 0

    for i in range(len(v)):

        # Search r for each i
        r = bin1(v[i], K, N)

        # Update ans
        ans = max(ans, r - i)

    # Print the length of subarray
    # found in the array
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [6, 8, 14, 9, 4, 11, 10]

    N = len(arr)

    # Given sum1 K
    K = 13

    # Function Call
    findSubarraysum1K(arr, N, K)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // To store the prefix sum array
    static List<int> v = new List<int>();

    // Function for searching the
    // lower bound of the subarray
    static int bin(int val, int k, int n)
    {
        int lo = 0;
        int hi = n;
        int mid;
        int ans = -1;

        // Iterate until low less
        // than equal to high
        while (lo <= hi) {
            mid = lo + (hi - lo) / 2;

            // For each mid finding sum
            // of sub array less than
            // or equal to k
            if (v[mid] - val <= k) {
                lo = mid + 1;
                ans = mid;
            }
            else
                hi = mid - 1;
        }

        // Return the final answer
        return ans;
    }

    // Function to find the length of
    // subarray with sum K
    static void findSubarraySumK(int[] arr, int N, int K)
    {

        // Initialize sum to 0
        int sum = 0;
        v.Add(0);

        // Push the prefix sum of the
        // array []arr in prefix[]
        for (int i = 0; i < N; i++) {
            sum += arr[i];
            v.Add(sum);
        }

        int ans = 0, r;

        for (int i = 0; i < v.Count; i++) {

            // Search r for each i
            r = bin(v[i], K, N);

            // Update ans
            ans = Math.Max(ans, r - i);
        }

        // Print the length of subarray
        // found in the array
        Console.Write(ans);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given array []arr
        int[] arr = { 6, 8, 14, 9, 4, 11, 10 };

        int N = arr.Length;

        // Given sum K
        int K = 13;

        // Function call
        findSubarraySumK(arr, N, K);
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// To store the prefix sum array
let v = [];

// Function for searching the
// lower bound of the subarray
function bin(val, k, n)
{
    let lo = 0;
    let hi = n;
    let mid;
    let ans = -1;

    // Iterate until low less
    // than equal to high
    while (lo <= hi) {
        mid = lo + parseInt((hi - lo) / 2);

        // For each mid finding sum
        // of sub array less than
        // or equal to k
        if (v[mid] - val <= k) {
            lo = mid + 1;
            ans = mid;
        }
        else
            hi = mid - 1;
    }

    // Return the final answer
    return ans;
}

// Function to find the length of
// subarray with sum K
function findSubarraySumK(arr, N, K)
{

    // Initialize sum to 0
    let sum = 0;
    v.push(0);

    // Push the prefix sum of the
    // array arr[] in prefix[]
    for (let i = 0; i < N; i++) {

        sum += arr[i];
        v.push(sum);
    }

    let l = 0, ans = 0, r;

    for (let i = 0; i < N; i++) {

        // Search r for each i
        r = bin(v[i], K, N);

        // Update ans
        ans = Math.max(ans, r - i);
    }

    // Print the length of subarray
    // found in the array
    document.write(ans);
}

// Driver Code
    // Given array arr[]
    let arr = [ 6, 8, 14, 9, 4, 11, 10 ];

    let N = arr.length;

    // Given sum K
    let K = 13;

    // Function Call
    findSubarraySumK(arr, N, K);

</script>
```

**Output**

```
2
```

**时间复杂度:***O(N * log<sub>2</sub>N)*
**辅助空间:** *O(N)*

**高效进场:**对于 **O(N)进场**，请参考[这篇](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)文章的高效进场。