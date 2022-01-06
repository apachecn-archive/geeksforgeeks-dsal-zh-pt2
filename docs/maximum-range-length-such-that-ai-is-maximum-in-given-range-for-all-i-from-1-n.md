# 最大范围长度，使得 A[i]在从[1，N]

开始的所有 I 的给定范围内最大

> 原文:[https://www . geesforgeks . org/最大范围长度-这样-ai-is-最大给定范围-所有 i-from-1-n/](https://www.geeksforgeeks.org/maximum-range-length-such-that-ai-is-maximum-in-given-range-for-all-i-from-1-n/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。对于每个 **i** (0 ≤ i < n)，找到一个范围**【l，r】**，使得 **A[i] = max(A[l]，A[l+1]，…，A[r])** 和 **l ≤ i ≤ r** 和 **r-l** 最大化。

**示例:**

> **输入:** arr[] = {1，3，2}
> **输出:** {0 0}、{0 2}、{2 2}
> **说明:**对于 i=0，1 仅在[0，0]范围内最大。对于 i=1，3 在范围[0，2]内最大，对于 i = 2，2 仅在范围[2，2]内最大。
> 
> **输入:** arr[] = {1，2}
> **输出:** {0，0}，{0，1}

**天真方法:**解决问题最简单的方法是对每个 **i** 、[使用变量 **r** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)、**【I+1，N-1】**和[使用变量 **l** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)T12【I-1，0】并在**arr【l】>arr【I】**时终止循环答案是**【l，r】**。

***时间复杂度:** O(N×N)*
***辅助空间:** O(1)*

**高效方法:**通过使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)，可以进一步优化上述方法。按照以下步骤解决问题:

