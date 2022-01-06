# 最大大小为 2 的最小分区和由给定值限定的总和

> 原文:[https://www . geeksforgeeks . org/最小-最大-大小-2-和-受给定值限制的分区/](https://www.geeksforgeeks.org/minimum-partitions-of-maximum-size-2-and-sum-limited-by-given-value/)

给定一个正数数组 arr[]，求数组中满足以下性质的最小集合数，
1。一个集合中最多可以包含两个元素。这两个元素不必是连续的。
2。集合元素的总和应小于或等于给定的键。可以假设给定的键大于或等于最大的数组元素。

**示例:**

```
Input: arr[] = [10, 20, 12], key = 25
Output: 2
We break into two parts {10, 12} and {2}

Input : arr[] = [3, 5, 3, 4], key=5
Output : 4
Explanation: 4 sets (3), (5), (3), (4)
```

其思路是先对数组进行排序，然后按照[两个指针的方法。](https://www.geeksforgeeks.org/two-pointers-technique/)我们从排序数组的两个角开始两个指针。如果它们的和小于或等于给定的键，那么我们把它们集合起来，否则我们只考虑最后一个元素。
以下是上述办法的实施情况:

## C++

```
// C++ program to count minimum number of partitions
// of size 2 and sum smaller than or equal to given
// key.
#include <algorithm>
#include <iostream>
using namespace std;

int minimumSets(int arr[], int n, int key)
{
    int i, j;

    // sort the array
    sort(arr, arr + n);

    // if sum of ith smaller and jth larger element is
    // less than key, then pack both numbers in a set
    // otherwise pack the jth larger number
    // alone in the set
    for (i = 0, j = n - 1; i <= j; ++i)
        if (arr[i] + arr[j] <= key)
            j--;

    // After ending of loop i will contain minimum
    // number of sets
    return i;
}

int main()
{
    int arr[] = { 3, 5, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 5;
    cout << minimumSets(arr, n, key);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum number of partitions
// of size 2 and sum smaller than or equal to given
// key.

import java.util.Arrays;
class GFG {

static int minimumSets(int arr[], int n, int key)
{
    int i, j;

    // sort the array
    Arrays.sort(arr);

    // if sum of ith smaller and jth larger element is
    // less than key, then pack both numbers in a set
    // otherwise pack the jth larger number
    // alone in the set
    for (i = 0, j = n - 1; i <= j; ++i)
        if (arr[i] + arr[j] <= key)
            j--;

    // After ending of loop i will contain minimum
    // number of sets
    return i;
}

    public static void main (String[] args) {
    int []arr = { 3, 5, 3, 4 };
    int n =arr.length;
    int key = 5;
    System.out.println( minimumSets(arr, n, key));
    }
}
// This code is contributed by chandan_jnu.
```

## 蟒蛇 3

```
# Python 3 program to count minimum number
# of partitions of size 2 and sum smaller
# than or equal to given key.

def minimumSets(arr, n, key):

    # sort the array
    arr.sort(reverse = False)

    # if sum of ith smaller and jth larger
    # element is less than key, then pack
    # both numbers in a set otherwise pack
    # the jth larger number alone in the set
    j = n - 1
    for i in range(0, j + 1, 1):
        if (arr[i] + arr[j] <= key):
            j -= 1

    # After ending of loop i will
    # contain minimum number of sets
    return i + 1

# Driver Code
if __name__ == '__main__':
    arr = [3, 5, 3, 4]
    n = len(arr)
    key = 5
    print(minimumSets(arr, n, key))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to count minimum
// number of partitions of size
// 2 and sum smaller than or
// equal to given key.
using System;
class GFG
{

static int minimumSets(int []arr,
                       int n, int key)
{
    int i, j;

    // sort the array
    Array.Sort(arr);

    // if sum of ith smaller and
    // jth larger element is less
    // than key, then pack both
    // numbers in a set otherwise
    // pack the jth larger number
    // alone in the set
    for (i = 0, j = n - 1; i <= j; ++i)
        if (arr[i] + arr[j] <= key)
            j--;

    // After ending of loop i
    // will contain minimum
    // number of sets
    return i;
}

// Driver Code
public static void Main ()
{
    int []arr = { 3, 5, 3, 4 };
    int n =arr.Length;
    int key = 5;
    Console.WriteLine(minimumSets(arr, n, key));
}
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count minimum
// number of partitions of size
// 2 and sum smaller than or
// equal to given key.
function minimumSets($arr, $n, $key)
{
    $i; $j;

    // sort the array
    sort($arr);

    // if sum of ith smaller and
    // jth larger element is less
    // than key, then pack both
    // numbers in a set otherwise
    // pack the jth larger number
    // alone in the set
    for ($i = 0, $j = $n - 1; $i <= $j; ++$i)
        if ($arr[$i] + $arr[$j] <= $key)
            $j--;
        return $i;
}

// Driver Code
$arr = array( 3, 5, 3, 4 );
$n = count($arr);
$key = 5;
echo minimumSets($arr, $n, $key);

// This code is contributed
// by chandan_jnu   
?>
```

## java 描述语言

```
<script>

// Javascript program to count minimum number of partitions
// of size 2 and sum smaller than or equal to given
// key.

function minimumSets(arr, n, key)
{
    var i, j;

    // sort the array
    arr.sort((a,b)=> a-b)

    // if sum of ith smaller and jth larger element is
    // less than key, then pack both numbers in a set
    // otherwise pack the jth larger number
    // alone in the set
    for (i = 0, j = n - 1; i <= j; ++i)
        if (arr[i] + arr[j] <= key)
            j--;

    // After ending of loop i will contain minimum
    // number of sets
    return i;
}

var arr = [3, 5, 3, 4];
var n = arr.length;
var key = 5;
document.write( minimumSets(arr, n, key));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(nlogn)