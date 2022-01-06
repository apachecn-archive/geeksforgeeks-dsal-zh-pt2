# 从一个数组中计数对，该数组中较大数除以较小数的商不超过 K

> 原文:[https://www . geeksforgeeks . org/从数组中计数-对-其较大数字除以较小数字的商不超过-k/](https://www.geeksforgeeks.org/count-pairs-from-an-array-whose-quotient-of-division-of-larger-number-by-the-smaller-number-does-not-exceed-k/)

给定一个大小为 **N** 、的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**和一个整数 **K** ，任务是计算给定数组中较大元素除以该对中较小元素的商不超过 **K** 的对的数量。

**示例:**

> **输入:** arr[] = {3，12，5，13}，K=2
> **输出:** 2
> **说明:**满足给定条件的对为(3，5)和(12，13)。
> 
> **输入:** arr[] = {2，3，9，5}，K=2
> **输出:** 3
> **说明:**满足给定条件的对为(2，3)、(3，5)和(5，9)。

**简单方法:**最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并针对每一对检查是否满足所需的条件。对于满足条件的对，将**计数**增加 **1** 。检查所有对后，打印获得的**计数**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是[按照升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组排序，然后对于每个数组元素 **arr[i]** ，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到刚刚大于 **K * arr[i]** 的元素的索引，比如**高、**。**【I+1，高–1】**范围内的所有元素将与**arr【I】**形成一对。
按照以下步骤解决问题:

*   初始化一个变量，比如 **ans，**来存储所需的对数。
*   [给定数组按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [使用变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，说 **i**
    *   将数值上限**2 * arr【I】**的[指数存储在一个变量中，比如说**高**。](https://www.geeksforgeeks.org/upper_bound-in-cpp/)
    *   通过添加**高–I–1**来更新**和**的值。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// having quotient of division
// of larger element by the smaller
// element in the pair not exceeding K
void countPairs(int arr[], int n, int k)
{
    // Sort the array in ascending order
    sort(arr, arr + n);

    // Store the required result
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // Store the upper bound for
        // the current array element
        int high
            = upper_bound(arr, arr + n, k * arr[i]) - arr;

        // Update the number of pairs
        ans += high - i - 1;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given array, arr[]
    int arr[] = { 2, 3, 9, 5 };

    // Store the size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 2;

    countPairs(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

public static int upper_bound(int arr[], int key)
{
    int l = -1, r = arr.length;
    while (l + 1 < r)
    {
        int m = (l + r) >>> 1;
        if (arr[m] <= key)
            l = m;
        else
            r = m;
    }
    return l + 1;
}

// Function to count the number
// having quotient of division
// of larger element by the smaller
// element in the pair not exceeding K
static void countPairs(int arr[], int n, int k)
{

    // Sort the array in ascending order
    Arrays.sort(arr);

    // Store the required result
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

        // Store the upper bound for
        // the current array element
        int high = upper_bound(arr, k * arr[i]);

        // Update the number of pairs
        ans += high - i - 1;
    }

    // Print the result
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given array, arr[]
    int arr[] = { 2, 3, 9, 5 };

    // Store the size of the array
    int n = arr.length;

    int k = 2;

    countPairs(arr, n, k);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_right

#  Function to count the number
#  having quotient of division
#  of larger element by the smaller
#  element in the pair not exceeding K
def countPairs(arr, n, k) :

    #  Sort the array in ascending order
    arr.sort()

    #  Store the required result
    ans = 0

    #  Traverse the array
    for i in range(n - 1):

        #  Store the upper bound for
        #  the current array element
        high = bisect_right(arr, k * arr[i])

        #  Update the number of pairs
        ans += high - i - 1

    #  Print result
    print(ans)

#  Driver Code

#  Given array, arr[]
arr = [ 2, 3, 9, 5 ]

#  Store the size of the array
n = len(arr)
k = 2
countPairs(arr, n, k)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

static int upper_bound(int []arr, int key)
{
    int l = -1, r = arr.Length;
    while (l + 1 < r)
    {
        int m = (l + r) >> 1;
        if (arr[m] <= key)
            l = m;
        else
            r = m;
    }
    return l + 1;
}

// Function to count the number
// having quotient of division
// of larger element by the smaller
// element in the pair not exceeding K
static void countPairs(int []arr, int n, int k)
{

    // Sort the array in ascending order
    Array.Sort(arr);

    // Store the required result
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

        // Store the upper bound for
        // the current array element
        int high = upper_bound(arr, k * arr[i]);

        // Update the number of pairs
        ans += high - i - 1;
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{

    // Given array, arr[]
    int []arr = { 2, 3, 9, 5 };

    // Store the size of the array
    int n = arr.Length;
    int k = 2;
    countPairs(arr, n, k);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

function upper_bound(arr, key)
{
    let l = -1, r = arr.length;
    while (l + 1 < r)
    {
        let m = (l + r) >>> 1;

        if (arr[m] <= key)
            l = m;
        else
            r = m;
    }
    return l + 1;
}

// Function to count the number
// having quotient of division
// of larger element by the smaller
// element in the pair not exceeding K
function countPairs(arr, n, k)
{

    // Sort the array in ascending order
    arr.sort();

    // Store the required result
    let ans = 0;

    // Traverse the array
    for(let i = 0; i < n - 1; i++)
    {

        // Store the upper bound for
        // the current array element
        let high = upper_bound(arr, k * arr[i]);

        // Update the number of pairs
        ans += high - i - 1;
    }

    // Print the result
    document.write(ans);
}

// Driver code

// Given array, arr[]
let arr = [ 2, 3, 9, 5 ];

// Store the size of the array
let n = arr.length;

let k = 2;

countPairs(arr, n, k);

// This code is contributed by target_2   

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*