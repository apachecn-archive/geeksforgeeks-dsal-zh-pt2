# 表示为邻接表的 n 元树(非循环图)的 DFS

> 原文:[https://www . geesforgeks . org/DFS-n-ary-tree-noncircular-graph-presented-邻接表/](https://www.geeksforgeeks.org/dfs-n-ary-tree-acyclic-graph-represented-adjacency-list/)

给出了一个由 n 个节点组成的树，我们需要打印它的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。
**例:**

```
Input : Edges of graph
        1 2
        1 3
        2 4
        3 5
Output : 1 2 4 3 5
```

一个简单的解决办法就是做执行标准 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。
我们可以修改我们的方法，以避免访问节点的额外空间。我们可以跟踪父级，而不是使用访问过的数组。我们遍历除父节点之外的所有相邻节点。
下面是实现:

## C++

```
/* CPP code to perform DFS of given tree : */
#include <bits/stdc++.h>
using namespace std;

// DFS on tree
void dfs(vector<int> list[], int node, int arrival)
{
    // Printing traversed node
    cout << node << '\n';

    // Traversing adjacent edges
    for (int i = 0; i < list[node].size(); i++) {

        // Not traversing the parent node
        if (list[node][i] != arrival)
            dfs(list, list[node][i], node);
    }
}

int main()
{
    // Number of nodes
    int nodes = 5;

    // Adjacency list
    vector<int> list[10000];

    // Designing the tree
    list[1].push_back(2);
    list[2].push_back(1);

    list[1].push_back(3);
    list[3].push_back(1);

    list[2].push_back(4);
    list[4].push_back(2);

    list[3].push_back(5);
    list[5].push_back(3);

    // Function call
    dfs(list, 1, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//JAVA Code For DFS for a n-ary tree (acyclic graph)
// represented as adjacency list
import java.util.*;

class GFG {

    // DFS on tree
    public static void dfs(LinkedList<Integer> list[],
                             int node, int arrival)
    {
        // Printing traversed node
        System.out.println(node);

        // Traversing adjacent edges
        for (int i = 0; i < list[node].size(); i++) {

            // Not traversing the parent node
            if (list[node].get(i) != arrival)
                dfs(list, list[node].get(i), node);
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

        // Number of nodes
        int nodes = 5;

        // Adjacency list
        LinkedList<Integer> list[] = new LinkedList[nodes+1];    

        for (int i = 0; i < list.length; i ++){
            list[i] = new LinkedList<Integer>();
        }

        // Designing the tree
        list[1].add(2);
        list[2].add(1);

        list[1].add(3);
        list[3].add(1);

        list[2].add(4);
        list[4].add(2);

        list[3].add(5);
        list[5].add(3);

        // Function call
        dfs(list, 1, 0);

    }
}
// This code is contributed by Arnav Kr. Mandal. 
```

## 蟒蛇 3

```
# Python3 code to perform DFS of given tree :

# DFS on tree
def dfs(List, node, arrival):

    # Printing traversed node
    print(node)

    # Traversing adjacent edges
    for i in range(len(List[node])):

        # Not traversing the parent node
        if (List[node][i] != arrival):
            dfs(List, List[node][i], node)

# Driver Code
if __name__ == '__main__':

    # Number of nodes
    nodes = 5

    # Adjacency List
    List = [[] for i in range(10000)]

    # Designing the tree
    List[1].append(2)
    List[2].append(1)

    List[1].append(3)
    List[3].append(1)

    List[2].append(4)
    List[4].append(2)

    List[3].append(5)
    List[5].append(3)

    # Function call
    dfs(List, 1, 0)

# This code is contributed by PranchalK
```

## C#

```
// C# Code For DFS for a n-ary tree (acyclic graph)
// represented as adjacency list
using System;
using System.Collections.Generic;
public class GFG {

    // DFS on tree
    public static void dfs(List<int> []list,
                            int node, int arrival)
    {
        // Printing traversed node
        Console.WriteLine(node);

        // Traversing adjacent edges
        for (int i = 0; i < list[node].Count; i++) {

            // Not traversing the parent node
            if (list[node][i] != arrival)
                dfs(list, list[node][i], node);
        }
    }

    /* Driver program to test above function */
    public static void Main(String[] args)
    {

        // Number of nodes
        int nodes = 5;

        // Adjacency list
        List<int> []list = new List<int>[nodes+1];    

        for (int i = 0; i < list.Length; i ++){
            list[i] = new List<int>();
        }

        // Designing the tree
        list[1].Add(2);
        list[2].Add(1);

        list[1].Add(3);
        list[3].Add(1);

        list[2].Add(4);
        list[4].Add(2);

        list[3].Add(5);
        list[5].Add(3);

        // Function call
        dfs(list, 1, 0);

    }
}
// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript Code For DFS for a n-ary tree (acyclic graph)
    // represented as adjacency list

    // DFS on tree
    function dfs(list, node, arrival)
    {
        // Printing traversed node
        document.write(node + "</br>");

        // Traversing adjacent edges
        for (let i = 0; i < list[node].length; i++) {

            // Not traversing the parent node
            if (list[node][i] != arrival)
                dfs(list, list[node][i], node);
        }
    }

    // Number of nodes
    let nodes = 5;

    // Adjacency list
    let list = new Array(nodes+1);    

    for (let i = 0; i < list.length; i ++){
      list[i] = [];
    }

    // Designing the tree
    list[1].push(2);
    list[2].push(1);

    list[1].push(3);
    list[3].push(1);

    list[2].push(4);
    list[4].push(2);

    list[3].push(5);
    list[5].push(3);

    // Function call
    dfs(list, 1, 0);

</script>
```

**输出:**

```
1
2
4
3
5
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。