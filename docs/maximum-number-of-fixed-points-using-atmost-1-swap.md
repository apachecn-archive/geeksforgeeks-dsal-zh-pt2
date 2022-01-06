# 使用 atmost 1 交换的最大固定点数

> 原文:[https://www . geesforgeks . org/最大固定点数-使用-atmat-1-swap/](https://www.geeksforgeeks.org/maximum-number-of-fixed-points-using-atmost-1-swap/)

给定 N 个元素的排列(元素在 0 到 N-1 的范围内)。A **不动点**是一个数值与指数相同的指数(即**a【I】= I**)。您可以进行 atmost 1 交换。找到你能得到的最大固定点数。
**例** :

```
Input : N = 5
        arr[] = {0, 1, 3, 4, 2}
Output : 3
2 and 3 can be swapped to get:
0 1 2 4 3
which has 3 fixed points.

Input : N = 5
        a[] = {0, 1, 2, 4, 3}
Output : 5 
```

因为我们只允许进行 1 次交换，所以固定点数可以增加 2 个。
让我们有一个数组 pos，它保存输入数组中每个元素的位置。现在，我们遍历数组，有以下情况:

*   如果，a[i] = i .我们可以简单地增加计数，然后继续前进。
*   If，pos[i] = a[i]，这意味着交换 2 个项将使 I 和 a[i]固定不变，因此计数增加 2。请记住，交换可以在大气中进行一次。

在遍历结束时，如果我们没有进行任何交换，这意味着我们的交换不能将计数增加 2，所以现在如果至少有 2 个元素不是固定点，我们可以进行交换，将计数增加 1，即使其中一个点成为固定点。
以下是上述方法的实现:

## C++

```
// CPP program to find maximum number of
// fixed points using atmost 1 swap

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum number of
// fixed points using atmost 1 swap
int maximumFixedPoints(int a[], int n)
{
    int i, pos[n], count = 0, swapped = 0;

    // Store position of each element in
    // input array
    for (i = 0; i < n; i++)
        pos[a[i]] = i;

    for (i = 0; i < n; i++) {

        // If fixed point, incremenmt count
        if (a[i] == i)
            count++;

        // Else check if swapping increments
        // count by 2
        else if (swapped == 0 && pos[i] == a[i]) {
            count += 2;
            swapped = 1;
        }
    }

    // If not swapped yet and elements remaining
    if (swapped == 0 && count < n - 1)
        count++;

    return count;
}

// Driver Code
int main()
{
    int a[] = { 0, 1, 3, 4, 2 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << maximumFixedPoints(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of
// fixed points using atmost 1 swap
import java.io.*;

class GFG {

// Function to find maximum number of
// fixed points using atmost 1 swap
static int maximumFixedPoints(int a[], int n)
{
    int i, count = 0, swapped = 0;
    int pos[] = new int[n];

    // Store position of each element in
    // input array
    for (i = 0; i < n; i++)
        pos[a[i]] = i;

    for (i = 0; i < n; i++) {

        // If fixed point, incremenmt count
        if (a[i] == i)
            count++;

        // Else check if swapping increments
        // count by 2
        else if (swapped == 0 && pos[i] == a[i]) {
            count += 2;
            swapped = 1;
        }
    }

    // If not swapped yet and elements remaining
    if (swapped == 0 && count < n - 1)
        count++;

    return count;
}

// Driver Code

    public static void main (String[] args) {
            int []a= { 0, 1, 3, 4, 2 };

    int n = a.length;

    System.out.println(maximumFixedPoints(a, n));
    }
}

// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 program to find the maximum number
# of fixed points using at most 1 swap

# Function to find maximum number of
# fixed points using atmost 1 swap
def maximumFixedPoints(a, n):

    pos = [None] * n
    count, swapped = 0, 0

    # Store position of each element
    # in input array
    for i in range(0, n):
        pos[a[i]] = i

    for i in range(0, n):

        # If fixed point, incremenmt count
        if a[i] == i:
            count += 1

        # Else check if swapping increments
        # count by 2
        elif swapped == 0 and pos[i] == a[i]:
            count += 2
            swapped = 1

    # If not swapped yet and elements remaining
    if swapped == 0 and count < n - 1:
        count += 1

    return count

# Driver Code
if __name__ == "__main__":

    a = [0, 1, 3, 4, 2]
    n = len(a)

    print(maximumFixedPoints(a, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find maximum number of
// fixed points using atmost 1 swap
using System;

class Program {

// Function to find maximum number of
// fixed points using atmost 1 swap
static int maximumFixedPoints(int []a, int n)
{
    int i, count = 0, swapped = 0;
    int []pos = new int[n];

    // Store position of each element in
    // input array
    for (i = 0; i < n; i++)
        pos[a[i]] = i;

    for (i = 0; i < n; i++) {

        // If fixed point, incremenmt count
        if (a[i] == i)
            count++;

        // Else check if swapping increments
        // count by 2
        else if (swapped == 0 && pos[i] == a[i]) {
            count += 2;
            swapped = 1;
        }
    }

    // If not swapped yet and elements remaining
    if (swapped == 0 && count < n - 1)
        count++;

    return count;
}

    // Driver Code
    static void Main()
    {
        int []a= { 0, 1, 3, 4, 2 };

        int n = a.Length;

        Console.WriteLine(maximumFixedPoints(a, n));
    }
}

// This code is contributed
// by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum number of
// fixed points using atmost 1 swap

// Function to find maximum number of
// fixed points using atmost 1 swap
function  maximumFixedPoints($a, $n)
{
    $i; $pos[$n]=array();
    $count = 0;
    $swapped = 0;

    // Store position of each element in
    // input array
    for ($i = 0; $i < $n; $i++)
        $pos[$a[$i]] = $i;

    for ($i = 0; $i < $n; $i++) {

        // If fixed point, incremenmt count
        if ($a[$i] == $i)
            $count++;

        // Else check if swapping increments
        // count by 2
        else if ($swapped == 0 && $pos[$i] == $a[$i]) {
            $count += 2;
            $swapped = 1;
        }
    }

    // If not swapped yet and elements remaining
    if ($swapped == 0 && $count < $n - 1)
        $count++;

    return $count;
}

// Driver Code
     $a = array (0, 1, 3, 4, 2 );
        $n = sizeof($a) / sizeof($a[0]);

    echo maximumFixedPoints($a, $n);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum number of
    // fixed points using atmost 1 swap

    // Function to find maximum number of
    // fixed points using atmost 1 swap
    function maximumFixedPoints(a, n)
    {
        let i, count = 0, swapped = 0;
        let pos = new Array(n);

        // Store position of each element in
        // input array
        for (i = 0; i < n; i++)
            pos[a[i]] = i;

        for (i = 0; i < n; i++) {

            // If fixed point, incremenmt count
            if (a[i] == i)
                count++;

            // Else check if swapping increments
            // count by 2
            else if (swapped == 0 && pos[i] == a[i]) {
                count += 2;
                swapped = 1;
            }
        }

        // If not swapped yet and elements remaining
        if (swapped == 0 && count < n - 1)
            count++;

        return count;
    }

    let a= [ 0, 1, 3, 4, 2 ];

    let n = a.length;

    document.write(maximumFixedPoints(a, n));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)