# 给定 OR 值的最长子序列:O(N)趋近

> 原文:[https://www . geesforgeks . org/最长子序列-具有给定或值的方法/](https://www.geeksforgeeks.org/longest-sub-sequence-with-a-given-or-value-on-approach/)

给定一个数组 **arr[]** ，任务是找到给定 OR 值 **M** 的最长子序列。如果没有这样的子序列，则打印 **0** 。
**举例:**

> **输入:** arr[] = {3，7，2，3}，M = 3
> **输出:** 3
> {3，2，3}是所需的子序列
> 3 | 2 | 3 = 3
> **输入:** arr[] = {2，2}，M = 3
> **输出:** 0

**天真方法:**解决这个问题的简单方法是生成所有可能的子序列，然后用所需的 OR 值找到其中最大的一个。
**有效方法:**一个关键的观察是，当所需子序列中的所有数字与 **M** 进行“或”运算时，它们应该产生值 **M** 。所以要过滤掉所有这样的元素，它们的或与 **M** 等于 **M** 。
现在，任务是在这个过滤的子集中找到最长的子序列。很明显，所有这些数字都将被“或”在一起。如果这个或的结果是 **M** ，那么答案将等于这个过滤集的大小。否则答案为 **0** 。这是因为“或”只设置未设置的位。因此，集合中的数字越大，它就越优化。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required length
int findLen(int* arr, int n, int m)
{
    // To store the filtered numbers
    vector<int> filter;

    // Filtering the numbers
    for (int i = 0; i < n; i++)
        if ((arr[i] | m) == m)
            filter.push_back(arr[i]);

    // If there are no elements to check
    if (filter.size() == 0)
        return 0;

    // Find the OR of all the
    // filtered elements
    int c_or = filter[0];
    for (int i = 1; i < filter.size(); i++)
        c_or |= filter[i];

    // Check if the OR is equal to m
    if (c_or == m)
        return filter.size();

    return 0;
}

// Driver code
int main()
{
    int arr[] = { 7, 3, 3, 1, 3 };
    int n = sizeof(arr) / sizeof(int);
    int m = 3;

    cout << findLen(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the required length
static int findLen(int arr[], int n, int m)
{
    // To store the filtered numbers
    Vector<Integer> filter = new Vector<Integer>();

    // Filtering the numbers
    for (int i = 0; i < n; i++)
        if ((arr[i] | m) == m)
            filter.add(arr[i]);

    // If there are no elements to check
    if (filter.size() == 0)
        return 0;

    // Find the OR of all the
    // filtered elements
    int c_or = filter.get(0);
    for (int i = 1; i < filter.size(); i++)
        c_or |= filter.get(i);

    // Check if the OR is equal to m
    if (c_or == m)
        return filter.size();

    return 0;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 7, 3, 3, 1, 3 };
    int n = arr.length;
    int m = 3;

    System.out.print(findLen(arr, n, m));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required length
def findLen(arr, n, m) :

    # To store the filtered numbers
    filter = [];

    # Filtering the numbers
    for i in range(n) :
        if ((arr[i] | m) == m) :
            filter.append(arr[i]);

    # If there are no elements to check
    if (len(filter) == 0) :
        return 0;

    # Find the OR of all the
    # filtered elements
    c_or = filter[0];
    for i in range(1, len(filter)) :
        c_or |= filter[i];

    # Check if the OR is equal to m
    if (c_or == m) :
        return len(filter);

# Driver code
if __name__ == "__main__" :

    arr = [ 7, 3, 3, 1, 3 ];
    n = len(arr);
    m = 3;

    print(findLen(arr, n, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

using System.Collections.Generic;

class GFG
{

// Function to return the required length
static int findLen(int [] arr, int n, int m)
{
    // To store the filtered numbers
    List<int> filter = new List<int>();

    // Filtering the numbers
    for (int i = 0; i < n; i++)
        if ((arr[i] | m) == m)
            filter.Add(arr[i]);

    // If there are no elements to check
    if (filter.Count == 0)
        return 0;

    // Find the OR of all the
    // filtered elements
    int c_or = filter[0];
    for (int i = 1; i < filter.Count; i++)
        c_or |= filter[i];

    // Check if the OR is equal to m
    if (c_or == m)
        return filter.Count;

    return 0;
}

// Driver code
public static void Main()
{
    int []arr = { 7, 3, 3, 1, 3 };
    int n = arr.Length;
    int m = 3;

    Console.Write(findLen(arr, n, m));
}
}

// This code is contributed by Mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required length
function findLen(arr, n, m)
{
    // To store the filtered numbers
    var filter = [];

    // Filtering the numbers
    for (var i = 0; i < n; i++)
        if ((arr[i] | m) == m)
            filter.push(arr[i]);

    // If there are no elements to check
    if (filter.length == 0)
        return 0;

    // Find the OR of all the
    // filtered elements
    var c_or = filter[0];
    for (var i = 1; i < filter.length; i++)
        c_or |= filter[i];

    // Check if the OR is equal to m
    if (c_or == m)
        return filter.length;

    return 0;
}

// Driver code
var arr = [7, 3, 3, 1, 3 ];
var n = arr.length;
var m = 3;
document.write( findLen(arr, n, m));

</script>
```

**Output:** 

```
4
```

时间复杂度:0(n)

辅助空间:O(n)