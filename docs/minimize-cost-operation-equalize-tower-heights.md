# 最小化操作成本以均衡塔高

> 原文:[https://www . geesforgeks . org/minimum-cost-operation-equalize-tower-heights/](https://www.geeksforgeeks.org/minimize-cost-operation-equalize-tower-heights/)

给定高度 n(n)<=10000) towers as an array h[]; we need to bring every tower to same height by either adding or removing blocks in a tower. Every addition or removal operation costs a different value in a different tower. The objective is to minimize this cost.
**例:**

```
Input : Tower heights h[] = {1, 2, 3}
Costs of operations cost[] = {10, 100, 1000}
Output : 120
The heights can be equalized by either "Removing 
one block from 3 and adding one in 1" or "Adding
two blocks in 1 and adding one in 2". Since the 
cost of operation in tower 3 is 1000, the first
process would yield 1010 while the second one 
yields 120\. Since the second process yields the
lowest cost of operation, it is the required 
output.

Input : h[] = {7,1,5 }; 
        cost[] = { 1, 1, 1 }; 
Output : 6
abs(7-5) + abs(1-5) + abs(5-5) = 6 (taking 5
as final height)

Input : h[] = {2, 4, 8}
        cost[] = {10, 100, 1000}
Output : 460
```

**天真的方法**:天真的方法是找到每一个可能的操作集的成本，然后找到最小的操作成本。在最坏的情况下，这将使 O(n <sup>2</sup> )成为可能。
**最佳进场点**:这里最好的进场点似乎是二分搜索法。我们存储最小高度&在每一步中将我们的合成高度改变 2 倍。

## C++

