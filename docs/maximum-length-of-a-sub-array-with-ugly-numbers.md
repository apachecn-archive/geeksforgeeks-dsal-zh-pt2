# 丑陋数字子阵列的最大长度

> 原文:[https://www . geeksforgeeks . org/带丑陋数字的子数组的最大长度/](https://www.geeksforgeeks.org/maximum-length-of-a-sub-array-with-ugly-numbers/)

给定一个由 **N** 元素(0 ≤ arr[i] ≤ 1000)组成的数组 **arr[]** 。任务是找到仅包含丑陋数字的子数组的最大长度。丑陋的数字是唯一的质因数是 **2** 、 **3** 或 **5** 的数字。
顺序 **1、2、3、4、5、6、8、9、10、12、15、…..**显示前几个难看的数字。按照惯例，包括 1。

**示例:**

> **输入:** arr[] = {1，2，7，9，120，810，374}
> **输出:** 3
> 最长可能丑数子阵 sis {9，120，810}
> **输入:** arr[] = {109，480，320，142，121，1}
> **输出:** 2

**进场:**

*   取一个[无序 _ 集合](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)，在集合中插入所有小于 1000 的难看数字。
*   使用两个名为 **current_max** 和 **max_so_far** 的变量遍历数组。
*   检查每个元素是否存在于集合中。
*   如果发现一个难看的数字，那么增加 current_max，并与 max_so_far 进行比较。
*   如果**电流 _ 最大值>最大值 _ 到目前为止**，那么**最大值 _ 到目前为止=电流 _ 最大值**。
*   每次发现非丑元素，复位 **current_max = 0** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the nth ugly number
unsigned uglyNumber(int n)
{
    // To store ugly numbers
    int ugly[n];
    int i2 = 0, i3 = 0, i5 = 0;
    int next_multiple_of_2 = 2;
    int next_multiple_of_3 = 3;
    int next_multiple_of_5 = 5;
    int next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++) {
        next_ugly_no = min(next_multiple_of_2,
                           min(next_multiple_of_3,
                               next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2) {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3) {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5) {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }

    return next_ugly_no;
}

// Function to return the length of the
// maximum sub-array of ugly numbers
int maxUglySubarray(int arr[], int n)
{
    unordered_set<int> s;
    int i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (1) {
        int next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s.insert(next_ugly_number);
        i++;
    }

    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++) {

        // Check if element is non ugly
        if (s.find(arr[i]) == s.end())
            current_max = 0;

        // If element is ugly, than update
        // current_max and max_so_far accordingly
        else {
            current_max++;
            max_so_far = max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver code
int main()
{

    int arr[] = { 1, 0, 6, 7, 320, 800, 100, 648 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxUglySubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to get the nth ugly number
static int uglyNumber(int n)
{
    // To store ugly numbers
    int []ugly = new int[n];
    int i2 = 0, i3 = 0, i5 = 0;
    int next_multiple_of_2 = 2;
    int next_multiple_of_3 = 3;
    int next_multiple_of_5 = 5;
    int next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++)
    {
        next_ugly_no = Math.min(next_multiple_of_2,
                       Math.min(next_multiple_of_3,
                                next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2)
        {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3)
        {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5)
        {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }
    return next_ugly_no;
}

// Function to return the length of the
// maximum sub-array of ugly numbers
static int maxUglySubarray(int arr[], int n)
{
    HashSet<Integer> s = new HashSet<>();
    int i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (true)
    {
        int next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s.add(next_ugly_number);
        i++;
    }

    int current_max = 0, max_so_far = 0;

    for (i = 0; i < n; i++)
    {

        // Check if element is non ugly
        if (!s.contains(arr[i]))
            current_max = 0;

        // If element is ugly, than update
        // current_max and max_so_far accordingly
        else
        {
            current_max++;
            max_so_far = Math.max(current_max,
                                  max_so_far);
        }
    }
    return max_so_far;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 6, 7, 320, 800, 100, 648 };
    int n = arr.length;
    System.out.println(maxUglySubarray(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to get the nth ugly number
def uglyNumber(n):

    # To store ugly numbers
    ugly = [None for i in range(n)]
    i2 = 0
    i3 = 0
    i5 = 0
    next_multiple_of_2 = 2
    next_multiple_of_3 = 3
    next_multiple_of_5 = 5
    next_ugly_no = 1

    ugly[0] = 1
    for i in range(1, n, 1):
        next_ugly_no = min(next_multiple_of_2,
                       min(next_multiple_of_3,
                           next_multiple_of_5))
        ugly[i] = next_ugly_no
        if (next_ugly_no == next_multiple_of_2):
            i2 = i2 + 1
            next_multiple_of_2 = ugly[i2] * 2
        if (next_ugly_no == next_multiple_of_3):
            i3 = i3 + 1
            next_multiple_of_3 = ugly[i3] * 3
        if (next_ugly_no == next_multiple_of_5):
            i5 = i5 + 1
            next_multiple_of_5 = ugly[i5] * 5

    return next_ugly_no

# Function to return the length of the
# maximum sub-array of ugly numbers
def maxUglySubarray(arr, n):
    s = set()
    i = 1

    # Insert ugly numbers in set
    # which are less than 1000
    while (1):
        next_ugly_number = uglyNumber(i)
        if (next_ugly_number >= 1000):
            break
        s.add(next_ugly_number)
        i += 1

    current_max = 0
    max_so_far = 0

    for i in range(n):

        # Check if element is non ugly
        if (arr[i] not in s):
            current_max = 0

        # If element is ugly, than update
        # current_max and max_so_far accordingly
        else:
            current_max += 1
            max_so_far = max(current_max,
                              max_so_far)

    return max_so_far

# Driver code
if __name__ == '__main__':
    arr = [1, 0, 6, 7, 320, 800, 100, 648]
    n = len(arr)
    print(maxUglySubarray(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to get the nth ugly number
static int uglyNumber(int n)
{
    // To store ugly numbers
    int []ugly = new int[n];
    int i2 = 0, i3 = 0, i5 = 0;
    int next_multiple_of_2 = 2;
    int next_multiple_of_3 = 3;
    int next_multiple_of_5 = 5;
    int next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++)
    {
        next_ugly_no = Math.Min(next_multiple_of_2,
                       Math.Min(next_multiple_of_3,
                                next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2)
        {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3)
        {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5)
        {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }
    return next_ugly_no;
}

// Function to return the length of the
// maximum sub-array of ugly numbers
static int maxUglySubarray(int []arr, int n)
{
    HashSet<int> s = new HashSet<int>();
    int i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (true)
    {
        int next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s.Add(next_ugly_number);
        i++;
    }

    int current_max = 0, max_so_far = 0;

    for (i = 0; i < n; i++)
    {

        // Check if element is non ugly
        if (!s.Contains(arr[i]))
            current_max = 0;

        // If element is ugly, than update
        // current_max and max_so_far accordingly
        else
        {
            current_max++;
            max_so_far = Math.Max(current_max,
                                  max_so_far);
        }
    }
    return max_so_far;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 6, 7, 320, 800, 100, 648 };
    int n = arr.Length;
    Console.WriteLine(maxUglySubarray(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to get the nth ugly number
function uglyNumber( n)
{
    // To store ugly numbers
    var ugly = [];
    var i2 = 0, i3 = 0, i5 = 0;
    var next_multiple_of_2 = 2;
    var next_multiple_of_3 = 3;
    var next_multiple_of_5 = 5;
    var next_ugly_no = 1;

    ugly[0] = 1;
    for (var i = 1; i < n; i++)
    {
        next_ugly_no = Math.min(next_multiple_of_2,
                       Math.min(next_multiple_of_3,
                                next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2)
        {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3)
        {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5)
        {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }
    return next_ugly_no;
}

// Function to return the length of the
// maximum sub-array of ugly numbers
function maxUglySubarray(arr,  n)
{
    var s = []
    var i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (true)
    {
        var next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s.push(next_ugly_number);
        i++;
    }

    var current_max = 0, max_so_far = 0;

    for (i = 0; i < n; i++)
    {

        // Check if element is non ugly
        if (!s.includes(arr[i]))
            current_max = 0;

        // If element is ugly, than update
        // current_max and max_so_far accordingly
        else
        {
            current_max++;
            max_so_far = Math.max(current_max,
                                  max_so_far);
        }
    }
    return max_so_far;
}

// Driver code

    var arr = [ 1, 0, 6, 7, 320, 800, 100, 648 ];
    var n = arr.length;
    document.write(maxUglySubarray(arr, n));

</script>
```

**Output:** 

```
4
```