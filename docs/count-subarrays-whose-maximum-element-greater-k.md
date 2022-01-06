# 最大元素大于 k 的子阵计数

> 原文:[https://www . geeksforgeeks . org/count-subarrays-what-maximum-element-greater-k/](https://www.geeksforgeeks.org/count-subarrays-whose-maximum-element-greater-k/)

给定一个由 **n** 个元素和一个整数 **k** 组成的数组。任务是找出最大元素大于 k 的子阵的个数
**例:**

```
Input : arr[] = {1, 2, 3} and k = 2.
Output : 3
All the possible subarrays of arr[] are 
{ 1 }, { 2 }, { 3 }, { 1, 2 }, { 2, 3 }, 
{ 1, 2, 3 }.
Their maximum elements are 1, 2, 3, 2, 3, 3.
There are only 3 maximum elements > 2.
```

其思想是通过计数最大元素小于或等于 k 的子阵列来处理问题，因为计数这样的子阵列更容易。求最大元素小于或等于 K 的子阵个数，去掉所有大于 K 的元素，求剩下元素的子阵个数。
一旦我们找到上面的计数，我们就可以从 n*(n+1)/2 中减去它，得到我们需要的结果。观察一下，n * n+1/2 个大小为 n 的任意数组都可能有 n 个子数组，所以，找到最大元素小于或等于 K 的子数组的个数，并从 n*(n+1)/2 中减去它，就得到答案。
以下是本办法的实施:

## C++

```
// C++ program to count number of subarrays
// whose maximum element is greater than K.
#include <bits/stdc++.h>
using namespace std;

// Return number of subarrays whose maximum
// element is less than or equal to K.
int countSubarray(int arr[], int n, int k)
{
    // To store count of subarrays with all
    // elements less than or equal to k.
    int s = 0;

    // Traversing the array.
    int i = 0;
    while (i < n) {
        // If element is greater than k, ignore.
        if (arr[i] > k) {
            i++;
            continue;
        }

        // Counting the subarray length whose
        // each element is less than equal to k.
        int count = 0;
        while (i < n && arr[i] <= k) {
            i++;
            count++;
        }

        // Suming number of subarray whose
        // maximum element is less than equal to k.
        s += ((count * (count + 1)) / 2);
    }

    return (n * (n + 1) / 2 - s);
}

// Driven Program
int main()
{
    int arr[] = { 1, 2, 3 };
    int k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countSubarray(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of subarrays
// whose maximum element is greater than K.
import java.util.*;

class GFG {

    // Return number of subarrays whose maximum
    // element is less than or equal to K.
    static int countSubarray(int arr[], int n, int k)
    {

        // To store count of subarrays with all
        // elements less than or equal to k.
        int s = 0;

        // Traversing the array.
        int i = 0;
        while (i < n) {

            // If element is greater than k, ignore.
            if (arr[i] > k) {
                i++;
                continue;
            }

            // Counting the subarray length whose
            // each element is less than equal to k.
            int count = 0;
            while (i < n && arr[i] <= k) {
                i++;
                count++;
            }

            // Suming number of subarray whose
            // maximum element is less than equal to k.
            s += ((count * (count + 1)) / 2);
        }

        return (n * (n + 1) / 2 - s);
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 1, 2, 3 };
        int k = 2;
        int n = arr.length;
        System.out.print(countSubarray(arr, n, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count
# number of subarrays
# whose maximum element
# is greater than K.

# Return number of
# subarrays whose maximum
# element is less than or equal to K.
def countSubarray(arr, n, k):

    # To store count of
    # subarrays with all
    # elements less than
    # or equal to k.
    s = 0

    # Traversing the array.
    i = 0
    while (i < n):

        # If element is greater
        # than k, ignore.
        if (arr[i] > k):

            i = i + 1
            continue

        # Counting the subarray
        # length whose
        # each element is less
        # than equal to k.
        count = 0
        while (i < n and arr[i] <= k):

            i = i + 1
            count = count + 1

        # Suming number of subarray whose
        # maximum element is less
        # than equal to k.
        s = s + ((count*(count + 1))//2)

    return (n*(n + 1)//2 - s)

# Driver code

arr = [1, 2, 3]
k = 2
n = len(arr)

print(countSubarray(arr, n, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count number of subarrays
// whose maximum element is greater than K.
using System;

class GFG {

    // Return number of subarrays whose maximum
    // element is less than or equal to K.
    static int countSubarray(int[] arr, int n, int k)
    {
        // To store count of subarrays with all
        // elements less than or equal to k.
        int s = 0;

        // Traversing the array.
        int i = 0;
        while (i < n) {

            // If element is greater than k, ignore.
            if (arr[i] > k) {
                i++;
                continue;
            }

            // Counting the subarray length whose
            // each element is less than equal to k.
            int count = 0;
            while (i < n && arr[i] <= k) {
                i++;
                count++;
            }

            // Suming number of subarray whose
            // maximum element is less than equal to k.
            s += ((count * (count + 1)) / 2);
        }

        return (n * (n + 1) / 2 - s);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = {1, 2, 3};
        int k = 2;
        int n = arr.Length;
        Console.WriteLine(countSubarray(arr, n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of subarrays
// whose maximum element is greater than K.

// Return number of subarrays whose maximum
// element is less than or equal to K.
function countSubarray( $arr, $n, $k)
{

    // To store count of subarrays with all
    // elements less than or equal to k.
    $s = 0;

    // Traversing the array.
    $i = 0;
    while ($i < $n) {

        // If element is greater than k,
        // ignore.
        if ($arr[$i] > $k) {
            $i++;
            continue;
        }

        // Counting the subarray length
        // whose each element is less
        // than equal to k.
        $count = 0;
        while ($i < $n and $arr[$i] <= $k) {
            $i++;
            $count++;
        }

        // Suming number of subarray whose
        // maximum element is less than
        // equal to k.
        $s += (($count * ($count + 1)) / 2);
    }

    return ($n * ($n + 1) / 2 - $s);
}

// Driven Program
    $arr = array( 1, 2, 3 );
    $k = 2;
    $n = count($arr);
    echo countSubarray($arr, $n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to count number of subarrays
    // whose maximum element is greater than K.

    // Return number of subarrays whose maximum
    // element is less than or equal to K.
    function countSubarray(arr, n, k)
    {
        // To store count of subarrays with all
        // elements less than or equal to k.
        let s = 0;

        // Traversing the array.
        let i = 0;
        while (i < n) {

            // If element is greater than k, ignore.
            if (arr[i] > k) {
                i++;
                continue;
            }

            // Counting the subarray length whose
            // each element is less than equal to k.
            let count = 0;
            while (i < n && arr[i] <= k) {
                i++;
                count++;
            }

            // Suming number of subarray whose
            // maximum element is less than equal to k.
            s += parseInt((count * (count + 1)) / 2, 10);
        }

        return (n * parseInt((n + 1) / 2, 10) - s);
    }

    let arr = [1, 2, 3];
    let k = 2;
    let n = arr.length;
    document.write(countSubarray(arr, n, k));

</script>
```

输出:

```
3
```

**时间复杂度:** O(n)。
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。