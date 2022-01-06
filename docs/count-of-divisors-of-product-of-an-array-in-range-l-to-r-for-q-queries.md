# 用于 Q 查询的 L 到 R 范围内的数组乘积的除数

> 原文:[https://www . geeksforgeeks . org/q 查询范围内的数组乘积因子数/](https://www.geeksforgeeks.org/count-of-divisors-of-product-of-an-array-in-range-l-to-r-for-q-queries/)

给定一个大小为 **N** 和 **Q** 的数组**【L，R】**查询，任务是在给定的范围内找到这个数组乘积的除数。
**注:**范围为 1 位。

**示例:**

> **输入:** arr[] = {4，1，9，12，5，3}，Q = {{1，3}，{3，5}}
> **输出:** 9
> 24
> 
> **输入:** arr[] = {5，2，3，1，4}，Q = {{2，4}，{1，5 } }
> T3】输出: 4
> 16

**蛮力:**

1.  对于每个查询，从 L 到 R 迭代数组，并计算给定范围内元素的乘积。
2.  计算该乘积的除数总数。

***时间复杂度:** Q * N * (log (N))*

**高效途径:**思路是用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)解决这个问题。

1.  由于限制，我们不能存储数组从 L 到 R 的乘积，所以我们可以将素数的幂存储在段树中。
2.  对于每个查询，我们根据查询合并树。

**从给定数组构建段树**

*   我们从片段 arr[0]开始。。。n-1]。
*   每次我们把当前线段分成两半，如果它还没有变成长度为 1 的线段。
*   然后在两半上调用相同的过程，对于每个这样的段，我们在相应的节点中存储素数的幂。
*   构建的段树的所有层都将被完全填充，除了最后一层。
*   此外，该树将是一个[完全二叉树](https://www.geeksforgeeks.org/check-whether-binary-tree-full-binary-tree-not/)，因为我们总是在每个级别将片段分成两半。
*   由于构造的树总是一棵有 n 片叶子的完全二叉树，因此会有 n-1 个内部节点。所以节点总数将为**2 * n–1**。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define MOD 1000000007

#define MAXN 1000001

// Array to store the precomputed prime numbers
int spf[MAXN];

// Function signatures
void merge(
    vector<pair<int, int> > tree[], int treeIndex);
void sieve();
vector<int> getFactorization(
    int x);
void buildTree(
    vector<pair<int, int> > tree[], int treeIndex,
    int start, int end, int arr[]);
int query(
    vector<pair<int, int> > tree[], int treeIndex,
    int start, int end,
    int left, int right);
vector<pair<int, int> > mergeUtil(
    vector<pair<int, int> > op1,
    vector<pair<int, int> > op2);
vector<pair<int, int> > queryUtil(
    vector<pair<int, int> > tree[], int treeIndex,
    int start, int end,
    int left, int right);

// Function to use Sieve to compute
// and store prime numbers
void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)
        spf[i] = i;

    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j < MAXN; j += i)
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to find the
// prime factors of a value
vector<int> getFactorization(int x)
{

    // Vectore to store the prime factors
    vector<int> ret;

    // For every prime factor of x,
    // push it to the vector
    while (x != 1) {

        ret.push_back(spf[x]);
        x = x / spf[x];
    }

    // Return the prime factors
    return ret;
}

// Recursive function to build segment tree
// by merging the power pf primes
void buildTree(vector<pair<int, int> > tree[],
               int treeIndex, int start,
               int end, int arr[])
{

    // Base case
    if (start == end) {

        int val = arr[start];
        vector<int> primeFac
            = getFactorization(val);

        for (auto it : primeFac) {
            int power = 0;
            while (val % it == 0) {
                val = val / it;
                power++;
            }

            // Storing powers of prime
            // in tree at treeIndex
            tree[treeIndex]
                .push_back({ it, power });
        }
        return;
    }

    int mid = (start + end) / 2;

    // Building the left tree
    buildTree(tree, 2 * treeIndex, start,
              mid, arr);

    // Building the right tree
    buildTree(tree, 2 * treeIndex + 1,
              mid + 1, end, arr);

    // Merges the right tree and left tree
    merge(tree, treeIndex);

    return;
}

