# 在 K 个三元组(A，B，C)之后创建一个数树[1，N]，这样从 A 到 C 的任何路径都不能包含 B

> 原文:[https://www . geesforgeks . org/create-a-数字树-1-n-following-k-triplets-a-B- c-这样从 a 到 c 的任何路径都不能包含-b/](https://www.geeksforgeeks.org/create-a-tree-of-numbers-1-n-following-k-triplets-a-b-c-such-that-any-path-from-a-to-c-cannot-contain-b/)

给定一个整数 **N** 代表数字**【1，N】**和 **K** 以三元组 **{A，B，C}，**的形式进行限制，这样从 **A** 到 **C** 的任何简单路径都不能包含**B。**任务是按照这些 K 个限制创建一个数字【1，N】的树，并打印该树的边。假设对于给定的一组限制，树总是存在的。

***例:***

> ***输入:** N = 8，限制[] = {{1，2，3}，{3，4，5}，{5，6，7}，{6，7，4}}*
> ***输出:***
> 3 4
> 3 5
> 3 1
> 1 2
> 2 8
> 8 6
> 8
> 7】解释:树形成如下
> 
> 3
> /| \
> 4 5 1
> |
> 2
> |
> 8
> /\
> 6 7
> 
> **输入:** N = 8，限制[] = {{3，2，4}，{3，5，4}，{5，8，7}，{6，1，8 } }
> T3】输出:T5】3 1
> 3 2
> 3 4
> 3 5
> 3 6
> 3 7
> 3 8

**方法:**这个问题的基本思路是，对于一棵树，每个节点只能有一个父节点。因此，总有一个节点不受限制，它可以位于任意两个节点之间。因此，将该节点连接到所有节点以获得答案。现在要解决这个问题，请遵循以下步骤:

1.  创建一个布尔[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **访问过的**，它会用限制标记所有节点 **1** ，并用 **0** 初始化它。
2.  对所有限制重复一个[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，并用 **1** 标记访问数组中有限制的所有节点。
3.  将**访问的**数组中 **0** 值的节点值存储为**根**。
4.  用**根**连接所有节点。
5.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the tree following
// the given restrictions
void RestrictedTree(
    vector<vector<int> >& restrictions,
    int N)
{
    // Vector to track the restricted nodes
    vector<int> visited(N + 1, false);

    // Loop to mark the restricted node visited
    for (int index = 0;
         index < restrictions.size();
         index++) {

        int a = restrictions[index][1];
        visited[a] = true;
    }

    // Variable to consider root node
    int root = -1;
    for (int index = 1; index <= N; index++) {
        if (visited[index] == false) {
            root = index;
            break;
        }
    }

    // Connecting all node to the root node
    for (int index = 1; index <= N; index++) {

        if (index != root) {
            cout << root << " "
                 << index << "\n";
        }
    }
    return;
}

// Driver code
int main()
{
    int N = 8;
    vector<vector<int> > restrictions = {
        { 3, 2, 4 },
        { 3, 5, 4 },
        { 5, 8, 7 },
        { 6, 1, 8 }
    };

    RestrictedTree(restrictions, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to print the tree following
// the given restrictions
static void RestrictedTree(
    int[][]restrictions,
    int N)
{

    // Vector to track the restricted nodes
    boolean visited[] = new boolean[N + 1];

    // Loop to mark the restricted node visited
    for (int index = 0;
         index < restrictions.length;
         index++) {

        int a = restrictions[index][1];
        visited[a] = true;
    }

    // Variable to consider root node
    int root = -1;
    for (int index = 1; index <= N; index++) {
        if (visited[index] == false) {
            root = index;
            break;
        }
    }

    // Connecting all node to the root node
    for (int index = 1; index <= N; index++) {

        if (index != root) {
            System.out.print(root+ " "
                 + index+ "\n");
        }
    }
    return;
}

// Driver code
public static void main(String[] args)
{
    int N = 8;
    int [][]restrictions = {
        { 3, 2, 4 },
        { 3, 5, 4 },
        { 5, 8, 7 },
        { 6, 1, 8 }
    };

    RestrictedTree(restrictions, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to print the tree following
# the given restrictions
def RestrictedTree(restrictions, N):

    # Vector to track the restricted nodes
    visited = [False] * (N + 1)

    # Loop to mark the restricted node visited
    for index in range(len(restrictions)):
        a = restrictions[index][1]
        visited[a] = True

    # Variable to consider root node
    root = -1
    for index in range(1, N + 1):
        if (visited[index] == False):
            root = index
            break

    # Connecting all node to the root node
    for index in range(1, N + 1):

        if (index != root):
            print(f'{root} {index}')

    return

# Driver code
N = 8
restrictions = [
    [3, 2, 4],
    [3, 5, 4],
    [5, 8, 7],
    [6, 1, 8]
]

RestrictedTree(restrictions, N)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to print the tree following
// the given restrictions
static void RestrictedTree(
    int[,]restrictions,
    int N)
{

    // Vector to track the restricted nodes
    bool []visited = new bool[N + 1];

    // Loop to mark the restricted node visited
    for (int index = 0;
         index < restrictions.GetLength(0);
         index++) {

        int a = restrictions[index,1];
        visited[a] = true;
    }

    // Variable to consider root node
    int root = -1;
    for (int index = 1; index <= N; index++) {
        if (visited[index] == false) {
            root = index;
            break;
        }
    }

    // Connecting all node to the root node
    for (int index = 1; index <= N; index++) {

        if (index != root) {
            Console.Write(root+ " "
                 + index+ "\n");
        }
    }
    return;
}

// Driver code
public static void Main(string[] args)
{
    int N = 8;
    int [,]restrictions = {
        { 3, 2, 4 },
        { 3, 5, 4 },
        { 5, 8, 7 },
        { 6, 1, 8 }
    };

    RestrictedTree(restrictions, N);
}
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach

      // Function to print the tree following
      // the given restrictions
      function RestrictedTree(
          restrictions, N)
         {

          // Vector to track the restricted nodes
          let visited = new Array(N + 1).fill(false);

          // Loop to mark the restricted node visited
          for (let index = 0;
              index < restrictions.length;
              index++) {

              let a = restrictions[index][1];
              visited[a] = true;
          }

          // Variable to consider root node
          let root = -1;
          for (let index = 1; index <= N; index++) {
              if (visited[index] == false) {
                  root = index;
                  break;
              }
          }

          // Connecting all node to the root node
          for (let index = 1; index <= N; index++) {

              if (index != root) {
                  document.write(root + " "
                      + index + '<br>');
              }
          }
          return;
      }

      // Driver code
      let N = 8;
      let restrictions = [
          [3, 2, 4],
          [3, 5, 4],
          [5, 8, 7],
          [6, 1, 8]
      ];

      RestrictedTree(restrictions, N);

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
3 1
3 2
3 4
3 5
3 6
3 7
3 8
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)