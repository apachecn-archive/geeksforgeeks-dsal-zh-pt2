# 计算减少给定数量所需的操作次数

> 原文:[https://www . geesforgeks . org/count-需要减少给定数量的操作数/](https://www.geeksforgeeks.org/count-the-number-of-operations-required-to-reduce-the-given-number/)

给定一个整数 **k** 和一个数组**op【】**，在一次操作中**op【0】**将被加到 **k** 上，然后在第二次操作中**k = k+op【1】**以循环方式依次类推，直到 **k > 0** 。任务是打印 **k** 降为 **≤ 0** 的操作号。如果给定操作无法减少 **k** ，则打印 **-1** 。
**例:**

> **输入:** op[] = {-60，10，-100}，k = 100
> **输出:** 3
> 运算 1:100–60 = 40
> 运算 2: 40 + 10 = 50
> 运算 3:50–100 =-50
> **输入:** op[] = {1，1，-1}，k = 10
> **输出:**

**方法:**对数字 **k** 计算所有操作可以执行的次数，而不需要实际减少就可以得到结果。然后更新**计数=次数* n** ，其中 **n** 为操作次数。现在，对于剩余的操作，逐个执行每个操作，并增加**计数**。第一次操作当 k 降低到 **≤ 0** 时，打印**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

int operations(int op[], int n, int k)
    {
        int i, count = 0;

        // To store the normalized value
        // of all the operations
        int nVal = 0;

        // Minimum possible value for
        // a series of operations
        int minimum = INT_MAX;
        for (i = 0; i < n; i++)
        {
            nVal += op[i];
            minimum  = min(minimum , nVal);

            // If k can be reduced with
            // first (i + 1) operations
            if ((k + nVal) <= 0)
                return (i + 1);
        }

        // Impossible to reduce k
        if (nVal >= 0)
            return -1;

        // Number of times all the operations
        // can be performed on k without
        // reducing it to <= 0
        int times = (k - abs(minimum )) / abs(nVal);

        // Perform operations
        k = (k - (times * abs(nVal)));
        count = (times * n);

        // Final check
        while (k > 0) {
            for (i = 0; i < n; i++) {
                k = k + op[i];
                count++;
                if (k <= 0)
                    break;
            }
        }

        return count;
    }

// Driver code
int main() {

        int op[] = { -60, 65, -1, 14, -25 };
        int n = sizeof(op)/sizeof(op[0]);
        int k = 100000;

        cout << operations(op, n, k) << endl;
}
// This code is contributed by Ryuga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int operations(int op[], int n, int k)
    {
        int i, count = 0;

        // To store the normalized value
        // of all the operations
        int nVal = 0;

        // Minimum possible value for
        // a series of operations
        int min = Integer.MAX_VALUE;
        for (i = 0; i < n; i++) {
            nVal += op[i];
            min = Math.min(min, nVal);

            // If k can be reduced with
            // first (i + 1) operations
            if ((k + nVal) <= 0)
                return (i + 1);
        }

        // Impossible to reduce k
        if (nVal >= 0)
            return -1;

        // Number of times all the operations
        // can be performed on k without
        // reducing it to <= 0
        int times = (k - Math.abs(min)) / Math.abs(nVal);

        // Perform operations
        k = (k - (times * Math.abs(nVal)));
        count = (times * n);

        // Final check
        while (k > 0) {
            for (i = 0; i < n; i++) {
                k = k + op[i];
                count++;
                if (k <= 0)
                    break;
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int op[] = { -60, 65, -1, 14, -25 };
        int n = op.length;
        int k = 100000;

        System.out.print(operations(op, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def operations(op, n, k):

    i, count = 0, 0

    # To store the normalized value
    # of all the operations
    nVal = 0

    # Minimum possible value for
    # a series of operations
    minimum = 10**9
    for i in range(n):
        nVal += op[i]
        minimum = min(minimum , nVal)

        # If k can be reduced with
        # first (i + 1) operations
        if ((k + nVal) <= 0):
            return (i + 1)

    # Impossible to reduce k
    if (nVal >= 0):
        return -1

    # Number of times all the operations
    # can be performed on k without
    # reducing it to <= 0
    times = (k - abs(minimum )) // abs(nVal)

    # Perform operations
    k = (k - (times * abs(nVal)))
    count = (times * n)

    # Final check
    while (k > 0):
        for i in range(n):
            k = k + op[i]
            count += 1
            if (k <= 0):
                break

    return count

# Driver code
op = [-60, 65, -1, 14, -25]
n = len(op)
k = 100000

print(operations(op, n, k))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int operations(int []op, int n, int k)
    {
        int i, count = 0;

        // To store the normalized value
        // of all the operations
        int nVal = 0;

        // Minimum possible value for
        // a series of operations
        int min = int.MaxValue;
        for (i = 0; i < n; i++)
        {
            nVal += op[i];
            min = Math.Min(min, nVal);

            // If k can be reduced with
            // first (i + 1) operations
            if ((k + nVal) <= 0)
                return (i + 1);
        }

        // Impossible to reduce k
        if (nVal >= 0)
            return -1;

        // Number of times all the operations
        // can be performed on k without
        // reducing it to <= 0
        int times = (k - Math.Abs(min)) / Math.Abs(nVal);

        // Perform operations
        k = (k - (times * Math.Abs(nVal)));
        count = (times * n);

        // Final check
        while (k > 0)
        {
            for (i = 0; i < n; i++)
            {
                k = k + op[i];
                count++;
                if (k <= 0)
                    break;
            }
        }

        return count;
    }

    // Driver code
    static void Main()
    {
        int []op = { -60, 65, -1, 14, -25 };
        int n = op.Length;
        int k = 100000;

        Console.WriteLine(operations(op, n, k));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
function operations($op, $n, $k)
{
    $count = 0;

    // To store the normalized value
    // of all the operations
    $nVal = 0;

    // Minimum possible value for
    // a series of operations
    $minimum = PHP_INT_MAX;
    for ($i = 0; $i < $n; $i++)
    {
        $nVal += $op[$i];
        $minimum = min($minimum , $nVal);

        // If k can be reduced with
        // first (i + 1) operations
        if (($k + $nVal) <= 0)
            return ($i + 1);
    }

    // Impossible to reduce k
    if ($nVal >= 0)
        return -1;

    // Number of times all the operations
    // can be performed on k without
    // reducing it to <= 0
    $times = round(($k - abs($minimum )) /
                         abs($nVal));

    // Perform operations
    $k = ($k - ($times * abs($nVal)));
    $count = ($times * $n);

    // Final check
    while ($k > 0)
    {
        for ($i = 0; $i < $n; $i++)
        {
            $k = $k + $op[$i];
            $count++;
            if ($k <= 0)
                break;
        }
    }

    return $count;
}

// Driver code
$op = array(-60, 65, -1, 14, -25 );
$n = sizeof($op);
$k = 100000;

echo operations($op, $n, $k);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

function operations(op,n,k)
{
    let i, count = 0;

        // To store the normalized value
        // of all the operations
        let nVal = 0;

        // Minimum possible value for
        // a series of operations
        let min = Number.MAX_VALUE;
        for (i = 0; i < n; i++) {
            nVal += op[i];
            min = Math.min(min, nVal);

            // If k can be reduced with
            // first (i + 1) operations
            if ((k + nVal) <= 0)
                return (i + 1);
        }

        // Impossible to reduce k
        if (nVal >= 0)
            return -1;

        // Number of times all the operations
        // can be performed on k without
        // reducing it to <= 0
        let times = Math.floor((k - Math.abs(min)) / Math.abs(nVal));

        // Perform operations
        k = (k - (times * Math.abs(nVal)));
        count = (times * n);

        // Final check
        while (k > 0) {
            for (i = 0; i < n; i++) {
                k = k + op[i];
                count++;
                if (k <= 0)
                    break;
            }
        }

        return count;
}

    // Driver code
    let op=[-60, 65, -1, 14, -25];
    let n = op.length;
    let k = 100000;
    document.write(operations(op, n, k));

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
71391
```