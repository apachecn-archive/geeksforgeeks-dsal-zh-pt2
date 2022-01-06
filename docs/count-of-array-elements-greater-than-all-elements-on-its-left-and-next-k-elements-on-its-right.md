# 数组元素的数量大于其左边的所有元素和右边的下一个 K 个元素

> 原文:[https://www . geesforgeks . org/数组元素计数-大于其左边的所有元素和其右边的下一个 k 元素/](https://www.geeksforgeeks.org/count-of-array-elements-greater-than-all-elements-on-its-left-and-next-k-elements-on-its-right/)

给定一个数组 **arr[]** ，任务是打印大于其左边所有元素以及大于其右边下一个 K 个元素的元素数。

**例:**

> **输入:** arr[] = { 4，2，3，6，4，3，2}，K = 2
> **输出:** 2
> **解释:**
> arr[0](= 4): arr[0]是数组中的第一个元素，大于其下一个 K(= 2)个元素{2，3}。
> arr[2](= 6): arr[2]大于其左侧的所有元素{4，2，3}，并大于其下一个 K(= 2)个元素{4，3}。
> 因此，只有两个元素满足给定条件。
> **输入:** arr[] = { 3，1，2，7，5，1，2，6}，K = 2
> **输出:** 2

**天真方法:**
遍历数组，对于每个元素，检查它左边的所有元素是否比它小，以及它右边的下一个 K 个元素是否比它小。对于每个这样的元素，增加**计数**。最后打印**计数**。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效途径:**
上述途径可以通过使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)进行优化。按照以下步骤解决问题:

1.  初始化一个新数组，并使用**堆栈**为每个数组元素存储[下一个更大元素](https://www.geeksforgeeks.org/next-greater-element/)的索引。
2.  遍历给定的数组，对于每个元素，检查它是否是目前为止获得的最大值，并且它的下一个更大的元素至少是当前索引之后的 **K** 个索引。如果发现是真的，增加**计数**。
3.  最后打印**计数**。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the count of
// Array elements greater than all
// elements on its left and next K
// elements on its right
int countElements(int arr[], int n,
                  int k)
{

    stack<int> s;

    vector<int> next_greater(n, n + 1);

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (s.empty()) {
            s.push(i);
            continue;
        }

        // If the stack is not empty and
        // the element at the top of the
        // stack is smaller than arr[i]
        while (!s.empty()
               && arr[s.top()] < arr[i]) {
            // Store the index of next
            // greater element
            next_greater[s.top()] = i;

            // Pop the top element
            s.pop();
        }

        // Insert the current index
        s.push(i);
    }

    // Stores the count
    int count = 0;
    int maxi = INT_MIN;
    for (int i = 0; i < n; i++) {
        if (next_greater[i] - i > k
            && maxi < arr[i]) {
            maxi = max(maxi, arr[i]);
            count++;
        }
    }

    return count;
}

// Driver Code
int main()
{

    int arr[] = { 4, 2, 3, 6, 4, 3, 2 };
    int K = 2;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countElements(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print the count of
// Array elements greater than all
// elements on its left and next K
// elements on its right
static int countElements(int arr[], int n,
                                    int k)
{
    Stack<Integer> s = new Stack<Integer>();

    int []next_greater = new int[n + 1];
    Arrays.fill(next_greater, n);

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        if (s.isEmpty())
        {
            s.add(i);
            continue;
        }

        // If the stack is not empty and
        // the element at the top of the
        // stack is smaller than arr[i]
        while (!s.isEmpty() &&
               arr[s.peek()] < arr[i])
        {

            // Store the index of next
            // greater element
            next_greater[s.peek()] = i;

            // Pop the top element
            s.pop();
        }

        // Insert the current index
        s.add(i);
    }

    // Stores the count
    int count = 0;
    int maxi = Integer.MIN_VALUE;

    for(int i = 0; i < n; i++)
    {
        if (next_greater[i] - i > k &&
              maxi < arr[i])
        {
            maxi = Math.max(maxi, arr[i]);
            count++;
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 2, 3, 6, 4, 3, 2 };
    int K = 2;
    int n = arr.length;

    System.out.print(countElements(arr, n, K));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to print the count of
# Array elements greater than all
# elements on its left and next K
# elements on its right
def countElements(arr, n, k):

    s = []

    next_greater = [n] * (n + 1)

    # Iterate over the array
    for i in range(n):
        if(len(s) == 0):
            s.append(i)
            continue

        # If the stack is not empty and
        # the element at the top of the
        # stack is smaller than arr[i]
        while(len(s) != 0 and
              arr[s[-1]] < arr[i]):

            # Store the index of next
            # greater element
            next_greater[s[-1]] = i

            # Pop the top element
            s.pop(-1)

        # Insert the current index
        s.append(i)

    # Stores the count
    count = 0
    maxi = -sys.maxsize - 1

    for i in range(n):
        if(next_greater[i] - i > k and
             maxi < arr[i]):
            maxi = max(maxi, arr[i])
            count += 1

    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 4, 2, 3, 6, 4, 3, 2 ]
    K = 2
    n = len(arr)

    # Function call
    print(countElements(arr, n, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the count of
// Array elements greater than all
// elements on its left and next K
// elements on its right
static int countElements(int[] arr, int n,
                         int k)
{
    Stack<int> s = new Stack<int>();

    int[] next_greater = new int[n + 1];
    Array.Fill(next_greater, n);

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        if (s.Count == 0)
        {
            s.Push(i);
            continue;
        }

        // If the stack is not empty and
        // the element at the top of the
        // stack is smaller than arr[i]
        while (s.Count != 0 &&
               arr[s.Peek()] < arr[i])
        {

            // Store the index of next
            // greater element
            next_greater[s.Peek()] = i;

            // Pop the top element
            s.Pop();
        }

        // Insert the current index
        s.Push(i);
    }

    // Stores the count
    int count = 0;
    int maxi = Int32.MinValue;

    for(int i = 0; i < n; i++)
    {
        if (next_greater[i] - i > k &&
                       maxi < arr[i])
        {
            maxi = Math.Max(maxi, arr[i]);
            count++;
        }
    }
    return count;
}

// Driver Code
static void Main()
{
    int[] arr = { 4, 2, 3, 6, 4, 3, 2 };
    int K = 2;
    int n = arr.Length;

    Console.Write(countElements(arr, n, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach

      // Function to print the count of
      // Array elements greater than all
      // elements on its left and next K
      // elements on its right
      function countElements(arr, n, k) {
        var s = [];

        var next_greater = new Array(n + 1).fill(n);

        // Iterate over the array
        for (var i = 0; i < n; i++) {
          if (s.length === 0) {
            s.push(i);
            continue;
          }

          // If the stack is not empty and
          // the element at the top of the
          // stack is smaller than arr[i]
          while (s.length !== 0 && arr[s[s.length - 1]] <
          arr[i]) {
            // Store the index of next
            // greater element
            next_greater[s[s.length - 1]] = i;

            // Pop the top element
            s.pop();
          }

          // Insert the current index
          s.push(i);
        }

        // Stores the count
        var count = 0;
        //min integer value
        var maxi = -2147483648;

        for (var i = 0; i < n; i++) {
          if (next_greater[i] - i > k && maxi < arr[i]) {
            maxi = Math.max(maxi, arr[i]);
            count++;
          }
        }
        return count;
      }

      // Driver Code
      var arr = [4, 2, 3, 6, 4, 3, 2];
      var K = 2;
      var n = arr.length;

      document.write(countElements(arr, n, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*