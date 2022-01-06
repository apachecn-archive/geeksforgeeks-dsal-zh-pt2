# N 元树中的最大级别和

> 原文:[https://www . geesforgeks . org/最大级别 n 进制总和树/](https://www.geeksforgeeks.org/maximum-level-sum-in-n-ary-tree/)

给定由值为**【1，N】**的节点和值为【】的数组**组成的 [**N 元树**](https://www.geeksforgeeks.org/generic-treesn-array-trees/) ，其中每个节点 **i** 与值**I**相关联，任务是找到 **N 元树**所有级别的所有节点值之和的最大值。**

**示例:**

> **输入:** N = 8，边[][2] = {{0，1}，{0，2}，{0，3}，{1，4}，{1，5}，{3，6}，{6，7}}，值[] = {4，2，3，-5，-1，3，-2，6}
> **输出:** 6
> **说明:**
> 第 0 <sup>级所有节点之和为 4</sup>
> 第 4<sup>级所有赋之和为 6。
> 因此，树的任意一级的最大和为 6。</sup>
> 
> **输入:** N = 10，边[][2] = {{0，1}，{0，2}，{0，3}，{1，4}，{1，5}，{3，6}，{6，7}，{6，8}，{6，9}，值[] = {1，2，-1，3，4，5，8，6，12，7}
> **输出:** 25

**方法:**这个问题可以使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)解决。在执行遍历时，分别处理不同级别的节点。对于正在处理的每个级别，计算该级别的节点总和，并跟踪最大总和。遵循以下步骤:

1.  将当前级别的所有子节点存储在[队列](https://www.geeksforgeeks.org/queue-data-structure/)中，然后在完成特定级别的[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)后，统计当前级别的节点总数。
2.  由于队列现在包含下一级的所有节点，所以通过遍历队列可以很容易地计算出下一级的节点总数。
3.  对连续的级别遵循相同的过程，并更新在每个级别找到的最大节点总数。
4.  完成上述步骤后，打印存储值的最大总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// a level in N-ary treeusing BFS
int maxLevelSum(int N, int M,
                vector<int> Value,
                int Edges[][2])
{
    // Stores the edges of the graph
    vector<int> adj[N];

    // Create Adjacency list
    for (int i = 0; i < M; i++) {
        adj[Edges[i][0]].push_back(
            Edges[i][1]);
    }

    // Initialize result
    int result = Value[0];

    // Stores the nodes of each level
    queue<int> q;

    // Insert root
    q.push(0);

    // Perform level order traversal
    while (!q.empty()) {

        // Count of nodes of the
        // current level
        int count = q.size();

        int sum = 0;

        // Traverse the current level
        while (count--) {

            // Dequeue a node from queue
            int temp = q.front();
            q.pop();

            // Update sum of current level
            sum = sum + Value[temp];

            // Enqueue the children of
            // dequeued node
            for (int i = 0;
                 i < adj[temp].size(); i++) {
                q.push(adj[temp][i]);
            }
        }

        // Update maximum level sum
        result = max(sum, result);
    }

    // Return the result
    return result;
}

// Driver Code
int main()
{
    // Number of nodes
    int N = 10;

    // Edges of the N-ary tree
    int Edges[][2] = { { 0, 1 }, { 0, 2 },
                       { 0, 3 }, { 1, 4 },
                       { 1, 5 }, { 3, 6 },
                       { 6, 7 }, { 6, 8 },
                       { 6, 9 } };
    // Given cost
    vector<int> Value = { 1, 2, -1, 3, 4,
                          5, 8, 6, 12, 7 };

    // Function call
    cout << maxLevelSum(N, N - 1,
                        Value, Edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

class GFG{

// Function to find the maximum sum
// a level in N-ary treeusing BFS
@SuppressWarnings("unchecked")
static int maxLevelSum(int N, int M, int[] Value,
                                     int Edges[][])
{

    // Stores the edges of the graph
    ArrayList<Integer>[] adj = new ArrayList[N];

    for(int i = 0; i < N; i++)
    {
        adj[i] = new ArrayList<>();
    }

    // Create Adjacency list
    for(int i = 0; i < M; i++)
    {
        adj[Edges[i][0]].add(Edges[i][1]);
    }

    // Initialize result
    int result = Value[0];

    // Stores the nodes of each level
    Queue<Integer> q = new LinkedList<>();

    // Insert root
    q.add(0);

    // Perform level order traversal
    while (!q.isEmpty())
    {

        // Count of nodes of the
        // current level
        int count = q.size();

        int sum = 0;

        // Traverse the current level
        while (count-- > 0)
        {

            // Dequeue a node from queue
            int temp = q.poll();

            // Update sum of current level
            sum = sum + Value[temp];

            // Enqueue the children of
            // dequeued node
            for(int i = 0; i < adj[temp].size(); i++)
            {
                q.add(adj[temp].get(i));
            }
        }

        // Update maximum level sum
        result = Math.max(sum, result);
    }

    // Return the result
    return result;
}

// Driver Code
public static void main(String[] args)
{

    // Number of nodes
    int N = 10;

    // Edges of the N-ary tree
    int[][] Edges = { { 0, 1 }, { 0, 2 },
                      { 0, 3 }, { 1, 4 },
                      { 1, 5 }, { 3, 6 },
                      { 6, 7 }, { 6, 8 },
                      { 6, 9 } };
    // Given cost
    int[] Value = { 1, 2, -1, 3, 4,
                    5, 8, 6, 12, 7 };

    // Function call
    System.out.println(maxLevelSum(N, N - 1,
                                   Value, Edges));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to find the maximum sum
# a level in N-ary treeusing BFS
def maxLevelSum(N, M, Value, Edges):

    # Stores the edges of the graph
    adj = [[] for i in range(N)]

    # Create Adjacency list
    for i in range(M):
        adj[Edges[i][0]].append(Edges[i][1])

    # Initialize result
    result = Value[0]

    # Stores the nodes of each level
    q = deque()

    # Insert root
    q.append(0)

    # Perform level order traversal
    while (len(q) > 0):

        # Count of nodes of the
        # current level
        count = len(q)

        sum = 0

        # Traverse the current level
        while (count):

            # Dequeue a node from queue
            temp = q.popleft()

            # Update sum of current level
            sum = sum + Value[temp]

            # Enqueue the children of
            # dequeued node
            for i in range(len(adj[temp])):
                q.append(adj[temp][i])

            count -= 1

        # Update maximum level sum
        result = max(sum, result)

    # Return the result
    return result

# Driver Code
if __name__ == '__main__':

    # Number of nodes
    N = 10

    # Edges of the N-ary tree
    Edges = [ [ 0, 1 ], [ 0, 2 ],
              [ 0, 3 ], [ 1, 4 ],
              [ 1, 5 ], [ 3, 6 ],
              [ 6, 7 ], [ 6, 8 ],
              [ 6, 9 ] ]

    # Given cost
    Value = [ 1, 2, -1, 3, 4,
              5, 8, 6, 12, 7 ]

    # Function call
    print(maxLevelSum(N, N - 1,
                      Value, Edges))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the maximum sum
// a level in N-ary treeusing BFS

static int maxLevelSum(int N, int M,
                       int[] Value,
                       int [,]Edges)
{
  // Stores the edges of the graph
  List<int>[] adj = new List<int>[N];

  for(int i = 0; i < N; i++)
  {
    adj[i] = new List<int>();
  }

  // Create Adjacency list
  for(int i = 0; i < M; i++)
  {
    adj[Edges[i, 0]].Add(Edges[i, 1]);
  }

  // Initialize result
  int result = Value[0];

  // Stores the nodes of each level
  Queue<int> q = new Queue<int>();

  // Insert root
  q.Enqueue(0);

  // Perform level order
  // traversal
  while (q.Count != 0)
  {
    // Count of nodes of the
    // current level
    int count = q.Count;

    int sum = 0;

    // Traverse the current
    // level
    while (count-- > 0)
    {
      // Dequeue a node from
      // queue
      int temp = q.Peek();
      q.Dequeue();

      // Update sum of current
      // level
      sum = sum + Value[temp];

      // Enqueue the children of
      // dequeued node
      for(int i = 0;
              i < adj[temp].Count; i++)
      {
        q.Enqueue(adj[temp][i]);
      }
    }

    // Update maximum level sum
    result = Math.Max(sum, result);
  }

  // Return the result
  return result;
}

// Driver Code
public static void Main(String[] args)
{   
  // Number of nodes
  int N = 10;

  // Edges of the N-ary tree
  int[,] Edges = {{0, 1}, {0, 2},
                  {0, 3}, {1, 4},
                  {1, 5}, {3, 6},
                  {6, 7}, {6, 8},
                  {6, 9}};
  // Given cost
  int[] Value = {1, 2, -1, 3, 4,
                 5, 8, 6, 12, 7};

  // Function call
  Console.WriteLine(maxLevelSum(N, N - 1,
                                Value, Edges));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to find the maximum sum
    // a level in N-ary treeusing BFS

    function maxLevelSum(N, M, Value, Edges)
    {
      // Stores the edges of the graph
      let adj = new Array(N);

      for(let i = 0; i < N; i++)
      {
        adj[i] = [];
      }

      // Create Adjacency list
      for(let i = 0; i < M; i++)
      {
        adj[Edges[i][0]].push(Edges[i][1]);
      }

      // Initialize result
      let result = Value[0];

      // Stores the nodes of each level
      let q = [];

      // Insert root
      q.push(0);

      // Perform level order
      // traversal
      while (q.length != 0)
      {
        // Count of nodes of the
        // current level
        let count = q.length;

        let sum = 0;

        // Traverse the current
        // level
        while (count-- > 0)
        {
          // Dequeue a node from
          // queue
          let temp = q[0];
          q.shift();

          // Update sum of current
          // level
          sum = sum + Value[temp];

          // Enqueue the children of
          // dequeued node
          for(let i = 0; i < adj[temp].length; i++)
          {
            q.push(adj[temp][i]);
          }
        }

        // Update maximum level sum
        result = Math.max(sum, result);
      }

      // Return the result
      return result;
    }

    // Number of nodes
    let N = 10;

    // Edges of the N-ary tree
    let Edges = [[0, 1], [0, 2],
                    [0, 3], [1, 4],
                    [1, 5], [3, 6],
                    [6, 7], [6, 8],
                    [6, 9]];
    // Given cost
    let Value = [1, 2, -1, 3, 4, 5, 8, 6, 12, 7];

    // Function call
    document.write(maxLevelSum(N, N - 1, Value, Edges));

</script>
```

**Output**

```
25
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)