# 对未排序的数组进行排序时，查找第一次出现的索引

> 原文:[https://www . geesforgeks . org/find-未排序数组排序时第一次出现的索引/](https://www.geeksforgeeks.org/find-index-of-first-occurrence-when-an-unsorted-array-is-sorted/)

给定一个未排序的数组和一个数字 x，当我们对数组排序时，找到 x 的第一次出现的索引。如果 x 不存在，打印-1。

**示例:**

```
Input : arr[] = {10, 30, 20, 50, 20}
           x = 20
Output : 1
Sorted array is {10, 20, 20, 30, 50}

Input : arr[] = {10, 30, 20, 50, 20}
           x = 60
Output : -1
60 is not present in array. 
```

一个**简单的解决方法**就是先排序数组，然后做[二分搜索法找到第一个出现的](https://www.geeksforgeeks.org/find-first-and-last-positions-of-an-element-in-a-sorted-array/)。

## C++

```
// C++ program to find index of first
// occurrence of x when array is sorted.
#include <bits/stdc++.h>
using namespace std;

int findFirst(int arr[], int n, int x)
{
    sort(arr, arr + n);

    // lower_bound returns iterator pointing to
    // first element that does not compare less
    // to x.
    int* ptr = lower_bound(arr, arr + n, x);

    // If x is not present return -1.
    return (*ptr != x) ? -1 : (ptr - arr);
}

int main()
{
    int x = 20, arr[] = { 10, 30, 20, 50, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findFirst(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of first
// occurrence of x when array is sorted.
import java.util.*;

class GFG {
    static int findFirst(int arr[], int n, int x)
    {
        Arrays.sort(arr);

        // lower_bound returns iterator pointing to
        // first element that does not compare less
        // to x.
        int ptr = lowerBound(arr, 0, n, x);

        // If x is not present return -1.
        return (arr[ptr] != x) ? -1 : (ptr);
    }

    static int lowerBound(int[] a, int low, int high,
                          int element)
    {
        while (low < high) {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int x = 20, arr[] = { 10, 30, 20, 50, 20 };
        int n = arr.length;
        System.out.println(findFirst(arr, n, x));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find index of first
# occurrence of x when array is sorted.
import math

def findFirst(arr, n, x):
    arr.sort()

    # lower_bound returns iterator pointing to
    # first element that does not compare less
    # to x.
    ptr = lowerBound(arr, 0, n, x)

    # If x is not present return -1.
    return 1 if (ptr != x) else (ptr - arr)

def lowerBound(a, low, high, element):
    while(low < high):
        middle = low + (high - low) // 2
        if(element > a[middle]):
            low = middle + 1
        else:
            high = middle
    return low

# Driver Code
if __name__ == '__main__':
    x = 20
    arr = [10, 30, 20, 50, 20]
    n = len(arr)
    print(findFirst(arr, n, x))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find index of first
// occurrence of x when array is sorted.
using System;

class GFG {
    static int findFirst(int[] arr, int n, int x)
    {
        Array.Sort(arr);

        // lower_bound returns iterator pointing to
        // first element that does not compare less
        // to x.
        int ptr = lowerBound(arr, 0, n, x);

        // If x is not present return -1.
        return (arr[ptr] != x) ? -1 : (ptr);
    }

    static int lowerBound(int[] a, int low, int high,
                          int element)
    {
        while (low < high) {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Driver Code
    static public void Main()
    {
        int x = 20;
        int[] arr = { 10, 30, 20, 50, 20 };
        int n = arr.Length;
        Console.Write(findFirst(arr, n, x));
    }
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find index of first
// occurrence of x when array is sorted.

function findFirst( $arr, $n, $x)
{
    sort($arr);

// lower_bound returns iterator pointing to
// first element that does not compare less
// to x.
$ptr = floor($arr);

// If x is not present return -1.
return ($ptr != $x)? 1 : ($ptr - $arr);
}
//Code driven
    $x = 20;
    $arr = array(10, 30, 20, 50, 20);
    $n = sizeof($arr)/sizeof($arr[0]);
    echo findFirst($arr, $n, $x);

#This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>

// Javascript program to find index of first
// occurrence of x when array is sorted.
function findFirst(arr, n, x)
{
    arr.sort();

    // lower_bound returns iterator pointing
    // to first element that does not compare
    // less to x.
    let ptr = lowerBound(arr, 0, n, x);

    // If x is not present return -1.
    return (arr[ptr] != x) ? -1 : (ptr);
}

function lowerBound(a, low, high, element)
{
    while (low < high)
    {
        let middle = low + parseInt(
                   (high - low) / 2, 10);

        if (element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Driver code
let x = 20;
let arr = [ 10, 30, 20, 50, 20 ];
let n = arr.length;

document.write(findFirst(arr, n, x));

// This code is contributed by mukesh07

</script>
```

**输出:**

```
1
```

**时间复杂度:** O(n Log n)

一个**有效的解决方案**是简单地计算比 x 小的元素。

## C++

```
// C++ program to find index of first
// occurrence of x when array is sorted.
#include <bits/stdc++.h>
using namespace std;

int findFirst(int arr[], int n, int x)
{
    int count = 0;
    bool isX = false;
    for (int i = 0; i < n; i++) {
        if (arr[i] == x)
            isX = true;
        else if (arr[i] < x)
            count++;
    }
    return (isX == false) ? -1 : count;
}

int main()
{
    int x = 20, arr[] = { 10, 30, 20, 50, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findFirst(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of first
// occurrence of x when array is sorted.

public class GFG {

    static int findFirst(int arr[], int n, int x)
    {
        int count = 0;
        boolean isX = false;
        for (int i = 0; i < n; i++) {
            if (arr[i] == x) {
                isX = true;
            }
            else if (arr[i] < x) {
                count++;
            }
        }
        return (isX == false) ? -1 : count;
    }

    // Driver main
    public static void main(String[] args)
    {
        int x = 20, arr[] = { 10, 30, 20, 50, 20 };
        int n = arr.length;
        System.out.println(findFirst(arr, n, x));
    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python 3 program to find index
# of first occurrence of x when
# array is sorted.

def findFirst(arr, n, x):

    count = 0
    isX = False
    for i in range(n):
        if (arr[i] == x):
            isX = True
        elif (arr[i] < x):
            count += 1

    return -1 if(isX == False) else count

# Driver Code
if __name__ == "__main__":
    x = 20
    arr = [10, 30, 20, 50, 20]
    n = len(arr)
    print(findFirst(arr, n, x))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find index of first
// occurrence of x when array is sorted.
using System;

public class GFG {

    static int findFirst(int[] arr, int n, int x)
    {
        int count = 0;
        bool isX = false;
        for (int i = 0; i < n; i++) {
            if (arr[i] == x) {
                isX = true;
            }
            else if (arr[i] < x) {
                count++;
            }
        }
        return (isX == false) ? -1 : count;
    }

    // Driver main
    public static void Main()
    {
        int x = 20;
        int[] arr = { 10, 30, 20, 50, 20 };
        int n = arr.Length;
        Console.WriteLine(findFirst(arr, n, x));
    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find index of first
// occurrence of x when array is sorted.

function findFirst($arr, $n, $x)
{
    $count = 0;
    $isX = false;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == $x)
            $isX = true;
        else if ($arr[$i] < $x)
            $count++;
    }
    return ($isX == false)? -1 : $count;
}

// Driver Code
$x = 20;
$arr = array(10, 30, 20, 50, 20);
$n = sizeof($arr);
echo findFirst($arr, $n, $x);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to find index of first
// occurrence of x when array is sorted.
function findFirst(arr, n, x)
{
    var count = 0;
    var isX = false;

    for(var i = 0; i < n; i++)
    {
        if (arr[i] == x)
        {
            isX = true;
        }
        else if (arr[i] < x)
        {
            count++;
        }
    }
    return (isX == false) ? -1 : count;
}

// Driver Code
var x = 20, arr = [ 10, 30, 20, 50, 20 ];
var n = arr.length;

document.write(findFirst(arr, n, x));

// This code is contributed by Khushboogoyal499

</script>
```

**输出:**

```
1
```

**时间复杂度:** O(N)