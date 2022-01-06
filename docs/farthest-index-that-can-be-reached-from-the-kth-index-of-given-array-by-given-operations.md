# 通过给定操作从给定数组的第 k 个索引可以到达的最远索引

> 原文:[https://www . geeksforgeeks . org/从给定操作给定数组的第 k 个索引可以到达的最远索引/](https://www.geeksforgeeks.org/farthest-index-that-can-be-reached-from-the-kth-index-of-given-array-by-given-operations/)

给定一个由 **N** 个整数和三个整数 **X** 、 **Y** 和 **K** 组成的[数组 **arr[]** ，任务是通过以下操作找到最远的索引:](https://www.geeksforgeeks.org/array-data-structure/)

*   **如果 arr[i] ≥ arr[i + 1]:** 从索引 **i** 移动到 **i + 1** 。
*   **如果 arr[i] < arr[i+1]:** 如果 **X > 0** 的值为则递减 **X** 为 **1** ，如果 **Y** >的值为**(arr[I+1]–arr[I])**，则递减**Y**(arr[I+1]–arr[I])。

**示例:**

> **输入:** arr[] = {4，2，7，6，9，14，12}，X = 1，Y = 5，K = 0
> **输出:** 4
> **解释:**
> 最初，K = 0。
> arr[0] > arr[1]:因此，移至索引 1。
> arr[1]<arr[2]:X 减 1，移至索引 2。现在 X = 0。
> arr[2] > arr[3]:移至索引 3。
> arr[3]<arr[4]:Y 减 3，移至索引 4。现在 Y = 2
> arr[4] < arr[5]:既不是 X > 0 也不是 Y > 5。因此，不可能移动到下一个索引。
> 因此，能达到的最大指标是 4。
> 
> **输入:** arr[] = {14，3，19，3}，X = 17，Y = 0，K = 1
> **输出:** 3

**方法:**思路是用 **X** 表示指数之间的最大差值，用 **Y** 表示剩余差值。按照以下步骤解决此问题:

*   声明一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下操作:
    *   如果当前元素( **arr[i]** )大于下一个元素(**arr[I+1]【T3])，则移动到下一个索引。**
    *   否则，[将**(arr[I+1]–arr[I])**的差值推送到**优先级队列**中。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
    *   如果优先队列的[大小大于 **Y** ，则通过**优先队列**T9】的](https://www.geeksforgeeks.org/priority_queueempty-priority_queuesize-c-stl/)[顶元素递减 **X** ，并且**弹出**该元素。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
    *   如果 **X** 小于 **0** ，能达到的最远指标就是 **i** 。
*   完成上述步骤后，如果 **X** 的值为**至少为 0** ，则能达到的最远指标为**(N–1)**。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the farthest index
// that can be reached
void farthestHill(int arr[], int X,
                  int Y, int N, int K)
{
    int i, diff;

    // Declare a priority queue
    priority_queue<int> pq;

    // Iterate the array
    for (i = K; i < N - 1; i++) {

        // If current element is
        // greater than the next element
        if (arr[i] >= arr[i + 1])
            continue;

        // Otherwise, store their difference
        diff = arr[i + 1] - arr[i];

        // Push diff into pq
        pq.push(diff);

        // If size of pq exceeds Y
        if (pq.size() > Y) {

            // Decrease X by the
            // top element of pq
            X -= pq.top();

            // Remove top of pq
            pq.pop();
        }

        // If X is exhausted
        if (X < 0) {

            // Current index is the
            // farthest possible
            cout << i;
            return;
        }
    }

    // Print N-1 as farthest index
    cout << N - 1;
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 7, 6, 9, 14, 12 };
    int X = 5, Y = 1;
    int K = 0;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    farthestHill(arr, X, Y, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the farthest index
// that can be reached
public static void farthestHill(int arr[], int X,
                                int Y, int N, int K)
{
    int i, diff;

    // Declare a priority queue
    PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

    // Iterate the array
    for(i = K; i < N - 1; i++)
    {

        // If current element is
        // greater than the next element
        if (arr[i] >= arr[i + 1])
            continue;

        // Otherwise, store their difference
        diff = arr[i + 1] - arr[i];

        // Push diff into pq
        pq.add(diff);

        // If size of pq exceeds Y
        if (pq.size() > Y)
        {

            // Decrease X by the
            // top element of pq
            X -= pq.peek();

            // Remove top of pq
            pq.poll();
        }

        // If X is exhausted
        if (X < 0)
        {

            // Current index is the
            // farthest possible
            System.out.print(i);
            return;
        }
    }

    // Print N-1 as farthest index
    System.out.print(N - 1);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 2, 7, 6, 9, 14, 12 };
    int X = 5, Y = 1;
    int K = 0;
    int N = arr.length;

    // Function Call
    farthestHill(arr, X, Y, N, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the farthest index
# that can be reached
def farthestHill(arr, X, Y, N, K):

    # Declare a priority queue
    pq = []

    # Iterate the array
    for i in range(K, N - 1, 1):

        # If current element is
        # greater than the next element
        if (arr[i] >= arr[i + 1]):
            continue

        # Otherwise, store their difference
        diff = arr[i + 1] - arr[i]

        # Push diff into pq
        pq.append(diff)

        # If size of pq exceeds Y
        if (len(pq) > Y):

            # Decrease X by the
            # top element of pq
            X -= pq[-1]

            # Remove top of pq
            pq[-1]

        # If X is exhausted
        if (X < 0):

            # Current index is the
            # farthest possible
            print(i)
            return

    # Print N-1 as farthest index
    print(N - 1)

# Driver Code
arr = [ 4, 2, 7, 6, 9, 14, 12 ]
X = 5
Y = 1
K = 0
N = len(arr)

# Function Call
farthestHill(arr, X, Y, N, K)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the farthest index
// that can be reached
public static void farthestHill(int[] arr, int X,
                                int Y, int N, int K)
{
    int i, diff;

    // Declare a priority queue
    List<int> pq = new List<int>();

    // Iterate the array
    for(i = K; i < N - 1; i++)
    {

        // If current element is
        // greater than the next element
        if (arr[i] >= arr[i + 1])
            continue;

        // Otherwise, store their difference
        diff = arr[i + 1] - arr[i];

        // Push diff into pq
        pq.Add(diff);
        pq.Sort();
        pq.Reverse();

        // If size of pq exceeds Y
        if (pq.Count > Y)
        {

            // Decrease X by the
            // top element of pq
            X -= pq[0];

            // Remove top of pq
            pq.RemoveAt(0);
        }

        // If X is exhausted
        if (X < 0)
        {

            // Current index is the
            // farthest possible
            Console.Write(i);
            return;
        }
    }

    // Print N-1 as farthest index
    Console.Write(N - 1);
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 4, 2, 7, 6, 9, 14, 12 };
    int X = 5, Y = 1;
    int K = 0;
    int N = arr.Length;

    // Function Call
    farthestHill(arr, X, Y, N, K);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the farthest index
// that can be reached
function farthestHill(arr, X, Y, N, K)
{
    var i, diff;

    // Declare a priority queue
    var pq = [];

    // Iterate the array
    for(i = K; i < N - 1; i++)
    {

        // If current element is
        // greater than the next element
        if (arr[i] >= arr[i + 1])
            continue;

        // Otherwise, store their difference
        diff = arr[i + 1] - arr[i];

        // Push diff into pq
        pq.push(diff);
        pq.sort();
        pq = pq.reverse();

        // If size of pq exceeds Y
        if (pq.length > Y)
        {

            // Decrease X by the
            // top element of pq
            X -= pq[0];

            // Remove top of pq
            pq = pq.slice(1);
        }

        // If X is exhausted
        if (X < 0)
        {

            // Current index is the
            // farthest possible
            document.write(i);
            return;
        }
    }

    // Print N-1 as farthest index
    document.write(N - 1);
}

// Driver code
    var arr = [4, 2, 7, 6, 9, 14, 12];
    var X = 5, Y = 1;
    var K = 0;
    var N = arr.length;

    // Function Call
    farthestHill(arr, X, Y, N, K);

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log(E))，其中 E 是优先级队列中元素的最大数量。*
***辅助空间:** O(E)*