# 所有子阵列的第一个和第二个最大值的异或最大值

> 原文:[https://www . geeksforgeeks . org/所有子阵列的第一和第二最大异或数/](https://www.geeksforgeeks.org/maximum-of-xor-of-first-and-second-maximum-of-all-subarrays/)

给定不同元素的数组 **arr[]** ，任务是找到每个可能子数组的第一个和第二个最大元素的异或值的最大值。
**注:**阵长大于 1。
**例:**

> **输入:** arr[] = {5，4，3}
> **输出:** 7
> **解释:**
> 长度大于 1 的所有可能子阵列及其第一和第二最大元素的 XOR 值–
> 第一和第二最大值({5，4})的 XOR = 1
> 第一和第二最大值({5，4，3})的 XOR = 1
> 第一和第二最大值({4，3 })= 7

**天真方法:**生成长度大于 1 的所有可能的子阵列，对于每个可能的子阵列，找到子阵列的第一个和第二个最大元素的异或值，并从中找出最大值。
**有效方法:**对于此问题，维护一个堆栈，并遵循给定的步骤–

*   从左到右遍历给定的数组，然后对于每个元素 arr[I]–
    1.  如果栈顶小于 arr[i]，则从栈中弹出元素，直到栈顶小于 arr[i]。
    2.  将 arr[i]推入堆栈。
    3.  找出堆栈前两个元素的异或值，如果当前异或值大于找到的最大值，则更新最大值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach.

#include <bits/stdc++.h>

using namespace std;

// Function to find the maximum XOR value
int findMaxXOR(vector<int> arr, int n){

    vector<int> stack;
    int res = 0, l = 0, i;

    // Traversing given array
    for (i = 0; i < n; i++) {

        // If there are elements in stack
        // and top of stack is less than
        // current element then pop the elements
        while (!stack.empty() &&
                stack.back() < arr[i]) {
            stack.pop_back();
            l--;
        }

        // Push current element
        stack.push_back(arr[i]);

        // Increasing length of stack
        l++;
        if (l > 1) {
            // Updating the maximum result
            res = max(res,
             stack[l - 1] ^ stack[l - 2]);
        }
    }

    return res;
}

// Driver Code
int main()
{
    // Initializing array
    vector<int> arr{ 9, 8, 3, 5, 7 };
    int result1 = findMaxXOR(arr, 5);

    // Reversing the array(vector)
    reverse(arr.begin(), arr.end());

    int result2 = findMaxXOR(arr, 5);

    cout << max(result1, result2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
import java.util.*;

class GFG{

// Function to find the maximum XOR value
static int findMaxXOR(Vector<Integer> arr, int n){

    Vector<Integer> stack = new Vector<Integer>();
    int res = 0, l = 0, i;

    // Traversing given array
    for (i = 0; i < n; i++) {

        // If there are elements in stack
        // and top of stack is less than
        // current element then pop the elements
        while (!stack.isEmpty() &&
                stack.get(stack.size()-1) < arr.get(i)) {
            stack.remove(stack.size()-1);
            l--;
        }

        // Push current element
        stack.add(arr.get(i));

        // Increasing length of stack
        l++;
        if (l > 1) {

            // Updating the maximum result
            res = Math.max(res,
            stack.get(l - 1) ^ stack.get(l - 2));
        }
    }

    return res;
}

// Driver Code
public static void main(String[] args)
{
    // Initializing array
    Integer []temp = { 9, 8, 3, 5, 7 };
    Vector<Integer> arr = new Vector<>(Arrays.asList(temp));
    int result1 = findMaxXOR(arr, 5);

    // Reversing the array(vector)
    Collections.reverse(arr);

    int result2 = findMaxXOR(arr, 5);

    System.out.print(Math.max(result1, result2));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python implementation of the approach

from collections import deque

def maxXOR(arr):
    # Declaring stack
    stack = deque()

    # Initializing the length of stack
    l = 0

    # Initializing res1 for array
    # traversal of left to right
    res1 = 0

    # Traversing the array
    for i in arr:

        # If there are elements in stack
        # And top of stack is less than
        # current element then pop the stack
        while stack and stack[-1]<i:
            stack.pop()
            # Simultaneously decrease the
            # length of stack
            l-= 1

        # Append the current element
        stack.append(i)
        # Increase the length of stack
        l+= 1

        # If there are atleast two elements
        # in stack If xor of top two elements
        # is maximum, we will update the res1
        if l>1:
            res1 = max(res1, stack[-1]^stack[-2])

    # Similar to the above method,
    # we calculate the xor for reversed array
    res2 = 0

    # Clear the whole stack
    stack.clear()
    l = 0

    # Reversing the array
    arr.reverse()
    for i in arr:
        while stack and stack[-1]<i:
            stack.pop()
            l-= 1

        stack.append(i)
        l+= 1
        if l>1:
            res2 = max(res2, stack[-1]^stack[-2])

    # Printing the maximum of res1, res2
    return max(res1, res2)

# Driver Code
if __name__ == "__main__":
    # Initializing the array
    arr = [9, 8, 3, 5, 7]
    print(maxXOR(arr))
```

## C#

```
// C# implementation of the above approach.
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum XOR value
static int findMaxXOR(List<int> arr, int n){

    List<int> stack = new List<int>();
    int res = 0, l = 0, i;

    // Traversing given array
    for (i = 0; i < n; i++) {

        // If there are elements in stack
        // and top of stack is less than
        // current element then pop the elements
        while (stack.Count!=0 &&
                stack[stack.Count-1] < arr[i]) {
            stack.RemoveAt(stack.Count-1);
            l--;
        }

        // Push current element
        stack.Add(arr[i]);

        // Increasing length of stack
        l++;
        if (l > 1) {

            // Updating the maximum result
            res = Math.Max(res,
            stack[l - 1] ^ stack[l - 2]);
        }
    }

    return res;
}

// Driver Code
public static void Main(String[] args)
{
    // Initializing array
    int []temp = { 9, 8, 3, 5, 7 };
    List<int> arr = new List<int>(temp);
    int result1 = findMaxXOR(arr, 5);

    // Reversing the array(vector)
    arr.Reverse();

    int result2 = findMaxXOR(arr, 5);

    Console.Write(Math.Max(result1, result2));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// C++ implementation of the above approach.

// Function to find the maximum XOR value
function findMaxXOR(arr, n){

    let stack = new Array();
    let res = 0, l = 0, i;

    // Traversing given array
    for (i = 0; i < n; i++) {

        // If there are elements in stack
        // and top of stack is less than
        // current element then pop the elements
        while (stack.length && stack[stack.length - 1] < arr[i]) {
            stack.pop();
            l--;
        }

        // Push current element
        stack.push(arr[i]);

        // Increasing length of stack
        l++;
        if (l > 1) {
            // Updating the maximum result
            res = Math.max(res,
            stack[l - 1] ^ stack[l - 2]);
        }
    }

    return res;
}

// Driver Code

    // Initializing array
    let arr = [ 9, 8, 3, 5, 7 ];
    let result1 = findMaxXOR(arr, 5);

    // Reversing the array(vector)
    arr.reverse();

    let result2 = findMaxXOR(arr, 5);

    document.write(Math.max(result1, result2));

    // This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
15
```