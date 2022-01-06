# 通过 K 次替换最小化最大和最小数组元素之间的差异

> 原文:[https://www . geeksforgeeks . org/按 k 替换最小化最大和最小数组元素之间的差异/](https://www.geeksforgeeks.org/minimize-difference-between-the-largest-and-smallest-array-elements-by-k-replacements/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是在替换 **K** 个元素后，找出给定数组中最大和最小元素之间的最小差。

**示例:**

> **输入:** A[] = {-1，3，-1，8，5，4}，K = 3
> **输出:** 2
> **说明:**将 A[0]和 A[2]分别替换为 3 和 4。用 5 代替 A[3]。修改后的数组 A[]为{3，3，4，5，5，4}。因此，所需输出= (5-3) = 2。
> 
> **输入:** A[] = {10，10，3，4，10}，K = 2
> T3】输出: 0

**排序方式:**思路是[给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)排序。检查从数组开始移除 **X** ( *0 ≤ X ≤ K* )元素和从数组末尾移除**K–X**元素的所有 **K + 1** 可能性，并计算可能的最小差异。最后，打印得到的最小差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum difference
// between largest and smallest element
// after K replacements
int minDiff(int A[], int K, int n)
{

    // Sort array in ascending order
    sort(A, A + n);

    if (n <= K)
        return 0;

    // Minimum difference
    int mindiff = A[n - 1] - A[0];

    if (K == 0)
        return mindiff;

    // Check for all K + 1 possibilities
    for(int i = 0, j = n - 1 - K; j < n;)
    {
        mindiff = min(
            mindiff, A[j] - A[i]);

        i++;
        j++;
    }

    // Return answer
    return mindiff;
}

// Driver Code
int main()
{

    // Given array
    int A[] = { -1, 3, -1, 8, 5, 4 };
    int K = 3;

    // Length of array
    int n = sizeof(A) / sizeof(A[0]);

    // Prints the minimum possible difference
    cout << minDiff(A, K, n);

    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find minimum difference
    // between largest and smallest element
    // after K replacements
    static int minDiff(int[] A, int K)
    {
        // Sort array in ascending order
        Arrays.sort(A);

        // Length of array
        int n = A.length;

        if (n <= K)
            return 0;

        // Minimum difference
        int mindiff = A[n - 1] - A[0];
        if (K == 0)
            return mindiff;

        // Check for all K + 1 possibilities
        for (int i = 0, j = n - 1 - K; j < n;) {
            mindiff = Math.min(
                mindiff, A[j] - A[i]);

            i++;
            j++;
        }

        // Return answer
        return mindiff;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int A[] = { -1, 3, -1, 8, 5, 4 };
        int K = 3;

        // Prints the minimum possible difference
        System.out.println(minDiff(A, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum difference
# between largest and smallest element
# after K replacements
def minDiff(A, K):

    # Sort array in ascending order
    A.sort();

    # Length of array
    n = len(A);
    if (n <= K):
        return 0;

    # Minimum difference
    mindiff = A[n - 1] - A[0];
    if (K == 0):
        return mindiff;

    # Check for all K + 1 possibilities
    i = 0;
    for j in range(n - 1 - K, n):
        mindiff = min(mindiff, A[j] - A[i]);

        i += 1;
        j += 1;

    # Return answer
    return mindiff;

# Driver Code
if __name__ == '__main__':

    # Given array
    A = [-1, 3, -1, 8, 5, 4];
    K = 3;

    # Prints the minimum possible difference
    print(minDiff(A, K));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum difference
// between largest and smallest element
// after K replacements
static int minDiff(int[] A, int K)
{

    // Sort array in ascending order
    Array.Sort(A);

    // Length of array
    int n = A.Length;

    if (n <= K)
        return 0;

    // Minimum difference
    int mindiff = A[n - 1] - A[0];

    if (K == 0)
        return mindiff;

    // Check for all K + 1 possibilities
    for(int i = 0, j = n - 1 - K; j < n;)
    {
        mindiff = Math.Min(
            mindiff, A[j] - A[i]);

        i++;
        j++;
    }

    // Return answer
    return mindiff;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []A = { -1, 3, -1, 8, 5, 4 };
    int K = 3;

    // Prints the minimum possible difference
    Console.WriteLine(minDiff(A, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find minimum difference
    // between largest and smallest element
    // after K replacements
    function minDiff(A, K)
    {

        // Sort array in ascending order
        A.sort(function(a, b){return a - b});

        // Length of array
        let n = A.length;

        if (n <= K)
            return 0;

        // Minimum difference
        let mindiff = A[n - 1] - A[0];

        if (K == 0)
            return mindiff;

        // Check for all K + 1 possibilities
        for(let i = 0, j = n - 1 - K; j < n;)
        {
            mindiff = Math.min(mindiff, A[j] - A[i]);

            i++;
            j++;
        }

        // Return answer
        return mindiff;
    }

    // Given array
    let A = [ -1, 3, -1, 8, 5, 4 ];
    let K = 3;

    // Prints the minimum possible difference
    document.write(minDiff(A, K));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*

[**堆**](https://www.geeksforgeeks.org/heap-data-structure/) **为主的方法:**这个方法和上面的方法类似。分别使用[最小堆和最大堆](https://www.geeksforgeeks.org/binary-heap/)找到 **K** 最小值和 **K** 最大值数组元素。

按照以下步骤解决问题:

1.  初始化两个[优先级队列](https://www.geeksforgeeks.org/priority-queue-class-in-java-2/)、 [**最小堆**和**最大堆**](https://www.geeksforgeeks.org/binary-heap/) 。
2.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[将所有元素逐一添加到堆](https://www.geeksforgeeks.org/insertion-and-deletion-in-heaps/)中。如果堆的[大小超过 **K** ，在任何堆中，移除队列](https://www.geeksforgeeks.org/priorityqueue-size-method-in-java/)顶部的元素。
3.  将 **K** 的最大和最小元素存储在两个单独的数组中， **maxList** 和 **minList** ，并初始化一个变量，比如说 **minDiff** 来存储最小差值。
4.  [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)对于每个索引，说 **i** ，更新 **minDiff** 为 **minDiff = min(minDiff，maxList[I]-minList[K–1])**并打印 **minDiff** 的最终值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum difference
// between the largest and smallest
// element after K replacements
int minDiff(int A[], int K, int N)
{
    if (N <= K + 1)
        return 0;

    // Create a MaxHeap
    priority_queue<int, vector<int>, greater<int>>
        maxHeap;

    // Create a MinHeap
    priority_queue<int> minHeap;

    // Update maxHeap and MinHeap with highest
    // and smallest K elements respectively
    for (int i = 0; i < N; i++)
    {

        // Insert current element
        // into the MaxHeap
        maxHeap.push(A[i]);

        // If maxHeap size exceeds K + 1
        if (maxHeap.size() > K + 1)

            // Remove top element
            maxHeap.pop();

        // Insert current element
        // into the MaxHeap
        minHeap.push(A[i]);

        // If maxHeap size exceeds K + 1
        if (minHeap.size() > K + 1)

            // Remove top element
            minHeap.pop();
    }

    // Store all max element from maxHeap
    vector<int> maxList;
    while (maxHeap.size() > 0)
    {
        maxList.push_back(maxHeap.top());
        maxHeap.pop();
    }

    // Store all min element from minHeap
    vector<int> minList;
    while (minHeap.size() > 0)
    {
        minList.push_back(minHeap.top());
        minHeap.pop();
    }

    int mindiff = INT_MAX;

    // Generating all K + 1 possibilities
    for (int i = 0; i <= K; i++)
    {
        mindiff = min(mindiff, maxList[i] - minList[K - i]);
    }

    // Return answer
    return mindiff;
}

// Driver Code
int main()
{

    // Given array
    int A[] = { -1, 3, -1, 8, 5, 4 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 3;

    // Function call
    cout << minDiff(A, K, N);
    return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to find minimum difference
    // between the largest and smallest
    // element after K replacements
    static int minDiff(int[] A, int K)
    {
        if (A.length <= K + 1)
            return 0;

        // Create a MaxHeap
        PriorityQueue<Integer> maxHeap
            = new PriorityQueue<>();

        // Create a MinHeap
        PriorityQueue<Integer> minHeap
            = new PriorityQueue<>(
                Collections.reverseOrder());

        // Update maxHeap and MinHeap with highest
        // and smallest K elements respectively
        for (int n : A) {

            // Insert current element
            // into the MaxHeap
            maxHeap.add(n);

            // If maxHeap size exceeds K + 1
            if (maxHeap.size() > K + 1)

                // Remove top element
                maxHeap.poll();

            // Insert current element
            // into the MaxHeap
            minHeap.add(n);

            // If maxHeap size exceeds K + 1
            if (minHeap.size() > K + 1)

                // Remove top element
                minHeap.poll();
        }

        // Store all max element from maxHeap
        List<Integer> maxList = new ArrayList<>();
        while (maxHeap.size() > 0)
            maxList.add(maxHeap.poll());

        // Store all min element from minHeap
        List<Integer> minList = new ArrayList<>();
        while (minHeap.size() > 0)
            minList.add(minHeap.poll());

        int mindiff = Integer.MAX_VALUE;

        // Generating all K + 1 possibilities
        for (int i = 0; i <= K; i++) {
            mindiff = Math.min(mindiff,
                               maxList.get(i)
                                   - minList.get(K - i));
        }
        // Return answer
        return mindiff;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int A[] = { -1, 3, -1, 8, 5, 4 };
        int K = 3;

        // Function call
        System.out.println(minDiff(A, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach
import sys

# Function to find minimum difference
# between the largest and smallest
# element after K replacements
def minDiff(A, K) :
    if (len(A) <= K + 1) :
        return 0

    # Create a MaxHeap
    maxHeap = []

    # Create a MinHeap
    minHeap = []

    # Update maxHeap and MinHeap with highest
    # and smallest K elements respectively
    for n in A :

        # Insert current element
        # into the MaxHeap
        maxHeap.append(n)
        maxHeap.sort()

        # If maxHeap size exceeds K + 1
        if (len(maxHeap) > K + 1) :

            # Remove top element
            del maxHeap[0]

        # Insert current element
        # into the MaxHeap
        minHeap.append(n)
        minHeap.sort()
        minHeap.reverse()

        # If maxHeap size exceeds K + 1
        if (len(minHeap) > K + 1) :

            # Remove top element
            del minHeap[0]

    # Store all max element from maxHeap
    maxList = []

    while (len(maxHeap) > 0) :

        maxList.append(maxHeap[0])
        del maxHeap[0]

    # Store all min element from minHeap
    minList = []

    while (len(minHeap) > 0) : 
        minList.append(minHeap[0])
        del minHeap[0]
    mindiff = sys.maxsize

    # Generating all K + 1 possibilities
    for i in range(K) :

        mindiff = min(mindiff, maxList[i] - minList[K - i])

    # Return answer
    return mindiff

# Given array
A = [ -1, 3, -1, 8, 5, 4 ]
K = 3

# Function call
print(minDiff(A, K))

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum difference
// between the largest and smallest
// element after K replacements
static int minDiff(int[] A, int K)
{
    if (A.Length <= K + 1)
        return 0;

    // Create a MaxHeap
    List<int> maxHeap = new List<int>();

    // Create a MinHeap
    List<int> minHeap = new List<int>();

    // Update maxHeap and MinHeap with highest
    // and smallest K elements respectively
    foreach(int n in A)
    {

        // Insert current element
        // into the MaxHeap
        maxHeap.Add(n);
        maxHeap.Sort();

        // If maxHeap size exceeds K + 1
        if (maxHeap.Count > K + 1)

            // Remove top element
            maxHeap.RemoveAt(0);

        // Insert current element
        // into the MaxHeap
        minHeap.Add(n);
        minHeap.Sort();
        minHeap.Reverse();

        // If maxHeap size exceeds K + 1
        if (minHeap.Count > K + 1)

            // Remove top element
            minHeap.RemoveAt(0);
    }

    // Store all max element from maxHeap
    List<int> maxList = new List<int>();

    while (maxHeap.Count > 0)
    {
        maxList.Add(maxHeap[0]);
        maxHeap.RemoveAt(0);
    }

    // Store all min element from minHeap
    List<int> minList = new List<int>();

    while (minHeap.Count > 0)
    {
        minList.Add(minHeap[0]);
        minHeap.RemoveAt(0);
    }

    int mindiff = Int32.MaxValue;

    // Generating all K + 1 possibilities
    for(int i = 0; i < K; i++)
    {
        mindiff = Math.Min(mindiff,
                           maxList[i] -
                           minList[K - i]);
    }

    // Return answer
    return mindiff;
}

// Driver code
static void Main()
{

    // Given array
    int[] A = { -1, 3, -1, 8, 5, 4 };
    int K = 3;

    // Function call
    Console.WriteLine(minDiff(A, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to find minimum difference
// between the largest and smallest
// element after K replacements
function minDiff(A, K, N)
{
    if (N <= K + 1)
        return 0;

    // Create a MaxHeap
    var maxHeap = [];

    // Create a MinHeap
    var minHeap = [];

    // Update maxHeap and MinHeap with highest
    // and smallest K elements respectively
    for (var i = 0; i < N; i++)
    {

        // Insert current element
        // into the MaxHeap
        maxHeap.push(A[i]);
        maxHeap.sort((a,b)=>b-a);

        // If maxHeap size exceeds K + 1
        if (maxHeap.length > K + 1)

            // Remove top element
            maxHeap.pop();

        // Insert current element
        // into the MaxHeap
        minHeap.push(A[i]);
        minHeap.sort((a,b)=>a-b);

        // If maxHeap size exceeds K + 1
        if (minHeap.length > K + 1)

            // Remove top element
            minHeap.pop();
    }

    // Store all max element from maxHeap
    var maxList = [];
    while (maxHeap.length > 0)
    {
        maxList.push(maxHeap[maxHeap.length-1]);
        maxHeap.pop();
    }

    // Store all min element from minHeap
    var minList = [];
    while (minHeap.length > 0)
    {
        minList.push(minHeap[minHeap.length-1]);
        minHeap.pop();
    }

    var mindiff = 1000000000;

    // Generating all K + 1 possibilities
    for (var i = 0; i <= K; i++)
    {
        mindiff = Math.min(mindiff, maxList[i] - minList[K - i]);
    }

    // Return answer
    return mindiff;
}

// Driver Code
// Given array
var A = [-1, 3, -1, 8, 5, 4];
var N = A.length;
var K = 3;

// Function call
document.write(minDiff(A, K, N));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)，其中 N 是给定数组的大小。*
***辅助空间:** O(N)*