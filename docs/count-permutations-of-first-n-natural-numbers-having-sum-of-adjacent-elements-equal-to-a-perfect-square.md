# 计算相邻元素之和等于完美平方的前 N 个自然数的排列数

> 原文:[https://www . geeksforgeeks . org/count-第一个 n 个自然数的排列-具有相邻元素之和-等于完美平方/](https://www.geeksforgeeks.org/count-permutations-of-first-n-natural-numbers-having-sum-of-adjacent-elements-equal-to-a-perfect-square/)

给定一个正整数 **N** ，任务是找出相邻元素之和等于一个[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)的第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的唯一排列数。

**示例:**

> **输入:** N = 17
> **输出:** 2
> **解释:**
> 以下排列的相邻元素之和等于一个完美的正方形:
> 
> 1.  {17, 8, 1, 15, 10, 6, 3, 13, 12, 4, 5, 11, 14, 2, 7, 9, 16}
> 2.  {16, 9, 7, 2, 14, 11, 5, 4, 12, 13, 3, 6, 10, 15, 1, 8, 17}
> 
> 因此，这种排列的计数是 2。
> 
> **输入:**N = 13
> T3】输出: 0

**方法:**利用[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)的概念可以解决给定的问题。按照以下步骤解决问题:

*   列出从[到**(2 * N–1)**的所有可以通过任意两个正整数相加得到的完美平方数](https://www.geeksforgeeks.org/print-all-perfect-squares-from-the-given-range/)。
*   将图表示为[邻接表表示](https://www.geeksforgeeks.org/graph-and-its-representations/)，这样如果两个数的和 **X** 和 **Y** 是一个完美的正方形，那么从节点 **X** 到节点 **Y** 添加一条边。
*   [计算图中内角为 1 的节点数](https://www.geeksforgeeks.org/finding-in-and-out-degrees-of-all-vertices-in-a-graph/)并将其存储在变量 **X** 中。
*   现在，置换数可以按照以下条件计算:
    *   如果 **X** 的值是 **0** ，那么总共有 **N 个**排列是可能的。因此，打印 **N** 作为结果。
    *   如果 **X** 的值是 **1** 或 **2** ，那么总共有 **2** 种排列是可能的。因此，打印 **2** 作为结果。
    *   否则，不存在满足给定标准的这种排列。因此，打印 **0** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count total number of
// permutation of the first N natural
// number having the sum of adjacent
// elements as perfect square
int countPermutations(int N)
{
    // Create an adjacency matrix
    vector<vector<int> > adj(105);

    // Count elements whose indegree
    // is 1
    int indeg = 0;

    // Generate adjacency matrix
    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= N; j++) {

            if (i == j)
                continue;

            // Find the sum of i and j
            int sum = i + j;

            // If sum is perfect square.
            // then move from i to j
            if (ceil(sqrt(sum))
                == floor(sqrt(sum))) {

                // Add it in adjacency
                // list of i
                adj[i].push_back(j);
            }
        }

        // If any list is of size 1,
        // then the indegree is 1
        if (adj[i].size() == 1)
            indeg++;
    }

    // If there is no element whose
    // indegree is 1, then N such
    // permutations are possible
    if (indeg == 0)
        return N;

    // If there is 1 or 2 elements
    // whose indegree is 1, then 2
    // permutations are possible
    else if (indeg <= 2)
        return 2;

    // If there are more than 2
    // elements whose indegree is
    // 1, then return 0
    else
        return 0;
}

// Driver Code
int main()
{
    int N = 17;
    cout << countPermutations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG{

// Function to count total number of
// permutation of the first N natural
// number having the sum of adjacent
// elements as perfect square
static int countPermutations(int N)
{

    // Create an adjacency matrix
    ArrayList<
    ArrayList<Integer>> adj = new ArrayList<
                                  ArrayList<Integer>>(105);

      for(int i = 0; i < 105; i++)
        adj.add(new ArrayList<Integer>());

    // Count elements whose indegree
    // is 1
    int indeg = 0;

    // Generate adjacency matrix
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            if (i == j)
                continue;

            // Find the sum of i and j
            int sum = i + j;

            // If sum is perfect square.
            // then move from i to j
            if (Math.ceil(Math.sqrt(sum)) ==
                Math.floor(Math.sqrt(sum)))
            {

                // Add it in adjacency
                // list of i
                adj.get(i).add(j);
            }
        }

        // If any list is of size 1,
        // then the indegree is 1
        if (adj.get(i).size() == 1)
            indeg++;
    }

    // If there is no element whose
    // indegree is 1, then N such
    // permutations are possible
    if (indeg == 0)
        return N;

    // If there is 1 or 2 elements
    // whose indegree is 1, then 2
    // permutations are possible
    else if (indeg <= 2)
        return 2;

    // If there are more than 2
    // elements whose indegree is
    // 1, then return 0
    else
        return 0;
}

// Driver Code
public static void main(String[] args)
{
    int N = 17;

    System.out.println(countPermutations(N));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python program for the above approach
from math import sqrt,floor,ceil

# Function to count total number of
# permutation of the first N natural
# number having the sum of adjacent
# elements as perfect square
def countPermutations(N):
    # Create an adjacency matrix
    adj = [[] for i in range(105)]

    # bCount elements whose indegree
    # bis 1
    indeg = 0

    # bGenerate adjacency matrix
    for i in range(1, N + 1):
        for j in range(1, N + 1):
            if (i == j):
                continue

            # Find the sum of i and j
            sum = i + j

            # If sum is perfect square.
            # then move from i to j
            if (ceil(sqrt(sum)) == floor(sqrt(sum))):

                # Add it in adjacency
                # list of i
                adj[i].append(j)

        # If any list is of size 1,
        # then the indegree is 1
        if (len(adj[i]) == 1):
            indeg += 1

    # If there is no element whose
    # indegree is 1, then N such
    # permutations are possible
    if (indeg == 0):
        return N

    # If there is 1 or 2 elements
    # whose indegree is 1, then 2
    # permutations are possible
    elif (indeg <= 2):
        return 2

    # If there are more than 2
    # elements whose indegree is
    # 1, then return 0
    else:
        return 0

# Driver Code
if __name__ == '__main__':
    N = 17
    print (countPermutations(N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count total number of
// permutation of the first N natural
// number having the sum of adjacent
// elements as perfect square
static int countPermutations(int N)
{

    // Create an adjacency matrix
    List<List<int>> adj = new List<List<int>>(105);

    for(int i = 0; i < 105; i++)
        adj.Add(new List<int>());

    // Count elements whose indegree
    // is 1
    int indeg = 0;

    // Generate adjacency matrix
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            if (i == j)
                continue;

            // Find the sum of i and j
            int sum = i + j;

            // If sum is perfect square.
            // then move from i to j
            if (Math.Ceiling(Math.Sqrt(sum)) ==
                Math.Floor(Math.Sqrt(sum)))
            {

                // Add it in adjacency
                // list of i
                adj[i].Add(j);
            }
        }

        // If any list is of size 1,
        // then the indegree is 1
        if (adj[i].Count == 1)
            indeg++;
    }

    // If there is no element whose
    // indegree is 1, then N such
    // permutations are possible
    if (indeg == 0)
        return N;

    // If there is 1 or 2 elements
    // whose indegree is 1, then 2
    // permutations are possible
    else if (indeg <= 2)
        return 2;

    // If there are more than 2
    // elements whose indegree is
    // 1, then return 0
    else
        return 0;
}

// Driver Code
public static void Main()
{
    int N = 17;

    Console.WriteLine(countPermutations(N));
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count total number of
// permutation of the first N natural
// number having the sum of adjacent
// elements as perfect square
function countPermutations(N)
{
    // Create an adjacency matrix
    let adj = [];

      for(let i = 0; i < 105; i++)
        adj.push([]);

    // Count elements whose indegree
    // is 1
    let indeg = 0;

    // Generate adjacency matrix
    for(let i = 1; i <= N; i++)
    {
        for(let j = 1; j <= N; j++)
        {
            if (i == j)
                continue;

            // Find the sum of i and j
            let sum = i + j;

            // If sum is perfect square.
            // then move from i to j
            if (Math.ceil(Math.sqrt(sum)) ==
                Math.floor(Math.sqrt(sum)))
            {

                // Add it in adjacency
                // list of i
                adj[i].push(j);
            }
        }

        // If any list is of size 1,
        // then the indegree is 1
        if (adj[i].length == 1)
            indeg++;
    }

    // If there is no element whose
    // indegree is 1, then N such
    // permutations are possible
    if (indeg == 0)
        return N;

    // If there is 1 or 2 elements
    // whose indegree is 1, then 2
    // permutations are possible
    else if (indeg <= 2)
        return 2;

    // If there are more than 2
    // elements whose indegree is
    // 1, then return 0
    else
        return 0;
}

// Driver Code
let N = 17;

document.write(countPermutations(N));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*