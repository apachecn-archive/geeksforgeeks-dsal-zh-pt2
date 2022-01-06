# 数组中每个索引的最大范围子数组，使得 A[i] = min(A[L]，A[L+1]，… A[R])

> 原文:[https://www . geeksforgeeks . org/数组中每个索引的最大范围子数组-ai-minal-al1-ar/](https://www.geeksforgeeks.org/maximum-range-subarray-for-each-index-in-array-such-that-ai-minal-al1-ar/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是为每个索引 **i (1≤i≤N)** 计算一个范围**【L，R】**，使得 **arr[i] = min(arr[L]，arr[L+1]，… arr[R])** ，其中 **L≤i≤R** 和 **R-L** 最大化。

**示例:**

> **输入:** N = 3，arr[] = {1，3，2}
> **输出:**1 3
> 2
> 2 3
> **说明:** 1 在[1，3]
> 范围内最小 3 在[2，2]
> 范围内最小 2 在[2，3]范围内最小
> 
> **输入:** N = 3，arr[] = {4，5，6}
> **输出:** 1 3
> 2 3
> 3 3

**方法:**可以观察到，每个指标都需要[**前面较小的**](https://www.geeksforgeeks.org/find-the-nearest-smaller-numbers-on-left-side-in-an-array/) 和 [**后面较小的**](https://www.geeksforgeeks.org/next-smaller-element/) 元素来计算所需范围。想法是用[栈](https://www.geeksforgeeks.org/stack-data-structure/)找到前一个更大的和后一个更大的元素。按照以下步骤解决问题:

*   创建两个[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **L[]** 和 **R[]** ，分别存储当前元素左边最近的小元素和右边最近的小元素。
*   创建一个[栈](https://www.geeksforgeeks.org/stack-data-structure/) **S** ，并在其中添加第一个元素的索引。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，弹出栈，直到栈顶、 **S** 不小于当前元素。
*   现在将左边最近的小元素**L【I】**设置为 **S** 的顶部，如果 **S** 为空，设置为 0。将电流元件推入 **S** 。
*   类似地，从末端以相反的方向遍历，并按照相同的步骤填充数组， **R[]** 。
*   在**【1，N】**范围内迭代，为每个索引 **i** 打印**L【I】**和**R【I】**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the range for each index
void rangeFinder(int arr[], int N)
{
    // Array to store index of closest smaller
    // element at left sub-array
    int L[N];

    // Array to store index of closest smaller
    // element at right sub-array
    int R[N];

    // Stack to find previous smaller element
    stack<int> S;

    // Since there is no element before first
    // element, so set L[0]=0
    L[0] = 0;

    // Push the first element index in stack
    S.push(0);

    // Traverse the array, arr[]
    for (int i = 1; i < N; i++) {

        // Pop until the top of stack is greater
        // than current element
        while (!S.empty() && arr[S.top()] > arr[i])
            S.pop();

        // Update L[i] as peek as it is
        // previous smaller element
        if (!S.empty())
            L[i] = S.top() + 1;

        // Otherwise, update L[i] to 0
        else
            L[i] = 0;

        // Push the current index
        S.push(i);
    }

    // Empty the stack, S
    while (!S.empty())
        S.pop();

    // Since there is no element after
    // last element, so set R[N-1]=N-1
    R[N - 1] = N - 1;

    // Push the last element index into stack
    S.push(N - 1);

    // Traverse the array from the end
    for (int i = N - 2; i >= 0; i--) {

        // Pop until the top of S is greater
        // than current element
        while (!S.empty() && arr[S.top()] > arr[i])
            S.pop();

        // Set R[i] as top as it is previous
        // smaller element from end
        if (!S.empty())
            R[i] = S.top() - 1;

        // Otherwise, update R[i] as N-1
        else
            R[i] = N - 1;

        // Push the current index
        S.push(i);
    }

    // Print the required range using L and R array
    for (int i = 0; i < N; i++) {
        cout << L[i] + 1 << " " << R[i] + 1 << endl;
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 1, 3, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    rangeFinder(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to print the range for each index
static void rangeFinder(int arr[], int N)
{

    // Array to store index of closest smaller
    // element at left sub-array
    int[] L = new int[N];

    // Array to store index of closest smaller
    // element at right sub-array
    int[] R = new int[N];

    // Stack to find previous smaller element
    Stack<Integer> S = new Stack<Integer>();

    // Since there is no element before first
    // element, so set L[0]=0
    L[0] = 0;

    // Push the first element index in stack
    S.push(0);

    // Traverse the array, arr[]
    for(int i = 1; i < N; i++)
    {

        // Pop until the top of stack is greater
        // than current element
        while (!S.empty() && arr[S.peek()] > arr[i])
            S.pop();

        // Update L[i] as peek as it is
        // previous smaller element
        if (!S.empty())
            L[i] = S.peek() + 1;

        // Otherwise, update L[i] to 0
        else
            L[i] = 0;

        // Push the current index
        S.push(i);
    }

    // Empty the stack, S
    while (!S.empty())
        S.pop();

    // Since there is no element after
    // last element, so set R[N-1]=N-1
    R[N - 1] = N - 1;

    // Push the last element index into stack
    S.push(N - 1);

    // Traverse the array from the end
    for(int i = N - 2; i >= 0; i--)
    {

        // Pop until the top of S is greater
        // than current element
        while (!S.empty() && arr[S.peek()] > arr[i])
            S.pop();

        // Set R[i] as top as it is previous
        // smaller element from end
        if (!S.empty())
            R[i] = S.peek() - 1;

        // Otherwise, update R[i] as N-1
        else
            R[i] = N - 1;

        // Push the current index
        S.push(i);
    }

    // Print the required range using L and R array
    for(int i = 0; i < N; i++)
    {
        System.out.println((L[i] + 1) + " " +
                           (R[i] + 1));
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { 1, 3, 2 };
    int N = arr.length;

    // Function Call
    rangeFinder(arr, N);
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the range for each index
def rangeFinder(arr, N):

    # Array to store index of closest smaller
    # element at left sub-array
    L = [0 for i in range(N)]

    # Array to store index of closest smaller
    # element at right sub-array
    R = [0 for i in range(N)]

    # Stack to find previous smaller element
    S = []

    # Since there is no element before first
    # element, so set L[0]=0
    L[0] = 0

    # Push the first element index in stack
    S.append(0)

    # Traverse the array, arr[]
    for i in range(1, N, 1):

        # Pop until the top of stack is greater
        # than current element
        while (len(S) > 0 and
         arr[S[len(S) - 1]] > arr[i]):
            S = S[:-1]

        # Update L[i] as peek as it is
        # previous smaller element
        if (len(S) > 0):
            L[i] = S[len(S) - 1] + 1

        # Otherwise, update L[i] to 0
        else:
            L[i] = 0

        # Push the current index
        S.append(i)

    # Empty the stack, S
    while (len(S) > 0):
        S.pop()

    # Since there is no element after
    # last element, so set R[N-1]=N-1
    R[N - 1] = N - 1

    # Push the last element index into stack
    S.append(N - 1)

    # Traverse the array from the end
    i = N - 2

    while (i >= 0):

        # Pop until the top of S is greater
        # than current element
        while (len(S) > 0 and
         arr[S[len(S) - 1]] > arr[i]):
            S = S[:-1]

        # Set R[i] as top as it is previous
        # smaller element from end
        if (len(S) > 0):
            R[i] = S[len(S) - 1] - 1;

        # Otherwise, update R[i] as N-1
        else:
            R[i] = N - 1

        # Push the current index
        S.append(i)
        i -= 1

    # Print the required range using L and R array
    for i in range(N):
        print(L[i] + 1, R[i] + 1)

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 1, 3, 2 ]
    N = len(arr)

    # Function Call
    rangeFinder(arr, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Function to print the range for each index
    static void rangeFinder(int[] arr, int N)
    {

        // Array to store index of closest smaller
        // element at left sub-array
        int[] L = new int[N];

        // Array to store index of closest smaller
        // element at right sub-array
        int[] R = new int[N];

        // Stack to find previous smaller element
        Stack S = new Stack();

        // Since there is no element before first
        // element, so set L[0]=0
        L[0] = 0;

        // Push the first element index in stack
        S.Push(0);

        // Traverse the array, arr[]
        for(int i = 1; i < N; i++)
        {

            // Pop until the top of stack is greater
            // than current element
            while (S.Count > 0 && arr[(int)S.Peek()] > arr[i])
                S.Pop();

            // Update L[i] as peek as it is
            // previous smaller element
            if (S.Count > 0)
                L[i] = (int)S.Peek() + 1;

            // Otherwise, update L[i] to 0
            else
                L[i] = 0;

            // Push the current index
            S.Push(i);
        }

        // Empty the stack, S
        while (S.Count > 0)
            S.Pop();

        // Since there is no element after
        // last element, so set R[N-1]=N-1
        R[N - 1] = N - 1;

        // Push the last element index into stack
        S.Push(N - 1);

        // Traverse the array from the end
        for(int i = N - 2; i >= 0; i--)
        {

            // Pop until the top of S is greater
            // than current element
            while (S.Count > 0 && arr[(int)S.Peek()] > arr[i])
                S.Pop();

            // Set R[i] as top as it is previous
            // smaller element from end
            if (S.Count > 0)
                R[i] = (int)S.Peek() - 1;

            // Otherwise, update R[i] as N-1
            else
                R[i] = N - 1;

            // Push the current index
            S.Push(i);
        }

        // Print the required range using L and R array
        for(int i = 0; i < N; i++)
        {
            Console.WriteLine((L[i] + 1) + " " + (R[i] + 1));
        }
    }

  static void Main()
  {

    // Given Input
    int[] arr = { 1, 3, 2 };
    int N = arr.Length;

    // Function Call
    rangeFinder(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the range for each index
function rangeFinder(arr, N) {
    // Array to store index of closest smaller
    // element at left sub-array
    let L = new Array(N).fill(0);

    // Array to store index of closest smaller
    // element at right sub-array
    let R = new Array(N).fill(0);

    // Stack to find previous smaller element
    let S = [];

    // Since there is no element before first
    // element, so set L[0]=0
    L[0] = 0;

    // Push the first element index in stack
    S.push(0);

    // Traverse the array, arr[]
    for (let i = 1; i < N; i++) {

        // Pop until the top of stack is greater
        // than current element
        while (S.length && arr[S[S.length - 1]] > arr[i])
            S.pop();

        // Update L[i] as peek as it is
        // previous smaller element
        if (S.length)
            L[i] = S[S.length - 1] + 1;

        // Otherwise, update L[i] to 0
        else
            L[i] = 0;

        // Push the current index
        S.push(i);
    }

    // Empty the stack, S
    while (S.length)
        S.pop();

    // Since there is no element after
    // last element, so set R[N-1]=N-1
    R[N - 1] = N - 1;

    // Push the last element index into stack
    S.push(N - 1);

    // Traverse the array from the end
    for (let i = N - 2; i >= 0; i--) {

        // Pop until the top of S is greater
        // than current element
        while (S.length && arr[S[S.length - 1]] > arr[i])
            S.pop();

        // Set R[i] as top as it is previous
        // smaller element from end
        if (S.length)
            R[i] = S[S.length - 1] - 1;

        // Otherwise, update R[i] as N-1
        else
            R[i] = N - 1;

        // Push the current index
        S.push(i);
    }

    // Print the required range using L and R array
    for (let i = 0; i < N; i++) {
        document.write(L[i] + 1 + " ")
        document.write(R[i] + 1 + "<br>");
    }
}

// Driver Code

// Given Input
let arr = [1, 3, 2];
let N = arr.length;

// Function Call
rangeFinder(arr, N);

</script>
```

**输出:**

```
1 3
2 2
2 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)