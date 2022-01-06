# 要移除的最小元素，使得相邻元素的总和总是偶数

> 原文:[https://www . geeksforgeeks . org/待移除的最小元素-这样相邻元素的总和总是偶数/](https://www.geeksforgeeks.org/minimum-elements-to-be-removed-such-that-sum-of-adjacent-elements-is-always-even/)

给定一个 N 个整数的数组。任务是消除最少数量的元素，以便在结果数组中任何两个相邻值的和为偶数。

**示例:**

```
Input : arr[] = {1, 2, 3}
Output : 1
Remove 2 from the array.

Input : arr[] = {1, 3, 5, 4, 2}
Output : 2
Remove 4 and 2.
```

**逼近:**两个数之和为偶数，如果其中一个都是奇数，或者两个都是偶数。这意味着对于每对具有不同奇偶性的连续数字，消除其中一个。
所以，要使相邻元素之和为偶数，要么所有元素都应为奇数，要么为偶数。所以下面的贪婪算法是有效的:

*   按顺序浏览所有元素。
*   计算数组中的奇数和偶数元素。
*   返回最小计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of eliminations
// such that sum of all adjacent elements is even
int min_elimination(int n, int arr[])
{
    int countOdd = 0;

    // Stores the new value
    for (int i = 0; i < n; i++)

        // Count odd numbers
        if (arr[i] % 2)
            countOdd++;

    // Return the minimum of even and
    // odd count
    return min(countOdd, n - countOdd);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 7, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << min_elimination(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to find minimum number of
// eliminations such that sum of all
// adjacent elements is even
static int min_elimination(int n, int arr[])
{
    int countOdd = 0;

    // Stores the new value
    for (int i = 0; i < n; i++)

        // Count odd numbers
        if (arr[i] % 2 == 1)
            countOdd++;

    // Return the minimum of even
    // and odd count
    return Math.min(countOdd, n - countOdd);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 7, 9 };
    int n = arr.length;

    System.out.println(min_elimination(n, arr));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function to find minimum number of
# eliminations such that sum of all
# adjacent elements is even
def min_elimination(n, arr):
    countOdd = 0

    # Stores the new value
    for i in range(n):

        # Count odd numbers
        if (arr[i] % 2):
            countOdd += 1

    # Return the minimum of even and
    # odd count
    return min(countOdd, n - countOdd)

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 7, 9]
    n = len(arr)

    print(min_elimination(n, arr))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to find minimum number of
// eliminations such that sum of all
// adjacent elements is even
static int min_elimination(int n, int[] arr)
{
    int countOdd = 0;

    // Stores the new value
    for (int i = 0; i < n; i++)

        // Count odd numbers
        if (arr[i] % 2 == 1)
            countOdd++;

    // Return the minimum of even
    // and odd count
    return Math.Min(countOdd, n - countOdd);
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 3, 7, 9 };
    int n = arr.Length;

    Console.WriteLine(min_elimination(n, arr));
}
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find minimum number of
// eliminations such that sum of all
// adjacent elements is even
function min_elimination($n, $arr)
{
    $countOdd = 0;

    // Stores the new value
    for ($i = 0; $i < $n; $i++)

        // Count odd numbers
        if ($arr[$i] % 2 == 1)
            $countOdd++;

    // Return the minimum of even
    // and odd count
    return min($countOdd, $n - $countOdd);
}

// Driver code
$arr = array(1, 2, 3, 7, 9);
$n = sizeof($arr);

echo(min_elimination($n, $arr));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

// Function to find minimum number of eliminations
// such that sum of all adjacent elements is even
function min_elimination(n, arr)
{
    let countOdd = 0;

    // Stores the new value
    for (let i = 0; i < n; i++)

        // Count odd numbers
        if (arr[i] % 2)
            countOdd++;

    // Return the minimum of even and
    // odd count
    return Math.min(countOdd, n - countOdd);
}

// Driver code

let arr= [1, 2, 3, 7, 9];
let n = arr.length;

document.write(min_elimination(n, arr));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)

**辅助空间:** O(1)