# 阵列中的魔法指数

> 原文:[https://www.geeksforgeeks.org/magical-indices-array/](https://www.geeksforgeeks.org/magical-indices-array/)

给定一个整数数组。如果 j = (i + A[i]) % n + 1(假设基于 1 的索引)，则 A 的索引 I 被称为连接到索引 j。从索引 I 开始遍历数组，并跳转到下一个连接的索引。如果按照所描述的顺序遍历数组，索引 I 再次被访问，那么索引 I 就是一个神奇的索引。计算数组中魔法索引的数量。假设数组 A 由非负整数组成。

**示例:**

```
Input : A = {1, 1, 1, 1}
Output : 4
Possible traversals:
1 -> 3 -> 1
2 -> 4 -> 2
3 -> 1 -> 3
4 -> 2 -> 4
Clearly all the indices are magical

Input : A = {0, 0, 0, 2}
Output : 2
Possible traversals:
1 -> 2 -> 3 -> 4 -> 3...
2 -> 3 -> 4 -> 3...
3 -> 4 -> 3
4 -> 3 ->4
Magical indices = 3, 4
```

**方法:**问题是计算图中存在的所有循环中的节点数。每个索引代表图中的一个节点。每个节点都有一条有向边，如问题陈述中所述。这个图有一个特殊的属性:从任意顶点开始遍历时，总是会检测到一个循环。该属性将有助于降低解决方案的时间复杂性。

阅读这篇关于如何检测有向图中的循环的帖子:[检测有向图中的循环](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)
让遍历从节点 I 开始。节点 I 将被称为该遍历的父节点，并且该父节点将被分配给遍历期间访问的所有节点。当遍历图时，如果我们发现一个已经被访问的节点，并且该被访问节点的父节点与遍历的父节点相同，则检测到新的循环。要计算此周期中的节点数，请从此节点启动另一个 dfs，直到不再访问该节点。对图的每个节点 I 重复这个过程。在最坏的情况下，每个节点最多将被遍历 3 次。因此解具有线性时间复杂度。

逐步算法是:

```
1\. For each node in the graph:
     if node i is not visited then:
       for every adjacent node j:
         if node j is not visited:
            par[j] = i
         else:
           if par[j]==i
             cycle detected
             count nodes in cycle
2\. return count       
```

**实施:**

## C++

```
// C++ program to find number of magical
// indices in the given array.
#include <bits/stdc++.h>
using namespace std;

#define mp make_pair
#define pb push_back
#define mod 1000000007

// Function to count number of magical indices.
int solve(int A[], int n)
{
    int i, cnt = 0, j;

    // Array to store parent node of traversal.
    int parent[n + 1];

    // Array to determine whether current node
    // is already counted in the cycle.
    int vis[n + 1];

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
                j = (j + A[j] + 1) % n;
            }

            // Check parent value to ensure
            // a cycle is present.
            if (parent[j] == i) {

                // Count number of nodes in
                // the cycle.
                while (!vis[j]) {
                    vis[j] = 1;
                    cnt++;
                    j = (j + A[j] + 1) % n;
                }
            }
        }
    }

    return cnt;
}

int main()
{
    int A[] = { 0, 0, 0, 2 };
    int n = sizeof(A) / sizeof(A[0]);
    cout << solve(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of magical
// indices in the given array.
import java.io.*;
import java.util.*;

public class GFG {

    // Function to count number of magical
    // indices.
    static int solve(int []A, int n)
    {
        int i, cnt = 0, j;

        // Array to store parent node of
        // traversal.
        int []parent = new int[n + 1];

        // Array to determine whether current node
        // is already counted in the cycle.
        int []vis = new int[n + 1];

        // Initialize the arrays.
        for (i = 0; i < n+1; i++) {
            parent[i] = -1;
            vis[i] = 0;
        }

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
                    j = (j + A[j] + 1) % n;
                }

                // Check parent value to ensure
                // a cycle is present.
                if (parent[j] == i) {

                    // Count number of nodes in
                    // the cycle.
                    while (vis[j]==0) {
                        vis[j] = 1;
                        cnt++;
                        j = (j + A[j] + 1) % n;
                    }
                }
            }
        }

        return cnt;
    }

    // Driver code    
    public static void main(String args[])
    {
        int []A = { 0, 0, 0, 2 };
        int n = A.length;
        System.out.print(solve(A, n));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find number of magical
# indices in the given array.

# Function to count number of magical
# indices.
def solve(A, n) :

    cnt = 0

    # Array to store parent node of
    # traversal.
    parent = [None] * (n + 1)

    # Array to determine whether current node
    # is already counted in the cycle.
    vis = [None] * (n + 1)

    # Initialize the arrays.
    for i in range(0, n+1):
        parent[i] = -1
        vis[i] = 0       

    for i in range(0, n):
        j = i

        # Check if current node is already
        # traversed or not. If node is not
        # traversed yet then parent value
        # will be -1.
        if (parent[j] == -1) :

            # Traverse the graph until an
            # already visited node is not
            # found.
            while (parent[j] == -1) :
                parent[j] = i
                j = (j + A[j] + 1) % n

            # Check parent value to ensure
            # a cycle is present.
            if (parent[j] == i) :

                # Count number of nodes in
                # the cycle.
                while (vis[j]==0) :
                    vis[j] = 1
                    cnt = cnt + 1
                    j = (j + A[j] + 1) % n
    return cnt

# Driver code    
A = [ 0, 0, 0, 2 ]
n = len(A)
print (solve(A, n))

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to find number of magical
// indices in the given array.
using System;
using System.Collections.Generic;
using System.Linq;

class GFG {

    // Function to count number of magical
    // indices.
    static int solve(int []A, int n)
    {
        int i, cnt = 0, j;

        // Array to store parent node of
        // traversal.
        int []parent = new int[n + 1];

        // Array to determine whether current node
        // is already counted in the cycle.
        int []vis = new int[n + 1];

        // Initialize the arrays.
        for (i = 0; i < n+1; i++) {
            parent[i] = -1;
            vis[i] = 0;
        }

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
                    j = (j + A[j] + 1) % n;
                }

                // Check parent value to ensure
                // a cycle is present.
                if (parent[j] == i) {

                    // Count number of nodes in
                    // the cycle.
                    while (vis[j]==0) {
                        vis[j] = 1;
                        cnt++;
                        j = (j + A[j] + 1) % n;
                    }
                }
            }
        }

        return cnt;
    }

    // Driver code    
    public static void Main()
    {
        int []A = { 0, 0, 0, 2 };
        int n = A.Length;
        Console.WriteLine(solve(A, n));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// number of magical
// indices in the given
// array.

// Function to count number
// of magical indices.
function solve($A, $n)
{
    $i = 0;
    $cnt = 0;
    $j = 0;

    // Array to store parent 
    // node of traversal.
    $parent = array();

    // Array to determine
    // whether current node
    // is already counted
    // in the cycle.
    $vis = array();

    // Initialize the arrays.
    for ($i = 0; $i < $n + 1; $i++)
    {
        $parent[$i] = -1;
        $vis[$i] = 0;
    }

    for ($i = 0; $i < $n; $i++)
    {
        $j = $i;

        // Check if current node is
        // already traversed or not.
        // If node is not traversed
        // yet then parent value will
        // be -1.
        if ($parent[$j] == -1)
        {

            // Traverse the graph until
            // an already visited node
            // is not found.
            while ($parent[$j] == -1)
            {
                $parent[$j] = $i;
                $j = ($j + $A[$j] + 1) % $n;
            }

            // Check parent value to ensure
            // a cycle is present.
            if ($parent[$j] == $i)
            {

                // Count number of
                // nodes in the cycle.
                while ($vis[$j] == 0)
                {
                    $vis[$j] = 1;
                    $cnt++;
                    $j = ($j + $A[$j] + 1) % $n;
                }
            }
        }
    }

    return $cnt;
}

// Driver code    
$A = array( 0, 0, 0, 2 );
$n = count($A);
echo (solve($A, $n));

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of magical
// indices in the given array.
mod = 1000000007

// Function to count number of magical indices.
function solve(A, n)
{
    var i, cnt = 0, j;

    // Array to store parent node of traversal.
    var parent = new Array(n + 1);

    // Array to determine whether current node
    // is already counted in the cycle.
    var vis = new Array(n + 1);

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
                j = (j + A[j] + 1) % n;
            }

            // Check parent value to ensure
            // a cycle is present.
            if (parent[j] == i)
            {

                // Count number of nodes in
                // the cycle.
                while (!vis[j])
                {
                    vis[j] = 1;
                    cnt++;
                    j = (j + A[j] + 1) % n;
                }
            }
        }
    }
    return cnt;
}

// Driver code
var A = [ 0, 0, 0, 2 ];
var n = A.length;

document.write(solve(A, n));  

// This code is contributed by SoumikMondal

</script>
```

**Output :** 

```
2
```

**时间复杂度:**O(n)
T3】空间复杂度: O(n)