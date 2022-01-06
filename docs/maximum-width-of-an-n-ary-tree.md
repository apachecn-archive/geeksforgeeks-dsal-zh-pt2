# N 元树的最大宽度

> 原文:[https://www . geesforgeks . org/an-n-ary-tree 最大宽度/](https://www.geeksforgeeks.org/maximum-width-of-an-n-ary-tree/)

给定一棵 [**N 元**树](https://www.geeksforgeeks.org/tag/n-ary-tree/)，任务是找到给定树的最大宽度。树的最大宽度是所有级别中最大的宽度。

**示例:**

> **输入:**
> 
> ```
>                    4
>                  / | \
>                 2  3 -5
>                / \    /\
>              -1   3 -2  6
> ```
> 
> **输出:**4
> T3】说明:T5】宽度为 0 <sup>第</sup>级为 1。
> 宽度为 1 <sup>st</sup> 等级为 3。
> 2<sup>和</sup>级宽度为 4。
> 因此，最大宽度为 4
> 
> **输入:**
> 
> ```
>               1
>             / | \
>            2  -1  3
>          /  \      \
>         4    5      8
>       /           / | \
>      2           6  12  7  
> ```
> 
> **输出:** 4

**进场:**这个问题可以用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 解决。想法是执行树的[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。遍历时，分别处理不同级别的节点。对于正在处理的每个级别，计算每个级别上存在的节点数，并跟踪最大计数。按照以下步骤解决问题:

1.  初始化一个变量，比如**最大宽度**来存储树的最大宽度。
2.  初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)来执行给定树的[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
3.  将根节点推入队列。
4.  如果任何级别的队列大小超过**最大宽度**，则将**最大宽度**更新为**T5 队列大小。**
5.  遍历队列，将下一级的所有节点推入队列，弹出当前级的所有节点。
6.  重复以上步骤，直到遍历树的所有级别。
7.  最后，返回**最大宽度**的最终值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum width of
// the tree using level order traversal
int maxWidth(int N, int M,
             vector<int> cost,
             vector<vector<int> > s)
{
    // Store the edges of the tree
    vector<int> adj[N];
    for (int i = 0; i < M; i++) {
        adj[s[i][0]].push_back(
            s[i][1]);
    }

    // Stores maximum width
    // of the tree
    int result = 0;

    // Stores the nodes
    // of each level
    queue<int> q;

    // Insert root node
    q.push(0);

    // Perform level order
    // traversal on the tree
    while (!q.empty()) {

        // Stores the size of
        // the queue
        int count = q.size();

        // Update maximum width
        result = max(count, result);

        // Push the nodes of the next
        // level and pop the elements
        // of the current level
        while (count--) {

            // Get element from the
            // front the Queue
            int temp = q.front();
            q.pop();

            // Push all nodes of the next level.
            for (int i = 0; i < adj[temp].size();
                 i++) {
                q.push(adj[temp][i]);
            }
        }
    }

    // Return the result.
    return result;
}

// Driver Code
int main()
{
    int N = 11, M = 10;

    vector<vector<int> > edges;
    edges.push_back({ 0, 1 });
    edges.push_back({ 0, 2 });
    edges.push_back({ 0, 3 });
    edges.push_back({ 1, 4 });
    edges.push_back({ 1, 5 });
    edges.push_back({ 3, 6 });
    edges.push_back({ 4, 7 });
    edges.push_back({ 6, 10 });
    edges.push_back({ 6, 8 });
    edges.push_back({ 6, 9 });

    vector<int> cost
        = { 1, 2, -1, 3, 4, 5,
            8, 2, 6, 12, 7 };

    /* Constructed tree is:
                1
              / | \
            2  -1  3
          /  \      \
         4    5      8
        /          / | \
       2          6  12  7
    */

    cout << maxWidth(N, M, cost, edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to find the maximum width of
    // the tree using level order traversal
    static int maxWidth(int N, int M,ArrayList<Integer> cost,
                        ArrayList<ArrayList<Integer> > s)
    {

        // Store the edges of the tree
        ArrayList<ArrayList<Integer> > adj =
          new ArrayList<ArrayList<Integer> >();
        for(int i = 0; i < N; i++)
        {
            adj.add(new ArrayList<Integer>());
        }
        for(int i = 0; i < M; i++)
        {
            adj.get(s.get(i).get(0)).add(s.get(i).get(1));
        }

        // Stores maximum width
        // of the tree
        int result = 0;

        // Stores the nodes
        // of each level
        Queue<Integer> q = new LinkedList<>();

        // Insert root node
        q.add(0);

        // Perform level order
        // traversal on the tree
        while(q.size() != 0)
        {

            // Stores the size of
            // the queue
            int count = q.size();

            // Update maximum width
            result = Math.max(count, result);

            // Push the nodes of the next
            // level and pop the elements
            // of the current level
            while(count-->0)
            {

                // Get element from the
                // front the Queue
                 int temp = q.remove();

                // Push all nodes of the next level.
                 for(int i = 0; i < adj.get(temp).size(); i++)
                 {
                     q.add(adj.get(temp).get(i));
                 }
            }
        }

        // Return the result.
        return result;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int N = 11, M = 10;
        ArrayList<ArrayList<Integer> > edges = new ArrayList<ArrayList<Integer> >();
        edges.add(new ArrayList<Integer>(Arrays.asList( 0, 1)));
        edges.add(new ArrayList<Integer>(Arrays.asList( 0, 2)));
        edges.add(new ArrayList<Integer>(Arrays.asList( 0, 3)));
        edges.add(new ArrayList<Integer>(Arrays.asList(1,4)));
        edges.add(new ArrayList<Integer>(Arrays.asList(1,5)));
        edges.add(new ArrayList<Integer>(Arrays.asList(3,6)));
        edges.add(new ArrayList<Integer>(Arrays.asList(4,7)));
        edges.add(new ArrayList<Integer>(Arrays.asList(6,10)));
        edges.add(new ArrayList<Integer>(Arrays.asList(6,8)));
        edges.add(new ArrayList<Integer>(Arrays.asList(6,9)));

        ArrayList<Integer> cost = new ArrayList<Integer>(Arrays.asList(1, 2, -1, 3, 4, 5,8, 2, 6, 12, 7 ));       
        /* Constructed tree is:
                1
              / | \
            2  -1  3
          /  \      \
         4    5      8
        /          / | \
       2          6  12  7
    */
        System.out.println(maxWidth(N, M, cost, edges));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import deque

# Function to find the maximum width of
#. he tree using level order traversal
def maxWidth(N, M, cost, s):

    # Store the edges of the tree
    adj = [[] for i in range(N)]
    for i in range(M):
        adj[s[i][0]].append(s[i][1])

    # Stores maximum width
    # of the tree
    result = 0

    # Stores the nodes
    # of each level
    q = deque()

    # Insert root node
    q.append(0)

    # Perform level order
    # traversal on the tree
    while (len(q) > 0):

        # Stores the size of
        # the queue
        count = len(q)

        # Update maximum width
        result = max(count, result)

        # Push the nodes of the next
        # level and pop the elements
        # of the current level
        while (count > 0):

            # Get element from the
            # front the Queue
            temp = q.popleft()

            # Push all nodes of the next level.
            for i in adj[temp]:
                q.append(i)

            count -= 1

    # Return the result.
    return result

# Driver Code
if __name__ == '__main__':

    N = 11
    M = 10

    edges = []
    edges.append([0, 1])
    edges.append([0, 2])
    edges.append([0, 3])
    edges.append([1, 4])
    edges.append([1, 5])
    edges.append([3, 6])
    edges.append([4, 7])
    edges.append([6, 1])
    edges.append([6, 8])
    edges.append([6, 9])

    cost = [ 1, 2, -1, 3, 4, 5,
             8, 2, 6, 12, 7]

    # Constructed tree is:
    #           1
    #         / | \
    #        2 -1  3
    #       / \       \
    #      4   5        8
    #     /          / | \
    #  2         6  12  7
    print(maxWidth(N, M, cost, edges))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum width of
// the tree using level order traversal
static int maxWidth(int N, int M, List<int> cost,
                             List<List<int>> s)
{

    // Store the edges of the tree
    List<List<int>> adj = new List<List<int>>();
    for(int i = 0; i < N; i++)
    {
        adj.Add(new List<int>());
    }

    for(int i = 0; i < M; i++)
    {
        adj[s[i][0]].Add(s[i][1]);
    }

    // Stores maximum width
    // of the tree
    int result = 0;

    // Stores the nodes
    // of each level
    Queue<int> q = new Queue<int>();

    // Insert root node
    q.Enqueue(0);

    // Perform level order
    // traversal on the tree
    while (q.Count != 0)
    {

        // Stores the size of
        // the queue
        int count = q.Count;

        // Update maximum width
        result = Math.Max(count, result);

        // Push the nodes of the next
        // level and pop the elements
        // of the current level
        while (count-- > 0)
        {

            // Get element from the
            // front the Queue
            int temp = q.Dequeue();

            // Push all nodes of the next level.
            for(int i = 0; i < adj[temp].Count; i++)
            {
                q.Enqueue(adj[temp][i]);
            }
        }
    }

    // Return the result.
    return result;
}

// Driver Code
static public void Main()
{
    int N = 11, M = 10;

    List<List<int>> edges = new List<List<int>>();
    edges.Add(new List<int>(){0, 1});
    edges.Add(new List<int>(){0, 2});
    edges.Add(new List<int>(){0, 3});
    edges.Add(new List<int>(){1, 4});
    edges.Add(new List<int>(){1, 5});
    edges.Add(new List<int>(){3, 6});
    edges.Add(new List<int>(){4, 7});
    edges.Add(new List<int>(){6, 10});
    edges.Add(new List<int>(){6, 8});
    edges.Add(new List<int>(){6, 9});

    List<int> cost = new List<int>(){ 1, 2, -1, 3,
                                      4, 5, 8, 2,
                                      6, 12, 7 };
    /* Constructed tree is:
            1
          / | \
        2  -1  3
      /  \      \
     4    5      8
    /          / | \
   2          6  12  7
    */

    Console.WriteLine(maxWidth(N, M, cost, edges));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to find the maximum width of
    // the tree using level order traversal
    function maxWidth(N, M, cost, s)
    {

        // Store the edges of the tree
        let adj = [];
        for(let i = 0; i < N; i++)
        {
            adj.push([]);
        }
        for(let i = 0; i < M; i++)
        {
            adj[s[i][0]].push(s[i][1]);
        }

        // Stores maximum width
        // of the tree
        let result = 0;

        // Stores the nodes
        // of each level
        let q = [];

        // Insert root node
        q.push(0);

        // Perform level order
        // traversal on the tree
        while(q.length != 0)
        {

            // Stores the size of
            // the queue
            let count = q.length;

            // Update maximum width
            result = Math.max(count, result);

            // Push the nodes of the next
            // level and pop the elements
            // of the current level
            while(count-->0)
            {

                // Get element from the
                // front the Queue
                 let temp = q.shift();

                // Push all nodes of the next level.
                 for(let i = 0; i < adj[temp].length; i++)
                 {
                     q.push(adj[temp][i]);
                 }
            }
        }

        // Return the result.
        return result;
    }

    let N = 11, M = 10;
    let edges = [];
    edges.push([ 0, 1]);
    edges.push([ 0, 2]);
    edges.push([ 0, 3]);
    edges.push([1,4]);
    edges.push([1,5]);
    edges.push([3,6]);
    edges.push([4,7]);
    edges.push([6,10]);
    edges.push([6,8]);
    edges.push([6,9]);

    let cost = [1, 2, -1, 3, 4, 5,8, 2, 6, 12, 7 ];      
    /* Constructed tree is:
                  1
                / | \
              2  -1  3
            /  \      \
           4    5      8
          /          / | \
         2          6  12  7
      */
    document.write(maxWidth(N, M, cost, edges));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)