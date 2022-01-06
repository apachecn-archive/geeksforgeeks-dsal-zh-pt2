# 数组中的最小值，先减小后增大

> 原文:[https://www . geeksforgeeks . org/数组中的最小值先减后增/](https://www.geeksforgeeks.org/minimum-in-an-array-which-is-first-decreasing-then-increasing/)

给定一个 N 个整数的数组，其中数组元素形成一个严格的递减和递增序列。任务是在这样的数组中找到最小的数。
**约束** : N > = 3
**示例:**

```
Input: a[] = {2, 1, 2, 3, 4}
Output: 1

Input: a[] = {8, 5, 4, 3, 4, 10}
Output: 3 
```

一种**天真的方法**是线性遍历数组，找出最小的数。时间复杂度将因此为 0(N)。
一个**有效的方法**是修改[二分搜索法](https://www.geeksforgeeks.org/binary-search/)并使用它。将阵列分成两半，使用二分搜索法检查[mid] <是否为[mid+1]。如果 *a【中】< a【中+1】*，那么最小的数字在前半部分*低到中*，否则在后半部分*中+1 到高*。
**算法:**

```
while(lo > 1

    if a[mid] < a[mid+1] then hi = mid

    else lo = mid+1
} 
```

以下是上述方法的实现:

## C++

```
// C++ program to find the smallest number
// in an array of decrease and increasing numbers
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest number's index
int minimal(int a[], int n)
{
    int lo = 0, hi = n - 1;

    // Do a binary search
    while (lo < hi) {

        // Find the mid element
        int mid = (lo + hi) >> 1;

        // Check for break point
        if (a[mid] < a[mid + 1]) {
            hi = mid;
        }
        else {
            lo = mid + 1;
        }
    }

    // Return the index
    return lo;
}

// Driver Code
int main()
{
    int a[] = { 8, 5, 4, 3, 4, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    int ind = minimal(a, n);

    // Print the smallest number
    cout << a[ind];
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest number
// in an array of decrease and increasing numbers
class Solution
{
// Function to find the smallest number's index
static int minimal(int a[], int n)
{
    int lo = 0, hi = n - 1;

    // Do a binary search
    while (lo < hi) {

        // Find the mid element
        int mid = (lo + hi) >> 1;

        // Check for break point
        if (a[mid] < a[mid + 1]) {
            hi = mid;
        }
        else {
            lo = mid + 1;
        }
    }

    // Return the index
    return lo;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 8, 5, 4, 3, 4, 10 };
    int n = a.length;
    int ind = minimal(a, n);

    // Print the smallest number
    System.out.println( a[ind]);
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find the smallest
# number in a array of decrease and
# increasing numbers

# function to find the smallest
# number's index
def minimal(a, n):

    lo, hi = 0, n - 1

    # Do a binary search
    while lo < hi:

        # find the mid element
        mid = (lo + hi) // 2

        # Check for break point
        if a[mid] < a[mid + 1]:
            hi = mid
        else:
            lo = mid + 1
        return lo

# Driver code
a = [8, 5, 4, 3, 4, 10]

n = len(a)

ind = minimal(a, n)

# print the smallest number
print(a[ind])

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find the smallest number
// in an array of decrease and increasing numbers
using System;
class Solution
{
// Function to find the smallest number's index
static int minimal(int[] a, int n)
{
    int lo = 0, hi = n - 1;

    // Do a binary search
    while (lo < hi) {

        // Find the mid element
        int mid = (lo + hi) >> 1;

        // Check for break point
        if (a[mid] < a[mid + 1]) {
            hi = mid;
        }
        else {
            lo = mid + 1;
        }
    }

    // Return the index
    return lo;
}

// Driver Code
public static void Main()
{
    int[] a = { 8, 5, 4, 3, 4, 10 };
    int n = a.Length;
    int ind = minimal(a, n);

    // Print the smallest number
    Console.WriteLine( a[ind]);
}
}
//contributed by Mukul singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the smallest number
// in an array of decrease and increasing numbers

// Function to find the smallest
// number's index
function minimal($a, $n)
{
    $lo = 0;
    $hi = $n - 1;

    // Do a binary search
    while ($lo < $hi)
    {

        // Find the mid element
        $mid = ($lo + $hi) >> 1;

        // Check for break point
        if ($a[$mid] < $a[$mid + 1])
        {
            $hi = $mid;
        }
        else
        {
            $lo = $mid + 1;
        }
    }

    // Return the index
    return $lo;
}

// Driver Code
$a = array( 8, 5, 4, 3, 4, 10 );
$n = sizeof($a);
$ind = minimal($a, $n);

// Print the smallest number
echo $a[$ind];

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the smallest number
    // in an array of decrease and increasing numbers

    // Function to find the smallest number's index
    function minimal(a, n)
    {
        let lo = 0, hi = n - 1;

        // Do a binary search
        while (lo < hi) {

            // Find the mid element
            let mid = (lo + hi) >> 1;

            // Check for break point
            if (a[mid] < a[mid + 1]) {
                hi = mid;
            }
            else {
                lo = mid + 1;
            }
        }

        // Return the index
        return lo;
    }

    let a = [ 8, 5, 4, 3, 4, 10 ];
    let n = a.length;
    let ind = minimal(a, n);

    // Print the smallest number
    document.write(a[ind]);

</script>
```

**Output:** 

```
3
```

**时间复杂度**:O(Log N)
T3】辅助空间 : O(1)