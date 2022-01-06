# 查找一个排序数组中存在的额外元素的索引

> 原文:[https://www . geeksforgeeks . org/find-一个额外元素存在于一个排序数组中的索引/](https://www.geeksforgeeks.org/find-index-of-an-extra-element-present-in-one-sorted-array/)

给定两个排序数组。数组之间只有 1 个区别。第一个数组中间额外添加了一个元素。找到额外元素的索引。

**示例:**

```
Input: {2, 4, 6, 8, 9, 10, 12};
       {2, 4, 6, 8, 10, 12};
Output: 4
Explanation: The first array has an extra element 9.
The extra element is present at index 4.

Input: {3, 5, 7, 9, 11, 13}
        {3, 5, 7, 11, 13}
Output: 3
Explanation: The first array has an extra element 9.
The extra element is present at index 3.
```

**<u>方法 1:</u>** 这包括解决这个特定问题的基本方法。

**方法:**基本方法是遍历整个第二个数组，如果不同就逐个元素检查。当数组被排序时，检查两个数组的相邻位置应该是相似的，除非找到了丢失的元素。

**算法:**

1.  从头到尾遍历数组。
2.  检查两个数组的第一个元素是否相似。
3.  如果元素不相似，则打印索引并断开

**实施:**

## C++

```
// C++ program to find an extra
// element present in arr1[]
#include <iostream>
using namespace std;

// Returns index of extra element
// in arr1[]. n is size of arr2[].
// Size of arr1[] is n-1.
int findExtra(int arr1[],
              int arr2[], int n)
{
for (int i = 0; i < n; i++)
    if (arr1[i] != arr2[i])
        return i;

return n;
}

// Driver code
int main()
{
    int arr1[] = {2, 4, 6, 8,
                  10, 12, 13};
    int arr2[] = {2, 4, 6,
                  8, 10, 12};
    int n = sizeof(arr2) / sizeof(arr2[0]);

    // Solve is passed both arrays
    cout << findExtra(arr1, arr2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an extra
// element present in arr1[]
class GFG
{

    // Returns index of extra element
    // in arr1[]. n is size of arr2[].
    // Size of arr1[] is n-1.
    static int findExtra(int arr1[],
                         int arr2[], int n)
    {
    for (int i = 0; i < n; i++)
        if (arr1[i] != arr2[i])
            return i;

    return n;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr1[] = {2, 4, 6, 8,
                      10, 12, 13};
        int arr2[] = {2, 4, 6,
                      8, 10, 12};
        int n = arr2.length;

        // Solve is passed both arrays
        System.out.println(findExtra(arr1,
                                     arr2, n));
    }
}

// This code is contributed by Harsh Agarwal
```

## 蟒蛇 3

```
# Python 3 program to find an
# extra element present in arr1[]

# Returns index of extra .
# element in arr1[] n is
# size of arr2[]. Size of
# arr1[] is n-1.
def findExtra(arr1, arr2, n) :
    for i in range(0, n) :
        if (arr1[i] != arr2[i]) :
            return i

    return n

# Driver code
arr1 = [2, 4, 6, 8,  10, 12, 13]
arr2 = [2, 4, 6, 8, 10, 12]
n = len(arr2)

# Solve is passed both arrays
print(findExtra(arr1, arr2, n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find an extra
// element present in arr1[]
using System;

class GfG
{

    // Returns index of extra
    // element in arr1[]. n is
    // size of arr2[]. Size of
    // arr1[] is n-1.
    static int findExtra(int []arr1,
                         int []arr2, int n)
    {
        for (int i = 0; i < n; i++)
            if (arr1[i] != arr2[i])
                return i;

        return n;
    }

    // Driver code
    public static void Main ()
    {
        int []arr1 = {2, 4, 6, 8,
                      10, 12, 13};
        int []arr2 = {2, 4, 6,
                      8, 10, 12};
        int n = arr2.Length;

        // Solve is passed both arrays
        Console.Write(findExtra(arr1, arr2, n));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an extra
// element present in arr1[]

// Returns index of extra element
// in arr1[]. n is size of arr2[].
// Size of arr1[] is n-1.
function findExtra($arr1,
                   $arr2, $n)
{
for ($i = 0; $i < $n; $i++)
    if ($arr1[$i] != $arr2[$i])
        return $i;

return $n;
}

// Driver code
$arr1 = array (2, 4, 6, 8,
               10, 12, 13);
$arr2 = array(2, 4, 6,
              8, 10, 12);
$n = sizeof($arr2);

// Solve is passed
// both arrays
echo findExtra($arr1, $arr2, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to find an extra
// element present in arr1[]

// Returns index of extra element
// in arr1[]. n is size of arr2[].
// Size of arr1[] is n-1.
function findExtra(arr1, arr2, n)
{
for (let i = 0; i < n; i++)
    if (arr1[i] != arr2[i])
        return i;

return n;
}

// Driver code

    let arr1 = [2, 4, 6, 8,
                10, 12, 13];
    let arr2 = [2, 4, 6,
                8, 10, 12];
    let n = arr2.length;

    // Solve is passed both arrays
    document.write(findExtra(arr1, arr2, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
 6
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    由于需要遍历数组一次，所以时间复杂度是线性的。
*   **空间复杂度:** O(1)。
    由于不需要额外的空间，时间复杂度是恒定的。

**<u>方法二:</u>** 这种方法是解决上述问题比较好的方法，采用了二分搜索法的概念。

**方法:**要在小于线性时间内找到缺失元素的索引，可以使用二分搜索法，其思想是大于或等于缺失元素索引的所有索引在两个数组中都将具有不同的元素，而小于该索引的所有索引在两个数组中都将具有相似的元素。

**算法:**

1.  创建三个变量，*低= 0* ，*高= n-1* ，*中*， *ans = n*
2.  运行一个循环，直到 low 小于或等于 high，即直到我们的搜索范围小于零。
3.  如果两个数组的中间元素，即(低+高)/2 相似，则将搜索更新到搜索范围的后一半，即*低=中+ 1*
4.  否则将搜索更新到搜索范围的前半部分，即*高=中–1*，并将答案更新到当前索引，ans *=中*
5.  打印索引。

**实施:**

## C++

```
// C++ program to find an extra
// element present in arr1[]
#include <iostream>
using namespace std;

// Returns index of extra element
// in arr1[]. n is size of arr2[].
// Size of arr1[] is n-1.
int findExtra(int arr1[],
              int arr2[], int n)
{
    // Initialize result
    int index = n;

    // left and right are end
    // points denoting the current range.
    int left = 0, right = n - 1;
    while (left <= right)
    {
        int mid = (left + right) / 2;

        // If middle element is same
        // of both arrays, it means
        // that extra element is after
        // mid so we update left to mid+1
        if (arr2[mid] == arr1[mid])
            left = mid + 1;

        // If middle element is different
        // of the arrays, it means that
        // the index we are searching for
        // is either mid, or before mid.
        // Hence we update right to mid-1.
        else
        {
            index = mid;
            right = mid - 1;
        }
    }

    // when right is greater than
    // left our search is complete.
    return index;
}

// Driver code
int main()
{
    int arr1[] = {2, 4, 6, 8, 10, 12, 13};
    int arr2[] = {2, 4, 6, 8, 10, 12};
    int n = sizeof(arr2) / sizeof(arr2[0]);

    // Solve is passed both arrays
    cout << findExtra(arr1, arr2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an extra
// element present in arr1[]
class GFG
{
    // Returns index of extra element
    // in arr1[]. n is size of arr2[].
    // Size of arr1[] is n-1.
    static int findExtra(int arr1[],
                         int arr2[], int n)
    {
        // Initialize result
        int index = n;

        // left and right are end
        // points denoting the current range.
        int left = 0, right = n - 1;
        while (left <= right)
        {
            int mid = (left+right) / 2;

            // If middle element is same
            // of both arrays, it means
            // that extra element is after
            // mid so we update left to mid+1
            if (arr2[mid] == arr1[mid])
                left = mid + 1;

            // If middle element is different
            // of the arrays, it means that
            // the index we are searching for
            // is either mid, or before mid.
            // Hence we update right to mid-1.
            else
            {
                index = mid;
                right = mid - 1;
            }
        }

        // when right is greater than
        // left, our search is complete.
        return index;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr1[] = {2, 4, 6, 8, 10, 12,13};
        int arr2[] = {2, 4, 6, 8, 10, 12};
        int n = arr2.length;

        // Solve is passed both arrays
        System.out.println(findExtra(arr1, arr2, n));
    }
}

// This code is contributed by Harsh Agarwal
```

## 蟒蛇 3

```
# Python3 program to find an extra
# element present in arr1[]

# Returns index of extra element
# in arr1[]. n is size of arr2[].
# Size of arr1[] is n-1.
def findExtra(arr1, arr2, n) :

    index = n # Initialize result

    # left and right are end points
    # denoting the current range.
    left = 0
    right = n - 1
    while (left <= right) :
        mid = (int)((left + right) / 2)

        # If middle element is same
        # of both arrays, it means
        # that extra element is after
        # mid so we update left to
        # mid + 1
        if (arr2[mid] == arr1[mid]) :
            left = mid + 1

        # If middle element is different
        # of the arrays, it means that
        # the index we are searching for
        # is either mid, or before mid.
        # Hence we update right to mid-1.
        else :
            index = mid
            right = mid - 1

    # when right is greater than left our
    # search is complete.
    return index

# Driver code
arr1 = [2, 4, 6, 8, 10, 12, 13]
arr2 = [2, 4, 6, 8, 10, 12]
n = len(arr2)

# Solve is passed both arrays
print(findExtra(arr1, arr2, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find an extra
// element present in arr1[]
using System;

class GFG {

    // Returns index of extra
    // element in arr1[]. n is
    // size of arr2[].
    // Size of arr1[] is
    // n - 1.
    static int findExtra(int []arr1,
                         int []arr2,
                         int n)
    {

        // Initialize result
        int index = n;

        // left and right are
        // end points denoting
        // the current range.
        int left = 0, right = n - 1;
        while (left <= right)
        {
            int mid = (left+right) / 2;

            // If middle element is
            // same of both arrays,
            // it means that extra
            // element is after mid
            // so we update left
            // to mid + 1
            if (arr2[mid] == arr1[mid])
                left = mid + 1;

            // If middle element is
            // different of the arrays,
            // it means that the index
            // we are searching for is
            // either mid, or before mid.
            // Hence we update right to mid-1.
            else
            {
                index = mid;
                right = mid - 1;
            }
        }

        // when right is greater
        // than left our
        // search is complete.
        return index;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr1 = {2, 4, 6, 8, 10, 12,13};
        int []arr2 = {2, 4, 6, 8, 10, 12};
        int n = arr2.Length;

        // Solve is passed
        // both arrays
        Console.Write(findExtra(arr1, arr2, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an extra
// element present in arr1[]

// Returns index of extra element
// in arr1[]. n is size of arr2[].
// Size of arr1[] is n-1.
function findExtra($arr1, $arr2, $n)
{
    // Initialize result
    $index = $n;

    // left and right are
    // end points denoting
    // the current range.
    $left = 0; $right = $n - 1;
    while ($left <= $right)
    {
        $mid = ($left+$right) / 2;

        // If middle element is same
        // of both arrays, it means
        // that extra element is after
        // mid so we update left to mid+1
        if ($arr2[$mid] == $arr1[$mid])
            $left = $mid + 1;

        // If middle element is different
        // of the arrays, it means that the
        // index we are searching for is either
        // mid, or before mid. Hence we update
        // right to mid-1.
        else
        {
            $index = $mid;
            $right = $mid - 1;
        }
    }

    // when right is greater than
    // left, our search is complete.
    return $index;
}

// Driver code
{
    $arr1 = array(2, 4, 6, 8,
                  10, 12, 13);
    $arr2 = array(2, 4, 6,
                  8, 10, 12);
    $n = sizeof($arr2) / sizeof($arr2[0]);

    // Solve is passed both arrays
    echo findExtra($arr1, $arr2, $n);
    return 0;
}

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to find an extra
// element present in arr1[]

// Returns index of extra element
// in arr1[]. n is size of arr2[].
// Size of arr1[] is n-1.
function findExtra( arr1, arr2, n)
{
    // Initialize result
    let index = n;

    // left and right are end
    // points denoting the current range.
    let left = 0, right = n - 1;
    while (left <= right)
    {
        let mid = Math.floor((left + right) / 2);

        // If middle element is same
        // of both arrays, it means
        // that extra element is after
        // mid so we update left to mid+1
        if (arr2[mid] == arr1[mid])
            left = mid + 1;

        // If middle element is different
        // of the arrays, it means that
        // the index we are searching for
        // is either mid, or before mid.
        // Hence we update right to mid-1.
        else
        {
            index = mid;
            right = mid - 1;
        }
    }

    // when right is greater than
    // left our search is complete.
    return index;
}

    // Driver program

    let arr1 = [2, 4, 6, 8, 10, 12, 13];
    let arr2 = [2, 4, 6, 8, 10, 12];
    let n = arr2.length;

    // Solve is passed both arrays
    document.write(findExtra(arr1, arr2, n));

</script>
```

**输出:**

```
 6
```

**复杂度分析:**

*   **时间复杂度:** O(log n)。
    二分搜索法的时间复杂度为 O(对数 n)
*   **空间复杂度:** O(1)。
    由于不需要额外的空间，所以时间复杂度是恒定的。

**<u>方法 3:</u>** 该方法使用预定义函数解决给定问题。

**逼近:**求不同的元素，求每个数组的和，相减和，求绝对值。搜索较大的数组，检查绝对值是否等于某个索引，并返回该索引。如果一个元素缺失，而所有其他元素都相同，那么总和的差将等于缺失的元素。

**算法:**

1.  创建一个函数来计算两个数组的和。
2.  求两个数组之和的绝对差(*值*)。
3.  从头到尾遍历较大的数组
4.  如果任何索引处的元素等于值，则打印索引并中断循环。

**实施:**

## C++

```
// C++ code for above approach
#include<bits/stdc++.h>
using namespace std;

// function return sum of array elements
int sum(int arr[], int n)
{
    int summ = 0;
    for (int i = 0; i < n; i++)
    {
        summ += arr[i];
    }
    return summ;
}

// function return index of given element
int indexOf(int arr[], int element, int n)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == element)
        {
            return i;
        }
    }
    return -1;
}

// Function to find Index
int find_extra_element_index(int arrA[],
                             int arrB[],
                             int n, int m)
{

    // Calculating extra element
    int extra_element = sum(arrA, n) -
                        sum(arrB, m);

    // returns index of extra element
    return indexOf(arrA, extra_element, n);
}

// Driver Code
int main()
{
    int arrA[] = {2, 4, 6, 8, 10, 12, 13};
    int arrB[] = {2, 4, 6, 8, 10, 12};
    int n = sizeof(arrA) / sizeof(arrA[0]);
    int m = sizeof(arrB) / sizeof(arrB[0]);
    cout << find_extra_element_index(arrA, arrB, n, m);
}

// This code is contributed by mohit kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
class GFG
{

    // Function to find Index
    static int find_extra_element_index(int[] arrA,
                                        int[] arrB)
    {

        // Calculating extra element
        int extra_element = sum(arrA) - sum(arrB);

        // returns index of extra element
        return indexOf(arrA, extra_element);
    }

    // function return sum of array elements
    static int sum(int[] arr)
    {
        int sum = 0;
        for (int i = 0; i < arr.length; i++)
        {
            sum += arr[i];
        }
        return sum;
    }

    // function return index of given element
    static int indexOf(int[] arr, int element)
    {
        for (int i = 0; i < arr.length; i++)
        {
            if (arr[i] == element)
            {
                return i;
            }
        }
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arrA = {2, 4, 6, 8, 10, 12, 13};
        int[] arrB = {2, 4, 6, 8, 10, 12};
        System.out.println(find_extra_element_index(arrA, arrB));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 code for above approach

# Function to find Index
def find_extra_element_index(arrA, arrB):

    # Calculating extra element
    extra_element = sum(arrA) - sum(arrB)

    # returns index of extra element
    return arrA.index(extra_element)

# Driver Code
arrA = [2, 4, 6, 8, 10, 12, 13]
arrB = [2, 4, 6, 8, 10, 12]
print(find_extra_element_index(arrA,arrB))

# This code is contributed by Dravid
```

## C#

```
// C# code for above approach
using System;

class GFG
{

    // Function to find Index
    static int find_extra_element_index(int[] arrA,
                                        int[] arrB)
    {

        // Calculating extra element
        int extra_element = sum(arrA) - sum(arrB);

        // returns index of extra element
        return indexOf(arrA, extra_element);
    }

    // function return sum of array elements
    static int sum(int[] arr)
    {
        int sum = 0;
        for (int i = 0; i < arr.Length; i++)
        {
            sum += arr[i];
        }
        return sum;
    }

    // function return index of given element
    static int indexOf(int[] arr, int element)
    {
        for (int i = 0; i < arr.Length; i++)
        {
            if (arr[i] == element)
            {
                return i;
            }
        }
        return -1;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arrA = {2, 4, 6, 8, 10, 12, 13};
        int[] arrB = {2, 4, 6, 8, 10, 12};
        Console.WriteLine(find_extra_element_index(arrA, arrB));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript code for above approach

    // Function to find Index
    function find_extra_element_index(arrA, arrB)
    {

        // Calculating extra element
        let extra_element = sum(arrA) - sum(arrB);

        // returns index of extra element
        return indexOf(arrA, extra_element);
    }

    // function return sum of array elements
    function sum(arr)
    {
        let sum = 0;
        for (let i = 0; i < arr.length; i++)
        {
            sum += arr[i];
        }
        return sum;
    }

    // function return index of given element
    function indexOf(arr, element)
    {
        for (let i = 0; i < arr.length; i++)
        {
            if (arr[i] == element)
            {
                return i;
            }
        }
        return -1;
    }

    let arrA = [2, 4, 6, 8, 10, 12, 13];
    let arrB = [2, 4, 6, 8, 10, 12];
    document.write(find_extra_element_index(arrA, arrB));

</script>
```

**输出:**

```
 6
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    由于只需要三次遍历数组，所以时间复杂度是线性的。
*   **空间复杂度:** O(1)。
    由于不需要额外的空间，所以时间复杂度是恒定的。

本文由 **Abhishek Khatri** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。