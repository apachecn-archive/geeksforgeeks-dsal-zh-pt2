# 在给定数组中找到一个固定点(值等于索引)|允许重复

> 原文:[https://www . geesforgeks . org/find-定点-值-相等-索引-给定-数组-允许重复/](https://www.geeksforgeeks.org/find-fixed-point-value-equal-index-given-array-duplicates-allowed/)

给定一个按升序排序的 n 个整数的数组，编写一个函数，返回数组中的一个定点，如果数组中有任何定点，否则返回-1。数组中的不动点是一个索引 I，这样 arr[i]等于 I。注意数组中的整数可以是负数。
示例:

```
  Input: arr[] = {-10, -5, 0, 3, 7}
  Output: 3  // arr[3] == 3 

  Input: arr[] = {-10, -5, 2, 2, 2, 3, 4, 7, 9, 12, 13}
  Output: 2  // arr[2] == 2 

  Input: arr[] = {-10, -5, 3, 4, 7, 9}
  Output: -1  // No Fixed Point
```

我们有一个解决方案[在一组不同的元素](https://www.geeksforgeeks.org/find-a-fixed-point-in-a-given-array/)中找到不动点。在这篇文章中，讨论了具有重复值的数组的解决方案。
考虑 arr[] = {-10，-5，2，2，2，3，4，7，9，12，13}，arr[mid] = 3
如果元素不是截然不同的，那么我们看到 arr[mid] < mid，我们不能断定固定在哪一边。它可能在左边，也可能在右边。
我们可以肯定地知道，由于 arr[5] = 3，arr[4]不可能是魔法索引，因为 arr[4]必须小于或等于 arr[5](数组是排序的)。
因此，我们搜索的一般模式是:

*   左侧:开始=开始，结束=最小(arr[midIndex]，midIndex-1)
*   右侧:开始=最大(arr[midIndex]，midIndex+1)，结束=结束

以下是上述算法的代码。

## C++

```
// CPP Program to find magic index.
#include <bits/stdc++.h>
using namespace std;

int magicIndex(int* arr, int start, int end)
{
    // If No Magic Index return -1;
    if (start > end)
        return -1;

    int midIndex = (start + end) / 2;
    int midValue = arr[midIndex];

    // Magic Index Found, return it.
    if (midIndex == midValue)
        return midIndex;

    // Search on Left side
    int left = magicIndex(arr, start, min(midValue,
                                     midIndex - 1));

    // If Found on left side, return.
    if (left >= 0)
        return left;

    // Return ans from right side.
    return magicIndex(arr, max(midValue, midIndex + 1),
                                                  end);
}

// Driver program
int main()
{
    int arr[] = { -10, -5, 2, 2, 2, 3, 4, 7,
                                 9, 12, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int index = magicIndex(arr, 0, n - 1);
    if (index == -1)
        cout << "No Magic Index";
    else
        cout << "Magic Index is : " << index;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find magic index.

class GFG {

    static int magicIndex(int arr[], int start, int end)
    {
        // If No Magic Index return -1;
        if (start > end)
            return -1;

        int midIndex = (start + end) / 2;
        int midValue = arr[midIndex];

        // Magic Index Found, return it.
        if (midIndex == midValue)
            return midIndex;

        // Search on Left side
        int left = magicIndex(arr, start, Math.min(midValue,
                                            midIndex - 1));

        // If Found on left side, return.
        if (left >= 0)
            return left;

        // Return ans from right side.
        return magicIndex(arr, Math.max(midValue,
                                midIndex + 1),end);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { -10, -5, 2, 2, 2, 3, 4, 7,
                    9, 12, 13 };
        int n = arr.length;
        int index = magicIndex(arr, 0, n - 1);
        if (index == -1)
            System.out.print("No Magic Index");
        else
            System.out.print("Magic Index is : "+index);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 Program to find
# magic index.

def magicIndex(arr, start, end):

    # If No Magic Index return -1
    if (start > end):
        return -1

    midIndex = int((start + end) / 2)
    midValue = arr[midIndex]

    # Magic Index Found, return it.
    if (midIndex == midValue):
        return midIndex

    # Search on Left side
    left = magicIndex(arr, start, min(midValue,
                                midIndex - 1))

    # If Found on left side, return.
    if (left >= 0):
        return left

    # Return ans from right side.
    return magicIndex(arr, max(midValue,
                        midIndex + 1),
                                    end)

# Driver program
arr = [-10, -5, 2, 2, 2, 3, 4, 7, 9, 12, 13]
n = len(arr)

index = magicIndex(arr, 0, n - 1)

if (index == -1):
    print("No Magic Index")
else:
    print("Magic Index is :", index)

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# Program to find magic index.
using System;

class GFG {

    static int magicIndex(int []arr, int start,
                                    int end)
    {
        // If No Magic Index return -1;
        if (start > end)
            return -1;

        int midIndex = (start + end) / 2;
        int midValue = arr[midIndex];

        // Magic Index Found, return it.
        if (midIndex == midValue)
            return midIndex;

        // Search on Left side
        int left = magicIndex(arr, start, Math.Min(midValue,
                                            midIndex - 1));

        // If Found on left side, return.
        if (left >= 0)
            return left;

        // Return ans from right side.
        return magicIndex(arr, Math.Max(midValue,
                                midIndex + 1),end);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { -10, -5, 2, 2, 2, 3,
                        4, 7, 9, 12, 13 };

        int n = arr.Length;

        int index = magicIndex(arr, 0, n - 1);

        if (index == -1)
            Console.WriteLine("No Magic Index");
        else
            Console.WriteLine("Magic Index is : " +
                                            index);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find magic index.

function magicIndex($arr, $start, $end)
{

    // If No Magic Index return -1;
    if ($start > $end)
        return -1;

    $midIndex = floor(($start + $end) / 2);
    $midValue = $arr[$midIndex];

    // Magic Index Found, return it.
    if ($midIndex == $midValue)
        return $midIndex;

    // Search on Left side
    $left = magicIndex($arr, $start,
            min($midValue, $midIndex - 1));

    // If Found on left side, return.
    if ($left >= 0)
        return $left;

    // Return ans from right side.
    return magicIndex($arr, max($midValue,
                     $midIndex + 1), $end);
}

    // Driver Code
    $arr = array(-10, -5, 2, 2, 2, 3,
                     4, 7, 9, 12, 13);
    $n = sizeof($arr);
    $index = magicIndex($arr, 0, $n - 1);
    if ($index == -1)
        echo "No Magic Index";
    else
        echo "Magic Index is : " , $index;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// JavaScript Program to find magic index.

function magicIndex(arr, start, end)
{
    // If No Magic Index return -1;
    if (start > end)
        return -1;

    let midIndex = Math.floor((start + end) / 2);
    let midValue = arr[midIndex];

    // Magic Index Found, return it.
    if (midIndex == midValue)
        return midIndex;

    // Search on Left side
    let left = magicIndex(arr, start, Math.min(midValue,
                                    midIndex - 1));

    // If Found on left side, return.
    if (left >= 0)
        return left;

    // Return ans from right side.
    return magicIndex(arr, Math.max(midValue, midIndex + 1),
                                                end);
}

// Driver program
    let arr = [ -10, -5, 2, 2, 2, 3, 4, 7,
                                9, 12, 13 ];
    let n = arr.length;
    let index = magicIndex(arr, 0, n - 1);
    if (index == -1)
        document.write("No Magic Index");
    else
        document.write("Magic Index is : " + index);

// This code is contributed by Surbhi Tyagi.
</script>
```

输出:

```
Magic Index is : 2
```

**时间复杂度:** O(N)

**辅助空间:** O(1)