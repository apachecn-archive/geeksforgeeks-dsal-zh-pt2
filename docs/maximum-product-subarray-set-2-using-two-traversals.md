# 最大乘积子阵|集合 2(使用两个遍历)

> 原文:[https://www . geesforgeks . org/max-product-subarray-set-2-use-two-traversals/](https://www.geeksforgeeks.org/maximum-product-subarray-set-2-using-two-traversals/)

给定一个包含正整数和负整数的数组，求最大乘积子数组的乘积。预期时间复杂度为 0(n)，只能使用 0(1)个额外空间。
**例:**

```
Input: arr[] = {6, -3, -10, 0, 2}
Output:   180  // The subarray is {6, -3, -10}

Input: arr[] = {-1, -3, -10, 0, 60}
Output:   60  // The subarray is {60}

Input: arr[] = {-1, -2, -3, 4}
Output:   24  // The subarray is {-2, -3, 4}

Input: arr[] = {-10}
Output:   0  // An empty array is also subarray
             // and product of empty subarray is
             // considered as 0.
```

我们在这里讨论了这个问题的解决方案[。
这篇文章讨论了一个有趣的解决方案。这个想法是基于这样一个事实，即总最大乘积是以下两个的最大值:](https://www.geeksforgeeks.org/maximum-product-subarray/) 

1.  从左到右遍历中的最大乘积。
2.  从右向左遍历的最大乘积

例如，考虑上面的第三个样本输入{-1，-2，-3，4}。如果我们仅向前遍历数组(将-1 视为输出的一部分)，最大乘积将是 2。如果我们向后遍历数组(将 4 视为输出的一部分)，最大乘积将是 24，即；{ -2, -3, 4}.
一件重要的事情是处理 0。每当我们看到 0 时，我们需要计算新的向前(或向后)总和。
以下是上述思路的实现:

## C++

```
// C++ program to find maximum product subarray
#include<bits/stdc++.h>
using namespace std;

// Function for maximum product
int max_product(int arr[], int n)
{
    // Initialize maximum products in forward and
    // backward directions
    int max_fwd = INT_MIN, max_bkd = INT_MIN;

    // Initialize current product
    int max_till_now = 1;

    //check if zero is present in an array or not
    bool isZero=false;

    // max_fwd for maximum contiguous product in
    // forward direction
    // max_bkd for maximum contiguous product in
    // backward direction
    // iterating within forward direction in array
    for (int i=0; i<n; i++)
    {
        // if arr[i]==0, it is breaking condition
        // for contiguous subarray
        max_till_now = max_till_now*arr[i];
        if (max_till_now == 0)
        {  
             isZero=true;
             max_till_now = 1;
            continue;
        }
        if (max_fwd < max_till_now) // update max_fwd
            max_fwd = max_till_now;
    }

     max_till_now = 1;

    // iterating within backward direction in array
    for (int i=n-1; i>=0; i--)
    {
        max_till_now = max_till_now * arr[i];
        if (max_till_now == 0)
        {
            isZero=true;
            max_till_now = 1;
            continue;
        }

        // update max_bkd
        if (max_bkd < max_till_now)
            max_bkd = max_till_now;
    }

    // return max of max_fwd and max_bkd
    int res =  max(max_fwd, max_bkd);

    // Product should not be negative.
    // (Product of an empty subarray is
    // considered as 0)
    if(isZero)
    return max(res, 0);

    return res;
}

// Driver Program to test above function
int main()
{
    int arr[] = {-1, -2, -3, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << max_product(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// maximum product subarray
import java.io.*;

class GFG
{

// Function for maximum product
static int max_product(int arr[], int n)
{
    // Initialize maximum products in
    // forward and backward directions
    int max_fwd = Integer.MIN_VALUE,
        max_bkd = Integer.MIN_VALUE;

    //check if zero is present in an array or not
    boolean isZero=false;

    // Initialize current product
    int max_till_now = 1;

    // max_fwd for maximum contiguous
    // product in forward direction
    // max_bkd for maximum contiguous
    // product in backward direction
    // iterating within forward
    // direction in array
    for (int i = 0; i < n; i++)
    {
        // if arr[i]==0, it is breaking
        // condition for contiguous subarray
        max_till_now = max_till_now * arr[i];
        if (max_till_now == 0)
        {
            isZero=true;
            max_till_now = 1;
            continue;
        }

        // update max_fwd
        if (max_fwd < max_till_now)
            max_fwd = max_till_now;
    }

    max_till_now = 1;

    // iterating within backward
    // direction in array
    for (int i = n - 1; i >= 0; i--)
    {
        max_till_now = max_till_now * arr[i];
        if (max_till_now == 0)
        {
            isZero=true;
            max_till_now = 1;
            continue;
        }

        // update max_bkd
        if (max_bkd < max_till_now)
            max_bkd = max_till_now;
    }

    // return max of max_fwd and max_bkd
    int res = Math. max(max_fwd, max_bkd);

    // Product should not be negative.
    // (Product of an empty subarray is
    // considered as 0)
    if(isZero)
    return Math.max(res, 0);

    return res;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {-1, -2, -3, 4};
    int n = arr.length;
    System.out.println( max_product(arr, n) );
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find
# maximum product subarray
import sys

# Function for maximum product
def max_product(arr, n):

    # Initialize maximum products
    # in forward and backward directions
    max_fwd = -sys.maxsize - 1
    max_bkd = -sys.maxsize - 1

    #check if zero is present in an array or not
    isZero=False;

    # Initialize current product
    max_till_now = 1

    # max_fwd for maximum contiguous
    # product in forward direction
    # max_bkd for maximum contiguous
    # product in backward direction
    # iterating within forward
    # direction in array
    for i in range(n):

        # if arr[i]==0, it is breaking
        # condition for contiguous subarray
        max_till_now = max_till_now * arr[i]
        if (max_till_now == 0):
            isZero=True
            max_till_now = 1;
            continue

        if (max_fwd < max_till_now): #update max_fwd
            max_fwd = max_till_now

    max_till_now = 1

    # iterating within backward
    # direction in array
    for i in range(n - 1, -1, -1):
        max_till_now = max_till_now * arr[i]

        if (max_till_now == 0):
            isZero=True
            max_till_now = 1
            continue

        # update max_bkd
        if (max_bkd < max_till_now) :
            max_bkd = max_till_now

    # return max of max_fwd and max_bkd
    res = max(max_fwd, max_bkd)

    # Product should not be negative.
    # (Product of an empty subarray is
    # considered as 0)
    if isZero==True :
        return max(res, 0)

    return res

# Driver Code
arr = [-1, -2, -3, 4]
n = len(arr)
print(max_product(arr, n))

# This code is contributed
# by Yatin Gupta
```

## C#

```
// C# program to find maximum product
// subarray
using System;

class GFG {

    // Function for maximum product
    static int max_product(int []arr, int n)
    {

        // Initialize maximum products in
        // forward and backward directions
        int max_fwd = int.MinValue,
            max_bkd = int.MinValue;

        // Initialize current product
        int max_till_now = 1;

        // max_fwd for maximum contiguous
        // product in forward direction
        // max_bkd for maximum contiguous
        // product in backward direction
        // iterating within forward
        // direction in array
        for (int i = 0; i < n; i++)
        {

            // if arr[i]==0, it is breaking
            // condition for contiguous subarray
            max_till_now = max_till_now * arr[i];

            if (max_till_now == 0)
            {
                max_till_now = 1;
                continue;
            }

            // update max_fwd
            if (max_fwd < max_till_now)
                max_fwd = max_till_now;
        }

        max_till_now = 1;

        // iterating within backward
        // direction in array
        for (int i = n - 1; i >= 0; i--)
        {
            max_till_now = max_till_now * arr[i];
            if (max_till_now == 0)
            {
                max_till_now = 1;
                continue;
            }

            // update max_bkd
            if (max_bkd < max_till_now)
                max_bkd = max_till_now;
        }

        // return max of max_fwd and max_bkd
        int res = Math. Max(max_fwd, max_bkd);

        // Product should not be negative.
        // (Product of an empty subarray is
        // considered as 0)
        return Math.Max(res, 0);
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {-1, -2, -3, 4};
        int n = arr.Length;

        Console.Write( max_product(arr, n) );
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// product subarray

// Function for maximum product
function max_product( $arr, $n)
{

    // Initialize maximum products
    // in forward and backward
    // directions
    $max_fwd = PHP_INT_MIN;
    $max_bkd = PHP_INT_MIN;

    // Initialize current product
    $max_till_now = 1;

    // max_fwd for maximum contiguous
    // product in forward direction
    // max_bkd for maximum contiguous
    // product in backward direction
    // iterating within forward direction
    // in array
    for ($i = 0; $i < $n; $i++)
    {

        // if arr[i]==0, it is
        // breaking condition
        // for contiguous subarray
        $max_till_now = $max_till_now * $arr[$i];
        if ($max_till_now == 0)
        {
            $max_till_now = 1;
            continue;
        }

        // update max_fwd
        if ($max_fwd < $max_till_now)
            $max_fwd = $max_till_now;
    }

    $max_till_now = 1;

    // iterating within backward
    // direction in array
    for($i = $n - 1; $i >= 0; $i--)
    {
        $max_till_now = $max_till_now * $arr[$i];
        if ($max_till_now == 0)
        {
            $max_till_now = 1;
            continue;
        }

        // update max_bkd
        if ($max_bkd < $max_till_now)
            $max_bkd = $max_till_now;
    }

    // return max of max_fwd
    // and max_bkd
    $res = max($max_fwd, $max_bkd);

    // Product should not be negative.
    // (Product of an empty subarray is
    // considered as 0)
    return max($res, 0);
}

    // Driver Code
    $arr = array(-1, -2, -3, 4);
    $n = count($arr);
    echo max_product($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find maximum product
    // subarray

    // Function for maximum product
    function max_product(arr, n)
    {

        // Initialize maximum products in
        // forward and backward directions
        let max_fwd = Number.MIN_VALUE,
            max_bkd = Number.MIN_VALUE;

        // Initialize current product
        let max_till_now = 1;

        // max_fwd for maximum contiguous
        // product in forward direction
        // max_bkd for maximum contiguous
        // product in backward direction
        // iterating within forward
        // direction in array
        for (let i = 0; i < n; i++)
        {

            // if arr[i]==0, it is breaking
            // condition for contiguous subarray
            max_till_now = max_till_now * arr[i];

            if (max_till_now == 0)
            {
                max_till_now = 1;
                continue;
            }

            // update max_fwd
            if (max_fwd < max_till_now)
                max_fwd = max_till_now;
        }

        max_till_now = 1;

        // iterating within backward
        // direction in array
        for (let i = n - 1; i >= 0; i--)
        {
            max_till_now = max_till_now * arr[i];
            if (max_till_now == 0)
            {
                max_till_now = 1;
                continue;
            }

            // update max_bkd
            if (max_bkd < max_till_now)
                max_bkd = max_till_now;
        }

        // return max of max_fwd and max_bkd
        let res = Math.max(max_fwd, max_bkd);

        // Product should not be negative.
        // (Product of an empty subarray is
        // considered as 0)
        return Math.max(res, 0);
    }

    let arr = [-1, -2, -3, 4];
    let n = arr.length;

    document.write(max_product(arr, n) );

</script>
```

**输出:**

```
24
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
注意，上面的解需要一个数组的两次遍历，而[之前的解](https://www.geeksforgeeks.org/maximum-product-subarray/)只需要一次遍历。
本文由**沙莎克·米什拉(古鲁)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。