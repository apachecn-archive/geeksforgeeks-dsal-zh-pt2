# 最小化数组中严格递增的子序列的数量|集合 2

> 原文:[https://www . geeksforgeeks . org/最小化数组集 2 中严格递增子序列的数量/](https://www.geeksforgeeks.org/minimize-the-number-of-strictly-increasing-subsequences-in-an-array-set-2/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是打印数组中严格递增的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)的最小可能计数。
***注意:**可以互换数组元素对。*

**示例:**

> **输入:** arr[] = {2，1，2，1，4，3}
> **输出:** 2
> **解释:**对数组进行排序会将数组修改为 arr[] = {1，1，2，2，3，4}。两个可能的递增子序列是{1，2，3}和{1，2，4}，这涉及所有数组元素。
> 
> **输入:** arr[] = {3，3，3 }
> T3】输出: 3

[**多集**](https://www.geeksforgeeks.org/multiset-in-cpp-stl/) **基于方法:**参考[之前的](https://www.geeksforgeeks.org/minimum-number-of-increasing-subsequences/)帖子解决问题使用[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)找到数组中[最长的递减子序列。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/longest-decreasing-subsequence/)

**空间优化方法:**最优思想基于以下观察:

> 具有相同值的两个元素不能包含在一个子序列中，因为它们不会形成严格递增的子序列。
> 因此，对于每个不同的数组元素，计算其频率，比如 **y** 。因此，至少需要 **y** 子序列。
> 因此，出现最多的数组元素的频率是必需的答案。

按照以下步骤解决问题:

1.  初始化一个变量，比如**计数**，来存储严格递增子序列的最终计数。
2.  [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr【】并执行以下观察:**
    *   初始化两个变量，比如 **X** ，存储当前数组元素， **freqX** 存储当前数组元素的频率。
    *   在 **freqX** 中查找并存储当前元素的所有出现。
    *   如果当前元素的频率大于之前的计数，则更新**计数**。
3.  打印**计数**的值。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of strictly
// increasing subsequences in an array
int minimumIncreasingSubsequences(
    int arr[], int N)
{
    // Sort the array
    sort(arr, arr + N);

    // Stores final count
    // of subsequences
    int count = 0;
    int i = 0;

    // Traverse the array
    while (i < N) {

        // Stores current element
        int x = arr[i];

        // Stores frequency of
        // the current element
        int freqX = 0;

        // Count frequency of
        // the current element
        while (i < N && arr[i] == x) {
            freqX++;
            i++;
        }

        // If current element frequency
        // is greater than count
        count = max(count, freqX);
    }

    // Print the final count
    cout << count;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 1, 2, 1, 4, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to find
    // the number of strictly
    // increasing subsequences
    minimumIncreasingSubsequences(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find the number of strictly
// increasing subsequences in an array
static void minimumIncreasingSubsequences(
    int arr[], int N)
{

    // Sort the array
    Arrays.sort(arr);

    // Stores final count
    // of subsequences
    int count = 0;
    int i = 0;

    // Traverse the array
    while (i < N)
    {

        // Stores current element
        int x = arr[i];

        // Stores frequency of
        // the current element
        int freqX = 0;

        // Count frequency of
        // the current element
        while (i < N && arr[i] == x)
        {
            freqX++;
            i++;
        }

        // If current element frequency
        // is greater than count
        count = Math.max(count, freqX);
    }

    // Print the final count
    System.out.print(count);
}

// Driver Code
public static void main(String args[])
{
    // Given array
    int arr[] = { 2, 1, 2, 1, 4, 3 };

    // Size of the array
    int N = arr.length;

    // Function call to find
    // the number of strictly
    // increasing subsequences
    minimumIncreasingSubsequences(arr, N);
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the number of strictly
# increasing subsequences in an array
def minimumIncreasingSubsequences(arr, N) :

    # Sort the array
    arr.sort()

    # Stores final count
    # of subsequences
    count = 0
    i = 0

    # Traverse the array
    while (i < N) :

        # Stores current element
        x = arr[i]

        # Stores frequency of
        # the current element
        freqX = 0

        # Count frequency of
        # the current element
        while (i < N and arr[i] == x) :
            freqX += 1
            i += 1

        # If current element frequency
        # is greater than count
        count = max(count, freqX)

    # Print the final count
    print(count)

# Given array
arr = [ 2, 1, 2, 1, 4, 3 ]

# Size of the array
N = len(arr)

# Function call to find
# the number of strictly
# increasing subsequences
minimumIncreasingSubsequences(arr, N)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to implement
// the above approach
using System;

public class GFG
{

// Function to find the number of strictly
// increasing subsequences in an array
static void minimumIncreasingSubsequences(
    int []arr, int N)
{

    // Sort the array
    Array.Sort(arr);

    // Stores readonly count
    // of subsequences
    int count = 0;
    int i = 0;

    // Traverse the array
    while (i < N)
    {

        // Stores current element
        int x = arr[i];

        // Stores frequency of
        // the current element
        int freqX = 0;

        // Count frequency of
        // the current element
        while (i < N && arr[i] == x)
        {
            freqX++;
            i++;
        }

        // If current element frequency
        // is greater than count
        count = Math.Max(count, freqX);
    }

    // Print the readonly count
    Console.Write(count);
}

// Driver Code
public static void Main(String []args)
{

    // Given array
    int []arr = { 2, 1, 2, 1, 4, 3 };

    // Size of the array
    int N = arr.Length;

    // Function call to find
    // the number of strictly
    // increasing subsequences
    minimumIncreasingSubsequences(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to find the number of strictly
    // increasing subsequences in an array
    function minimumIncreasingSubsequences(arr, N)
    {

        // Sort the array
        arr.sort(function(a, b){return a - b});

        // Stores readonly count
        // of subsequences
        let count = 0;
        let i = 0;

        // Traverse the array
        while (i < N)
        {

            // Stores current element
            let x = arr[i];

            // Stores frequency of
            // the current element
            let freqX = 0;

            // Count frequency of
            // the current element
            while (i < N && arr[i] == x)
            {
                freqX++;
                i++;
            }

            // If current element frequency
            // is greater than count
            count = Math.max(count, freqX);
        }

        // Print the readonly count
        document.write(count);
    }

    // Given array
    let arr = [ 2, 1, 2, 1, 4, 3 ];

    // Size of the array
    let N = arr.length;

    // Function call to find
    // the number of strictly
    // increasing subsequences
    minimumIncreasingSubsequences(arr, N);

  // This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*