// Function to merge the right
// and the left tree
void merge(vector<pair<int, int> > tree[],
           int treeIndex)
{
    int index1 = 0;
    int index2 = 0;
    int len1 = tree[2 * treeIndex].size();
    int len2 = tree[2 * treeIndex + 1].size();

    // Fill this array in such a way such that values
    // of prime remain sorted similar to mergesort
    while (index1 < len1 && index2 < len2) {

        // If both of the elements are same
        if (tree[2 * treeIndex][index1].first
            == tree[2 * treeIndex + 1][index2].first) {

            tree[treeIndex].push_back(
                { tree[2 * treeIndex][index1].first,
                  tree[2 * treeIndex][index1].second
                      + tree[2 * treeIndex + 1]
                            [index2]
                                .second });
            index1++;
            index2++;
        }

        // If the element on the left part
        // is greater than the right part
        else if (tree[2 * treeIndex][index1].first
                 > tree[2 * treeIndex + 1][index2].first) {

            tree[treeIndex].push_back(
                { tree[2 * treeIndex + 1][index2].first,
                  tree[2 * treeIndex + 1][index2].second });
            index2++;
        }

        // If the element on the left part
        // is less than the right part
        else {
            tree[treeIndex].push_back(
                { tree[2 * treeIndex][index1].first,
                  tree[2 * treeIndex][index1].second });
            index1++;
        }
    }

    // Insert the leftover elements
    // from the left part
    while (index1 < len1) {
        tree[treeIndex].push_back(
            { tree[2 * treeIndex][index1].first,
              tree[2 * treeIndex][index1].second });
        index1++;
    }

    // Insert the leftover elements
    // from the right part
    while (index2 < len2) {
        tree[treeIndex].push_back(
            { tree[2 * treeIndex + 1][index2].first,
              tree[2 * treeIndex + 1][index2].second });
        index2++;
    }
    return;
}

// Function similar to merge() method
// But here it takes two vectors and
// return a vector of power of primes
vector<pair<int, int> > mergeUtil(
    vector<pair<int, int> > op1,
    vector<pair<int, int> > op2)
{
    int index1 = 0;
    int index2 = 0;
    int len1 = op1.size();
    int len2 = op2.size();
    vector<pair<int, int> > res;

    while (index1 < len1 && index2 < len2) {

        if (op1[index1].first == op2[index2].first) {
            res.push_back({ op1[index1].first,
                            op1[index1].second
                                + op2[index2].second });
            index1++;
            index2++;
        }

        else if (op1[index1].first > op2[index2].first) {
            res.push_back({ op2[index2].first,
                            op2[index2].second });
            index2++;
        }
        else {
            res.push_back({ op1[index1].first,
                            op1[index1].second });
            index1++;
        }
    }
    while (index1 < len1) {
        res.push_back({ op1[index1].first,
                        op1[index1].second });
        index1++;
    }
    while (index2 < len2) {
        res.push_back({ op2[index2].first,
                        op2[index2].second });
        index2++;
    }
    return res;
}

// Function similar to query() method
// as in segment tree
// Here also the result is merged
vector<pair<int, int> > queryUtil(
    vector<pair<int, int> > tree[],
    int treeIndex, int start,
    int end, int left, int right)
{
    if (start > right || end < left) {
        tree[0].clear();
        return tree[0];
    }
    if (start >= left && end <= right) {
        return tree[treeIndex];
    }
    int mid = (start + end) / 2;

    vector<pair<int, int> > op1
        = queryUtil(tree, 2 * treeIndex,
                    start, mid,
                    left, right);
    vector<pair<int, int> > op2
        = queryUtil(tree, 2 * treeIndex + 1,
                    mid + 1, end,
                    left, right);

    return mergeUtil(op1, op2);
}

