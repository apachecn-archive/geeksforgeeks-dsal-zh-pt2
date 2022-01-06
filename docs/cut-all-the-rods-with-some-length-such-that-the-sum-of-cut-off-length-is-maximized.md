# 将所有的杆切割成一定长度，使切割长度的总和最大化

> 原文:[https://www . geeksforgeeks . org/将所有棒切割成一定长度，以便最大化切割长度的总和/](https://www.geeksforgeeks.org/cut-all-the-rods-with-some-length-such-that-the-sum-of-cut-off-length-is-maximized/)

给定 N 根不同长度的棒。任务是切割具有某个最大整数高度“h”的所有杆，使得杆的切割长度之和最大化，并且如果不可能切割，则必须大于 M. Print -1。
**注:**杖不可斩也。
**示例:**

> **输入:** N = 7，M = 8，a[] = {1，2，3，5，4，7，6}
> **输出:** 3
> 棒 1 和棒 2 未被触及，棒 3，4，5，6，7 被切断，切断长度为(3-3) + (4-3) + (5-3) + (7-3) + (6-3)，等于大于 M = 8 的 10。
> **输入:** N = 4，M = 2，a[] = {1，2，3，3}
> **输出:** 2

**进场:**

*   [按升序排列数组](https://www.geeksforgeeks.org/sorting-algorithms/)
*   运行数值低=0、高=长度[n-1]的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，使 mid=(低+高)/2。
*   从 n-1 到 0 运行一个循环，将杆的高度**截止值**加到总和。
*   如果总和大于或等于 m，用 mid+1 指定低，否则高将更新为 mid。
*   二分搜索法完成后，答案将是低-1。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum possible
// length of rod which will be cut such that
// sum of cut off lengths will be maximum
#include <bits/stdc++.h>
using namespace std;

// Function to run Binary Search to
// find maximum cut off length
int binarySearch(int adj[], int target, int length)
{

    int low = 0;
    int high = adj[length - 1];
    while (low < high) {

        // f is the flag variable
        // sum is for the total length cutoff
        int f = 0, sum = 0;

        int mid = low + (high - low) / 2;

        // Loop from higher to lower
        // for optimization
        for (int i = length - 1; i >= 0; i--) {

            // Only if length is greater
            // than cut-off length
            if (adj[i] > mid) {
                sum = sum + adj[i] - mid;
            }

            // When total cut off length becomes greater
            // than desired cut off length
            if (sum >= target) {
                f = 1;
                low = mid + 1;
                break;
            }
        }

        // If flag variable is not set
        // Change high
        if (f == 0)
            high = mid;
    }

    // returning the maximum cut off length
    return low - 1;
}

// Driver Function
int main()
{
    int n1 = 7;
    int n2 = 8;

    int adj[] = { 1, 2, 3, 4, 5, 7, 6 };

    // Sorting the array in ascending order
    sort(adj, adj + n1);

    // Calling the binarySearch Function
    cout << binarySearch(adj, n2, n1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// maximum possible length
// of rod which will be cut
// such that sum of cut off
// lengths will be maximum
import java.util.*;

class GFG
{
// Function to run Binary
// Search to find maximum
// cut off length
static int binarySearch(int adj[],
                        int target,
                        int length)
{
int low = 0;
int high = adj[length - 1];
while (low < high)
{

    // f is the flag variable
    // sum is for the total
    // length cutoff
    int f = 0, sum = 0;

    int mid = low + (high - low) / 2;

    // Loop from higher to lower
    // for optimization
    for (int i = length - 1;
            i >= 0; i--)
    {

        // Only if length is greater
        // than cut-off length
        if (adj[i] > mid)
        {
            sum = sum + adj[i] - mid;
        }

        // When total cut off length
        // becomes greater than
        // desired cut off length
        if (sum >= target)
        {
            f = 1;
            low = mid + 1;
            break;
        }
    }

    // If flag variable is
    // not set Change high
    if (f == 0)
        high = mid;
}

// returning the maximum
// cut off length
return low - 1;
}

// Driver Code
public static void main(String args[])
{
    int n1 = 7;
    int n2 = 8;

    int adj[] = { 1, 2, 3, 4, 5, 7, 6 };

    // Sorting the array
    // in ascending order
    Arrays.sort(adj);

    // Calling the binarySearch Function
    System.out.println(binarySearch(adj, n2, n1));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find the
# maximum possible length of
# rod which will be cut such
# that sum of cut off lengths
# will be maximum

# Function to run Binary Search
# to find maximum cut off length
def binarySearch(adj, target, length) :
    low = 0
    high = adj[length - 1]

    while (low < high) :

        # f is the flag variable
        # sum is for the total
        # length cutoff

        # multiple assignments
        f, sum = 0, 0

        # take integer value
        mid = low + (high - low) // 2;

        # Loop from higher to lower
        # for optimization
        for i in range(length - 1, -1 , -1) :

            # Only if length is greater
            # than cut-off length
            if adj[i] > mid :
                sum = sum + adj[i] - mid

            # When total cut off length
            # becomes greater than
            # desired cut off length
            if sum >= target :
                f = 1
                low = mid + 1
                break

        # If flag variable is
        # not set. Change high
        if f == 0 :
            high = mid

    # returning the maximum
    # cut off length
    return low - 1

# Driver code
if __name__ == "__main__" :

    n1 = 7
    n2 = 8

    # adj = [1,2,3,3]
    adj = [ 1, 2, 3, 4, 5, 7, 6]

    # Sorting the array
    # in ascending order
    adj.sort()

    # Calling the binarySearch Function
    print(binarySearch(adj, n2, n1))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to find the
// maximum possible length
// of rod which will be cut
// such that sum of cut off
// lengths will be maximum
using System;

class GFG
{
// Function to run Binary
// Search to find maximum
// cut off length
static int binarySearch(int []adj,
                        int target,
                        int length)
{
int low = 0;
int high = adj[length - 1];
while (low < high)
{

    // f is the flag variable
    // sum is for the total
    // length cutoff
    int f = 0, sum = 0;

    int mid = low + (high - low) / 2;

    // Loop from higher to lower
    // for optimization
    for (int i = length - 1;
            i >= 0; i--)
    {

        // Only if length is greater
        // than cut-off length
        if (adj[i] > mid)
        {
            sum = sum + adj[i] - mid;
        }

        // When total cut off length
        // becomes greater than
        // desired cut off length
        if (sum >= target)
        {
            f = 1;
            low = mid + 1;
            break;
        }
    }

    // If flag variable is
    // not set Change high
    if (f == 0)
        high = mid;
}

// returning the maximum
// cut off length
return low - 1;
}

// Driver Code
public static void Main()
{
    int n1 = 7;
    int n2 = 8;

    int []adj = {1, 2, 3, 4, 5, 7, 6};

    // Sorting the array
    // in ascending order
    Array.Sort(adj);

    // Calling the binarySearch Function
    Console.WriteLine(binarySearch(adj, n2, n1));
}
}

// This code is contributed
// by Subhadeep Gupta
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// possible length of rod which will
// be cut such that sum of cut off
// lengths will be maximum

// Function to run Binary Search
// to find maximum cut off length
function binarySearch(&$adj, $target,
                            $length)
{
    $low = 0;
    $high = $adj[$length - 1];
    while ($low < $high)
    {

        // f is the flag variable
        // sum is for the total
        // length cutoff
        $f = 0;
        $sum = 0;

        $mid = $low + ($high - $low) / 2;

        // Loop from higher to lower
        // for optimization
        for ($i = $length - 1; $i >= 0; $i--)
        {

            // Only if length is greater
            // than cut-off length
            if ($adj[$i] > $mid)
            {
                $sum = $sum + $adj[$i] - $mid;
            }

            // When total cut off length becomes
            // greater than desired cut off length
            if ($sum >= $target)
            {
                $f = 1;
                $low = $mid + 1;
                break;
            }
        }

        // If flag variable is not
        // set Change high
        if ($f == 0)
            $high = $mid;
    }

    // returning the maximum cut off length
    return $low - 1;
}

// Driver Code
$n1 = 7;
$n2 = 8;

$adj = array( 1, 2, 3, 4, 5, 7, 6 );

// Sorting the array in ascending order
sort($adj);

// Calling the binarySearch Function
echo (int)binarySearch($adj, $n2, $n1);

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// maximum possible length
// of rod which will be cut
// such that sum of cut off
// lengths will be maximum

// Function to run Binary
// Search to find maximum
// cut off length
function binarySearch(adj,target,length)
{
let low = 0;
let high = adj[length - 1];
while (low < high)
{

    // f is the flag variable
    // sum is for the total
    // length cutoff
    let f = 0, sum = 0;

    let mid = low + Math.floor((high - low) / 2);

    // Loop from higher to lower
    // for optimization
    for (let i = length - 1;
            i >= 0; i--)
    {

        // Only if length is greater
        // than cut-off length
        if (adj[i] > mid)
        {
            sum = sum + adj[i] - mid;
        }

        // When total cut off length
        // becomes greater than
        // desired cut off length
        if (sum >= target)
        {
            f = 1;
            low = mid + 1;
            break;
        }
    }

    // If flag variable is
    // not set Change high
    if (f == 0)
        high = mid;
}

// returning the maximum
// cut off length
return low - 1;
}

// Driver Code   
let n1 = 7;
let n2 = 8;
let adj=[1, 2, 3, 4, 5, 7, 6 ];

// Sorting the array
// in ascending order
adj.sort(function(a,b){return a-b;});

// Calling the binarySearch Function
document.write(binarySearch(adj, n2, n1));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(1)