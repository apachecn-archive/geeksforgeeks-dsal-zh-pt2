# K 个附加整数后的中位数

> 原文:[https://www.geeksforgeeks.org/median-k-additional-integers/](https://www.geeksforgeeks.org/median-k-additional-integers/)

给定 n 个整数的数组。我们可以在数组中添加 k 个额外的整数，然后求出结果数组的中值。我们可以选择任何要添加的 k 值。
**约束:**

```
k < n
n + k is always odd.
```

**例:**

```
Input : arr[] = { 4, 7 }
         k = 1 
Output : 7
Explanation : One of the possible solutions 
is to add 8 making the array [4, 7, 8], whose
median is 7

Input : arr[] = { 6, 1, 1, 1, 1 }
         k = 2
Output : 1
Explanation : No matter what elements we add 
to this array, the median will always be 1
```

我们首先按升序对数组进行排序。由于 k 的值小于 n，n+k 总是奇数，所以我们总是可以选择添加大于数组最大元素的 k 个元素，并且(n+k)/第 2 个元素总是数组的中值。

## C++

```
// CPP program to find median of an array when
// we are allowed to add additional K integers
// to it.
#include <bits/stdc++.h>
using namespace std;

// Find median of array after adding k elements
void printMedian(int arr[], int n, int K)
{
    // sorting  the array in increasing order.
    sort(arr, arr + n);

    // printing the median of array.
    // Since n + K is always odd and K < n,
    // so median of array always lies in
    // the range of n.
    cout << arr[(n + K) / 2];
}

// driver function
int main()
{
    int arr[] = { 5, 3, 2, 8 };
    int k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    printMedian(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find median of an array when
// we are allowed to add additional K integers
// to it.
import java.util.Arrays;

class GFG {

    // Find median of array after adding k elements
    static void printMedian(int arr[], int n, int K)
    {

        // sorting the array in increasing order.
        Arrays.sort(arr);

        // printing the median of array.
        // Since n + K is always odd and K < n,
        // so median of array always lies in
        // the range of n.
        System.out.print(arr[(n + K) / 2]);
    }

    //Driver code
    public static void main (String[] args)
    {

        int arr[] = { 5, 3, 2, 8 };
        int k = 3;
        int n = arr.length;

        printMedian(arr, n, k);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 code to find median of an
# array when we are allowed to add
# additional K integers to it.

# Find median of array after
# adding k elements
def printMedian (arr, n, K):

    # sorting the array in
    # increasing order.
    arr.sort()

    # printing the median of array.
    # Since n + K is always odd
    # and K < n, so median of
    # array always lies in
    # the range of n.
    print( arr[int((n + K) / 2)])

# driver function
arr = [ 5, 3, 2, 8 ]
k = 3
n = len(arr)
printMedian(arr, n, k)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find median of an array when
// we are allowed to add additional K integers
// to it.
using System;

class GFG
{
    // Find median of array after adding k elements
    static void printMedian(int []arr, int n, int K)
    {
        // sorting  the array in increasing order.
        Array.Sort(arr);

        // printing the median of array.
        // Since n + K is always odd and K < n,
        // so median of array always lies in
        // the range of n.
        Console.Write(arr[(n + K) / 2]);
    }

    //Driver code
    public static void Main ()
    {
    int []arr = { 5, 3, 2, 8 };
        int k = 3;
        int n = arr.Length;
        printMedian(arr, n, k);
    }
}

// This code is contributed by  anant321.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find median
// of an array when we are allowed
// to add additional K integers to it.

// Find median of array
// after adding k elements
function printMedian($arr, $n, $K)
{
    // sorting the array
    // in increasing order.
    sort($arr);

    // printing the median of
    // array. Since n + K is
    // always odd and K < n,
    // so median of array always
    // lies in the range of n.
    echo $arr[($n + $K) / 2];
}

// Driver Code
$arr = array( 5, 3, 2, 8 );
$k = 3;
$n = count($arr);
printMedian($arr, $n, $k);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find median of an array when
// we are allowed to add additional K integers
// to it.

    // Find median of array after adding k elements
    function printMedian(arr, n, K)
    {

        // sorting the array in increasing order.
        arr.sort();

        // printing the median of array.
        // Since n + K is always odd and K < n,
        // so median of array always lies in
        // the range of n.
        document.write(arr[Math.floor((n + K) / 2)]);
    }

// driver program

        let arr = [ 5, 3, 2, 8 ];
        let k = 3;
        let n = arr.length;

        printMedian(arr, n, k);

</script>
```

**输出:**

```
8
```

本文由**萨洛尼·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。