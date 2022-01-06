# 一对或一个元素平方乘积的元素计数

> 原文:[https://www . geeksforgeeks . org/元素计数-一对或一个元素平方的乘积/](https://www.geeksforgeeks.org/count-of-elements-which-is-product-of-a-pair-or-an-element-square/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算数组元素的个数，数组元素可以表示为两个不同数组元素的乘积，也可以表示为任意数组元素的平方。

**示例:**

> **输入:** N = 5，arr[] = {3，2，6，18，4}
> **输出:** 3
> **解释:**
> 给定数组 6，18，4 中的 3 个元素可以分别表示为{2 * 3，6 * 3，2 * 2}。
> 
> **输入:** N = 6，arr[] = {5，15，3，7，10，17}
> **输出:** 1
> **说明:**
> 只有 15 可以表示为 5 * 3。

**天真方法:**
最简单的方法是遍历范围**【0，N-1】**内的数组，对于给定范围内具有索引值 **i** 的每个数，在同一个数组上运行嵌套循环，找出乘积为 arr[i]的两个值。如果找到一对数字，打印 1，否则根据相应的索引打印 0。

***时间复杂度:** O(N <sup>3</sup> )*

**高效方法:**
要解决这个问题，我们需要找到每个元素的所有因子，对于每个元素，检查数组中是否存在该元素的任何一对因子。按照以下步骤解决问题:

1.  [按递增顺序对给定数组进行排序](https://www.geeksforgeeks.org/sort-c-stl/)。
2.  现在，遍历数组，对于每个元素，[找到该元素的所有因子对](https://www.geeksforgeeks.org/program-to-print-factors-of-a-number-in-pairs/)，并使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)检查数组中是否存在任何因子对。
3.  对数组进行排序可以让我们在搜索因子的同时进行二分搜索法运算，从而将计算复杂度降低到 *O(logN)* 。
4.  如果找到任何这样的配对，增加**计数**并移动到下一个元素，重复相同的过程。
5.  打印数组中所有此类数字的最终**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Stores all factors a number
vector<int> v[100000];

// Function to calculate and
// store in a vector
void div(int n)
{
    for (int i = 2; i <= sqrt(n);
         i++) {

        if (n % i == 0) {
            v[n].push_back(i);
        }
    }
}

// Function to return the count of
// array elements which are a
// product of two array elements
int prodof2elements(int arr[], int n)
{
    int arr2[n];

    // Copy elements into a
    // a duplicate array
    for (int i = 0; i < n; i++) {
        arr2[i] = arr[i];
    }

    // Sort the duplicate array
    sort(arr2, arr2 + n);

    // Store the count of elements
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // If the factors are not
        // calculated already
        if (v[arr[i]].size() == 0)
            div(arr[i]);

        // Traverse its factors
        for (auto j : v[arr[i]]) {

            // If a pair of
            // factors is found
            if (binary_search(
                    arr2, arr2 + n, j)
                and binary_search(
                        arr2, arr2 + n,
                        arr[i] / j)) {
                ans++;
                break;
            }
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 8, 4, 32, 18 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << prodof2elements(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.util.*;
class GFG{

// Stores all factors a number
static Vector<Integer>[] v =
       new Vector[100000];

// Function to calculate and
// store in a vector
static void div(int n)
{
  for (int i = 2;
           i <= Math.sqrt(n); i++)
  {
    if (n % i == 0)
    {
      v[n].add(i);
    }
  }
}

// Function to return the count of
// array elements which are a
// product of two array elements
static int prodof2elements(int arr[],
                           int n)
{
  int []arr2 = new int[n];

  // Copy elements into a
  // a duplicate array
  for (int i = 0; i < n; i++)
  {
    arr2[i] = arr[i];
  }

  // Sort the duplicate
  // array
  Arrays.sort(arr2);

  // Store the count
  // of elements
  int ans = 0;

  for (int i = 0; i < n; i++)
  {
    // If the factors are not
    // calculated already
    if (v[arr[i]].size() == 0)
      div(arr[i]);

    // Traverse its factors
    for (int j : v[arr[i]])
    {
      // If a pair of
      // factors is found
      if (Arrays.binarySearch(arr2, j) >= 0 &&
          Arrays.binarySearch(arr2,
          (int)arr[i] / j) >= 0)
      {
        ans++;
        break;
      }
    }
  }

  return ans;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {2, 1, 8, 4, 32, 18};
  int N = arr.length;

  for (int i = 0; i < v.length; i++)
    v[i] = new Vector<Integer>();

  System.out.print(prodof2elements(arr, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach
import math

# Stores all factors a number
v = [[] for i in range(100000)]

# Function to calculate and
# store in a vector
def div(n):

    global v

    for i in range(2, int(math.sqrt(n)) + 1):
        if (n % i == 0):
            v[n].append(i)

# Function to return the count of
# array elements which are a
# product of two array elements
def prodof2elements(arr, n):

    # Copy elements into a
    # a duplicate array
    arr2 = arr.copy()

    # Sort the duplicate array
    arr2.sort()

    # Store the count of elements
    ans = 0

    for i in range(n):

        # If the factors are not
        # calculated already
        if (len(v[arr[i]]) == 0):
            div(arr[i])

        # Traverse its factors
        for j in v[arr[i]]:

            # If a pair of
            # factors is found
            if j in arr2:
                if int(arr[i] / j) in arr2:
                    ans += 1
                    break

    return ans

# Driver Code
arr = [ 2, 1, 8, 4, 32, 18 ]
N = len(arr)

print(prodof2elements(arr, N))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# Program to implement the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Stores all factors a number
static List<int>[] v =
       new List<int>[100000];

// Function to calculate and
// store in a vector
static void div(int n)
{
  for (int i = 2;
           i <= Math.Sqrt(n); i++)
  {
    if (n % i == 0)
    {
      v[n].Add(i);
    }
  }
}

// Function to return the count of
// array elements which are a
// product of two array elements
static int prodof2elements(int []arr,
                           int n)
{
  int []arr2 = new int[n];

  // Copy elements into a
  // a duplicate array
  for (int i = 0; i < n; i++)
  {
    arr2[i] = arr[i];
  }

  // Sort the duplicate
  // array
  Array.Sort(arr2);

  // Store the count
  // of elements
  int ans = 0;

  for (int i = 0; i < n; i++)
  {
    // If the factors are not
    // calculated already
    if (v[arr[i]].Count == 0)
      div(arr[i]);

    // Traverse its factors
    foreach (int j in v[arr[i]])
    {
      // If a pair of
      // factors is found
      if (Array.BinarySearch(arr2, j) >= 0 &&
          Array.BinarySearch(arr2,
          (int)arr[i] / j) >= 0)
      {
        ans++;
        break;
      }
    }
  }

  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {2, 1, 8, 4, 32, 18};
  int N = arr.Length;

  for (int i = 0; i < v.Length; i++)
    v[i] = new List<int>();

  Console.Write(prodof2elements(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
3
```

**时间复杂度:***O(N<sup>3/2</sup>* log N)*
**辅助空间:** *O(N)*