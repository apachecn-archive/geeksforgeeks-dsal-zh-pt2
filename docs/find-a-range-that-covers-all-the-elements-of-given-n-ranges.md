# 找到一个覆盖给定 N 个范围的所有元素的范围

> 原文:[https://www . geesforgeks . org/find-a-range-覆盖给定 n-range 的所有元素/](https://www.geeksforgeeks.org/find-a-range-that-covers-all-the-elements-of-given-n-ranges/)

给定 N 个包含 L 和 r 的范围。任务是检查或查找覆盖所有其他给定 N-1 范围的范围的索引(从 0 开始)。如果没有这样的范围，请打印-1。
**注:**所有的 L 点和 R 点都是截然不同的。
**示例:**

> **输入:** L[] = {1，2}，R[] = {1，2}
> **输出:** -1
> **输入:** L[] = {2，4，3，1}，R[] = {4，6，7，9}
> **输出:** 3
> 第 3 个索引处的范围即 1 到 9 涵盖了
> 其他 N-1 范围的所有元素。

**方法:**由于所有的 L 点和 R 点都是不同的，找到最小的 **L** 点的范围和最大的 **R** 点的范围，如果两者都在同一个范围内，就意味着所有其他范围都在其中，否则不可能。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check range
int findRange(int n, int lf[], int rt[])
{

    // Index of smallest L and largest R
    int mnlf = 0, mxrt = 0;
    for (int i = 1; i < n; i++) {
        if (lf[i] < lf[mnlf])
            mnlf = i;
        if (rt[i] > rt[mxrt])
            mxrt = i;
    }

    // If the same range has smallest L
    // and largest R
    if (mnlf == mxrt)
        return mnlf;
    else
        return -1;
}

// Driver Code
int main()
{
    int N = 4;
    int L[] = { 2, 4, 3, 1 };
    int R[] = { 4, 6, 7, 9 };

    cout << findRange(N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {
// Function to check range
static int  findRange(int n, int lf[], int rt[])
{

    // Index of smallest L and largest R
    int mnlf = 0, mxrt = 0;
    for (int i = 1; i < n; i++) {
        if (lf[i] < lf[mnlf])
            mnlf = i;
        if (rt[i] > rt[mxrt])
            mxrt = i;
    }

    // If the same range has smallest L
    // and largest R
    if (mnlf == mxrt)
        return mnlf;
    else
        return -1;
}

// Driver Code

    public static void main (String[] args) {
            int N = 4;
    int[] L = { 2, 4, 3, 1 };
    int []R = { 4, 6, 7, 9 };

    System.out.println( findRange(N, L, R));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to check range
def findRange(n, lf, rt):

    # Index of smallest L and
    # largest R
    mnlf, mxrt = 0, 0
    for i in range(1, n):
        if lf[i] < lf[mnlf]:
            mnlf = i
        if rt[i] > rt[mxrt]:
            mxrt = i

    # If the same range has smallest
    # L and largest R
    if mnlf == mxrt:
        return mnlf
    else:
        return -1

# Driver Code
if __name__ == "__main__":

    N = 4
    L = [2, 4, 3, 1]
    R = [4, 6, 7, 9]

    print(findRange(N, L, R))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{
// Function to check range
static int findRange(int n, int []lf,
                            int []rt)
{

    // Index of smallest L and largest R
    int mnlf = 0, mxrt = 0;
    for (int i = 1; i < n; i++)
    {
        if (lf[i] < lf[mnlf])
            mnlf = i;
        if (rt[i] > rt[mxrt])
            mxrt = i;
    }

    // If the same range has smallest L
    // and largest R
    if (mnlf == mxrt)
        return mnlf;
    else
        return -1;
}

// Driver Code
public static void Main ()
{
    int N = 4;
    int[] L = { 2, 4, 3, 1 };
    int []R = { 4, 6, 7, 9 };

    Console.WriteLine(findRange(N, L, R));
}
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to check range
function findRange($n, $lf, $rt)
{

    // Index of smallest L and largest R
    $mnlf = 0; $mxrt = 0;
    for ($i = 1; $i <$n; $i++)
    {
        if ($lf[$i] < $lf[$mnlf])
            $mnlf = $i;
        if ($rt[$i] > $rt[$mxrt])
            $mxrt = $i;
    }

    // If the same range has smallest
    // L and largest R
    if ($mnlf == $mxrt)
        return $mnlf;
    else
        return -1;
}

// Driver Code
$N = 4;
$L = array( 2, 4, 3, 1 );
$R = array( 4, 6, 7, 9 );

echo findRange($N, $L, $R);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to check range
function findRange(n, lf, rt)
{

    // Index of smallest L and largest R
    let mnlf = 0, mxrt = 0;
    for (let i = 1; i < n; i++) {
        if (lf[i] < lf[mnlf])
            mnlf = i;
        if (rt[i] > rt[mxrt])
            mxrt = i;
    }

    // If the same range has smallest L
    // and largest R
    if (mnlf == mxrt)
        return mnlf;
    else
        return -1;
}

// Driver Code
    let N = 4;
    let L = [ 2, 4, 3, 1 ];
    let R = [ 4, 6, 7, 9 ];

    document.write(findRange(N, L, R));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)