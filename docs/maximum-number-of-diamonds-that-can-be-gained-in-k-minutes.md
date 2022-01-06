# K 分钟内可以获得的最大钻石数量

> 原文:[https://www . geesforgeks . org/k 分钟内可获得的最大钻石数量/](https://www.geeksforgeeks.org/maximum-number-of-diamonds-that-can-be-gained-in-k-minutes/)

给定一个由 **N** 正整数组成的数组**arr【】**，使得**arr【I】**表示**I**包包含**arr【I】**钻石和一个正整数 **K** ，任务是找出在精确的 **K** 分钟内可以获得的钻石的最大数量，如果丢一个包需要 1 分钟，那么如果一个包带有 **P【的话**

**示例:**

> **输入:** arr[] = {2，1，7，4，2}，K = 3
> **输出:** 14
> **说明:**
> 包的初始状态为{2，1，7，4，2}。
> **操作 1:** 从第三个袋子中取出所有钻石，即 arr[2](= 7)，袋子的状态变为:{2，1，3，4，2}。
> **操作 2:** 从第四个袋子中取出所有钻石，即 arr[3](= 4)，袋子的状态变为:{2，1，3，2，2}。
> **操作 3:** 从第三个袋子中取出所有钻石，即 arr[2](= 3)，袋子的状态变为{2，1，1，2，2}。
> 因此，钻石总收益为 7 + 4 + 3 = 14。
> 
> **输入:** arr[] = {7，1，2}，K = 2
> T3】输出: 10

**方法:**在[最大堆](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)的帮助下，使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，比如说 **PQ** ，然后[将给定数组的所有元素插入 **PQ**](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) 。
*   初始化一个变量，比如说**和**为 **0** 来存储最终获得的最大钻石。
*   [循环](https://www.geeksforgeeks.org/range-based-loop-c/)直到[优先级队列 **PQ** 不为空](https://www.geeksforgeeks.org/priority_queueempty-priority_queuesize-c-stl/)和 **K > 0** 的值:
    *   弹出优先级队列的[顶部元素，并将弹出的元素添加到变量**和**中。](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)
    *   将弹出的元素除以 **2** 并插入优先级队列 **PQ** 。
    *   将 **K** 的值减 **1** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of diamonds that can be gained in
// exactly K minutes
void maxDiamonds(int A[], int N, int K)
{
    // Stores all the array elements
    priority_queue<int> pq;

    // Push all the elements to the
    // priority queue
    for (int i = 0; i < N; i++) {
        pq.push(A[i]);
    }

    // Stores the required result
    int ans = 0;

    // Loop while the queue is not
    // empty and K is positive
    while (!pq.empty() && K--) {

        // Store the top element
        // from the pq
        int top = pq.top();

        // Pop it from the pq
        pq.pop();

        // Add it to the answer
        ans += top;

        // Divide it by 2 and push it
        // back to the pq
        top = top / 2;
        pq.push(top);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int A[] = { 2, 1, 7, 4, 2 };
    int K = 3;
    int N = sizeof(A) / sizeof(A[0]);
    maxDiamonds(A, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum number
// of diamonds that can be gained in
// exactly K minutes
static void maxDiamonds(int A[], int N, int K)
{

    // Stores all the array elements
    PriorityQueue<Integer> pq = new PriorityQueue<>(
        (a, b) -> b - a);

    // Push all the elements to the
    // priority queue
    for(int i = 0; i < N; i++)
    {
        pq.add(A[i]);
    }

    // Stores the required result
    int ans = 0;

    // Loop while the queue is not
    // empty and K is positive
    while (!pq.isEmpty() && K-- > 0)
    {

        // Store the top element
        // from the pq
        int top = pq.peek();

        // Pop it from the pq
        pq.remove();

        // Add it to the answer
        ans += top;

        // Divide it by 2 and push it
        // back to the pq
        top = top / 2;
        pq.add(top);
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 1, 7, 4, 2 };
    int K = 3;
    int N = A.length;

    maxDiamonds(A, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of diamonds that can be gained in
# exactly K minutes
def maxDiamonds(A, N, K):

    # Stores all the array elements
    pq = []

    # Push all the elements to the
    # priority queue
    for i in range(N):
        pq.append(A[i])

    pq.sort()

    # Stores the required result
    ans = 0

    # Loop while the queue is not
    # empty and K is positive
    while (len(pq) > 0 and K > 0):
        pq.sort()

        # Store the top element
        # from the pq
        top = pq[len(pq) - 1]

        # Pop it from the pq
        pq = pq[0:len(pq) - 1]

        # Add it to the answer
        ans += top

        # Divide it by 2 and push it
        # back to the pq
        top = top // 2;
        pq.append(top)
        K -= 1

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    A = [ 2, 1, 7, 4, 2 ]
    K = 3
    N = len(A)

    maxDiamonds(A, N, K)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to find the maximum number
// of diamonds that can be gained in
// exactly K minutes
static void maxDiamonds(int []A, int N, int K)
{

    // Stores all the array elements
    var pq = new List<int>();

    // Push all the elements to the
    // priority queue
    for(int i = 0; i < N; i++)
    {
        pq.Add(A[i]);
    }

    // Stores the required result
    int ans = 0;

    // Loop while the queue is not
    // empty and K is positive
    while (pq.Count!=0 && K-- > 0)
    {
        pq.Sort();
        // Store the top element
        // from the pq
        int top = pq[pq.Count-1];

        // Pop it from the pq
        pq.RemoveAt(pq.Count-1);

        // Add it to the answer
        ans += top;

        // Divide it by 2 and push it
        // back to the pq
        top = top / 2;
        pq.Add(top);
    }

    // Print the answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(string[] args)
{
    int []A= { 2, 1, 7, 4, 2 };
    int K = 3;
    int N = A.Length;

    maxDiamonds(A, N, K);
}
}

// This code is contributed by rrrtnx.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum number
// of diamonds that can be gained in
// exactly K minutes
function maxDiamonds(A, N, K) {
    // Stores all the array elements
    let pq = [];

    // Push all the elements to the
    // priority queue
    for (let i = 0; i < N; i++) {
        pq.push(A[i]);
    }

    // Stores the required result
    let ans = 0;

    // Loop while the queue is not
    // empty and K is positive
    pq.sort((a, b) => a - b)

    while (pq.length && K--) {

        pq.sort((a, b) => a - b)
        // Store the top element
        // from the pq
        let top = pq[pq.length - 1];

        // Pop it from the pq
        pq.pop();

        // Add it to the answer
        ans += top;

        // Divide it by 2 and push it
        // back to the pq
        top = Math.floor(top / 2);
        pq.push(top);
    }

    // Print the answer
    document.write(ans);
}

// Driver Code

let A = [2, 1, 7, 4, 2];
let K = 3;
let N = A.length;
maxDiamonds(A, N, K);

</script>
```

**Output:** 

```
14
```

***时间复杂度:**O((N+K)* log N)*
***辅助空间:** O(N)*