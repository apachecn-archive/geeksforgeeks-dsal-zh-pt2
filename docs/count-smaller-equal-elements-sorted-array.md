# 排序数组中较小或相等元素的计数

> 原文:[https://www . geesforgeks . org/count-small-equal-elements-sorted-array/](https://www.geeksforgeeks.org/count-smaller-equal-elements-sorted-array/)

给定一个大小为 n 的排序数组。找出小于或等于给定元素的元素数。
**例:**

```
Input : arr[] = {1, 2, 4, 5, 8, 10}
        key = 9
Output : 5
Elements less than or equal to 9 are 1, 2, 
4, 5, 8 therefore result will be 5.

Input : arr[] = {1, 2, 2, 2, 5, 7, 9}
        key = 2
Output : 4
Elements less than or equal to 2 are 1, 2, 
2, 2 therefore result will be 4\. 
```

**天真方法:**线性搜索整个数组，统计小于等于键的元素。
**高效的方法:**由于整个数组是有序的，我们可以使用二分搜索法来查找结果。
情况 1:当数组中存在键时，键的最后一个位置就是结果。
情况 2:当数组中没有 key 时，如果 key 大于 mid，我们忽略左半部分。如果 key 小于 mid，我们忽略右半部分。我们总是在中间元素之前出现一个键。

## C++

```
// C++ program to count smaller or equal
// elements in sorted array.
#include <bits/stdc++.h>
using namespace std;

// A binary search function. It returns
// number of elements less than of equal
// to given key
int binarySearchCount(int arr[], int n, int key)
{
    int left = 0, right = n;

    int mid;
    while (left < right) {
        mid = (right + left) >> 1;

        // Check if key is present in array
        if (arr[mid] == key) {

            // If duplicates are present it returns
            // the position of last element
            while (mid + 1 < n && arr[mid + 1] == key)
                mid++;
            break;
        }

        // If key is smaller, ignore right half
        else if (arr[mid] > key)
            right = mid;

        // If key is greater, ignore left half
        else
            left = mid + 1;
    }

    // If key is not found
    // in array then it will be
    // before mid
    while (mid > -1 && arr[mid] > key)
        mid--;

    // Return mid + 1 because of 0-based indexing
    // of array
    return mid + 1;
}

// Driver program to test binarySearchCount()
int main()
{
    int arr[] = { 1, 2, 4, 5, 8, 10 };
    int key = 11;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << binarySearchCount(arr, n, key);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count smaller or equal
// elements in sorted array.

class GFG {

  // A binary search function. It returns
  // number of elements less than of equal
  // to given key
  static int binarySearchCount(int arr[], int n, int key)
  {
    int left = 0, right = n;

    int mid = 0;
    while (left < right) {
      mid = (right + left) >> 1;

      // Check if key is present in array
      if (arr[mid] == key) {

        // If duplicates are present it returns
        // the position of last element
        while (mid + 1 < n && arr[mid + 1] == key)
          mid++;
        break;
      }

      // If key is smaller, ignore right half
      else if (arr[mid] > key)
        right = mid;

      // If key is greater, ignore left half
      else
        left = mid + 1;
    }

    // If key is not found in array then it will be
    // before mid
    while (mid > -1 && arr[mid] > key)
      mid--;

    // Return mid + 1 because of 0-based indexing
    // of array
    return mid + 1;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 1, 2, 4, 5, 8, 10 };
    int key = 11;
    int n = arr.length;
    System.out.print(binarySearchCount(arr, n, key));
  }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to
# count smaller or equal
# elements in sorted array.

# A binary search function.
# It returns
# number of elements
# less than of equal
# to given key
def binarySearchCount(arr, n, key):

    left = 0
    right = n

    mid = 0
    while (left < right):

        mid = (right + left)//2

        # Check if key is present in array
        if (arr[mid] == key):

            # If duplicates are
            # present it returns
            # the position of last element
            while (mid + 1<n and arr[mid + 1] == key):
                 mid+= 1
            break

        # If key is smaller,
        # ignore right half
        elif (arr[mid] > key):
            right = mid

        # If key is greater,
        # ignore left half
        else:
            left = mid + 1

    # If key is not found in
    # array then it will be
    # before mid
    while (mid > -1 and  arr[mid] > key):
        mid-= 1

    # Return mid + 1 because
    # of 0-based indexing
    # of array
    return mid + 1

# Driver code

arr = [1, 2, 4, 5, 8, 10]
key = 11
n = len(arr)

print(binarySearchCount(arr, n, key))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count smaller or
// equal elements in sorted array.
using System;

class GFG {

    // A binary search function.
    // It returns number of elements
    // less than of equal to given key
    static int binarySearchCount(int[] arr,
                                 int n, int key)
    {
        int left = 0;
        int right = n;

        int mid = 0;
        while (left < right) {
            mid = (right + left) / 2;

            // Check if key is
            // present in array
            if (arr[mid] == key) {

                // If duplicates are present
                // it returns the position
                // of last element
                while (mid + 1 < n && arr[mid + 1] == key)
                    mid++;
                break;
            }

            // If key is smaller,
            // ignore right half
            else if (arr[mid] > key)
                right = mid;

            // If key is greater,
            // ignore left half
            else
                left = mid + 1;
        }

        // If key is not found in array
        // then it will be before mid
        while (mid > -1 && arr[mid] > key)
            mid--;

        // Return mid + 1 because of
        // 0-based indexing of array
        return mid + 1;
    }

    // Driver code
    static public void Main()
    {
        int[] arr = { 1, 2, 4, 5, 8, 10 };
        int key = 11;
        int n = arr.Length;
        Console.Write(binarySearchCount(arr, n, key));
    }
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// smaller or equal
// elements in sorted array.

// A binary search function.
// It returns number of
// elements less than of
// equal to given key
function binarySearchCount($arr, $n, $key)
{
    $left = 0;
    $right = $n;
    $mid;
    while ($left < $right)
    {
        $mid = ($right + $left) / 2;

        // Check if key is
        // present in array
        if ($arr[$mid] == $key)
        {
            // If duplicates are
            // present it returns
            // the position of
            // last element
            while ($mid + 1 < $n && $arr[$mid + 1] == $key)
                $mid++;
            break;
        }

        // If key is smaller,
        // ignore right half
        else if ($mid > -1 && $arr[$mid] > $key)
            $right = $mid;

        // If key is greater,
        // ignore left half
        else
            $left = $mid + 1;
    }

    // If key is not found in
    // array then it will be
    // before mid
    while ($arr[$mid] > $key)
        $mid--;

    // Return mid + 1 because
    // of 0-based indexing
    // of array
    return $mid + 1;
}

// Driver Code
$arr = array (1, 2, 4,
              5, 8, 10);
$key = 11;
$n = sizeof($arr) ;
echo binarySearchCount($arr, $n, $key);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to
    // count smaller or equal
    // elements in sorted array.

    // A binary search function. It returns
    // number of elements less than of equal
    // to given key
    function binarySearchCount(arr, n, key)
    {
        let left = 0, right = n;

        let mid;
        while (left < right) {
            mid = (right + left) >> 1;

            // Check if key is present in array
            if (arr[mid] == key) {

                // If duplicates are
                // present it returns
                // the position of last element
                while ((mid + 1) < n &&
                       arr[mid + 1] == key)
                    mid++;
                break;
            }

            // If key is smaller, ignore right half
            else if (arr[mid] > key)
                right = mid;

            // If key is greater, ignore left half
            else
                left = mid + 1;
        }

        // If key is not found
        // in array then it will be
        // before mid
        while (mid > -1 && arr[mid] > key)
            mid--;

        // Return mid + 1 because of 0-based indexing
        // of array
        return mid + 1;
    }

    let arr = [ 1, 2, 4, 5, 8, 10 ];
    let key = 11;
    let n = arr.length;
    document.write(binarySearchCount(arr, n, key));

</script>
```

**Output**

```
6
```

尽管这种解决方案的平均性能更好，但这种解决方案的最坏情况时间复杂度仍然是 O(n)。
上述程序可以使用更简化的二分搜索法实现。想法是检查中间元素是否大于给定元素，然后将**右侧**索引更新为**中间–1**但是如果中间元素小于或等于关键更新**则回答**为**中间+ 1** ，将**左侧**索引更新为**中间+ 1** 。

下面是上述方法的实现:

## C++

```
// C++ program to count smaller or equal
// elements in sorted array
#include <bits/stdc++.h>
using namespace std;

// A binary search function to return
// the number of elements less than
// or equal to the given key
int binarySearchCount(int arr[], int n, int key)
{
    int left = 0;
    int right = n - 1;

    int count = 0;

    while (left <= right) {
        int mid = (right + left) / 2;

        // Check if middle element is
        // less than or equal to key
        if (arr[mid] <= key) {

            // At least (mid + 1) elements are there
            // whose values are less than
            // or equal to key
            count = mid + 1;
            left = mid + 1;
        }

        // If key is smaller, ignore right half
        else
            right = mid - 1;
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 11, 11, 16 };
    int key = 11;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << binarySearchCount(arr, n, key);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count smaller or equal
import java.io.*;

class GFG
{

// A binary search function to return
// the number of elements less than
// or equal to the given key
static int binarySearchCount(int arr[],
                             int n, int key)
{
    int left = 0;
    int right = n - 1;

    int count = 0;

    while (left <= right)
    {
        int mid = (right + left) / 2;

        // Check if middle element is
        // less than or equal to key
        if (arr[mid] <= key)
        {

            // At least (mid + 1) elements are there
            // whose values are less than
            // or equal to key
            count = mid + 1;
            left = mid + 1;
        }

        // If key is smaller, ignore right half
        else
            right = mid - 1;
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 4, 11, 11, 16 };
    int key = 11;
    int n = arr.length;

    System.out.println (binarySearchCount(arr, n, key));
}
}

// The code is contributed by Sachin.
```

## 蟒蛇 3

```
# Python3 program to count smaller or equal
# elements in sorted array

# A binary search function to return
# the number of elements less than
# or equal to the given key
def binarySearchCount(arr, n, key):

    left = 0
    right = n - 1

    count = 0

    while (left <= right):
        mid = int((right + left) / 2)

        # Check if middle element is
        # less than or equal to key
        if (arr[mid] <= key):

            # At least (mid + 1) elements are there
            # whose values are less than
            # or equal to key
            count = mid + 1
            left = mid + 1

        # If key is smaller, ignore right half
        else:
            right = mid - 1

    return count

# Driver code
arr = [ 1, 2, 4, 11, 11, 16 ]
key = 11
n = len(arr)

print( binarySearchCount(arr, n, key))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to count smaller or equal
using System;

class GFG
{

// A binary search function to return
// the number of elements less than
// or equal to the given key
static int binarySearchCount(int []arr,
                             int n, int key)
{
    int left = 0;
    int right = n - 1;

    int count = 0;

    while (left <= right)
    {
        int mid = (right + left) / 2;

        // Check if middle element is
        // less than or equal to key
        if (arr[mid] <= key)
        {

            // At least (mid + 1) elements are there
            // whose values are less than
            // or equal to key
            count = mid + 1;
            left = mid + 1;
        }

        // If key is smaller,
        // ignore right half
        else
            right = mid - 1;
    }
    return count;
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 1, 2, 4, 11, 11, 16 };
    int key = 11;
    int n = arr.Length;

    Console.WriteLine(binarySearchCount(arr, n, key));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to count smaller or equal
    // elements in sorted array

    // A binary search function to return
    // the number of elements less than
    // or equal to the given key
    function binarySearchCount(arr, n, key)
    {
        let left = 0;
        let right = n - 1;

        let count = 0;

        while (left <= right) {
            let mid = parseInt((right + left) / 2, 10);

            // Check if middle element is
            // less than or equal to key
            if (arr[mid] <= key) {

                // At least (mid + 1) elements are there
                // whose values are less than
                // or equal to key
                count = mid + 1;
                left = mid + 1;
            }

            // If key is smaller, ignore right half
            else
                right = mid - 1;
        }

        return count;
    }

    let arr = [ 1, 2, 4, 11, 11, 16 ];
    let key = 11;
    let n = arr.length;

    document.write(binarySearchCount(arr, n, key));

    // This code is contributed by rameshtravel07.
</script>
```

**Output**

```
5
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。