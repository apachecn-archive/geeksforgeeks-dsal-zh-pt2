# 执行 Q 查询后，在给定的未连接图中找到第一个未删除的从 K 到 N 的整数

> 原文:[https://www . geeksforgeeks . org/find-first-undeleted-整数-从-k-到-n-in-给定-未连接-执行-q-查询后的图形/](https://www.geeksforgeeks.org/find-first-undeleted-integer-from-k-to-n-in-given-unconnected-graph-after-performing-q-queries/)

给定代表整数集**【1，N】**的正整数 **N** 和长度为 **{L，K}** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **查询[]** ，任务是根据以下规则执行给定的查询并打印结果:

*   **如果 L 的值为 1** ，则删除给定的整数 **K** 。
*   **如果 L 的值为 2** ，则打印第一个从 **K** 到 **N** 的整数，不删除。

**注:**当右侧元素全部删除后，答案为 **-1** 。

**示例:**

> **输入:** N = 3，查询[] = {{2，1}，{1，1}，{2，1}，{2，3}}
> **输出:** 1 2 3
> **解释:**
> 对于第一个查询:1 最右边的元素只有 1。
> 第二次查询后:删除 1。
> 对于第三个查询:1 最右边的元素是 2。
> 对于第四个查询:3 最右边的元素是 3。
> 
> **输入:** N = 5，查询= {{2，1}、{1，3}、{2，3}、{1，2}、{2，2}、{1，5}、{2，5}}
> **输出:** 1 4 4 -1

**方法:**给定的问题可以通过使用[不相交集合并数据结构](https://www.geeksforgeeks.org/disjoint-set-data-structures/)来解决。最初，所有元素都在不同的集合中，对于第一种类型的查询，对给定的整数执行[联合操作](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)。对于第二种类型的查询，获取给定顶点的父顶点，并打印存储在数组**graph【】**中的值。按照以下步骤解决问题:

*   [初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **图(N + 2)** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N+1】**，并将**图形【I】**的值设置为 **i** 。
*   [使用变量**查询**](https://www.geeksforgeeks.org/range-based-loop-c/) 迭代**查询[]** ，并执行以下步骤:
    *   如果 **query.first** 是 **1** ，那么调用[功能](https://www.geeksforgeeks.org/functions-in-c/)操作 **Union(图形，query.second，query.second + 1)** 。
    *   否则，调用函数操作**获取(图形，查询.秒)**，并将其分配给变量 **a** 。现在如果 **a** 的值是 **(N + 1)** ，那么打印 **-1** 。否则，打印**图形【a】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform th Get operation
// of disjoint set union
int Get(vector<int>& graph, int a)
{
    return graph[a]
           = (graph[a] == a ? a
                            : Get(graph, graph[a]));
}

// Function to perform the union
// operation of disjoint set union
void Union(vector<int>& graph,
           int a, int b)
{

    a = Get(graph, a);
    b = Get(graph, b);

    // Update the graph[a] as b
    graph[a] = b;
}

// Function to perform given queries on
// set of vertices initially not connected
void Queries(vector<pair<int, int> >& queries,
             int N, int M)
{

    // Stores the vertices
    vector<int> graph(N + 2);

    // Mark every vertices rightmost
    // vertex as i
    for (int i = 1; i <= N + 1; i++) {

        graph[i] = i;
    }

    // Traverse the queries array
    for (auto query : queries) {

        // Check if it is first type
        // of the givan query
        if (query.first == 1) {

            Union(graph, query.second,
                  query.second + 1);
        }
        else {

            // Get the parent of a
            int a = Get(graph, query.second);

            // Print the answer for
            // the second query
            if (a == N + 1)
                cout << -1 << " ";
            else
                cout << graph[a] << " ";
        }
    }
}

// Driver Code
int main()
{
    int N = 5;
    vector<pair<int, int> > queries{
        { 2, 1 }, { 1, 1 }, { 2, 1 }, { 2, 3 }
    };
    int Q = queries.size();

    Queries(queries, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to perform th Get operation
// of disjoint set union
public static int Get(int[] graph, int a)
{
    return graph[a]
           = (graph[a] == a ? a
                            : Get(graph, graph[a]));
}

// Function to perform the union
// operation of disjoint set union
public static void Union(int[] graph,
           int a, int b)
{

    a = Get(graph, a);
    b = Get(graph, b);

    // Update the graph[a] as b
    graph[a] = b;
}

// Function to perform given queries on
// set of vertices initially not connected
public static void Queries(int[][] queries,
             int N, int M)
{

    // Stores the vertices
    int[] graph = new int[N + 2];

    // Mark every vertices rightmost
    // vertex as i
    for (int i = 1; i <= N + 1; i++) {

        graph[i] = i;
    }

    // Traverse the queries array
    for (int[] query : queries) {

        // Check if it is first type
        // of the givan query
        if (query[0] == 1) {

            Union(graph, query[1],
                  query[1] + 1);
        }
        else {

            // Get the parent of a
            int a = Get(graph, query[1]);

            // Print the answer for
            // the second query
            if (a == N + 1)
                System.out.print(-1);
            else
                System.out.print(graph[a] + " ");
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 5;
    int[][] queries  = { { 2, 1 }, { 1, 1 }, { 2, 1 }, { 2, 3 }};
    int Q = queries.length;

    Queries(queries, N, Q);

}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to perform th Get operation
# of disjoint set union
def Get(graph, a):
    if graph[graph[a]]!= graph[a]:
        graph[a] = Get(graph, graph[a])
    else:
        return graph[a]

# Function to perform the union
# operation of disjoint set union
def Union(graph, a, b):
    a = Get(graph, a)
    b = Get(graph, b)

    # Update the graph[a] as b
    graph[a] = b

# Function to perform given queries on
# set of vertices initially not connected
def Queries(queries, N, M):

    # Stores the vertices
    graph = [0 for i in range(N + 2)]

    # Mark every vertices rightmost
    # vertex as i
    for i in range(1,N + 2,1):
        graph[i] = i

    # Traverse the queries array
    for query in queries:

        # Check if it is first type
        # of the givan query
        if (query[0] == 1):
            Union(graph, query[1], query[1] + 1)

        else:

            # Get the parent of a
            a = Get(graph, query[1])

            # Print the answer for
            # the second query
            if (a == N + 1):
                print(-1)
            else:
                print(graph[a],end = " ")

# Driver Code
if __name__ == '__main__':
    N = 5
    queries = [[2, 1],[1, 1],[2, 1],[2, 3]]
    Q = len(queries)

    Queries(queries, N, Q)

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to perform th Get operation
// of disjoint set union
function Get(graph, a) {
  return (graph[a] = graph[a] == a ? a : Get(graph, graph[a]));
}

// Function to perform the union
// operation of disjoint set union
function Union(graph, a, b) {
  a = Get(graph, a);
  b = Get(graph, b);

  // Update the graph[a] as b
  graph[a] = b;
}

// Function to perform given queries on
// set of vertices initially not connected
function Queries(queries, N, M) {
  // Stores the vertices
  let graph = new Array(N).fill(2);

  // Mark every vertices rightmost
  // vertex as i
  for (let i = 1; i <= N + 1; i++) {
    graph[i] = i;
  }

  // Traverse the queries array
  for (let query of queries) {
    // Check if it is first type
    // of the givan query
    if (query[0] == 1) {
      Union(graph, query[1], query[1] + 1);
    } else {
      // Get the parent of a
      let a = Get(graph, query[1]);

      // Print the answer for
      // the second query
      if (a == N + 1) document.write(-1 + " ");
      else document.write(graph[a] + " ");
    }
  }
}

// Driver Code
let N = 5;
let queries = [
  [2, 1],
  [1, 1],
  [2, 1],
  [2, 3],
];
let Q = queries.length;

Queries(queries, N, Q);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
1 2 3
```

***时间复杂度:** O(M*log N)*
***辅助空间:** O(N)*