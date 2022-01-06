# 以索引 I 开始或结束的子阵列计数，使得 arr[i]在子阵列中最大

> 原文:[https://www . geeksforgeeks . org/子数组计数-在索引 I 处开始或结束，这样子数组中的 arri 就是最大值/](https://www.geeksforgeeks.org/count-of-subarrays-starting-or-ending-at-an-index-i-such-that-arri-is-maximum-in-subarray/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出在索引 **i** 处开始或结束的子阵列的数量，使得**arr【I】**是子阵列的[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。

**示例:**

> **输入:** arr[] = {3，4，1，6，2}
> **输出:**1 3 1 5 1
> T6】解释:
> 
> 1.  从索引 0 开始或结束且最大 arr[0](=3)的子阵列是{3}。因此，计数为 1。
> 2.  从索引 1 开始或结束并具有最大 arr[1](=4)的子阵列是{3，4}、{4}和{4，1}。因此，计数为 3。
> 3.  从索引 2 开始或结束且最大 arr[2](=1)的子阵列是{1}。因此，计数为 1。
> 4.  从索引 3 开始或结束并具有最大 arr[3](=6)的子阵列是{3，4，1，6}、{4，1，6}、{1，6}、{6}和{6，2}。因此，计数为 5。
> 5.  从索引 4 开始或结束且最大 arr[4](=2)的子阵列是{2}。因此，计数为 1。
> 
> **输入:** arr[] = {1，2，3}
> **输出:** 1 2 3

**天真方法:**解决给定问题的最简单方法是，对于每个**I<sup>th</sup>T5】索引，前后迭代，直到子阵列的最大值保持等于**arr【I】**，然后打印获得的子阵列总数。**

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**通过为每个索引 **i** 存储[下一个较大元素](https://www.geeksforgeeks.org/next-greater-element/)和[上一个较大元素](https://www.geeksforgeeks.org/previous-greater-element/)的索引，并为每个索引找到相应的子阵列计数，可以优化上述方法。按照以下步骤解决给定的问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/array-data-structure/)比如**PGE【】**和**nge【】**为每个索引 **i** 存储[上一个较大元素](https://www.geeksforgeeks.org/previous-greater-element/)和[下一个较大元素](https://www.geeksforgeeks.org/next-greater-element/)的索引。
*   为每个索引找到[上一个较大元素](https://www.geeksforgeeks.org/previous-greater-element/)的索引，并将结果数组存储在 **pge[]** 中。
*   为每个索引找到[下一个更大元素](https://www.geeksforgeeks.org/next-greater-element/)的索引，并将结果数组存储在**区间[]** 中。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**并使用变量 **i** ，在每次迭代打印中，以索引 **i** 和**arr【I】**作为最大值的子阵列计数为**nge[I]+PGE[I]–1**并打印该计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find previous greater
// element
int* getPGE(int arr[], int n)
{

    // Stores the previous greater
    // element for each index
    int* pge = new int[n];
    stack<int> stack;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Iterate until stack is empty
        // and top element is less than
        // the current element arr[i]
        while (!stack.empty() &&
            arr[stack.top()] <= arr[i])
        {
            stack.pop();
        }

        // Update the previous greater
        // element for arr[i]
        pge[i] = stack.empty() ? -1 : stack.top();

        // Push the current index to
        // the stack
        stack.push(i);
    }

    // Return the PGE[] array
    return pge;
}

// Function to find the Next Greater Element
int* getNGE(int arr[], int n)
{

    // Stores the next greater element
    // for each index
    int* nge = new int[n];
    stack<int> stack;

    // Traverse the array from the back
    for(int i = n - 1; i >= 0; i--)
    {

        // Iterate until stack is empty
        // and top element is less than
        // the current element arr[i]
        while (!stack.empty() &&
            arr[stack.top()] <= arr[i])
        {
            stack.pop();
        }

        // Update the next greater
        // element for arr[i]
        nge[i] = stack.empty() ? n : stack.top();

        // Push the current index
        stack.push(i);
    }

    // Return the NGE[] array
    return nge;
}

// Function to find the count of
// subarrays starting or ending at
// index i having arr[i] as maximum
void countSubarrays(int arr[], int n)
{

    // Function call to find the
    // previous greater element
    // for each array elements
    int* pge = getPGE(arr, n);

    // Function call to find the
    // previous greater element
    // for each elements
    int* nge = getNGE(arr, n);

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Print count of subarrays
        // satisfying the conditions
        cout << nge[i] - pge[i] - 1 << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 4, 1, 6, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    countSubarrays(arr, n);

    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG {

    // Function to find previous greater
    // element
    private static int[] getPGE(int[] arr)
    {
        // Stores the previous greater
        // element for each index
        int[] pge = new int[arr.length];
        Stack<Integer> stack = new Stack<>();

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {

            // Iterate until stack is empty
            // and top element is less than
            // the current element arr[i]
            while (!stack.isEmpty()
                   && arr[stack.peek()] <= arr[i]) {
                stack.pop();
            }

            // Update the previous greater
            // element for arr[i]
            pge[i] = stack.isEmpty() ? -1 : stack.peek();

            // Push the current index to
            // the stacl
            stack.push(i);
        }

        // Return the PGE[] array
        return pge;
    }

    // Function to find the Next Greater Element
    private static int[] getNGE(int[] arr)
    {
        // Stores the next greater element
        // for each index
        int[] nge = new int[arr.length];
        Stack<Integer> stack = new Stack<>();

        // Traverse the array from the back
        for (int i = arr.length - 1; i >= 0; i--) {

            // Iterate until stack is empty
            // and top element is less than
            // the current element arr[i]
            while (!stack.isEmpty()
                   && arr[stack.peek()] <= arr[i]) {
                stack.pop();
            }

            // Update the next greater
            // element for arr[i]
            nge[i] = stack.isEmpty() ? arr.length
                                     : stack.peek();

            // Push the current index
            stack.push(i);
        }

        // Return the NGE[] array
        return nge;
    }

    // Function to find the count of
    // subarrays starting or ending at
    // index i having arr[i] as maximum
    private static void countSubarrays(int[] arr)
    {

        // Function call to find the
        // previous greater element
        // for each array elements
        int[] pge = getPGE(arr);

        // Function call to find the
        // previous greater element
        // for each elements
        int[] nge = getNGE(arr);

        // Traverse the array arr[]
        for (int i = 0; i < arr.length; i++) {

            // Print count of subarrays
            // satisfying the conditions
            System.out.print(
                nge[i] - pge[i] - 1 + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 3, 4, 1, 6, 2 };
        countSubarrays(arr);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach
# Stores the previous greater
# element for each index
pge = []

# Stores the next greater element
# for each index
nge = []

# Function to find previous greater
# element
def getPGE(arr, n) :
  s = list()

  # Traverse the array
  for i in range(0, n):

    # Iterate until stack is empty
    # and top element is less than
    # the current element arr[i]
    while (len(s) > 0 and arr[s[-1]] <= arr[i]):
      s.pop()

    # Update the previous greater
    # element for arr[i]
    if len(s) == 0:
      pge.append(-1)
    else:
      pge.append(s[-1])

    # Push the current index
    s.append(i)

# Function to find the Next Greater Element  
def getNGE(arr, n) :
  s = list()

  # Traverse the array from the back
  for i in range(n-1, -1, -1):

    # Iterate until stack is empty
    # and top element is less than
    # the current element arr[i]
    while (len(s) > 0 and arr[s[-1]] <= arr[i]):
      s.pop()

    # Update the next greater
    # element for arr[i]
    if len(s) == 0:
      nge.append(n)
    else:
      nge.append(s[-1])

    # Push the current index
    s.append(i)
  nge.reverse();

# Function to find the count of
# subarrays starting or ending at
# index i having arr[i] as maximum
def countSubarrays(arr, n):

  # Function call to find the
  # previous greater element
  # for each array elements
  getNGE(arr, n);

  # Function call to find the
  # previous greater element
  # for each elements
  getPGE(arr, n);

  # Traverse the array arr[]
  for i in range(0,n):
    print(nge[i]-pge[i]-1,end = " ")

arr = [ 3, 4, 1, 6, 2 ]
n = len(arr)
countSubarrays(arr,n);

# This code is contributed by codersaty
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Function to find previous greater
    // element
    static int[] getPGE(int[] arr)
    {

        // Stores the previous greater
        // element for each index
        int[] pge = new int[arr.Length];
        Stack stack = new Stack();

        // Traverse the array
        for (int i = 0; i < arr.Length; i++) {

            // Iterate until stack is empty
            // and top element is less than
            // the current element arr[i]
            while (stack.Count > 0 && arr[(int)stack.Peek()] <= arr[i]) {
                stack.Pop();
            }

            // Update the previous greater
            // element for arr[i]
            pge[i] = stack.Count == 0 ? -1 : (int)stack.Peek();

            // Push the current index to
            // the stacl
            stack.Push(i);
        }

        // Return the PGE[] array
        return pge;
    }

    // Function to find the Next Greater Element
    static int[] getNGE(int[] arr)
    {
        // Stores the next greater element
        // for each index
        int[] nge = new int[arr.Length];
        Stack stack = new Stack();

        // Traverse the array from the back
        for (int i = arr.Length - 1; i >= 0; i--) {

            // Iterate until stack is empty
            // and top element is less than
            // the current element arr[i]
            while (stack.Count > 0 && arr[(int)stack.Peek()] <= arr[i]) {
                stack.Pop();
            }

            // Update the next greater
            // element for arr[i]
            nge[i] = stack.Count == 0 ? arr.Length : (int)stack.Peek();

            // Push the current index
            stack.Push(i);
        }

        // Return the NGE[] array
        return nge;
    }

    // Function to find the count of
    // subarrays starting or ending at
    // index i having arr[i] as maximum
    static void countSubarrays(int[] arr)
    {

        // Function call to find the
        // previous greater element
        // for each array elements
        int[] pge = getPGE(arr);

        // Function call to find the
        // previous greater element
        // for each elements
        int[] nge = getNGE(arr);

        // Traverse the array arr[]
        for (int i = 0; i < arr.Length; i++) {

            // Print count of subarrays
            // satisfying the conditions
            Console.Write((nge[i] - pge[i] - 1) + " ");
        }
    }

  // Driver code
  static void Main() {
    int[] arr = { 3, 4, 1, 6, 2 };
    countSubarrays(arr);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for the above approach
// Stores the previous greater
// element for each index
let pge = [];

// Stores the next greater element
// for each index
let nge = [];

// Function to find previous greater
// element
function getPGE(arr, n) {
  let s = [];

  // Traverse the array
  for (let i = 0; i < n; i++)
  {

    // Iterate until stack is empty
    // and top element is less than
    // the current element arr[i]
    while (s.length > 0 && arr[s[s.length - 1]] <= arr[i])
    {
      s.pop();
    }

    // Update the previous greater
    // element for arr[i]
    if (s.length == 0) pge.push(-1);
    else pge.push(s[s.length - 1]);

    // Push the current index
    s.push(i);
  }
}

// Function to find the Next Greater Element
function getNGE(arr, n) {
  let s = [];

  // Traverse the array from the back
  for (let i = n - 1; i >= 0; i--)
  {

    // Iterate until stack is empty
    // and top element is less than
    // the current element arr[i]
    while (s.length > 0 && arr[s[s.length - 1]] <= arr[i]) {
      s.pop();
    }

    // Update the next greater
    // element for arr[i]
    if (s.length == 0) nge.push(n);
    else nge.push(s[s.length - 1]);

    // Push the current index
    s.push(i);
  }
  nge.reverse();
}

// Function to find the count of
// subarrays starting or ending at
// index i having arr[i] as maximum
function countSubarrays(arr, n)
{

  // Function call to find the
  // previous greater element
  // for each array elements
  getNGE(arr, n);

  // Function call to find the
  // previous greater element
  // for each elements
  getPGE(arr, n);

  // Traverse the array arr[]
  for (let i = 0; i < n; i++) {
    document.write(nge[i] - pge[i] - 1 + " ");
  }
}

let arr = [3, 4, 1, 6, 2];
let n = arr.length;
countSubarrays(arr, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
1 3 1 5 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)