# 两个二进制数组中的最小翻转，使得它们的异或等于另一个数组

> 原文:[https://www . geesforgeks . org/minimum-flips-two-binary-arrays-xor-equal-other-array/](https://www.geeksforgeeks.org/minimum-flips-two-binary-arrays-xor-equal-another-array/)

给定三个二进制数组，每个数组大小为 **n** ，任务是找到第一和第二数组中的最小位翻转，使得第一和第二数组的第 I 个索引位的异或等于第三数组的第 I 个索引位。给定一个限制，即我们最多只能翻转数组 1 的 p 位，最多只能翻转数组 2 的 q 位。如果不可能，输出-1。
不允许重新排列位。
**示例:**

```
Input :  p = 2, q = 2
  arr1[] = {0, 0, 1}
  arr2[] = {0, 1, 0}
  arr3[] = {0, 1, 0}
Output : 1
arr1[0] ^ arr2[0] = 0 ^ 0 = 0, which is equal 
to arr3[0], so no flip required.
arr1[1] ^ arr2[1] = 0 ^ 1 = 1, which is equal
to arr3[1], so no flip required.
arr1[2] ^ arr2[2] = 1 ^ 0 = 1, which is not 
equal to arr3[0], so one flip required.
Also p = 2 and q = 2, so flip arr1[2].

Input :  p = 2, q = 4
  arr1 = { 1, 0, 1, 1, 1, 1, 1 }
  arr2 = { 0, 1, 1, 1, 1, 0, 0 }
  arr3 = { 1, 1, 1, 1, 0, 0, 1 }
Output : 3
```

```
When the XOR of i'th bit of array1 and arry2 is
equal to i'th bit of array3, no flip is required.

Now let's observe when XOR is not equal. 
There can be following cases:
Case 1: When arr3[i] = 0, 
        then either arr1[i] = 1, arr2[i] = 0 or
                    arr1[i] = 0, arr2[i] = 1.
Case 2: When arr3[i] = 1, 
        then either arr1[i] = 1, arr2[i] = 1 or 
                    arr1[i] = 0, arr2[i] = 0.
At least one flip is required in each case. 
```

对于情况 1，XOR 应该是 0，这可以通过 0 ^ 0 或 1 ^ 1 获得，对于情况 2，1 可以通过 1 ^ 0 或 0 ^ 1 获得。
所以，观察我们可以根据 p 和 q 的值翻转 arr1[i]或 arr2[i]，
如果 p = 0，翻转 arr2 需要翻转，如果 q 也是 0，输出-1。同样，如果 p = 0，翻转 arr1 需要翻转，如果 p 也是 0，输出-1
所以，我们可以说，使 arr1 和 arr2 的异或等于 arr3 所需的翻转次数应该小于或等于 p+q。
下面是这种方法的实现:

## C++

```
// C++ program to find minimum flip required to make
// XOR of two arrays equal to another array with
// constraints on number of flip on each array.

#include <bits/stdc++.h>
using namespace std;

// Return minimum number of flip required
int minflip(int arr1[], int arr2[], int arr3[],
            int p, int q, int n)
{
    int flip = 0;

    // Counting number of mismatch, XOR of arr1[] and
    // arr2[] is not equal to arr3[].
    for (int i = 0; i < n; i++)
        if (arr1[i] ^ arr2[i] != arr3[i])
            flip++;

    // if flip is less then allowed constraint return
    // it. else return -1.
    return (flip <= p + q) ? flip : -1;
}

// Driven Program
int main()
{
    int arr1[] = { 1, 0, 1, 1, 1, 1, 1 };
    int arr2[] = { 0, 1, 1, 1, 1, 0, 0 };
    int arr3[] = { 1, 1, 1, 1, 0, 0, 1 };

    int n = sizeof(arr1) / sizeof(arr1[0]);
    int p = 2, q = 4;

    cout << minflip(arr1, arr2, arr3, p, q, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum flip required to make
// XOR of two arrays equal to another array with
// constraints on number of flip on each array.
import java.io.*;

class GFG {

    // Return minimum number of flip required
    static int minflip(int[] arr1, int[] arr2, int[] arr3,
                                      int p, int q, int n)
    {
        int flip = 0;

        // Counting number of mismatch, XOR of arr1[] and
        // arr2[] is not equal to arr3[].
        for (int i = 0; i < n; i++)
            if (arr1[i] > 0 ^ arr2[i] > 0 != arr3[i] > 0)
                flip++;

        // if flip is less then allowed constraint return
        // it. else return -1.
        return (flip <= p + q) ? flip : -1;
    }

    // Driver program
    static public void main(String[] args)
    {
        int[] arr1 = {1, 0, 1, 1, 1, 1, 1};
        int[] arr2 = {0, 1, 1, 1, 1, 0, 0};
        int[] arr3 = {1, 1, 1, 1, 0, 0, 1};

        int n = arr1.length;
        int p = 2, q = 4;

        System.out.println(minflip(arr1, arr2, arr3, p, q, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find
# minimum flip required to
# make XOR of two arrays
# equal to another array
# with constraints on number
# of flip on each array.

# Return minimum number
# of flip required
def minflip(arr1, arr2,
            arr3, p, q, n):

    flip = 0

    # Counting number of
    # mismatch, XOR of
    # arr1[] and arr2[]
    # is not equal to arr3[].
    for i in range(0 , n):
        if (arr1[i] ^
            arr2[i] != arr3[i]):
            flip += 1

    # if flip is less then
    # allowed constraint return
    # it. else return -1.
    return flip if (flip <= p + q) else -1

# Driver Code
arr1 = [1, 0, 1, 1, 1, 1, 1]
arr2 = [0, 1, 1, 1, 1, 0, 0]
arr3 = [1, 1, 1, 1, 0, 0, 1]

n = len(arr1)
p = 2
q = 4

print(minflip(arr1, arr2,
              arr3, p, q, n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find minimum flip required to make
// XOR of two arrays equal to another array with
// constraints on number of flip on each array.
using System;

class GFG {

    // Return minimum number of flip required
    static int minflip(int[] arr1, int[] arr2, int[] arr3,
                                      int p, int q, int n)
    {
        int flip = 0;

        // Counting number of mismatch, XOR of arr1[] and
        // arr2[] is not equal to arr3[].
        for (int i = 0; i < n; i++)
            if (arr1[i] > 0 ^ arr2[i] > 0 != arr3[i] > 0)
                flip++;

        // if flip is less then allowed constraint return
        // it. else return -1.
        return (flip <= p + q) ? flip : -1;
    }

    // Driver program
    static public void Main()
    {
        int[] arr1 = { 1, 0, 1, 1, 1, 1, 1 };
        int[] arr2 = { 0, 1, 1, 1, 1, 0, 0 };
        int[] arr3 = { 1, 1, 1, 1, 0, 0, 1 };

        int n = arr1.Length;
        int p = 2, q = 4;

        Console.WriteLine(minflip(arr1, arr2, arr3, p, q, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// flip required to make XOR
// of two arrays equal to another
// array with constraints on number
// of flip on each array.

// Return minimum number
// of flip required
function minflip($arr1, $arr2, $arr3,
                          $p, $q, $n)
{
    $flip = 0;

    // Counting number of mismatch,
    // XOR of arr1[] and arr2[]
    // is not equal to arr3[].
    for ($i = 0; $i < $n; $i++)
        if ($arr1[$i] ^ $arr2[$i] != $arr3[$i])
            $flip++;

    // if flip is less then
    // allowed constraint return
    // it. else return -1.
    return ($flip <= $p + $q) ? $flip : -1;
}

    // Driver code
    $arr1 = array(1, 0, 1, 1, 1, 1, 1);
    $arr2 = array(0, 1, 1, 1, 1, 0, 0);
    $arr3 = array(1, 1, 1, 1, 0, 0, 1);

    $n = count($arr1);
    $p = 2; $q = 4;

    echo minflip($arr1, $arr2, $arr3, $p, $q, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// minimum flip required to make
// XOR of two arrays equal to
// another array with
// constraints on number of
// flip on each array.

// Return minimum number
// of flip required
function minflip(arr1, arr2, arr3, p, q, n)
{
    let flip = 0;

    // Counting number of mismatch,
    // XOR of arr1[] and
    // arr2[] is not equal to arr3[].
    for (let i = 0; i < n; i++)
        if (arr1[i] ^ arr2[i] != arr3[i])
            flip++;

    // if flip is less then
    // allowed constraint return
    // it. else return -1.
    return (flip <= p + q) ? flip : -1;
}

// Driven Program
    let arr1 = [ 1, 0, 1, 1, 1, 1, 1 ];
    let arr2 = [ 0, 1, 1, 1, 1, 0, 0 ];
    let arr3 = [ 1, 1, 1, 1, 0, 0, 1 ];

    let n = arr1.length;
    let p = 2, q = 4;

    document.write(minflip(arr1, arr2, arr3, p, q, n));

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n)。
本文由 [**Anuj Chauhan**](https://web.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。