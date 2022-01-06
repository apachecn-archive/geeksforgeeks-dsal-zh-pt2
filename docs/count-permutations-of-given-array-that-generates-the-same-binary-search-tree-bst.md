# 计算生成相同二叉查找树(BST)的给定数组的排列数

> 原文:[https://www . geesforgeks . org/count-给定数组的排列-生成相同的二进制搜索树-bst/](https://www.geeksforgeeks.org/count-permutations-of-given-array-that-generates-the-same-binary-search-tree-bst/)

给定一个由范围**【1，N】**中的元素组成的大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr[]**，该数组表示元素插入到[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/)中的顺序，任务是计算重新排列给定数组的方式数，以获得相同的 [BST](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) 。

**示例:**

> **输入:** arr[ ] ={3，4，5，1，2}
> **输出:** 6
> **解释:**
> 表示同一个 BST 的数组排列为:{{3，4，5，1，2}，{3，1，2，4，5}，{3，1，4，2，5}，{3，1，4，5，2}，{3，2，5，2}，{3，4，5，2}，{3，1，2，5}，{3，4，1 因此，输出为 6。
> 
> **输入:** arr[ ] ={2，1，6，5，4，3 }
> T3】输出: 5

**做法:**思路是先固定根节点，然后递归统计重新排列左子树元素和右子树元素的方式个数，使得左子树和右子树元素内的相对顺序必须相同。这里是循环关系:

> count way(arr)= count way(左)* countWays(右)*组合(N，X)。
> **左:**包含左子树中的所有元素(小于根的元素)
> **右:**包含右子树中的所有元素(大于根的元素)
> **N**= arr 中的元素总数[]
> **X** =左子树中的元素总数。

按照以下步骤解决问题:

1.  固定 BST 的根节点，存储左子树的元素(小于 arr[0]的元素)，说 **ctLeft[]** ，存储右子树的元素(大于 arr[0]的元素)，说 **ctRight[]。**
2.  为了生成相同的 BST，保持左子树和右子树元素的相对顺序。
3.  使用上述递归关系计算重新排列数组以生成 BST 的方式数。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to precompute the
// factorial of 1 to N
void calculateFact(int fact[], int N)
{
    fact[0] = 1;
    for (long long int i = 1; i < N; i++) {
        fact[i] = fact[i - 1] * i;
    }
}

// Function to get the value of nCr
int nCr(int fact[], int N, int R)
{
    if (R > N)
        return 0;

    // nCr= fact(n)/(fact(r)*fact(n-r))
    int res = fact[N] / fact[R];
    res /= fact[N - R];

    return res;
}

// Function to count the number of ways
// to rearrange the array to obtain same BST
int countWays(vector<int>& arr, int fact[])
{
    // Store the size of the array
    int N = arr.size();

    // Base case
    if (N <= 2) {
        return 1;
    }

    // Store the elements of the
    // left subtree of BST
    vector<int> leftSubTree;

    // Store the elements of the
    // right subtree of BST
    vector<int> rightSubTree;

    // Store the root node
    int root = arr[0];

    for (int i = 1; i < N; i++) {

        // Push all the elements
        // of the left subtree
        if (arr[i] < root) {
            leftSubTree.push_back(
                arr[i]);
        }

        // Push all the elements
        // of the right subtree
        else {
            rightSubTree.push_back(
                arr[i]);
        }
    }

    // Store the size of leftSubTree
    int N1 = leftSubTree.size();

    // Store the size of rightSubTree
    int N2 = rightSubTree.size();

    // Recurrence relation
    int countLeft
        = countWays(leftSubTree,
                    fact);
    int countRight
        = countWays(rightSubTree,
                    fact);

    return nCr(fact, N - 1, N1)
           * countLeft * countRight;
}

// Driver Code
int main()
{

    vector<int> arr;
    arr = { 3, 4, 5, 1, 2 };

    // Store the size of arr
    int N = arr.size();

    // Store the factorial up to N
    int fact[N];

    // Precompute the factorial up to N
    calculateFact(fact, N);

    cout << countWays(arr, fact);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to precompute the
// factorial of 1 to N
static void calculateFact(int fact[], int N)
{
    fact[0] = 1;
    for(int i = 1; i < N; i++)
    {
        fact[i] = fact[i - 1] * i;
    }
}

// Function to get the value of nCr
static int nCr(int fact[], int N, int R)
{
    if (R > N)
        return 0;

    // nCr= fact(n)/(fact(r)*fact(n-r))
    int res = fact[N] / fact[R];
    res /= fact[N - R];

    return res;
}

// Function to count the number of ways
// to rearrange the array to obtain same BST
static int countWays(Vector<Integer> arr,
                     int fact[])
{

    // Store the size of the array
    int N = arr.size();

    // Base case
    if (N <= 2) 
    {
        return 1;
    }

    // Store the elements of the
    // left subtree of BST
    Vector<Integer> leftSubTree = new Vector<Integer>();

    // Store the elements of the
    // right subtree of BST
    Vector<Integer> rightSubTree = new Vector<Integer>();

    // Store the root node
    int root = arr.get(0);

    for(int i = 1; i < N; i++)
    {

        // Push all the elements
        // of the left subtree
        if (arr.get(i) < root)
        {
            leftSubTree.add(arr.get(i));
        }

        // Push all the elements
        // of the right subtree
        else 
        {
            rightSubTree.add(arr.get(i));
        }
    }

    // Store the size of leftSubTree
    int N1 = leftSubTree.size();

    // Store the size of rightSubTree
    int N2 = rightSubTree.size();

    // Recurrence relation
    int countLeft = countWays(leftSubTree,
                              fact);
    int countRight = countWays(rightSubTree,
                               fact);

    return nCr(fact, N - 1, N1) * 
             countLeft * countRight;
}

// Driver Code
public static void main(String[] args)
{
    int []a = { 3, 4, 5, 1, 2 };

    Vector<Integer> arr = new Vector<Integer>();
    for(int i : a)
        arr.add(i);

    // Store the size of arr
    int N = a.length;

    // Store the factorial up to N
    int []fact = new int[N];

    // Precompute the factorial up to N
    calculateFact(fact, N);

    System.out.print(countWays(arr, fact));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to precompute the
# factorial of 1 to N
def calculateFact(fact: list, N: int) -> None:

    fact[0] = 1
    for i in range(1, N):
        fact[i] = fact[i - 1] * i

# Function to get the value of nCr
def nCr(fact: list, N: int, R: int) -> int:

    if (R > N):
        return 0

    # nCr= fact(n)/(fact(r)*fact(n-r))
    res = fact[N] // fact[R]
    res //= fact[N - R]

    return res

# Function to count the number of ways
# to rearrange the array to obtain same BST
def countWays(arr: list, fact: list) -> int:

    # Store the size of the array
    N = len(arr)

    # Base case
    if (N <= 2):
        return 1

    # Store the elements of the
    # left subtree of BST
    leftSubTree = []

    # Store the elements of the
    # right subtree of BST
    rightSubTree = []

    # Store the root node
    root = arr[0]

    for i in range(1, N):

        # Push all the elements
        # of the left subtree
        if (arr[i] < root):
            leftSubTree.append(arr[i])

        # Push all the elements
        # of the right subtree
        else:
            rightSubTree.append(arr[i])

    # Store the size of leftSubTree
    N1 = len(leftSubTree)

    # Store the size of rightSubTree
    N2 = len(rightSubTree)

    # Recurrence relation
    countLeft = countWays(leftSubTree, fact)
    countRight = countWays(rightSubTree, fact)

    return (nCr(fact, N - 1, N1) * 
            countLeft * countRight)

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 4, 5, 1, 2 ]

    # Store the size of arr
    N = len(arr)

    # Store the factorial up to N
    fact = [0] * N

    # Precompute the factorial up to N
    calculateFact(fact, N)

    print(countWays(arr, fact))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to precompute the
// factorial of 1 to N
static void calculateFact(int []fact, int N)
{
    fact[0] = 1;
    for(int i = 1; i < N; i++)
    {
        fact[i] = fact[i - 1] * i;
    }
}

// Function to get the value of nCr
static int nCr(int []fact, int N, int R)
{
    if (R > N)
        return 0;

    // nCr= fact(n)/(fact(r)*fact(n-r))
    int res = fact[N] / fact[R];
    res /= fact[N - R];

    return res;
}

// Function to count the number of ways
// to rearrange the array to obtain same BST
static int countWays(List<int> arr,
                     int []fact)
{

    // Store the size of the array
    int N = arr.Count;

    // Base case
    if (N <= 2) 
    {
        return 1;
    }

    // Store the elements of the
    // left subtree of BST
    List<int> leftSubTree = new List<int>();

    // Store the elements of the
    // right subtree of BST
    List<int> rightSubTree = new List<int>();

    // Store the root node
    int root = arr[0];

    for(int i = 1; i < N; i++)
    {

        // Push all the elements
        // of the left subtree
        if (arr[i] < root)
        {
            leftSubTree.Add(arr[i]);
        }

        // Push all the elements
        // of the right subtree
        else
        {
            rightSubTree.Add(arr[i]);
        }
    }

    // Store the size of leftSubTree
    int N1 = leftSubTree.Count;

    // Store the size of rightSubTree
    int N2 = rightSubTree.Count;

    // Recurrence relation
    int countLeft = countWays(leftSubTree,
                              fact);
    int countRight = countWays(rightSubTree,
                               fact);

    return nCr(fact, N - 1, N1) * 
             countLeft * countRight;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 3, 4, 5, 1, 2 };

    List<int> arr = new List<int>();
    foreach(int i in a)
        arr.Add(i);

    // Store the size of arr
    int N = a.Length;

    // Store the factorial up to N
    int []fact = new int[N];

    // Precompute the factorial up to N
    calculateFact(fact, N);

    Console.Write(countWays(arr, fact));
}
}

// This code is contributed by Amit Katiyar 
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to precompute the
// factorial of 1 to N
function calculateFact(fact, N)
{
    fact[0] = 1;
    for (var i = 1; i < N; i++) {
        fact[i] = fact[i - 1] * i;
    }
}

// Function to get the value of nCr
function nCr(fact, N, R)
{
    if (R > N)
        return 0;

    // nCr= fact(n)/(fact(r)*fact(n-r))
    var res = parseInt(fact[N] / fact[R]);
    res = parseInt(res / fact[N - R]);

    return res;
}

// Function to count the number of ways
// to rearrange the array to obtain same BST
function countWays(arr, fact)
{
    // Store the size of the array
    var N = arr.length;

    // Base case
    if (N <= 2) {
        return 1;
    }

    // Store the elements of the
    // left subtree of BST
    var leftSubTree = [];

    // Store the elements of the
    // right subtree of BST
    var rightSubTree = [];

    // Store the root node
    var root = arr[0];

    for (var i = 1; i < N; i++) {

        // Push all the elements
        // of the left subtree
        if (arr[i] < root) {
            leftSubTree.push(
                arr[i]);
        }

        // Push all the elements
        // of the right subtree
        else {
            rightSubTree.push(
                arr[i]);
        }
    }

    // Store the size of leftSubTree
    var N1 = leftSubTree.length;

    // Store the size of rightSubTree
    var N2 = rightSubTree.length;

    // Recurrence relation
    var countLeft
        = countWays(leftSubTree,
                    fact);
    var countRight
        = countWays(rightSubTree,
                    fact);

    return nCr(fact, N - 1, N1)
           * countLeft * countRight;
}

// Driver Code

var arr = [];
arr = [3, 4, 5, 1, 2];

// Store the size of arr
var N = arr.length;

// Store the factorial up to N
var fact = Array(N);

// Precompute the factorial up to N
calculateFact(fact, N);
document.write( countWays(arr, fact));

</script>  
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*