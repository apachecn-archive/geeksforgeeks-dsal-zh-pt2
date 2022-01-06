# 根据给定的约束条件在数组中形成循环的元素数

> 原文:[https://www . geeksforgeeks . org/根据给定约束形成数组循环的元素计数/](https://www.geeksforgeeks.org/count-of-elements-which-form-a-loop-in-an-array-according-to-given-constraints/)

给定一个包含 **N** 个整数的**数组 A** ，任务是根据以下条件计算数组中形成循环的元素数量。
从索引 **i** 开始遍历数组，跳转到下一个连接的索引。如果 **j = GCD(i，A[i]) % N** ，则 A **有向边从 A 的索引 I 退出到索引 j** 。如果按照所描述的顺序遍历数组，索引 I 再次被访问，那么索引 I 被称为在数组中形成一个循环。
**示例:**

> **输入:** A = { 1，1，6，2 }
> **输出:** 2
> **解释:**
> 给定条件下可能的遍历为:
> 0->1->1
> 1->1
> 2->2
> 3->2->2
> 显然，只有顶点 1 和 2 形成一个循环。
> **输入:** A = {0，0，0，6}
> **输出:** 4
> **解释:**
> 给定条件下可能的遍历为:
> 0->0
> 1->1
> 2->2
> 3->3
> 很明显，所有顶点形成一个循环。

**方法:**
为了解决上面提到的问题，我们必须假设每个**指数代表图中的单个节点**。

*   如果 j = GCD(i，A[i]) % n，则每个节点都有一条从 A 的索引 I 到索引 j 的有向边。如果遍历从节点 I 开始
*   节点 I 将被称为该遍历的**父节点**，并且该父节点将被分配给遍历期间访问的所有节点。
*   当遍历图时，如果我们发现一个已经被访问的节点，并且该被访问节点的父节点与遍历的父节点相同，则检测到新的循环。
*   现在，这个循环中的每个节点都将被计算在内，因为它们每个都在形成循环。要计算该周期中的节点数，从该节点开始另一个 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，直到该节点不再被访问。
*   对图的每个节点 I 重复这个过程。

在最坏的情况下，每个节点最多将被遍历 3 次。因此解具有线性时间复杂度。
以下是上述方法的实施:

## C++

```
// C++ program to number of elements
// which form a cycle in an array

#include <bits/stdc++.h>
using namespace std;

#define mp make_pair
#define pb push_back
#define mod 1000000007

// Function to count number of
// elements forming a cycle
int solve(int A[], int n)
{
    int i, cnt = 0, j;

    // Array to store parent
    // node of traversal.
    int parent[n];

    // Array to determine
    // whether current node
    // is already counted
    // in the cycle.
    int vis[n];

    // Initialize the arrays.
    memset(parent, -1, sizeof(parent));
    memset(vis, 0, sizeof(vis));

    for (i = 0; i < n; i++) {
        j = i;

        // Check if current node is already
        // traversed or not. If node is not
        // traversed yet then parent value
        // will be -1.
        if (parent[j] == -1) {

            // Traverse the graph until an
            // already visited node is not
            // found.
            while (parent[j] == -1) {
                parent[j] = i;
                j = __gcd(j, A[j]) % n;
            }

            // Check parent value to ensure
            // a cycle is present.
            if (parent[j] == i) {

                // Count number of nodes in
                // the cycle.
                while (!vis[j]) {
                    vis[j] = 1;
                    cnt++;
                    j = __gcd(j, A[j]) % n;
                }
            }
        }
    }

    return cnt;
}

int main()
{
    int A[] = { 1, 1, 6, 2 };
    int n = sizeof(A) / sizeof(A[0]);
    cout << solve(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to number of elements
// which form a cycle in an array
import java.util.*;
class GFG{

static final int mod = 1000000007;

// Function to count number of
// elements forming a cycle
static int solve(int A[], int n)
{
    int i, cnt = 0, j;

    // Array to store parent
    // node of traversal.
    int []parent = new int[n];

    // Array to determine
    // whether current node
    // is already counted
    // in the cycle.
    int []vis = new int[n];

    // Initialize the arrays.
    Arrays.fill(parent, -1);
    Arrays.fill(vis, 0);

    for(i = 0; i < n; i++)
    {
        j = i;

        // Check if current node is already
        // traversed or not. If node is not
        // traversed yet then parent value
        // will be -1.
        if (parent[j] == -1)
        {

            // Traverse the graph until an
            // already visited node is not
            // found.
            while (parent[j] == -1)
            {
                parent[j] = i;
                j = __gcd(j, A[j]) % n;
            }

            // Check parent value to ensure
            // a cycle is present.
            if (parent[j] == i)
            {

                // Count number of nodes in
                // the cycle.
                while (vis[j] == 0)
                {
                    vis[j] = 1;
                    cnt++;
                    j = __gcd(j, A[j]) % n;
                }
            }
        }
    }
    return cnt;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 1, 1, 6, 2 };
    int n = A.length;

    System.out.print(solve(A, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to number of elements
# which form a cycle in an array
import math

mod = 1000000007

# Function to count number of
# elements forming a cycle
def solve(A, n):

    cnt = 0

    # Array to store parent
    # node of traversal.
    parent = [-1] * n

    # Array to determine
    # whether current node
    # is already counted
    # in the cycle.
    vis = [0] * n

    for i in range(n):
        j = i

        # Check if current node is already
        # traversed or not. If node is not
        # traversed yet then parent value
        # will be -1.
        if (parent[j] == -1):

            # Traverse the graph until an
            # already visited node is not
            # found.
            while (parent[j] == -1):
                parent[j] = i
                j = math.gcd(j, A[j]) % n

            # Check parent value to ensure
            # a cycle is present.
            if (parent[j] == i):

                # Count number of nodes in
                # the cycle.
                while (vis[j] == 0):
                    vis[j] = 1
                    cnt += 1
                    j = math.gcd(j, A[j]) % n

    return cnt

# Driver code
A = [ 1, 1, 6, 2 ]
n = len(A)

print(solve(A, n))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to number of elements
// which form a cycle in an array
using System;

class GFG{

// Function to count number of
// elements forming a cycle
static int solve(int[] A, int n)
{
    int i, cnt = 0, j;

    // Array to store parent
    // node of traversal.
    int[] parent = new int[n];

    // Array to determine
    // whether current node
    // is already counted
    // in the cycle.
    int[] vis = new int[n];

    // Initialize the arrays.
    Array.Fill(parent, -1);
    Array.Fill(vis, 0);

    for(i = 0; i < n; i++)
    {
        j = i;

        // Check if current node is already
        // traversed or not. If node is not
        // traversed yet then parent value
        // will be -1.
        if (parent[j] == -1)
        {

            // Traverse the graph until an
            // already visited node is not
            // found.
            while (parent[j] == -1)
            {
                parent[j] = i;
                j = __gcd(j, A[j]) % n;
            }

            // Check parent value to ensure
            // a cycle is present.
            if (parent[j] == i)
            {

                // Count number of nodes in
                // the cycle.
                while (vis[j] == 0)
                {
                    vis[j] = 1;
                    cnt++;
                    j = __gcd(j, A[j]) % n;
                }
            }
        }
    }
    return cnt;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
static void Main()
{
    int[] A = { 1, 1, 6, 2 };
    int n = A.Length;

    Console.WriteLine(solve(A, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // JavaScript program to number of elements
    // which form a cycle in an array

    // Function to count number of
    // elements forming a cycle
    function solve(A, n)
    {
        let i, cnt = 0, j;

        // Array to store parent
        // node of traversal.
        let parent = new Array(n);

        // Array to determine
        // whether current node
        // is already counted
        // in the cycle.
        let vis = new Array(n);

        // Initialize the arrays.
        parent.fill(-1);
        vis.fill(0);

        for(i = 0; i < n; i++)
        {
            j = i;

            // Check if current node is already
            // traversed or not. If node is not
            // traversed yet then parent value
            // will be -1.
            if (parent[j] == -1)
            {

                // Traverse the graph until an
                // already visited node is not
                // found.
                while (parent[j] == -1)
                {
                    parent[j] = i;
                    j = __gcd(j, A[j]) % n;
                }

                // Check parent value to ensure
                // a cycle is present.
                if (parent[j] == i)
                {

                    // Count number of nodes in
                    // the cycle.
                    while (vis[j] == 0)
                    {
                        vis[j] = 1;
                        cnt++;
                        j = __gcd(j, A[j]) % n;
                    }
                }
            }
        }
        return cnt;
    }

    function __gcd(a, b)
    {
        return b == 0 ? a : __gcd(b, a % b);    
    }

    let A = [ 1, 1, 6, 2 ];
    let n = A.length;

    document.write(solve(A, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***空间复杂度:** O(N)*