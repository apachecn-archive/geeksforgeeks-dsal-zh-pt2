# 通过销售 M 种产品使利润最大化，这样一种产品的利润就是该供应商剩余的产品数量

> 原文:[https://www . geeksforgeeks . org/通过销售 m 产品实现利润最大化，这样产品利润就是供应商剩余的产品数量/](https://www.geeksforgeeks.org/maximize-profit-possible-by-selling-m-products-such-that-profit-of-a-product-is-the-number-of-products-left-of-that-supplier/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，使得**arr【I】**代表 **i <sup>th</sup>** 供应商拥有的产品数量，以及一个正整数 **M** ，如果某个特定产品的利润与该供应商剩余的产品数量相同，则任务是通过销售 **M** 产品找到最大利润。

**示例:**

> **输入:** arr[] = {4，6}，M = 4
> **输出:** 19
> **说明:**
> 下面是产品卖出获得最大利润的顺序:
> **产品 1:** 从第二个供应商卖出一个产品，然后数组修改为{4，5}，利润为 6。
> **产品 2:** 向第二供应商销售一个产品，然后数组修改为{4，4}，利润为 6 + 5 = 11。
> **产品 3:** 从第二个供应商处卖出一个产品，然后数组修改为{4，3}，利润为 6 + 5 + 4 = 15。
> **产品 4:** 从第一个供应商处卖出一个产品，然后数组修改为{3，3}，利润为 6 + 5 + 4 + 4 = 19。
> 因此，销售 4 款产品能获得的最大利润是 19。
> 
> **输入:** arr[] = {1，2，3}，M = 2
> T3】输出: 5

**天真方法:**给定的问题可以通过从当前剩余产品数量最大的供应商处销售产品来解决。所以，思路是[迭代一个循环 **M** 次](https://www.geeksforgeeks.org/loops-in-java/)，在每次迭代[中找到数组中最大元素的值](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，将其值加到利润上，然后将其在数组中的值减 1。循环结束后，打印利润值。

***时间复杂度:** O(M * N)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用 [Max-Heap](https://www.geeksforgeeks.org/max-heap-in-java/) 在 ***O(log N)*** 时间中跟踪数组中的[最大元素进行优化。按照以下步骤解决问题:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

*   使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)初始化[最大堆](https://www.geeksforgeeks.org/max-heap-in-java/)，比如 **Q** 来跟踪数组中存在的最大元素。
*   [遍历阵](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr[]**[将](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)[堆](https://www.geeksforgeeks.org/binary-heap/)中的所有元素插入到 **Q** 中。
*   初始化一个变量，将**最大利润**设为 **0** 存储得到的结果最大利润。
*   [迭代一个循环](https://www.geeksforgeeks.org/loops-in-java/)直到 **M > 0** ，并执行以下步骤:
    *   将 **M** 的值减少 **1** 。
    *   将优先级队列 **Q** 的[顶元素的值存储在变量 **X** 和](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)[中，并将其从优先级队列](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)中弹出。
    *   将 **X** 的值添加到变量**最大利润**中，并将**(X–1)**插入到变量 **Q** 中。
*   完成上述步骤后，打印**最大利润**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum profit
// by selling M number of products
void findMaximumProfit(int arr[], int M, int N)
{

    // Initialize a Max-Heap to keep
    // track of the maximum value
    priority_queue<int> max_heap;

    // Stores the maximum profit
    int maxProfit = 0;

    // Traverse the array and push
    // all the elements in max_heap
    for(int i = 0; i < N; i++)
        max_heap.push(arr[i]);

    // Iterate a loop until M > 0
    while (M > 0)
    {

        // Decrement the value
        // of M by 1
        M--;

        // Pop the maximum element
        // from the heap
        int X = max_heap.top();
        max_heap.pop();

        // Update the maxProfit
        maxProfit += X;

        // Push (X - 1) to max heap
        max_heap.push(X - 1);
    }

    // Print the result
    cout<<maxProfit;
}

// Driver Code
int main()
{
    int arr[] = { 4, 6 };
    int M = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    findMaximumProfit(arr, M, N);
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the maximum profit
    // by selling M number of products
    static void findMaximumProfit(
        int[] arr, int M, int N)
    {

        // Initialize a Max-Heap to keep
        // track of the maximum value
        PriorityQueue<Integer> max_heap
            = new PriorityQueue<>((a, b) -> b - a);

        // Stores the maximum profit
        int maxProfit = 0;

        // Traverse the array and push
        // all the elements in max_heap
        for (int i = 0; i < N; i++)
            max_heap.add(arr[i]);

        // Iterate a loop until M > 0
        while (M > 0) {

            // Decrement the value
            // of M by 1
            M--;

            // Pop the maximum element
            // from the heap
            int X = max_heap.poll();

            // Update the maxProfit
            maxProfit += X;

            // Push (X - 1) to max heap
            max_heap.add(X - 1);
        }

        // Print the result
        System.out.println(maxProfit);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 4, 6 };
        int M = 4;
        int N = arr.length;
        findMaximumProfit(arr, M, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum profit
# by selling M number of products
def findMaximumProfit(arr, M, N):

    # Initialize a Max-Heap to keep
    # track of the maximum value
    max_heap = []

    # Stores the maximum profit
    maxProfit = 0

    # Traverse the array and push
    # all the elements in max_heap
    for i in range(0, N):
        max_heap.append(arr[i])

    max_heap.sort()
    max_heap.reverse()

    # Iterate a loop until M > 0
    while (M > 0):

        # Decrement the value
        # of M by 1
        M -= 1

        # Pop the maximum element
        # from the heap
        X = max_heap[0]
        max_heap.pop(0)

        # Update the maxProfit
        maxProfit += X

        # Push (X - 1) to max heap
        max_heap.append(X - 1)
        max_heap.sort()
        max_heap.reverse()

    # Print the result
    print(maxProfit)

# Driver code
arr = [ 4, 6 ]
M = 4
N = len(arr)

findMaximumProfit(arr, M, N)

# This code is contributed by rameshtravel07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the maximum profit
    // by selling M number of products
    static void findMaximumProfit(int[] arr, int M, int N)
    {

        // Initialize a Max-Heap to keep
        // track of the maximum value
        List<int> max_heap = new List<int>();

        // Stores the maximum profit
        int maxProfit = 0;

        // Traverse the array and push
        // all the elements in max_heap
        for(int i = 0; i < N; i++)
            max_heap.Add(arr[i]);

        max_heap.Sort();
        max_heap.Reverse();

        // Iterate a loop until M > 0
        while (M > 0)
        {

            // Decrement the value
            // of M by 1
            M--;

            // Pop the maximum element
            // from the heap
            int X = max_heap[0];
            max_heap.RemoveAt(0);

            // Update the maxProfit
            maxProfit += X;

            // Push (X - 1) to max heap
            max_heap.Add(X - 1);
            max_heap.Sort();
            max_heap.Reverse();
        }

        // Print the result
        Console.Write(maxProfit);
    }

  static void Main() {
    int[] arr = { 4, 6 };
    int M = 4;
    int N = arr.Length;

    findMaximumProfit(arr, M, N);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the maximum profit
    // by selling M number of products
    function findMaximumProfit(arr, M, N)
    {

        // Initialize a Max-Heap to keep
        // track of the maximum value
        let max_heap = [];

        // Stores the maximum profit
        let maxProfit = 0;

        // Traverse the array and push
        // all the elements in max_heap
        for(let i = 0; i < N; i++)
            max_heap.push(arr[i]);

        max_heap.sort(function(a, b){return a - b});
        max_heap.reverse();

        // Iterate a loop until M > 0
        while (M > 0)
        {

            // Decrement the value
            // of M by 1
            M--;

            // Pop the maximum element
            // from the heap
            let X = max_heap[0];
            max_heap.shift();

            // Update the maxProfit
            maxProfit += X;

            // Push (X - 1) to max heap
            max_heap.push(X - 1);
            max_heap.sort(function(a, b){return a - b});
            max_heap.reverse();
        }

        // Print the result
        document.write(maxProfit);
    }

    let arr = [ 4, 6 ];
    let M = 4;
    let N = arr.length;

    findMaximumProfit(arr, M, N);

 // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(M * log(N))*
***辅助空间:** O(N)*