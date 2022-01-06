# 最长的 arr[i]链，arr[arr[i]]，..不重复

> 原文:[https://www . geeksforgeeks . org/最长 arri-arr RRI-不重复/](https://www.geeksforgeeks.org/longest-chain-of-arri-arrarri-without-repetition/)

给定大小为 n 的数组，使得数组中的元素是不同的，并且在 0 到 n-1 的范围内。我们需要找出最长链{arr[i]，arr[arr[i]]，arr[arr[arr[I]]……}的长度，这样就不会有集合元素重复。

**示例:**

```
Input : arr[] = [5, 4, 0, 3, 1, 6, 2]
Output :4
Explanation:
The longest chain without repetition is
{arr[0], arr[5], arr[6], arr[2]} = {5, 6, 2, 0}

Input : arr[] = {1, 0, 4, 2, 3}
Output :3
Explanation:
The longest chain without repetition is
{arr[2], arr[4], arr[3]} = {4, 2, 3}
```

一个**天真的解决方案**是从每个元素开始寻找最长链的长度。为了跟踪被访问的节点，保留一个被访问的数组，并在每次从一个元素中找到最长的链后重置这个数组。

一个**有效的解决方案**是遍历每个索引，并将它们设置为-1。一旦我们看到一个我们设置为-1 的指数，我们知道我们遇到了相同的指数，所以我们停下来比较当前的计数是否大于我们到目前为止看到的最大值。我们可以将此设置为-1，这样我们就不会一次又一次地重新访问相同的索引。为什么这样做是因为因为每个数字都是不同的，所以只有一种方法可以达到特定的指数。因此，无论你在特定周期中从哪个指数开始，你总是会看到相同的周期，因此计数也是相同的。因此，一旦一个循环被完全访问，我们就可以跳过检查这个循环中的所有索引。

## C++

```
// C++ program to find longest chain of
// arr[i], arr[arr[i]], arr[arr[arr[i]]]
// without repetition.
#include <iostream>
using namespace std;

void aNesting(int arr[], int start, int& max)
{
    // Local maximum
    int c_max = 0;

    // if current element is not visited then
    // increase c_max by one, set arr[start]
    // and change the start to current value.
    while (arr[start] != -1) {
        c_max++;
        int temp = arr[start];
        arr[start] = -1;
        start = temp;
    }

   // if local max is greater than global max
   // then update global maximum
   if (c_max > max) max = c_max;
}

int maxLength(int arr[], int n)
{
    int max = 0;
    for (int i = 0; i < n; i++) {
        aNesting(arr, i, max);
    }
    return max;
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 0, 3, 1, 6, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxLength(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest chain of
// arr[i], arr[arr[i]], arr[arr[arr[i]]]
// without repetition.
import java.util.*;

class solution
{

static int aNesting(int arr[], int start, int max)
{
    // Local maximum
    int c_max = 0;

    // if current element is not visited then
    // increase c_max by one, set arr[start]
    // and change the start to current value.
    while (arr[start] != -1)
    {
        c_max++;
        int temp = arr[start];
        arr[start] = -1;
        start = temp;
    }

// if local max is greater than global max
// then update global maximum
     if (c_max > max)
      max = c_max;

     return max;
  }

static int maxLength(int[] arr, int n)
{
    int max = 0,max1;
    for (int i = 0; i < n; i++)
    {
        max1 = aNesting(arr, i, max);
        if(max1>max)
         max = max1;
    }
    return max;
 }

// Driver code
public static void main(String args[])
{
    int arr[] = { 5, 4, 0, 3, 1, 6, 2 };
    int n = arr.length;
    System.out.println(maxLength(arr, n));
}
}

// Thi code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 program to find longest chain
# of arr[i], arr[arr[i]], arr[arr[arr[i]]]
# without repetition.
def aNesting(arr,start, max):

    # Local maximum
    c_max = 0

    # if current element is not visited then
    # increase c_max by one, set arr[start]
    # and change the start to current value.
    while (arr[start] != -1):
        c_max += 1
        temp = arr[start]
        arr[start] = -1
        start = temp

    # if local max is greater than global
    # max then update global maximum
    if (c_max > max):
        max = c_max

    return max

def maxLength(arr, n):
    max = 0
    for i in range(0, n, 1):
        max__ = aNesting(arr, i, max)
        if (max__>max):
            max = max__
    return max__

# Driver code
if __name__ =='__main__':
    arr = [5, 4, 0, 3, 1, 6, 2]
    n = len(arr)
    print(maxLength(arr, n))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find longest chain of
// arr[i], arr[arr[i]], arr[arr[arr[i]]]
// without repetition.
using System;

class GFG
{

static int aNesting(int[] arr, int start, int max)
{
    // Local maximum
    int c_max = 0;

    // if current element is not visited then
    // increase c_max by one, set arr[start]
    // and change the start to current value.
    while (arr[start] != -1)
    {
        c_max++;
        int temp = arr[start];
        arr[start] = -1;
        start = temp;
    }

    // if local max is greater than global max
    // then update global maximum
    if (c_max > max)
    max = c_max;

    return max;
}

static int maxLength(int[] arr, int n)
{
    int max = 0, max1;
    for (int i = 0; i < n; i++)
    {
        max1 = aNesting(arr, i, max);
        if(max1>max)
        max = max1;
    }
    return max;
}

// Driver code
public static void Main()
{
    int[] arr = { 5, 4, 0, 3, 1, 6, 2 };
    int n = arr.Length;
    Console.WriteLine(maxLength(arr, n));
}
}

// Thi code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find longest chain of
// arr[i], arr[arr[i]], arr[arr[arr[i]]]
// without repetition.

function aNesting($arr, $start, &$max)
{
    // Local maximum
    $c_max = 0;

    // if current element is not visited then
    // increase c_max by one, set arr[start]
    // and change the start to current value.
    while ($arr[$start] != -1)
    {
        $c_max++;
        $temp = $arr[$start];
        $arr[$start] = -1;
        $start = $temp;
    }

// if local max is greater than global
// max then update global maximum
if ($c_max > $max)
    $max = $c_max;
}

function maxLength($arr, $n)
{
    $max = 0;
    for ($i = 0; $i < $n; $i++)
    {
        aNesting($arr, $i, $max);
    }
    return $max;
}

// Driver code
$arr = array(5, 4, 0, 3, 1, 6, 2 );
$n = sizeof($arr);
echo maxLength($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find longest chain of
// arr[i], arr[arr[i]], arr[arr[arr[i]]]
// without repetition.
function aNesting(arr, start, max)
{

    // Local maximum
    var c_max = 0;

    // If current element is not visited then
    // increase c_max by one, set arr[start]
    // and change the start to current value.
    while (arr[start] != -1)
    {
        c_max++;
        var temp = arr[start];
        arr[start] = -1;
        start = temp;
    }

    // If local max is greater than global
    // max then update global maximum
    if (c_max > max)
        max = c_max;

    return max;
}

function maxLength(arr, n)
{
    var max = 0, max1;
    for(var i = 0; i < n; i++)
    {
        max1 = aNesting(arr, i, max);

        if (max1 > max)
            max = max1;
    }
    return max;
}

// Driver code
var arr = [ 5, 4, 0, 3, 1, 6, 2 ];
var n = arr.length;

document.write(maxLength(arr, n));

// This code is contributed by bunnyram19

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)