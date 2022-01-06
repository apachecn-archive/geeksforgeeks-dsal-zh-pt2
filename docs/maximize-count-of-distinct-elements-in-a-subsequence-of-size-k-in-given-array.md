# 最大化给定数组中大小为 K 的子序列中不同元素的数量

> 原文:[https://www . geesforgeks . org/给定数组中大小为 k 的子序列中不同元素的最大计数/](https://www.geeksforgeeks.org/maximize-count-of-distinct-elements-in-a-subsequence-of-size-k-in-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是在 **K** 个整数的所有子序列中找到不同元素的最大[个数。](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

**示例:**

> **输入:** arr[]={1，1，2，2}，K=3
> **输出:** 2
> **解释:**子序列{1，1，2}有 3 个整数，其中不同整数的个数是 2，这是最大可能。其他可能的子序列是{1，2，2}。
> 
> **输入:** arr[]={1，2，3，4}，K = 3
> T3】输出: 3

**方法:**可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决给定的问题，方法是观察所需答案是给定数组或 k 中唯一元素计数的最小值。现在，要解决这个问题，请按照以下步骤操作:

1.  创建一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) **S** ，它存储存在于[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中的不同整数。
2.  遍历数组 **arr[]** ，并将每个数字插入到集合 **S** 中。
3.  返回所需答案 **K** 的最小值和 **S** 的大小。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of maximum
// distinct elements in a subsequence
// of size K of the given array arr[]
int maxUnique(vector<int>& arr, int K)
{
    // Set data structure to
    // store the unique elements
    unordered_set<int> S;

    // Loop to traverse the given array
    for (auto x : arr) {

        // Insert into the set
        S.insert(x);
    }

    // Returning the minimum out of the two
    return min(K, (int)S.size());
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1, 2, 2 };
    int K = 3;
    cout << maxUnique(arr, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find count of maximum
// distinct elements in a subsequence
// of size K of the given array arr[]
static int maxUnique(int []arr, int K)
{

    // Set data structure to
    // store the unique elements
    HashSet<Integer> S = new HashSet<Integer>();

    // Loop to traverse the given array
    for (int x : arr) {

        // Insert into the set
        S.add(x);
    }

    // Returning the minimum out of the two
    return Math.min(K, (int)S.size());
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 1, 2, 2 };
    int K = 3;
    System.out.print(maxUnique(arr, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find count of maximum
# distinct elements in a subsequence
# of size K of the given array arr[]
def maxUnique(arr, K):

    # Set data structure to
    # store the unique elements
    S = set()

    # Loop to traverse the given array
    for x in arr:

        # Insert into the set
        S.add(x)

    # Returning the minimum out of the two
    return min(K, len(S))

# Driver Code
arr = [1, 1, 2, 2]
K = 3
print(maxUnique(arr, K))

# This code is contributed by gfgking
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to find count of maximum
// distinct elements in a subsequence
// of size K of the given array arr[]
static int maxUnique(int []arr, int K)
{
    // Set data structure to
    // store the unique elements
    HashSet<int> S = new HashSet<int>();

    // Loop to traverse the given array
    foreach (int x in arr) {

        // Insert into the set
        S.Add(x);
    }

    // Returning the minimum out of the two
    return Math.Min(K, (int)S.Count);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 1, 2, 2 };
    int K = 3;
    Console.Write(maxUnique(arr, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

     // JavaScript Program to implement
     // the above approach

     // Function to find count of maximum
     // distinct elements in a subsequence
     // of size K of the given array arr[]
     function maxUnique(arr, K)
     {

         // Set data structure to
         // store the unique elements
         let S = new Set();

         // Loop to traverse the given array
         for (let x of arr) {

             // Insert into the set
             S.add(x);
         }

         // Returning the minimum out of the two
         return Math.min(K, S.size);
     }

     // Driver Code
     let arr = [1, 1, 2, 2];
     let K = 3;
     document.write(maxUnique(arr, K));

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)