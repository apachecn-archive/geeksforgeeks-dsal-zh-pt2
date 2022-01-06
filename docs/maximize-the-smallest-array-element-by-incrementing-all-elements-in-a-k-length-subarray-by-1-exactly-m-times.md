# 通过将 K 长度子阵列中的所有元素精确地增加 1M 倍来最大化最小的阵列元素

> 原文:[https://www . geeksforgeeks . org/通过将 k 长度子数组中的所有元素递增 1 乘以正好 m 倍来最大化最小的数组元素/](https://www.geeksforgeeks.org/maximize-the-smallest-array-element-by-incrementing-all-elements-in-a-k-length-subarray-by-1-exactly-m-times/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**和整数 **M** 和 **K** ，任务是通过执行 **M** 运算找到**最大**可能值的**最小**数组元素。在每次操作中，将长度为 **K** 的相邻[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中所有元素的值增加 **1** 。

**示例:**

> **输入:** arr[ ] = {2，2，2，2，1，1}，M = 1，K = 3
> **输出:** 2
> **说明:**更新第一次移动的最后 3 个元素那么更新后的数组就是【2，2，2，3，2，2】。最小元素的值为 2。
> 
> **输入:** arr[ ] = {5，8}，M = 5，K = 1
> T3】输出: 9

**方式:**使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以解决问题。[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个元素 **arr[i]** ，计算所需的操作次数。如果当前元素需要更新 **x** 次，则在答案中加上 **x** ，将长度为 **K** 的连续段更新 **x** 次。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
ll n, m, k, l, r, i;

// Function to check if the smallest
// value of v is achievable or not
ll check(ll v, vector<ll>& a)
{
    ll tec = 0, ans = 0;

    // Create array to
    // store previous moves
    vector<ll> b(n + k + 1);

    for (i = 0; i < n; i++) {

        // Remove previous moves
        tec -= b[i];

        if (a[i] + tec < v) {

            // Add balance to ans
            ll mov = v - a[i] - tec;
            ans = ans + mov;

            // Update contiguous
            // subarray of length k
            tec += mov;
            b[i + k] = mov;
        }
    }

    // Number of moves
    // should not exceed m
    return (ans <= m);
}

// Function to find the maximum
// value of the smallest array
// element that can be obtained
ll FindLargest(vector<ll> a)
{
    l = 1;
    r = pow(10, 10);

    // Perform Binary search
    while (r - l > 0) {

        ll tm = (l + r + 1) / 2;

        if (check(tm, a))
            l = tm;
        else
            r = tm - 1;
    }
    return l;
}

// Driver Code
int main()
{
    // Given Input
    vector<ll> a{ 2, 2, 2, 2, 1, 1 };
    m = 2;
    k = 3;
    n = a.size();

    // Function Call
    cout << FindLargest(a);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

static long n, m, k, l, r, i;

// Function to check if the smallest
// value of v is achievable or not
static boolean check(long v, long[] a)
{
    long tec = 0, ans = 0;

    // Create array to
    // store previous moves
    long[] b = new long[(int)(n + k + 1)];

    for(int i = 0; i < n; i++)
    {

        // Remove previous moves
        tec -= b[i];

        if (a[i] + tec < v)
        {

            // Add balance to ans
            long mov = v - a[i] - tec;
            ans = ans + mov;

            // Update contiguous
            // subarray of length k
            tec += mov;
            b[i + (int)k] = mov;
        }
    }

    // Number of moves
    // should not exceed m
    return ans <= m;
}

// Function to find the maximum
// value of the smallest array
// element that can be obtained
static long FindLargest(long[] a)
{
    l = 1;
    r = (long)Math.pow(10, 10);

    // Perform Binary search
    while (r - l > 0)
    {
        long tm = (l + r + 1) / 2;

        if (check(tm, a))
            l = tm;
        else
            r = tm - 1;
    }
    return l;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    long[] a = { 2, 2, 2, 2, 1, 1 };
    m = 2;
    k = 3;
    n = a.length;

    // Function Call
    System.out.println(FindLargest(a));
}
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python 3 program for above approach

n = 0
m = 0
k = 0
l = 0
r = 0
i = 0

from math import pow
# Function to check if the smallest
# value of v is achievable or not
def check(v, a):
    tec = 0
    ans = 0

    # Create array to
    # store previous moves
    b = [0 for i in range(n + k + 1)]

    for i in range(n):
        # Remove previous moves
        tec -= b[i]

        if (a[i] + tec < v):
            # Add balance to ans
            mov = v - a[i] - tec
            ans = ans + mov

            # Update contiguous
            # subarray of length k
            tec += mov
            b[i + k] = mov

    # Number of moves
    # should not exceed m
    return (ans <= m)

# Function to find the maximum
# value of the smallest array
# element that can be obtained
def FindLargest(a):
    l = 1
    r = pow(10, 10)

    # Perform Binary search
    while (r - l > 0):
        tm = (l + r + 1) // 2

        if (check(tm, a)):
            l = tm
        else:
            r = tm - 1
    return l

# Driver Code
if __name__ == '__main__':

    # Given Input
    a = [2, 2, 2, 2, 1, 1]
    m = 2
    k = 3
    n = len(a)

    # Function Call
    print(int(FindLargest(a)))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

static long n, m, k, l, r, i;

// Function to check if the smallest
// value of v is achievable or not
static bool check(long v, long[] a)
{
    long tec = 0, ans = 0;

    // Create array to
    // store previous moves
    long[] b = new long[(int)(n + k + 1)];

    for(int i = 0; i < n; i++)
    {

        // Remove previous moves
        tec -= b[i];

        if (a[i] + tec < v)
        {

            // Add balance to ans
            long mov = v - a[i] - tec;
            ans = ans + mov;

            // Update contiguous
            // subarray of length k
            tec += mov;
            b[i + (int)k] = mov;
        }
    }

    // Number of moves
    // should not exceed m
    return ans <= m;
}

// Function to find the maximum
// value of the smallest array
// element that can be obtained
static long FindLargest(long[] a)
{
    l = 1;
    r = (long)Math.Pow(10, 10);

    // Perform Binary search
    while (r - l > 0)
    {
        long tm = (l + r + 1) / 2;

        if (check(tm, a))
            l = tm;
        else
            r = tm - 1;
    }
    return l;
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    long[] a = { 2, 2, 2, 2, 1, 1 };
    m = 2;
    k = 3;
    n = a.Length;

    // Function Call
    Console.WriteLine(FindLargest(a));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for above approach
let n = 0, m = 0, k = 0, l = 0, r = 0, i = 0;

// Function to check if the smallest
// value of v is achievable or not
function check(v, a)
{
    let tec = 0,
    ans = 0;

    // Create array to
    // store previous moves
    let b = new Array(n + k + 1).fill(0);

    for(i = 0; i < n; i++)
    {

        // Remove previous moves
        tec -= b[i];

        if (a[i] + tec < v)
        {

            // Add balance to ans
            let mov = v - a[i] - tec;
            ans = ans + mov;

            // Update contiguous
            // subarray of length k
            tec += mov;
            b[i + k] = mov;
        }
    }

    // Number of moves
    // should not exceed m
    return ans <= m;
}

// Function to find the maximum
// value of the smallest array
// element that can be obtained
function FindLargest(a)
{
    l = 1;
    r = Math.pow(10, 10);

    // Perform Binary search
    while (r - l > 0)
    {
        let tm = Math.floor((l + r + 1) / 2);

        if (check(tm, a)) l = tm;
        else r = tm - 1;
    }
    return l;
}

// Driver Code

// Given Input
let a = [ 2, 2, 2, 2, 1, 1 ];
m = 2;
k = 3;
n = a.length;

// Function Call
document.write(FindLargest(a));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N + K)*