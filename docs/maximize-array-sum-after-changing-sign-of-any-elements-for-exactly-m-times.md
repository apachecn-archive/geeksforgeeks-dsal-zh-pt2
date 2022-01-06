# 在精确 M 次改变任何元素的符号后最大化数组和

> 原文:[https://www . geesforgeks . org/maximize-array-sum-after-changed-sign-of-any-elements-for-just-m-times/](https://www.geeksforgeeks.org/maximize-array-sum-after-changing-sign-of-any-elements-for-exactly-m-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**和一个整数 **M，**任务是在将数组中任何元素的符号精确地改变 **M** 次后，找到数组的**最大值**和。允许多次改变同一元素的符号。

**示例:**

> **输入:** arr[ ] = {-3，7，-1，-5，-3}，M = 4
> **输出:** 19
> **说明:**
> 数组上的 4 个操作可以执行为，
> **操作 1:** 更改 arr[0] - > {3，7，-1，-5，-3}
> **操作 2:** 更改 arr[2] - >的符号 1，5，-3}
> **运算 4:** 改变 arr[4] - > {3，7，1，5，3}
> 得到的数组最大和为 19。
> 
> **输入:** arr[ ] = {-4，2，3，1}，M = 3
> T3】输出: 10

**方法:**解决问题的主要思路是在每次迭代中翻转数组的最小个数。通过这样做，负值将变为正值，并且数组和将最大化。
按照以下步骤解决问题:

*   初始化一个最小[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，说 **pq[]，**并推送数组的所有元素 **arr[]。**
*   初始化一个变量，比如 **sum = 0，**存储数组的最大和。
*   [重复一个 while 循环，直到 M](https://www.geeksforgeeks.org/range-based-loop-c/) 大于 **0** ，并执行以下操作:
    *   [从优先级队列](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)中弹出，从变量**和**中减去。
    *   翻转弹出元素的符号，将其乘以 **-1** ，并将其加到**和**中。
    *   **推送**优先级队列中新翻转的元素，并从 **M** 中减去 **1** 。
*   最后，打印变量**总和**中存储的**最大值**总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// with M flips
void findMaximumSumWithMflips(
    int arr[], int N, int M)
{

    // Declare a priority queue
    // i.e. min heap
    priority_queue<int, vector<int>, greater<int> > pq;

    // Declare the sum as zero
    int sum = 0;

    // Push all elements of the
    // array in it
    for (int i = 0; i < N; i++) {
        pq.push(arr[i]);
        sum += arr[i];
    }

    // Iterate for M times
    while (M--) {

        // Get the top element
        sum -= pq.top();

        // Flip the sign of the
        // top element
        int temp = -1 * pq.top();

        // Remove the top element
        pq.pop();

        // Update the sum
        sum += temp;

        // Push the temp into
        // the queue
        pq.push(temp);
    }

    cout << sum;
}

// Driver program
int main()
{

    int arr[] = { -3, 7, -1, -5, -3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 4;

    findMaximumSumWithMflips(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.lang.*;
import java.lang.Math;
class GFG {

// Function to find the maximum sum
// with M flips
static void findMaximumSumWithMflips(
    int arr[], int N, int M)
{

    // Declare a priority queue
    // i.e. min heap
    PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>();

    // Declare the sum as zero
    int sum = 0;

    // Push all elements of the
    // array in it
    for (int i = 0; i < N; i++) {
        minHeap.add(arr[i]);
        sum += arr[i];
    }

    // Iterate for M times
    while (M-- >0) {

        // Get the top element
        sum -= minHeap.peek();

        // Flip the sign of the
        // top element
        int temp = -1 * minHeap.peek();

        // Remove the top element
        minHeap.remove();

        // Update the sum
        sum += temp;

        // Push the temp into
        // the queue
        minHeap.add(temp);
    }

     System.out.println(sum);
}

    // Driver Code
    public static void main(String[] args)
    {

        // Given input
        int arr[] = { -3, 7, -1, -5, -3 };
        int M = 4,N=5;
        findMaximumSumWithMflips(arr, N, M);

    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum sum
# with M flips
def findMaximumSumWithMflips(arr, N, M):
    # Declare a priority queue
    # i.e. min heap
    pq = []

    # Declare the sum as zero
    sum = 0

    # Push all elements of the
    # array in it
    for i in range(N):
        pq.append(arr[i])
        sum += arr[i]
        pq.sort()

    # Iterate for M times
    while (M>0):
        # Get the top element
        sum -= pq[0]

        # Flip the sign of the
        # top element
        temp = -1 * pq[0]

        # Remove the top element
        pq = pq[1:]

        # Update the sum
        sum += temp

        # Push the temp into
        # the queue
        pq.append(temp)

        pq.sort()
        M -= 1

    print(sum)

# Driver program
if __name__ == '__main__':
    arr = [-3, 7, -1, -5, -3]

    # Size of the array
    N = len(arr)
    M = 4

    findMaximumSumWithMflips(arr, N, M)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
public class GFG {

  // Function to find the maximum sum
  // with M flips
  static void findMaximumSumWithMflips(int[] arr, int N,
                                       int M)
  {

    // Declare a priority queue
    // i.e. min heap
    List<int> minHeap = new List<int>();

    // Declare the sum as zero
    int sum = 0;

    // Push all elements of the
    // array in it
    for (int i = 0; i < N; i++) {
      minHeap.Add(arr[i]);
      sum += arr[i];
    }
    minHeap.Sort();
    // Iterate for M times
    while (M-- > 0) {

      // Get the top element
      sum -= minHeap[0];
      // minHeap.RemoveAt(0);

      // Flip the sign of the
      // top element
      int temp = -1 * minHeap[0];

      // Remove the top element
      minHeap.RemoveAt(0);

      // Update the sum
      sum += temp;

      // Push the temp into
      // the queue
      minHeap.Add(temp);
      minHeap.Sort();
    }

    Console.WriteLine(sum);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given input
    int[] arr = { -3, 7, -1, -5, -3 };
    int M = 4, N = 5;
    findMaximumSumWithMflips(arr, N, M);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum sum
// with M flips
function findMaximumSumWithMflips(arr, N, M)
{

    // Declare a priority queue
    // i.e. min heap
    let pq = []

    // Declare the sum as zero
    let sum = 0

    // Push all elements of the
    // array in it
    for(let i = 0; i < N; i++){
        pq.push(arr[i])
        sum += arr[i]
        pq.sort((a, b) => a - b)
    }

    // Iterate for M times
    while (M > 0){
        // Get the top element
        sum -= pq[0]

        // Flip the sign of the
        // top element
        temp = -1 * pq[0]

        // Remove the top element
        pq.shift()

        // Update the sum
        sum += temp

        // Push the temp into
        // the queue
        pq.push(temp)

        pq.sort((a, b) => a - b)
        M -= 1
    }

    document.write(sum)
}

// Driver program
    let arr = [-3, 7, -1, -5, -3]

    // Size of the array
    let N = arr.length
    let M = 4

    findMaximumSumWithMflips(arr, N, M)

// This code is contributed by gfgking.   
</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(NLogN)*
***辅助空间:** O(N)*