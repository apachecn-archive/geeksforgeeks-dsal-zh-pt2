# 通过连接任何一对成本至少为 0 的顶点来最小化连接图的成本

> 原文:[https://www . geeksforgeeks . org/通过连接任何一对成本至少为 0 的顶点来最小化连接图形的成本/](https://www.geeksforgeeks.org/minimize-cost-to-connect-the-graph-by-connecting-any-pairs-of-vertices-having-cost-at-least-0/)

给定一个具有 **N 个**顶点和 **M 个**边的[不连续图](https://www.geeksforgeeks.org/bfs-disconnected-graph/) **G** 和一个对应于每个顶点的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **成本【】**，任务是通过连接任意对顶点成本**至少为 0** 的顶点找到制作该图的最小成本，并且连接那对顶点的成本是各个顶点的成本之和。如果不可能，则打印**-1”**。

**示例:**

> **输入:** N = 6，G[] = {{3，1}，{2，3}，{2，1}，{4，5}，{5，6}，{6，4}}，成本[] = {2，1，5，3，2，9}
> **输出:** 3
> **解释:**初始图形有两个相连的组件–{ 1，2，3}和{4，5，6}。我们可以以成本[2] +成本[5] = 1 + 2 = 3 为代价，在 2 到 5 之间增加一条边。添加这条边后，整个图是连通的。
> 
> **输入:** N = 6，G[] = {{3，1}，{2，3}，{2，1}，{4，5}，{5，6}，{6，4}}，成本[] = {2，1，5，-3，-2，-9}
> **输出:** -1
> **解释:**无法使图形连通

**方法:**给定的问题可以使用[不相交集并集](https://www.geeksforgeeks.org/union-find/)数据结构来解决。想法是存储所有**最小值**大于或等于 **0** 的所有值，对于所有不同的连接部件说 **minVal[]** ，如果是 **true** 则检查 **minVal[]** 中是否有小于零的值，然后打印 **-1** ，否则在 **minVal[]** 中找到最小值，说【T20

按照以下步骤解决问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **minVal[]** 来寻找每个集合的最小元素。
*   初始化向量**父(N+1)，秩(N+1，0)，minVal(N+1)** 。
*   初始化一个集合，比如说 **s** ，来存储每个集合的父集合。
*   初始化一个变量，比如**最小成本**，它存储最小成本。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N+1】**，并将**父项【I】**的值设置为 **I** ，将**minVal【I】**设置为**成本【I–1】**。
*   [使用变量 **i** 迭代向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **G** ，并调用函数操作 **Union(父，rank，minVal，i.first，i.second)** 。
*   使用变量 **i** 迭代范围**【1，N+1】**，并将 **I** 的父元素插入到 **s** 中。
*   迭代设置 **s** 并找到 **s** 的最小值，并将其存储在 **min** 中，如果任何值为负，则将**标志**标记为真。
*   [如果给定图形已经连接](https://www.geeksforgeeks.org/check-if-a-given-graph-is-2-edge-connected-or-not/)或者**标志**值为**假**，则:
    *   使用变量 **I** 迭代 **s** ，如果 **min** 值不等于 **I** ，则将 **minCost** 的值更新为**min cost+=(min val[I]+min . second)**。
    *   完成上述步骤后，打印**最小成本**的值作为最终最小成本。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the find operation
// to find the parent of a disjoint set
int Find(vector<int>& parent, int a)
{

    return parent[a]
           = (parent[a] == a ? a : Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
void Union(vector<int>& parent,
           vector<int>& rank,
           vector<int>& minVal,
           int a, int b)
{

    a = Find(parent, a);
    b = Find(parent, b);

    if (rank[a] == rank[b])
        rank[a]++;

    if (rank[a] > rank[b]) {
        parent[b] = a;

        // Update the minimum value
        // such than it should be
        // greater than 0
        if (minVal[a] >= 0
            && minVal[b] >= 0) {
            minVal[a] = min(minVal[a],
                            minVal[b]);
        }
        else if (minVal[a] >= 0
                 && minVal[b] < 0) {
            minVal[a] = minVal[a];
        }
        else if (minVal[a] < 0
                 && minVal[b] >= 0) {
            minVal[a] = minVal[b];
        }
        else {
            minVal[a] = max(minVal[a],
                            minVal[b]);
        }
    }
    else {
        parent[a] = b;

        // Update the minimum value
        // such than it should be
        // greater than 0
        if (minVal[a] >= 0
            && minVal[b] >= 0) {
            minVal[b] = min(minVal[a],
                            minVal[b]);
        }
        else if (minVal[a] >= 0
                 && minVal[b] < 0) {
            minVal[b] = minVal[a];
        }
        else if (minVal[a] < 0
                 && minVal[b] >= 0) {
            minVal[b] = minVal[b];
        }
        else {
            minVal[b] = max(minVal[a],
                            minVal[b]);
        }
    }
}

// Function to minimize the cost to
// make the graph connected as per
// the given condition
void findMinCost(vector<pair<int, int> >& G,
                 vector<int>& cost,
                 int N, int M)
{

    // Stores the parent elements of sets
    vector<int> parent(N + 1);

    // Stores the rank of the sets
    vector<int> rank(N + 1, 0);

    // Stores the minValue of the sets
    vector<int> minVal(N + 1);

    for (int i = 1; i < N + 1; i++) {

        // Update parent[i] to i
        parent[i] = i;

        // Update minValue[i] to cost[i-1]
        minVal[i] = cost[i - 1];
    }

    for (auto i : G) {

        // Add i.first and i.second
        // elements to the same set
        Union(parent, rank, minVal,
              i.first, i.second);
    }

    // Stores the parent elements of
    // the different components
    set<int> s;

    for (int i = 1; i < N + 1; i++) {

        // Insert parent of i to s
        s.insert(Find(parent, i));
    }

    // Stores the minimum value from s
    pair<int, int> min = { 0, INT_MAX };

    // Flag to mark if any minimum
    // value is negative
    bool flag = false;

    for (auto i : s) {

        // If minVal[i] is negative
        if (minVal[i] < 0) {

            // Mark flag as true
            flag = true;
        }

        if (min.second > minVal[i]) {

            // Update the minimum value
            min = { i, minVal[i] };
        }
    }

    // Stores minimum cost to add the edges
    int minCost = 0;

    // If the given graph is connected
    // or components minimum values not
    // having any negative edge
    if (!flag || (flag && s.size() == 1)) {

        for (auto i : s) {

            if (i != min.first) {

                // Update the minCost
                minCost += (minVal[i] + min.second);
            }
        }

        // Print the value of minCost
        cout << minCost << endl;
    }
    else {

        // Print -1
        cout << -1 << endl;
    }
}

// Driver Code
int main()
{
    int N = 6;
    vector<pair<int,int>> G = {
        { 3, 1 }, { 2, 3 }, { 2, 1 },
        { 4, 5 }, { 5, 6 }, { 6, 4 }
    };
    vector<int> cost{ 2, 1, 5, 3, 2, 9 };
    int M = G.size();

    findMinCost(G, cost, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Function to perform the find operation
// to find the parent of a disjoint set
static int Find(int[] parent, int a)
{

    return parent[a]
           = (parent[a] == a ? a : Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
static void Union(int [] parent,
           int [] rank,
           int [] minVal,
           int a, int b)
{

    a = Find(parent, a);
    b = Find(parent, b);

    if (rank[a] == rank[b])
        rank[a]++;

    if (rank[a] > rank[b]) {
        parent[b] = a;

        // Update the minimum value
        // such than it should be
        // greater than 0
        if (minVal[a] >= 0
            && minVal[b] >= 0) {
            minVal[a] = Math.min(minVal[a],
                            minVal[b]);
        }
        else if (minVal[a] >= 0
                 && minVal[b] < 0) {
            minVal[a] = minVal[a];
        }
        else if (minVal[a] < 0
                 && minVal[b] >= 0) {
            minVal[a] = minVal[b];
        }
        else {
            minVal[a] = Math.max(minVal[a],
                            minVal[b]);
        }
    }
    else {
        parent[a] = b;

        // Update the minimum value
        // such than it should be
        // greater than 0
        if (minVal[a] >= 0
            && minVal[b] >= 0) {
            minVal[b] = Math.min(minVal[a],
                            minVal[b]);
        }
        else if (minVal[a] >= 0
                 && minVal[b] < 0) {
            minVal[b] = minVal[a];
        }
        else if (minVal[a] < 0
                 && minVal[b] >= 0) {
            minVal[b] = minVal[b];
        }
        else {
            minVal[b] = Math.max(minVal[a],
                            minVal[b]);
        }
    }
}

// Function to minimize the cost to
// make the graph connected as per
// the given condition
static void findMinCost(pair[] G,
                 int [] cost,
                 int N, int M)
{

    // Stores the parent elements of sets
    int [] parent = new int[N + 1];

    // Stores the rank of the sets
    int [] rank = new int[N + 1];

    // Stores the minValue of the sets
    int [] minVal = new int[N + 1];

    for (int i = 1; i < N + 1; i++) {

        // Update parent[i] to i
        parent[i] = i;

        // Update minValue[i] to cost[i-1]
        minVal[i] = cost[i - 1];
    }

    for (pair i : G) {

        // Add i.first and i.second
        // elements to the same set
        Union(parent, rank, minVal,
              i.first, i.second);
    }

    // Stores the parent elements of
    // the different components
    HashSet<Integer> s = new HashSet<Integer>();

    for (int i = 1; i < N + 1; i++) {

        // Insert parent of i to s
        s.add(Find(parent, i));
    }

    // Stores the minimum value from s
    pair min = new pair( 0, Integer.MAX_VALUE );

    // Flag to mark if any minimum
    // value is negative
    boolean flag = false;

    for (int i : s) {

        // If minVal[i] is negative
        if (minVal[i] < 0) {

            // Mark flag as true
            flag = true;
        }

        if (min.second > minVal[i]) {

            // Update the minimum value
            min = new pair( i, minVal[i] );
        }
    }

    // Stores minimum cost to add the edges
    int minCost = 0;

    // If the given graph is connected
    // or components minimum values not
    // having any negative edge
    if (!flag || (flag && s.size() == 1)) {

        for (int i : s) {

            if (i != min.first) {

                // Update the minCost
                minCost += (minVal[i] + min.second);
            }
        }

        // Print the value of minCost
        System.out.print(minCost +"\n");
    }
    else {

        // Print -1
        System.out.print(-1 +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;
    pair []G = {
            new pair( 3, 1 ), new pair( 2, 3 ), new pair( 2, 1 ),
            new pair( 4, 5 ), new pair( 5, 6 ), new pair( 6, 4 )
    };
    int[] cost = { 2, 1, 5, 3, 2, 9 };
    int M = G.length;

    findMinCost(G, cost, N, M);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

import sys
# Function to perform the find operation
# to find the parent of a disjoint set
def Find(parent, a):
    if parent[parent[a]] != parent[a]:
        parent[a]  = Find(parent, parent[a])
    return parent[a]

# FUnction to perform union operation
# of disjoint set union
def Union(parent, rank, minVal, a, b):
    a = Find(parent, a)
    b = Find(parent, b)

    if (rank[a] == rank[b]):
        rank[a] += 1

    if (rank[a] > rank[b]):
        parent[b] = a

        # Update the minimum value
        # such than it should be
        # greater than 0
        if (minVal[a] >= 0 and minVal[b] >= 0):
            minVal[a] = min(minVal[a],minVal[b])
        elif(minVal[a] >= 0 and minVal[b] < 0):
            minVal[a] = minVal[a]
        elif(minVal[a] < 0 and minVal[b] >= 0):
            minVal[a] = minVal[b]
        else:
            minVal[a] = max(minVal[a],minVal[b])
    else:
        parent[a] = b

        # Update the minimum value
        # such than it should be
        # greater than 0
        if (minVal[a] >= 0 and minVal[b] >= 0):
            minVal[b] = min(minVal[a],minVal[b])
        elif(minVal[a] >= 0 and minVal[b] < 0):
            minVal[b] = minVal[a]
        elif(minVal[a] < 0 and minVal[b] >= 0):
            minVal[b] = minVal[b]
        else:
            minVal[b] = max(minVal[a],minVal[b])

# Function to minimize the cost to
# make the graph connected as per
# the given condition
def findMinCost(G,cost,N, M):
    # Stores the parent elements of sets
    parent = [0 for i in range(N + 1)]

    # Stores the rank of the sets
    rank = [0 for i in range(N + 1)]

    # Stores the minValue of the sets
    minVal = [0 for i in range(N + 1)]

    for i in range(1,N + 1,1):
        # Update parent[i] to i
        parent[i] = i

        # Update minValue[i] to cost[i-1]
        minVal[i] = cost[i - 1]

    for i in G:
        # Add i.first and i.second
        # elements to the same set
        Union(parent, rank, minVal, i[0], i[1])

    # Stores the parent elements of
    # the different components
    s = set()

    for i in range(1,N + 1,1):
        # Insert parent of i to s
        s.add(Find(parent, i))

    # Stores the minimum value from s
    min1  = [0, sys.maxsize]

    # Flag to mark if any minimum
    # value is negative
    flag = False

    for i in s:
        # If minVal[i] is negative
        if (minVal[i] < 0):

            # Mark flag as true
            flag = True

        if (min1[1] > minVal[i]):
            # Update the minimum value
            min1 = [i, minVal[i]]

    # Stores minimum cost to add the edges
    minCost = 0

    # If the given graph is connected
    # or components minimum values not
    # having any negative edge
    if (flag == False or (flag and len(s) == 1)):

        for i in s:
            if (i != min1[0]):

                # Update the minCost
                minCost += (minVal[i] + min1[1])

        # Print the value of minCost
        print(minCost)
    else:
        # Print -1
        print(-1)

# Driver Code
if __name__ == '__main__':
    N = 6
    G = [[3, 1],[2, 3],[2, 1],[4, 5],[5, 6],[6, 4]]
    cost = [2, 1, 5, 3, 2, 9]
    M = len(G)

    findMinCost(G, cost, N, M)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG{
    class pair
    {
        public int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Function to perform the find operation
// to find the parent of a disjoint set
static int Find(int[] parent, int a)
{

    return parent[a]
           = (parent[a] == a ? a : Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
static void Union(int [] parent,
           int [] rank,
           int [] minVal,
           int a, int b)
{

    a = Find(parent, a);
    b = Find(parent, b);

    if (rank[a] == rank[b])
        rank[a]++;

    if (rank[a] > rank[b]) {
        parent[b] = a;

        // Update the minimum value
        // such than it should be
        // greater than 0
        if (minVal[a] >= 0
            && minVal[b] >= 0) {
            minVal[a] = Math.Min(minVal[a],
                            minVal[b]);
        }
        else if (minVal[a] >= 0
                 && minVal[b] < 0) {
            minVal[a] = minVal[a];
        }
        else if (minVal[a] < 0
                 && minVal[b] >= 0) {
            minVal[a] = minVal[b];
        }
        else {
            minVal[a] = Math.Max(minVal[a],
                            minVal[b]);
        }
    }
    else {
        parent[a] = b;

        // Update the minimum value
        // such than it should be
        // greater than 0
        if (minVal[a] >= 0
            && minVal[b] >= 0) {
            minVal[b] = Math.Min(minVal[a],
                            minVal[b]);
        }
        else if (minVal[a] >= 0
                 && minVal[b] < 0) {
            minVal[b] = minVal[a];
        }
        else if (minVal[a] < 0
                 && minVal[b] >= 0) {
            minVal[b] = minVal[b];
        }
        else {
            minVal[b] = Math.Max(minVal[a],
                            minVal[b]);
        }
    }
}

// Function to minimize the cost to
// make the graph connected as per
// the given condition
static void findMinCost(pair[] G,
                 int [] cost,
                 int N, int M)
{

    // Stores the parent elements of sets
    int [] parent = new int[N + 1];

    // Stores the rank of the sets
    int [] rank = new int[N + 1];

    // Stores the minValue of the sets
    int [] minVal = new int[N + 1];

    for (int i = 1; i < N + 1; i++) {

        // Update parent[i] to i
        parent[i] = i;

        // Update minValue[i] to cost[i-1]
        minVal[i] = cost[i - 1];
    }

    foreach (pair i in G) {

        // Add i.first and i.second
        // elements to the same set
        Union(parent, rank, minVal,
              i.first, i.second);
    }

    // Stores the parent elements of
    // the different components
    HashSet<int> s = new HashSet<int>();

    for (int i = 1; i < N + 1; i++) {

        // Insert parent of i to s
        s.Add(Find(parent, i));
    }

    // Stores the minimum value from s
    pair min = new pair( 0, int.MaxValue );

    // Flag to mark if any minimum
    // value is negative
    bool flag = false;

    foreach (int i in s) {

        // If minVal[i] is negative
        if (minVal[i] < 0) {

            // Mark flag as true
            flag = true;
        }

        if (min.second > minVal[i]) {

            // Update the minimum value
            min = new pair( i, minVal[i] );
        }
    }

    // Stores minimum cost to add the edges
    int minCost = 0;

    // If the given graph is connected
    // or components minimum values not
    // having any negative edge
    if (!flag || (flag && s.Count == 1)) {

        foreach (int i in s) {

            if (i != min.first) {

                // Update the minCost
                minCost += (minVal[i] + min.second);
            }
        }

        // Print the value of minCost
        Console.Write(minCost +"\n");
    }
    else {

        // Print -1
        Console.Write(-1 +"\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 6;
    pair []G = {
            new pair( 3, 1 ), new pair( 2, 3 ), new pair( 2, 1 ),
            new pair( 4, 5 ), new pair( 5, 6 ), new pair( 6, 4 )
    };
    int[] cost = { 2, 1, 5, 3, 2, 9 };
    int M = G.Length;

    findMinCost(G, cost, N, M);

}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log M)*
***辅助空间:** O(N)*