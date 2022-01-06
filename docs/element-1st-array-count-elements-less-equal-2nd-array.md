# 对于第一个数组中的每个元素，计算第二个数组中小于或等于它的元素数

> 原文:[https://www . geesforgeks . org/element-1st-array-count-elements-less-equal-2nd-array/](https://www.geeksforgeeks.org/element-1st-array-count-elements-less-equal-2nd-array/)

给定两个未排序的数组 arr1[]和 arr2[]。它们可能包含重复项。对于 arr1[]中的每个元素，计数数组 arr2[]中小于或等于它的元素。
**来源:** [亚马逊面试体验|第 354 集(针对 SDE-2)](https://www.geeksforgeeks.org/amazon-interview-experience-set-354-sde-2/)
**示例:**

```
Input : arr1[] = [1, 2, 3, 4, 7, 9]
        arr2[] = [0, 1, 2, 1, 1, 4]
Output : [4, 5, 5, 6, 6, 6]
So the number of elements less than or equal to 
1 is 4, 2 is 5, 3 is 5, 4 is 6, 7 is 6 and 9 is 6.

Input : arr1[] = [5, 10, 2, 6, 1, 8, 6, 12]
        arr2[] = [6, 5, 11, 4, 2, 3, 7]
Output : [4, 6, 1, 5, 0, 6, 5, 7]
So the number of elements less than or equal to 
5 is 4, 10 is 6, 2 is 1, 6 is 5, 1 is 0, 8 is 6, 
6 is 5 and 12 is 7 
```

**<u>天真法:</u>**
**法:**思路是使用两个循环，一个外循环用于数组的元素 **arr1[]** ，一个内循环用于数组的元素 **arr2[]** 。然后对于 **arr1[]** 的每个元素，在 **arr2[]** 中计数小于或等于它的元素。
**算法:**

1.  从头到尾遍历第一个数组的元素。
2.  对于第一个数组中的每个元素。
3.  遍历第二个数组中的元素，找到小于或等于第一个数组元素的元素数。
4.  打印每个索引的计数。

## C++

```
// C++ code for the above algorithm
#include <bits/stdc++.h>
using namespace std;

// Function to count for each
// element in 1st array,
// elements less than or equal
// to it in 2nd array
void countEleLessThanOrEqual(int arr1[], int arr2[],
                             int m, int n)
{
    // Run two loops to count
    // First loop to traverse the first array
    // Second loop to traverse the second array
    for (int i = 0; i < m; i++) {
        int count = 0;

        // Traverse through second array
        for (int j = 0; j < n; j++)
            if (arr2[j] <= arr1[i])
                count++;

        cout << count << " ";
    }
}

// Driver program to test above
int main()
{
    int arr1[] = { 1, 2, 3, 4, 7, 9 };
    int arr2[] = { 0, 1, 2, 1, 1, 4 };
    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);
    countEleLessThanOrEqual(arr1, arr2, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

class GFG {

    // function to count for each
    // element in 1st array,
    // elements less than or equal
    // to it in 2nd array
    static int countEleLessThanOrEqual(
        int arr1[], int arr2[],
        int m, int n)
    {
        // Run two loops to count
        // First loop to traverse the first array
        // Second loop to traverse the second array
        for (int i = 0; i < m; i++) {
            int count = 0;

            // Traverse through second array
            for (int j = 0; j < n; j++)
                if (arr2[j] <= arr1[i])
                    count++;
            System.out.print(count + " ");
        }
        return m;
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr1[] = { 1, 2, 3, 4, 7, 9 };
        int arr2[] = { 0, 1, 2, 1, 1, 4 };
        countEleLessThanOrEqual(
            arr1, arr2, arr1.length, arr2.length);
    }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 code for the above algorithm

# function to count for each element in 1st array,
# elements less than or equal to it in 2nd array
def countEleLessThanOrEqual(arr1, arr2, m, n):

    # Run two loops to count
    # First loop to traverse the first array
    # Second loop to traverse the second array
    for i in range(m):

        count = 0
        # Traverse through second array
        for j in range(n):
            if (arr2[j] <= arr1[i]):
                count+= 1

        print(count, end =" ")

# Driver program to test above
arr1 = [1, 2, 3, 4, 7, 9]
arr2 = [0, 1, 2, 1, 1, 4]
m = len(arr1)
n = len(arr2)
countEleLessThanOrEqual(arr1, arr2, m, n)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of For each element
using System;

class GFG {

    // function to count for each element in 1st array,
    // elements less than or equal to it in 2nd array
    static void countEleLessThanOrEqual(
        int[] arr1, int[] arr2,
        int m, int n)
    {
        // Run two loops to count
        // First loop to traverse the first array
        // Second loop to traverse the second array
        for (int i = 0; i < m; i++) {
            int count = 0;

            // Traverse through second array
            for (int j = 0; j < n; j++)
                if (arr2[j] <= arr1[i])
                    count++;
            Console.Write((count) + " ");
        }
    }

    // Driver method
    public static void Main()
    {
        int[] arr1 = { 1, 2, 3, 4, 7, 9 };
        int[] arr2 = { 0, 1, 2, 1, 1, 4 };

        countEleLessThanOrEqual(arr1,
                                arr2, arr1.Length, arr2.Length);
    }
}

// This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// JavaScript code for the above algorithm

// Function to count for each
// element in 1st array,
// elements less than or equal
// to it in 2nd array
function countEleLessThanOrEqual(arr1, arr2, m, n)
{
    // Run two loops to count
    // First loop to traverse the first array
    // Second loop to traverse the second array
    for (let i = 0; i < m; i++) {
        let count = 0;

        // Traverse through second array
        for (let j = 0; j < n; j++)
            if (arr2[j] <= arr1[i])
                count++;

        document.write(count + " ");
    }
}

// Driver program to test above 
    let arr1 = [ 1, 2, 3, 4, 7, 9 ];
    let arr2 = [ 0, 1, 2, 1, 1, 4 ];
    let m = arr1.length;
    let n = arr2.length;
    countEleLessThanOrEqual(arr1, arr2, m, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
4 5 5 6 6 6 
```

**复杂度分析:**

*   **时间复杂度:** O(m * n)。
    考虑到 **arr1[]** 和 **arr2[]** 的尺寸分别为 **m** 和 **n** 。
*   **空间复杂度:** O(1)。
    由于不需要额外空间

**<u>高效解:</u>**
**进场:**排序第二阵的元素，即阵 **arr2[]** 。然后在阵列 **arr2[]** 上执行修改后的二分搜索法。对于数组 **arr1[]** 的每个元素 **x** ，在排序后的数组 **arr2[]** 中找到小于或等于 **x** 的最大元素的最后一个索引。最大元素的索引将给出元素的计数。
**算法:**

1.  对第二个数组排序。
2.  从头到尾遍历第一个数组的元素。
3.  对于第一个数组中的每个元素。
4.  对第二个数组进行二分搜索法运算，找出小于或等于第一个数组元素的最大元素的索引。
5.  最大元素的索引将给出元素的计数。打印每个索引的计数。

## C++

```
// C++ implementation of For each element in 1st
// array count elements less than or equal to it
// in 2nd array
#include <bits/stdc++.h>

using namespace std;

// function returns the index of largest element
// smaller than equal to 'x' in 'arr'. For duplicates
// it returns the last index of occurrence of required
// element. If no such element exits then it returns -1.
int binary_search(int arr[], int l, int h, int x)
{
    while (l <= h) {
        int mid = (l + h) / 2;

        // if 'x' is greater than or equal to arr[mid],
        // then search in arr[mid+1...h]
        if (arr[mid] <= x)
            l = mid + 1;

        // else search in arr[l...mid-1]
        else
            h = mid - 1;
    }

    // required index
    return h;
}

// function to count for each element in 1st array,
// elements less than or equal to it in 2nd array
void countEleLessThanOrEqual(
    int arr1[], int arr2[],
    int m, int n)
{
    // sort the 2nd array
    sort(arr2, arr2 + n);

    // for each element of 1st array
    for (int i = 0; i < m; i++) {
        // last index of largest element
        // smaller than or equal to x
        int index = binary_search(
            arr2, 0, n - 1, arr1[i]);

        // required count for the element arr1[i]
        cout << (index + 1) << " ";
    }
}

// Driver program to test above
int main()
{
    int arr1[] = { 1, 2, 3, 4, 7, 9 };
    int arr2[] = { 0, 1, 2, 1, 1, 4 };
    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);
    countEleLessThanOrEqual(arr1, arr2, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of For
// each element in 1st
// array count elements less
// than or equal to it
// in 2nd array

import java.util.Arrays;

class GFG {
    // method returns the index
    // of largest element
    // smaller than equal to 'x'
    // in 'arr'. For duplicates
    // it returns the last index
    // of occurrence of required
    // element. If no such element
    // exits then it returns -1.
    static int binary_search(
        int arr[], int l,
        int h, int x)
    {
        while (l <= h) {
            int mid = (l + h) / 2;

            // if 'x' is greater than or equal
            // to arr[mid], then search in
            // arr[mid+1...h]
            if (arr[mid] <= x)
                l = mid + 1;

            // else search in arr[l...mid-1]
            else
                h = mid - 1;
        }

        // Required index
        return h;
    }

    // Method to count for each
    // element in 1st array,
    // elements less than or equal
    // to it in 2nd array
    static void countEleLessThanOrEqual(
        int arr1[], int arr2[],
        int m, int n)
    {
        // Sort the 2nd array
        Arrays.sort(arr2);

        // for each element of 1st array
        for (int i = 0; i < m; i++) {
            // Last index of largest element
            // smaller than or equal to x
            int index = binary_search(
                arr2, 0, n - 1, arr1[i]);

            // Required count for the element arr1[i]
            System.out.print((index + 1) + " ");
        }
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr1[] = { 1, 2, 3, 4, 7, 9 };
        int arr2[] = { 0, 1, 2, 1, 1, 4 };

        countEleLessThanOrEqual(
            arr1, arr2, arr1.length,
            arr2.length);
    }
}
```

## 计算机编程语言

```
# python implementation of For each element in 1st
# array count elements less than or equal to it
# in 2nd array

# function returns the index of largest element
# smaller than equal to 'x' in 'arr'. For duplicates
# it returns the last index of occurrence of required
# element. If no such element exits then it returns -1
def bin_search(arr, n, x):

l = 0
h = n - 1
while(l <= h):
    mid = int((l + h) / 2)
    # if 'x' is greater than or equal to arr[mid],
    # then search in arr[mid + 1...h]
    if(arr[mid] <= x):
    l = mid + 1;
    else:
    # else search in arr[l...mid-1]
    h = mid - 1
# required index
return h

# function to count for each element in 1st array,
# elements less than or equal to it in 2nd array
def countElements(arr1, arr2, m, n):
# sort the 2nd array
arr2.sort()

# for each element in first array
for i in range(m):
    # last index of largest element
    # smaller than or equal to x
    index = bin_search(arr2, n, arr1[i])
    # required count for the element arr1[i]
    print(index + 1)

# driver program to test above function
arr1 = [1, 2, 3, 4, 7, 9]
arr2 = [0, 1, 2, 1, 1, 4]
m = len(arr1)
n = len(arr2)
countElements(arr1, arr2, m, n)

# This code is contributed by Aditi Sharma
```

## C#

```
// C# implementation of For each element
// in 1st array count elements less than
// or equal to it in 2nd array
using System;

public class GFG {

    // method returns the index of
    // largest element smaller than
    // equal to 'x' in 'arr'. For
    // duplicates it returns the last
    // index of occurrence of required
    // element. If no such element
    // exits then it returns -1.
    static int binary_search(int[] arr,
                             int l, int h, int x)
    {
        while (l <= h) {
            int mid = (l + h) / 2;

            // if 'x' is greater than or
            // equal to arr[mid], then
            // search in arr[mid+1...h]
            if (arr[mid] <= x)
                l = mid + 1;

            // else search in
            // arr[l...mid-1]
            else
                h = mid - 1;
        }

        // required index
        return h;
    }

    // method to count for each element
    // in 1st array, elements less than
    // or equal to it in 2nd array
    static void countEleLessThanOrEqual(
        int[] arr1, int[] arr2,
        int m, int n)
    {

        // sort the 2nd array
        Array.Sort(arr2);

        // for each element of 1st array
        for (int i = 0; i < m; i++) {
            // last index of largest
            // element smaller than or
            // equal to x
            int index = binary_search(
                arr2, 0, n - 1, arr1[i]);

            // required count for the
            // element arr1[i]
            Console.Write((index + 1) + " ");
        }
    }

    // Driver method
    public static void Main()
    {
        int[] arr1 = { 1, 2, 3, 4, 7, 9 };
        int[] arr2 = { 0, 1, 2, 1, 1, 4 };

        countEleLessThanOrEqual(arr1,
                                arr2, arr1.Length, arr2.Length);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation of For each element
// in 1st array count elements less than
// or equal to it in 2nd array

// function returns the index of largest
// element smaller than equal to 'x' in
// 'arr'. For duplicates it returns the
// last index of occurrence of required
// element. If no such element exits then
// it returns -1.
function binary_search($arr, $l, $h, $x)
{
    while ($l <= $h)
    {
        $mid = (floor($l+$h) / 2);

        // if 'x' is greater than or
        // equal to arr[mid], then
        // search in arr[mid+1...h]
        if ($arr[$mid] <= $x)
            $l = $mid + 1;

        // else search in arr[l...mid-1]
        else
            $h = $mid - 1;
    }

    // required index
    return $h;
}

// function to count for each element
// in 1st array, elements less than or
// equal to it in 2nd array
function countEleLessThanOrEqual($arr1,
                           $arr2, $m, $n)
{
    // sort the 2nd array
    sort($arr2); sort($arr2, $n);

    // for each element of 1st array
    for ($i = 0; $i < $m; $i++)
    {
        // last index of largest element
        // smaller than or equal to x
        $index = binary_search($arr2, 0,
                        $n-1, $arr1[$i]);

        // required count for the
        // element arr1[i]
        echo ($index+1), " ";
    }
}

// Driver program to test above
$arr1 = array(1, 2, 3, 4, 7, 9);
$arr2 = array(0, 1, 2, 1, 1, 4);
$m = sizeof($arr1) / sizeof($arr1[0]);
$n = sizeof($arr2) / sizeof($arr2[0]);
countEleLessThanOrEqual($arr1, $arr2, $m, $n);

//This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of For
// each element in 1st
// array count elements less
// than or equal to it
// in 2nd array

    // method returns the index
    // of largest element
    // smaller than equal to 'x'
    // in 'arr'. For duplicates
    // it returns the last index
    // of occurrence of required
    // element. If no such element
    // exits then it returns -1.
       function binary_search(arr,l,h,x)
    {
        while (l <= h) {
            let mid = Math.floor((l + h) / 2);

            // if 'x' is greater than or equal
            // to arr[mid], then search in
            // arr[mid+1...h]
            if (arr[mid] <= x)
                l = mid + 1;

            // else search in arr[l...mid-1]
            else
                h = mid - 1;
        }

        // Required index
        return h;
    }

    // Method to count for each
    // element in 1st array,
    // elements less than or equal
    // to it in 2nd array
    function countEleLessThanOrEqual(arr1,arr2,m,n)
    {
        // Sort the 2nd array
        arr2.sort(function(a,b){return a-b;});

        // for each element of 1st array
        for (let i = 0; i < m; i++) {
            // Last index of largest element
            // smaller than or equal to x
            let index = binary_search(
                arr2, 0, n - 1, arr1[i]);

            // Required count for the element arr1[i]
            document.write((index + 1) + " ");
        }
    }

    // Driver method
    let arr1=[1, 2, 3, 4, 7, 9 ];
    let arr2=[0, 1, 2, 1, 1, 4];
    countEleLessThanOrEqual(
            arr1, arr2, arr1.length,
            arr2.length);

// This code is contributed by patel2127

</script>
```

**输出:**

```
4 5 5 6 6 6
```

**复杂度分析:**

*   **时间复杂度:** O(mlogn + nlogn)。
    分别考虑尺寸 **m** 和 **n** 的 **arr1[]** 和 **arr2[]** 。
*   **空间复杂度:** O(1)。
    由于不需要额外空间

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。