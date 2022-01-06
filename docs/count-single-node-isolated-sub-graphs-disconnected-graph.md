# 计算断开图中的单节点孤立子图

> 原文:[https://www . geesforgeks . org/count-单节点-隔离-子图-断开-图/](https://www.geeksforgeeks.org/count-single-node-isolated-sub-graphs-disconnected-graph/)

给出了一个有 N 个顶点和 K 条边的不连通图。任务是找出单例子图的数量。单例图是只有一个顶点的图。
**例:**

```
Input : 
Vertices : 6
Edges :    1 2
           1 3
           5 6
Output : 1
Explanation :  The Graph has 3 components : {1-2-3}, {5-6}, {4}
Out of these, the only component forming singleton graph is {4}.
```

这种思想对于作为邻接表表示的图来说很简单。我们遍历列表，找到列表中没有元素的索引(代表一个节点)，即没有连接的组件。
以下是表示:

## C++

```
// CPP code to count the singleton sub-graphs
// in a disconnected graph
#include <bits/stdc++.h>
using namespace std;

// Function to compute the count
int compute(vector<int> graph[], int N)
{
    // Storing intermediate result
    int count = 0;

    // Traversing the Nodes
    for (int i = 1; i <= N; i++)

        // Singleton component
        if (graph[i].size() == 0)
            count++;   

    // Returning the result
    return count;
}

// Driver
int main()
{
    // Number of nodes
    int N = 6;

    // Adjacency list for edges 1..6
    vector<int> graph[7];

    // Representing edges
    graph[1].push_back(2);
    graph[2].push_back(1);

    graph[2].push_back(3);
    graph[3].push_back(2);

    graph[5].push_back(6);
    graph[6].push_back(5);

    cout << compute(graph, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count the singleton sub-graphs
// in a disconnected graph
import java.util.*;

class GFG
{

// Function to compute the count
static int compute(int []graph, int N)
{
    // Storing intermediate result
    int count = 0;

    // Traversing the Nodes
    for (int i = 1; i < 7; i++)
    {
        // Singleton component
        if (graph[i] == 0)
            count++;    
    }

    // Returning the result
    return count;
}

// Driver Code
public static void main(String[] args)
{
    // Number of nodes
    int N = 6;

    // Adjacency list for edges 1..6
    int []graph = new int[7];
    // Representing edges
    graph[1] = 2;
    graph[2] = 1;
    graph[2] = 3;
    graph[3] = 2;
    graph[5] = 6;
    graph[6] = 5;

    System.out.println(compute(graph, N));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python code to count the singleton sub-graphs
# in a disconnected graph

# Function to compute the count
def compute(graph, N):
    # Storing intermediate result
    count = 0

    # Traversing the Nodes
    for i in range(1, N+1):

        # Singleton component
        if (len(graph[i]) == 0):
            count += 1   

    # Returning the result
    return count

# Driver
if __name__ == '__main__':

    # Number of nodes
    N = 6

    # Adjacency list for edges 1..6
    graph = [[] for i in range(7)]

    # Representing edges
    graph[1].append(2)
    graph[2].append(1)

    graph[2].append(3)
    graph[3].append(2)

    graph[5].append(6)
    graph[6].append(5)

    print(compute(graph, N))
```

## C#

```
// C# code to count the singleton sub-graphs
// in a disconnected graph
using System;

class GFG
{

// Function to compute the count
static int compute(int []graph, int N)
{
    // Storing intermediate result
    int count = 0;

    // Traversing the Nodes
    for (int i = 1; i < 7; i++)
    {
        // Singleton component
        if (graph[i] == 0)
            count++;    
    }

    // Returning the result
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    // Number of nodes
    int N = 6;

    // Adjacency list for edges 1..6
    int []graph = new int[7];

    // Representing edges
    graph[1] = 2;
    graph[2] = 1;
    graph[2] = 3;
    graph[3] = 2;
    graph[5] = 6;
    graph[6] = 5;

    Console.WriteLine(compute(graph, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript code to count the singleton sub-graphs
// in a disconnected graph

// Function to compute the count
function compute(graph,N)
{
    // Storing intermediate result
    let count = 0;

    // Traversing the Nodes
    for (let i = 1; i < 7; i++)
    {
        // Singleton component
        if (graph[i].length == 0)
            count++;    
    }

    // Returning the result
    return count;
}

// Driver Code
// Number of nodes
let N = 6;

// Adjacency list for edges 1..6
let graph = new Array(7);
for(let i=0;i<7;i++)
{
    graph[i]=[];
}
// Representing edges
graph[1].push(2)
graph[2].push(1)

graph[2].push(3)
graph[3].push(2)

graph[5].push(6)
graph[6].push(5)
document.write(compute(graph, N));

// This code is contributed by rag2127

</script>
```

**输出:**

```
1
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。