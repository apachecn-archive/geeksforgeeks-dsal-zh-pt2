# 最大化图中不属于任何边的节点数

> 原文:[https://www . geeksforgeeks . org/最大化不是图中任何边的一部分的节点数/](https://www.geeksforgeeks.org/maximize-number-of-nodes-which-are-not-part-of-any-edge-in-a-graph/)

给定一个有 n 个节点和 m 条边的图。找出不属于任何边的最大可能节点数(m 总是小于或等于完全图中的边数)。
**例:**

```
Input: n = 3, m = 3
Output: Maximum Nodes Left Out: 0
Since it is a complete graph.

Input: n = 7, m = 6 
Output: Maximum Nodes Left Out: 3
We can construct a complete graph on 4 vertices using 6 edges.
```

**方法:**遍历所有 n 个节点，看看在哪个节点上，如果我们做一个完整的图，我们得到的边数大于 m，说它是 k，答案是 **n-k** 。

*   可用于在 n 个节点上形成图的最大边数为**n *(n–1)/2**(一个完整的图)。
*   然后求最大 n 的个数，用 m 条或 m 条以下的边组成一个完整的图。
*   如果还剩下边，那么它将只覆盖一个以上的节点，就好像它已经覆盖了一个以上的节点一样，这不是 n 的最大值。

以下是上述方法的实现:

## C++

```
// C++ program to illustrate above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return number of nodes left out
int answer(int n, int m)
{
    int i;
    for (i = 0; i <= n; i++) {

        // Condition to terminate, when
        // m edges are covered
        if ((i * (i - 1)) >= 2 * m)
            break;
    }

    return n - i;
}

// Driver Code
int main()
{
    int n = 7;
    int m = 6;
    cout << answer(n, m) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate above approach

import java.io.*;

class GFG {

// Function to return number of nodes left out
static int answer(int n, int m)
{
    int i;
    for (i = 0; i <= n; i++) {

        // Condition to terminate, when
        // m edges are covered
        if ((i * (i - 1)) >= 2 * m)
            break;
    }

    return n - i;
}

        // Driver Code
    public static void main (String[] args) {
        int n = 7;
    int m = 6;
    System.out.print( answer(n, m));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to illustrate
# above approach

# Function to return number of
# nodes left out
def answer(n, m):
    for i in range(0, n + 1, 1):

        # Condition to terminate, when
        # m edges are covered
        if ((i * (i - 1)) >= 2 * m):
            break

    return n - i

# Driver Code
if __name__ == '__main__':
    n = 7
    m = 6
    print(answer(n, m))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to illustrate
// above approach
using System;

class GFG
{

// Function to return number
// of nodes left out
static int answer(int n, int m)
{
    int i;
    for (i = 0; i <= n; i++)
    {

        // Condition to terminate, when
        // m edges are covered
        if ((i * (i - 1)) >= 2 * m)
            break;
    }

    return n - i;
}

// Driver Code
static public void Main ()
{
    int n = 7;
    int m = 6;
    Console.WriteLine(answer(n, m));
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to illustrate
// above approach

// Function to return number
// of nodes left out
function answer($n, $m)
{
    for ($i = 0; $i <= $n; $i++)
    {

        // Condition to terminate, when
        // m edges are covered
        if (($i * ($i - 1)) >= 2 * $m)
            break;
    }

    return $n - $i;
}

// Driver Code
$n = 7;
$m = 6;
echo answer($n, $m) + "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return number of nodes left out
function answer(n, m)
{
    let i;
    for (i = 0; i <= n; i++) {

        // Condition to terminate, when
        // m edges are covered
        if ((i * (i - 1)) >= 2 * m)
            break;
    }

    return n - i;
}

// driver program

    let n = 7;
    let m = 6;
    document.write( answer(n, m));

</script>
```

**Output:** 

```
3
```