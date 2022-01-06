# 在 0 和 1 的排序数组中找到第一个 1 的索引

> 原文:[https://www . geesforgeks . org/find-index-first-1-sorted-array-0s-1s/](https://www.geeksforgeeks.org/find-index-first-1-sorted-array-0s-1s/)

给定一个由 0 和 1 组成的排序数组。问题是找到排序数组中第一个“1”的索引。数组可能只包含 0 或 1。如果数组中没有 1，则打印“-1”。
示例:

```
Input : arr[] = {0, 0, 0, 0, 0, 0, 1, 1, 1, 1}
Output : 6
The index of first 1 in the array is 6.

Input : arr[] = {0, 0, 0, 0}
Output : -1
1's are not present in the array.
```

**来源:**亚马逊采访
提问

**天真方法:**从左到右遍历数组，返回第一个“1”的索引。如果数组中没有 1，则打印“-1”。

## C++

```
// C++ implementation to find the index of
// first '1' in a sorted array of 0's and 1's
#include <bits/stdc++.h>
using namespace std;

// function to find the index of first '1'
int indexOfFirstOne(int arr[], int n)
{
    // traverse the array from left to right
    for (int i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above
int main()
{
    int arr[] = { 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << indexOfFirstOne(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the index of
// first '1' in a sorted array of 0's and 1's
class GFG {

    // function to find the index of first '1'
    public static int indexOfFirstOne(int arr[], int n)
    {
        // traverse the array from left to right
        for (int i = 0; i < n; i++)

            // if true, then return i
            if (arr[i] == 1)
                return i;

        // 1's are not present in the array
        return -1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 };
        int n = arr.length;
        System.out.println(indexOfFirstOne(arr, n));

    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 implementation to find
# the index of first '1' in a
# sorted array of 0's and 1's

# function to find the index of first '1'
def indexOfFirstOne(arr, n):

    # traverse the array from left to right
    for i in range(0, n):

        # if true, then return i
        if (arr[i] == 1):
            return i

    # 1's are not present in the array
    return -1

# Driver program to test above
arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ]
n = len(arr)
ans = indexOfFirstOne(arr, n)
print(ans)

# This code is contributed by saloni1297
```

## C#

```
// C# program to find the index of
// first '1' in a sorted array
// of 0's and 1's
using System;

class GFG
{
    // function to find the index of first '1'
    public static int indexOfFirstOne(int []arr, int n)
    {
        // traverse the array from left to right
        for (int i = 0; i < n; i++)

            // if true, then return i
            if (arr[i] == 1)
                return i;

        // 1's are not present in the array
        return -1;
    }

    // Driver program
    public static void Main()
    {
        int []arr = { 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 };
        int n = arr.Length;
        Console.Write(indexOfFirstOne(arr, n));

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the index of
// first '1' in a sorted array of 0's and 1's
// function to find the index of first '1'

function indexOfFirstOne($arr, $n)
{

    // traverse the array from
    // left to right
    for ($i = 0; $i < $n; $i++)

        // if true, then return i
        if ($arr[$i] == 1)
            return $i;

    // 1's are not present
    // in the array
    return -1;
}

    // Driver Code
    $arr = array(0, 0, 0, 0, 0, 0, 1, 1, 1, 1);
    $n = sizeof($arr) / sizeof($arr[0]);
    echo indexOfFirstOne($arr, $n);
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
<script>

// Javascript implementation to find the index of
// first '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
function indexOfFirstOne(arr, n)
{
    // traverse the array from left to right
    for (let i = 0; i < n; i++)

        // if true, then return i
        if (arr[i] == 1)
            return i;

    // 1's are not present in the array
    return -1;
}

// Driver program to test above

    let arr = [ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ];
    let n = arr.length;
    document.write(indexOfFirstOne(arr, n));

//This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
6
```

时间复杂度:O(n)
**高效方法(二分搜索法):**在排序后的数组上使用二分搜索法的技巧，从而找到第一个‘1’的索引。

## C++

```
// C++ implementation to find the index of first
// '1' in a sorted array of 0's and 1's
#include <bits/stdc++.h>
using namespace std;

// function to find the index of first '1'
// binary search technique is applied
int indexOfFirstOne(int arr[], int low, int high)
{
    while (low <= high) {
        int mid = (low + high) / 2;

        // if true, then 'mid' is the index of first '1'
        if (arr[mid] == 1 && (mid == 0 || arr[mid - 1] == 0))
            return mid;

        // first '1' lies to the left of 'mid'
        else if (arr[mid] == 1)
            high = mid - 1;

        // first '1' lies to the right of 'mid'
        else
            low = mid + 1;
    }

    // 1's are not present in the array
    return -1;
}

// Driver program to test above
int main()
{
    int arr[] = { 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << indexOfFirstOne(arr, 0, n - 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the index of
// first '1' in a sorted array of 0's and 1's
class GFG {

    // function to find the index of first '1'
    // binary search technique is applied
    public static int indexOfFirstOne(int arr[], int low,
                                                int high)
    {
        while (low <= high) {
            int mid = (low + high) / 2;

            // if true, then 'mid' is the index of first '1'
            if (arr[mid] == 1 && (mid == 0 || arr[mid - 1]
                                                    == 0))
                return mid;

            // first '1' lies to the left of 'mid'
            else if (arr[mid] == 1)
                high = mid - 1;

            // first '1' lies to the right of 'mid'
            else
                low = mid + 1;
        }

        // 1's are not present in the array
        return -1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 };
        int n = arr.length;
        System.out.println(indexOfFirstOne(arr, 0,
                                              n - 1));

    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 implementation to find
# the index of first '1' in a
# sorted array of 0's and 1's

# function to find the index of first '1'
# binary search technique is applied
def indexOfFirstOne( arr, low, high):

    while (low <= high):

        mid = int((low + high) / 2)

        # if true, then 'mid' is the index of first '1'
        if (arr[mid] == 1 and (mid == 0 or arr[mid - 1] == 0)):
            return mid

        # first '1' lies to the left of 'mid'
        elif (arr[mid] == 1):
            high = mid - 1

        # first '1' lies to the right of 'mid'
        else:
            low = mid + 1

    # 1's are not present in the array
    return -1;

# Driver program to test above
arr = [0, 0, 0, 0, 0, 0, 1, 1, 1, 1 ]
n = len(arr)
ans = indexOfFirstOne(arr, 0, n - 1)
print (ans)

# This code is contributed by saloni1297
```

## C#

```
// C# program to find the index of
// first '1' in a sorted array of 0's and 1's
using System;

class GFG
{
    // function to find the index of first '1'
    // binary search technique is applied
    public static int indexOfFirstOne(int []arr, int low,
                                                int high)
    {
        while (low <= high) {
            int mid = (low + high) / 2;

            // if true, then 'mid' is the index of first '1'
            if (arr[mid] == 1 && (mid == 0 || arr[mid - 1]
                                                    == 0))
                return mid;

            // first '1' lies to the left of 'mid'
            else if (arr[mid] == 1)
                high = mid - 1;

            // first '1' lies to the right of 'mid'
            else
                low = mid + 1;
        }

        // 1's are not present in the array
        return -1;
    }

    // Driver program
    public static void Main()
    {
        int []arr = { 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 };
        int n = arr.Length;
        Console.Write(indexOfFirstOne(arr, 0, n - 1));

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the index of first '1' in
// a sorted array of 0's and 1's

// function to find the index
// of first '1' binary search
// technique is applied
function indexOfFirstOne($arr,
                         $low,
                         $high)
{
    while ($low <= $high)
    {
        $mid = ceil($low +
                    $high) / 2;

        // if true, then 'mid' is
        // the index of first '1'
        if ($arr[$mid] == 1 and
            ($mid == 0 or
              $arr[$mid - 1] == 0))
            return $mid;

        // first '1' lies to the
        // left of 'mid'
        else if ($arr[$mid] == 1)
            $high = $mid - 1;

        // first '1' lies to
        // the right of 'mid'
        else
            $low = $mid + 1;
    }

    // 1's are not present
    // in the array
    return -1;
}

// Driver Code
$arr = array(0, 0, 0, 0, 0,
             0, 1, 1, 1, 1);
$n = count($arr);
echo indexOfFirstOne($arr, 0, $n - 1);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the index of first
// '1' in a sorted array of 0's and 1's

// function to find the index of first '1'
// binary search technique is applied
function indexOfFirstOne(arr, low, high)
{
    while (low <= high) {
        var mid = parseInt((low + high) / 2);

        // if true, then 'mid' is the index of first '1'
        if (arr[mid] == 1 && (mid == 0 || arr[mid - 1] == 0))
            return mid;

        // first '1' lies to the left of 'mid'
        else if (arr[mid] == 1)
            high = mid - 1;

        // first '1' lies to the right of 'mid'
        else
            low = mid + 1;
    }

    // 1's are not present in the array
    return -1;
}

// Driver program to test above
var arr = [0, 0, 0, 0, 0, 0, 1, 1, 1, 1];
var n = arr.length;
document.write( indexOfFirstOne(arr, 0, n - 1));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
6
```

时间复杂度:O(Logn)
**参考文献:**[https://www.careercup.com/question?id=17316686](https://www.careercup.com/question?id=17316686)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。