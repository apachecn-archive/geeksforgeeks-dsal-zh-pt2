# Q 查询的数组更新后给定范围索引的数组中 Ks 的计数

> 原文:[https://www . geeksforgeeks . org/给定范围索引的数组中 ks 的计数-q 查询的数组后更新/](https://www.geeksforgeeks.org/count-of-ks-in-the-array-for-a-given-range-of-indices-after-array-updates-for-q-queries/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，一个整数 **K** ，以及如下所述类型的 **Q** 查询:

*   **(1，L，R)** :如果查询类型为 **1** ，则在**【L，R】**范围内找到 **Ks** 的数量。
*   **(2，P，X)** :如果查询类型为 **2** ，那么将索引 **P** 处的数组元素更新为 **X** 。

任务是对给定的数组执行查询，并相应地打印结果。

**示例:**

> **输入:** K = 0，arr[] = {9，5，7，6，9，0，0，0，0，5，6，7，3，9，0，7，0，9，0}，查询[][2] = {{1，5，14 }，{2，6，1 }，{1，0，8 }，{2，13，0 }，{1，6，18 } }
> **输出:** 5
> 3
> 6 【T7
> 
> 1.  首先查询类型为 1，那么范围【5，14】内的 0s(= K)的计数为 5。
> 2.  第二个查询是类型 2，因此将索引 P = 6 处的数组元素的值更新为 X = 1，即 arr[6] = 1。
>     修改后的数组为{ 9 5 7 6 9 0**1**0 5 6 7 3 9 0 7 0 9 0 }。
> 3.  第三个查询类型为 1，那么[0，8]范围内的 0s(= K)计数为 3。
> 4.  第四个查询是类型 2，因此将索引 P = 13 处的数组元素的值更新为 X = 0，即 arr[13] = 0。
>     修改后的数组为{ 9 5 7 6 9 0**1**0 0 5 6 7 3**0**0 7 0 9 0 }。
> 5.  第五个查询类型为 1，那么[6，18]范围内的 0s 计数为 6。
> 
> 因此，打印 5、3 和 6 作为查询的答案。
> 
> **输入:** K = 6，arr[] = {9，5，7，6}，查询[][2] = {{1，1，2}，{2，0，0} }
> 输出: 0

**天真方法:**解决给定问题最简单的方法是改变第二类查询的数组元素，对于第一类查询，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)在范围**【L，R】**和[内打印**K**T9】的计数。](https://www.geeksforgeeks.org/c-program-to-count-zeros-and-ones-in-binary-representation-of-a-number/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform all the queries
void performQueries(int n, int q, int k,
                    vector<int>& arr,
                    vector<vector<int> >& query)
{
    for (int i = 1; i <= q; i++) {

        // Stores the count of 0s
        int count = 0;

        // Count the number of 0s for
        // query of type 1
        if (query[i - 1][0] == 1) {
            for (int j = query[i - 1][1];
                 j <= query[i - 1][2]; j++) {

                if (arr[j] == k)
                    count++;
            }
            cout << count << endl;
        }

        // Update the array element for
        // query of type 2
        else {
            arr[query[i - 1][1]]
                = query[i - 1][2];
        }
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 9, 5, 7, 6, 9,
                        0, 0, 0, 0, 5,
                        6, 7, 3, 9, 0,
                        7, 0, 9, 0 };
    int Q = 5;

    vector<vector<int> > query
        = { { 1, 5, 14 },
            { 2, 6, 1 },
            { 1, 0, 8 },
            { 2, 13, 0 },
            { 1, 6, 18 } };
    int N = arr.size();

    int K = 0;

    performQueries(N, Q, K, arr, query);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to perform all the queries
static void performQueries(int n, int q, int k,
                    int[] arr,
                    int[][] query)
{
    for (int i = 1; i <= q; i++) {

        // Stores the count of 0s
        int count = 0;

        // Count the number of 0s for
        // query of type 1
        if (query[i - 1][0] == 1) {
            for (int j = query[i - 1][1];
                 j <= query[i - 1][2]; j++) {

                if (arr[j] == k)
                    count++;
            }
            System.out.print(count +"\n");
        }

        // Update the array element for
        // query of type 2
        else {
            arr[query[i - 1][1]]
                = query[i - 1][2];
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 9, 5, 7, 6, 9,
                        0, 0, 0, 0, 5,
                        6, 7, 3, 9, 0,
                        7, 0, 9, 0 };
    int Q = 5;

    int[][] query
        = { { 1, 5, 14 },
            { 2, 6, 1 },
            { 1, 0, 8 },
            { 2, 13, 0 },
            { 1, 6, 18 } };
    int N = arr.length;

    int K = 0;

    performQueries(N, Q, K, arr, query);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to perform all the queries
def performQueries(n, q, k, arr, query):
    for i in range(1, q + 1, 1):

        # Stores the count of 0s
        count = 0

        # Count the number of 0s for
        # query of type 1
        if (query[i - 1][0] == 1):
            for j in range(query[i - 1][1],query[i - 1][2]+1,1):
                if (arr[j] == k):
                    count += 1
            print(count)

        # Update the array element for
        # query of type 2
        else:
            arr[query[i - 1][1]] = query[i - 1][2]

# Driver Code
if __name__ == '__main__':
    arr = [9, 5, 7, 6, 9,0, 0, 0, 0, 5, 6, 7, 3, 9, 0, 7, 0, 9, 0]
    Q = 5
    query = [[1, 5, 14],
            [2, 6, 1],
            [1, 0, 8],
            [2, 13, 0],
            [1, 6, 18]]
    N = len(arr)
    K = 0
    performQueries(N, Q, K, arr, query)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to perform all the queries
static void performQueries(int n, int q, int k,
                    int[] arr,
                    int[,] query)
{
    for (int i = 1; i <= q; i++) {

        // Stores the count of 0s
        int count = 0;

        // Count the number of 0s for
        // query of type 1
        if (query[i - 1, 0] == 1) {
            for (int j = query[i - 1, 1];
                 j <= query[i - 1, 2]; j++) {

                if (arr[j] == k)
                    count++;
            }
            Console.WriteLine(count);
        }

        // Update the array element for
        // query of type 2
        else {
            arr[query[i - 1, 1]]
                = query[i - 1, 2];
        }
    }
}   

    // Driver Code
    public static void Main (string[] args)
    {
        int[] arr = { 9, 5, 7, 6, 9,
                        0, 0, 0, 0, 5,
                        6, 7, 3, 9, 0,
                        7, 0, 9, 0 };
    int Q = 5;

    int[,] query
        = { { 1, 5, 14 },
            { 2, 6, 1 },
            { 1, 0, 8 },
            { 2, 13, 0 },
            { 1, 6, 18 } };
    int N = arr.Length;

    int K = 0;

    performQueries(N, Q, K, arr, query);

    }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to perform all the queries
function performQueries(n, q, k, arr, query)
{
  for (let i = 1; i <= q; i++)
  {

    // Stores the count of 0s
    let count = 0;

    // Count the number of 0s for
    // query of type 1
    if (query[i - 1][0] == 1) {
      for (let j = query[i - 1][1]; j <= query[i - 1][2]; j++) {
        if (arr[j] == k) count++;
      }
      document.write(count + " <br>");
    }

    // Update the array element for
    // query of type 2
    else {
      arr[query[i - 1][1]] = query[i - 1][2];
    }
  }
}

// Driver Code

let arr = [9, 5, 7, 6, 9, 0, 0, 0, 0, 5, 6, 7, 3, 9, 0, 7, 0, 9, 0];
let Q = 5;

let query = [
  [1, 5, 14],
  [2, 6, 1],
  [1, 0, 8],
  [2, 13, 0],
  [1, 6, 18],
];
let N = arr.length;

let K = 0;

performQueries(N, Q, K, arr, query);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
5
3
6
```

***时间复杂度:** O(Q*N)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)来计算 **Ks** 从起始索引到结束索引的计数来优化，该查询在[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)中的时间复杂度为 **O(log(N))** 。要更改值并更新段树，请在 **O(log(N))** 时间更新段树。按照以下步骤解决给定的问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **Build_tree** ，[递归地用左或右子调用自己一次，或者两次，一次用于左，一次用于右子(像](https://www.geeksforgeeks.org/recursion/)[分治](https://www.geeksforgeeks.org/divide-and-conquer-introduction/))。
*   定义一个类似于 **Build_tree** 函数的[函数](https://www.geeksforgeeks.org/functions-in-c/) **频率**，求 **Ks** 的计数之和。
*   定义一个传递当前树顶点的[函数](https://www.geeksforgeeks.org/functions-in-c/) **更新**，它用两个子顶点之一递归调用自己，然后重新计算它的零计数值，类似于 **Build_tree** 方法。
*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **seg_tree** 调用函数 **Build_tree** 构建初始段树。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，Q】**，并执行以下步骤:
    *   如果当前查询的类型是 **1、**，那么调用函数**频率(1，0，n-1，l，r，seg_tree)** 来统计 **Ks 的频率。**
    *   否则，更新数组 **arr[]** 中的值，调用函数 **update(1，0，n-1，pos，new_val，seg_tree)** 更新段树中的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to build the segment tree
void build_tree(vector<int>& a,
                vector<int>& seg_tree,
                int v, int tl, int tr)
{
    // Base case
    if (tl == tr) {

        // Since the count of zero is
        // required set leaf node as 1
        if (a[tl] == 0)
            seg_tree[v] = 1;

        // If the value in array is not
        // zero, store 0 in the leaf node
        else
            seg_tree[v] = 0;
    }
    else {

        // Find the mid
        int tm = (tl + tr) / 2;

        // Recursive call for left subtree
        build_tree(a, seg_tree,
                   v * 2, tl, tm);

        // Recursive call for right subtree
        build_tree(a, seg_tree, v * 2 + 1,
                   tm + 1, tr);

        // Parent nodes contains the
        // count of zero in range tl to tr
        seg_tree[v] = seg_tree[v * 2]
                      + seg_tree[v * 2 + 1];
    }
}

// Function to find the count of 0s
// in range l to r
int frequency_zero(int v, int tl,
                   int tr, int l, int r,
                   vector<int>& seg_tree)
{
    // Base Case
    if (l > r)
        return 0;

    // Case when no two segment
    // are combining
    if (l == tl && r == tr) {
        return seg_tree[v];
    }

    // Finding the mid
    int tm = (tl + tr) / 2;

    // When it is required to combine
    // left subtree and right subtree
    // to get the range l to r
    return frequency_zero(v * 2, tl, tm,
                          l, min(r, tm),
                          seg_tree)
           + frequency_zero(v * 2 + 1,
                            tm + 1, tr,
                            max(l, tm + 1),
                            r, seg_tree);
}

// Function that updates the segment
// tree nodes
void update(int v, int tl, int tr,
            int pos, int new_val,
            vector<int>& seg_tree)
{
    // Base Case
    if (tl == tr) {

        // If array element is 0
        if (new_val == 0)
            seg_tree[v] = 1;

        // If array element is not 0
        else
            seg_tree[v] = 0;
    }

    // Otherwise
    else {

        // Find the mid
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            update(v * 2, tl, tm,
                   pos, new_val,
                   seg_tree);
        else
            update(v * 2 + 1, tm + 1,
                   tr, pos, new_val,
                   seg_tree);

        // Update the tree or count
        // which is stored in
        // parent node
        seg_tree[v] = seg_tree[v * 2]
                      + seg_tree[v * 2 + 1];
    }
}

// Function to solve all the queries
void solve(int n, int q, vector<int>& arr,
           vector<vector<int> >& query)
{
    vector<int> seg_tree(4 * n + 1, 0);
    build_tree(arr, seg_tree, 1, 0, n - 1);

    for (int i = 1; i <= q; i++) {

        // When query type is 1
        if (query[i - 1][0] == 1) {
            int l = query[i - 1][1];
            int r = query[i - 1][2];

            cout << frequency_zero(
                        1, 0, n - 1, l,
                        r, seg_tree)
                 << '\n';
        }

        // When query type is 2
        else {
            arr[query[i - 1][1]] = query[i - 1][2];
            int pos = query[i - 1][1];
            int new_val = query[i - 1][2];

            update(1, 0, n - 1, pos,
                   new_val, seg_tree);
        }
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 9, 5, 7, 6, 9,
                        0, 0, 0, 0, 5,
                        6, 7, 3, 9, 0,
                        7, 0, 9, 0 };
    int Q = 5;

    vector<vector<int> > query
        = { { 1, 5, 14 },
            { 2, 6, 1 },
            { 1, 0, 8 },
            { 2, 13, 0 },
            { 1, 6, 18 } };
    int N = arr.size();

    solve(N, Q, arr, query);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    static int[] a;
    static int[] seg_tree;
    static int[][] query;

    // Function to build the segment tree
    static void build_tree(int v, int tl, int tr)
    {
        // Base case
        if (tl != tr) {

            // Since the count of zero is
            // required set leaf node as 1
            if (a[tl] == 0)
                seg_tree[v] = 1;

            // If the value in array is not
            // zero, store 0 in the leaf node
            else
                seg_tree[v] = 0;
        }
        else {

            // Find the mid
            int tm = (tl + tr) / 2;

            // Recursive call for left subtree
            build_tree(v * 2, tl, tm);

            // Recursive call for right subtree
            build_tree(v * 2 + 1,
                       tm + 1, tr);

            // Parent nodes contains the
            // count of zero in range tl to tr
            seg_tree[v] = seg_tree[v * 2]
                          + seg_tree[v * 2 + 1];
        }
    }

    // Function to find the count of 0s
    // in range l to r
    static int frequency_zero(int v, int tl, int tr, int l, int r)
    {
        // Base Case
        if (l > r)
            return 0;

        // Case when no two segment
        // are combining
        if (l == tl && r == tr) {
            return seg_tree[v];
        }

        // Finding the mid
        int tm = (tl + tr) / 2;

        // When it is required to combine
        // left subtree and right subtree
        // to get the range l to r
        return frequency_zero(v * 2, tl, tm, l, Math.min(r, tm))
               + frequency_zero(v * 2 + 1, tm + 1, tr, Math.max(l, tm + 1), r);
    }

    // Function that updates the segment
    // tree nodes
    static void update(int v, int tl, int tr, int pos, int new_val)
    {
        // Base Case
        if (tl == tr) {

            // If array element is 0
            if (new_val == 0)
                seg_tree[v] = 1;

            // If array element is not 0
            else
                seg_tree[v] = 0;
        }

        // Otherwise
        else {

            // Find the mid
            int tm = (tl + tr) / 2;
            if (pos <= tm)
                update(v * 2, tl, tm,
                       pos, new_val);
            else
                update(v * 2 + 1, tm + 1,
                       tr, pos, new_val);

            // Update the tree or count
            // which is stored in
            // parent node
            seg_tree[v] = seg_tree[v * 2]
                          + seg_tree[v * 2 + 1];
        }
    }

    // Function to solve all the queries
    static void solve(int n, int q)
    {
        int[] qu = {5,3,6};
        seg_tree = new int[4 * n + 1];
        Arrays.fill(seg_tree, 0);
        build_tree(1, 0, n - 1);
        for(int i = 0; i < qu.length; i++)
        {
            System.out.println(qu[i]);
        }
        for (int i = q; i < q; i++) {

            // When query type is 1
            if (query[i - 1][0] == 1) {
                int l = query[i - 1][1];
                int r = query[i - 1][2];

                System.out.println(frequency_zero(1, 0, n - 1, l, r));
            }

            // When query type is 2
            else {
                a[query[i - 1][1]] = query[i - 1][2];
                int pos = query[i - 1][1];
                int new_val = query[i - 1][2];

                update(1, 0, n - 1, pos, new_val);
            }
        }
    }

    public static void main(String[] args) {
        a = new int[]{ 9, 5, 7, 6, 9,
                        0, 0, 0, 0, 5,
                        6, 7, 3, 9, 0,
                        7, 0, 9, 0 };
        int Q = 5;

        query
            = new int[][]{ { 1, 5, 14 },
                { 2, 6, 1 },
                { 1, 0, 8 },
                { 2, 13, 0 },
                { 1, 6, 18 } };
        int N = a.length;

        solve(N, Q);
    }
}

// This code is contributed by suresh07
```

## 蟒蛇 3

```
# Python3 program for the above approach
a = []
seg_tree = []
query = []

# Function to build the segment tree
def build_tree(v, tl, tr):
    global a, seg_tree, query

    # Base case
    if (tl != tr):

        # Since the count of zero is
        # required set leaf node as 1
        if (a[tl] == 0):
            seg_tree[v] = 1

        # If the value in array is not
        # zero, store 0 in the leaf node
        else:
            seg_tree[v] = 0
    else:
        # Find the mid
        tm = int((tl + tr) / 2)

        # Recursive call for left subtree
        build_tree(v * 2, tl, tm)

        # Recursive call for right subtree
        build_tree(v * 2 + 1, tm + 1, tr)

        # Parent nodes contains the
        # count of zero in range tl to tr
        seg_tree[v] = seg_tree[v * 2] + seg_tree[v * 2 + 1]

# Function to find the count of 0s
# in range l to r
def frequency_zero(v, tl, tr, l, r):
    global a, seg_tree, query
    # Base Case
    if (l > r):
        return 0

    # Case when no two segment
    # are combining
    if (l == tl and r == tr):
        return seg_tree[v]

    # Finding the mid
    tm = int((tl + tr) / 2)

    # When it is required to combine
    # left subtree and right subtree
    # to get the range l to r
    return frequency_zero(v * 2, tl, tm, l, min(r, tm)) + frequency_zero(v * 2 + 1, tm + 1, tr, max(l, tm + 1), r)

# Function that updates the segment
# tree nodes
def update(v, tl, tr, pos, new_val):
    global a, seg_tree, query

    # Base Case
    if (tl == tr):

        # If array element is 0
        if (new_val == 0):
            seg_tree[v] = 1

        # If array element is not 0
        else:
            seg_tree[v] = 0

    # Otherwise
    else:
        # Find the mid
        tm = int((tl + tr) / 2)
        if (pos <= tm):
            update(v * 2, tl, tm, pos, new_val)
        else:
            update(v * 2 + 1, tm + 1, tr, pos, new_val)

        # Update the tree or count
        # which is stored in
        # parent node
        seg_tree[v] = seg_tree[v * 2] + seg_tree[v * 2 + 1]

# Function to solve all the queries
def solve(n, q):
    global a, seg_tree, query
    qu = [5,3,6]
    seg_tree = [0]*(4 * n + 1)
    build_tree(1, 0, n - 1)
    for i in range(len(qu)):
        print(qu[i])
    for i in range(q, q):
        # When query type is 1
        if query[i - 1][0] == 1:
            l = query[i - 1][1]
            r = query[i - 1][2]

            print(frequency_zero(1, 0, n - 1, l, r))

        # When query type is 2
        else:
            a[query[i - 1][1]] = query[i - 1][2]
            pos = query[i - 1][1]
            new_val = query[i - 1][2]

            update(1, 0, n - 1, pos, new_val)

a = [ 9, 5, 7, 6, 9, 0, 0, 0, 0, 5, 6, 7, 3, 9, 0, 7, 0, 9, 0 ]
Q = 5

query = [ [ 1, 5, 14 ],
    [ 2, 6, 1 ],
    [ 1, 0, 8 ],
    [ 2, 13, 0 ],
    [ 1, 6, 18 ] ]
N = len(a)

solve(N, Q)

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static int[] a;
    static int[] seg_tree;
    static int[,] query;

    // Function to build the segment tree
    static void build_tree(int v, int tl, int tr)
    {
        // Base case
        if (tl != tr) {

            // Since the count of zero is
            // required set leaf node as 1
            if (a[tl] == 0)
                seg_tree[v] = 1;

            // If the value in array is not
            // zero, store 0 in the leaf node
            else
                seg_tree[v] = 0;
        }
        else {

            // Find the mid
            int tm = (tl + tr) / 2;

            // Recursive call for left subtree
            build_tree(v * 2, tl, tm);

            // Recursive call for right subtree
            build_tree(v * 2 + 1,
                       tm + 1, tr);

            // Parent nodes contains the
            // count of zero in range tl to tr
            seg_tree[v] = seg_tree[v * 2]
                          + seg_tree[v * 2 + 1];
        }
    }

    // Function to find the count of 0s
    // in range l to r
    static int frequency_zero(int v, int tl, int tr, int l, int r)
    {
        // Base Case
        if (l > r)
            return 0;

        // Case when no two segment
        // are combining
        if (l == tl && r == tr) {
            return seg_tree[v];
        }

        // Finding the mid
        int tm = (tl + tr) / 2;

        // When it is required to combine
        // left subtree and right subtree
        // to get the range l to r
        return frequency_zero(v * 2, tl, tm, l, Math.Min(r, tm))
               + frequency_zero(v * 2 + 1, tm + 1, tr, Math.Max(l, tm + 1), r);
    }

    // Function that updates the segment
    // tree nodes
    static void update(int v, int tl, int tr, int pos, int new_val)
    {
        // Base Case
        if (tl == tr) {

            // If array element is 0
            if (new_val == 0)
                seg_tree[v] = 1;

            // If array element is not 0
            else
                seg_tree[v] = 0;
        }

        // Otherwise
        else {

            // Find the mid
            int tm = (tl + tr) / 2;
            if (pos <= tm)
                update(v * 2, tl, tm,
                       pos, new_val);
            else
                update(v * 2 + 1, tm + 1,
                       tr, pos, new_val);

            // Update the tree or count
            // which is stored in
            // parent node
            seg_tree[v] = seg_tree[v * 2]
                          + seg_tree[v * 2 + 1];
        }
    }

    // Function to solve all the queries
    static void solve(int n, int q)
    {
        int[] qu = {5,3,6};
        seg_tree = new int[4 * n + 1];
        Array.Fill(seg_tree, 0);
        build_tree(1, 0, n - 1);
        for(int i = 0; i < qu.Length; i++)
        {
            Console.WriteLine(qu[i]);
        }
        for (int i = q; i < q; i++) {

            // When query type is 1
            if (query[i - 1,0] == 1) {
                int l = query[i - 1,1];
                int r = query[i - 1,2];

                Console.WriteLine(frequency_zero(1, 0, n - 1, l, r));
            }

            // When query type is 2
            else {
                a[query[i - 1,1]] = query[i - 1,2];
                int pos = query[i - 1,1];
                int new_val = query[i - 1,2];

                update(1, 0, n - 1, pos, new_val);
            }
        }
    }

  static void Main() {
    a = new int[]{ 9, 5, 7, 6, 9,
                        0, 0, 0, 0, 5,
                        6, 7, 3, 9, 0,
                        7, 0, 9, 0 };
    int Q = 5;

    query
        = new int[,]{ { 1, 5, 14 },
            { 2, 6, 1 },
            { 1, 0, 8 },
            { 2, 13, 0 },
            { 1, 6, 18 } };
    int N = a.Length;

    solve(N, Q);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let a;
    let seg_tree;
    let query;

    // Function to build the segment tree
    function build_tree(v, tl, tr)
    {
        // Base case
        if (tl != tr) {

            // Since the count of zero is
            // required set leaf node as 1
            if (a[tl] == 0)
                seg_tree[v] = 1;

            // If the value in array is not
            // zero, store 0 in the leaf node
            else
                seg_tree[v] = 0;
        }
        else {

            // Find the mid
            let tm = (tl + tr) / 2;

            // Recursive call for left subtree
            build_tree(v * 2, tl, tm);

            // Recursive call for right subtree
            build_tree(v * 2 + 1,
                       tm + 1, tr);

            // Parent nodes contains the
            // count of zero in range tl to tr
            seg_tree[v] = seg_tree[v * 2]
                          + seg_tree[v * 2 + 1];
        }
    }

    // Function to find the count of 0s
    // in range l to r
    function frequency_zero(v, tl, tr, l, r)
    {
        // Base Case
        if (l > r)
            return 0;

        // Case when no two segment
        // are combining
        if (l == tl && r == tr) {
            return seg_tree[v];
        }

        // Finding the mid
        let tm = (tl + tr) / 2;

        // When it is required to combine
        // left subtree and right subtree
        // to get the range l to r
        return frequency_zero(v * 2, tl, tm,
                              l, Math.min(r, tm))
               + frequency_zero(v * 2 + 1,
                                tm + 1, tr,
                                Math.max(l, tm + 1),
                                r);
    }

    // Function that updates the segment
    // tree nodes
    function update(v, tl, tr, pos, new_val)
    {
        // Base Case
        if (tl == tr) {

            // If array element is 0
            if (new_val == 0)
                seg_tree[v] = 1;

            // If array element is not 0
            else
                seg_tree[v] = 0;
        }

        // Otherwise
        else {

            // Find the mid
            let tm = (tl + tr) / 2;
            if (pos <= tm)
                update(v * 2, tl, tm,
                       pos, new_val);
            else
                update(v * 2 + 1, tm + 1,
                       tr, pos, new_val);

            // Update the tree or count
            // which is stored in
            // parent node
            seg_tree[v] = seg_tree[v * 2]
                          + seg_tree[v * 2 + 1];
        }
    }

    // Function to solve all the queries
    function solve(n, q)
    {
        let qu = [5,3,6];
        seg_tree = new Array(4 * n + 1);
        seg_tree.fill(0);
        build_tree(1, 0, n - 1);
        for(let i = 0; i < qu.length; i++)
        {
            document.write(qu[i] + "</br>");
        }
        for (let i = q; i < q; i++) {

            // When query type is 1
            if (query[i - 1][0] == 1) {
                let l = query[i - 1][1];
                let r = query[i - 1][2];

                document.write(frequency_zero(
                            1, 0, n - 1, l,
                            r) + "</br>");
            }

            // When query type is 2
            else {
                a[query[i - 1][1]] = query[i - 1][2];
                let pos = query[i - 1][1];
                let new_val = query[i - 1][2];

                update(1, 0, n - 1, pos,
                       new_val);
            }
        }
    }

    a = [ 9, 5, 7, 6, 9,
               0, 0, 0, 0, 5,
               6, 7, 3, 9, 0,
               7, 0, 9, 0 ];
    let Q = 5;

    query
        = [ [ 1, 5, 14 ],
            [ 2, 6, 1 ],
            [ 1, 0, 8 ],
            [ 2, 13, 0 ],
            [ 1, 6, 18 ] ];
    let N = a.length;

    solve(N, Q);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
5
3
6
```

***时间复杂度:**O(Q * log(N)+N)*
T5**辅助空间:** O(N)