# 在给定条件下将一个置换转换为另一个置换所需的相邻置换的最小数量

> 原文:[https://www . geeksforgeeks . org/最小相邻交换次数-按给定条件将一个置换转换为另一个置换所需的次数/](https://www.geeksforgeeks.org/minimum-number-of-adjacent-swaps-required-to-convert-a-permutation-to-another-permutation-by-given-condition/)

给定大小为 **N** 的排列 P ，其值从 **1 到 N** 。任务是找到所需的相邻交换的最小数量，使得对于范围**【1，N】**，**P【I】不等于 i** 中的所有 I。
**举例:**

> **输入:** P = [1，4，3，5，2]
> **输出:** 2
> **解释:**
> 这里 P = [1，4，3，5，2]在索引 1，2，3，4，5 处。我们可以看到，P[1] = 1，P[3] = 3。因此，我们需要去掉这个不变量。
> 交换 1:交换索引 1 和索引 2 = > [4，1，3，5，2]
> 交换 2:交换索引 2 和索引 3 = > [4，3，1，5，2]
> 最终数组没有 I，其中 P[i] = i。因此，至少需要 2 次交换。
> **输入:** P = [1，2，4，9，5，8，7，3，6]
> **输出:** 3
> **解释:**
> 互换 1:互换指数 1 和指数 2 =>【2，1，4，9，5，8，7，3，6】
> 互换 2:互换指数 5 和指数 6 =>【2，1，4，9，8，5

**进场:**我们来考虑一下 **P[i] = i** 用 **X** 表示的位置，其他位置用 **O** 表示。以下是对这个问题的三个基本观察:

*   如果排列的任意两个相邻索引处的值是 **XO** 的形式，我们可以简单地交换这两个索引以获得“OO”。
*   如果排列的任意两个相邻索引处的值是 **XX** 的形式，我们可以简单地交换这两个索引以获得“OO”。
*   如果排列的任意两个相邻索引处的值是 **OX** 的形式，那么一旦指针到达位于 **X** 的索引处，它就是**【XO】**或**【XX】**。

以下是步骤:

1.  从 **1 迭代到 N–1**并检查 **P[i] = i** 然后我们简单地**交换(P[i]，P[i + 1])** ，否则继续下一个相邻对的过程。
2.  给定问题的基本情况是当 **i = N** 时，如果 P[i] = i，那么我们**交换(P[i]，P[I–1])**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of swaps
void solve(vector<int>& P, int n)
{

    // New array to convert
    // to 1-based indexing
    vector<int> arr;

    arr.push_back(0);

    for (auto x : P)
        arr.push_back(x);

    // Keeps count of swaps
    int cnt = 0;

    for (int i = 1; i < n; i++) {

        // Check if it is an 'X' position
        if (arr[i] == i) {
            swap(arr[i], arr[i + 1]);
            cnt++;
        }
    }

    // Corner Case
    if (arr[n] == n) {

        swap(arr[n - 1], arr[n]);
        cnt++;
    }

    // Print the minimum swaps
    cout << cnt << endl;
}

// Driver Code
signed main()
{
    // Given Number N
    int N = 9;

    // Given Permutation of N numbers
    vector<int> P = { 1, 2, 4, 9, 5,
                      8, 7, 3, 6 };

    // Function Call
    solve(P, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum
// number of swaps
static void solve(int P[], int n)
{

    // New array to convert
    // to 1-based indexing
    int arr[] = new int[n + 1];

    arr[0] = 0;

    for(int i = 0; i < n; i++)
       arr[i + 1] = P[i];

    // Keeps count of swaps
    int cnt = 0;

    for(int i = 1; i < n; i++)
    {

       // Check if it is an 'X' position
       if (arr[i] == i)
       {
           int t = arr[i + 1];
           arr[i + 1] = arr[i];
           arr[i] = t;
           cnt++;
       }
    }

    // Corner Case
    if (arr[n] == n)
    {

        // Swap
        int t = arr[n - 1];
        arr[n - 1] = arr[n];
        arr[n] = t;
        cnt++;
    }

    // Print the minimum swaps
    System.out.println(cnt);
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int N = 9;

    // Given Permutation of N numbers
    int P[] = new int[]{ 1, 2, 4, 9, 5,
                         8, 7, 3, 6 };

    // Function Call
    solve(P, N);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# number of swaps
def solve(P, n):

    # New array to convert
    # to 1-based indexing
    arr = []

    arr.append(0)

    for x in P:
        arr.append(x)

    # Keeps count of swaps
    cnt = 0

    for i in range(1, n):

        # Check if it is an 'X' position
        if (arr[i] == i):
            arr[i], arr[i + 1] = arr[i + 1], arr[i]
            cnt += 1

    # Corner Case
    if (arr[n] == n):
        arr[n - 1], arr[n] = arr[n] , arr[n - 1]
        cnt += 1

    # Print the minimum swaps
    print(cnt)

# Driver Code

# Given number N
N = 9

# Given permutation of N numbers
P = [ 1, 2, 4, 9, 5,
      8, 7, 3, 6 ]

# Function call
solve(P, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum
// number of swaps
static void solve(int []P, int n)
{

    // New array to convert
    // to 1-based indexing
    int []arr = new int[n + 1];

    arr[0] = 0;

    for(int i = 0; i < n; i++)
        arr[i + 1] = P[i];

    // Keeps count of swaps
    int cnt = 0;

    for(int i = 1; i < n; i++)
    {

        // Check if it is an 'X' position
        if (arr[i] == i)
        {
            int t = arr[i + 1];
            arr[i + 1] = arr[i];
            arr[i] = t;
            cnt++;
        }
    }

    // Corner Case
    if (arr[n] == n)
    {

        // Swap
        int t = arr[n - 1];
        arr[n - 1] = arr[n];
        arr[n] = t;
        cnt++;
    }

    // Print the minimum swaps
    Console.WriteLine(cnt);
}

// Driver code
public static void Main(String[] args)
{

    // Given Number N
    int N = 9;

    // Given Permutation of N numbers
    int []P = { 1, 2, 4, 9, 5,
                8, 7, 3, 6 };

    // Function Call
    solve(P, N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum
// number of swaps
function solve(P, n)
{

    // New array to convert
    // to 1-based indexing
    let arr = Array.from({length: n+1}, (_, i) => 0);

    arr[0] = 0;

    for(let i = 0; i < n; i++)
       arr[i + 1] = P[i];

    // Keeps count of swaps
    let cnt = 0;

    for(let i = 1; i < n; i++)
    {

       // Check if it is an 'X' position
       if (arr[i] == i)
       {
           let t = arr[i + 1];
           arr[i + 1] = arr[i];
           arr[i] = t;
           cnt++;
       }
    }

    // Corner Case
    if (arr[n] == n)
    {

        // Swap
        let t = arr[n - 1];
        arr[n - 1] = arr[n];
        arr[n] = t;
        cnt++;
    }

    // Prlet the minimum swaps
    document.write(cnt);
}

// Driver Code

    // Given Number N
    let N = 9;

    // Given Permutation of N numbers
    let P = [ 1, 2, 4, 9, 5,
                         8, 7, 3, 6 ];

    // Function Call
    solve(P, N);

</script>
```

**Output:**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)