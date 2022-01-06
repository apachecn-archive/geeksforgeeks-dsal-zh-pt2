# 使用二元索引树

计算右侧较小元素和左侧较大元素的数量

> 原文:[https://www . geesforgeks . org/count-右侧小元素和左侧大元素-使用二进制索引树/](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side-and-greater-elements-on-left-side-using-binary-index-tree/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是为给定数组中的每个元素 **arr[i]** 找到右侧的较小元素和左侧的较大元素。
**举例:**

> **输入:** arr[] = {12，1，2，3，0，11，4}
> **输出:**
> 小右:6 1 1 0 1 0 1 0
> 大左:0 1 1 4 1 2
> **输入:** arr[] = {5，4，3，2，1}
> **输出:**
> 小右:4 3 2 1 0
> 大左:0 1 2 3 4

**先决条件:** [使用 BIT](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)
**方法计算数组中的反转:**我们已经在[这篇](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)帖子中讨论了计算右侧较小元素的实现。在这里，我们将使用[二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)来计算数组中每个元素右侧的较小元素和左侧的较大元素。首先，按照上一篇文章中的建议，从右向左遍历数组，并在右侧找到更小的元素。然后重置位数组，从左到右遍历数组，在左侧找到更大的元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of arr[0..index]
// This function assumes that the array is preprocessed
// and partial sums of array elements are stored in BITree[]
int getSum(int BITree[], int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0) {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at given index
// in BITree. The given value 'val' is added to BITree[i] and
// all of its ancestors in tree.
void updateBIT(int BITree[], int n, int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n) {

        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent in update View
        index += index & (-index);
    }
}

// Converts an array to an array with values from 1 to n
// and relative order of smaller and greater elements remains
// same. For example, {7, -90, 100, 1} is converted to
// {3, 1, 4, 2 }
void convert(int arr[], int n)
{
    // Create a copy of arrp[] in temp and sort the temp array
    // in increasing order
    int temp[n];
    for (int i = 0; i < n; i++)
        temp[i] = arr[i];
    sort(temp, temp + n);

    // Traverse all array elements
    for (int i = 0; i < n; i++) {
        // lower_bound() Returns pointer to the first element
        // greater than or equal to arr[i]
        arr[i] = lower_bound(temp, temp + n, arr[i]) - temp + 1;
    }
}

// Function to find smaller_right array
void findElements(int arr[], int n)
{
    // Convert arr[] to an array with values from 1 to n and
    // relative order of smaller and greater elements remains
    // same. For example, {7, -90, 100, 1} is converted to
    // {3, 1, 4, 2 }
    convert(arr, n);

    // Create a BIT with size equal to maxElement+1 (Extra
    // one is used so that elements can be directly be
    // used as index)
    int BIT[n + 1];
    for (int i = 1; i <= n; i++)
        BIT[i] = 0;

    // To store smaller elements in right side
    // and greater elements on left side
    int smaller_right[n], greater_left[n];

    // Traverse all elements from right.
    for (int i = n - 1; i >= 0; i--) {

        // Get count of elements smaller than arr[i]
        smaller_right[i] = getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    cout << "Smaller right: ";

    // Print smaller_right array
    for (int i = 0; i < n; i++)
        cout << smaller_right[i] << " ";
    cout << endl;

    for (int i = 1; i <= n; i++)
        BIT[i] = 0;

    // Find all left side greater elements
    for (int i = 0; i < n; i++) {

        // Get count of elements greater than arr[i]
        greater_left[i] = i - getSum(BIT, arr[i]);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    cout << "Greater left: ";

    // Print greater_left array
    for (int i = 0; i < n; i++)
        cout << greater_left[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 12, 1, 2, 3, 0, 11, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    findElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function to return the sum of
// arr[0..index]. This function
// assumes that the array is
// preprocessed and partial sums
// of array elements are stored in BITree[]
public static int getSum(int BITree[], int index)
{

    // Initialize result
    int sum = 0;

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {

        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree
// (BITree) at given index in BITree.
// The given value 'val' is added to BITree[i]
// and all of its ancestors in tree.
public static void updateBIT(int BITree[], int n,
                             int index, int val)
{

    // Traverse all ancestors and add 'val'
    while (index <= n)
    {

        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent
        // in update View
        index += index & (-index);
    }
}

// Converts an array to an array with values
// from 1 to n and relative order of smaller
// and greater elements remains same.
// For example, {7, -90, 100, 1} is converted to
// {3, 1, 4, 2 }
public static void convert(int arr[], int n)
{

    // Create a copy of arrp[] in temp
    // and sort the temp array in
    // increasing order
    int[] temp = new int[n];
    for(int i = 0; i < n; i++)
        temp[i] = arr[i];

    Arrays.sort(temp);

    // Traverse all array elements
    for(int i = 0; i < n; i++)
    {

        // Arrays.binarySearch() returns index
        // to the first element greater than
        // or equal to arr[i]
        arr[i] = Arrays.binarySearch(temp, arr[i]) + 1;
    }
}

// Function to find smaller_right array
public static void findElements(int arr[], int n)
{

    // Convert arr[] to an array with values
    // from 1 to n and relative order of smaller
    // and greater elements remains same. For
    // example, {7, -90, 100, 1} is converted to
    // {3, 1, 4, 2 }
    convert(arr, n);

    // Create a BIT with size equal to
    // maxElement+1 (Extra one is used
    // so that elements can be directly be
    // used as index)
    int[] BIT = new int[n + 1];
    for(int i = 1; i <= n; i++)
        BIT[i] = 0;

    // To store smaller elements in right side
    // and greater elements on left side
    int[] smaller_right = new int[n];
    int[] greater_left = new int[n];

    // Traverse all elements from right.
    for(int i = n - 1; i >= 0; i--)
    {

        // Get count of elements smaller than arr[i]
        smaller_right[i] = getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    System.out.print("Smaller right: ");

    // Print smaller_right array
    for(int i = 0; i < n; i++)
        System.out.print(smaller_right[i] + " ");

    System.out.println();

    for(int i = 1; i <= n; i++)
        BIT[i] = 0;

    // Find all left side greater elements
    for(int i = 0; i < n; i++)
    {

        // Get count of elements greater than arr[i]
        greater_left[i] = i - getSum(BIT, arr[i]);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    System.out.print("Greater left: ");

    // Print greater_left array
    for(int i = 0; i < n; i++)
        System.out.print(greater_left[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 12, 1, 2, 3, 0, 11, 4 };

    int n = arr.length;

    // Function call
    findElements(arr, n);
}
}

// This code is contributed by kunalsg18elec   
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from bisect import bisect_left as lower_bound

# Function to return the sum of arr[0..index]
# This function assumes that the array is
# preprocessed and partial sums of array elements
# are stored in BITree[]
def getSum(BITree, index):

    # Initialize result
    s = 0

    # Traverse ancestors of BITree[index]
    while index > 0:

        # Add current element of BITree to sum
        s += BITree[index]

        # Move index to parent node in getSum View
        index -= index & (-index)

    return s

# Updates a node in Binary Index Tree (BITree)
# at given index in BITree. The given value 'val'
# is added to BITree[i] and all of its ancestors in tree.
def updateBIT(BITree, n, index, val):

    # Traverse all ancestors and add 'val'
    while index <= n:

        # Add 'val' to current node of BI Tree
        BITree[index] += val

        # Update index to that of parent in update View
        index += index & (-index)

# Converts an array to an array with values
# from 1 to n and relative order of smaller
# and greater elements remains same.
# For example, {7, -90, 100, 1} is
# converted to {3, 1, 4, 2 }
def convert(arr, n):

    # Create a copy of arrp[] in temp and
    # sort the temp array in increasing order
    temp = [0] * n
    for i in range(n):
        temp[i] = arr[i]

    temp.sort()

    # Traverse all array elements
    for i in range(n):

        # lower_bound() Returns pointer to the first element
        # greater than or equal to arr[i]
        arr[i] = lower_bound(temp, arr[i]) + 1

# Function to find smaller_right array
def findElements(arr, n):

    # Convert arr[] to an array with values
    # from 1 to n and relative order of smaller and
    # greater elements remains same. For example,
    # {7, -90, 100, 1} is converted to {3, 1, 4, 2 }
    convert(arr, n)

    # Create a BIT with size equal to maxElement+1
    # (Extra one is used so that elements can be
    # directly be used as index)
    BIT = [0] * (n + 1)

    # To store smaller elements in right side
    # and greater elements on left side
    smaller_right = [0] * n
    greater_left = [0] * n

    # Traverse all elements from right.
    for i in range(n - 1, -1, -1):

        # Get count of elements smaller than arr[i]
        smaller_right[i] = getSum(BIT, arr[i] - 1)

        # Add current element to BIT
        updateBIT(BIT, n, arr[i], 1)

    print("Smaller right:", end = " ")
    for i in range(n):
        print(smaller_right[i], end = " ")
    print()

    # Print smaller_right array
    for i in range(1, n + 1):
        BIT[i] = 0

    # Find all left side greater elements
    for i in range(n):

        # Get count of elements greater than arr[i]
        greater_left[i] = i - getSum(BIT, arr[i])

        # Add current element to BIT
        updateBIT(BIT, n, arr[i], 1)

    print("Greater left:", end = " ")

    # Print greater_left array
    for i in range(n):
        print(greater_left[i], end = " ")
    print()

# Driver Code
if __name__ == "__main__":

    arr = [12, 1, 2, 3, 0, 11, 4]
    n = len(arr)

    # Function call
    findElements(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG{

// Function to return the sum of
// arr[0..index]. This function
// assumes that the array is
// preprocessed and partial sums
// of array elements are stored
// in BITree[]
public static int getSum(int []BITree,
                         int index)
{    
  // Initialize result
  int sum = 0;

  // Traverse ancestors
  // of BITree[index]
  while (index > 0)
  {
    // Add current element
    // of BITree to sum
    sum += BITree[index];

    // Move index to parent node
    // in getSum View
    index -= index & (-index);
  }
  return sum;
}

// Updates a node in Binary Index Tree
// (BITree) at given index in BITree.
// The given value 'val' is added to BITree[i]
// and all of its ancestors in tree.
public static void updateBIT(int []BITree, int n,
                             int index, int val)
{    
  // Traverse all ancestors
  // and add 'val'
  while (index <= n)
  {

    // Add 'val' to current
    // node of BI Tree
    BITree[index] += val;

    // Update index to that
    // of parent in update View
    index += index & (-index);
  }
}

// Converts an array to an array
// with values from 1 to n and
// relative order of smaller and
// greater elements remains same.
// For example, {7, -90, 100, 1}
// is converted to {3, 1, 4, 2 }
public static void convert(int []arr,
                           int n)
{    
  // Create a copy of arrp[] in temp
  // and sort the temp array in
  // increasing order
  int[] temp = new int[n];

  for(int i = 0; i < n; i++)
    temp[i] = arr[i];

  Array.Sort(temp);

  // Traverse all array elements
  for(int i = 0; i < n; i++)
  {
    // Arrays.binarySearch()
    // returns index to the
    // first element greater
    // than or equal to arr[i]
    arr[i] =  Array.BinarySearch(temp,
                                 arr[i]) + 1;
  }
}

// Function to find smaller_right array
public static void findElements(int []arr,
                                int n)
{    
  // Convert []arr to an array with
  // values from 1 to n and relative
  // order of smaller and greater
  // elements remains same. For
  // example, {7, -90, 100, 1} is
  // converted to {3, 1, 4, 2 }
  convert(arr, n);

  // Create a BIT with size equal
  // to maxElement+1 (Extra one is
  // used so that elements can be
  // directly be used as index)
  int[] BIT = new int[n + 1];

  for(int i = 1; i <= n; i++)
    BIT[i] = 0;

  // To store smaller elements in
  // right side and greater elements
  // on left side
  int[] smaller_right = new int[n];
  int[] greater_left = new int[n];

  // Traverse all elements from right.
  for(int i = n - 1; i >= 0; i--)
  {
    // Get count of elements smaller
    // than arr[i]
    smaller_right[i] = getSum(BIT,
                              arr[i] - 1);

    // Add current element to BIT
    updateBIT(BIT, n, arr[i], 1);
  }

  Console.Write("Smaller right: ");

  // Print smaller_right array
  for(int i = 0; i < n; i++)
    Console.Write(smaller_right[i] + " ");

  Console.WriteLine();

  for(int i = 1; i <= n; i++)
    BIT[i] = 0;

  // Find all left side greater
  // elements
  for(int i = 0; i < n; i++)
  {
    // Get count of elements greater
    // than arr[i]
    greater_left[i] = i - getSum(BIT,
                                 arr[i]);

    // Add current element to BIT
    updateBIT(BIT, n, arr[i], 1);
  }

  Console.Write("Greater left: ");

  // Print greater_left array
  for(int i = 0; i < n; i++)
    Console.Write(greater_left[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {12, 1, 2,
               3, 0, 11, 4};
  int n = arr.Length;

  // Function call
  findElements(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
Smaller right: 6 1 1 1 0 1 0 
Greater left: 0 1 1 1 4 1 2
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(N)