```
// C++ program to minimize the cost of operation
// to bring all towers to same height.
#include <bits/stdc++.h>
using namespace std;

// Returns the cost of entire operation in bringing
// the height of all towers to equal height eq_h
long int costOfOperation(int n, int h[], int cost[],
                         int eq_h)
{
    // Initialize initial cost to 0
    long int c = 0;

    // Adding cost for each tower
    for (int i = 0; i < n; i++)
        c += abs(h[i] - eq_h) * cost[i];

    return c;
}

// Return the minimum possible cost of operation
// to bring all the towers of different height
// in height[0..n-1] to same height.
long long int Bsearch(int n, int h[], int cost[])
{
    long int max_h = *max_element(h, h + n);
    long int ans = LONG_MAX;

    // Do binary search for minimum cost
    long int high = 1 + max_h;
    long int low = 0;
    while (high > low) {
        int mid = (low + high) >> 1;

        // Cost below mid
        long int bm = (mid > 0) ?
                costOfOperation(n, h, cost, mid - 1) :
                LONG_MAX;

        // Cost at mid
        long int m = costOfOperation(n, h, cost, mid);

        // Cost above mid
        long int am = costOfOperation(n, h, cost, mid + 1);

        // ans should hold the minimum cost of operation
        ans = min(ans, m);

        // Search lower cost
        if (bm <= m)
            high = mid;

        // Search higher cost
        else if (am <= m)
            low = mid + 1;

        // If am > m and bm > m
        // then ans is m
        else
            return m;
    }

    return ans;
}

// Driver code
int main()
{
    int h[] = { 1, 2, 3 };
    int cost[] = { 10, 100, 1000 };
    int n = sizeof(h)/sizeof(h[0]);
    cout << Bsearch(n, h, cost);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize the cost of operation
// to bring all towers to same height.
import java.util.Arrays;
public class MinCostOp_Mintowerheight {

    // Returns the cost of entire operation in bringing
    // the height of all towers to equal height eq_h
    static long costOfOperation(int n, int h[], int cost[],
                                                int eq_h)
    {
        // Initialize initial cost to 0
        long c = 0;

        // Adding cost for each tower
        for (int i = 0; i < n; i++)
            c += Math.abs(h[i] - eq_h) * cost[i];

        return c;
    }

    // Return the minimum possible cost of operation
    // to bring all the towers of different height
    // in height[0..n-1] to same height.
    static long Bsearch(int n, int h[], int cost[])
    {
        int max_h =    Arrays.stream(h).max().getAsInt();
        long ans = Long.MAX_VALUE;

        // Do binary search for minimum cost
        long high = 1 + max_h;
        long low = 0;
        while (high > low) {
            int mid = (int) ((low + high) >> 1);

            // Cost below mid
            long bm = (mid > 0) ?
                    costOfOperation(n, h, cost, mid - 1) :
                    Long.MAX_VALUE;

            // Cost at mid
            long m = costOfOperation(n, h, cost, mid);

            // Cost above mid
            long am = costOfOperation(n, h, cost, mid + 1);

            // Break if the answer becomes equal to
            // minimum cost m
            if (ans == m)
                break;

            // ans should hold the minimum cost of operation
            ans = Long.min(ans, m);

            // Search lower cost
            if (bm <= m)
                high = mid;

            // Search higher cost
            else if (am <= m)
               low = mid + 1;

           // If am > m and bm > m
           // then ans is m
           else
               return m;
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int h[] = { 1, 2, 3 };
        int cost[] = { 10, 100, 1000 };
        int n = h.length;
        System.out.println(Bsearch(n, h, cost));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to minimize the cost of
# operation to bring all towers to same height.
import sys

# Returns the cost of entire operation in
# bringing the height of all towers to
# equal height eq_h
def costOfOperation(n, h,cost, eq_h):

    # Initialize initial cost to 0
    c = 0

    # Adding cost for each tower
    for i in range(0, n, 1):
        c += abs(h[i] - eq_h) * cost[i]

    return c

# Return the minimum possible cost of
# operation to bring all the towers of
# different height in height[0..n-1]
# to same height.
def Bsearch(n, h, cost):
    max_h = h[0]
    for i in range(len(h)):
        if(h[i] > max_h):
            max_h = h[i]
    ans = sys.maxsize

    # Do binary search for minimum cost
    high = 1 + max_h
    low = 0
    while (high > low):
        mid = (low + high) >> 1

        # Cost below mid
        if(mid > 0):
            bm = costOfOperation(n, h, cost, mid - 1)

        else:
            bm = sys.maxsize

        # Cost at mid
        m = costOfOperation(n, h, cost, mid)

        # Cost above mid
        am = costOfOperation(n, h, cost, mid + 1)

        # Break if the answer becomes equal
        # to minimum cost m
        if (ans == m):
            break

        # ans should hold the minimum cost
        # of operation
        ans = min(ans, m)

        # Search lower cost
        if (bm <= m):
            high = mid

        # Search higher cost
        elif(am <= m):
            low = mid + 1

        # If am > m and bm > m
        # then ans is m
        else :
            return m;

    return ans

# Driver code
if __name__ == '__main__':
    h = [1, 2, 3]
    cost = [10, 100, 1000]
    n = len(h)
    print(Bsearch(n, h, cost))

# This code is contributed by
# Sahil_shelangia
```

## C#

