# 正负整数形式的最长交替子序列

> 原文:[https://www . geeksforgeeks . org/最长正负整数交替子序列/](https://www.geeksforgeeks.org/longest-alternating-subsequence-in-terms-of-positive-and-negative-integers/)

给定一个只有正数和负数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找出出现在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中的最长交替(表示负-正-负或正-负-正)子序列的长度。

**示例:**

> **输入:** arr[] = {-4，3，-5，9，10，12，2，-1}
> **输出:** 5
> **解释:**
> 最长的序列是{-4，3，-5，9，-1}，长度为 5。这个长度的子序列可以有更多。
> 
> **输入:** arr[] = {10，12，2，-1}
> **输出:** 2
> **解释:**
> 最长的序列是{10，-1}，也就是 2。这个长度的子序列可以有更多。

**方法:**
这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。这是一个变异[最长增加子序列(LIS)](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/) 。以下是步骤:

1.  对于 LAS(最长可选子序列)的给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中的包含和排除元素，使用变量 **pos** ，当 **pos** = true 时，表示当前元素需要为正，如果 **pos** = false，则当前元素需要为负。
2.  如果我们包含当前元素，请更改**位置**的值，并为下一个元素递归，因为我们需要与之前包含的元素相反的下一个元素。
3.  现在 **LAS[i][pos]** 可以递归地写成:
    *   **<u>基本情况:</u>** 如果递归调用的索引大于最后一个元素，那么返回 0，因为没有这样的元素剩下来形成 LAS，如果计算出 **LAS[i][pos]** ，那么返回该值。

> if(i == N) {
> 返回 0；
> }
> if(LAS[i][pos]) {
> 返回 LAS[I][pos]；

*   **<u>递归调用:</u>** 如果不满足基本情况，则在包含和排除当前元素时递归调用，然后在该索引处找到要查找的 LAS 的最大值。

> LAS[i][pos] =索引 I 处的最长交替子序列，包括或排除 **pos** 、
> LAS[I][pos]= max(1+recursive_function(i+1，pos)，recursive _ function(I+1，pos))；

*   **<u>返回语句:</u>** 在每次递归调用时(基本情况除外)，返回**LAS【I】【pos】**的值。

> 返回[I][pos]；

1.  给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 的 LAS 是 LAS[0][0]和 LAS[0][1]的最大值。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// length of longest alternate
// subsequence
#include <bits/stdc++.h>
using namespace std;

// LAS[i][pos] array to find
// the length of LAS till
// index i by including or
// excluding element arr[i]
// on the basis of value of pos
int LAS[1000][2] = { false };

int solve(int arr[], int n, int i, bool pos)
{
    // Base Case
    if (i == n)
        return 0;

    if (LAS[i][pos])
        return LAS[i][pos];

    int inc = 0, exc = 0;

    // If current element is
    // positive and pos is true
    // Include the current element
    // and change pos to false
    if (arr[i] > 0 && pos == true) {
        pos = false;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // negative and pos is false
    // Include the current element
    // and change pos to true
    else if (arr[i] < 0 && pos == false) {
        pos = true;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // excluded, reccur for
    // next iteration
    exc = solve(arr, n, i + 1, pos);

    LAS[i][pos] = max(inc, exc);

    return LAS[i][pos];
}

// Driver's Code
int main()
{
    int arr[] = { -1, 2, 3, 4, 5,
                  -6, 8, -99 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Print LAS
    cout << max(solve(arr, n, 0, 0),
                solve(arr, n, 0, 1));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// length of longest alternate
// subsequence
class GFG {

// LAS[i][pos] array to find
// the length of LAS till
// index i by including or
// excluding element arr[i]
// on the basis of value of pos
static int LAS[][] = new int[1000][2];

static int solve(int arr[], int n, int i,int pos)
{

    // Base Case
    if (i == n)
        return 0;

    if (LAS[i][pos]== 1)
        return LAS[i][pos];

    int inc = 0, exc = 0;

    // If current element is
    // positive and pos is 1
    // Include the current element
    // and change pos to 0
    if (arr[i] > 0 && pos == 1) {
        pos = 0;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // negative and pos is o
    // Include the current element
    // and change pos to 1
    else if (arr[i] < 0 && pos == 0) {
        pos = 1;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // excluded, reccur for
    // next iteration
    exc = solve(arr, n, i + 1, pos);

    LAS[i][pos] = Math.max(inc, exc);

    return LAS[i][pos];
}

// Driver's Code
public static void main (String[] args)
{
    int arr[] = { -1, 2, 3, 4, 5, -6, 8, -99 };
    int n = arr.length;

    // Print LAS
    System.out.println(Math.max(solve(arr, n, 0, 0),solve(arr, n, 0, 1)));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the
# length of longest alternate
# subsequence
import numpy as np

# LAS[i][pos] array to find
# the length of LAS till
# index i by including or
# excluding element arr[i]
# on the basis of value of pos
LAS = np.zeros((1000, 2))

for i in range(1000) :
    for j in range(2) :
        LAS[i][j] = False

def solve(arr, n, i, pos) :

    # Base Case
    if (i == n) :
        return 0;

    if (LAS[i][pos]) :
        return LAS[i][pos];

    inc = 0; exc = 0;

    # If current element is
    # positive and pos is true
    # Include the current element
    # and change pos to false
    if (arr[i] > 0 and pos == True) :
        pos = False;

        # Recurr for the next
        # iteration
        inc = 1 + solve(arr, n, i + 1, pos);

    # If current element is
    # negative and pos is false
    # Include the current element
    # and change pos to true
    elif (arr[i] < 0 and pos == False) :
        pos = True;

        # Recurr for the next
        # iteration
        inc = 1 + solve(arr, n, i + 1, pos);

    # If current element is
    # excluded, reccur for
    # next iteration
    exc = solve(arr, n, i + 1, pos);

    LAS[i][pos] = max(inc, exc);

    return LAS[i][pos];

# Driver's Code
if __name__ == "__main__" :

    arr = [ -1, 2, 3, 4, 5, -6, 8, -99 ];
    n = len(arr);

    # Print LAS
    print(max(solve(arr, n, 0, 0), solve(arr, n, 0, 1)));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the
// length of longest alternate
// subsequence

using System;

public class GFG {

// LAS[i][pos] array to find
// the length of LAS till
// index i by including or
// excluding element arr[i]
// on the basis of value of pos
static int [,]LAS = new int[1000,2];

static int solve(int []arr, int n, int i,int pos)
{

    // Base Case
    if (i == n)
        return 0;

    if (LAS[i,pos]== 1)
        return LAS[i,pos];

    int inc = 0, exc = 0;

    // If current element is
    // positive and pos is 1
    // Include the current element
    // and change pos to 0
    if (arr[i] > 0 && pos == 1) {
        pos = 0;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // negative and pos is o
    // Include the current element
    // and change pos to 1
    else if (arr[i] < 0 && pos == 0) {
        pos = 1;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // excluded, reccur for
    // next iteration
    exc = solve(arr, n, i + 1, pos);

    LAS[i,pos] = Math.Max(inc, exc);

    return LAS[i,pos];
}

// Driver's Code
public static void Main()
{
    int []arr = { -1, 2, 3, 4, 5, -6, 8, -99 };
    int n = arr.Length;

    // Print LAS
    Console.WriteLine(Math.Max(solve(arr, n, 0, 0),solve(arr, n, 0, 1)));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to find the
// length of longest alternate
// subsequence

// LAS[i][pos] array to find
// the length of LAS till
// index i by including or
// excluding element arr[i]
// on the basis of value of pos
let LAS = new Array();

for(let i = 0; i < 1000; i++){
    let temp = new Array()
    for(let j = 0; j < 2; j++){
        temp.push([])
    }
    LAS.push(temp);
}

for(let i = 0; i < 1000; i++){
    for(let j = 0; j < 2; j++){
        LAS[i][j] = false
    }
}

function solve(arr, n, i, pos)
{
    // Base Case
    if (i == n)
        return 0;

    if (LAS[i][pos])
        return LAS[i][pos];

    let inc = 0, exc = 0;

    // If current element is
    // positive and pos is true
    // Include the current element
    // and change pos to false
    if (arr[i] > 0 && pos == true) {
        pos = false;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // negative and pos is false
    // Include the current element
    // and change pos to true
    else if (arr[i] < 0 && pos == false) {
        pos = true;

        // Recurr for the next
        // iteration
        inc = 1 + solve(arr, n, i + 1, pos);
    }

    // If current element is
    // excluded, reccur for
    // next iteration
    exc = solve(arr, n, i + 1, pos);

    LAS[i][pos] = Math.max(inc, exc);

    return LAS[i][pos];
}

// Driver's Code

let arr = [ -1, 2, 3, 4, 5,
            -6, 8, -99 ];
let n = arr.length;

// Print LAS
document.write(Math.max(solve(arr, n, 0, 0), solve(arr, n, 0, 1)));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)，其中 N 为数组长度。