# 要更改的最小元素，以便对于索引 I，左侧的所有元素都是-ve，右侧的所有元素都是+ve

> 原文:[https://www . geeksforgeeks . org/最少要更改的元素以至于左边的所有元素都是 ve，右边的所有元素都是 ve/](https://www.geeksforgeeks.org/minimum-elements-to-change-so-that-for-an-index-i-all-elements-on-the-left-are-ve-and-all-elements-on-the-right-are-ve/)

给定一个大小为 **n** 的数组 **arr** ，任务是找到应该更改的元素的最小数量(元素值可以更改为任何值)，以便存在一个索引 **0 ≤ i ≤ n-2** ，这样:

1.  范围 **0** 至 **i** (含)的所有数字均为 **< 0** 。
2.  范围 **i+1** 至 **n-1** (含)内的所有数字均为 **> 0** 。

**例:**

> **输入:** arr[] = {-1，-2，-3，3，-5，3，4}
> **输出:** 1
> 变为-5 到 5，数组变为{-1，-2，-3，3，5，3，4}
> **输入:** arr[] = {3，-5}
> **输出:** 2
> 变为 3 到-3 和-5 到 5

**方法:**固定 **i** 的值，我们需要做哪些改变才能使指数 **i** 成为所需的指数？将 **i** 左侧的所有正元素变为负，将 **i** 右侧的所有负元素变为正。因此，所需的操作数将是:
**(I 左边的正项数)+(I 右边的负项数)**
为了找到所需的项，我们可以使用后缀和来预先计算它们。
因此，我们尝试每个 **i** 作为所需的指标，并选择需要最小变化的指标。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of required changes
int minimumChanges(int n, int a[])
{
    int i, sf[n + 1];
    sf[n] = 0;
    for (i = n - 1; i >= 0; i--) {
        sf[i] = sf[i + 1];
        if (a[i] <= 0)
            sf[i]++;
    }

    // number of elements >=0 in prefix
    int pos = 0;

    // Minimum elements to change
    int mn = n;
    for (i = 0; i < n - 1; i++) {
        if (a[i] >= 0)
            pos++;
        mn = min(mn, pos + sf[i + 1]);
    }
    return mn;
}

// Driver Program to test above function
int main()
{
    int a[] = { -1, -2, -3, 3, -5, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minimumChanges(n, a);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// Function to return the minimum number
// of required changes
static int minimumChanges(int n, int a[])
{
    int i;
    int []sf= new int[n+1];
    sf[n] = 0;
    for (i = n - 1; i >= 0; i--) {
        sf[i] = sf[i + 1];
        if (a[i] <= 0)
            sf[i]++;
    }

    // number of elements >=0 in prefix
    int pos = 0;

    // Minimum elements to change
    int mn = n;
    for (i = 0; i < n - 1; i++) {
        if (a[i] >= 0)
            pos++;
        mn = Math.min(mn, pos + sf[i + 1]);
    }
    return mn;
}

    // Driver Program to test above function
    public static void main (String[] args) {
    int []a = { -1, -2, -3, 3, -5, 3, 4 };
    int n = a.length;
    System.out.println( minimumChanges(n, a));
    }
}
// This code is contributed by inder_verma.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum
# number of required changes
def minimumChanges(n, a):

    sf = [0] * (n + 1)
    sf[n] = 0
    for i in range(n - 1, -1, -1) :
        sf[i] = sf[i + 1]
        if (a[i] <= 0):
            sf[i] += 1

    # number of elements >=0 in prefix
    pos = 0

    # Minimum elements to change
    mn = n
    for i in range(n - 1) :
        if (a[i] >= 0):
            pos += 1
        mn = min(mn, pos + sf[i + 1])

    return mn

# Driver Code
if __name__ == "__main__":

    a = [ -1, -2, -3, 3, -5, 3, 4 ]
    n = len(a)
    print(minimumChanges(n, a))

# This code is contributed
# by ChitraNayal
```

## C#

```
using System;

// C# implementation of the approach

public class GFG
{

// Function to return the minimum number 
// of required changes
public static int minimumChanges(int n, int[] a)
{
    int i;
    int[] sf = new int[n + 1];
    sf[n] = 0;
    for (i = n - 1; i >= 0; i--)
    {
        sf[i] = sf[i + 1];
        if (a[i] <= 0)
        {
            sf[i]++;
        }
    }

    // number of elements >=0 in prefix
    int pos = 0;

    // Minimum elements to change
    int mn = n;
    for (i = 0; i < n - 1; i++)
    {
        if (a[i] >= 0)
        {
            pos++;
        }
        mn = Math.Min(mn, pos + sf[i + 1]);
    }
    return mn;
}

    // Driver Program to test above function
    public static void Main(string[] args)
    {
    int[] a = new int[] {-1, -2, -3, 3, -5, 3, 4};
    int n = a.Length;
    Console.WriteLine(minimumChanges(n, a));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number
// of required changes
function minimumChanges($n, $a)
{
    $i;
    $sf[$n + 1] = array();
    $sf[$n] = 0;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        $sf[$i] = $sf[$i + 1];
        if ($a[$i] <= 0)
            $sf[$i]++;
    }

    // number of elements >=0 in prefix
    $pos = 0;

    // Minimum elements to change
    $mn = $n;
    for ($i = 0; $i < $n - 1; $i++)
    {
        if ($a[$i] >= 0)
            $pos++;
        $mn = min($mn, $pos + $sf[$i + 1]);
    }
    return $mn;
}

// Driver Code
$a = array(-1, -2, -3, 3, -5, 3, 4 );
$n = sizeof($a);
echo minimumChanges($n, $a);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the minimum number 
    // of required changes
    function minimumChanges(n, a)
    {
        let i;
        let sf = new Array(n + 1);
        sf.fill(0);
        sf[n] = 0;
        for (i = n - 1; i >= 0; i--)
        {
            sf[i] = sf[i + 1];
            if (a[i] <= 0)
            {
                sf[i]++;
            }
        }

        // number of elements >=0 in prefix
        let pos = 0;

        // Minimum elements to change
        let mn = n;
        for (i = 0; i < n - 1; i++)
        {
            if (a[i] >= 0)
            {
                pos++;
            }
            mn = Math.min(mn, pos + sf[i + 1]);
        }
        return mn;
    }

    let a = [-1, -2, -3, 3, -5, 3, 4];
    let n = a.length;
    document.write(minimumChanges(n, a));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n)