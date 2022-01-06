# 所有可能子阵列中最大和第二大元素的最大异或值

> 原文:[https://www . geesforgeks . org/max-xor-value-of-maximum-second-maximum-element-in-all-可能的子数组/](https://www.geeksforgeeks.org/maximum-xor-value-of-maximum-and-second-maximum-element-among-all-possible-subarrays/)

给定一个由 **N** 个不同正整数组成的数组 **arr[]** ，让我们将 **max(i，j)** 和 **secondMax(i，j)** 表示为子数组**arr【I…j】**的最大值和第二大值元素。任务是为 **i** 和 **j** 的所有可能值找到 **max(i，j) XOR secondMax(i，j)** 的最大值。**注意**子阵列的尺寸必须至少为两个。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 3
> {1，2}、{2，3}和{1，2，3}是唯一有效的子阵。
> 显然，所需的异或值分别为 3、1 和 1。
> **输入:** arr[] = {1，8，2}
> **输出:** 9

**天真的方法:**天真的方法将是简单地逐个迭代所有子阵列，然后找到所需的值。这种方法需要 **O(N <sup>3</sup> )** 的时间复杂度。
**有效方法:**让 **arr[i]** 成为某个子阵列的第二个最大元素，那么最大元素可以是向前或向后方向大于 **arr[i]** 的第一个元素。
因此，可以表明，除了第一个和最后一个元素之外，每个元素最多只能充当第二个最大元素 2 次。现在，只需计算向前和向后方向上每个元素的下一个更大的元素，并返回它们的最大异或。本文中描述了一种使用堆栈查找下一个更大元素的方法。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum possible xor
int maximumXor(int arr[], int n)
{
    stack<int> sForward, sBackward;

    // To store the final answer
    int ans = -1;

    for (int i = 0; i < n; i++) {

        // Borward traversal
        while (!sForward.empty()
               && arr[i] < arr[sForward.top()]) {
            ans = max(ans, arr[i] ^ arr[sForward.top()]);
            sForward.pop();
        }
        sForward.push(i);

        // Backward traversal
        while (!sBackward.empty()
               && arr[n - i - 1] < arr[sBackward.top()]) {
            ans = max(ans, arr[n - i - 1] ^ arr[sBackward.top()]);
            sBackward.pop();
        }

        sBackward.push(n - i - 1);
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maximumXor(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the maximum possible xor
static int maximumXor(int arr[], int n)
{
    Stack<Integer> sForward = new Stack<Integer>(),
            sBackward = new Stack<Integer>();

    // To store the final answer
    int ans = -1;

    for (int i = 0; i < n; i++)
    {

        // Borward traversal
        while (!sForward.isEmpty()
            && arr[i] < arr[sForward.peek()])
        {
            ans = Math.max(ans, arr[i] ^ arr[sForward.peek()]);
            sForward.pop();
        }
        sForward.add(i);

        // Backward traversal
        while (!sBackward.isEmpty()
            && arr[n - i - 1] < arr[sBackward.peek()])
        {
            ans = Math.max(ans, arr[n - i - 1] ^ arr[sBackward.peek()]);
            sBackward.pop();
        }

        sBackward.add(n - i - 1);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 1, 2 };
    int n = arr.length;

    System.out.print(maximumXor(arr, n));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum possible xor
def maximumXor(arr: list, n: int) -> int:
    sForward, sBackward = [], []

    # To store the final answer
    ans = -1

    for i in range(n):

        # Borward traversal
        while len(sForward) > 0 and arr[i] < arr[sForward[-1]]:
            ans = max(ans, arr[i] ^ arr[sForward[-1]])
            sForward.pop()

        sForward.append(i)

        # Backward traversal
        while len(sBackward) > 0 and arr[n - i - 1] < arr[sBackward[-1]]:
            ans = max(ans, arr[n - i - 1] ^ arr[sBackward[-1]])
            sBackward.pop()

        sBackward.append(n - i - 1)

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [8, 1, 2]
    n = len(arr)
    print(maximumXor(arr, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the maximum possible xor
static int maximumXor(int []arr, int n)
{
    Stack<int> sForward = new Stack<int>(),
            sBackward = new Stack<int>();

    // To store the readonly answer
    int ans = -1;

    for (int i = 0; i < n; i++)
    {

        // Borward traversal
        while (sForward.Count != 0
            && arr[i] < arr[sForward.Peek()])
        {
            ans = Math.Max(ans, arr[i] ^ arr[sForward.Peek()]);
            sForward.Pop();
        }
        sForward.Push(i);

        // Backward traversal
        while (sBackward.Count != 0
            && arr[n - i - 1] < arr[sBackward.Peek()])
        {
            ans = Math.Max(ans, arr[n - i - 1] ^ arr[sBackward.Peek()]);
            sBackward.Pop();
        }

        sBackward.Push(n - i - 1);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 1, 2 };
    int n = arr.Length;

    Console.Write(maximumXor(arr, n));

}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximum possible xor
    function maximumXor(arr, n)
    {
        let sForward = [];
          let sBackward = [];

        // To store the readonly answer
        let ans = -1;

        for (let i = 0; i < n; i++)
        {

            // Borward traversal
            while (sForward.length != 0
                && arr[i] < arr[sForward[sForward.length - 1]])
            {
                ans = Math.max(ans, arr[i] ^ arr[sForward[sForward.length - 1]]);
                sForward.pop();
            }
            sForward.push(i);

            // Backward traversal
            while (sBackward.length != 0
                && arr[n - i - 1] < arr[sBackward[sBackward.length - 1]])
            {
                ans = Math.max(ans, arr[n - i - 1] ^ arr[sBackward[sBackward.length - 1]]);
                sBackward.pop();
            }

            sBackward.push(n - i - 1);
        }
        return ans;
    }

    let arr = [ 8, 1, 2 ];
    let n = arr.length;

    document.write(maximumXor(arr, n));

    // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
9
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)。