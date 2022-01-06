# 获得相反奇偶性元素的最小跳跃次数

> 原文:[https://www . geeksforgeeks . org/为获得相反奇偶校验元素的最小跳跃次数/](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-obtain-an-element-of-opposite-parity/)

给定两个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和**跳转[]** ，每个数组元素 **arr[i]** 的任务是找到到达相反奇偶校验的元素所需的最小跳转次数。从任何数组元素**arr【I】**唯一可能的跳转是 **(i +跳转[i])** 或**(I–跳转[i])** 。

**示例:**

> **输入:** arr[] = {4，2，5，2，1}，跳转[] = {1，2，3，1，2}
> **输出:** 3 2 -1 1 -1
> **解释:**
> 以下是每个元素所需的最小步骤:
> **arr[4]:** 由于跳转[4] = 2，唯一可能的跳转是(4–跳转[4]) = 2。由于 arr[2]与 arr[4]具有相同的奇偶性，并且不可能在数组指示的范围内进一步跳转，因此打印 **-1** 。
> **arr[3]:** 由于跳转[3] = 1，所以跳转(3 +跳转[3]) = 4 或(3–跳转[3]) = 2 都是可能的。由于元素 arr[2]和 arr[4]与 arr[3]具有相反的奇偶性，因此打印 **1** 。
> **arr[2]:** 打印 **-1** 。
> **arr[1]:** 唯一可能的跳转是(2 +跳转[2])。由于 arr[3]与 arr[2]具有相同的奇偶性，并且从 arr[3]到达相反奇偶性的数组元素所需的最小跳转次数是 1，因此所需的跳转次数是 2。
> **arr[0]:**arr[0]->arr[3]->(arr[4]或 arr[2])。因此，所需的最小跳跃是 3。
> 
> **输入:** arr[] = {4，5，7，6，7，5，4，4，6，4}，跳转[] = {1，2，3，3，5，2，7，2，4，1}
> **输出:**1 1 2 1 1-1 1 1 2

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并对每个数组元素**arr【I】**执行[广度优先遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)，通过反复转换到**arr【I–jumps【I】】**和**arr【I+jumps【I】】**，直到出现任何无效索引，每次转换后，检查数组元素是否与前一个元素奇偶相反。相应地打印每个数组元素所需的最小跳转次数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是将[多源 BFS](https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/) 单独用于偶奇阵元。按照以下步骤解决问题:

1.  初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**ans【】**，来存储每个数组元素到达一个相反奇偶校验的元素所需的最小跳跃。
2.  初始化向量的[数组](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/)、**调整[]** ，以存储生成的图的[邻接表。](https://www.geeksforgeeks.org/graph-and-its-representations/)
3.  对于每个索引的每对有效跳转 **(i，j)** ，数组的 **i** 通过将边初始化为 **(j，i)** 来创建倒排图。
4.  对奇数元素执行**多源 BFS 遍历**。请执行以下步骤:
    *   [将包含奇数数组元素的所有索引推入](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)[队列](https://www.geeksforgeeks.org/queue-data-structure/)，并将所有这些节点标记为同时访问。
    *   迭代直到[队列非空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下操作:
        *   弹出位于队列前面[的节点，检查它现在连接的任何节点是否具有相同的奇偶校验。如果发现为真，将子节点的**距离更新为父节点的 **1 +距离。****](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)
        *   标记已访问的子节点，并将其推入队列。
5.  对偶数元素执行**多源 BFS 遍历**，并将距离存储在**ans【】**中。
6.  完成上述步骤后，打印存储在**和**中的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Bfs for odd numbers are source
void bfs(int n, vector<int>& a,
         vector<int> invGr[],
         vector<int>& ans, int parity)
{
    // Initialize queue
    queue<int> q;

    // Stores for each node, the nodes
    // visited and their distances
    vector<int> vis(n + 1, 0);
    vector<int> dist(n + 1, 0);

    // Push odd and even numbers
    // as sources to the queue

    // If parity is 0 -> odd
    // Otherwise -> even
    for (int i = 1; i <= n; i++) {
        if ((a[i] + parity) & 1) {
            q.push(i);
            vis[i] = 1;
        }
    }

    // Perform multi-source bfs
    while (!q.empty()) {

        // Extract the front element
        // of the queue
        int v = q.front();
        q.pop();

        // Traverse nodes connected
        // to the current node
        for (int u : invGr[v]) {

            // If u is not visited
            if (!vis[u]) {

                dist[u] = dist[v] + 1;
                vis[u] = 1;

                // If element with opposite
                // parity is obtained
                if ((a[u] + parity) % 2 == 0) {
                    if (ans[u] == -1)

                        // Store its distance from
                        // source in ans[]
                        ans[u] = dist[u];
                }

                // Push the current neighbour
                // to the queue
                q.push(u);
            }
        }
    }
}

// Function to find the minimum jumps
// required by each index to reach
// element of opposite parity
void minJumps(vector<int>& a,
              vector<int>& jump, int n)
{
    // Initialise Inverse Graph
    vector<int> invGr[n + 1];

    // Stores the result for each index
    vector<int> ans(n + 1, -1);

    for (int i = 1; i <= n; i++) {

        // For the jumped index
        for (int ind : { i + jump[i],
                         i - jump[i] }) {

            // If the ind is valid then
            // add reverse directed edge
            if (ind >= 1 and ind <= n) {
                invGr[ind].push_back(i);
            }
        }
    }

    // Multi-source bfs with odd
    // numbers as source by passing 0
    bfs(n, a, invGr, ans, 0);

    // Multi-source bfs with even
    // numbers as source by passing 1
    bfs(n, a, invGr, ans, 1);

    // Print the answer
    for (int i = 1; i <= n; i++) {
        cout << ans[i] << ' ';
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 0, 4, 2, 5, 2, 1 };
    vector<int> jump = { 0, 1, 2, 3, 1, 2 };

    int N = arr.size();

    minJumps(arr, jump, N - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;

class Gfg
{

  // Bfs for odd numbers are source
  static void bfs(int n, int[] a,
                  ArrayList<ArrayList<Integer>> invGr,
                  int[] ans, int parity)
  {

    // Initialize queue
    Queue<Integer> q = new LinkedList<>();

    // Stores for each node, the nodes
    // visited and their distances
    int[] vis = new int[n + 1];
    int[] dist = new int[n + 1];

    // Push odd and even numbers
    // as sources to the queue

    // If parity is 0 -> odd
    // Otherwise -> even
    for (int i = 1; i <= n; i++) {
      if (((a[i] + parity) & 1) != 0) {
        q.add(i);
        vis[i] = 1;
      }
    }

    // Perform multi-source bfs
    while (!q.isEmpty()) {

      // Extract the front element
      // of the queue
      int v = q.peek();
      q.poll();

      // Traverse nodes connected
      // to the current node
      for (Integer u : invGr.get(v)) {

        // If u is not visited
        if (vis[u] == 0) {

          dist[u] = dist[v] + 1;
          vis[u] = 1;

          // If element with opposite
          // parity is obtained
          if ((a[u] + parity) % 2 == 0) {
            if (ans[u] == -1)

              // Store its distance from
              // source in ans[]
              ans[u] = dist[u];
          }

          // Push the current neighbour
          // to the queue
          q.add(u);
        }
      }
    }
  }

  // Function to find the minimum jumps
  // required by each index to reach
  // element of opposite parity
  static void minJumps(int[] a,
                       int[] jump, int n)
  {

    // Initialise Inverse Graph
    ArrayList<ArrayList<Integer>> invGr = new ArrayList<>();

    for(int i = 0; i <= n; i++)
      invGr.add(new ArrayList<Integer>());

    // Stores the result for each index
    int[] ans = new int[n + 1];
    Arrays.fill(ans, -1);

    for (int i = 1; i <= n; i++) 
    {

      // For the jumped index
      // If the ind is valid then
      // add reverse directed edge
      if (i+ jump[i] >= 1 && i+jump[i] <= n) {
        invGr.get(i+ jump[i]).add(i);
      }
      if (i-jump[i] >= 1 && i-jump[i] <= n) {
        invGr.get(i- jump[i]).add(i);
      }
    }

    // Multi-source bfs with odd
    // numbers as source by passing 0
    bfs(n, a, invGr, ans, 0);

    // Multi-source bfs with even
    // numbers as source by passing 1
    bfs(n, a, invGr, ans, 1);

    // Print the answer
    for (int i = 1; i <= n; i++) 
    {
      System.out.print(ans[i] + " ");
    }
  }

  // Driver function
  public static void main (String[] args)
  {
    int[] arr = { 0, 4, 2, 5, 2, 1 };
    int[] jump = { 0, 1, 2, 3, 1, 2 };

    int N = arr.length;

    minJumps(arr, jump, N - 1);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Bfs for odd numbers are source
def bfs(n, a, invGr, ans, parity):

    # Initialize queue
    q = []

    # Stores for each node, the nodes
    # visited and their distances
    vis = [0 for i in range(n + 1)]
    dist = [0 for i in range(n + 1)]

    # Push odd and even numbers
    # as sources to the queue

    # If parity is 0 -> odd
    # Otherwise -> even
    for i in range(1, n + 1):
        if ((a[i] + parity) & 1):
            q.append(i)
            vis[i] = 1

    # Perform multi-source bfs
    while (len(q) != 0):

        # Extract the front element
        # of the queue
        v = q[0]
        q.pop(0)

        # Traverse nodes connected
        # to the current node
        for u in invGr[v]:

            # If u is not visited
            if (not vis[u]):
                dist[u] = dist[v] + 1
                vis[u] = 1

                # If element with opposite
                # parity is obtained
                if ((a[u] + parity) % 2 == 0):
                    if (ans[u] == -1):

                        # Store its distance from
                        # source in ans[]
                        ans[u] = dist[u]

                # Push the current neighbour
                # to the queue
                q.append(u)

# Function to find the minimum jumps
# required by each index to reach
# element of opposite parity
def minJumps(a, jump, n):

    # Initialise Inverse Graph
    invGr = [[] for i in range(n + 1)]

    # Stores the result for each index
    ans = [-1 for i in range(n + 1)]

    for i in range(1, n + 1):

        # For the jumped index
        for ind in [i + jump[i], i - jump[i]]:

            # If the ind is valid then
            # add reverse directed edge
            if (ind >= 1 and ind <= n):
                invGr[ind].append(i)

    # Multi-source bfs with odd
    # numbers as source by passing 0
    bfs(n, a, invGr, ans, 0)

    # Multi-source bfs with even
    # numbers as source by passing 1
    bfs(n, a, invGr, ans, 1)

    # Print the answer
    for i in range(1, n + 1):
        print(str(ans[i]), end = ' ')

# Driver Code
if __name__=='__main__':

    arr = [ 0, 4, 2, 5, 2, 1 ]
    jump = [ 0, 1, 2, 3, 1, 2 ]

    N = len(arr)

    minJumps(arr, jump, N - 1)

# This code is contributed by pratham76
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Bfs for odd numbers are source
function bfs(n, a, invGr, ans, parity)
{
    // Initialize queue
    var q = [];

    // Stores for each node, the nodes
    // visited and their distances
    var vis = Array(n+1).fill(0);
    var dist = Array(n+1).fill(0);

    // Push odd and even numbers
    // as sources to the queue

    // If parity is 0 -> odd
    // Otherwise -> even
    for (var i = 1; i <= n; i++) {
        if ((a[i] + parity) & 1) {
            q.push(i);
            vis[i] = 1;
        }
    }

    // Perform multi-source bfs
    while (q.length!=0) {

        // Extract the front element
        // of the queue
        var v = q[0];
        q.shift();

        // Traverse nodes connected
        // to the current node
        invGr[v].forEach(u => {

            // If u is not visited
            if (!vis[u]) {

                dist[u] = dist[v] + 1;
                vis[u] = 1;

                // If element with opposite
                // parity is obtained
                if ((a[u] + parity) % 2 == 0) {
                    if (ans[u] == -1)

                        // Store its distance from
                        // source in ans[]
                        ans[u] = dist[u];
                }

                // Push the current neighbour
                // to the queue
                q.push(u);
            }
        });
    }
    return ans;
}

// Function to find the minimum jumps
// required by each index to reach
// element of opposite parity
function minJumps(a, jump, n)
{
    // Initialise Inverse Graph
    var invGr = Array.from(Array(n+1), ()=>Array())

    // Stores the result for each index
    var ans = Array(n + 1).fill(-1);

    for (var i = 1; i <= n; i++) {

        // For the jumped index
        [i + jump[i], i - jump[i]].forEach(ind => {

            // If the ind is valid then
            // add reverse directed edge
            if (ind >= 1 && ind <= n) {
                invGr[ind].push(i);
            }
        });
    }

    // Multi-source bfs with odd
    // numbers as source by passing 0
    ans = bfs(n, a, invGr, ans, 0);

    // Multi-source bfs with even
    // numbers as source by passing 1
    ans = bfs(n, a, invGr, ans, 1);

    // Print the answer
    for (var i = 1; i <= n; i++) {
        document.write( ans[i] + ' ');
    }
}

// Driver Code
var arr = [0, 4, 2, 5, 2, 1];
var jump = [0, 1, 2, 3, 1, 2];
var N = arr.length;
minJumps(arr, jump, N - 1);

</script>
```

**Output:** 

```
3 2 -1 1 -1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)