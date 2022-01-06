# 增量/减量操作的最小次数，使得数组包含从 1 到 N 的所有元素

> 原文:[https://www . geesforgeks . org/最小增量-减量-操作数-这样-数组-包含-所有元素-从-1 到-n/](https://www.geeksforgeeks.org/minimum-number-of-increment-decrement-operations-such-that-array-contains-all-elements-from-1-to-n/)

给定一个由 N 个元素组成的数组，任务是通过使用以下操作最少次数将其转换为置换(从 1 到 N 的每个数字恰好出现一次):

*   递增任意数字。
*   递减任意数字。

**示例:**

```
Input: arr[] = {1, 1, 4}
Output: 2
The array can be converted into [1, 2, 3]
by adding 1 to the 1st index i.e. 1 + 1 = 2
and decrementing 2nd index by 1 i.e. 4- 1 = 3

Input: arr[] = {3, 0}
Output: 2

The array can be converted into [2, 1]
```

**方法:**为了最小化移动/操作的数量，对给定的数组进行排序，并生成一个[i] = i+1(基于 0)的数组，该数组将为每个元素取 **abs(i+1-a[i])** 个操作数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
long long minimumMoves(int a[], int n)
{

    long long operations = 0;

    // Sort the given array
    sort(a, a + n);

    // Count operations by assigning a[i] = i+1
    for (int i = 0; i < n; i++)
        operations += abs(a[i] - (i + 1));

    return operations;
}

// Driver Code
int main()
{
    int arr[] = { 5, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minimumMoves(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;
class solution
{
// Function to find the minimum operations
static long minimumMoves(int a[], int n)
{

    long operations = 0;

    // Sort the given array
    Arrays.sort(a);

    // Count operations by assigning a[i] = i+1
    for (int i = 0; i < n; i++)
        operations += (long)Math.abs(a[i] - (i + 1));

    return operations;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 5, 3, 2 };
    int n = arr.length;

    System.out.print(minimumMoves(arr, n));

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to find the minimum operations
def minimumMoves(a, n):

    operations = 0
    # Sort the given array
    a.sort(reverse = False)

    # Count operations by assigning a[i] = i+1
    for i in range(0,n,1):
        operations = operations + abs(a[i] - (i + 1))

    return operations

# Driver Code
if __name__ == '__main__':
    arr = [ 5, 3, 2 ]
    n = len(arr)

    print(minimumMoves(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to find the minimum operations
static long minimumMoves(int []a, int n)
{

    long operations = 0;

    // Sort the given array
    Array.Sort(a);

    // Count operations by assigning
    // a[i] = i+1
    for (int i = 0; i < n; i++)
        operations += (long)Math.Abs(a[i] - (i + 1));

    return operations;
}

// Driver Code
static public void Main ()
{
    int []arr = { 5, 3, 2 };
    int n = arr.Length;

    Console.WriteLine(minimumMoves(arr, n));
}
}

// This code is contributed by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
// Function to find the minimum operations

function minimumMoves($a, $n)
{
    $operations = 0;

    // Sort the given array
    sort($a);

    // Count operations by assigning
    // a[i] = i+1
    for ($i = 0; $i < $n; $i++)
        $operations += abs($a[$i] -
                          ($i + 1));

    return $operations;
}

// Driver Code
$arr = array( 5, 3, 2 );
$n = sizeof($arr);

echo minimumMoves($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the minimum operations
function minimumMoves(a, n)
{
    let operations = 0;

    // Sort the given array
    a.sort();

    // Count operations by assigning
    // a[i] = i+1
    for(let i = 0; i < n; i++)
        operations += Math.abs(a[i] - (i + 1));

    return operations;
}

// Driver code
let arr = [ 5, 3, 2 ];
let n = arr.length;

document.write(minimumMoves(arr, n));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(NlogN)