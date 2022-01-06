# 尽量减少到达数组末尾所需的步数|设置 2

> 原文:[https://www . geeksforgeeks . org/最小化到达阵列末端所需的步骤数集-2/](https://www.geeksforgeeks.org/minimize-the-number-of-steps-required-to-reach-the-end-of-the-array-set-2/)

给定一个由正整数组成的长度为 **N** 的整数数组 **arr[]** ，任务是从 **arr[0]** 开始最小化到达**arr[N–1]**所需的步数。在给定的步骤中，如果我们在索引 **i** 处，我们可以转到索引**I–arr[I]**或 **i + arr[i]** ，因为我们以前没有访问过这些索引。此外，我们不能超出数组的界限。没有可能的话打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，1，1}
> **输出:** 2
> 路径将为 0 - > 1 - > 2。
> **输入:** arr[] = {2，1}
> **输出:** -1

**方法:**我们已经在[这篇](https://www.geeksforgeeks.org/minimize-the-number-of-steps-required-to-reach-the-end-of-the-array/)文章中讨论了一种基于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的方法，其时间复杂度为 **O(n * 2 <sup>n</sup> )** 。
这里我们将讨论一个基于 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的解决方案:

1.  这个问题可以可视化为一个有向图，其中**I<sup>th</sup>T3】细胞与细胞 **i + arr[i]** 和**I–arr[I]**相连。**
2.  这个图没有加权。

由于以上原因，BFS 可以用来寻找 **0 <sup>th</sup>** 和**(N–1)<sup>th</sup>**索引之间的最短路径。我们将使用以下算法:

1.  在队列中推送索引 **0** 。
2.  将所有相邻单元格推到队列中的 **0** 。
3.  重复上述步骤，即如果队列中的所有元素以前没有被访问/遍历过，则再次单独遍历它们。
4.  重复，直到我们没有达到指标**N–1**。
5.  这个遍历的深度将给出到达终点所需的最小步数。

记住在遍历完一个单元格后，将其标记为已访问。为此，我们将使用布尔数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum steps
// required to reach the end
// of the given array
int minSteps(int arr[], int n)
{
    // Array to determine whether
    // a cell has been visited before
    bool v[n] = { 0 };

    // Queue for bfs
    queue<int> q;

    // Push the source i.e. index 0
    q.push(0);

    // Variable to store
    // the depth of search
    int depth = 0;

    // BFS algorithm
    while (q.size() != 0) {

        // Current queue size
        int x = q.size();
        while (x--) {

            // Top-most element of queue
            int i = q.front();
            q.pop();

            // Base case
            if (v[i])
                continue;

            // If we reach the destination
            // i.e. index (n - 1)
            if (i == n - 1)
                return depth;

            // Marking the cell visited
            v[i] = 1;

            // Pushing the adjacent nodes
            // i.e. indices reachable
            // from the current index
            if (i + arr[i] < n)
                q.push(i + arr[i]);
            if (i - arr[i] >= 0)
                q.push(i - arr[i]);
        }
        depth++;
    }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << minSteps(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum steps
// required to reach the end
// of the given array
static int minSteps(int arr[], int n)
{
    // Array to determine whether
    // a cell has been visited before
    boolean[] v = new boolean[n];

    // Queue for bfs
    Queue<Integer> q = new LinkedList<>();

    // Push the source i.e. index 0
    q.add(0);

    // Variable to store
    // the depth of search
    int depth = 0;

    // BFS algorithm
    while (q.size() > 0)
    {

        // Current queue size
        int x = q.size();
        while (x-- > 0)
        {

            // Top-most element of queue
            int i = q.peek();
            q.poll();

            // Base case
            if (v[i])
                continue;

            // If we reach the destination
            // i.e. index (n - 1)
            if (i == n - 1)
                return depth;

            // Marking the cell visited
            v[i] = true;

            // Pushing the adjacent nodes
            // i.e. indices reachable
            // from the current index
            if (i + arr[i] < n)
                q.add(i + arr[i]);
            if (i - arr[i] >= 0)
                q.add(i - arr[i]);
        }
        depth++;
    }

    return -1;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 1, 1, 1 };
    int n = arr.length;
    System.out.println(minSteps(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum steps
# required to reach the end
# of the given array
def minSteps(arr,n):

    # Array to determine whether
    # a cell has been visited before
    v = [0 for i in range(n)]

    # Queue for bfs
    q = []

    # Push the source i.e. index 0
    q.append(0)

    # Variable to store
    # the depth of search
    depth = 0

    # BFS algorithm
    while (len(q) != 0):
        # Current queue size
        x = len(q)
        while (x >= 1):
            # Top-most element of queue
            i = q[0]
            q.remove(i)

            x -= 1

            # Base case
            if (v[i]):
                continue;

            # If we reach the destination
            # i.e. index (n - 1)
            if (i == n - 1):
                return depth

            # Marking the cell visited
            v[i] = 1

            # Pushing the adjacent nodes
            # i.e. indices reachable
            # from the current index
            if (i + arr[i] < n):
                q.append(i + arr[i])
            if (i - arr[i] >= 0):
                q.append(i - arr[i])

        depth += 1

    return -1

# Driver code
if __name__ == '__main__':
    arr = [1, 1, 1, 1, 1, 1]
    n = len(arr)

    print(minSteps(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// A C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the minimum steps
// required to reach the end
// of the given array
static int minSteps(int []arr, int n)
{
    // Array to determine whether
    // a cell has been visited before
    Boolean[] v = new Boolean[n];

    // Queue for bfs
    Queue<int> q = new Queue<int>();

    // Push the source i.e. index 0
    q.Enqueue(0);

    // Variable to store
    // the depth of search
    int depth = 0;

    // BFS algorithm
    while (q.Count > 0)
    {

        // Current queue size
        int x = q.Count;
        while (x-- > 0)
        {

            // Top-most element of queue
            int i = q.Peek();
            q.Dequeue();

            // Base case
            if (v[i])
                continue;

            // If we reach the destination
            // i.e. index (n - 1)
            if (i == n - 1)
                return depth;

            // Marking the cell visited
            v[i] = true;

            // Pushing the adjacent nodes
            // i.e. indices reachable
            // from the current index
            if (i + arr[i] < n)
                q.Enqueue(i + arr[i]);
            if (i - arr[i] >= 0)
                q.Enqueue(i - arr[i]);
        }
        depth++;
    }

    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 1, 1, 1, 1 };
    int n = arr.Length;
    Console.WriteLine(minSteps(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum steps
// required to reach the end
// of the given array
function minSteps(arr, n)
{
    // Array to determine whether
    // a cell has been visited before
    var v = Array(n).fill(0);

    // Queue for bfs
    var q = [];

    // Push the source i.e. index 0
    q.push(0);

    // Variable to store
    // the depth of search
    var depth = 0;

    // BFS algorithm
    while (q.length != 0) {

        // Current queue size
        var x = q.length;
        while (x--) {

            // Top-most element of queue
            var i = q[0];
            q.shift();

            // Base case
            if (v[i])
                continue;

            // If we reach the destination
            // i.e. index (n - 1)
            if (i == n - 1)
                return depth;

            // Marking the cell visited
            v[i] = 1;

            // Pushing the adjacent nodes
            // i.e. indices reachable
            // from the current index
            if (i + arr[i] < n)
                q.push(i + arr[i]);
            if (i - arr[i] >= 0)
                q.push(i - arr[i]);
        }
        depth++;
    }

    return -1;
}

// Driver code
var arr = [1, 1, 1, 1, 1, 1];
var n = arr.length;
document.write( minSteps(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)