// Function to return the number of divisors
// of product of array from left to right
int query(vector<pair<int, int> > tree[],
          int treeIndex, int start,
          int end, int left, int right)
{
    vector<pair<int, int> > res
        = queryUtil(tree, treeIndex,
                    start, end,
                    left, right);

    int sum = 1;
    for (auto it : res) {
        sum *= (it.second + 1);
        sum %= MOD;
    }
    return sum;
}

// Function to solve queries
void solveQueries(
    int arr[], int len,
    int l, int r)
{

    // Calculate the size of segment tree
    int x = (int)(ceil(log2(len)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // first of pair is used to store the prime
    // second of pair is use to store its power
    vector<pair<int, int> > tree[max_size];

    // building the tree
    buildTree(tree, 1, 0, len - 1, arr);

    // Find the required number of divisors
    // of product of array from l to r
    cout << query(tree, 1, 0,
                  len - 1, l - 1, r - 1)
         << endl;
}

// Driver code
int main()
{

    // Precomputing the prime numbers using sieve
    sieve();

    int arr[] = { 5, 2, 3, 1, 4 };
    int len = sizeof(arr) / sizeof(arr[0]);
    int queries = 2;
    int Q[queries][2] = { { 2, 4 }, { 1, 5 } };

    // Solve the queries
    for (int i = 0; i < queries; i++) {
        solveQueries(arr, len, Q[i][0], Q[i][1]);
    }
    return 0;
}
```

## 蟒蛇 3

```
from typing import List, Tuple
from math import ceil, log2, pow
import sys

sys.setrecursionlimit(10000)

MOD = 1000000007

MAXN = 1000001

# Array to store the precomputed prime numbers
spf = [0 for _ in range(MAXN)]

# Function to use Sieve to compute
# and store prime numbers
def sieve() -> None:

    spf[1] = 1
    for i in range(2, MAXN):
        spf[i] = i

    for i in range(4, MAXN, 2):
        spf[i] = 2

    i = 3

    while i * i < MAXN:
        if (spf[i] == i):
            for j in range(i * i, MAXN, i):
                if (spf[j] == j):
                    spf[j] = i

        i += 1

# Function to find the
# prime factors of a value
def getFactorization(x: int) -> List[int]:

    # Vectore to store the prime factors
    ret = []

    # For every prime factor of x,
    # push it to the vector
    while (x != 1):

        ret.append(spf[x])
        x = x // spf[x]

    # Return the prime factors
    return ret

# Recursive function to build segment tree
# by merging the power pf primes
def buildTree(tree: List[List[Tuple[int]]], treeIndex: int,
              start: int, end: int, arr: List[int]) -> None:

    # Base case
    if (start == end):
        val = arr[start]
        primeFac = getFactorization(val)

        for it in primeFac:
            power = 0

            while (val % it == 0):
                val = val // it
                power += 1

            # Storing powers of prime
            # in tree at treeIndex
            tree[treeIndex].append((it, power))

        return

    mid = (start + end) // 2

    # Building the left tree
    buildTree(tree, 2 * treeIndex, start, mid, arr)

    # Building the right tree
    buildTree(tree, 2 * treeIndex + 1, mid + 1, end, arr)

    # Merges the right tree and left tree
    merge(tree, treeIndex)

    return

# Function to merge the right
# and the left tree
def merge(tree: List[List[Tuple[int]]], treeIndex: int) -> None:

    index1 = 0
    index2 = 0
    len1 = len(tree[2 * treeIndex])
    len2 = len(tree[2 * treeIndex + 1])

    # Fill this array in such a way such that values
    # of prime remain sorted similar to mergesort
    while (index1 < len1 and index2 < len2):

        # If both of the elements are same
        if (tree[2 * treeIndex][index1][0] ==
            tree[2 * treeIndex + 1][index2][0]):
            tree[treeIndex].append((tree[2 * treeIndex][index1][0],
                                    tree[2 * treeIndex][index1][1] +
                                    tree[2 * treeIndex + 1][index2][1]))
            index1 += 1
            index2 += 1

        # If the element on the left part
        # is greater than the right part
        elif (tree[2 * treeIndex][index1][0] >
              tree[2 * treeIndex + 1][index2][0]):

            tree[treeIndex].append((tree[2 * treeIndex + 1][index2][0],
                                    tree[2 * treeIndex + 1][index2][1]))
            index2 += 1

        # If the element on the left part
        # is less than the right part
        else:
            tree[treeIndex].append((tree[2 * treeIndex][index1][0],
                                    tree[2 * treeIndex][index1][1]))
            index1 += 1

    # Insert the leftover elements
    # from the left part
    while (index1 < len1):
        tree[treeIndex].append(
            (tree[2 * treeIndex][index1][0],
             tree[2 * treeIndex][index1][1]))
        index1 += 1

    # Insert the leftover elements
    # from the right part
    while (index2 < len2):
        tree[treeIndex].append((tree[2 * treeIndex + 1][index2][0],
                                tree[2 * treeIndex + 1][index2][1]))
        index2 += 1

    return

# Function similar to merge() method
# But here it takes two vectors and
# return a vector of power of primes
def mergeUtil(op1: List[Tuple[int]],
              op2: List[Tuple[int]]) -> List[Tuple[int]]:

    index1 = 0
    index2 = 0
    len1 = len(op1)
    len2 = len(op2)
    res = []

    while (index1 < len1 and index2 < len2):
        if (op1[index1][0] == op2[index2][0]):
            res.append((op1[index1][0],
                       (op1[index1][1] +
                        op2[index2][1])))
            index1 += 1
            index2 += 1

        elif (op1[index1][0] > op2[index2][0]):
            res.append((op2[index2][0], op2[index2][1]))
            index2 += 1

        else:
            res.append((op1[index1][0], op1[index1][1]))
            index1 += 1

    while (index1 < len1):
        res.append((op1[index1][0], op1[index1][1]))
        index1 += 1

    while (index2 < len2):
        res.append((op2[index2][0], op2[index2][1]))
        index2 += 1

    return res

# Function similar to query() method
# as in segment tree
# Here also the result is merged
def queryUtil(tree: List[List[Tuple[int]]], treeIndex: int,
              start: int,end: int, left: int,
              right: int) -> List[Tuple[int]]:

    if (start > right or end < left):
        tree[0].clear()
        return tree[0]

    if (start >= left and end <= right):
        return tree[treeIndex]

    mid = (start + end) // 2

    op1 = queryUtil(tree, 2 * treeIndex, start,
                    mid, left, right)
    op2 = queryUtil(tree, 2 * treeIndex + 1, mid + 1,
                    end, left, right)

    return mergeUtil(op1, op2)

# Function to return the number of divisors
# of product of array from left to right
def query(tree: List[List[Tuple[int]]], treeIndex: int,
          start: int, end: int, left: int, right: int) -> int:

    res = queryUtil(tree, treeIndex, start, end, left, right)

    sum = 1
    for it in res:
        sum *= (it[1] + 1)
        sum %= MOD

    return sum

# Function to solve queries
def solveQueries(arr: List[int], length: int,
                 l: int, r: int) -> None:

    # Calculate the size of segment tree
    x = int(ceil(log2(length)))

    # Maximum size of segment tree
    max_size = 2 * int(pow(2, x)) - 1

    # First of pair is used to store the prime
    # second of pair is use to store its power
    tree = [[] for _ in range(max_size)]

    # building the tree
    buildTree(tree, 1, 0, length - 1, arr)

    # Find the required number of divisors
    # of product of array from l to r
    print(query(tree, 1, 0, length - 1, l - 1, r - 1))

# Driver code
if __name__ == "__main__":

    # Precomputing the prime numbers using sieve
    sieve()

    arr = [ 5, 2, 3, 1, 4 ]
    length = len(arr)
    queries = 2
    Q = [ [ 2, 4 ], [ 1, 5 ] ]

    # Solve the queries
    for i in range(queries):
        solveQueries(arr, length, Q[i][0], Q[i][1])

# This code is contributed by sanjeev2552
```

**Output:** 

```
4
16
```

***时间复杂度:** Q * (log (N))*