# 使所有元素相等的最小移动次数

> 原文:[https://www . geesforgeks . org/最小移动次数-使所有元素相等/](https://www.geeksforgeeks.org/minimum-number-of-moves-to-make-all-elements-equal/)

给定一个包含 N 个元素和一个整数 k 的数组，允许在给定的数组上执行任意次以下操作:

*   在数组末尾插入第 K 个元素，删除数组的第一个元素。

任务是找到使数组所有元素相等所需的最小移动次数。如果不可能，打印-1。
**例:**

```
Input : arr[] = {1, 2, 3, 4}, K = 4
Output : 3
Step 1: 2 3 4 4
Step 2: 3 4 4 4
Step 3: 4 4 4 4

Input : arr[] = {2, 1}, K = 1
Output : -1
The array will keep alternating between 1, 2 and 
2, 1 regardless of how many moves you apply.
```

让我们看看关于原始数组的操作，首先，我们复制一个[k]到最后，然后是一个[k+1]，依此类推。为了确保我们只复制相等的元素，K 到 N 范围内的所有元素都应该相等。
所以，为了找到最小的移动次数，我们需要移除 1 到 K 范围内所有不等于 a[k]的元素。因此，我们需要继续应用操作，直到我们到达范围 1 到 K 中不等于 a[k]的最右边的项。
以下是上述方法的实施:

## C++

```
// C++ Program to find minimum number of
// operations to make all array Elements
// equal

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of operations
// to make all array Elements equal
int countMinimumMoves(int arr[], int n, int k)
{
    int i;

    // Check if it is possible or not
    // That is if all the elements from
    // index K to N are not equal
    for (i = k - 1; i < n; i++)
        if (arr[i] != arr[k - 1])
            return -1;

    // Find minimum number of moves
    for (i = k - 1; i >= 0; i--)
        if (arr[i] != arr[k - 1])
            return i + 1;

    // Elements are already equal
    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int K = 4;

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countMinimumMoves(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find minimum number of
// operations to make all array Elements
// equal

import java.io.*;

class GFG {

// Function to find minimum number of operations
// to make all array Elements equal
static int countMinimumMoves(int arr[], int n, int k)
{
    int i;

    // Check if it is possible or not
    // That is if all the elements from
    // index K to N are not equal
    for (i = k - 1; i < n; i++)
        if (arr[i] != arr[k - 1])
            return -1;

    // Find minimum number of moves
    for (i = k - 1; i >= 0; i--)
        if (arr[i] != arr[k - 1])
            return i + 1;

    // Elements are already equal
    return 0;
}

// Driver Code

    public static void main (String[] args) {
        int arr[] = { 1, 2, 3, 4 };
    int K = 4;

    int n = arr.length;

    System.out.print(countMinimumMoves(arr, n, K));
    }
}
// This code is contributed by shs
```

## 蟒蛇 3

```
# Python3 Program to find minimum
# number of operations to make all
# array Elements equal

# Function to find minimum number
# of operations to make all array
# Elements equal
def countMinimumMoves(arr, n, k) :

    # Check if it is possible or not
    # That is if all the elements from
    # index K to N are not equal
    for i in range(k - 1, n) :
        if (arr[i] != arr[k - 1]) :
            return -1

    # Find minimum number of moves
    for i in range(k - 1, -1, -1) :
        if (arr[i] != arr[k - 1]) :
            return i + 1

    # Elements are already equal
    return 0

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4 ]
    K = 4

    n = len(arr)

    print(countMinimumMoves(arr, n, K))

# This code is contributed by Ryuga
```

## C#

```
// C# Program to find minimum number of
// operations to make all array Elements
// equal
using System;

class GFG
{

// Function to find minimum number
// of operations to make all array
// Elements equal
static int countMinimumMoves(int []arr,
                             int n, int k)
{
    int i;

    // Check if it is possible or not
    // That is if all the elements from
    // index K to N are not equal
    for (i = k - 1; i < n; i++)
        if (arr[i] != arr[k - 1])
            return -1;

    // Find minimum number of moves
    for (i = k - 1; i >= 0; i--)
        if (arr[i] != arr[k - 1])
            return i + 1;

    // Elements are already equal
    return 0;
}

// Driver Code
public static void Main ()
{
    int []arr = { 1, 2, 3, 4 };
    int K = 4;

    int n = arr.Length;

    Console.Write(countMinimumMoves(arr, n, K));
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find minimum number of
// operations to make all array Elements
// equal

// Function to find minimum number
// of operations to make all array
// Elements equal
function countMinimumMoves($arr, $n, $k)
{

    // Check if it is possible or not
    // That is if all the elements from
    // index K to N are not equal
    for ($i = $k - 1; $i < $n; $i++)
        if ($arr[$i] != $arr[$k - 1])
            return -1;

    // Find minimum number of moves
    for ($i = $k - 1; $i >= 0; $i--)
        if ($arr[$i] != $arr[$k - 1])
            return $i + 1;

    // Elements are already equal
    return 0;
}

// Driver Code
$arr = array(1, 2, 3, 4);
$K = 4;

$n = sizeof($arr);

echo countMinimumMoves($arr, $n, $K);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find minimum number of
// operations to make all array Elements
// equal

// Function to find minimum number of operations
// to make all array Elements equal
function countMinimumMoves(arr, n, k)
{
    let i;

    // Check if it is possible or not
    // That is if all the elements from
    // index K to N are not equal
    for (i = k - 1; i < n; i++)
        if (arr[i] != arr[k - 1])
            return -1;

    // Find minimum number of moves
    for (i = k - 1; i >= 0; i--)
        if (arr[i] != arr[k - 1])
            return i + 1;

    // Elements are already equal
    return 0;
}

// Driver Code
    let arr = [ 1, 2, 3, 4 ];
    let K = 4;

    let n = arr.length;

    document.write(countMinimumMoves(arr, n, K));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)