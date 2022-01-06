# 从给定的 3 个数组的任意排列中最大化递增三元组的计数

> 原文:[https://www . geeksforgeeks . org/从给定 3 个数组的任意排列中最大化递增三元组的计数/](https://www.geeksforgeeks.org/maximize-count-of-increasing-triplets-from-any-permutation-of-given-3-arrays/)

给定三个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**X【】**、**Y【】**和**Z【】**各由 **N** 个整数组成，任务是找出三个数组 **(X[i]、Y[i]、Z[i])** 的最大三元组数，使得**(X[I]<Y[I]<Z[I])**对于三个数组[的任意排列](https://www.geeksforgeeks.org/count-all-the-permutation-of-an-array/)

**示例:**

> **输入:** X = {9，6，14，1，8}，Y = {2，10，3，12，11}，Z = {15，13，5，7，4}
> **输出:** 3
> **解释:**
> 将数组 X[]，Y[]，Z[]重新排列为{1，6，8，9，14}，{3，2，10，12，11}，{4，7，8 }增加的三元组是{1，3，4}、{8，10，15}和{9，12，13}。
> 所以这样的三胞胎总数是 3。
> 
> **输入:** X = {1，2，3，4}，Y = {5，6，7，8}，Z = {9，10，11，12}
> 输出: 4

**天真方法:**给定的问题可以通过[生成三个数组的三元组的所有可能组合](https://www.geeksforgeeks.org/combinations-from-n-arrays-picking-one-element-from-each-array/)并计算那些满足给定条件的三元组来解决。检查所有排列后，打印获得的三胞胎总数。

***时间复杂度:** O(N*(N！) <sup>3</sup> )*
***辅助空间:** O(1)*

**高效方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，其思想是[对给定的数组 **X[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) 进行排序，然后为了找到三元组，选择数组 **Y[]** 和 **Z[]** 中的那些元素，它们为数组的每个元素形成递增的三元组，并且该思想可以使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)来实现。按照以下步骤解决问题:

*   [按递增顺序排列数组**X[]**](https://www.geeksforgeeks.org/sorting-algorithms/)。
*   初始化两个优先级队列，比如说 **PQY** 和 **PQZ** 分别为数组 **Y[]** 和 **Z[]** 实现 [MinHeap](https://www.geeksforgeeks.org/implement-min-heap-using-stl/) 。
*   将数组 **Y[]** 的所有元素存储在 **PQY** 中。
*   将数组的所有元素 **Z[]** 存储在 **PQZ** 中。
*   遍历数组 **X[]** 并执行以下步骤:
    *   对于每个元素 **X[i]** ，[从优先级队列](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) **PQY** 弹出该元素，直到其顶部元素小于 **X[i]** 且 **PQY** 不为空。
    *   对于 **PQY** 的每个元素顶部元素，比如 temp，[从优先级队列](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) **PQZ** 弹出该元素，直到其顶部元素小于 **temp** 且 **PQY** 不为空。
    *   将**计数**的值增加 **1** 。
*   完成上述步骤后，打印**计数**的值，作为三胞胎的最大计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of triplets
// that are in increasing order from the
// given three arrays after rearranging
int countTriplet(int arr1[], int arr2[],
                 int arr3[], int N)
{

    // Sort the given array arr[]
    sort(arr1, arr1 + N);

    // Initializing priority queues
    priority_queue<int, vector<int>,
                   greater<int> >
        Y;
    priority_queue<int, vector<int>,
                   greater<int> >
        Z;

    // Push array elements arr2[i] in Y
    for (int i = 0; i < N; i++) {
        Y.push(arr2[i]);
    }

    // Push array elements arr3[i] in Y
    for (int i = 0; i < N; i++) {
        Z.push(arr3[i]);
    }

    int x, y, z;
    int ans = 0;

    // Traverse the array arr1[]
    for (int i = 0; i < N; i++) {

        x = arr1[i];
        while (!Y.empty()
               && Y.top() <= x)
            Y.pop();

        // If Y is empty then there is
        // no more triplets possible
        if (Y.empty())
            break;

        y = Y.top();
        Y.pop();

        while (!Z.empty()
               && Z.top() <= y)
            Z.pop();

        // If Z is empty then there is
        // no more triplets possible
        if (Z.empty())
            break;

        z = Z.top();
        Z.pop();

        // Increment the triplets count
        ++ans;
    }

    // Return the maximum count of triplets
    return ans;
}

// Driver Code
int main()
{
    int X[] = { 9, 6, 14, 1, 8 };
    int Y[] = { 2, 10, 3, 12, 11 };
    int Z[] = { 15, 13, 5, 7, 4 };
    int N = sizeof(X) / sizeof(X[0]);

    cout << countTriplet(X, Y, Z, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to find the number of triplets
    // that are in increasing order from the
    // given three arrays after rearranging
    static int countTriplet(int[] arr1, int[] arr2,
                     int[] arr3, int N)
    {

        // Sort the given array arr[]
        Arrays.sort(arr1);

        // Initializing priority queues
        Vector<Integer> Y = new Vector<Integer>();
        Vector<Integer> Z = new Vector<Integer>();

        // Push array elements arr2[i] in Y
        for (int i = 0; i < N; i++) {
            Y.add(arr2[i]);
        }
        // Push array elements arr3[i] in Y
        for (int i = 0; i < N; i++) {
            Z.add(arr3[i]);
        }
        Collections.sort(Y);
        Collections.sort(Z);

        int x, y, z;
        int ans = 0;

        // Traverse the array arr1[]
        for (int i = 0; i < N; i++) {

            x = arr1[i];
            while (Y.size() > 0 && Y.get(0) <= x)
                Y.remove(0);

            // If Y is empty then there is
            // no more triplets possible
            if (Y.size() == 0)
                break;

            y = Y.get(0);
            Y.remove(0);

            while (Z.size() > 0 && Z.get(0) <= y)
                Z.remove(0);

            // If Z is empty then there is
            // no more triplets possible
            if (Z.size() == 0)
                break;

            z = Z.get(0);
            Z.remove(0);

            // Increment the triplets count
            ++ans;
        }

        // Return the maximum count of triplets
        return ans;
    }

    public static void main(String[] args) {
        int[] X = { 9, 6, 14, 1, 8 };
        int[] Y = { 2, 10, 3, 12, 11 };
        int[] Z = { 15, 13, 5, 7, 4 };
        int N = X.length;

        System.out.println(countTriplet(X, Y, Z, N));
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python program for the above approach
from queue import PriorityQueue

# Function to find the number of triplets
# that are in increasing order from the
# given three arrays after rearranging
def countTriplet(arr1, arr2, arr3, N):

    # Sort the given array arr[]
    arr1.sort();

    # Initializing priority queues
    Y = PriorityQueue();
    Z = PriorityQueue();

    # Push array elements arr2[i] in Y
    for i in range(N):
        Y.put(arr2[i]);

    # Push array elements arr3[i] in Y
    for i in range(N):
        Z.put(arr3[i]);

    x = 0
    y = 0
    z = 0
    ans = 0;

    # Traverse the array arr1[]
    for i in range(N):

        x = arr1[i];
        while (not Y.empty() and Y.queue[0] <= x):
            Y.get();

        # If Y is empty then there is
        # no more triplets possible
        if (Y.empty()):
            break;

        y = Y.queue[0];
        Y.get()

        while (not Z.empty() and Z.queue[0] <= y):
            Z.get();

        # If Z is empty then there is
        # no more triplets possible
        if (Z.empty()):
            break;

        z = Z.queue[0];
        Z.get();

        # Increment the triplets count
        ans += 1;

    # Return the maximum count of triplets
    return ans;

# Driver Code
X = [ 9, 6, 14, 1, 8 ];
Y = [ 2, 10, 3, 12, 11 ];
Z = [ 15, 13, 5, 7, 4 ];
N = len(X);

print(countTriplet(X, Y, Z, N));

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the number of triplets
    // that are in increasing order from the
    // given three arrays after rearranging
    static int countTriplet(int[] arr1, int[] arr2,
                     int[] arr3, int N)
    {

        // Sort the given array arr[]
        Array.Sort(arr1);

        // Initializing priority queues
        List<int> Y = new List<int>();
        List<int> Z = new List<int>();

        // Push array elements arr2[i] in Y
        for (int i = 0; i < N; i++) {
            Y.Add(arr2[i]);
        }
        // Push array elements arr3[i] in Y
        for (int i = 0; i < N; i++) {
            Z.Add(arr3[i]);
        }
        Y.Sort();
        Z.Sort();

        int x, y, z;
        int ans = 0;

        // Traverse the array arr1[]
        for (int i = 0; i < N; i++) {

            x = arr1[i];
            while (Y.Count > 0
                   && Y[0] <= x)
                Y.RemoveAt(0);

            // If Y is empty then there is
            // no more triplets possible
            if (Y.Count == 0)
                break;

            y = Y[0];
            Y.RemoveAt(0);

            while (Z.Count > 0
                   && Z[0] <= y)
                Z.RemoveAt(0);

            // If Z is empty then there is
            // no more triplets possible
            if (Z.Count == 0)
                break;

            z = Z[0];
            Z.RemoveAt(0);

            // Increment the triplets count
            ++ans;
        }

        // Return the maximum count of triplets
        return ans;
    }

  static void Main() {
    int[] X = { 9, 6, 14, 1, 8 };
    int[] Y = { 2, 10, 3, 12, 11 };
    int[] Z = { 15, 13, 5, 7, 4 };
    int N = X.Length;

    Console.Write(countTriplet(X, Y, Z, N));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the number of triplets
    // that are in increasing order from the
    // given three arrays after rearranging
    function countTriplet(arr1, arr2, arr3, N)
    {

        // Sort the given array arr[]
        arr1.sort(function(a, b){return a - b});

        // Initializing priority queues
        Y = [];
        Z = [];

        // Push array elements arr2[i] in Y
        for (let i = 0; i < N; i++) {
            Y.push(arr2[i]);
        }
        // Push array elements arr3[i] in Y
        for (let i = 0; i < N; i++) {
            Z.push(arr3[i]);
        }
        Y.sort(function(a, b){return a - b});
        Z.sort(function(a, b){return a - b});

        let x, y, z;
        let ans = 0;

        // Traverse the array arr1[]
        for (let i = 0; i < N; i++) {

            x = arr1[i];
            while (Y.length > 0 && Y[0] <= x)
                Y.shift();

            // If Y is empty then there is
            // no more triplets possible
            if (Y.Count == 0)
                break;

            y = Y[0];
            Y.shift();

            while (Z.length > 0 && Z[0] <= y)
                Z.shift();

            // If Z is empty then there is
            // no more triplets possible
            if (Z.length == 0)
                break;

            z = Z[0];
            Z.shift();

            // Increment the triplets count
            ++ans;
        }

        // Return the maximum count of triplets
        return ans;
    }

    X = [ 9, 6, 14, 1, 8 ];
    Y = [ 2, 10, 3, 12, 11 ];
    Z = [ 15, 13, 5, 7, 4 ];
    N = X.length;

    document.write(countTriplet(X, Y, Z, N));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*