# 对于 Q 查询，通过将最多 L 个元素替换为 R 来最大化数组和

> 原文:[https://www . geeksforgeeks . org/通过将最多 l 个元素替换为 r 进行 q 查询来最大化数组总和/](https://www.geeksforgeeks.org/maximize-array-sum-by-replacing-at-most-l-elements-to-r-for-q-queries/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个由类型为 **{L，R}** 的 **M** 对组成的数组 **Query[][]** ，任务是通过执行查询 **Query[][]** 找到数组的最大和，这样对于每个查询 **{L，R}** 最多将**个**数组元素替换为

**示例:**

> **输入:** arr[]= {5，1，4}，Query[][] = {{2，3}，{1，5}}
> **输出:** 14
> **解释:**
> 以下是执行的操作:
> **查询 1:** 对于查询{2，3}，什么都不做。
> **查询 2:** 对于查询{1，5}，将最多 L(= 1)个数组元素替换为值 R(= 5)，将 arr[1]替换为值 5。
> 经过上述步骤后，数组修改为{5，5，4}。数组元素的和是 14，这是最大值。
> 
> **输入:** arr[] = {1，2，3，4}，Query[][] = {{3，1}，{2，5}}
> **输出:** 17

**进场:**给定问题可以借助 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 解决。最大化[数组和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的主要思想是执行查询以将最小值增加到最大值，因为操作的顺序无关紧要，因为它们彼此独立。按照以下步骤解决给定的问题:

*   维护一个 [**最小堆优先级队列**](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) 并存储所有数组元素。
*   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**Q[][]**，对于每个查询 **{L，R}** 执行以下步骤:
    *   将小于R 的**元素最多 L** 的值改为 **R** 的值，从最小的开始。
    *   执行上述操作，弹出小于 **R** 的元素，并将 **R** 推到[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中的位置。
*   完成上述步骤后，打印优先级队列中存储的值的总和作为最大总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum array
// sum after performing M queries
void maximumArraySumWithMQuery(
    int arr[], vector<vector<int> >& Q,
    int N, int M)
{

    // Maintain a min-heap Priority-Queue
    priority_queue<int, vector<int>,
                   greater<int> >
        pq;

    // Push all the elements in the
    // priority queue
    for (int i = 0; i < N; i++) {
        pq.push(arr[i]);
    }

    // Iterate through M Operations
    for (int i = 0; i < M; i++) {

        // Iterate through the total
        // possible changes allowed
        // and maximize the array sum
        int l = Q[i][0];
        int r = Q[i][1];

        for (int j = 0; j < l; j++) {

            // Change the value of elements
            // less than r to r, starting
            // from the smallest
            if (pq.top() < r) {
                pq.pop();
                pq.push(r);
            }

            // Break if current element >= R
            else {
                break;
            }
        }
    }

    // Find the resultant maximum sum
    int ans = 0;

    while (!pq.empty()) {
        ans += pq.top();
        pq.pop();
    }

    // Print the sum
    cout << ans;
}

// Driver Code
int main()
{
    int N = 3, M = 2;
    int arr[] = { 5, 1, 4 };
    vector<vector<int> > Query
        = { { 2, 3 }, { 1, 5 } };

    maximumArraySumWithMQuery(
        arr, Query, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.PriorityQueue;

class GFG {

    // Function to find the maximum array
    // sum after performing M queries
    public static void maximumArraySumWithMQuery(int arr[], int[][] Q, int N, int M) {

        // Maintain a min-heap Priority-Queue
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

        // Push all the elements in the
        // priority queue
        for (int i = 0; i < N; i++) {
            pq.add(arr[i]);
        }

        // Iterate through M Operations
        for (int i = 0; i < M; i++) {

            // Iterate through the total
            // possible changes allowed
            // and maximize the array sum
            int l = Q[i][0];
            int r = Q[i][1];

            for (int j = 0; j < l; j++) {

                // Change the value of elements
                // less than r to r, starting
                // from the smallest
                if (pq.peek() < r) {
                    pq.remove();
                    pq.add(r);
                }

                // Break if current element >= R
                else {
                    break;
                }
            }
        }

        // Find the resultant maximum sum
        int ans = 0;

        while (!pq.isEmpty()) {
            ans += pq.peek();
            pq.remove();
        }

        // Print the sum
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String args[]) {
        int N = 3, M = 2;
        int arr[] = { 5, 1, 4 };
        int[][] Query = { { 2, 3 }, { 1, 5 } };

        maximumArraySumWithMQuery(arr, Query, N, M);

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python program for the above approach
from queue import PriorityQueue

# Function to find the maximum array
# sum after performing M queries
def maximumArraySumWithMQuery(arr, Q, N, M):

    # Maintain a min-heap Priority-Queue
    pq = PriorityQueue()

    # Push all the elements in the
    # priority queue
    for i in range(N):
        pq.put(arr[i])

    # Iterate through M Operations
    for i in range(M):

        # Iterate through the total
        # possible changes allowed
        # and maximize the array sum
        l = Q[i][0];
        r = Q[i][1];

        for j in range(l):

            # Change the value of elements
            # less than r to r, starting
            # from the smallest
            if (pq.queue[0] < r):
                pq.get();
                pq.put(r);

            # Break if current element >= R
            else:
                break

    # Find the resultant maximum sum
    ans = 0;

    while ( not pq.empty() ):
        ans += pq.queue[0];
        pq.get();

    # Print the sum
    print(ans)

# Driver Code
N = 3
M = 2
arr = [5, 1, 4]
Query = [[2, 3], [1, 5]]

maximumArraySumWithMQuery(arr, Query, N, M)

# This code is contributed by gfgking.
```

**Output:** 

```
14
```

***时间复杂度:**O(M * N * log N)*
T5**辅助空间:** O(N)