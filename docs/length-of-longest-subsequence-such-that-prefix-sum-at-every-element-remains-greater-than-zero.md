# 最长子序列的长度，使得每个元素的前缀和保持大于零

> 原文:[https://www . geeksforgeeks . org/最长子序列长度-每个元素的前缀总和-保持大于零/](https://www.geeksforgeeks.org/length-of-longest-subsequence-such-that-prefix-sum-at-every-element-remains-greater-than-zero/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-class-c/)**arr【】**和一个整数 **X，**的任务是找到[最长子序列](https://www.geeksforgeeks.org/longest-subsequence-such-that-difference-between-adjacents-is-one/)的长度，使得子序列的每个元素处的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)保持大于零。

**示例:**

> **输入:** arr[] = {-2，-1，1，2，-2}，N = 5
> **输出:** 3
> **说明:**序列可以由索引 2，3，4 处的元素组成。每个元素的前缀和都大于零:1，3，1
> 
> **输入:** arr[] = {-2，3，3，-7，-5，1}，N = 6
> T3】输出: 12

**方法:**给定的问题可以使用[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)方法来解决。想法是创建一个[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/) [优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)和[从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。将当前元素**arr【I】**加到**和**和 minheap 上，如果**和**变得小于零，则从 minheap 中去掉最负的元素，从**和**中减去。可以遵循以下方法来解决问题:

*   用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)数据结构初始化[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/)
*   初始化一个变量**和**来计算所需子序列的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并在每个元素**arr【I】**处将值添加到**和**及最小堆中
*   如果**和**的值小于零，从最小堆中移除最负的元素，并从**和**中减去该值
*   返回最小堆的大小作为最长子序列的长度

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate longest length
// of subsequence such that its prefix sum
// at every element stays greater than zero
int maxScore(int arr[], int N)
{
    // Variable to store the answer
    int score = 0;

    // Min heap implementation
    // using a priority queue
    priority_queue<int, vector<int>,
                   greater<int> >
        pq;

    // Variable to store the sum
    int sum = 0;
    for (int i = 0; i < N; i++) {

        // Add the current element
        // to the sum
        sum += arr[i];

        // Push the element in
        // the min-heap
        pq.push(arr[i]);

        // If the sum becomes less than
        // zero pop the top element of
        // the min-heap and subtract it
        // from the sum
        if (sum < 0) {
            int a = pq.top();
            sum -= a;
            pq.pop();
        }
    }

    // Return the answer
    return pq.size();
}

// Driver Code
int main()
{
    int arr[] = { -2, 3, 3, -7, -5, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxScore(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
import java.util.PriorityQueue;
class GFG
{

    // Function to calculate longest length
    // of subsequence such that its prefix sum
    // at every element stays greater than zero
    static int maxScore(int arr[], int N)
    {

        // Variable to store the answer
        int score = 0;

        // Min heap implementation
        // using a priority queue

        PriorityQueue<Integer> pq
            = new PriorityQueue<Integer>();

        // Variable to store the sum
        int sum = 0;
        for (int i = 0; i < N; i++) {

            // Add the current element
            // to the sum
            sum += arr[i];

            // Push the element in
            // the min-heap
            pq.add(arr[i]);

            // If the sum becomes less than
            // zero pop the top element of
            // the min-heap and subtract it
            // from the sum
            if (sum < 0) {
                int a = pq.poll();
                sum -= a;
            }
        }

        // Return the answer
        return pq.size();
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { -2, 3, 3, -7, -5, 1 };
        int N = arr.length;

        System.out.println(maxScore(arr, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python implementation for the above approach
from queue import PriorityQueue

# Function to calculate longest length
# of subsequence such that its prefix sum
# at every element stays greater than zero
def maxScore(arr, N):

    # Variable to store the answer
    score = 0;

    # Min heap implementation
    # using a priority queue
    pq = PriorityQueue();

    # Variable to store the sum
    sum = 0;
    for i in range(N) :

        # Add the current element
        # to the sum
        sum += arr[i];

        # Push the element in
        # the min-heap
        pq.put(arr[i]);

        # If the sum becomes less than
        # zero pop the top element of
        # the min-heap and subtract it
        # from the sum
        if (sum < 0):
            a = pq.queue[0]
            sum -= a;
            pq.get()

    # Return the answer
    return pq.qsize();

# Driver Code
arr = [ -2, 3, 3, -7, -5, 1 ];
N = len(arr)

print(maxScore(arr, N))

# This code is contributed by saurabh_jaiswal.
```

**Output**

```
4
```

**时间复杂度:** O(N * log N)
**辅助空间:** O(N)