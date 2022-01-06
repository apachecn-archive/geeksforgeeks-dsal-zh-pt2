# 通过用数组元素的和重复替换成对不相等的相邻数组元素来最小化数组长度

> 原文:[https://www . geeksforgeeks . org/通过按数组元素的总和重复替换不相等的相邻数组元素对来最小化数组长度/](https://www.geeksforgeeks.org/minimize-array-length-by-repeatedly-replacing-pairs-of-unequal-adjacent-array-elements-by-their-sum/)

给定一个整数数组 **arr[]，**，任务是通过用两个不相等的相邻数组元素的和重复替换**来最小化给定数组的长度。一旦数组减少到最小可能长度，即数组中没有相邻的不相等对，打印所需的操作计数。**

**示例:**

> **输入:** arr[] = {2，1，3，1}
> **输出:** 1
> **解释:**
> 操作 1: { **2，1，** 3，1} - > { **3** ，3，1}
> 操作 2: {3， **3，1** } - > {3，4}
> 操作 3: {3，4}
> 
> **输入:** arr[] = {1，1，1，1}
> **输出:** 4
> **解释:**
> 由于无法获得不相等的相邻对，因此无法进行合并操作。
> 因此，数组的最小长度是 4。

**天真方法:**解决问题最简单的方法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个相邻的不等对，用其和替换该对。最后，如果数组中不存在不相等的对，打印数组的长度。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间** : O(N)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   如果数组的所有元素都相等，则不能执行任何操作。因此，打印***【N】***，即数组的初始长度，作为数组的最小可约长度
*   否则，数组的最小长度始终为 **1** 。

因此，要解决这个问题，只需遍历数组并检查所有数组元素是否相等。如果发现是真的，打印 **N** 作为所需答案。否则，打印 **1** 。
以下是上述办法的实施情况:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the minimum
// length of the array after merging
// unequal adjacent elements
int minLength(int A[], int N)
{

    // Stores the first element
    // and its frequency
    int elem = A[0], count = 1;

    // Traverse the array
    for (int i = 1; i < N; i++) {
        if (A[i] == elem) {
            count++;
        }
        else {
            break;
        }
    }

    // If all elements are equal
    if (count == N)

        // No merge-pair operations
        // can be performed
        return N;

    // Otherwise
    else
        return 1;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 1, 3, 1 };

    // Length of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minLength(arr, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Function that returns the minimum
// length of the array
// after merging unequal
// adjacent elements 
static int minLength(int A[],
                     int N)
{
  // Stores the first element
  // and its frequency
  int elem = A[0], count = 1;

  // Traverse the array
  for (int i = 1; i < N; i++)
  {
    if (A[i] == elem)
    {
      count++;
    }
    else
    {
      break;
    }
  }

  // If all elements are equal
  if (count == N)

    // No merge-pair operations
    // can be performed
    return N;

  // Otherwise
  else
    return 1;
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int arr[] = {2, 1, 3, 1};

  // Length of the array
  int N = arr.length;

  // Function Call
  System.out.print(minLength(arr, N) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that returns the minimum
# length of the array after merging
# unequal adjacent elements
def minLength(A, N):

    # Stores the first element
    # and its frequency
    elem = A[0]
    count = 1

    # Traverse the array
    for i in range(1, N):
        if (A[i] == elem):
            count += 1
        else:
            break

    # If all elements are equal
    if (count == N):

        # No merge-pair operations
        # can be performed
        return N

    # Otherwise
    else:
        return 1

# Driver Code

# Given array
arr = [ 2, 1, 3, 1 ]

# Length of the array
N = len(arr)

# Function call
print(minLength(arr, N))

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that returns the minimum
// length of the array
// after merging unequal
// adjacent elements 
static int minLength(int []A,
                     int N)
{
  // Stores the first element
  // and its frequency
  int elem = A[0], count = 1;

  // Traverse the array
  for (int i = 1; i < N; i++)
  {
    if (A[i] == elem)
    {
      count++;
    }
    else
    {
      break;
    }
  }

  // If all elements are equal
  if (count == N)

    // No merge-pair operations
    // can be performed
    return N;

  // Otherwise
  else
    return 1;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int []arr = {2, 1, 3, 1};

  // Length of the array
  int N = arr.Length;

  // Function Call
  Console.Write(minLength(arr, N) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach   

// Function that returns the minimum
    // length of the array
    // after merging unequal
    // adjacent elements

    function minLength(A , N)
    {
        // Stores the first element
        // and its frequency
        var elem = A[0], count = 1;

        // Traverse the array
        for (var i = 1; i < N; i++) {
            if (A[i] == elem) {
                count++;
            } else {
                break;
            }
        }

        // If all elements are equal
        if (count == N)

            // No merge-pair operations
            // can be performed
            return N;

        // Otherwise
        else
            return 1;
    }

    // Driver Code

        // Given array
        var arr = [ 2, 1, 3, 1 ];

        // Length of the array
        var N = arr.length;

        // Function Call
        document.write(minLength(arr, N) + "\n");

// This code contributed by aashish1995

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(1)