# 使用优先级队列

合并两个排序的数组

> 原文:[https://www . geesforgeks . org/merge-two-sorted-arrays-use-priority-queue/](https://www.geeksforgeeks.org/merge-two-sorted-arrays-using-priority-queue/)

给定大小分别为 **N** 和 **M** 的两个排序的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是以排序的方式合并它们。

**示例:**

> **输入:** A[] = { 5，6，8 }，B[] = { 4，7，8 }
> T3】输出: 4 5 6 7 8 8
> 
> **输入:** A[] = {1，3，4，5}，B] = {2，4，6，8 }
> T3】输出:1 2 3 4 5 6 8
> 
> **输入:** A[] = {5，8，9}，B[] = {4，7，8 }
> T3】输出: 4 5 7 8 8 9

**方法:**给定的问题，[使用 minheap](https://www.geeksforgeeks.org/merge-two-sorted-arrays-in-constant-space-using-min-heap/) 合并两个排序的数组已经存在。但是这里的想法是使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)来实现[最小堆](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)由 [STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 提供。按照以下步骤解决问题:

*   初始化一个 [min 优先级队列](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)说 **PQ** 实现 [Min 堆。](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]，**将阵中所有元素推入 **PQ** 。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **B[]，**将阵中所有元素推入 **PQ** 。
*   现在将 **PQ** 的所有元素放入一个数组中，说**RES【】**T4】逐个弹出 **PQ** 的顶部元素。
*   最后打印排序后的数组 **res[]** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to merge two arrays
void merge(int A[], int B[], int N, int M)
{
    // Stores the merged array
    int res[N + M];

    // Create a min priority_queue
    priority_queue<int, vector<int>, greater<int> > pq;

    // Traverse the array A[]
    for (int i = 0; i < N; i++)
        pq.push(A[i]);

    // Traverse the array B[]
    for (int i = 0; i < M; i++)
        pq.push(B[i]);

    int j = 0;

    // Iterate until the
    // pq is not empty
    while (!pq.empty()) {

        // Stores the top element
        // of pq into res[j]
        res[j++] = pq.top();

        // Removes the top element
        pq.pop();
    }

    // Print the merged array
    for (int i = 0; i < N + M; i++)
        cout << res[i] << ' ';
}

// Driver Code
int main()
{

    // Input
    int A[] = { 5, 6, 8 };
    int B[] = { 4, 7, 8 };

    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function call
    merge(A, B, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to merge two arrays
static void merge(int A[], int B[], int N, int M)
{

    // Stores the merged array
    int []res = new int[N + M];

    // Create a min priority_queue
    Queue<Integer> pq = new PriorityQueue<>();

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
        pq.add(A[i]);

    // Traverse the array B[]
    for(int i = 0; i < M; i++)
        pq.add(B[i]);

    int j = 0;

    // Iterate until the
    // pq is not empty
    while (!pq.isEmpty())
    {

        // Stores the top element
        // of pq into res[j]
        res[j++] = pq.peek();

        // Removes the top element
        pq.remove();
    }

    // Print the merged array
    for(int i = 0; i < N + M; i++)
        System.out.print(res[i] + " ");
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int A[] = { 5, 6, 8 };
    int B[] = { 4, 7, 8 };

    int N = A.length;
    int M = B.length;

    // Function call
    merge(A, B, N, M);
}
}

// This code is contributed by todaysgaurav
```

## 蟒蛇 3

```
# Python3 program for the above approach
from queue import PriorityQueue

# Function to merge two arrays
def merge(A, B, N, M):

    # Stores the merged array
    res = [0 for i in range(N + M)]

    # Create a min priority_queue
    pq = PriorityQueue()

    # Traverse the array A[]
    for i in range(N):
        pq.put(A[i])

    # Traverse the array B[]
    for i in range(M):
        pq.put(B[i])

    j = 0

    # Iterate until the
    # pq is not empty
    while not pq.empty():

        # Removes the top element and
        # stores it into res[j]
        res[j] = pq.get()
        j += 1

    # Print the merged array
    for i in range(N + M):
        print(res[i], end = " ")

    # return back to main
    return

# Driver code
if __name__ == '__main__':

    # Input
    A = [ 5, 6, 8 ]
    B = [ 4, 7, 8 ]

    N = len(A)
    M = len(B)

    # Function call
    merge(A, B, N, M)

# This code is contributed by MuskanKalra1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to merge two arrays
function merge(A, B, N, M)
{

    // Stores the merged array
    var res = Array(N+M).fill(0);

    // Create a min priority_queue
    var pq = [];

    // Traverse the array A[]
    for (var i = 0; i < N; i++)
        pq.push(A[i]);

    // Traverse the array B[]
    for (var i = 0; i < M; i++)
        pq.push(B[i]);

    var j = 0;
    pq.sort((a,b)=>b-a);

    // Iterate until the
    // pq is not empty
    while (pq.length!=0) {

        // Stores the top element
        // of pq into res[j]
        res[j++] = pq[pq.length-1];

        // Removes the top element
        pq.pop();
        pq.sort((a,b)=>b-a);
    }

    // Print the merged array
    for (var i = 0; i < N + M; i++)
        document.write(res[i] + ' ');
}

// Driver Code
// Input
var A = [5, 6, 8];
var B = [4, 7, 8];
var N = A.length;
var M = B.length;

// Function call
merge(A, B, N, M);

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
4 5 6 7 8 8 
```

***时间复杂度:**O((N+M)* log(N+M))*
***辅助空间:** O(N+M)*