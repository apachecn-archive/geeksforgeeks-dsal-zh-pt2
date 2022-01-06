# 动态连通性|集 1(增量)

> 原文:[https://www . geesforgeks . org/dynamic-connectivity-set-1-incremental/](https://www.geeksforgeeks.org/dynamic-connectivity-set-1-incremental/)

动态连接是一种数据结构，它动态地维护关于图的连接组件的信息。简单地说，假设有一个图 G(V，E)，其中顶点的数量 V 是恒定的，但是边的数量 E 是可变的。有三种方法可以改变边的数量

1.  增量连通性:边只添加到图中。
2.  递减连通性:仅从图中删除边。
3.  完全动态连接:边既可以删除，也可以添加到图中。

本文只讨论**增量连接**。主要有两个操作需要处理。

1.  图中增加了一条边。
2.  关于两个节点 x 和 y 的信息，无论它们是否在相同的连接组件中。

**示例:**

```
Input : V = 7
        Number of operations = 11
        1 0 1
        2 0 1
        2 1 2
        1 0 2
        2 0 2
        2 2 3
        2 3 4
        1 0 5
        2 4 5
        2 5 6
        1 2 6
Note: 7 represents number of nodes, 
      11 represents number of queries. 
      There are two types of queries 
      Type 1: 1 x y in  this if the node 
               x and y are connected print 
               Yes else No
      Type 2: 2 x y in this add an edge 
               between node x and y
Output: No
         Yes
         No
         Yes
Explanation :
Initially there are no edges so node 0 and 1
will be disconnected so answer will be No
Node 0 and 2 will be connected through node 
1 so answer will be Yes similarly for other
queries we can find whether two nodes are 
connected or not

```

为了解决增量连接[的问题，使用了不相交的数据结构](https://www.geeksforgeeks.org/union-find/)。这里，每个连接的组件代表一个集合，如果两个节点属于同一个集合，这意味着它们是连接的。

下面给出了实现，这里我们使用的是等级和路径压缩的联合

## C++

```
// C++ implementation of incremental connectivity
#include<bits/stdc++.h>
using namespace std;

// Finding the root of node i
int root(int arr[], int i)
{
    while (arr[i] != i)
    {
       arr[i] = arr[arr[i]];
       i = arr[i];
    }
    return i;
}

// union of two nodes a and b
void weighted_union(int arr[], int rank[],
                            int a, int b)
{
    int root_a = root (arr, a);
    int root_b = root (arr, b);

    // union based on rank
    if (rank[root_a] < rank[root_b])
    {
       arr[root_a] = arr[root_b];
       rank[root_b] += rank[root_a];
    }
    else
    {
        arr[root_b] = arr[root_a];
        rank[root_a] += rank[root_b];
    }
}

// Returns true if two nodes have same root
bool areSame(int arr[], int a, int b)
{
    return (root(arr, a) == root(arr, b));
}

// Performing an operation according to query type
void query(int type, int x, int y, int arr[], int rank[])
{
    // type 1 query means checking if node x and y
    // are connected or not
    if (type == 1)
    {
        // If roots of x and y is same then yes
        // is the answer
        if (areSame(arr, x, y) == true)
            cout << "Yes" << endl;
        else
           cout << "No" << endl;
    }

    // type 2 query refers union of x and y
    else if (type == 2)
    {
        // If x and y have different roots then
        // union them
        if (areSame(arr, x, y) == false)
            weighted_union(arr, rank, x, y);
    }
}

// Driver function
int main()
{
    // No.of nodes
    int n = 7;

    // The following two arrays are used to
    // implement disjoint set data structure.
    // arr[] holds the parent nodes while rank
    // array holds the rank of subset
    int arr[n], rank[n];

    // initializing both array and rank
    for (int i=0; i<n; i++)
    {
        arr[i] = i;
        rank[i] = 1;
    }

    // number of queries
    int q = 11;
    query(1, 0, 1, arr, rank);
    query(2, 0, 1, arr, rank);
    query(2, 1, 2, arr, rank);
    query(1, 0, 2, arr, rank);
    query(2, 0, 2, arr, rank);
    query(2, 2, 3, arr, rank);
    query(2, 3, 4, arr, rank);
    query(1, 0, 5, arr, rank);
    query(2, 4, 5, arr, rank);
    query(2, 5, 6, arr, rank);
    query(1, 2, 6, arr, rank);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of 
// incremental connectivity
import java.util.*;

class GFG
{

// Finding the root of node i
static int root(int arr[], int i)
{
    while (arr[i] != i)
    {
        arr[i] = arr[arr[i]];
        i = arr[i];
    }
    return i;
}

// union of two nodes a and b
static void weighted_union(int arr[], int rank[],
                           int a, int b)
{
    int root_a = root (arr, a);
    int root_b = root (arr, b);

    // union based on rank
    if (rank[root_a] < rank[root_b])
    {
        arr[root_a] = arr[root_b];
        rank[root_b] += rank[root_a];
    }
    else
    {
        arr[root_b] = arr[root_a];
        rank[root_a] += rank[root_b];
    }
}

// Returns true if two nodes have same root
static boolean areSame(int arr[], 
                       int a, int b)
{
    return (root(arr, a) == root(arr, b));
}

// Performing an operation
// according to query type
static void query(int type, int x, int y, 
                  int arr[], int rank[])
{
    // type 1 query means checking if 
    // node x and y are connected or not
    if (type == 1)
    {
        // If roots of x and y is same then yes
        // is the answer
        if (areSame(arr, x, y) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // type 2 query refers union of x and y
    else if (type == 2)
    {
        // If x and y have different roots then
        // union them
        if (areSame(arr, x, y) == false)
            weighted_union(arr, rank, x, y);
    }
}

// Driver Code
public static void main(String[] args)
{
    // No.of nodes
    int n = 7;

    // The following two arrays are used to
    // implement disjoint set data structure.
    // arr[] holds the parent nodes while rank
    // array holds the rank of subset
    int []arr = new int[n];
    int []rank = new int[n];

    // initializing both array and rank
    for (int i = 0; i < n; i++)
    {
        arr[i] = i;
        rank[i] = 1;
    }

    // number of queries
    int q = 11;
    query(1, 0, 1, arr, rank);
    query(2, 0, 1, arr, rank);
    query(2, 1, 2, arr, rank);
    query(1, 0, 2, arr, rank);
    query(2, 0, 2, arr, rank);
    query(2, 2, 3, arr, rank);
    query(2, 3, 4, arr, rank);
    query(1, 0, 5, arr, rank);
    query(2, 4, 5, arr, rank);
    query(2, 5, 6, arr, rank);
    query(1, 2, 6, arr, rank);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# incremental connectivity 

# Finding the root of node i 
def root(arr, i):
    while (arr[i] != i):
        arr[i] = arr[arr[i]] 
        i = arr[i]
    return i

# union of two nodes a and b 
def weighted_union(arr, rank, a, b):
    root_a = root (arr, a) 
    root_b = root (arr, b) 

    # union based on rank 
    if (rank[root_a] < rank[root_b]):
        arr[root_a] = arr[root_b] 
        rank[root_b] += rank[root_a]
    else:
        arr[root_b] = arr[root_a] 
        rank[root_a] += rank[root_b]

# Returns true if two nodes have
# same root 
def areSame(arr, a, b):
    return (root(arr, a) == root(arr, b))

# Performing an operation according
# to query type 
def query(type, x, y, arr, rank):

    # type 1 query means checking if 
    # node x and y are connected or not 
    if (type == 1):

        # If roots of x and y is same
        # then yes is the answer 
        if (areSame(arr, x, y) == True): 
            print("Yes") 
        else:
            print("No")

    # type 2 query refers union of
    # x and y 
    elif (type == 2):

        # If x and y have different 
        # roots then union them 
        if (areSame(arr, x, y) == False):
            weighted_union(arr, rank, x, y)

# Driver Code
if __name__ == '__main__':

    # No.of nodes 
    n = 7

    # The following two arrays are used to 
    # implement disjoset data structure. 
    # arr[] holds the parent nodes while rank 
    # array holds the rank of subset 
    arr = [None] * n
    rank = [None] * n

    # initializing both array 
    # and rank
    for i in range(n):
        arr[i] = i 
        rank[i] = 1

    # number of queries 
    q = 11
    query(1, 0, 1, arr, rank) 
    query(2, 0, 1, arr, rank) 
    query(2, 1, 2, arr, rank) 
    query(1, 0, 2, arr, rank) 
    query(2, 0, 2, arr, rank) 
    query(2, 2, 3, arr, rank) 
    query(2, 3, 4, arr, rank) 
    query(1, 0, 5, arr, rank) 
    query(2, 4, 5, arr, rank) 
    query(2, 5, 6, arr, rank) 
    query(1, 2, 6, arr, rank)

# This code is contributed by PranchalK
```

## C#

```
// C# implementation of 
// incremental connectivity
using System;

class GFG
{

// Finding the root of node i
static int root(int []arr, int i)
{
    while (arr[i] != i)
    {
        arr[i] = arr[arr[i]];
        i = arr[i];
    }
    return i;
}

// union of two nodes a and b
static void weighted_union(int []arr, int []rank,
                           int a, int b)
{
    int root_a = root (arr, a);
    int root_b = root (arr, b);

    // union based on rank
    if (rank[root_a] < rank[root_b])
    {
        arr[root_a] = arr[root_b];
        rank[root_b] += rank[root_a];
    }
    else
    {
        arr[root_b] = arr[root_a];
        rank[root_a] += rank[root_b];
    }
}

// Returns true if two nodes have same root
static Boolean areSame(int []arr, 
                       int a, int b)
{
    return (root(arr, a) == root(arr, b));
}

// Performing an operation
// according to query type
static void query(int type, int x, int y, 
                  int []arr, int []rank)
{
    // type 1 query means checking if 
    // node x and y are connected or not
    if (type == 1)
    {
        // If roots of x and y is same then yes
        // is the answer
        if (areSame(arr, x, y) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

    // type 2 query refers union of x and y
    else if (type == 2)
    {

        // If x and y have different roots then
        // union them
        if (areSame(arr, x, y) == false)
            weighted_union(arr, rank, x, y);
    }
}

// Driver Code
public static void Main(String[] args)
{
    // No.of nodes
    int n = 7;

    // The following two arrays are used to
    // implement disjoint set data structure.
    // arr[] holds the parent nodes while rank
    // array holds the rank of subset
    int []arr = new int[n];
    int []rank = new int[n];

    // initializing both array and rank
    for (int i = 0; i < n; i++)
    {
        arr[i] = i;
        rank[i] = 1;
    }

    // number of queries
    query(1, 0, 1, arr, rank);
    query(2, 0, 1, arr, rank);
    query(2, 1, 2, arr, rank);
    query(1, 0, 2, arr, rank);
    query(2, 0, 2, arr, rank);
    query(2, 2, 3, arr, rank);
    query(2, 3, 4, arr, rank);
    query(1, 0, 5, arr, rank);
    query(2, 4, 5, arr, rank);
    query(2, 5, 6, arr, rank);
    query(1, 2, 6, arr, rank);
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
No
Yes
No
Yes

```

**时间复杂度:**

每一次运算的摊余时间复杂度为 O(α(n))，其中α为近似恒定的[逆阿克曼函数](https://en.wikipedia.org/wiki/Ackermann_function#Inverse)。

**参考:**T2[https://en.wikipedia.org/wiki/Dynamic_connectivity](https://en.wikipedia.org/wiki/Dynamic_connectivity)

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。