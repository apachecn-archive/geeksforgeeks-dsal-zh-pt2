# 连接表示为数组的加权节点的最小成本

> 原文:[https://www . geesforgeks . org/最低成本-连接-加权-节点-表示-阵列/](https://www.geeksforgeeks.org/minimum-cost-connect-weighted-nodes-represented-array/)

给定 N 个元素(节点)的数组，其中每个元素都是该节点的权重。连接两个节点需要花费它们重量的乘积。您必须将每个节点与其他节点连接起来(直接或间接)。输出所需的最低成本。
**例:**

```
Input : a[] = {6, 2, 1, 5}
Output :  13
Explanation : 
Here, we connect the nodes as follows:
connect a[0] and a[2], cost = 6*1 = 6,
connect a[2] and a[1], cost = 1*2 = 2,
connect a[2] and a[3], cost = 1*5 = 5.
every node is reachable from every other node:
Total cost = 6+2+5 = 13.

Input  : a[] = {5, 10}
Output : 50
Explanation : connections:
connect a[0] and a[1], cost = 5*10 = 50,
Minimum cost = 50\. 
```

我们需要做一些观察，我们必须做一个有 N-1 条边的连通图。由于输出将是两个数乘积的和，我们必须最小化和方程中每个项的乘积。我们怎么做？显然，选择数组中的最小元素，并将其相互连接。通过这种方式，我们可以从一个特定的节点到达每隔一个节点。
Let，最小元素= a[i]，(让它的指数为 0)
**最小成本**
那么，答案是*最小元素与除最小元素之外的所有元素之和的乘积。*

## C++

```
// cpp code for Minimum Cost Required to connect weighted nodes
#include <bits/stdc++.h>
using namespace std;
int minimum_cost(int a[], int n)
{
    int mn = INT_MAX;
    int sum = 0;
    for (int i = 0; i < n; i++) {

        // To find the minimum element
        mn = min(a[i], mn);

        // sum of all the elements
        sum += a[i];
    }

    return mn * (sum - mn);
}

// Driver code
int main()
{
    int a[] = { 4, 3, 2, 5 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minimum_cost(a, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Minimum Cost Required to
// connect weighted nodes

import java.io.*;

class GFG {

    static int minimum_cost(int a[], int n)
    {

        int mn = Integer.MAX_VALUE;
        int sum = 0;

        for (int i = 0; i < n; i++) {

            // To find the minimum element
            mn = Math.min(a[i], mn);

            // sum of all the elements
            sum += a[i];
        }

        return mn * (sum - mn);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 4, 3, 2, 5 };
        int n = a.length;

        System.out.println(minimum_cost(a, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 code for Minimum Cost
# Required to connect weighted nodes
import sys

def minimum_cost(a, n):

    mn = sys.maxsize
    sum = 0
    for i in range(n):

        # To find the minimum element
        mn = min(a[i], mn)

        # sum of all the elements
        sum += a[i]

    return mn * (sum - mn)

# Driver code
if __name__ == "__main__":

    a = [ 4, 3, 2, 5 ]
    n = len(a)
    print(minimum_cost(a, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code for Minimum Cost Required
// to connect weighted nodes
using System;

class GFG {

    // Function to calculate minimum cost
    static int minimum_cost(int []a, int n)
    {

        int mn = int.MaxValue;
        int sum = 0;

        for (int i = 0; i < n; i++)
        {

            // To find the minimum element
            mn = Math.Min(a[i], mn);

            // sum of all the elements
            sum += a[i];
        }

        return mn * (sum - mn);
    }

    // Driver code
    public static void Main()
    {
        int []a = {4, 3, 2, 5};
        int n = a.Length;

        Console.WriteLine(minimum_cost(a, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for Minimum Cost Required
// to connect weighted nodes
function minimum_cost($a, $n)
{
    $mn = PHP_INT_MAX;
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // To find the minimum element
        $mn = min($a[$i], $mn);

        // sum of all the elements
        $sum += $a[$i];
    }

    return $mn * ($sum - $mn);
}

// Driver code
$a = array( 4, 3, 2, 5 );
$n = sizeof($a);
echo minimum_cost($a, $n), "\n";

// This code is contributed
// by Kiit_Tush
?>
```

## java 描述语言

```
<script>
    // Javascript code for Minimum Cost Required
    // to connect weighted nodes

    // Function to calculate minimum cost
    function minimum_cost(a, n)
    {

        let mn = Number.MAX_VALUE;
        let sum = 0;

        for (let i = 0; i < n; i++)
        {

            // To find the minimum element
            mn = Math.min(a[i], mn);

            // sum of all the elements
            sum += a[i];
        }

        return mn * (sum - mn);
    }

    let a = [4, 3, 2, 5];
    let n = a.length;

    document.write(minimum_cost(a, n));

</script>
```

**输出:**

```
  24
```

**时间复杂度:** O(n)。
本文由**哈沙·莫加利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。