# Q 查询给定节点的连通分量中的最大元素

> 原文:[https://www . geeksforgeeks . org/q 查询给定节点的最大连接元素组件/](https://www.geeksforgeeks.org/maximum-element-in-connected-component-of-given-node-for-q-queries/)

给定长度为 **N** 的成对**arr【】【】**的[数组](https://www.geeksforgeeks.org/array-data-structure/)，长度为 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)查询【】，以及整数 **R** ，其中**查询【I】**包含从 **1** 到 **R** 的整数，每个**查询【I】**的任务为

> **注:**最初从 **1** 到 **R** 的每个整数都属于不同的集合。

**示例:**

> **输入:** R = 5，arr = {{1，2}，{2，3}，{4，5}}，查询[] = {2，4，1，3}
> **输出:**3 5 3
> T6】解释:从 arr[]对生成集合后，{1，2，3}，{4，5}
> 对于第一个查询:2 属于集合{1，2，3}，最大元素为 3
> 对于 5}且最大元素为 5
> 对于第三个查询:1 属于集合{1，2，3}，最大元素为 3
> 对于第四个查询:3 属于集合{1，2，3}，最大元素为 3
> 
> **输入:** R = 6，arr = {{1，3}，{2，4}}，查询= {2，5，6，1 }
> T3】输出: 4 5 6 3

**方法:**给定的问题可以使用[不相交集合并](https://www.geeksforgeeks.org/union-find/)来解决。最初，所有元素都在不同的集合中，处理 **arr[]** 并对给定的对执行[联合操作](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)，在联合更新中，数组中每个集合的最大值，比如父元素的 **maxValue[]** 值。对于每个查询，执行[查找操作](https://www.geeksforgeeks.org/union-find/)，对于返回的父元素，查找**最大父元素**。按照以下步骤解决问题:

*   初始化一个向量 **maxValue[]** 求每个集合的最大元素。
*   初始化向量**父(R+1)，秩(R+1，0)，最大值(R+1)** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，R+1】**，并将**父项【I】**和**最大值【I】**的值设置为 **i** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N-1】**，并调用函数操作 **Union(父，秩，最大值，arr[i]。首先，arr[i]。第二)**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，M-1】**，并执行以下步骤:
    *   调用函数操作**查找(父，查询[i])** 。
    *   打印**最大值【I】**的值作为结果最大元素。

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
    return parent[a] = (parent[a] == a)
                           ? a
                           : (Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
void Union(vector<int>& parent,
           vector<int>& rank,
           vector<int>& maxValue,
           int a, int b)
{

    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    // If the rank are the same
    if (rank[a] == rank[b]) {
        rank[a]++;
    }

    if (rank[a] < rank[b]) {
        int temp = a;
        a = b;
        b = temp;
    }

    parent[b] = a;

    // Update the maximum value
    maxValue[a] = max(maxValue[a],
                      maxValue[b]);
}

// Function to find the maximum element
// of the set which belongs to the
// element queries[i]
void findMaxValueOfSet(
    vector<pair<int, int> >& arr,
    vector<int>& queries, int R, int N,
    int M)
{

    // Stores the parent elements
    // of the sets
    vector<int> parent(R + 1);

    // Stores the rank of the sets
    vector<int> rank(R + 1, 0);

    // Stores the maxValue of the sets
    vector<int> maxValue(R + 1);

    for (int i = 1; i < R + 1; i++) {

        // Update parent[i] and
        // maxValue[i] to i
        parent[i] = maxValue[i] = i;
    }

    for (int i = 0; i < N; i++) {

        // Add arr[i].first and
        // arr[i].second elements to
        // the same set
        Union(parent, rank, maxValue,
              arr[i].first,
              arr[i].second);
    }

    for (int i = 0; i < M; i++) {

        // Find the parent element of
        // the element queries[i]
        int P = Find(parent, queries[i]);

        // Print the maximum value
        // of the set which belongs
        // to the element P
        cout << maxValue[P] << " ";
    }
}

// Driver Code
int main()
{

    int R = 5;
    vector<pair<int, int> > arr{ { 1, 2 },
                                 { 2, 3 },
                                 { 4, 5 } };
    vector<int> queries{ 2, 4, 1, 3 };
    int N = arr.size();
    int M = queries.size();

    findMaxValueOfSet(arr, queries, R, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to perform the find operation
// to find the parent of a disjoint set
static int Find(int [] parent, int a)
{
    return parent[a] = (parent[a] == a)
                           ? a
                           : (Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
static void Union(int [] parent,
           int [] rank,
           int [] maxValue,
           int a, int b)
{

    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    // If the rank are the same
    if (rank[a] == rank[b]) {
        rank[a]++;
    }

    if (rank[a] < rank[b]) {
        int temp = a;
        a = b;
        b = temp;
    }

    parent[b] = a;

    // Update the maximum value
    maxValue[a] = Math.max(maxValue[a],
                      maxValue[b]);
}

// Function to find the maximum element
// of the set which belongs to the
// element queries[i]
static void findMaxValueOfSet(
    int[][]  arr,
    int [] queries, int R, int N,
    int M)
{

    // Stores the parent elements
    // of the sets
    int [] parent = new int[R + 1];

    // Stores the rank of the sets
    int [] rank = new int[R + 1];

    // Stores the maxValue of the sets
    int [] maxValue = new int[R + 1];

    for (int i = 1; i < R + 1; i++) {

        // Update parent[i] and
        // maxValue[i] to i
        parent[i] = maxValue[i] = i;
    }

    for (int i = 0; i < N; i++) {

        // Add arr[i][0] and
        // arr[i][1] elements to
        // the same set
        Union(parent, rank, maxValue,
              arr[i][0],
              arr[i][1]);
    }

    for (int i = 0; i < M; i++) {

        // Find the parent element of
        // the element queries[i]
        int P = Find(parent, queries[i]);

        // Print the maximum value
        // of the set which belongs
        // to the element P
        System.out.print(maxValue[P]+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int R = 5;
    int[][]  arr ={ { 1, 2 },
                                 { 2, 3 },
                                 { 4, 5 } };
    int [] queries = { 2, 4, 1, 3 };
    int N = arr.length;
    int M = queries.length;

    findMaxValueOfSet(arr, queries, R, N, M);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to perform the find operation
# to find the parent of a disjoint set
def Find(parent, a):
    if(parent[parent[a]]!=parent[a]):
        parent[a]=findParent(parent,parent[a])
    return parent[a]
    #return parent[a] = a if (parent[a] == a) else Find(parent, parent[a])

# FUnction to perform union operation
# of disjoint set union
def Union(parent, rank, maxValue, a, b):
    a = Find(parent, a)
    b = Find(parent, b)

    if (a == b):
        return

    # If the rank are the same
    if (rank[a] == rank[b]):
        rank[a] += 1

    if (rank[a] < rank[b]):
        temp = a
        a = b
        b = temp

    parent[b] = a

    # Update the maximum value
    maxValue[a] = max(maxValue[a],maxValue[b])

# Function to find the maximum element
# of the set which belongs to the
# element queries[i]
def findMaxValueOfSet(arr,queries, R, N, M):
    # Stores the parent elements
    # of the sets
    parent = [1 for i in range(R+1)]

    # Stores the rank of the sets
    rank = [0 for i in range(R+1)]

    # Stores the maxValue of the sets
    maxValue = [0 for i in range(R + 1)]

    for i in range(1,R + 1,1):

        # Update parent[i] and
        # maxValue[i] to i
        parent[i] = maxValue[i] = i

    for i in range(N):
        # Add arr[i].first and
        # arr[i].second elements to
        # the same set
        Union(parent, rank, maxValue, arr[i][0],arr[i][1])

    for i in range(M):
        # Find the parent element of
        # the element queries[i]
        P = Find(parent, queries[i])

        # Print the maximum value
        # of the set which belongs
        # to the element P
        print(maxValue[P],end = " ")

# Driver Code
if __name__ == '__main__':
    R = 5
    arr = [[1, 2],
           [2, 3],
           [4, 5]];
    queries =  [2, 4, 1, 3]
    N = len(arr)
    M = len(queries)

    findMaxValueOfSet(arr, queries, R, N, M)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to perform the find operation
// to find the parent of a disjoint set
static int Find(int [] parent, int a)
{
    return parent[a] = (parent[a] == a)
                           ? a
                           : (Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
static void Union(int [] parent,
           int [] rank,
           int [] maxValue,
           int a, int b)
{

    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    // If the rank are the same
    if (rank[a] == rank[b]) {
        rank[a]++;
    }

    if (rank[a] < rank[b]) {
        int temp = a;
        a = b;
        b = temp;
    }

    parent[b] = a;

    // Update the maximum value
    maxValue[a] = Math.Max(maxValue[a],
                      maxValue[b]);
}

// Function to find the maximum element
// of the set which belongs to the
// element queries[i]
static void findMaxValueOfSet(
    int[,]  arr,
    int [] queries, int R, int N,
    int M)
{

    // Stores the parent elements
    // of the sets
    int [] parent = new int[R + 1];

    // Stores the rank of the sets
    int [] rank = new int[R + 1];

    // Stores the maxValue of the sets
    int [] maxValue = new int[R + 1];

    for (int i = 1; i < R + 1; i++) {

        // Update parent[i] and
        // maxValue[i] to i
        parent[i] = maxValue[i] = i;
    }

    for (int i = 0; i < N; i++) {

        // Add arr[i,0] and
        // arr[i,1] elements to
        // the same set
        Union(parent, rank, maxValue,
              arr[i,0],
              arr[i,1]);
    }

    for (int i = 0; i < M; i++) {

        // Find the parent element of
        // the element queries[i]
        int P = Find(parent, queries[i]);

        // Print the maximum value
        // of the set which belongs
        // to the element P
        Console.Write(maxValue[P]+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int R = 5;
    int[,]  arr ={ { 1, 2 },
                                 { 2, 3 },
                                 { 4, 5 } };
    int [] queries = { 2, 4, 1, 3 };
    int N = arr.GetLength(0);
    int M = queries.Length;

    findMaxValueOfSet(arr, queries, R, N, M);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to perform the find operation
// to find the parent of a disjoint set
function Find(parent, a) {
  return (parent[a] = parent[a] == a ? a : Find(parent, parent[a]));
}

// FUnction to perform union operation
// of disjoint set union
function Union(parent, rank, maxValue, a, b) {
  a = Find(parent, a);
  b = Find(parent, b);

  if (a == b) return;

  // If the rank are the same
  if (rank[a] == rank[b]) {
    rank[a]++;
  }

  if (rank[a] < rank[b]) {
    let temp = a;
    a = b;
    b = temp;
  }

  parent[b] = a;

  // Update the maximum value
  maxValue[a] = Math.max(maxValue[a], maxValue[b]);
}

// Function to find the maximum element
// of the set which belongs to the
// element queries[i]
function findMaxValueOfSet(arr, queries, R, N, M) {
  // Stores the parent elements
  // of the sets
  let parent = new Array(R + 1);

  // Stores the rank of the sets
  let rank = new Array(R + 1).fill(0);

  // Stores the maxValue of the sets
  let maxValue = new Array(R + 1);

  for (let i = 1; i < R + 1; i++) {
    // Update parent[i] and
    // maxValue[i] to i
    parent[i] = maxValue[i] = i;
  }

  for (let i = 0; i < N; i++) {
    // Add arr[i][0] and
    // arr[i][1] elements to
    // the same set
    Union(parent, rank, maxValue, arr[i][0], arr[i][1]);
  }

  for (let i = 0; i < M; i++) {
    // Find the parent element of
    // the element queries[i]
    let P = Find(parent, queries[i]);

    // Print the maximum value
    // of the set which belongs
    // to the element P
    document.write(maxValue[P] + " ");
  }
}

// Driver Code

let R = 5;
let arr = [
  [1, 2],
  [2, 3],
  [4, 5],
];
let queries = [2, 4, 1, 3];
let N = arr.length;
let M = queries.length;

findMaxValueOfSet(arr, queries, R, N, M);

// This code is contributed by ipg2016107
</script>
```

**Output:** 

```
3 5 3 3
```

***时间复杂度:** O(N*log M)*
***辅助空间:** O(N)*