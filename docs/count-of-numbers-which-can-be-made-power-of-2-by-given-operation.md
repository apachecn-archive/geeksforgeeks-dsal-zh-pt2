# 通过给定操作

可以 2 的幂的数的计数

> 原文:[https://www . geeksforgeeks . org/可通过给定操作获得 2 次方的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-which-can-be-made-power-of-2-by-given-operation/)

给定一个数组**arr【】**，任务是通过以下操作计算可以使**的 2 的幂**的数字:
T5】1 可以加到任意元素 atmost 一次，如果它还不是 2 的幂的话。

**示例:**

> **输入:** arr[] = {2，3，7，9，15}
> **输出:** 4
> 3，7，15 加 1 可以做 2 的幂，2 已经是 2 的幂了
> 
> **输入:** arr[] = {5，6，9，3，1}
> 输出: 2

**方法:**遍历数组，检查当前元素是否是 2 的幂，如果是则更新**计数=计数+ 1** 。如果不是 2 的幂，则检查一个更大的元素，即 **arr[i] + 1** 。要检查一个元素是否是 2 的幂:

*   **天真法**就是反复**将**元素除以 **2** ，直到给出 **0** 或者 **1** 作为余数。如果余数是 **1** ，那么它是 2 的幂，否则它不是 2 的幂。
*   **高效法:**如果**X&(X–1)= 0**那么 **X** 就是 2 的幂。
    说， **X = 16 = 10000** 和**X–1 = 15 = 01111**那么**X&(X–1)= 10000&01111 = 0**即 **X = 16** 是 2 的幂。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if x is a power of 2
bool isPowerOfTwo(int x)
{
    if (x == 0)
        return false;

    // If x & (x-1) = 0 then x is a power of 2
    if (!(x & (x - 1)))
        return true;
    else
        return false;
}

// Function to return the required count
int countNum(int a[], int n)
{
    int count = 0;

    for (int i = 0; i < n; i++) {

        // If a[i] or (a[i]+1) is a power of 2
        if (isPowerOfTwo(a[i]) || isPowerOfTwo(a[i] + 1))
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 9, 3, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countNum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if x is a power of 2
static boolean isPowerOfTwo(int x)
{
    if (x == 0)
        return false;

    // If x & (x-1) = 0 then x is a power of 2
    if ((x & (x - 1)) == 0)
        return true;
    else
        return false;
}

// Function to return the required count
static int countNum(int a[], int n)
{
    int count = 0;

    for (int i = 0; i < n; i++) {

        // If a[i] or (a[i]+1) is a power of 2
        if (isPowerOfTwo(a[i]) || isPowerOfTwo(a[i] + 1))
            count++;
    }

    return count;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 5, 6, 9, 3, 1 };

    int n = arr.length;

    System.out.println(countNum(arr, n));

}
}

// This code is contributed by
// Sahil_Shelangia
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if x
# is a power of 2
def isPowerOfTwo(x):
    if (x == 0):
        return False

    # If x & (x-1) = 0 then x is a power of 2
    if ((x & (x - 1)) == 0):
        return True
    else:
        return False

# Function to return the required count
def countNum(a, n):
    count = 0

    for i in range(0, n, 1):

        # If a[i] or (a[i]+1) is a power of 2
        if (isPowerOfTwo(a[i]) or
            isPowerOfTwo(a[i] + 1)):
            count += 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [5, 6, 9, 3, 1]

    n = len(arr)

    print(countNum(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if x is a power of 2
static bool isPowerOfTwo(int x)
{
    if (x == 0)
        return false;

    // If x & (x-1) = 0 then x is a power of 2
    if ((x & (x - 1)) == 0)
        return true;
    else
        return false;
}

// Function to return the required count
static int countNum(int[] a, int n)
{
    int count = 0;

    for (int i = 0; i < n; i++)
    {
        // If a[i] or (a[i]+1) is a power of 2
        if (isPowerOfTwo(a[i]) || isPowerOfTwo(a[i] + 1))
            count++;
    }

    return count;
}

// Driver code
public static void Main()
{
    int[] arr = { 5, 6, 9, 3, 1 };
    int n = arr.Length;
    Console.WriteLine(countNum(arr, n));

}
}

// This code is contributed by
// Mukul Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if x is
// a power of 2
function isPowerOfTwo( $x)
{
    if ($x == 0)
        return false;

    // If x & (x-1) = 0 then x is a
    // power of 2
    if (!($x & ($x - 1)))
        return true;
    else
        return false;
}

// Function to return the required count
function countNum($a, $n)
{
    $cnt = 0;

    for ( $i = 0; $i < $n; $i++)
    {

        // If a[i] or (a[i]+1) is a power of 2
        if (isPowerOfTwo($a[$i]) ||
            isPowerOfTwo($a[$i] + 1))
            $cnt++;
    }

    return $cnt;
}

// Driver Code
$arr = array( 5, 6, 9, 3, 1 );

$n = count($arr);

echo countNum($arr, $n);

// This code is contributed by 29AjayKumar
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if x is a power of 2
function isPowerOfTwo(x)
{
    if (x == 0)
        return false;

    // If x & (x-1) = 0 then x is a power of 2
    if ((x & (x - 1)) == 0)
        return true;
    else
        return false;
}

// Function to return the required count
function countNum(a, n)
{
    let count = 0;

    for(let i = 0; i < n; i++)
    {

        // If a[i] or (a[i]+1) is a power of 2
        if (isPowerOfTwo(a[i]) ||
            isPowerOfTwo(a[i] + 1))
            count++;
    }
    return count;
}

// Driver code
let arr = [ 5, 6, 9, 3, 1 ];
let n = arr.length;

document.write(countNum(arr, n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```