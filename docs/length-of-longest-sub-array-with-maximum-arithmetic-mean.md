# 算术平均值最大的最长子阵列长度。

> 原文:[https://www . geeksforgeeks . org/最长算术平均值子数组长度/](https://www.geeksforgeeks.org/length-of-longest-sub-array-with-maximum-arithmetic-mean/)

给定一个 n 元素数组，找到算术平均值最大的最长子数组。子数组的长度必须大于 1，并且平均值只能作为整数计算。
**例:**

```
Input : arr[] = {3, 2, 1, 2}
Output : 2
sub-array 3, 2 has greatest arithmetic mean

Input :arr[] = {3, 3, 3, 2}
Output : 3
```

其思想是首先从数组中找到两个连续元素的最大平均值。再次迭代数组，并尝试找到最长的序列，其中每个元素必须大于或等于计算出的最大平均值。
上述方法之所以有效，是因为以下几点:

*   最小可能序列长度为 2，因此两个连续元素的最大平均值将始终是结果的一部分。
*   任何等于或大于计算平均值的元素都可能是最长序列的一部分。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum distance
// between unequal elements
int longestSubarray(int arr[], int n)
{

    // Calculate maxMean
    int maxMean = 0;
    for (int i = 1; i < n; i++)
        maxMean = max(maxMean,
                      (arr[i] + arr[i - 1]) / 2);

    // Iterate over array and calculate largest subarray
    // with all elements greater or equal to maxMean
    int ans = 0;
    int subarrayLength = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] >= maxMean)
            ans = max(ans, ++subarrayLength);
        else
            subarrayLength = 0;

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 4, 3, 3, 2, 1, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestSubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

// Function to find maximum distance
// between unequal elements
static int longestSubarray(int arr[], int n)
{

    // Calculate maxMean
    int maxMean = 0;
    for (int i = 1; i < n; i++)
        maxMean = Math.max(maxMean,
                    (arr[i] + arr[i - 1]) / 2);

    // Iterate over array and calculate largest subarray
    // with all elements greater or equal to maxMean
    int ans = 0;
    int subarrayLength = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] >= maxMean)
            ans = Math.max(ans, ++subarrayLength);
        else
            subarrayLength = 0;

    return ans;
}

// Driver code
public static void main (String[] args)
{

    int arr[] = { 4, 3, 3, 2, 1, 4 };
    int n = arr.length;
    System.out.println (longestSubarray(arr, n));
}
}

// This code is contributed by ajit_00023
```

## 蟒蛇 3

```

# Python implementation of the above approach

# Function to find maximum distance
# between unequal elements
def longestSubarray(arr, n):

    # Calculate maxMean
    maxMean = 0;
    for i in range(1, n):
        maxMean = max(maxMean,
                    (arr[i] + arr[i - 1]) // 2);

    # Iterate over array and calculate largest subarray
    # with all elements greater or equal to maxMean
    ans = 0;
    subarrayLength = 0;
    for i in range(n):
        if (arr[i] >= maxMean):
            subarrayLength += 1;
            ans = max(ans, subarrayLength);
        else:
            subarrayLength = 0;

    return ans;

# Driver code
arr = [ 4, 3, 3, 2, 1, 4 ];

n = len(arr);

print(longestSubarray(arr, n));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find maximum distance
    // between unequal elements
    static int longestSubarray(int []arr,
                               int n)
    {

        // Calculate maxMean
        int maxMean = 0;
        for (int i = 1; i < n; i++)
            maxMean = Math.Max(maxMean,
                              (arr[i] + arr[i - 1]) / 2);

        // Iterate over array and calculate
        // largest subarray with all elements
        // greater or equal to maxMean
        int ans = 0;
        int subarrayLength = 0;
        for (int i = 0; i < n; i++)
            if (arr[i] >= maxMean)
                ans = Math.Max(ans, ++subarrayLength);
            else
                subarrayLength = 0;

        return ans;
    }

    // Driver code
    public static void Main ()
    {

        int []arr = { 4, 3, 3, 2, 1, 4 };
        int n = arr.Length;
        Console.WriteLine(longestSubarray(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find maximum distance
// between unequal elements
function longestSubarray(arr, n)
{

    // Calculate maxMean
    var maxMean = 0;
    for (var i = 1; i < n; i++)
        maxMean = Math.max(maxMean,
                      parseInt((arr[i] + arr[i - 1]) / 2));

    // Iterate over array and calculate largest subarray
    // with all elements greater or equal to maxMean
    var ans = 0;
    var subarrayLength = 0;
    for (var i = 0; i < n; i++)
        if (arr[i] >= maxMean)
            ans = Math.max(ans, ++subarrayLength);
        else
            subarrayLength = 0;

    return ans;
}

// Driver code
var arr = [ 4, 3, 3, 2, 1, 4 ];
var n = arr.length;
document.write( longestSubarray(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)