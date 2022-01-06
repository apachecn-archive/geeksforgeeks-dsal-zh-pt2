# 所有前缀之和为负数的最长子序列的长度

> 原文:[https://www . geesforgeks . org/最长前缀为负和的子序列长度/](https://www.geeksforgeeks.org/length-of-the-longest-subsequence-with-negative-sum-of-all-prefixes/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到最长的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，使得子序列每个索引处的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)为负。

**示例:**

> **输入:** arr[] = {-1，-3，3，-5，8，2}
> 输出: 5
> **解释:**满足条件的最长子序列为{-1，-3，3，-5，2}。
> 
> **输入:** arr[] = {2，-5，2，-1，5，1，-9，10}
> **输出:** 6
> **说明:**满足条件的最长子序列为{-1，-3，3，-5，2}。

**方法:**使用[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)可以解决问题。按照以下步骤解决问题:

*   初始化一个优先级队列，比如说 **pq** ，和一个变量，比如说 **S** 作为 **0** ，以存储由元素直到索引 **i** 形成的子序列的元素，并存储优先级队列中元素的总和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   通过**arr【I】**和[将](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)**arr【I】**增加 **S** 为 **pq。**
    *   迭代直到 **S** 大于 **0** ，在每次迭代中，用 **pq** 的[顶元素](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)递减 **S** ，然后[弹出顶元素。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
*   最后，完成以上步骤后，打印 **pq.size()** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// of a subsequence such that prefix sum
// of any index is negative
int maxLengthSubsequence(int arr[], int N)
{
    // Max priority Queue
    priority_queue<int> pq;

    // Stores the temporary sum of a
    // prefix of selected subsequence
    int S = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // Increment S by arr[i]
        S += arr[i];

        // Push arr[i] into pq
        pq.push(arr[i]);

        // Iterate until S
        // is greater than 0
        while (S > 0) {

            // Decrement S by pq.top()
            S -= pq.top();

            // Pop the top element
            pq.pop();
        }
    }

    // Return the maxLength
    return pq.size();
}

// Driver Code
int main()
{
    // Given Input
    int arr[6] = { -1, -3, 3, -5, 8, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    // Function call
    cout << maxLengthSubsequence(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Collections;
import java.util.PriorityQueue;

public class GFG
{

    // Function to find the maximum length
    // of a subsequence such that prefix sum
    // of any index is negative
    static int maxLengthSubsequence(int arr[], int N)
    {

        // Max priority Queue
        PriorityQueue<Integer> pq = new PriorityQueue<>(
            Collections.reverseOrder());

        // Stores the temporary sum of a
        // prefix of selected subsequence
        int S = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++)
        {

            // Increment S by arr[i]
            S += arr[i];

            // Add arr[i] into pq
            pq.add(arr[i]);

            // Iterate until S
            // is greater than 0
            while (S > 0)
            {

                // Decrement S by pq.peek()
                S -= pq.peek();

                // Remove the top element
                pq.remove();
            }
        }

        // Return the maxLength
        return pq.size();
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { -1, -3, 3, -5, 8, 2 };
        int N = arr.length;

        // Function call
        System.out.println(maxLengthSubsequence(arr, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum length
# of a subsequence such that prefix sum
# of any index is negative
def maxLengthSubsequence(arr, N):

    # Max priority Queue
    pq = []

    # Stores the temporary sum of a
    # prefix of selected subsequence
    S = 0

    # Traverse the array arr[]
    for i in range(N):

        # Increment S by arr[i]
        S += arr[i]

        # Push arr[i] into pq
        pq.append(arr[i])

        # Iterate until S
        # is greater than 0
        pq.sort(reverse = False)

        while (S > 0):

            # Decrement S by pq.top()
            # pq.sort(reverse=False)
            S = S - max(pq)

            # Pop the top element
            pq = pq[1:]

        # print(len(pq))

    # Return the maxLength
    return len(pq)

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ -1, -3, 3, -5, 8, 2 ]
    N = len(arr)

    # Function call
    print(maxLengthSubsequence(arr, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum length
// of a subsequence such that prefix sum
// of any index is negative
static int maxLengthSubsequence(int []arr, int N)
{
    // Max priority Queue
    List<int> pq = new List<int>();

    // Stores the temporary sum of a
    // prefix of selected subsequence
    int S = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Increment S by arr[i]
        S += arr[i];

        // Push arr[i] into pq
        pq.Add(arr[i]);

        pq.Sort();
        // Iterate until S
        // is greater than 0
        while (S > 0) {
            pq.Sort();
            // Decrement S by pq.top()
            S -=  pq[pq.Count-1];

            // Pop the top element
            pq.RemoveAt(0);
        }
    }

    // Return the maxLength
    return pq.Count;
}

// Driver Code
public static void Main()
{

    // Given Input
    int []arr = { -1, -3, 3, -5, 8, 2 };
    int N = arr.Length;

    // Function call
    Console.Write(maxLengthSubsequence(arr, N));

}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum length
// of a subsequence such that prefix sum
// of any index is negative
function maxLengthSubsequence(arr, N) {
    // Max priority Queue
    let pq = new Array();

    // Stores the temporary sum of a
    // prefix of selected subsequence
    let S = 0;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

        // Increment S by arr[i]
        S += arr[i];

        // Push arr[i] into pq
        pq.push(arr[i]);

        pq.sort((a, b) => a - b);
        // Iterate until S
        // is greater than 0
        while (S > 0) {
            pq.sort((a, b) => a - b);
            // Decrement S by pq.top()
            S -= pq[pq.length - 1];

            // Pop the top element
            pq.shift();
        }
    }

    // Return the maxLength
    return pq.length;
}

// Driver Code

// Given Input
let arr = [-1, -3, 3, -5, 8, 2];
let N = arr.length;

// Function call
document.write(maxLengthSubsequence(arr, N));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*