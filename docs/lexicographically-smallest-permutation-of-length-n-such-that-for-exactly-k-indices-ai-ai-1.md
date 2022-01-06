# 长度为 N 的字典最小排列，对于精确的 K 个索引，a[i] > a[i] + 1

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小长度排列-n-so-for-just-k-indexs-ai-ai-1/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-length-n-such-that-for-exactly-k-indices-ai-ai-1/)

给定两个整数 N 和 K，任务是生成 N 个数字的排列(从 1 到 N 的每个数字恰好出现一次)，使得 a[i]>a[i+1]的索引数正好为 K。如果没有这样的排列，则打印“不可能”。
**例:**

```
Input: N = 5, K = 3
Output: 5 4 3 1 2
Starting 3 indices satisfying the condition 
a[i] > a[i]+1

Input: N = 7, k = 4
Output: 7 6 5 4 1 2 3
```

**方法:**因为置换在字典上应该是最小的，k 个索引满足条件，即 a[i] > a[i+1]。因此，开始的 K+1 位应该是递减的，剩余的应该是递增的。所以只需打印从 N 到 1 的 K 个数字。然后打印从 1 到 N-K 的数字

> **例如:** N = 6，K = 4
> 从 N 到 1 打印 K 个数字，即 6，5，4，3
> 从 1 到 N-K 打印 N-K 个数字，即 1，2
> 排列将为 654312，即对于 i = 1 到 K
> ，开始的 4 个索引满足 a[i] > a[i+1]

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

void printPermutation(int n, int k)
{
    int i, mx = n;
    for (i = 1; i <= k; i++) // Decreasing part
    {
        cout << mx << " ";
        mx--;
    }
    for (i = 1; i <= mx; i++) // Increasing part
        cout << i << " ";
}

// Driver Code
int main()
{
    int N = 5, K = 3;

    if (K >= N - 1)
        cout << "Not Possible";

    else
        printPermutation(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {

static void printPermutation(int n, int k)
{
    int i, mx = n;
    for (i = 1; i <= k; i++) // Decreasing part
    {
        System.out.print( mx + " ");
        mx--;
    }
    for (i = 1; i <= mx; i++) // Increasing part
        System.out.print( i + " ");
}

// Driver Code

    public static void main (String[] args) {
            int N = 5, K = 3;

    if (K >= N - 1)
        System.out.print( "Not Possible");

    else
        printPermutation(N, K);
    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
def printPermutation(n, k):

    mx = n
    for i in range(1, k + 1): # Decreasing part
        print(mx, end = " ")
        mx -= 1

    for i in range(1, mx + 1): # Increasing part
        print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    N, K = 5, 3

    if K >= N - 1:
        print("Not Possible")

    else:
        printPermutation(N, K)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;
class GFG {

static void printPermutation(int n, int k)
{
    int i, mx = n;
    for (i = 1; i <= k; i++) // Decreasing part
    {
        Console.Write( mx + " ");
        mx--;
    }
    for (i = 1; i <= mx; i++) // Increasing part
        Console.Write( i + " ");
}

// Driver Code

    public static void Main () {
            int N = 5, K = 3;

    if (K >= N - 1)
        Console.WriteLine( "Not Possible");

    else
        printPermutation(N, K);
    }
}

// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  implementation of the above approach

function printPermutation($n, $k)
{
    $i; $mx = $n;
    for ($i = 1; $i <=$k; $i++) // Decreasing part
    {
        echo  $mx , " ";
        $mx--;
    }
    for ($i = 1; $i <=$mx; $i++) // Increasing part
        echo $i , " ";
}

// Driver Code

    $N = 5; $K = 3;

    if ($K >= $N - 1)
        echo "Not Possible";

    else
        printPermutation($N, $K);

// This code is contributed by inder_verma..
?>
```

## java 描述语言

```
<script>
// javascript implementation of the above approach
function printPermutation(n , k)
{
    var i, mx = n;
    for (i = 1; i <= k; i++) // Decreasing part
    {
        document.write( mx + " ");
        mx--;
    }
    for (i = 1; i <= mx; i++) // Increasing part
        document.write( i + " ");
}

// Driver Code
var N = 5, K = 3;

if (K >= N - 1)
    document.write( "Not Possible");

else
    printPermutation(N, K);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
5 4 3 1 2
```

**时间复杂度:** O(N)