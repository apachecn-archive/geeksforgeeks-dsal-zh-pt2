# 使二进制数组 K 周期的最小移动次数

> 原文:[https://www . geesforgeks . org/最小移动次数-制作二进制数组-k-periodic/](https://www.geeksforgeeks.org/minimum-number-of-moves-to-make-a-binary-array-k-periodic/)

给定一个二进制数组 **arr[]** (只包含 0 和 1)和一个整数 **K** 。任务是找到最小的移动次数，使数组 K 周期。
如果子阵列**【1 到 K】**、**【K+1 到 2K】**、**【2K+1 到 3K】、…** 都完全相同，则称一个阵列是 K 周期的。
在单次移动中，任何 1 都可以变成 0，或者任何 0 都可以变成 1。

**示例:**

> **输入:** arr[] = {1，1，0，0，1，1}，K = 2
> **输出:** 2
> 新数组可以是{1，1，1，1，1，1}
> 
> **输入:** arr[] = {1，0，0，0，1，0}，K = 2
> **输出:** 1
> 新数组可以是{1，0，1，0，1，0}

**方法:**对于 K 周期的数组。考虑指数 **i** 其中 **i % K = X** 。所有这些指数必须具有相同的值。因此，1 可以转换为 0，反之亦然。为了减少移动次数，我们选择最小的转换。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum moves required
int minMoves(int n, int a[], int k)
{

    int ct1[k] = { 0 }, ct0[k] = { 0 }, moves = 0;

    // Count the number of 1s and 2s
    // at each X such that i % K = X
    for (int i = 0; i < n; i++)
        if (a[i] == 1)
            ct1[i % k]++;
        else
            ct0[i % k]++;

    // Choose the minimum elements to change
    for (int i = 0; i < k; i++)
        moves += min(ct1[i], ct0[i]);

    // Return the minimum moves required
    return moves;
}

// Driver code
int main()
{
    int k = 2;
    int a[] = { 1, 0, 0, 0, 1, 0 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minMoves(n, a, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the minimum
// moves required
static int minMoves(int n, int a[], int k)
{
    int ct1[] = new int [k];
    int ct0[] = new int[k];
    int moves = 0;

    // Count the number of 1s and 2s
    // at each X such that i % K = X
    for (int i = 0; i < n; i++)
        if (a[i] == 1)
            ct1[i % k]++;
        else
            ct0[i % k]++;

    // Choose the minimum elements to change
    for (int i = 0; i < k; i++)
        moves += Math.min(ct1[i], ct0[i]);

    // Return the minimum moves required
    return moves;
}

// Driver code
public static void main (String[] args)
{
    int k = 2;
    int a[] = { 1, 0, 0, 0, 1, 0 };
    int n = a.length;
    System.out.println(minMoves(n, a, k));
}
}

// This is code contributed by inder_verma
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# moves required
def minMoves(n, a, k):
    ct1 = [0 for i in range(k)]
    ct0 = [0 for i in range(k)]
    moves = 0

    # Count the number of 1s and 2s
    # at each X such that i % K = X
    for i in range(n):
        if (a[i] == 1):
            ct1[i % k] += 1
        else:
            ct0[i % k] += 1

    # Choose the minimum elements to change
    for i in range(k):
        moves += min(ct1[i], ct0[i])

    # Return the minimum moves required
    return moves

# Driver code
if __name__ == '__main__':
    k = 2
    a = [1, 0, 0, 0, 1, 0]
    n = len(a)
    print(minMoves(n, a, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// moves required
static int minMoves(int n, int[] a, int k)
{
    int[] ct1 = new int [k];
    int[] ct0 = new int[k];
    int moves = 0;

    // Count the number of 1s and 2s
    // at each X such that i % K = X
    for (int i = 0; i < n; i++)
        if (a[i] == 1)
            ct1[i % k]++;
        else
            ct0[i % k]++;

    // Choose the minimum elements to change
    for (int i = 0; i < k; i++)
        moves += Math.Min(ct1[i], ct0[i]);

    // Return the minimum moves required
    return moves;
}

// Driver code
public static void Main ()
{
    int k = 2;
    int[] a = { 1, 0, 0, 0, 1, 0 };
    int n = a.Length;
    Console.WriteLine(minMoves(n, a, k));
}
}

// This is code contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// moves required
function minMoves($n, $a, $k)
{
    $ct1 = array();
    $ct0 = array();
    $moves = 0;

    // Count the number of 1s and 2s
    // at each X such that i % K = X
    for ($i = 0; $i < $n; $i++)
        if ($a[$i] == 1)
            $ct1[$i % $k]++;
        else
            $ct0[$i % $k]++;

    // Choose the minimum elements to change
    for ($i = 0; $i < $k; $i++)
        $moves += min($ct1[$i], $ct0[$i]);

    // Return the minimum moves required
    return $moves;
}

// Driver code
$k = 2;
$a = array(1, 0, 0, 0, 1, 0);
$n = sizeof($a);
echo(minMoves($n, $a, $k));

// This is code contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum moves required
function minMoves(n, a, k)
{

    let ct1 = new Uint8Array(k),
        ct0 = new Uint8Array(k), moves = 0;

    // Count the number of 1s and 2s
    // at each X such that i % K = X
    for(let i = 0; i < n; i++)
        if (a[i] == 1)
            ct1[i % k]++;
        else
            ct0[i % k]++;

    // Choose the minimum elements to change
    for(let i = 0; i < k; i++)
        moves += Math.min(ct1[i], ct0[i]);

    // Return the minimum moves required
    return moves;
}

// Driver code
let k = 2;
let a = [ 1, 0, 0, 0, 1, 0 ];
let n = a.length;

document.write(minMoves(n, a, k));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)