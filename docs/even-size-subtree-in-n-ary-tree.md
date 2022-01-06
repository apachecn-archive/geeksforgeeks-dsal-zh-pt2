# n 元树中偶数大小的子树

> 原文:[https://www . geesforgeks . org/n 元树中的偶数大小子树/](https://www.geeksforgeeks.org/even-size-subtree-in-n-ary-tree/)

给定 n 个顶点和 n-1 条边的 n 元树。该树以邻接表的形式给出。找出给定树中偶数大小的子树的数目。

**示例:**

```
Input : 
                1
               / \
              2   3
             / \   \
            4   5   6
               / \
              7   8

Output : 2
Subtree rooted at 1 and 3 are of even size. 

Input :
                1
               / \
              2   3
            / | \   \
           4  5  6   7
            / | \
           8  9 10

Output : 3
Subtree rooted at 1, 3 and 5 are of even size.
```

一个简单的**解决方案是从每个节点开始执行 dfs，并找到以该节点为根的子树的大小。如果大小是偶数增量计数。上述解的时间复杂度为 0(n<sup>2</sup>)。**

**更好的解决方案是对给定的树执行单个 dfs。其思想是先递归求所有子节点的子树的大小，然后取子节点子树的大小之和，如果大小为偶数，则递增计数，求以当前节点为根的子树大小。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to find number of subtrees of even size.
#include <bits/stdc++.h>
using namespace std;

// DFS function to traverse the tree and find
// number of even size subtree.
int dfs(vector<int> adj[], int n, int v, int& ans)
{
    // Size of subtree is minimum possible 1 for
    // leaf node.
    int size = 1;

    // Find size of subtree rooted at children nodes
    // and add the size to current subtree size.
    for (auto ele : adj[v]) {
        size += dfs(adj, n, ele, ans);
    }

    // If size is even then increment count.
    if (size % 2 == 0)
        ans++;

    return size;
}

// Driver code
int main()
{
    int n;
    n = 10;

    vector<int> adj[n + 1];
    /*
                1
               / \
              2   3
             / \   \
            4   5   6
               / \
              7   8
    */
    adj[1].push_back(2);
    adj[1].push_back(3);
    adj[2].push_back(4);
    adj[2].push_back(5);
    adj[3].push_back(6);
    adj[5].push_back(7);
    adj[5].push_back(8);

    /*
                 1
                / \
               2   3
             / | \  \
            4  5  6  7
             / | \
            8  9 10
    */
    /*adj[1].push_back(2);
    adj[1].push_back(3);
    adj[2].push_back(4);
    adj[2].push_back(5);
    adj[2].push_back(6);
    adj[3].push_back(7);
    adj[5].push_back(8);
    adj[5].push_back(9);
    adj[5].push_back(10);
    */
    int ans = 0;

    dfs(adj, n, 1, ans);

    cout << ans;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find number of
// subtrees of even size.
import java.io.*;
import java.util.*;
class GFG
{
  public static int ans = 0;

  // DFS function to traverse the tree and
  // find number of even size subtree.
  static int dfs(ArrayList<ArrayList<Integer>> adj,
                 int n,int v)
  {

    // Size of subtree is minimum possible 1
    // for leaf node.
    int size = 1;

    // Find size of subtree rooted at children
    // nodes and add the size to current
    // subtree size.
    for(int ele:adj.get(v))
    {
      size += dfs(adj, n, ele);
    }

    // If size is even then increment count.
    if(size % 2 == 0)
    {
      ans++;
    }
    return size;
  }

  // Driver code
  public static void main (String[] args)
  {
    int n;
    n = 10;
    ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer> >();
    for(int i = 0; i < n + 1; i++)
    {
      adj.add(new ArrayList<Integer>());
    }

    /*
                1
               / \
              2   3
             / \   \
            4   5   6
               / \
              7   8
        */
    adj.get(1).add(2);
    adj.get(1).add(3);
    adj.get(2).add(4);
    adj.get(2).add(5);
    adj.get(3).add(6);
    adj.get(5).add(7);
    adj.get(5).add(8);

    /*
                 1
                / \
               2   3
             / | \  \
            4  5  6  7
             / | \
            8  9 10
        */
    /*adj[1].Add(2);
        adj[1].Add(3);
        adj[2].Add(4);
        adj[2].Add(5);
        adj[2].Add(6);
        adj[3].Add(7);
        adj[5].Add(8);
        adj[5].Add(9);
        adj[5].Add(10);
        */

    dfs(adj, n, 1);       
    System.out.println(ans);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## **蟒蛇 3**

```
# Python3 program to find number
# of subtrees of even size
ans = 0

# DFS function to traverse the tree
# and find number of even size subtree
def dfs(adj, n, v):

    global ans

    # Size of subtree is minimum possible
    # 1 for leaf node.
    size = 1

    # Find size of subtree rooted at
    # children nodes and add the size
    # to current subtree size.
    for ele in adj[v]:
        size += dfs(adj, n, ele)

    # If size is even then increment count.
    if (size % 2 == 0):
        ans += 1

    return size

# Driver code
if __name__ == '__main__':

    n = 10

    adj = [[] for i in range(n + 1)]

    #             1
    #            / \
    #           2   3
    #          / \   \
    #         4   5   6
    #            / \
    #           7   8
    adj[1].append(2)
    adj[1].append(3)
    adj[2].append(4)
    adj[2].append(5)
    adj[3].append(6)
    adj[5].append(7)
    adj[5].append(8)

    #              1
    #             / \
    #            2   3
    #          / | \  \
    #         4  5  6  7
    #          / | \
    #         8  9 10
    #
    # adj[1].append(2)
    # adj[1].append(3)
    # adj[2].append(4)
    # adj[2].append(5)
    # adj[2].append(6)
    # adj[3].append(7)
    # adj[5].append(8)
    # adj[5].append(9)
    # adj[5].append(10)
    #
    # ans = 0

    dfs(adj, n, 1)

    print(ans)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program to find number of
// subtrees of even size.
using System;
using System.Collections;

class GFG{

// DFS function to traverse the tree and
// find number of even size subtree.
static int dfs(ArrayList []adj, int n,
              int v, ref int ans)
{

    // Size of subtree is minimum possible 1
    // for leaf node.
    int size = 1;

    // Find size of subtree rooted at children
    // nodes and add the size to current
    // subtree size.
    foreach(int ele in adj[v])
    {
        size += dfs(adj, n, ele, ref ans);
    }

    // If size is even then increment count.
    if (size % 2 == 0)
        ans++;

    return size;
}

// Driver code
public static void Main(string []args)
{
    int n;
    n = 10;

    ArrayList []adj = new ArrayList[n + 1];

    for(int i = 0; i < n + 1; i++)
    {
        adj[i] = new ArrayList();
    }

    /*
                1
               / \
              2   3
             / \   \
            4   5   6
               / \
              7   8
    */
    adj[1].Add(2);
    adj[1].Add(3);
    adj[2].Add(4);
    adj[2].Add(5);
    adj[3].Add(6);
    adj[5].Add(7);
    adj[5].Add(8);

    /*
                 1
                / \
               2   3
             / | \  \
            4  5  6  7
             / | \
            8  9 10
    */
    /*adj[1].Add(2);
    adj[1].Add(3);
    adj[2].Add(4);
    adj[2].Add(5);
    adj[2].Add(6);
    adj[3].Add(7);
    adj[5].Add(8);
    adj[5].Add(9);
    adj[5].Add(10);
    */
    int ans = 0;

    dfs(adj, n, 1, ref ans);

    Console.Write(ans);
}
}

// This code is contributed by rutvik_56
```

## **java 描述语言**

```
<script>
// Javascript program to find number of subtrees of even size.

var ans = 0;

// DFS function to traverse the tree and find
// number of even size subtree.
function dfs(adj, n, v)
{
    // Size of subtree is minimum possible 1 for
    // leaf node.
    var size = 1;

    // Find size of subtree rooted at children nodes
    // and add the size to current subtree size.
    for(var i =0; i< adj[v].length; i++)
    {
        size += dfs(adj, n, adj[v][i]);
    }

    // If size is even then increment count.
    if (size % 2 == 0)
        ans++;

    return size;
}

// Driver code
var n;
n = 10;
var adj = Array.from(Array(n+1), () => new Array(0))
/*
            1
           / \
          2   3
         / \   \
        4   5   6
           / \
          7   8
*/
adj[1].push(2);
adj[1].push(3);
adj[2].push(4);
adj[2].push(5);
adj[3].push(6);
adj[5].push(7);
adj[5].push(8);
/*
             1
            / \
           2   3
         / | \  \
        4  5  6  7
         / | \
        8  9 10
*/
/*adj[1].push(2);
adj[1].push(3);
adj[2].push(4);
adj[2].push(5);
adj[2].push(6);
adj[3].push(7);
adj[5].push(8);
adj[5].push(9);
adj[5].push(10);
*/
dfs(adj, n, 1);
document.write( ans);

// This code is contributed by noob2000.
</script>
```

****输出:****

```
 2
```

****时间复杂度:**O(n)
T3】辅助空间: O(1)**