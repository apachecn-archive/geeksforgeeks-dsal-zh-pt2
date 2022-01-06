# 正负元素个数相等的最大和子集

> 原文:[https://www . geesforgeks . org/最大和子集具有相等数量的正负元素/](https://www.geeksforgeeks.org/maximum-sum-subset-having-equal-number-of-positive-and-negative-elements/)

给定一个数组 **arr[]** ，任务是找到包含相同数量的正负元素的最大和子集。

**示例:**

> **输入:** arr[] = {1，-2，3，4，-5，8}
> **输出:** 6
> **解释:**
> 正负元素个数相等的最大和子集{8，-2}
> 
> **输入:** arr[] = {-1，-2，-3，-4，-5}
> **输出:** 0
> **解释:**
> 由于数组中没有正元素，最大和子集将为{}

**方法:**想法是将正负元素存储到两个不同的数组中，然后[按照递增的顺序对它们进行单独排序。然后使用](https://www.geeksforgeeks.org/merge-sort/)[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)从每个数组的最高元素开始，包括那些和大于 0 的对。否则，如果该对的和小于 0，那么停止寻找更多的元素，因为在左对中没有这样的和大于 0 的对。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum sum subset having equal
// number of positive and negative
// elements in the subset

#include <bits/stdc++.h>

using namespace std;

// Function to find maximum sum
// subset with equal number of
// positive and negative elements
int findMaxSum(int* arr, int n)
{
    vector<int> a;
    vector<int> b;

    // Loop to store the positive
    // and negative elements in
    // two different array
    for (int i = 0; i < n; i++) {
        if (arr[i] > 0) {
            a.push_back(arr[i]);
        }
        else if (arr[i] < 0) {
            b.push_back(arr[i]);
        }
    }

    // Sort both the array
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());

    // Pointers starting from
    // the highest elements
    int p = a.size() - 1;
    int q = b.size() - 1;
    int s = 0;

    // Find pairs having sum
    // greater than zero
    while (p >= 0 && q >= 0) {
        if (a[p] + b[q] > 0) {
            s = s + a[p] + b[q];
        }
        else {
            break;
        }
        p = p - 1;
        q = q - 1;
    }
    return s;
}

// Driver code
int main()
{
    int arr1[] = { 1, -2, 3, 4, -5, 8 };
    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    cout << findMaxSum(arr1, n1) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum subset having equal
// number of positive and negative
// elements in the subset
import java.util.*;

class GFG{

// Function to find maximum sum
// subset with equal number of
// positive and negative elements
static int findMaxSum(int []arr, int n)
{
    Vector<Integer> a = new Vector<Integer>();
    Vector<Integer> b = new Vector<Integer>();

    // Loop to store the positive
    // and negative elements in
    // two different array
    for(int i = 0; i < n; i++)
    {
       if (arr[i] > 0)
       {
           a.add(arr[i]);
       }
       else if (arr[i] < 0)
       {
           b.add(arr[i]);
       }
    }

    // Sort both the array
    Collections.sort(a);
    Collections.sort(b);

    // Pointers starting from
    // the highest elements
    int p = a.size() - 1;
    int q = b.size() - 1;
    int s = 0;

    // Find pairs having sum
    // greater than zero
    while (p >= 0 && q >= 0)
    {
        if (a.get(p) + b.get(q) > 0)
        {
            s = s + a.get(p) + b.get(q);
        }
        else
        {
            break;
        }
        p = p - 1;
        q = q - 1;
    }

    return s;
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 1, -2, 3, 4, -5, 8 };
    int n1 = arr1.length;

    System.out.print(
           findMaxSum(arr1, n1) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum sum subset having equal
# number of positive and negative
# elements in the subset

# Function to find maximum sum
# subset with equal number of
# positive and negative elements
def findMaxSum(arr, n):

    a = []
    b = []

    # Loop to store the positive
    # and negative elements in
    # two different array
    for i in range(n):
        if (arr[i] > 0):
            a.append(arr[i])

        elif (arr[i] < 0):
            b.append(arr[i])

    # Sort both the array
    a.sort()
    b.sort()

    # Pointers starting from
    # the highest elements
    p = len(a) - 1
    q = len(b) - 1
    s = 0

    # Find pairs having sum
    # greater than zero
    while (p >= 0 and q >= 0):
        if (a[p] + b[q] > 0):
            s = s + a[p] + b[q]

        else:
            break
        p = p - 1
        q = q - 1

    return s

# Driver code
arr1 = [ 1, -2, 3, 4, -5, 8 ]
n1 = len(arr1)

print(findMaxSum(arr1, n1))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find the
// maximum sum subset having equal
// number of positive and negative
// elements in the subset
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum sum
// subset with equal number of
// positive and negative elements
static int findMaxSum(int []arr, int n)
{

    List<int> a = new List<int>();
    List<int> b = new List<int>();

    // Loop to store the positive
    // and negative elements in
    // two different array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] > 0)
        {
            a.Add(arr[i]);
        }
        else if (arr[i] < 0)
        {
            b.Add(arr[i]);
        }
    }

    // Sort both the array
    a.Sort();
    b.Sort();

    // Pointers starting from
    // the highest elements
    int p = a.Count - 1;
    int q = b.Count - 1;
    int s = 0;

    // Find pairs having sum
    // greater than zero
    while (p >= 0 && q >= 0)
    {
        if (a[p] + b[q] > 0)
        {
            s = s + a[p] + b[q];
        }
        else
        {
            break;
        }

        p = p - 1;
        q = q - 1;
    }
    return s;
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = { 1, -2, 3, 4, -5, 8 };
    int n1 = arr1.Length;

    Console.Write(findMaxSum(arr1, n1) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// maximum sum subset having equal
// number of positive and negative
// elements in the subset

// Function to find maximum sum
// subset with equal number of
// positive and negative elements
function findMaxSum(arr, n)
{
    var a = [];
    var b = [];

    // Loop to store the positive
    // and negative elements in
    // two different array
    for(var i = 0; i < n; i++)
    {
        if (arr[i] > 0)
        {
            a.push(arr[i]);
        }
        else if (arr[i] < 0)
        {
            b.push(arr[i]);
        }
    }

    // Sort both the array
    a.sort((a, b) => a - b)
    b.sort((a, b) => a - b)

    // Pointers starting from
    // the highest elements
    var p = a.length - 1;
    var q = b.length - 1;
    var s = 0;

    // Find pairs having sum
    // greater than zero
    while (p >= 0 && q >= 0)
    {
        if (a[p] + b[q] > 0)
        {
            s = s + a[p] + b[q];
        }
        else
        {
            break;
        }
        p = p - 1;
        q = q - 1;
    }
    return s;
}

// Driver code
var arr1 = [ 1, -2, 3, 4, -5, 8 ];
var n1 = arr1.length;

document.write( findMaxSum(arr1, n1));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
6
```

**性能分析:**

*   **时间复杂度:** O(N*logN)
*   **辅助空间:** O(N)