# 具有 K 个完美指数的前 N 个自然数的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的第一个 n 个自然数的最小排列-拥有-k 个完美索引/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-first-n-natural-numbers-having-k-perfect-indices/)

给定两个正整数 **N** 和 **K** ，任务是从字典上找到第一个 **N** 自然数的最小排列，这样就正好有 **K** 个完美的索引。

> 如果索引小于**I**的所有元素都小于索引为**I**的元素，则数组中的索引为**完美**。

**示例:**

> **输入:** N = 10，K = 3
> **输出:** 8 9 10 1 2 3 4 5 6 7
> **说明:**正好有 3 个完美指数 0，1，2。
> 
> **输入:** N = 12，K = 4
> T3】输出: 9 10 11 12 1 2 3 4 5 6 7 8

**天真方法:**想法是[生成第一个 **N** 自然数](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能的排列，并打印该[排列，该排列在词典上是最小的](https://www.geeksforgeeks.org/lexicographically-n-th-permutation-string/)，并且具有 **K 个完美索引**。
***时间复杂度:** O(N*N！)*
***辅助空间:** O(1)*

**高效途径:**对上述途径进行优化，思路是观察[最小排列](https://www.geeksforgeeks.org/find-smallest-permutation-given-number/)将使范围**【1，N】**的最后 **K** 元素按递增顺序在前。剩余的元素可以按递增的顺序添加。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 来存储第一个 **N 个**自然数的[字典最小排列](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-1-n-no-position-not-match/)。
*   使用变量迭代范围**【0，K–1】**，说 **i** ，更新数组元素**A【I】**来存储**(N–K+1)+I**。
*   使用变量 **i** 迭代范围**【K，N–1】**，并将数组元素**A【I】**更新为**(I–K+1)**。
*   完成上述步骤后，[用 **K 个完美索引**打印包含字典上最小排列的数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **A[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to print the lexicographically
// smallest permutation with K perfect indices
void findPerfectIndex(int N, int K)
{
    // Iterator to traverse the array
    int i = 0;

    // Traverse first K array indices
    for (; i < K; i++) {
        cout << (N - K + 1) + i << " ";
    }

    // Traverse remaining indices
    for (; i < N; i++) {
        cout << i - K + 1 << " ";
    }
}

// Driver Code
int main()
{
    int N = 10, K = 3;
    findPerfectIndex(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to print the lexicographically
// smallest permutation with K perfect indices
static void findPerfectIndex(int N, int K)
{

    // Iterator to traverse the array
    int i = 0;

    // Traverse first K array indices
    for (; i < K; i++)
    {
        System.out.print((N - K + 1) + i+ " ");
    }

    // Traverse remaining indices
    for (; i < N; i++)
    {
        System.out.print(i - K + 1+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 10, K = 3;
    findPerfectIndex(N, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print the lexicographically
# smallest permutation with K perfect indices
def findPerfectIndex(N, K) :

    # Iterator to traverse the array
    i = 0

    # Traverse first K array indices
    for i in range(K):
        print((N - K + 1) + i, end = " ")

    # Traverse remaining indices
    for i in range(3, N):
        print( i - K + 1, end = " ")

# Driver Code

N = 10
K = 3
findPerfectIndex(N, K)

# This code is contributed by code_hunt.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to print the lexicographically
// smallest permutation with K perfect indices
static void findPerfectIndex(int N, int K)
{

    // Iterator to traverse the array
    int i = 0;

    // Traverse first K array indices
    for (; i < K; i++)
    {
        Console.Write((N - K + 1) + i+ " ");
    }

    // Traverse remaining indices
    for (; i < N; i++)
    {
        Console.Write(i - K + 1+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 10, K = 3;
    findPerfectIndex(N, K);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// javascript program for the above approach
// Function to prvar the lexicographically
// smallest permutation with K perfect indices
function findPerfectIndex(N , K)
{

    // Iterator to traverse the array
    var i = 0;

    // Traverse first K array indices
    for (; i < K; i++)
    {
        document.write((N - K + 1) + i+ " ");
    }

    // Traverse remaining indices
    for (; i < N; i++)
    {
        document.write(i - K + 1+ " ");
    }
}

// Driver Code
var N = 10, K = 3;
findPerfectIndex(N, K);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
8 9 10 1 2 3 4 5 6 7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)