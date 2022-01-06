# 使用回溯的给定和的最大大小子集

> 原文:[https://www . geeksforgeeks . org/最大大小子集带给定总和使用回溯/](https://www.geeksforgeeks.org/maximum-size-subset-with-given-sum-using-backtracking/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** ，任务是找出最长子序列的长度，其和等于 **K** 。
**示例:**

> **输入:** arr[] = {-4，-2，-2，-1，6}，K = 0
> **输出:** 3
> **解释:**
> 最长的子序列长度为 3，长度为{-4，-2，6}总和为 0。
> **输入:** arr[] = {-3，0，1，1，2}，K = 1
> **输出:** 5
> **解释:**最长的子序列长度为 5，长度为{-3，0，1，1，2}和为 1。

**天真方法:**解决问题最简单的方法是生成所有可能的不同长度的子序列，并检查它们的和是否等于 **K** 。从所有这些带有和 **K** 的子序列中，找出长度最长的子序列。
***时间复杂度:**O(2<sup>N</sup>)*
**递归&回溯法:**这个问题的基本方法是对向量进行排序，找出所有可能子序列的和，并提取具有给定和的最大长度的子序列。这可以使用[递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)来完成。
按照以下步骤解决这个问题:

*   给定数组/向量排序。
*   初始化一个全局变量 **max_length** 为 0，存储最大长度子集。
*   对于数组中的每个索引 **i** ，调用递归函数找出元素在范围**【I，N-1】**内且具有和 **K** 的所有可能子集。
*   每次找到一个和为 **K** 的子集，检查其大小是否大于当前的 **max_length** 值。如果是，则更新**最大长度**的值。
*   计算出所有可能的子集和后，返回**最大长度**。

以下是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Initialise maximum possible
// length of subsequence
int max_length = 0;

// Store elements to compare
// max_length with its size
// and change the value of
// max_length accordingly
vector<int> store;

// Store the elements of the
// longest subsequence
vector<int> ans;

// Function to find the length
// of longest subsequence
void find_max_length(
    vector<int>& arr,
    int index, int sum, int k)
{
    sum = sum + arr[index];
    store.push_back(arr[index]);
    if (sum == k) {
        if (max_length < store.size()) {
            // Update max_length
            max_length = store.size();

            // Store the subsequence
            // elements
            ans = store;
        }
    }

    for (int i = index + 1;
         i < arr.size(); i++) {
        if (sum + arr[i] <= k) {

            // Recursively proceed
            // with obtained sum
            find_max_length(arr, i,
                            sum, k);

            // poping elements
            // from back
            // of vector store
            store.pop_back();
        }

        // if sum > 0 then we don't
        // required thatsubsequence
        // so return and continue
        // with earlier elements
        else
            return;
    }

    return;
}

int longestSubsequence(vector<int> arr,
                       int n, int k)
{

    // Sort the given array
    sort(arr.begin(), arr.end());

    // Traverse the array
    for (int i = 0; i < n; i++) {
        // If max_length is already
        // greater than or equal
        // than remaining length
        if (max_length >= n - i)
            break;

        store.clear();

        find_max_length(arr, i, 0, k);
    }

    return max_length;
}

// Driver code
int main()
{
    vector<int> arr{ -3, 0, 1, 1, 2 };
    int n = arr.size();
    int k = 1;

    cout << longestSubsequence(arr,
                               n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.util.*;
class GFG{

// Initialise maximum possible
// length of subsequence
static int max_length = 0;

// Store elements to compare
// max_length with its size
// and change the value of
// max_length accordingly
static Vector<Integer> store = new Vector<Integer>();

// Store the elements of the
// longest subsequence
static Vector<Integer> ans = new Vector<Integer>();

// Function to find the length
// of longest subsequence
static void find_max_length(
    int []arr,
    int index, int sum, int k)
{
    sum = sum + arr[index];
    store.add(arr[index]);
    if (sum == k)
    {
        if (max_length < store.size())
        {
            // Update max_length
            max_length = store.size();

            // Store the subsequence
            // elements
            ans = store;
        }
    }

    for (int i = index + 1;
             i < arr.length; i++)
    {
        if (sum + arr[i] <= k)
        {

            // Recursively proceed
            // with obtained sum
            find_max_length(arr, i,
                            sum, k);

            // poping elements
            // from back
            // of vector store
            store.remove(store.size() - 1);
        }

        // if sum > 0 then we don't
        // required thatsubsequence
        // so return and continue
        // with earlier elements
        else
            return;
    }
    return;
}

static int longestSubsequence(int []arr,
                                 int n, int k)
{

    // Sort the given array
    Arrays.sort(arr);

    // Traverse the array
    for (int i = 0; i < n; i++)
    {
        // If max_length is already
        // greater than or equal
        // than remaining length
        if (max_length >= n - i)
            break;

        store.clear();

        find_max_length(arr, i, 0, k);
    }
    return max_length;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { -3, 0, 1, 1, 2 };
    int n = arr.length;
    int k = 1;

    System.out.print(longestSubsequence(arr,
                                           n, k));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 Program to implement the
# above approach
# Initialise maximum possible
# length of subsequence
max_length = 0

# Store elements to compare
# max_length with its size
# and change the value of
# max_length accordingly
store = []

# Store the elements of the
# longest subsequence
ans = []

# Function to find the length
# of longest subsequence
def find_max_length(arr, index, sum, k): 
    global max_length
    sum = sum + arr[index]
    store.append(arr[index])
    if (sum == k):
        if (max_length < len(store)):
            # Update max_length
            max_length = len(store)

            # Store the subsequence
            # elements
            ans = store

    for i in range ( index + 1, len(arr)):
        if (sum + arr[i] <= k):

            # Recursively proceed
            # with obtained sum
            find_max_length(arr, i,
                            sum, k)

            # poping elements
            # from back
            # of vector store
            store.pop()

        # if sum > 0 then we don't
        # required thatsubsequence
        # so return and continue
        # with earlier elements
        else:
            return
    return

def longestSubsequence(arr, n, k):

    # Sort the given array
    arr.sort()

    # Traverse the array
    for i in range (n):

        # If max_length is already
        # greater than or equal
        # than remaining length
        if (max_length >= n - i):
            break

        store.clear()
        find_max_length(arr, i, 0, k)

    return max_length

# Driver code
if __name__ == "__main__":

    arr = [-3, 0, 1, 1, 2]
    n = len(arr)
    k = 1
    print (longestSubsequence(arr, n, k))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Initialise maximum possible
// length of subsequence
static int max_length = 0;

// Store elements to compare
// max_length with its size
// and change the value of
// max_length accordingly
static List<int> store = new List<int>();

// Store the elements of the
// longest subsequence
static List<int> ans = new List<int>();

// Function to find the length
// of longest subsequence
static void find_max_length(int []arr,
                            int index,
                            int sum, int k)
{
    sum = sum + arr[index];
    store.Add(arr[index]);

    if (sum == k)
    {
        if (max_length < store.Count)
        {

            // Update max_length
            max_length = store.Count;

            // Store the subsequence
            // elements
            ans = store;
        }
    }

    for(int i = index + 1;
            i < arr.Length; i++)
    {
        if (sum + arr[i] <= k)
        {

            // Recursively proceed
            // with obtained sum
            find_max_length(arr, i,
                            sum, k);

            // poping elements
            // from back
            // of vector store
            store.RemoveAt(store.Count - 1);
        }

        // If sum > 0 then we don't
        // required thatsubsequence
        // so return and continue
        // with earlier elements
        else
            return;
    }
    return;
}

static int longestSubsequence(int []arr,
                              int n, int k)
{

    // Sort the given array
    Array.Sort(arr);

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If max_length is already
        // greater than or equal
        // than remaining length
        if (max_length >= n - i)
            break;

        store.Clear();

        find_max_length(arr, i, 0, k);
    }
    return max_length;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { -3, 0, 1, 1, 2 };
    int n = arr.Length;
    int k = 1;

    Console.Write(longestSubsequence(arr,
                                     n, k));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript Program to implement the
// above approach

// Initialise maximum possible
// length of subsequence
let max_length = 0;

// Store elements to compare
// max_length with its size
// and change the value of
// max_length accordingly
let store = [];

// Store the elements of the
// longest subsequence
let ans = [];

// Function to find the length
// of longest subsequence
function find_max_length(arr,index,sum,k)
{
    sum = sum + arr[index];
    store.push(arr[index]);
    if (sum == k)
    {
        if (max_length < store.length)
        {
            // Update max_length
            max_length = store.length;

            // Store the subsequence
            // elements
            ans = store;
        }
    }

    for (let i = index + 1;
             i < arr.length; i++)
    {
        if (sum + arr[i] <= k)
        {

            // Recursively proceed
            // with obtained sum
            find_max_length(arr, i,
                            sum, k);

            // poping elements
            // from back
            // of vector store
            store.pop();
        }

        // if sum > 0 then we don't
        // required thatsubsequence
        // so return and continue
        // with earlier elements
        else
            return;
    }
    return;
}

function longestSubsequence(arr, n, k)
{

    // Sort the given array
    arr.sort(function(a,b){return a-b;});

    // Traverse the array
    for (let i = 0; i < n; i++)
    {

        // If max_length is already
        // greater than or equal
        // than remaining length
        if (max_length >= n - i)
            break;

        store=[];

        find_max_length(arr, i, 0, k);
    }
    return max_length;
}

// Driver code
let arr = [-3, 0, 1, 1, 2 ];
let n = arr.length;
let k = 1;
document.write(longestSubsequence(arr,n, k));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*
**动态规划方法:**参考[本文](https://www.geeksforgeeks.org/maximum-size-subset-given-sum/)进一步优化解决问题的方法。