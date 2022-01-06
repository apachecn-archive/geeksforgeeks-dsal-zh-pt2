# 子阵和与其最小元素的乘积最大化

> 原文:[https://www . geeksforgeeks . org/subarray 的最大乘积与其最小元素之和/](https://www.geeksforgeeks.org/maximize-product-of-subarray-sum-with-its-minimum-element/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出子阵和与该子阵的最小元素的最大乘积。

**示例:**

> **输入:** arr[] = {3，1，6，4，5，2}
> **输出:** 60
> **解释:**
> 使用子阵列{6，4，5}
> 可以得到所需的最大乘积因此，最大乘积= (6 + 4 + 5) * (4) = 60
> 
> **输入:** arr[] = {4，1，2，9，3}
> **输出:** 81
> **解释:**
> 使用子阵列{9}
> 最大乘积= (9)* (9) = 81 可以获得所需的最大乘积

**天真法:**解决问题最简单的方法是[生成给定阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有子阵列，对于每个子阵列，计算子阵列的[和，并与子阵列中的最小元素相乘。通过与计算的产品进行比较，更新最大产品。最后，打印处理所有子阵列后获得的最大产品。](https://www.geeksforgeeks.org/sum-of-all-subarrays/)

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)和[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)进行优化。其思想是使用堆栈来获取每个元素左侧和右侧[最近的较小元素的索引。现在，使用这些，可以获得所需的产品。按照以下步骤解决问题:](https://www.geeksforgeeks.org/find-the-nearest-smaller-numbers-on-left-side-in-an-array/)

*   初始化数组**假定[]** 存储给定数组的所有结果前缀和数组。
*   初始化两个数组 **l[]** 和 **r[]** ，分别存储最近的左右较小元素的索引。
*   对于每个元素**arr【I】**，使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)计算**l【I】**和**r【I】**。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个索引 **i** ，可以通过以下方式计算乘积:

> arr[i] * （presum[r[i]] – presum[l[i]-1]）

*   完成以上所有步骤后，打印最大产品

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the
// maximum product possible
void maxValue(int a[], int n)
{

    // Stores prefix sum
    int presum[n];

    presum[0] = a[0];

    // Find the prefix sum array
    for(int i = 1; i < n; i++)
    {
        presum[i] = presum[i - 1] + a[i];
    }

    // l[] and r[] stores index of
    // nearest smaller elements on
    // left and right respectively
    int l[n], r[n];

    stack<int> st;

    // Find all left index
    for(int i = 1; i < n; i++)
    {

        // Until stack is non-empty
        // & top element is greater
        // than the current element
        while (!st.empty() &&
              a[st.top()] >= a[i])
            st.pop();

        // If stack is empty
        if (!st.empty())
            l[i] = st.top() + 1;
        else
            l[i] = 0;

        // Push the current index i
        st.push(i);
    }

    // Reset stack
    while(!st.empty())
    st.pop();

    // Find all right index
    for(int i = n - 1; i >= 0; i--)
    {

        // Until stack is non-empty
        // & top element is greater
        // than the current element
        while (!st.empty() &&
              a[st.top()] >= a[i])
            st.pop();

            if (!st.empty())
                r[i] = st.top() - 1;
            else
                r[i] = n - 1;

        // Push the current index i
        st.push(i);
    }

    // Stores the maximum product
    int maxProduct = 0;

    int tempProduct;

    // Iterate over the range [0, n)
    for(int i = 0; i < n; i++)
    {

        // Calculate the product
        tempProduct = a[i] * (presum[r[i]] -
                     (l[i] == 0 ? 0 :
                    presum[l[i] - 1]));

        // Update the maximum product
        maxProduct = max(maxProduct,
                        tempProduct);
    }

    // Return the maximum product
    cout << maxProduct;
}

// Driver Code
int main()
{

    // Given array
    int n = 6;
    int arr[] = { 3, 1, 6, 4, 5, 2 };

    // Function call
    maxValue(arr, n);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

class GFG {

    // Function to find the
    // maximum product possible
    public static void
    maxValue(int[] a, int n)
    {

        // Stores prefix sum
        int[] presum = new int[n];

        presum[0] = a[0];

        // Find the prefix sum array
        for (int i = 1; i < n; i++) {

            presum[i] = presum[i - 1] + a[i];
        }

        // l[] and r[] stores index of
        // nearest smaller elements on
        // left and right respectively
        int[] l = new int[n], r = new int[n];

        Stack<Integer> st = new Stack<>();

        // Find all left index
        for (int i = 1; i < n; i++) {

            // Until stack is non-empty
            // & top element is greater
            // than the current element
            while (!st.isEmpty()
                   && a[st.peek()] >= a[i])
                st.pop();

            // If stack is empty
            if (!st.isEmpty())
                l[i] = st.peek() + 1;
            else
                l[i] = 0;

            // Push the current index i
            st.push(i);
        }

        // Reset stack
        st.clear();

        // Find all right index
        for (int i = n - 1; i >= 0; i--) {

            // Until stack is non-empty
            // & top element is greater
            // than the current element
            while (!st.isEmpty()
                   && a[st.peek()] >= a[i])
                st.pop();

            if (!st.isEmpty())
                r[i] = st.peek() - 1;
            else
                r[i] = n - 1;

            // Push the current index i
            st.push(i);
        }

        // Stores the maximum product
        int maxProduct = 0;

        int tempProduct;

        // Iterate over the range [0, n)
        for (int i = 0; i < n; i++) {

            // Calculate the product
            tempProduct
                = a[i]
                  * (presum[r[i]]
                     - (l[i] == 0 ? 0
                                  : presum[l[i] - 1]));

            // Update the maximum product
            maxProduct
                = Math.max(maxProduct,
                           tempProduct);
        }

        // Return the maximum product
        System.out.println(maxProduct);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 3, 1, 6, 4, 5, 2 };

        // Function Call
        maxValue(arr, arr.length);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the
# maximum product possible
def maxValue(a, n):

    # Stores prefix sum
    presum = [0 for i in range(n)]

    presum[0] = a[0]

    # Find the prefix sum array
    for i in range(1, n, 1):
        presum[i] = presum[i - 1] + a[i]

    # l[] and r[] stores index of
    # nearest smaller elements on
    # left and right respectively
    l = [0 for i in range(n)]
    r = [0 for i in range(n)]

    st = []

    # Find all left index
    for i in range(1, n):

        # Until stack is non-empty
        # & top element is greater
        # than the current element
        while (len(st) and
          a[st[len(st) - 1]] >= a[i]):
            st.remove(st[len(st) - 1])

        # If stack is empty
        if (len(st)):
            l[i] = st[len(st) - 1] + 1;
        else:
            l[i] = 0

        # Push the current index i
        st.append(i)

    # Reset stack
    while(len(st)):
        st.remove(st[len(st) - 1])

    # Find all right index
    i = n - 1
    while(i >= 0):

        # Until stack is non-empty
        # & top element is greater
        # than the current element
        while (len(st) and
          a[st[len(st) - 1]] >= a[i]):
            st.remove(st[len(st) - 1])

            if (len(st)):
                r[i] = st[len(st) - 1] - 1
            else:
                r[i] = n - 1

        # Push the current index i
        st.append(i)
        i -= 1

    # Stores the maximum product
    maxProduct = 0

    # Iterate over the range [0, n)
    for i in range(n):

        # Calculate the product
        if l[i] == 0:
            tempProduct = (a[i] *
                    presum[r[i]])
        else:
            tempProduct = (a[i] *
                   (presum[r[i]] -
                    presum[l[i] - 1]))

        # Update the maximum product
        maxProduct = max(maxProduct,
                        tempProduct)

    # Return the maximum product
    print(maxProduct)

# Driver Code
if __name__ == '__main__':

    # Given array
    n = 6
    arr =  [ 3, 1, 6, 4, 5, 2 ]

    # Function call
    maxValue(arr, n)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the
// maximum product possible
public static void maxValue(int[] a,
                            int n)
{

    // Stores prefix sum
    int[] presum = new int[n];

    presum[0] = a[0];

    // Find the prefix sum array
    for(int i = 1; i < n; i++)
    {
        presum[i] = presum[i - 1] + a[i];
    }

    // l[] and r[] stores index of
    // nearest smaller elements on
    // left and right respectively
    int[] l = new int[n], r = new int[n];

    Stack<int> st = new Stack<int>();

    // Find all left index
    for(int i = 1; i < n; i++)
    {

        // Until stack is non-empty
        // & top element is greater
        // than the current element
        while (st.Count > 0 &&
           a[st.Peek()] >= a[i])
            st.Pop();

        // If stack is empty
        if (st.Count > 0)
            l[i] = st.Peek() + 1;
        else
            l[i] = 0;

        // Push the current index i
        st.Push(i);
    }

    // Reset stack
    st.Clear();

    // Find all right index
    for(int i = n - 1; i >= 0; i--)
    {

        // Until stack is non-empty
        // & top element is greater
        // than the current element
        while (st.Count > 0 &&
           a[st.Peek()] >= a[i])
            st.Pop();

        if (st.Count > 0)
            r[i] = st.Peek() - 1;
        else
            r[i] = n - 1;

        // Push the current index i
        st.Push(i);
    }

    // Stores the maximum product
    int maxProduct = 0;

    int tempProduct;

    // Iterate over the range [0, n)
    for(int i = 0; i < n; i++)
    {

        // Calculate the product
        tempProduct = a[i] * (presum[r[i]] -
                     (l[i] == 0 ? 0 :
                     presum[l[i] - 1]));

        // Update the maximum product
        maxProduct = Math.Max(maxProduct,
                             tempProduct);
    }

    // Return the maximum product
    Console.WriteLine(maxProduct);
}

// Driver code
static void Main()
{

    // Given array
    int[] arr = { 3, 1, 6, 4, 5, 2 };

    // Function call
    maxValue(arr, arr.Length);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
 // Javascript program to implement
// the above approach

// Function to find the
// maximum product possible
function maxValue(a, n)
{

    // Stores prefix sum
    var presum = Array(n);

    presum[0] = a[0];

    // Find the prefix sum array
    for(var i = 1; i < n; i++)
    {
        presum[i] = presum[i - 1] + a[i];
    }

    // l[] and r[] stores index of
    // nearest smaller elements on
    // left and right respectively
    var l = Array(n).fill(0), r = Array(n).fill(0);

    var st = [];

    // Find all left index
    for(var i = 1; i < n; i++)
    {

        // Until stack is non-empty
        // & top element is greater
        // than the current element
        while (st.length!=0 &&
              a[st[st.length-1]] >= a[i])
            st.pop();

        // If stack is empty
        if (st.length!=0)
            l[i] = st[st.length-1] + 1;
        else
            l[i] = 0;

        // Push the current index i
        st.push(i);
    }

    // Reset stack
    while(st.length!=0)
        st.pop();

    // Find all right index
    for(var i = n - 1; i >= 0; i--)
    {

        // Until stack is non-empty
        // & top element is greater
        // than the current element
        while (st.length!=0 &&
              a[st[st.length-1]] >= a[i])
            st.pop();

            if (st.length!=0)
                r[i] = st[st.length-1] - 1;
            else
                r[i] = n - 1;

        // Push the current index i
        st.push(i);
    }

    // Stores the maximum product
    var maxProduct = 0;

    var tempProduct;

    // Iterate over the range [0, n)
    for(var i = 0; i < n; i++)
    {

        // Calculate the product
        tempProduct = a[i] * (presum[r[i]] -
                     (l[i] == 0 ? 0 :
                    presum[l[i] - 1]));

        // Update the maximum product
        maxProduct = Math.max(maxProduct,
                        tempProduct);
    }

    // Return the maximum product
    document.write( maxProduct);
}

// Driver Code
// Given array
var n = 6;
var arr = [3, 1, 6, 4, 5, 2];
// Function call
maxValue(arr, n);

</script>
```

**Output:** 

```
60
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)