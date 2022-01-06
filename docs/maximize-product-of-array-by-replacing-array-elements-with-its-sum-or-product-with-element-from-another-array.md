# 通过用数组元素的和替换数组元素，或者用另一个数组的元素替换数组元素的积，最大化数组的积

> 原文:[https://www . geeksforgeeks . org/通过用另一个数组的元素替换数组元素的总和或乘积来最大化数组的乘积/](https://www.geeksforgeeks.org/maximize-product-of-array-by-replacing-array-elements-with-its-sum-or-product-with-element-from-another-array/)

给定由 **N** 个整数组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是通过将每个数组元素 **A[i]** 分配给单个元素 **B[j]** 来更新数组 **A[]** ，并将 **A[i]** 更新为 **A[i] + B[j]** 或 **A[i]**

***注意:**两个数组中的每个数组元素只能与另一个数组中的单个元素配对一次。*

**示例:**

> **输入:** A[] = {1，1，6}，B[] = {1，2，3}
> **输出:** 108
> **解释:**
> 
> 1.  更新 A[0] = A[0] + B[0]，A[]修改为{2，1，6}
> 2.  更新 A[1] = A[1] + B[1]，A[]修改为{2，3，6}
> 3.  更新 A[0] = A[0] * B[2]，A[]修改为{6，3，6}
> 
> 因此，数组 A[]的乘积是 6 * 3 * 6 = 108。
> 
> **输入:** A[] = {1，1，10}，B[] ={1，1，1}
> **输出:** 60
> **解释:**
> 
> 1.  更新 A[0] = A[0] + B[0]，A[]修改为{2，1，10}
> 2.  更新 A[1] = A[1] + B[1]，A[]修改为{2，2，10}
> 3.  更新 A[0] = A[0] * B[2]，A[]修改为{3，2，10}

**方法:**上述问题可以通过使用[优先级队列(最小堆)](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)来解决。按照以下步骤解决问题:

*   [排序阵](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)T2【B】。
*   将数组 **A[]** 的所有元素插入优先级队列，以便每次获得最少的元素。
*   [使用变量 **j** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **B[]** ，从优先级队列中弹出一个元素作为 **minE + B[j]** 或 **minE*B[j]** 的最大值，并将该最大值推入优先级队列。
*   在上述步骤之后，优先级队列中元素的乘积就是所需的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// product of array A[]
int largeProduct(vector<int> A,
                 vector<int> B, int N)
{

    // Base Case
    if (N == 0)
        return 0;

    // Store all the elements of
    // the array A[]
    priority_queue<int, vector<int>,
           greater<int>> pq;

    for(int i = 0; i < N; i++)
        pq.push(A[i]);

    // Sort the Array B[]
    sort(B.begin(), B.end());

    // Traverse the array B[]
    for(int i = 0; i < N; i++)
    {

        // Pop minimum element
        int minn = pq.top();
        pq.pop();

        // Check which operation is
        // producing maximum element
        int maximized_element = max(minn * B[i],
                                    minn + B[i]);

        // Insert resultant element
        // into the priority queue
        pq.push(maximized_element);
    }

    // Evaluate the product
    // of the elements of A[]
    int max_product = 1;
    while (pq.size() > 0)
    {
        max_product *= pq.top();
        pq.pop();
    }

    // Return the maximum product
    return max_product;
}

// Driver Code
int main()
{

    // Given arrays
    vector<int> A = { 1, 1, 10 };
    vector<int> B = { 1, 1, 1 };

    int N = 3;

    // Function Call
    cout << largeProduct(A, B, N);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to find the largest
    // product of array A[]
    public static int largeProduct(
        int A[], int B[], int N)
    {
        // Base Case
        if (N == 0)
            return 0;

        // Store all the elements of
        // the array A[]
        PriorityQueue<Integer> pq
            = new PriorityQueue<>();

        for (int i = 0; i < N; i++)
            pq.add(A[i]);

        // Sort the Array B[]
        Arrays.sort(B);

        // Traverse the array B[]
        for (int i = 0; i < N; i++) {

            // Pop minimum element
            int minn = pq.poll();

            // Check which operation is
            // producing maximum element
            int maximized_element
                = Math.max(minn * B[i],
                           minn + B[i]);

            // Insert resultant element
            // into the priority queue
            pq.add(maximized_element);
        }

        // Evaluate the product
        // of the elements of A[]
        int max_product = 1;
        while (pq.size() > 0) {

            max_product *= pq.poll();
        }

        // Return the maximum product
        return max_product;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given arrays
        int A[] = { 1, 1, 10 };
        int B[] = { 1, 1, 1 };

        int N = 3;

        // Function Call
        System.out.println(
            largeProduct(A, B, N));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the largest
# product of array A[]
def largeProduct(A, B, N):

    # Base Case
    if(N == 0):
        return 0

    # Store all the elements of
    # the array A[]
    pq = []
    for i in range(N):
        pq.append(A[i])

    # Sort the Array B[]
    B.sort()
    pq.sort(reverse = True)

    # Traverse the array B[]
    for i in range(N):

        # Pop minimum element
        minn = pq.pop()

        # Check which operation is
        # producing maximum element
        maximized_element = max(minn * B[i], minn + B[i])

        # Insert resultant element
        # into the priority queue
        pq.append(maximized_element)
        pq.sort(reverse = True)

    # Evaluate the product
    # of the elements of A[]
    max_product = 1
    while(len(pq) > 0):
        max_product *= pq.pop();

    # Return the maximum product   
    return max_product

# Driver Code

# Given arrays
A = [1, 1, 10]
B = [1, 1, 1]
N = 3

# Function Call
print(largeProduct(A, B, N))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the largest
    // product of array A[]
    public static int largeProduct(int[] A, int[] B, int N)
    {

        // Base Case
        if(N == 0)
        {
            return 0;
        }

        // Store all the elements of
        // the array A[]
        List<int> pq = new List<int>();
        for(int i = 0; i < N; i++)
        {
            pq.Add(A[i]);
        }

        // Sort the Array B[]
        Array.Sort(B);
        pq.Sort();

        // Traverse the array B[]
        for(int i = 0; i < N; i++)
        {
            int min = pq[0];

            // Pop minimum element
            pq.RemoveAt(0);

            // Check which operation is
            // producing maximum element
            int maximized_element = Math.Max(min* B[i], min + B[i]);

            // Insert resultant element
            // into the priority queue
            pq.Add(maximized_element);
            pq.Sort();
        }

        // Evaluate the product
        // of the elements of A[]
        int max_product = 1;
        while(pq.Count > 0)
        {
            max_product *= pq[0];
            pq.RemoveAt(0);
        }

        // Return the maximum product
        return max_product;
    }

    // Driver Code
    static public void Main ()
    {

        // Given arrays
        int[] A = { 1, 1, 10 };
        int[] B = { 1, 1, 1 };
        int N = 3;

        // Function Call
        Console.WriteLine(largeProduct(A, B, N));
    }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the largest
// product of array A[]
function  largeProduct(A, B, N)
{

    // Base Case
        if (N == 0)
            return 0;

        // Store all the elements of
        // the array A[]
        let pq=[];

        for (let i = 0; i < N; i++)
            pq.push(A[i]);
        pq.sort(function(a,b){return a-b;});

        // Sort the Array B[]
        B.sort(function(a,b){return a-b;});

        // Traverse the array B[]
        for (let i = 0; i < N; i++) {

            // Pop minimum element
            let minn = pq.shift();

            // Check which operation is
            // producing maximum element
            let maximized_element
                = Math.max(minn * B[i],
                           minn + B[i]);

            // Insert resultant element
            // into the priority queue
            pq.push(maximized_element);
            pq.sort(function(a,b){return a-b;});
        }

        // Evaluate the product
        // of the elements of A[]
        let max_product = 1;
        while (pq.length > 0) {

            max_product *= pq.shift();
        }

        // Return the maximum product
        return max_product;
}

// Driver Code
let A=[1, 1, 10 ];
let B=[1, 1, 1];
let N = 3;
document.write(largeProduct(A, B, N));

// This code is contributed by patel2127
</script>
```

**Output:**

```
60
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*