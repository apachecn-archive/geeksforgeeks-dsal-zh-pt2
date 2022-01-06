# 在有重复项的排序数组中找到相等(或中间)点

> 原文:[https://www . geeksforgeeks . org/find-相等或中间点排序重复数组/](https://www.geeksforgeeks.org/find-equal-or-middle-point-in-a-sorted-array-with-duplicates/)

给定一个大小为 n 的排序数组，任务是找出数组中是否存在一个元素，其中较小元素的数量等于较大元素的数量。
如果相等点在输入数组中出现多次，返回其第一次出现的索引。如果不存在，返回-1。
**例:**

```
Input  : arr[] = {1, 2, 3, 3, 3, 3}
Output : 1
Equal Point is arr[1] which is 2\. Number of
elements smaller than 2 and greater than 2 
are same.

Input  : arr[] = {1, 2, 3, 3, 3, 3, 4, 4}
Output : Equal Point does not exist.

Input : arr[] = {1, 2, 3, 4, 4, 5, 6, 6, 6, 7}
Output : 3
First occurrence of equal point is arr[3]
```

一种**天真的**方法是取每一个元素，计算有多少元素比那个小，然后是更大的元素。然后比较两者是否相等。
一种**高效的**方法是创建一个辅助数组，并在其中存储所有不同的元素。如果不同元素的计数是偶数，则不存在相等点。如果计数是奇数，那么等点数就是辅助数组的中点。
以下是上述想法的实现。

## C++

```
// C++ program to find Equal point in a sorted array
// which may have many duplicates.
#include <bits/stdc++.h>
using namespace std;

// Returns value of Equal point in a sorted array arr[]
// It returns -1 if there is no Equal Point.
int findEqualPoint(int arr[], int n)
{
     // To store first indexes of distinct elements of arr[]
     int distArr[n];

     // Traverse input array and store indexes of first
     // occurrences of distinct elements in distArr[]
     int i = 0, di = 0;
     while (i < n)
     {
        // This element must be first occurrence of a
        // number (this is made sure by below loop),
        // so add it to distinct array.
        distArr[di++] = i++;

        // Avoid all copies of arr[i] and move to next
        // distinct element.
        while (i<n && arr[i] == arr[i-1])
             i++;
     }

     // di now has total number of distinct elements.
     // If di is odd, then equal point exists and is at
     // di/2, otherwise return -1.
     return (di & 1)? distArr[di>>1] : -1;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 4, 5, 6, 6, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);
    int index = findEqualPoint(arr, n);
    if (index != -1)
        cout << "Equal Point = " << arr[index] ;
    else
        cout << "Equal Point does not exists";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find Equal point in a sorted array
// which may have many duplicates.

class Test
{
    // Returns value of Equal point in a sorted array arr[]
    // It returns -1 if there is no Equal Point.
    static int findEqualPoint(int arr[], int n)
    {
         // To store first indexes of distinct elements of arr[]
         int distArr[] = new int[n];

         // Traverse input array and store indexes of first
         // occurrences of distinct elements in distArr[]
         int i = 0, di = 0;
         while (i < n)
         {
            // This element must be first occurrence of a
            // number (this is made sure by below loop),
            // so add it to distinct array.
            distArr[di++] = i++;

            // Avoid all copies of arr[i] and move to next
            // distinct element.
            while (i<n && arr[i] == arr[i-1])
                 i++;
         }

         // di now has total number of distinct elements.
         // If di is odd, then equal point exists and is at
         // di/2, otherwise return -1.
         return (di & 1)!=0 ? distArr[di>>1] : -1;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = {1, 2, 3, 4, 4, 5, 6, 6, 6, 7};

        int index = findEqualPoint(arr, arr.length);
        System.out.println(index != -1 ? "Equal Point = " + arr[index]
                            : "Equal Point does not exists");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# Equal point in a sorted
# array which may have
# many duplicates.

# Returns value of Equal
# point in a sorted array
# arr[]. It returns -1 if
# there is no Equal Point.
def findEqualPoint(arr, n):

    # To store first indexes of
    # distinct elements of arr[]
    distArr = [0] * n

    # Traverse input array and
    # store indexes of first
    # occurrences of distinct
    # elements in distArr[]
    i = 0
    di = 0
    while (i < n):

        # This element must be
        # first occurrence of a
        # number (this is made
        # sure by below loop),
        # so add it to distinct array.
        distArr[di] = i
        di += 1
        i += 1

        # Avoid all copies of
        # arr[i] and move to
        # next distinct element.
        while (i < n and
               arr[i] == arr[i - 1]):
            i += 1

    # di now has total number
    # of distinct elements.
    # If di is odd, then equal
    # point exists and is at
    # di/2, otherwise return -1.
    return distArr[di >> 1] if (di & 1) else -1

# Driver code
arr = [1, 2, 3, 4, 4,
       5, 6, 6, 6, 7]
n = len(arr)
index = findEqualPoint(arr, n)
if (index != -1):
    print("Equal Point = " ,
                 arr[index])
else:
    print("Equal Point does " +
                  "not exists")

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find Equal
// point in a sorted array
// which may have many duplicates.
using System;

class GFG
{
    // Returns value of Equal point
    // in a sorted array arr[]
    // It returns -1 if there
    // is no Equal Point.
    static int findEqualPoint(int []arr,
                              int n)
    {
        // To store first indexes of
        // distinct elements of arr[]
        int []distArr = new int[n];

        // Traverse input array and
        // store indexes of first
        // occurrences of distinct
        // elements in distArr[]
        int i = 0, di = 0;
        while (i < n)
        {
            // This element must be
            // first occurrence of a
            // number (this is made
            // sure by below loop),
            // so add it to distinct array.
            distArr[di++] = i++;

            // Avoid all copies of
            // arr[i] and move to
            // next distinct element.
            while (i < n && arr[i] == arr[i - 1])
                i++;
        }

        // di now has total number
        // of distinct elements.
        // If di is odd, then equal
        // point exists and is at
        // di/2, otherwise return -1.
        return (di & 1) != 0 ?
            distArr[di >> 1] :
                           -1;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 4,
                     5, 6, 6, 6, 7};

        int index = findEqualPoint(arr, arr.Length);
        Console.Write(index != -1 ?
                      "Equal Point = " + arr[index] :
                      "Equal Point does not exists");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Equal point in a
// sorted array which may have many
// duplicates.

// Returns value of Equal point in a
// sorted array arr[] It returns -1
// if there is no Equal Point.
function findEqualPoint( $arr, $n)
{
    // To store first indexes of distinct
    // elements of arr[]
    $distArr = array();

    // Traverse input array and store
    // indexes of first occurrences of
    // distinct elements in distArr[]
    $i = 0; $di = 0;

    while ($i < $n)
    {
        // This element must be first
        // occurrence of a number (this
        // is made sure by below loop),
        // so add it to distinct array.
        $distArr[$di++] = $i++;

        // Avoid all copies of arr[i]
        // and move to next distinct
        // element.
        while ($i < $n and
                 $arr[$i] == $arr[$i-1])
            $i++;
    }

    // di now has total number of
    // distinct elements. If di is odd,
    // then equal point exists and is
    // at di/2, otherwise return -1.
    return ($di & 1)? $distArr[$di>>1] : -1;
}

// Driver code
$arr = array(1, 2, 3, 4, 4, 5, 6, 6, 6, 7);
$n = count($arr);
$index = findEqualPoint($arr, $n);
if ($index != -1)
    echo "Equal Point = " , $arr[$index] ;
else
    echo "Equal Point does not exists";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find Equal
    // point in a sorted array
    // which may have many duplicates.

    // Returns value of Equal point
    // in a sorted array arr[]
    // It returns -1 if there
    // is no Equal Point.
    function findEqualPoint(arr, n)
    {
        // To store first indexes of
        // distinct elements of arr[]
        let distArr = new Array(n);
        distArr.fill(0);

        // Traverse input array and
        // store indexes of first
        // occurrences of distinct
        // elements in distArr[]
        let i = 0, di = 0;
        while (i < n)
        {
            // This element must be
            // first occurrence of a
            // number (this is made
            // sure by below loop),
            // so add it to distinct array.
            distArr[di++] = i++;

            // Avoid all copies of
            // arr[i] and move to
            // next distinct element.
            while (i < n && arr[i] == arr[i - 1])
                i++;
        }

        // di now has total number
        // of distinct elements.
        // If di is odd, then equal
        // point exists and is at
        // di/2, otherwise return -1.
        return (di & 1) != 0 ?
            distArr[di >> 1] :
                           -1;
    }

    let arr = [1, 2, 3, 4, 4, 5, 6, 6, 6, 7];

    let index = findEqualPoint(arr, arr.length);
    document.write(index != -1 ?
                  "Equal Point = " + arr[index] :
                  "Equal Point does not exists");

</script>
```

**输出:**

```
Equal Point = 4
```

**时间复杂度:** O(n)
**辅助空间:** O(n)
**空间优化:**
我们可以通过遍历数组两次而不是一次来减少额外的空间。

1.  通过遍历输入数组来计算不同元素的总数。让这个计数为 distCount。
2.  如果 distCount 为偶数，则返回-1。
3.  如果 distCount 为奇数，则再次遍历数组，并在 distCount/2 处停止，然后返回该索引。

感谢帕万·库马尔·J·S 提出这种空间优化方法。
本文由 [**萨希尔·查布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。