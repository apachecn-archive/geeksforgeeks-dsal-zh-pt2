# 最长递增绝对偶数子序列的长度

> 原文:[https://www . geesforgeks . org/最长递增绝对偶数子序列的长度/](https://www.geeksforgeeks.org/length-of-longest-increasing-absolute-even-subsequence/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到最长递增绝对偶子序列的长度。

> **递增的绝对偶子序列**是相邻偶对之间具有绝对差的数组元素的递增子序列。

**示例:**

> **输入:** arr[] = {10，22，9，33，21，50，41，60}
> **输出:** 4
> **解释:**最长递增的绝对偶子序列是{10，22，50，60}。因此，所需长度为 4。
> 
> **输入:** arr[] = {11，-22，43，-54，66，5}
> **输出:** 3
> **解释:**
> 最长递增的绝对偶子序列是 3，即{-22，-54，66}。因此，所需长度为 4。

**朴素方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，对于每个子序列，检查子序列是否在增加，相邻元素之间的绝对差是否为偶数。打印最长的子序列的长度。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路类似于寻找[最长的递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)。但是唯一需要改变的条件是检查子序列的两个相邻元素之间的绝对差是否相等。按照以下步骤解决问题:

1.  初始化一个辅助数组 **dp[]** ，其中最初都是 **1** 。
2.  [在范围**【0，N】**内，使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，并对每个索引执行以下操作:
    *   使用变量 **j** 在范围**【0，i)** 内迭代，并检查以下三个条件:
        1.  如果绝对值**arr【I】**>**arr【j】**。
        2.  如果 **arr[i]** 和 **arr[j]** 都是偶数或者不是。
        3.  假如 **dp[i]** < **dp[j] + 1** 。
    *   如果任何指标 **j** 满足上述三个条件，则更新 **dp[i] = dp[j] + 1** 。
3.  打印数组 **dp[]** 的[最大元素作为所需结果。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++14

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest
// increasing absolute even subsequence
void EvenLIS(int arr[], int n)
{

    // Stores length of
    // required subsequence
    int lis[n];
    for(int i = 0; i < n; i++)
        lis[i] = 1;

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // Traverse prefix of current
        // array element
        for(int j = 0; j < i; j++)
        {

            // Check if the subsequence is
            // LIS and have even absolute
            // difference of adjacent pairs
            if (abs(arr[i]) > abs(arr[j]) &&
                abs(arr[i]) % 2 == 0 &&
                abs(arr[j]) % 2 == 0 &&
                    lis[i] < lis[j] + 1)

                // Update lis[]
                lis[i] = lis[j] + 1;
        }
    }

    // Stores maximum length
    int maxlen = 0;

    // Find the length of longest
    // absolute even subsequence
    for(int i = 0; i < n; i++)
        maxlen = max(maxlen, lis[i]);

    // Return the maximum length of
    // absolute even subsequence
    cout << maxlen << endl;
}

// Driver code
int main()
{

    // Given array arr[] and brr[]
    int arr[] = { 11, -22, 43, -54, 66, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    EvenLIS(arr, N);
}

// This code is contributed by code_hunt
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to find the longest
// increasing absolute even subsequence
static void EvenLIS(int arr[])
{

    // Length of arr
    int n = arr.length;

    // Stores length of
    // required subsequence
    int lis[] = new int[n];
    Arrays.fill(lis, 1);

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // Traverse prefix of current
        // array element
        for(int j = 0; j < i; j++)
        {

            // Check if the subsequence is
            // LIS and have even absolute
            // difference of adjacent pairs
            if (Math.abs(arr[i]) > Math.abs(arr[j]) &&
                Math.abs(arr[i]) % 2 == 0 &&
                Math.abs(arr[j]) % 2 == 0 &&
                          lis[i] < lis[j] + 1)

                // Update lis[]
                lis[i] = lis[j] + 1;
        }
    }

    // Stores maximum length
    int maxlen = 0;

    // Find the length of longest
    // absolute even subsequence
    for(int i = 0; i < n; i++)
        maxlen = Math.max(maxlen, lis[i]);

    // Return the maximum length of
    // absolute even subsequence
    System.out.println(maxlen);
}

// Driver code
public static void main(String args[])
{

    // Given array arr[] and brr[]
    int arr[] = { 11, -22, 43, -54, 66, 5 };

    int N = arr.length;

    // Function call
    EvenLIS(arr);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest
# increasing absolute even subsequence
def EvenLIS(arr):

    # Length of arr
    n = len(arr)

    # Stores length of
    # required subsequence
    lis = [1]*n

    # Traverse the array
    for i in range(1, n):

        # Traverse prefix of current
        # array element
        for j in range(0, i):

            # Check if the subsequence is
            # LIS and have even absolute
            # difference of adjacent pairs

            if abs(arr[i]) > abs(arr[j]) \
            and abs(arr[i] % 2) == 0 \
            and abs(arr[j] % 2) == 0 \
            and lis[i] < lis[j]+1:

                # Update lis[]
                lis[i] = lis[j]+1

    # Stores maximum length
    maxlen = 0

    # Find the length of longest
    # absolute even subsequence
    for i in range(n):
        maxlen = max(maxlen, lis[i])

    # Return the maximum length of
    # absolute even subsequence
    print(maxlen)

# Driver Code

# Given arr[]
arr = [11, -22, 43, -54, 66, 5]

# Function Call
EvenLIS(arr)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the longest
// increasing absolute even subsequence
static void EvenLIS(int []arr)
{

    // Length of arr
    int n = arr.Length;

    // Stores length of
    // required subsequence
    int []lis = new int[n];
    for(int i = 0; i < n; i++)
        lis[i] = 1;

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // Traverse prefix of current
        // array element
        for(int j = 0; j < i; j++)
        {

            // Check if the subsequence is
            // LIS and have even absolute
            // difference of adjacent pairs
            if (Math.Abs(arr[i]) > Math.Abs(arr[j]) &&
                Math.Abs(arr[i]) % 2 == 0 &&
                Math.Abs(arr[j]) % 2 == 0 &&
                         lis[i] < lis[j] + 1)

                // Update lis[]
                lis[i] = lis[j] + 1;
        }
    }

    // Stores maximum length
    int maxlen = 0;

    // Find the length of longest
    // absolute even subsequence
    for(int i = 0; i < n; i++)
        maxlen = Math.Max(maxlen, lis[i]);

    // Return the maximum length of
    // absolute even subsequence
    Console.WriteLine(maxlen);
}

// Driver code
public static void Main(String []args)
{
    // Given array []arr and brr[]
    int []arr = { 11, -22, 43, -54, 66, 5 };

    int N = arr.Length;

    // Function call
    EvenLIS(arr);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the longest
// increasing absolute even subsequence
function EvenLIS(arr)
{

    // Length of arr
    let n = arr.length;

    // Stores length of
    // required subsequence
    let lis = new Array(n).fill(1);

    // Traverse the array
    for(let i = 1; i < n; i++)
    {

        // Traverse prefix of current
        // array element
        for(let j = 0; j < i; j++)
        {

            // Check if the subsequence is
            // LIS and have even absolute
            // difference of adjacent pairs
            if (Math.abs(arr[i]) > Math.abs(arr[j]) &&
                Math.abs(arr[i]) % 2 == 0 &&
                Math.abs(arr[j]) % 2 == 0 &&
                          lis[i] < lis[j] + 1)

                // Update lis[]
                lis[i] = lis[j] + 1;
        }
    }

    // Stores maximum length
    let maxlen = 0;

    // Find the length of longest
    // absolute even subsequence
    for(let i = 0; i < n; i++)
        maxlen = Math.max(maxlen, lis[i]);

    // Return the maximum length of
    // absolute even subsequence
    document.write(maxlen);
}

// Driver Code

    // Given array arr[] and brr[]
    let arrr = [ 11, -22, 43, -54, 66, 5 ];

    let N = arrr.length;

    // Function call
    EvenLIS(arrr);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*