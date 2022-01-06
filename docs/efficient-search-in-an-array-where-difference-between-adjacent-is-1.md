# 在相邻值之差为 1 的数组中进行有效搜索

> 原文:[https://www . geesforgeks . org/efficient-search-in-a-array-neighbor-is-1/](https://www.geeksforgeeks.org/efficient-search-in-an-array-where-difference-between-adjacent-is-1/)

给定一组 **n 个**整数。每个数组元素都是通过将+1 或-1 加到前一个元素上获得的，即任意两个连续元素之间的绝对差值为 1。任务是搜索具有最少比较次数的元素索引(少于简单的逐元素搜索)。如果元素多次出现，则打印最小的索引。如果元素不存在，打印-1。
示例:

```
Input : arr[] = {5, 4, 5, 6, 5, 4, 3, 2} 
        x = 4.
Output : 1
The first occurrence of element x is at 
index 1.

Input : arr[] = { 5, 4, 5, 6, 4, 3, 2, 3 } 
        x = 9.
Output : -1
Element x is not present in arr[]
```

让要搜索元素是 x。在任何索引 I，如果 arr[i]！= x，x 出现的可能性在位置 I+ABS(arr[I]–a)，因为每个元素都是通过将+1 或-1 加到前面的元素上获得的。I 和 i + abs 之间不可能有 El(arr[I]–a)。所以直接跳到 I+ABS(arr[i]–a)，如果 arr[I]！= x.

```
Algorithm to solve the problem:
1\. Start from index = 0.
2\. Compare arr[index] and x.
   a) If both are equal, return index.
   b) If not, set index = index + abs(arr[index] - x).
3\. Repeat step 2.
```

以下是上述思路的实现:

## C++

```
// C++ program to search an element in an array
// where each element is obtained by adding
// either +1 or -1 to previous element.
#include<bits/stdc++.h>
using namespace std;

// Return the index of the element to be searched.
int search(int arr[], int n, int x)
{
    // Searching x in arr[0..n-1]
    int i = 0;
    while (i <= n-1)
    {
        // Checking if element is found.
        if (arr[i] == x)
            return i;

        // Else jumping to abs(arr[i]-x).
        i += abs(arr[i]-x);
    }

    return -1;
}

// Driven Program
int main()
{
    int arr[] =  {5, 4, 5, 6, 5, 4, 3, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    int x = 4;

    cout << search(arr, n, x) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to search an element
// in an array where each element is
// obtained by adding either +1 or
// -1 to previous element.
class GFG
{

// Return the index of the
// element to be searched.
static int search(int arr[], int n, int x)
{
    // Searching x in arr[0..n-1]
    int i = 0;
    while (i <= n-1)
    {
        // Checking if element is found.
        if (arr[i] == x)
            return i;

        // Else jumping to abs(arr[i]-x).
        i += Math.abs(arr[i]-x);
    }

    return -1;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = {5, 4, 5, 6, 5, 4, 3, 2};
    int n = arr.length;
    int x = 4;

    System.out.println(search(arr, n, x));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to search an element in
# an array where each element is obtained
# by adding either +1 or -1 to previous element

# Return the index of the element to be searched
def search(arr, n, x):

    # Searching x in arr[0..n-1]
    i = 0
    while (i <= n-1):

        # Checking if element is found.
        if (arr[i] == x):
            return i

        # Else jumping to abs(arr[i]-x).
        i += abs(arr[i] - x)

    return -1

# Driver code
arr = [5, 4, 5, 6, 5, 4, 3, 2]
n = len(arr)
x = 4

print(search(arr, n, x))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to search an element in
// an array where each element is
// obtained by adding either + 1 or
// -1 to previous element.
using System;

class GFG
{

// Return the index of the
// element to be searched.
static int search(int []arr, int n,
                  int x)
{

    // Searching x in arr[0.. n - 1]
    int i = 0;
    while (i <= n - 1)
    {
        // Checking if element is found
        if (arr[i] == x)
            return i;

        // Else jumping to abs(arr[i] - x)
        i += Math.Abs(arr[i] - x);
    }

    return -1;
}

// Driver code
public static void Main ()
{
    int []arr = {5, 4, 5, 6, 5, 4, 3, 2};
    int n = arr.Length;
    int x = 4;

    Console.WriteLine(search(arr, n, x));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to search an
// element in an array where
// each element is obtained
// by adding either +1 or -1
// to previous element.

// Return the index of the
// element to be searched.
function search($arr, $n, $x)
{

    // Searching x in arr[0..n-1]
    $i = 0;
    while ($i <= $n-1)
    {

        // Checking if element
        // is found.
        if ($arr[$i] == $x)
            return $i;

        // Else jumping to
        // abs(arr[i]-x).
        $i += abs($arr[$i] - $x);
    }

    return -1;
}

    // Driver Code
    $arr= array(5, 4, 5, 6, 5, 4, 3, 2);
    $n = sizeof($arr);
    $x = 4;

    echo search($arr, $n, $x) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to search an element
// in an array where each element is
// obtained by adding either +1 or
// -1 to previous element.

 // Return the index of the
// element to be searched.
function search(arr, n, x)
{
    // Searching x in arr[0..n-1]
    let i = 0;
    while (i <= n-1)
    {
        // Checking if element is found.
        if (arr[i] == x)
            return i;

        // Else jumping to abs(arr[i]-x).
        i += Math.abs(arr[i]-x);
    }

    return -1;
}

// Driver code
    let arr = [5, 4, 5, 6, 5, 4, 3, 2];
    let n = arr.length;
    let x = 4;

    document.write(search(arr, n, x));

</script>
```

**输出:**

```
1
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。