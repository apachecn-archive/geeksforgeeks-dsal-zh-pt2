# 通过最多 K 个约简来最小化数组的和

> 原文:[https://www . geeksforgeeks . org/最大限度地减少 k 个阵列的总和/](https://www.geeksforgeeks.org/minimize-sum-of-an-array-by-at-most-k-reductions/)

给定一个由 **N** 个整数组成的整数数组 **arr[]** ，任务是通过最多执行 **K** 个运算来最小化给定数组的和，其中每个运算涉及将数组元素 **arr[i]** 减少到**层(arr[i]/2)** 。

**示例:**

> **输入:** N = 4，a[] = {20，7，5，4}，K = 3
> **输出:** 17
> **解释:**
> 操作 1: {20，7，5，4} - > {10，7，5，4}
> 操作 2: {10，7，5，4} - > {5，7，5，4}
> 操作 3: {5，7，5，4}因此，数组的和= 17。
> 
> **输入:** N = 4，a[] = {10，4，6，16}，K = 2
> **输出:** 23

**方法:**为了获得最小可能和，每次操作的主要思想是在每次操作之前减少数组中的最大元素。这可以使用 [**MaxHeap**](https://www.geeksforgeeks.org/max-heap-in-java/) 来实现。按照以下步骤解决问题:

*   将所有数组元素插入 **MaxHeap** 。
*   弹出 **MaxHeap** 的根，将**(弹出元素)/ 2** 插入 **MaxHeap**
*   重复上述步骤 **K** 次后，逐个弹出 **MaxHeap** 的元素，并不断添加它们的值。最后，打印总和。

**以下是上述方法的实施:**

## C++

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to obtain the minimum possible
// sum from the array by K reductions
int minSum(int a[], int n, int k)
{
    priority_queue <int> q;

    // Insert elements into the MaxHeap
    for(int i = 0; i < n; i++)
    {
        q.push(a[i]);
    }

    while(!q.empty() && k > 0)
    {
        int top = q.top() / 2;

        // Remove the maximum            
        q.pop();

        // Insert maximum / 2
        q.push(top);
        k -= 1;
    }

    // Stores the sum of remaining elements
    int sum = 0;
    while(!q.empty())
    {
        sum += q.top();
        q.pop();
    }
    return sum;
}

// Driver code
int main()
{
    int n = 4;
    int k = 3;
    int a[] = { 20, 7, 5, 4 };

    cout << (minSum(a, n, k));

    return 0;
}

// This code is contributed by jojo9911
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.io.*;
import java.util.*;
class GFG {

    // Function to obtain the minimum possible
    // sum from the array by K reductions
    public static int minSum(int a[], int n, int k)
    {
        // Implements the MaxHeap
        PriorityQueue<Integer> maxheap
            = new PriorityQueue<>((one, two) -> two - one);

        // Insert elements into the MaxHeap
        for (int i = 0; i < n; i++)
            maxheap.add(a[i]);

        while (maxheap.size() > 0 && k > 0) {

            // Remove the maximum
            int max_ele = maxheap.poll();

            // Insert maximum / 2
            maxheap.add(max_ele / 2);
            k -= 1;
        }

        // Stores the sum of remaining elements

        int sum = 0;
        while (maxheap.size() > 0)
            sum += maxheap.poll();

        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        int k = 3;
        int a[] = { 20, 7, 5, 4 };
        System.out.println(minSum(a, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to obtain the minimum possible
# sum from the array by K reductions
def minSum(a, n, k):

    q = []

    # Insert elements into the MaxHeap
    for i in range(n):
        q.append(a[i])

    q = sorted(q)   

    while (len(q) > 0 and k > 0):
        top = q[-1] // 2

        # Remove the maximum
        del q[-1]

        # Insert maximum / 2
        q.append(top)
        k -= 1
        q = sorted(q)

    # Stores the sum of remaining elements
    sum = 0
    while(len(q) > 0):
        sum += q[-1]
        del q[-1]

    return sum

# Driver code
if __name__ == '__main__':

    n = 4
    k = 3

    a = [ 20, 7, 5, 4 ]

    print(minSum(a, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to obtain the minimum possible
// sum from the array by K reductions
static int minSum(int[] a, int n, int k)
{

    // Implements the MaxHeap
    List<int> q = new List<int>();
    for(int i = 0; i < n; i++)
    {

        // Insert elements into the MaxHeap
        q.Add(a[i]);
    }

    q.Sort();
    while (q.Count != 0 && k > 0)
    {
        int top = q[q.Count - 1] / 2;

        // Remove the maximum
        // Insert maximum / 2
        q[q.Count - 1] = top;

        k--;
        q.Sort();
    }

    // Stores the sum of remaining elements
    int sum = 0;
    while (q.Count != 0)
    {
        sum += q[0];
        q.RemoveAt(0);
    }
    return sum;
}

// Driver Code
static public void Main()
{
    int n = 4;
    int k = 3;
    int[] a = { 20, 7, 5, 4 };

    Console.WriteLine(minSum(a, n, k));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript Program to implement the
// above approach

// Function to obtain the minimum possible
    // sum from the array by K reductions
function  minSum(a,n,k)
{
    // Implements the MaxHeap
        let maxheap = [];

        // Insert elements into the MaxHeap
        for (let i = 0; i < n; i++)
            maxheap.push(a[i]);

        maxheap.sort(function(a,b){return a-b;});

        while (maxheap.length > 0 && k > 0) {

            // Remove the maximum
            let max_ele = maxheap.pop();

            // Insert maximum / 2
            maxheap.push(Math.floor(max_ele / 2));
            k -= 1;
            maxheap.sort(function(a,b){return a-b;});
        }

        // Stores the sum of remaining elements

        let sum = 0;
        while (maxheap.length > 0)
            sum += maxheap.shift();

        return sum;
}

// Driver Code
let n = 4;
let k = 3;
let a = [ 20, 7, 5, 4 ];
document.write(minSum(a, n, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
17
```

***时间复杂度:** O(Klog(N))*
***辅助空间:** O(N)*