*   初始化两个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**左**和**右**，分别存储每个 **i** 的左索引和右索引。
*   初始化一堆[对](https://www.geeksforgeeks.org/stack-of-pair-in-c-stl-with-examples/)，比如 **s** 。
*   将 **INT_MAX** 和 **-1** 作为一对插入堆栈中。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   而 **s.top()。首先< arr[i]** ，从堆栈中弹出顶部元素。
    *   将**左侧【I】**的值修改为 **s.top()。第二**。
    *   在[栈](https://www.geeksforgeeks.org/stack-data-structure/)中推 **{arr[i]，i}** 。
*   现在从堆栈中移除所有元素。
*   将 **INT_MAX** 和 **N** 成对插入堆栈中。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代，并执行以下步骤:
    *   而 **s.top()。首先< arr[i]** ，从堆栈中弹出顶部元素。
    *   将**右侧【I】**的值修改为 **s.top()。第二**。
    *   在[栈](https://www.geeksforgeeks.org/stack-data-structure/)中推 **{arr[i]，i}** 。
*   [使用变量 **i** 在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**范围内迭代，打印**左【I】+1**、**右【I】-1**作为带有元素的**的答案。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum range for
// each i such that arr[i] is max in range
void MaxRange(vector<int> A, int n)
{
    // Vector to store the left and right index
    // for each i such that left[i]>arr[i]
    // and right[i] > arr[i]
    vector<int> left(n), right(n);

    stack<pair<int, int> > s;
    s.push({ INT_MAX, -1 });

    // Traverse the array
    for (int i = 0; i < n; i++) {
        // While s.top().first<a[i]
        // remove the top element from
        // the stack
        while (s.top().first < A[i])
            s.pop();

        // Modify left[i]
        left[i] = s.top().second;
        s.push({ A[i], i });
    }
    // Clear the stack
    while (!s.empty())
        s.pop();
    s.push(make_pair(INT_MAX, n));

    // Traverse the array to find
    // right[i] for each i
    for (int i = n - 1; i >= 0; i--) {
        // While s.top().first<a[i]
        // remove the top element from
        // the stack
        while (s.top().first < A[i])
            s.pop();

        // Modify right[i]
        right[i] = s.top().second;
        s.push({ A[i], i });
    }

    // Print the value range for each i
    for (int i = 0; i < n; i++) {
        cout << left[i] + 1 << ' ' << right[i] - 1 << "\n";
    }
}

// Driver Code
int main()
{
    // Given Input
    vector<int> arr{ 1, 3, 2 };
    int n = arr.size();

    // Function Call
    MaxRange(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program for above approach
import java.awt.*;
import java.util.*;
class GFG{
    static class pair<T, V>{
        T first;
        V second;
    }

    // Function to find maximum range for
    // each i such that arr[i] is max in range
    static void MaxRange(ArrayList<Integer> A, int n)
    {
        // Vector to store the left and right index
        // for each i such that left[i]>arr[i]
        // and right[i] > arr[i]

        int[] left = new int[n];
        int[] right = new int[n];

        Stack<pair<Integer,Integer>> s = new Stack<>();
        pair<Integer,Integer> x = new pair<>();
        x.first =Integer.MAX_VALUE;
        x.second = -1;
        s.push(x);

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // While s.top().first<a[i]
            // remove the top element from
            // the stack
            while (s.peek().first < A.get(i))
                s.pop();

            // Modify left[i]
            left[i] = s.peek().second;
            pair<Integer,Integer> y = new pair<>();
            y.first = A.get(i);
            y.second = i;
            s.push(y);
        }

        // Clear the stack
        while (!s.empty())
            s.pop();
        pair<Integer,Integer> k = new pair<>();
        k.first =Integer.MAX_VALUE;
        k.second = n;
        s.push(k);

        // Traverse the array to find
        // right[i] for each i
        for (int i = n - 1; i >= 0; i--)
        {

            // While s.top().first<a[i]
            // remove the top element from
            // the stack
            while (s.peek().first < A.get(i))
                s.pop();

            // Modify right[i]
            right[i] = s.peek().second;
            pair<Integer,Integer> y = new pair<>();
            y.first = A.get(i);
            y.second = i;
            s.push(y);
        }

        // Print the value range for each i
        for (int i = 0; i < n; i++) {
            System.out.print(left[i]+1);
            System.out.print(" ");
            System.out.println(right[i]-1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        ArrayList<Integer> arr = new ArrayList<>();
        arr.add(1);
        arr.add(3);
        arr.add(2);
        int n = arr.size();

        // Function Call
        MaxRange(arr, n);
    }
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function to find maximum range for
# each i such that arr[i] is max in range
def MaxRange(A, n):

    # Vector to store the left and right index
    # for each i such that left[i]>arr[i]
    # and right[i] > arr[i]
    left = [0] * n
    right = [0] * n

    s = []
    s.append((sys.maxsize, -1))

    # Traverse the array
    for i in range(n):

        # While s.top().first<a[i]
        # remove the top element from
        # the stack
        while (s[-1][0] < A[i]):
            s.pop()

        # Modify left[i]
        left[i] = s[-1][1]
        s.append((A[i], i))

    # Clear the stack
    while (len(s) != 0):
        s.pop()
    s.append((sys.maxsize, n))

    # Traverse the array to find
    # right[i] for each i
    for i in range(n - 1, -1, -1):

        # While s.top().first<a[i]
        # remove the top element from
        # the stack
        while (s[-1][0] < A[i]):
            s.pop()

        # Modify right[i]
        right[i] = s[-1][1]
        s.append((A[i], i))

    # Print the value range for each i
    for i in range(n):
        print(left[i] + 1, ' ', right[i] - 1)

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [1, 3, 2]
    n = len(arr)

    # Function Call
    MaxRange(arr, n)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach.
using System;
using System.Collections;
using System.Collections.Generic;
class GFG
{

    // Function to find maximum range for
    // each i such that arr[i] is max in range
    static void MaxRange(List<int> A, int n)
    {
        // Vector to store the left and right index
        // for each i such that left[i]>arr[i]
        // and right[i] > arr[i]
        int[] left = new int[n];
        int[] right = new int[n];

        Stack s = new Stack();
        s.Push(new Tuple<int, int>(Int32.MaxValue, -1));

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // While s.top().first<a[i]
            // remove the top element from
            // the stack
            while (((Tuple<int, int>)s.Peek()).Item1 < A[i])
                s.Pop();

            // Modify left[i]
            left[i] = ((Tuple<int, int>)s.Peek()).Item2;
            s.Push(new Tuple<int, int>(A[i], i));
        }
        // Clear the stack
        while (s.Count > 0)
            s.Pop();
        s.Push(new Tuple<int, int>(Int32.MaxValue, n));

        // Traverse the array to find
        // right[i] for each i
        for (int i = n - 1; i >= 0; i--) {
            // While s.top().first<a[i]
            // remove the top element from
            // the stack
            while (((Tuple<int, int>)s.Peek()).Item1 < A[i])
                s.Pop();

            // Modify right[i]
            right[i] = ((Tuple<int, int>)s.Peek()).Item2;
            s.Push(new Tuple<int, int>(A[i], i));
        }

        // Print the value range for each i
        for (int i = 0; i < n; i++) {
            Console.WriteLine((left[i] + 1) + " " + (right[i] - 1));
        }
    }

  static void Main ()
  {
    List<int> arr = new List<int>();

    // adding elements in firstlist
    arr.Add(1);
    arr.Add(3);
    arr.Add(2);

    int n = arr.Count;

    // Function Call
    MaxRange(arr, n);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find maximum range for
// each i such that arr[i] is max in range
function MaxRange(A, n)
{

    // Vector to store the left and right index
    // for each i such that left[i]>arr[i]
    // and right[i] > arr[i]
    let left = new Array(n).fill(0),
       right = new Array(n).fill(0);

    let s = [];
    s.push([Number.MAX_SAFE_INTEGER, -1]);

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // While s.top()[0]<a[i]
        // remove the top element from
        // the stack
        while (s[s.length - 1][0] < A[i])
            s.pop();

        // Modify left[i]
        left[i] = s[s.length - 1][1];
        s.push([A[i], i]);
    }

    // Clear the stack
    while (s.length)
        s.pop();

    s.push([Number.MAX_SAFE_INTEGER, n]);

    // Traverse the array to find
    // right[i] for each i
    for(let i = n - 1; i >= 0; i--)
    {

        // While s.top()[0]<a[i]
        // remove the top element from
        // the stack
        while (s[s.length - 1][0] < A[i])
            s.pop();

        // Modify right[i]
        right[i] = s[s.length - 1][1];
        s.push([A[i], i]);
    }

    // Print the value range for each i
    for(let i = 0; i < n; i++)
    {
        document.write(left[i] + 1 + " ")
        document.write(right[i] - 1 + "<br>")
    }
}

// Driver Code

// Given Input
let arr = [ 1, 3, 2 ];
let n = arr.length;

// Function Call
MaxRange(arr, n);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
0 0
0 2
2 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)