```
// C# program to minimize the
// cost of operation to bring
// all towers to same height.
using System;
using System.Linq;

public class MinCostOp_Mintowerheight
{

    // Returns the cost of entire
    // operation in bringing the height
    // of all towers to equal height eq_h
    static long costOfOperation(int n, int []h,
                                int []cost, int eq_h)
    {
        // Initialize initial cost to 0
        long c = 0;

        // Adding cost for each tower
        for (int i = 0; i < n; i++)
            c += Math.Abs(h[i] - eq_h) * cost[i];

        return c;
    }

    // Return the minimum possible
    // cost of operation to bring
    // all the towers of different height
    // in height[0..n-1] to same height.
    static long Bsearch(int n, int []h, int []cost)
    {
        int max_h = h.Max();
        long ans = long.MaxValue;

        // Do binary search for minimum cost
        long high = 1 + max_h;
        long low = 0;
        while (high > low)
        {
            int mid = (int) ((low + high) >> 1);

            // Cost below mid
            long bm = (mid > 0) ?
                    costOfOperation(n, h, cost, mid - 1) :
                    long.MaxValue;

            // Cost at mid
            long m = costOfOperation(n, h, cost, mid);

            // Cost above mid
            long am = costOfOperation(n, h, cost, mid + 1);

            // Break if the answer becomes
            //  equal to minimum cost m
            if (ans == m)
                break;

            // ans should hold the minimum
            // cost of operation
            ans = Math.Min(ans, m);

            // Search lower cost
            if (bm <= m)
                high = mid;

            // Search higher cost
            else if (am <= m)
                low = mid + 1;

            // If am > m and bm > m
            // then ans is m
            else
                return m;
        }

        return ans;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []h = { 1, 2, 3 };
        int []cost = { 10, 100, 1000 };
        int n = h.Length;
        Console.WriteLine(Bsearch(n, h, cost));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to minimize the cost
// of operation to bring all towers
// to same height.

// Returns the cost of entire operation
// in bringing the height of all towers
// to equal height eq_h
function costOfOperation($n, $h, $cost, $eq_h)
{
    // Initialize initial cost to 0
    $c = 0;

    // Adding cost for each tower
    for ($i = 0; $i < $n; $i++)
        $c += abs($h[$i] - $eq_h) * $cost[$i];

    return $c;
}

// Return the minimum possible cost of operation
// to bring all the towers of different height
// in height[0..n-1] to same height.
function Bsearch($n, $h, $cost)
{
    $max_h = max($h);
    $ans = PHP_INT_MAX;

    // Do binary search for minimum cost
    $high = 1 + $max_h;
    $low = 0;
    while ($high > $low)
    {
        $mid = ($low + $high) >> 1;

        // Cost below mid
        $bm = ($mid > 0) ?
               costOfOperation($n, $h, $cost, $mid - 1) :
                                           PHP_INT_MAX;

        // Cost at mid
        $m = costOfOperation($n, $h, $cost, $mid);

        // Cost above mid
        $am = costOfOperation($n, $h, $cost, $mid + 1);

        // Break if the answer becomes equal to
        // minimum cost m
        if ($ans == $m)
            break;

        // ans should hold the minimum
        // cost of operation
        $ans = min($ans, $m);

        // Search lower cost
        if ($bm <= $m)
            $high = $mid;

        // Search higher cost
        else if ($am <= $m)
            $low = $mid + 1;

        // If am > m and bm > m
        // then ans is m
        else
            return $m;
    }

    return $ans;
}

// Driver code
$h = array( 1, 2, 3 );
$cost = array( 10, 100, 1000 );
$n = count($h);
echo Bsearch($n, $h, $cost);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to minimize the cost
// of operation to bring all towers
// to same height.

// Returns the cost of entire operation
// in bringing the height of all towers
// to equal height eq_h
function costOfOperation(n, h, cost, eq_h)
{
    // Initialize initial cost to 0
    let c = 0;

    // Adding cost for each tower
    for (let i = 0; i < n; i++)
        c += Math.abs(h[i] - eq_h) * cost[i];

    return c;
}

// Return the minimum possible cost of operation
// to bring all the towers of different height
// in height[0..n-1] to same height.
function Bsearch(n, h, cost)
{
    let max_h = [...h].sort((a, b) => a - b)[h.length - 1];
    let ans = Number.MAX_SAFE_INTEGER;

    // Do binary search for minimum cost
    let high = 1 + max_h;
    let low = 0;
    while (high > low)
    {
        let mid = (low + high) >> 1;

        // Cost below mid
        let bm = (mid > 0) ?
            costOfOperation(n, h, cost, mid - 1) :
                                        PHP_INT_MAX;

        // Cost at mid
        let m = costOfOperation(n, h, cost, mid);

        // Cost above mid
        let am = costOfOperation(n, h, cost, mid + 1);

        // Break if the answer becomes equal to
        // minimum cost m
        if (ans == m)
            break;

        // ans should hold the minimum
        // cost of operation
        ans = Math.min(ans, m);

        // Search lower cost
        if (bm <= m)
            high = mid;

        // Search higher cost
        else if (am <= m)
            low = mid + 1;

        // If am > m and bm > m
        // then ans is m
        else
            return m;
    }

    return ans;
}

// Driver code
let h = new Array( 1, 2, 3 );
let cost = new Array( 10, 100, 1000 );
let n = h.length;
document.write(Bsearch(n, h, cost));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
120
```

本文由 [**Raghav Jajodia**](https://github.com/jajodiaraghav) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。