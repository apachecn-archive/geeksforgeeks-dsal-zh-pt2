# 通过从给定阵列的子阵列的所有元素中减去相同的值来最大化总和

> 原文:[https://www . geeksforgeeks . org/通过从给定数组的所有子数组元素中减去相同的值来最大化可能的总和/](https://www.geeksforgeeks.org/maximize-sum-possible-by-subtracting-same-value-from-all-elements-of-a-subarray-of-the-given-array/)

给定一个由 **N** 个整数组成的数组**a【】**，任务是从一个子数组的所有元素中减去任意值，比如 **X** ，得到最大可能的和。

**示例:**

> **输入:** N = 3，a[] = {80，48，82}
> **输出:** 144
> **说明:**
> 48 可以从每个数组元素中扣除。因此，得到的和= 48 * 3 = 144
> **输入:** N = a[] = {8，40，77}
> **输出:** 80
> **解释:**
> 从所有数组元素中减去 8 生成和 24。
> 从 arr[1]和 arr[2]中减去 40 产生总和 80。
> 从 arr[2]中减去 77 产生总和 77。
> 因此，最大可能和为 80。

**方法:**
按照以下步骤解决问题:

*   遍历数组
*   对于每个元素，找出最靠近左边较小的和最靠近右边较小的的**元素。**
*   通过该元素计算***current _ element *(j–I–1)***计算可能的总和，其中 **j** 和 **i** 分别是左侧和右侧最近的较小数字的索引。
*   找出它们之间最大可能的和。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate previous smaller
// element for each array element
vector<int> findPrevious(vector<int> a, int n)
{
    vector<int> ps(n);

    // The first element has no
    // previous smaller
    ps[0] = -1;

    // Stack to keep track of elements
    // that have occurred previously
    stack<int> Stack;

    // Push the first index
    Stack.push(0);

    for(int i = 1; i < n; i++)
    {

        // Pop all the elements until the previous
        // element is smaller than current element
        while (Stack.size() > 0 &&
             a[Stack.top()] >= a[i])
            Stack.pop();

        // Store the previous smaller element
        ps[i] = Stack.size() > 0 ?
                Stack.top() : -1;

        // Push the index of the current element
        Stack.push(i);
    }

    // Return the array
    return ps;
}

// Function to generate next smaller element
// for each array element
vector<int> findNext(vector<int> a, int n)
{
    vector<int> ns(n);

    ns[n - 1] = n;

    // Stack to keep track of elements
    // that have occurring next
    stack<int> Stack;
    Stack.push(n - 1);

    // Iterate in reverse order
    // for calculating next smaller
    for(int i = n - 2; i >= 0; i--)
    {

        // Pop all the elements until the
        // next element is smaller
        // than current element
        while (Stack.size() > 0 &&
             a[Stack.top()] >= a[i])
            Stack.pop();

        // Store the next smaller element
        ns[i] = Stack.size() > 0 ?
                Stack.top() : n;

        // Push the index of the current element
        Stack.push(i);
    }

    // Return the array
    return ns;
}

// Function to find the maximum sum by
// subtracting same value from all
// elements of a Subarray
int findMaximumSum(vector<int> a, int n)
{

    // Stores previous smaller element
    vector<int> prev_smaller = findPrevious(a, n);

    // Stores next smaller element
    vector<int> next_smaller = findNext(a, n);

    int max_value = 0;
    for(int i = 0; i < n; i++)
    {

        // Calculate contribution
        // of each element
        max_value = max(max_value, a[i] *
                       (next_smaller[i] -
                        prev_smaller[i] - 1));
    }

    // Return answer
    return max_value;
}

// Driver Code   
int main()
{
    int n = 3;
    vector<int> a{ 80, 48, 82 };

    cout << findMaximumSum(a, n);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

public class GFG {

    // Function to find the maximum sum by
    // subtracting same value from all
    // elements of a Subarray
    public static int findMaximumSum(int[] a, int n)
    {
        // Stores previous smaller element
        int prev_smaller[] = findPrevious(a, n);

        // Stores next smaller element
        int next_smaller[] = findNext(a, n);

        int max_value = 0;
        for (int i = 0; i < n; i++) {

            // Calculate contribution
            // of each element
            max_value
                = Math.max(max_value,
                        a[i] * (next_smaller[i]
                                - prev_smaller[i] - 1));
        }

        // Return answer
        return max_value;
    }

    // Function to generate previous smaller element
    // for each array element
    public static int[] findPrevious(int[] a, int n)
    {
        int ps[] = new int[n];

        // The first element has no
        // previous smaller
        ps[0] = -1;

        // Stack to keep track of elements
        // that have occurred previously
        Stack<Integer> stack = new Stack<>();

        // Push the first index
        stack.push(0);
        for (int i = 1; i < a.length; i++) {

            // Pop all the elements until the previous
            // element is smaller than current element
            while (stack.size() > 0
                && a[stack.peek()] >= a[i])
                stack.pop();

            // Store the previous smaller element
            ps[i] = stack.size() > 0 ? stack.peek() : -1;

            // Push the index of the current element
            stack.push(i);
        }

        // Return the array
        return ps;
    }

    // Function to generate next smaller element
    // for each array element
    public static int[] findNext(int[] a, int n)
    {
        int ns[] = new int[n];

        ns[n - 1] = n;

        // Stack to keep track of elements
        // that have occurring next
        Stack<Integer> stack = new Stack<>();
        stack.push(n - 1);

        // Iterate in reverse order
        // for calculating next smaller
        for (int i = n - 2; i >= 0; i--) {

            // Pop all the elements until the
            // next element is smaller
            // than current element
            while (stack.size() > 0
                && a[stack.peek()] >= a[i])
                stack.pop();

            // Store the next smaller element
            ns[i] = stack.size() > 0 ? stack.peek()
                                    : a.length;

            // Push the index of the current element
            stack.push(i);
        }

        // Return the array
        return ns;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 3;
        int a[] = { 80, 48, 82 };
        System.out.println(findMaximumSum(a, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum by
# subtracting same value from all
# elements of a Subarray
def findMaximumSum(a, n):

    # Stores previous smaller element
    prev_smaller = findPrevious(a, n)

    # Stores next smaller element
    next_smaller = findNext(a, n)

    max_value = 0
    for i in range(n):

        # Calculate contribution
        # of each element
        max_value = max(max_value, a[i] *
                    (next_smaller[i] -
                        prev_smaller[i] - 1))

    # Return answer
    return max_value

# Function to generate previous smaller
# element for each array element
def findPrevious(a, n):

    ps = [0] * n

    # The first element has no
    # previous smaller
    ps[0] = -1

    # Stack to keep track of elements
    # that have occurred previously
    stack = []

    # Push the first index
    stack.append(0)

    for i in range(1, n):

        # Pop all the elements until the previous
        # element is smaller than current element
        while len(stack) > 0 and a[stack[-1]] >= a[i]:
            stack.pop()

        # Store the previous smaller element
        ps[i] = stack[-1] if len(stack) > 0 else -1

        # Push the index of the current element
        stack.append(i)

    # Return the array
    return ps

# Function to generate next smaller
# element for each array element
def findNext(a, n):

    ns = [0] * n
    ns[n - 1] = n

    # Stack to keep track of elements
    # that have occurring next
    stack = []
    stack.append(n - 1)

    # Iterate in reverse order
    # for calculating next smaller
    for i in range(n - 2, -1, -1):

        # Pop all the elements until the
        # next element is smaller
        # than current element
        while (len(stack) > 0 and
                a[stack[-1]] >= a[i]):
            stack.pop()

        # Store the next smaller element
        ns[i] = stack[-1] if len(stack) > 0 else n

        # Push the index of the current element
        stack.append(i)

    # Return the array
    return ns

# Driver code
n = 3
a = [ 80, 48, 82 ]

print(findMaximumSum(a, n))

# This code is contributed by Stuti Pathak
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the maximum sum by
// subtracting same value from all
// elements of a Subarray
public static int findMaximumSum(int[] a, int n)
{
    // Stores previous smaller element
    int []prev_smaller = findPrevious(a, n);

    // Stores next smaller element
    int []next_smaller = findNext(a, n);

    int max_value = 0;
    for (int i = 0; i < n; i++)
    {

    // Calculate contribution
    // of each element
    max_value = Math.Max(max_value,
                a[i] * (next_smaller[i] -
                        prev_smaller[i] - 1));
    }

    // Return answer
    return max_value;
}

// Function to generate previous smaller element
// for each array element
public static int[] findPrevious(int[] a, int n)
{
    int []ps = new int[n];

    // The first element has no
    // previous smaller
    ps[0] = -1;

    // Stack to keep track of elements
    // that have occurred previously
    Stack<int> stack = new Stack<int>();

    // Push the first index
    stack.Push(0);
    for (int i = 1; i < a.Length; i++)
    {

    // Pop all the elements until the previous
    // element is smaller than current element
    while (stack.Count > 0 &&
            a[stack.Peek()] >= a[i])
        stack.Pop();

    // Store the previous smaller element
    ps[i] = stack.Count > 0 ? stack.Peek() : -1;

    // Push the index of the current element
    stack.Push(i);
    }

    // Return the array
    return ps;
}

// Function to generate next smaller element
// for each array element
public static int[] findNext(int[] a, int n)
{
    int []ns = new int[n];

    ns[n - 1] = n;

    // Stack to keep track of elements
    // that have occurring next
    Stack<int> stack = new Stack<int>();
    stack.Push(n - 1);

    // Iterate in reverse order
    // for calculating next smaller
    for (int i = n - 2; i >= 0; i--)
    {

    // Pop all the elements until the
    // next element is smaller
    // than current element
    while (stack.Count > 0 &&
            a[stack.Peek()] >= a[i])
        stack.Pop();

    // Store the next smaller element
    ns[i] = stack.Count > 0 ? stack.Peek()
        : a.Length;

    // Push the index of the current element
    stack.Push(i);
    }

    // Return the array
    return ns;
}

// Driver Code
public static void Main(String []args)
{
    int n = 3;
    int []a = { 80, 48, 82 };
    Console.WriteLine(findMaximumSum(a, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript Program to implement
// the above approach

    // Function to find the maximum sum by
    // subtracting same value from all
    // elements of a Subarray
    function findMaximumSum(a ,n)
    {

        // Stores previous smaller element
        var prev_smaller = findPrevious(a, n);

        // Stores next smaller element
        var next_smaller = findNext(a, n);

        var max_value = 0;
        for (var i = 0; i < n; i++)
        {

            // Calculate contribution
            // of each element
            max_value = Math.max(max_value, a[i] * (next_smaller[i] - prev_smaller[i] - 1));
        }

        // Return answer
        return max_value;
    }

    // Function to generate previous smaller element
    // for each array element
      function findPrevious(a , n) {
        var ps = Array(n).fill(0);

        // The first element has no
        // previous smaller
        ps[0] = -1;

        // Stack to keep track of elements
        // that have occurred previously
        let stack = Array();

        // Push the first index
        stack.push(0);
        for (var i = 1; i < a.length; i++) {

            // Pop all the elements until the previous
            // element is smaller than current element
            while (stack.length > 0 && a[stack[stack.length-1]] >= a[i])
                stack.pop();

            // Store the previous smaller element
            ps[i] = stack.length > 0 ?stack[stack.length-1] : -1;

            // Push the index of the current element
            stack.push(i);
        }

        // Return the array
        return ps;
    }

    // Function to generate next smaller element
    // for each array element
      function findNext(a , n) {
        var ns = Array(n).fill(0);

        ns[n - 1] = n;

        // Stack to keep track of elements
        // that have occurring next
        var stack = Array();
        stack.push(n - 1);

        // Iterate in reverse order
        // for calculating next smaller
        for (var i = n - 2; i >= 0; i--) {

            // Pop all the elements until the
            // next element is smaller
            // than current element
            while (stack.length > 0 && a[stack[stack.length-1]] >= a[i])
                stack.pop();

            // Store the next smaller element
            ns[i] = stack.length > 0 ? stack[stack.length-1] : a.length;

            // Push the index of the current element
            stack.push(i);
        }

        // Return the array
        return ns;
    }

    // Driver Code
        var n = 3;
        var a = [ 80, 48, 82 ];
        document.write(findMaximumSum(a, n));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
144
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)