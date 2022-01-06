# 循环寻找最长的递增子序列

> 原文:[https://www . geesforgeks . org/find-最长-递增-子序列-循环-方式/](https://www.geeksforgeeks.org/find-longest-increasing-subsequence-circular-manner/)

给定一个数组，任务是循环找到 [LIS(最长递增子序列)](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)。
**例:**

```
Input : arr[] = {5, 4, 3, 2, 1}
Output : 2
Although there is no LIS in a given array 
but in a circular form there can be
{1, 5}, {2, 5}, ...... 

Input : arr[]= {5, 6, 7, 1, 2, 3}
Output : 6
{1, 2, 3, 5, 6, 7} will be the LIS in the
circular manner.
```

1.  将相同的元素(即整个数组)附加到给定的数组中。
2.  对于每个大小为 n 的窗口(给定数组中元素的数量)，执行 LIS。
3.  返回最大长度。

```
For example : Given array is {1, 4, 6, 2, 3}

After appending elements resultant array
will be {1, 4, 6, 2, 3, 1, 4, 6, 2, 3}.

Now for every consecutive n elements perform LIS.
1- {1, 4, 6, 2, 3} --3 is length of LIS.
2- {4, 6, 2, 3, 1} --2 is length of LIS.
3- {6, 2, 3, 1, 4} --3
4- {2, 3, 1, 4, 6}-- 4 {2, 3, 4, 6}
5- {3, 1, 4, 6, 2} --3.
6- {1, 4, 6, 2, 3} Original list.

So, maximum length of LIS in circular manner is 4\. 
```

在最后一个窗口中，我们将拥有与给定数组中相同的元素，我们不需要再次计算，因此我们可以只追加 n-1 个元素来减少操作的数量。

## C++

```
// C++ implementation to find LIS in circular way
#include<bits/stdc++.h>
using namespace std;

// Utility function to find LIS using Dynamic programming
int computeLIS(int circBuff[], int start, int end, int n)
{
    int LIS[end-start];

    /* Initialize LIS values for all indexes */
    for (int i = start; i < end; i++)
        LIS[i] = 1;

    /* Compute optimized LIS values in bottom up manner */
    for (int i = start + 1; i < end; i++)

        // Set j on the basis of current window
        // i.e. first element of the current window
        for (int j = start; j < i; j++ )
            if (circBuff[i] > circBuff[j] && LIS[i] < LIS[j] + 1)
                LIS[i] = LIS[j] + 1;

    /* Pick maximum of all LIS values */
    int res = INT_MIN;
    for (int i = start; i < end; i++)
        res = max(res, LIS[i]);

    return res;
}

// Function to find Longest Increasing subsequence in
// Circular manner
int LICS(int arr[], int n)
{
    // Make a copy of given array by appending same
    // array elements  to itself
    int circBuff[2 * n];
    for (int i = 0; i<n; i++)
        circBuff[i] = arr[i];
    for (int i = n; i < 2*n; i++)
        circBuff[i] = arr[i-n];

    // Perform LIS for each window of size n
    int res = INT_MIN;
    for (int i=0; i<n; i++)
        res = max(computeLIS(circBuff, i, i + n, n), res);

    return res;
}

/* Driver program to test above function */
int main()
{
    int arr[] = { 1, 4, 6, 2, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Length of LICS is " << LICS( arr, n );
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find LIS in circular way

class Test
{
    // Utility method to find LIS using Dynamic programming
    static int computeLIS(int circBuff[], int start, int end, int n)
    {
        int LIS[] = new int[n+end-start];

        /* Initialize LIS values for all indexes */
        for (int i = start; i < end; i++)
            LIS[i] = 1;

        /* Compute optimized LIS values in bottom up manner */
        for (int i = start + 1; i < end; i++)

            // Set j on the basis of current window
            // i.e. first element of the current window
            for (int j = start; j < i; j++ )
                if (circBuff[i] > circBuff[j] && LIS[i] < LIS[j] + 1)
                    LIS[i] = LIS[j] + 1;

        /* Pick maximum of all LIS values */
        int res = Integer.MIN_VALUE;
        for (int i = start; i < end; i++)
            res = Math.max(res, LIS[i]);

        return res;
    }

    // Function to find Longest Increasing subsequence in
    // Circular manner
    static int LICS(int arr[], int n)
    {
        // Make a copy of given array by appending same
        // array elements  to itself
        int circBuff[] = new int[2 * n];
        for (int i = 0; i<n; i++)
            circBuff[i] = arr[i];
        for (int i = n; i < 2*n; i++)
            circBuff[i] = arr[i-n];

        // Perform LIS for each window of size n
        int res = Integer.MIN_VALUE;
        for (int i=0; i<n; i++)
            res = Math.max(computeLIS(circBuff, i, i + n, n), res);

        return res;
    }

    // Driver method
    public static void main(String args[])
    {
         int arr[] = { 1, 4, 6, 2, 3 };
         System.out.println("Length of LICS is " + LICS( arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find
# LIS in circular way Utility
# function to find LIS using
# Dynamic programmi
def computeLIS(circBuff, start, end, n):
    LIS = [0 for i in range(end)]

    # Initialize LIS values
    # for all indexes
    for i in range(start, end):
        LIS[i] = 1

    # Compute optimized LIS values
    # in bottom up manner
    for i in range(start + 1, end):

        # Set j on the basis of current
        # window i.e. first element of
        # the current window
        for j in range(start,i):
            if (circBuff[i] > circBuff[j] and
                LIS[i] < LIS[j] + 1):
                LIS[i] = LIS[j] + 1

    # Pick maximum of all LIS values
    res = -100000
    for i in range(start, end):
        res = max(res, LIS[i])
    return res

# Function to find Longest Increasing
# subsequence in Circular manner
def LICS(arr, n):

    # Make a copy of given
    # array by appending same
    # array elements to itself
    circBuff = [0 for i in range(2 * n)]
    for i in range(n):
        circBuff[i] = arr[i]
    for i in range(n, 2 * n):
        circBuff[i] = arr[i - n]

    # Perform LIS for each
    # window of size n
    res = -100000
    for i in range(n):
        res = max(computeLIS(circBuff, i,
                             i + n, n), res)
    return res

# Driver code
arr = [ 1, 4, 6, 2, 3 ]
n = len(arr)
print("Length of LICS is", LICS(arr, n))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# implementation to find
// LIS in circular way
using System;

class Test
{
    // Utility method to find LIS
    // using Dynamic programming
    static int computeLIS(int []circBuff, int start,
                                     int end, int n)
    {
        int []LIS = new int[n+end-start];

        /* Initialize LIS values for all indexes */
        for (int i = start; i < end; i++)
            LIS[i] = 1;

        /* Compute optimized LIS values
           in bottom up manner */
        for (int i = start + 1; i < end; i++)

            // Set j on the basis of current window
            // i.e. first element of the current window
            for (int j = start; j < i; j++ )
                if (circBuff[i] > circBuff[j] &&
                            LIS[i] < LIS[j] + 1)
                    LIS[i] = LIS[j] + 1;

        /* Pick maximum of all LIS values */
        int res = int.MinValue;
        for (int i = start; i < end; i++)
            res = Math.Max(res, LIS[i]);

        return res;
    }

    // Function to find Longest Increasing
    // subsequence in Circular manner
    static int LICS(int []arr, int n)
    {
        // Make a copy of given array by
        // appending same array elements to itself
        int []circBuff = new int[2 * n];

        for (int i = 0; i<n; i++)
            circBuff[i] = arr[i];
        for (int i = n; i < 2*n; i++)
            circBuff[i] = arr[i-n];

        // Perform LIS for each window of size n
        int res = int.MinValue;
        for (int i=0; i<n; i++)
            res = Math.Max(computeLIS(circBuff, i, i + n, n), res);

        return res;
    }

    // Driver method
    public static void Main()
    {
        int []arr = {1, 4, 6, 2, 3};
        Console.Write("Length of LICS is " +
                    LICS( arr, arr.Length));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find LIS in circular way

// Utility function to find
// LIS using Dynamic programming
function computeLIS($circBuff,
                    $start,
                    $end, $n)
{
    $LIS = Array();

    /* Initialize LIS values
    for all indexes */
    for ($i = $start; $i < $end; $i++)
        $LIS[$i] = 1;

    /* Compute optimized LIS
    values in bottom up manner */
    for ($i = $start + 1; $i < $end; $i++)

        // Set j on the basis of
        // current window
        // i.e. first element of
        // the current window
        for ( $j = $start; $j < $i; $j++ )
            if ($circBuff[$i] > $circBuff[$j] &&
                     $LIS[$i] < $LIS[$j] + 1)
                $LIS[$i] = $LIS[$j] + 1;

    /* Pick maximum of
    all LIS values */
    $res = PHP_INT_MIN;
    for ($i = $start; $i < $end; $i++)
        $res = max($res, $LIS[$i]);

    return $res;
}

// Function to find LIS
// in Circular manner
function LICS($arr, $n)
{
    // Make a copy of given array
    // by appending same array
    // elements to itself
    for ($i = 0; $i < $n; $i++)
        $circBuff[$i] = $arr[$i];
    for ($i = $n; $i < 2 * $n; $i++)
        $circBuff[$i] = $arr[$i - $n];

    // Perform LIS for each
    // window of size n
    $res = PHP_INT_MIN;
    for ($i = 0; $i < $n; $i++)
        $res = max(computeLIS($circBuff, $i,
                              $i + $n, $n),
                              $res);

    return $res;
}

// Driver Code
$arr = array(1, 4, 6, 2, 3);
$n = sizeof($arr);

echo "Length of LICS is " ,
            LICS($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to find LIS in circular way

    // Utility method to find LIS
    // using Dynamic programming
    function computeLIS(circBuff, start, end, n)
    {
        let LIS = new Array(n+end-start);

        /* Initialize LIS values for all indexes */
        for (let i = start; i < end; i++)
            LIS[i] = 1;

        /* Compute optimized LIS values
           in bottom up manner */
        for (let i = start + 1; i < end; i++)

            // Set j on the basis of current window
            // i.e. first element of the current window
            for (let j = start; j < i; j++ )
                if (circBuff[i] > circBuff[j] && LIS[i] < LIS[j] + 1)
                    LIS[i] = LIS[j] + 1;

        /* Pick maximum of all LIS values */
        let res = Number.MIN_VALUE;
        for (let i = start; i < end; i++)
            res = Math.max(res, LIS[i]);

        return res;
    }

    // Function to find Longest Increasing
    // subsequence in Circular manner
    function LICS(arr, n)
    {
        // Make a copy of given array by
        // appending same array elements to itself
        let circBuff = new Array(2 * n);

        for (let i = 0; i<n; i++)
            circBuff[i] = arr[i];
        for (let i = n; i < 2*n; i++)
            circBuff[i] = arr[i-n];

        // Perform LIS for each window of size n
        let res = Number.MIN_VALUE;
        for (let i=0; i<n; i++)
            res = Math.max(computeLIS(circBuff, i, i + n, n), res);

        return res;
    }

    let arr = [1, 4, 6, 2, 3];
    document.write("Length of LICS is " + LICS( arr, arr.length));

</script>
```

**输出:**

```
Length of LICS is 4
```

上述解的时间复杂度为 O(n <sup>3</sup> )。使用 [O(n Log n)算法查找 LIS](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/) 可以减少 O(n <sup>2</sup> Log n)。
**参考:**
[https://www.careercup.com/question?id=5942735794077696](https://www.careercup.com/question?id=5942735794077696)
本文由 [**萨希尔·查布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。