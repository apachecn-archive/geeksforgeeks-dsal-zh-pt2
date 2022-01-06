# 填充 N 个自然数数组中缺失的数字，使得 arr[i]不等于 i

> 原文:[https://www . geeksforgeeks . org/在 n 个自然数的数组中填充缺失的数字-这样，arri 不等于 i/](https://www.geeksforgeeks.org/fill-the-missing-numbers-in-the-array-of-n-natural-numbers-such-that-arri-not-equal-to-i/)

给定一个未排序的数组 **arr[]** ，该数组由 **N 个自然数**组成，缺失的数字为 **0** ，这样**arr【I】≠I**，任务是在不改变初始顺序的情况下找到并填充这些缺失的数字。请注意，数组只能包含一次从 1 到 N 的数字。

**示例:**

> **输入:** arr[] = {7，4，0，3，0，5，1}
> **输出:** 7 4 6 3 2 5 1
> **解释:**
> 在给定数组中，未填充的索引为 2 和 4。因此，为了满足标准 arr[i] ≠ i，可以填充的缺失数字分别是 6 和 2。
> 
> **输入:** arr[] = {2，1，0，0，0}
> **输出:** 2 1 4 5 3
> **解释:**
> 在给定的数组中，未填充的索引是 3、4 和 5。因此，为了满足标准 arr[i] ≠ i，可以填充的缺失数字分别是 4、5 和 3。

**进场:**

*   将所有未填充的索引存储在一个数组中**未填充 _ 索引[]** 。即，对于所有的 **i** 使得 **arr[i] = 0。**
*   同时存储数组中所有缺失的元素**缺失[]** 。这可以通过首先将所有元素从 **1** 插入到 **N** 然后删除所有不是 **0** 的元素来完成
*   只需迭代**未填充 _ indexes【】**数组，并开始分配存储在**missing【】**数组中的所有元素，可能从后开始取每个元素(以避免任何 **i** 得到 **arr[i] = i** )。
*   现在，最大一个索引可能获得相同的 **arr[i] = i** 。在检查其他索引应该出现在**未填充的 _ indexes【】**中之后，只需将其与任何其他元素交换即可。
*   打印新数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print array
void printArray(int[], int);

// Function to fill the position
// with arr[i] = 0
void solve(int arr[], int n)
{

    set<int> unfilled_indices;
    set<int> missing;

    // Inserting all elements in
    // missing[] set from 1 to N
    for (int i = 1; i < n; i++)
        missing.insert(i);

    for (int i = 1; i < n; i++) {

        // Inserting unfilled positions
        if (arr[i] == 0)
            unfilled_indices.insert(i);

        // Removing allocated_elements
        else {
            auto it = missing.find(arr[i]);
            missing.erase(it);
        }
    }
    auto it2 = missing.end();
    it2--;

    // Loop for filling the positions
    // with arr[i] != i
    for (auto it = unfilled_indices.begin();
         it != unfilled_indices.end();
         it++, it2--) {
        arr[*it] = *it2;
    }
    int pos = 0;

    // Checking for any arr[i] = i
    for (int i = 1; i < n; i++) {
        if (arr[i] == i) {
            pos = i;
        }
    }

    int x;

    // Finding the suitable position
    // in the array to swap with found i
    // for which arr[i] = i
    if (pos != 0) {
        for (int i = 1; i < n; i++) {
            if (pos != i) {

                // Checking if the position
                // is present in unfilled_position
                if (unfilled_indices.find(i)
                    != unfilled_indices.end()) {

                    // Swapping arr[i] & arr[pos]
                    // (arr[pos] = pos)
                    x = arr[i];
                    arr[i] = pos;
                    arr[pos] = x;
                    break;
                }
            }
        }
    }
    printArray(arr, n);
}

// Function to Print the array
void printArray(int arr[], int n)
{
    for (int i = 1; i < n; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 0, 7, 4, 0,
                  3, 0, 5, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    solve(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to fill the position
  // with arr[i] = 0
  static void solve(int arr[], int n)
  {
    Set<Integer> unfilled_indices = new HashSet<Integer>();
    Set<Integer> missing = new HashSet<Integer>();

    // Inserting all elements in
    // missing[] set from 1 to N
    for (int i = 1; i < n; i++)
    {
      missing.add(i);
    }
    for (int i = 1; i < n; i++)
    {

      // Inserting unfilled positions
      if (arr[i] == 0)
      {
        unfilled_indices.add(i);
      }

      // Removing allocated_elements
      else
      {
        missing.remove(arr[i]);
      }
    }
    int[] mi = new int[missing.size()];
    int l = 0;
    for(int x:missing)
    {
      mi[l++] = x;
    }
    int m = missing.size();

    // Loop for filling the positions
    // with arr[i] != i
    for(int it:unfilled_indices)
    {
      arr[it] = mi[m - 1];
      m--;
    }
    int pos = 0;

    // Checking for any arr[i] = i
    for (int i = 1; i < n; i++)
    {
      if (arr[i] == i)
      {
        pos = i;
      }
    }
    int x;

    // Finding the suitable position
    // in the array to swap with found i
    // for which arr[i] = i
    if (pos != 0)
    {
      for (int i = 1; i < n; i++)
      {
        if (pos != i)
        {

          // Checking if the position
          // is present in unfilled_position
          if(unfilled_indices.contains(i))
          {

            // Swapping arr[i] & arr[pos]
            // (arr[pos] = pos)
            x = arr[i];
            arr[i] = pos;
            arr[pos] = x;
            break;
          }
        }
      }
    }
    printArray(arr, n);
  }

  // Function to Print the array
  static void printArray(int arr[], int n)
  {
    for (int i = 1; i < n; i++)
    {
      System.out.print(arr[i] + " ");   
    }
  }

  // Driver Code
  public static void main (String[] args)
  {
    int[] arr = { 0, 7, 4, 0,3, 0, 5, 1 };
    int n = arr.length;
    solve(arr, n);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to fill the position
# with arr[i] = 0
def solve(arr, n):

    unfilled_indices = {}
    missing = {}

    # Inserting all elements in
    # missing[] set from 1 to N
    for i in range(n):
        missing[i] = 1

    for i in range(1, n):

        # Inserting unfilled positions
        if (arr[i] == 0):
            unfilled_indices[i] = 1

        # Removing allocated_elements
        else:
            del missing[arr[i]]

    it2 = list(missing.keys())
    m = len(it2)

    # Loop for filling the positions
    # with arr[i] != i
    for it in unfilled_indices:
        arr[it] = it2[m - 1]
        m -= 1

    pos = 0

    # Checking for any arr[i] = i
    for i in range(1, n):
        if (arr[i] == i):
            pos = i

    x  = 0

    # Finding the suitable position
    # in the array to swap with found i
    # for which arr[i] = i
    if (pos != 0):
        for i in range(1, n):
            if (pos != i):

                # Checking if the position
                # is present in unfilled_position
                if i in unfilled_indices:

                    # Swapping arr[i] & arr[pos]
                    # (arr[pos] = pos)
                    x = arr[i]
                    arr[i] = pos
                    arr[pos] = x
                    break

    printArray(arr, n)

# Function to Print the array
def printArray(arr, n):

    for i in range(1, n):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 7, 4, 0, 3, 0, 5, 1 ]

    n = len(arr)

    solve(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to fill the position
// with arr[i] = 0
static void solve(int[] arr, int n)
{
    HashSet<int> unfilled_indices = new HashSet<int>();
    HashSet<int> missing = new HashSet<int>();

    // Inserting all elements in
    // missing[] set from 1 to N
    for(int i = 1; i < n; i++)
    {
        missing.Add(i);
    }
    for(int i = 1; i < n; i++)
    {

        // Inserting unfilled positions
        if (arr[i] == 0)
        {
            unfilled_indices.Add(i);
        }

        // Removing allocated_elements
        else
        {
            missing.Remove(arr[i]);
        }
    }

    int[] mi = new int[missing.Count];
    int l = 0;

    foreach(int x in missing)
    {
        mi[l++] = x;
    }

    int m = missing.Count;

    // Loop for filling the positions
    // with arr[i] != i
    foreach(int it in unfilled_indices)
    {
        arr[it] = mi[m - 1];
        m--;
    }
    int pos = 0;

    // Checking for any arr[i] = i
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == i)
        {
            pos = i;
        }
    }

    // Finding the suitable position
    // in the array to swap with found i
    // for which arr[i] = i
    if (pos != 0)
    {
        for(int i = 1; i < n; i++)
        {
            if (pos != i)
            {

                // Checking if the position
                // is present in unfilled_position
                if (unfilled_indices.Contains(i))
                {

                    // Swapping arr[i] & arr[pos]
                    // (arr[pos] = pos)
                    int x = arr[i];
                    arr[i] = pos;
                    arr[pos] = x;
                    break;
                }
            }
        }
    }
    printArray(arr, n);
}

// Function to Print the array
static void printArray(int[] arr, int n)
{
    for(int i = 1; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
static public void Main()
{
    int[] arr = { 0, 7, 4, 0, 3, 0, 5, 1 };
    int n = arr.Length;

    solve(arr, n);
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

 // Function to fill the position
  // with arr[i] = 0
function solve(arr,n)
{
    let unfilled_indices = new Set();
    let missing = new Set();

    // Inserting all elements in
    // missing[] set from 1 to N
    for (let i = 1; i < n; i++)
    {
      missing.add(i);
    }
    for (let i = 1; i < n; i++)
    {

      // Inserting unfilled positions
      if (arr[i] == 0)
      {
        unfilled_indices.add(i);
      }

      // Removing allocated_elements
      else
      {
        missing.delete(arr[i]);
      }
    }
    let mi = new Array(missing.size);
    let l = 0;
    for(let x of missing.values())
    {
      mi[l++] = x;
    }
    let m = missing.size;

    // Loop for filling the positions
    // with arr[i] != i
    for(let it of unfilled_indices.values())
    {
      arr[it] = mi[m - 1];
      m--;
    }
    let pos = 0;

    // Checking for any arr[i] = i
    for (let i = 1; i < n; i++)
    {
      if (arr[i] == i)
      {
        pos = i;
      }
    }
    let x;

    // Finding the suitable position
    // in the array to swap with found i
    // for which arr[i] = i
    if (pos != 0)
    {
      for (let i = 1; i < n; i++)
      {
        if (pos != i)
        {

          // Checking if the position
          // is present in unfilled_position
          if(unfilled_indices.has(i))
          {

            // Swapping arr[i] & arr[pos]
            // (arr[pos] = pos)
            x = arr[i];
            arr[i] = pos;
            arr[pos] = x;
            break;
          }
        }
      }
    }
    printArray(arr, n);
}

 // Function to Print the array
function printArray(arr,n)
{
    for (let i = 1; i < n; i++)
    {
      document.write(arr[i] + " ");  
    }
}

// Driver Code
let arr=[0, 7, 4, 0,3, 0, 5, 1 ];
let n = arr.length;
solve(arr, n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
7 4 6 3 2 5 1
```