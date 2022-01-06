# Q 查询后数组中形成的所有段中的最大段和

> 原文:[https://www . geeksforgeeks . org/q 查询后数组中所有段的最大段数总和/](https://www.geeksforgeeks.org/maximum-sum-of-segments-among-all-segments-formed-in-array-after-q-queries/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】***(基于 1 的索引)*和**查询【】**由 **N** 个整数和**个查询【】**组成，包含第一个 **N** [个自然数](https://www.geeksforgeeks.org/natural-numbers/)的[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，任务是对数组执行查询，并在形成的所有段中找到最大的段和，使得在每个查询中**查询【I】**

**示例:**

> **输入:** arr[] = {1，3，2，5}，查询[] = {3，4，1，2}
> **输出:** 5 4 3 0
> **解释:**
> 执行以下查询:
> 
> *   **查询 1:** 删除索引 3 处的元素，将当前数组拆分为{1，3}，{5}。所有段的最大和是 5。
> *   **查询 2:** 删除索引 4 处的元素，将当前数组拆分为{1，3} {}。所有段的最大和是 4。
> *   **查询 3:** 删除索引 1 处的元素，将当前数组拆分为{1}、{}。所有段的最大和为 1。
> *   **查询 4:** 删除索引 2 处的元素，将当前数组拆分为{}、{}。所有段的最大和为 0。
> 
> **输入:** arr[] = {1，2，3，4，5}，查询[] = {4，2，3，5，1 }
> T3】输出 : 6 5 5 1 0

**方法:**给定的问题可以通过使用[不相交集合并数据结构](https://www.geeksforgeeks.org/disjoint-set-data-structures/)来解决。其思想是将所有查询存储在一个数组中，最初，所有元素都在不同的集合中，以相反的顺序处理查询，对于每个查询，使用[查找操作](https://www.geeksforgeeks.org/union-find/)对当前元素及其左侧和右侧元素进行[联合操作](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)，并行跟踪最大元素，然后将其存储在一个数组中，然后以相反的顺序打印数组元素。按照以下步骤解决问题:

*   [初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **父(N + 1)****秩(N + 1，0)****集合和(N+1，0)** 和 **currMax** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N+1】**，并将**父项【I】**的值设置为 **-1** ，**设置 sum【I】**为**arr【I–1】**。
*   [将值 **0** 推送到向量 **currMax[]**](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) 中，因为在最后一次查询之后，答案将是 **0** 。
*   使用变量 **i** 以相反的顺序迭代范围**【N–1，0】**，并执行以下步骤:
    *   如果**父【查询【**I**】**为 **-1** ，则设置为**查询【I】**。
    *   如果**查询【I】–1>= 0&&父【查询【I】–1】！= -1** ，然后调用函数操作 **union(父，rank，setSum，查询【** I **】，查询【I】-1)**。
    *   如果**查询【I】+1<= N&&父【查询【I】+1】！= -1，**然后调用函数操作 **union(父，rank，setSum，查询【** I **】，查询【I】+1)**。
    *   将 **maxAns** 的值设置为 **maxAns** 或 **setSum【查询【**I**】**的最大值，并将 **maxAns** 的值推入向量**curr max【】**。
*   [反转向量 **currMax[]**](https://www.geeksforgeeks.org/stdreverse-in-c/) 并将其值打印为答案。

下面是上述算法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the maximum integer of the sets
// for each query
int maxAns = INT_MIN;

// Function to perform the find operation
// of disjoint set union
int Find(vector<int>& parent, int a)
{
    return parent[a]
           = (parent[a] == a)
                 ? a
                 : (Find(
                       parent, parent[a]));
}

// Function to perform the Union operation
// of disjoint set union
void Union(vector<int>& parent, vector<int>& rank,
           vector<int>& setSum, int a, int b)
{
    // Find the parent of a and b
    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    if (rank[a] > rank[b])
        rank[a]++;

    if (rank[b] > rank[a])
        swap(a, b);

    // Update the parent
    parent[b] = a;

    // Update the sum of set a
    setSum[a] += setSum[b];
}

// Function to find the maximum element
// from the sets after each operation
void maxValues(vector<int> arr,
               vector<int> queries, int N)
{

    // Stores the parent elements of
    // the sets
    vector<int> parent(N + 1);

    // Stores the rank of the sets
    vector<int> rank(N + 1, 0);

    // Stores the sum of the sets
    vector<int> setSum(N + 1, 0);

    // Stores the maximum element for
    // each query
    vector<int> currMax;

    for (int i = 1; i < N + 1; i++) {

        // Initially set is empty
        parent[i] = -1;

        // Update the sum as the
        // current element
        setSum[i] = arr[i - 1];
    }

    // After the last query set will
    // be empty and sum will be 0
    currMax.push_back(0);

    for (int i = N - 1; i > 0; i--) {

        // Check if the current element
        // is not in any set then make
        // parent as current element
        // of the queries
        if (parent[queries[i]] == -1) {

            parent[queries[i]] = queries[i];
        }

        // Check left side of the queries[i]
        // is not added in any set
        if (queries[i] - 1 >= 0
            && parent[queries[i] - 1] != -1) {

            // Add the queries[i] and the
            // queries[i]-1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] - 1);
        }

        // Check right side of the queries[i]
        // is not added in any set
        if (queries[i] + 1 <= N
            && parent[queries[i] + 1] != -1) {

            // Add queries[i] and the
            // queries[i]+1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] + 1);
        }

        // Update the maxAns
        maxAns = max(setSum[queries[i]],
                     maxAns);

        // Push maxAns to the currMax
        currMax.push_back(maxAns);
    }

    // Print currMax values in the
    // reverse order
    for (int i = currMax.size() - 1;
         i >= 0; i--) {
        cout << currMax[i] << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 3, 2, 5 };
    vector<int> queries = { 3, 4, 1, 2 };
    int N = arr.size();

    maxValues(arr, queries, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Stores the maximum integer of the sets
// for each query
static int maxAns = Integer.MIN_VALUE;

// Function to perform the find operation
// of disjoint set union
static int Find(int [] parent, int a)
{
    return parent[a]
           = (parent[a] == a)
                 ? a
                 : (Find(
                       parent, parent[a]));
}

// Function to perform the Union operation
// of disjoint set union
static void Union(int [] parent, int [] rank,
           int [] setSum, int a, int b)
{
    // Find the parent of a and b
    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    if (rank[a] > rank[b])
        rank[a]++;

    if (rank[b] > rank[a]) {
        int x = a;
        a = b;
        b = x;
    }

    // Update the parent
    parent[b] = a;

    // Update the sum of set a
    setSum[a] += setSum[b];
}

// Function to find the maximum element
// from the sets after each operation
static void maxValues(int [] arr,
               int [] queries, int N)
{

    // Stores the parent elements of
    // the sets
    int [] parent = new int[N + 1];

    // Stores the rank of the sets
    int [] rank = new int[N + 1];

    // Stores the sum of the sets
    int [] setSum = new int[N + 1];

    // Stores the maximum element for
    // each query
    Vector<Integer> currMax = new Vector<Integer>();

    for (int i = 1; i < N + 1; i++) {

        // Initially set is empty
        parent[i] = -1;

        // Update the sum as the
        // current element
        setSum[i] = arr[i - 1];
    }

    // After the last query set will
    // be empty and sum will be 0
    currMax.add(0);

    for (int i = N - 1; i > 0; i--) {

        // Check if the current element
        // is not in any set then make
        // parent as current element
        // of the queries
        if (parent[queries[i]] == -1) {

            parent[queries[i]] = queries[i];
        }

        // Check left side of the queries[i]
        // is not added in any set
        if (queries[i] - 1 >= 0
            && parent[queries[i] - 1] != -1) {

            // Add the queries[i] and the
            // queries[i]-1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] - 1);
        }

        // Check right side of the queries[i]
        // is not added in any set
        if (queries[i] + 1 <= N
            && parent[queries[i] + 1] != -1) {

            // Add queries[i] and the
            // queries[i]+1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] + 1);
        }

        // Update the maxAns
        maxAns = Math.max(setSum[queries[i]],
                     maxAns);

        // Push maxAns to the currMax
        currMax.add(maxAns);
    }

    // Print currMax values in the
    // reverse order
    for (int i = currMax.size() - 1;
         i >= 0; i--) {
        System.out.print(currMax.get(i)+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int [] arr = { 1, 3, 2, 5 };
    int [] queries = { 3, 4, 1, 2 };
    int N = arr.length;

    maxValues(arr, queries, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Stores the maximum integer of the sets
# for each query
maxAns = -sys.maxsize - 1

# Function to perform the find operation
# of disjoint set union
def Find(parent, a):

    if(parent[a] == a):
        return a
    return Find(parent, parent[a])

# Function to perform the Union operation
# of disjoint set union
def Union(parent,  rank,
          setSum, a, b):
    # Find the parent of a and b
    a = Find(parent, a)
    b = Find(parent, b)

    if (a == b):
        return

    if (rank[a] > rank[b]):
        rank[a] += 1

    if (rank[b] > rank[a]):
        swap(a, b)

    # Update the parent
    parent[b] = a

    # Update the sum of set a
    setSum[a] += setSum[b]

# Function to find the maximum element
# from the sets after each operation
def maxValues(arr,
              queries, N):

    global maxAns
    # Stores the parent elements of

    # the sets
    parent = [0]*(N + 1)

    # Stores the rank of the sets
    rank = [0]*(N + 1)

    # Stores the sum of the sets
    setSum = [0]*(N + 1)

    # Stores the maximum element for
    # each query
    currMax = []

    for i in range(1, N + 1):

        # Initially set is empty
        parent[i] = -1

        # Update the sum as the
        # current element
        setSum[i] = arr[i - 1]

    # After the last query set will
    # be empty and sum will be 0
    currMax.append(0)

    for i in range(N - 1, 0, -1):

        # Check if the current element
        # is not in any set then make
        # parent as current element
        # of the queries
        if (parent[queries[i]] == -1):

            parent[queries[i]] = queries[i]

        # Check left side of the queries[i]
        # is not added in any set
        if (queries[i] - 1 >= 0
                and parent[queries[i] - 1] != -1):

            # Add the queries[i] and the
            # queries[i]-1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] - 1)

        # Check right side of the queries[i]
        # is not added in any set
        if (queries[i] + 1 <= N
                and parent[queries[i] + 1] != -1):

            # Add queries[i] and the
            # queries[i]+1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] + 1)

        # Update the maxAns
        maxAns = max(setSum[queries[i]], maxAns)

        # Push maxAns to the currMax
        currMax.append(maxAns)

    # Print currMax values in the
    # reverse order
    for i in range(len(currMax) - 1, -1, -1):
        print(currMax[i], end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 2, 5]
    queries = [3, 4, 1, 2]
    N = len(arr)

    maxValues(arr, queries, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Stores the maximum integer of the sets
// for each query
static int maxAns = int.MinValue;

// Function to perform the find operation
// of disjoint set union
static int Find(int [] parent, int a)
{
    return parent[a]
           = (parent[a] == a)
                 ? a
                 : (Find(
                       parent, parent[a]));
}

// Function to perform the Union operation
// of disjoint set union
static void Union(int [] parent, int [] rank,
           int [] setSum, int a, int b)
{
    // Find the parent of a and b
    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    if (rank[a] > rank[b])
        rank[a]++;

    if (rank[b] > rank[a]) {
        int x = a;
        a = b;
        b = x;
    }

    // Update the parent
    parent[b] = a;

    // Update the sum of set a
    setSum[a] += setSum[b];
}

// Function to find the maximum element
// from the sets after each operation
static void maxValues(int [] arr,
               int [] queries, int N)
{

    // Stores the parent elements of
    // the sets
    int [] parent = new int[N + 1];

    // Stores the rank of the sets
    int [] rank = new int[N + 1];

    // Stores the sum of the sets
    int [] setSum = new int[N + 1];

    // Stores the maximum element for
    // each query
    List<int> currMax = new List<int>();

    for (int i = 1; i < N + 1; i++) {

        // Initially set is empty
        parent[i] = -1;

        // Update the sum as the
        // current element
        setSum[i] = arr[i - 1];
    }

    // After the last query set will
    // be empty and sum will be 0
    currMax.Add(0);

    for (int i = N - 1; i > 0; i--) {

        // Check if the current element
        // is not in any set then make
        // parent as current element
        // of the queries
        if (parent[queries[i]] == -1) {

            parent[queries[i]] = queries[i];
        }

        // Check left side of the queries[i]
        // is not added in any set
        if (queries[i] - 1 >= 0
            && parent[queries[i] - 1] != -1) {

            // Add the queries[i] and the
            // queries[i]-1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] - 1);
        }

        // Check right side of the queries[i]
        // is not added in any set
        if (queries[i] + 1 <= N
            && parent[queries[i] + 1] != -1) {

            // Add queries[i] and the
            // queries[i]+1 in one set
            Union(parent, rank, setSum,
                  queries[i],
                  queries[i] + 1);
        }

        // Update the maxAns
        maxAns = Math.Max(setSum[queries[i]],
                     maxAns);

        // Push maxAns to the currMax
        currMax.Add(maxAns);
    }

    // Print currMax values in the
    // reverse order
    for (int i = currMax.Count - 1;
         i >= 0; i--) {
        Console.Write(currMax[i]+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int [] arr = { 1, 3, 2, 5 };
    int [] queries = { 3, 4, 1, 2 };
    int N = arr.Length;

    maxValues(arr, queries, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Stores the maximum integer of the sets
    // for each query
    let maxAns = -2147483648;

    // Function to perform the find operation
    // of disjoint set union
    const Find = (parent, a) => {
        return parent[a]
            = (parent[a] == a)
                ? a
                : (Find(
                    parent, parent[a]));
    }

    // Function to perform the Union operation
    // of disjoint set union
    const Union = (parent, rank, setSum, a, b) => {

        // Find the parent of a and b
        a = Find(parent, a);
        b = Find(parent, b);

        if (a == b)
            return;

        if (rank[a] > rank[b])
            rank[a]++;

        if (rank[b] > rank[a])
            swap(a, b);

        // Update the parent
        parent[b] = a;

        // Update the sum of set a
        setSum[a] += setSum[b];
    }

    // Function to find the maximum element
    // from the sets after each operation
    const maxValues = (arr, queries, N) => {

        // Stores the parent elements of
        // the sets
        let parent = new Array(N + 1).fill(0);

        // Stores the rank of the sets
        let rank = new Array(N + 1).fill(0);

        // Stores the sum of the sets
        let setSum = new Array(N + 1).fill(0);

        // Stores the maximum element for
        // each query
        let currMax = [];

        for (let i = 1; i < N + 1; i++) {

            // Initially set is empty
            parent[i] = -1;

            // Update the sum as the
            // current element
            setSum[i] = arr[i - 1];
        }

        // After the last query set will
        // be empty and sum will be 0
        currMax.push(0);

        for (let i = N - 1; i > 0; i--) {

            // Check if the current element
            // is not in any set then make
            // parent as current element
            // of the queries
            if (parent[queries[i]] == -1) {

                parent[queries[i]] = queries[i];
            }

            // Check left side of the queries[i]
            // is not added in any set
            if (queries[i] - 1 >= 0
                && parent[queries[i] - 1] != -1) {

                // Add the queries[i] and the
                // queries[i]-1 in one set
                Union(parent, rank, setSum,
                    queries[i],
                    queries[i] - 1);
            }

            // Check right side of the queries[i]
            // is not added in any set
            if (queries[i] + 1 <= N
                && parent[queries[i] + 1] != -1) {

                // Add queries[i] and the
                // queries[i]+1 in one set
                Union(parent, rank, setSum,
                    queries[i],
                    queries[i] + 1);
            }

            // Update the maxAns
            maxAns = Math.max(setSum[queries[i]], maxAns);

            // Push maxAns to the currMax
            currMax.push(maxAns);
        }

        // Print currMax values in the
        // reverse order
        for (let i = currMax.length - 1; i >= 0; i--) {
            document.write(`${currMax[i]} `);
        }
    }

    // Driver Code
    let arr = [1, 3, 2, 5];
    let queries = [3, 4, 1, 2];
    let N = arr.length;

    maxValues(arr, queries, N);

    // This code is contributed by rakeshsahni
</script>
```

**Output:** 

```
5 4 3 0
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*