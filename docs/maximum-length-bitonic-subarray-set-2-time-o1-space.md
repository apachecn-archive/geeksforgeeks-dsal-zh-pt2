# 最大长度双离子子阵列|集合 2 (O(n)时间和 O(1)空间)

> 原文:[https://www . geesforgeks . org/maximum-length-bitonic-subarray-set-2-time-O1-space/](https://www.geeksforgeeks.org/maximum-length-bitonic-subarray-set-2-time-o1-space/)

给定一个包含 n 个正整数的数组 A[0 … n-1]，如果有一个 k 和 i <= k <= j such that A[i] = .. A[j – 1] > = A[j]，那么子数组 A[i … j]就是双调和的。编写一个函数，以数组为参数，返回最大长度的二次子数组的长度。

我们已经在下面的帖子中讨论了 O(n)时间和 O(n)空间方法。
[最大长度双离子子阵列|集合 1 (O(n)时间和 O(n)空间)](https://www.geeksforgeeks.org/maximum-length-bitonic-subarray/)
在这个集合中，我们将讨论取常数额外空间的解。
想法是从 A[i]开始检查最长的双离子子阵列。从 A[i]开始，首先我们将检查上升结束，然后下降结束。当沿着当前子阵列的斜率下降时，当发现两个相等的值时，通过记录下一个开始位置来考虑双子阵列的重叠。如果这个子阵列的长度大于 max_len，我们将更新 max_len。我们继续这个过程，直到数组结束。

## C++

```
// C++ program to find length of longest bitonic
// subarray. O(n) time and O(1) extra space
#include <iostream>
using namespace std;

// Function to find length of longest bitonic
// subarray
int bitonic(int *A, int n)
{
    // if A is empty
    if (n == 0)
        return 0;

    // initializing max_len
    int maxLen=1;

    int start=0;
    int nextStart=0;

    int j =0;
    while (j < n-1)
    {
        // look for end of ascent      
        while (j<n-1 && A[j]<=A[j+1])
            j++;

        // look for end of descent      
        while (j<n-1 && A[j]>=A[j+1]){

            // adjusting nextStart;
            // this will be necessarily executed at least once,
            // when we detect the start of the descent
            if (j<n-1 && A[j]>A[j+1])
                nextStart=j+1;

            j++;
        }

        // updating maxLen, if required
        maxLen = max(maxLen,j-(start-1));

        start=nextStart;
    }

    return maxLen;
}

int main()
{
    int A[] = {12, 4, 78, 90, 45, 23};
    int n = sizeof(A)/sizeof(A[0]);
    printf("Length of max length Bitonic "
            "Subarray is %d", bitonic(A, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of longest bitonic
// subarray O(n) time and O(1) extra space

public class MaxLengthBitonic
{
    // Method to find length of longest bitonic
    // subarray
    static int maxLenBitonic(int[] A,int n)
    {
        // if A is empty
        if (n == 0)
            return 0;

        // initializing max_len
        int maxLen=1;

        int start=0;
        int nextStart=0;

        int j =0;
        while (j < n-1)
        {
            // look for end of ascent      
            while (j<n-1 && A[j]<=A[j+1])
                j++;

            // look for end of descent      
            while (j<n-1 && A[j]>=A[j+1]){

                // adjusting nextStart;
                // this will be necessarily executed at least once,
                // when we detect the start of the descent
                if (j<n-1 && A[j]>A[j+1])
                    nextStart=j+1;

                j++;
            }

            // updating maxLen, if required
            maxLen = Math.max(maxLen,j-(start-1));

            start=nextStart;
        }

        return maxLen;
    }

    public static void  main(String[] args)
    {
        int A[] = {12, 4, 78, 90, 45, 23};
        System.out.println("Length of maximal length bitonic " +
                            "subarray is " + maxLenBitonic(A,A.length));

    }
}
// This code is contributed by Markus Schott
```

## 蟒蛇 3

```
# Python3 program to find length of longest bitonic
# subarray. O(n) time and O(1) extra space

# Function to find length of longest
# bitonic subarray
def bitonic(A, n):

    # if A is empty
    if (n == 0):
        return 0;

    # initializing max_len
    maxLen = 1;

    start = 0;
    nextStart = 0;

    j = 0;
    while (j < n - 1):

        # look for end of ascent    
        while (j < n - 1 and A[j] <= A[j + 1]):
            j = j + 1;

        # look for end of descent
        while (j < n - 1 and A[j] >= A[j + 1]):

            # adjusting nextStart;
            # this will be necessarily executed
            # at least once, when we detect the
            # start of the descent
            if (j < n - 1 and A[j] > A[j + 1]):
                nextStart = j + 1;

            j = j + 1;

        # updating maxLen, if required
        maxLen = max(maxLen, j - (start - 1));

        start = nextStart;

    return maxLen;

# Driver Code
A = [12, 4, 78, 90, 45, 23];
n = len(A);
print("Length of max length Bitonic Subarray is",
                                  bitonic(A, n));

# This code is contributed by Shivi_Aggarwal
```

## C#

```
// C# program to find length of longest bitonic
// subarray O(n) time and O(1) extra space
using System;

class MaxLengthBitonic
{
    // Method to find length of
    // longest bitonic subarray
    static int maxLenBitonic(int[] A, int n)
    {
        // if A is empty
        if (n == 0)
            return 0;

        // initializing max_len
        int maxLen = 1;

        int start = 0;
        int nextStart = 0;

        int j = 0;
        while (j < n-1)
        {
            // look for end of ascent    
            while (j < n-1 && A[j] <= A[j+1])
                j++;

            // look for end of descent    
            while (j < n-1 && A[j] >= A[j+1]){

                // adjusting nextStart;
                // this will be necessarily executed at least once,
                // when we detect the start of the descent
                if (j < n-1 && A[j] > A[j+1])
                    nextStart=j + 1;

                j++;
            }

            // updating maxLen, if required
            maxLen = Math.Max(maxLen, j - (start - 1));

            start=nextStart;
        }
        return maxLen;
    }

    public static void Main()
    {
        int []A = {12, 4, 78, 90, 45, 23};
        Console.Write("Length of maximal length bitonic " +
                      "subarray is " + maxLenBitonic(A, A.Length));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of
// longest bitonic subarray.
// O(n) time and O(1) extra space

// Function to find length of
// longest bitonic subarray
function bitonic($A, $n)
{

    // if A is empty
    if ($n == 0)
        return 0;

    // initializing max_len
    $maxLen = 1;

    $start = 0;
    $nextStart = 0;

    $j = 0;
    while ($j < $n - 1)
    {

        // look for end of ascent    
        while ($j < $n - 1 &&
               $A[$j] <= $A[$j + 1])
            $j++;

        // look for end of descent    
        while ($j < $n - 1 &&
               $A[$j] >= $A[$j + 1])
        {

            // adjusting nextStart;
            // this will be necessarily
            // executed at least once,
            // when we detect the start
            // of the descent
            if ($j < $n - 1 && $A[$j] >
                          $A[$j + 1])
                $nextStart = $j + 1;
            $j++;
        }

        // updating maxLen,
        // if required
        $maxLen = max($maxLen, $j - ($start - 1));
        $start = $nextStart;
    }

    return $maxLen;
}

    // Driver Code
    $A = array(12, 4, 78, 90, 45, 23);
    $n = sizeof($A);
    echo "Length of max length Bitonic "
        ,"Subarray is ", bitonic($A, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find length of
// longest bitonic subarray.
// O(n) time and O(1) extra space

// Function to find length of
// longest bitonic subarray
function bitonic(A, n) {

    // if A is empty
    if (n == 0)
        return 0;

    // initializing max_len
    let maxLen = 1;

    let start = 0;
    let nextStart = 0;

    let j = 0;
    while (j < n - 1) {

        // look for end of ascent   
        while (j < n - 1 &&
            A[j] <= A[j + 1])
            j++;

        // look for end of descent   
        while (j < n - 1 &&
            A[j] >= A[j + 1]) {

            // adjusting nextStart;
            // this will be necessarily
            // executed at least once,
            // when we detect the start
            // of the descent
            if (j < n - 1 && A[j] >
                A[j + 1])
                nextStart = j + 1;
            j++;
        }

        // updating maxLen,
        // if required
        maxLen = Math.max(maxLen, j - (start - 1));
        start = nextStart;
    }

    return maxLen;
}

// Driver Code
let A = new Array(12, 4, 78, 90, 45, 23);
let n = A.length;
document.write("Length of max length Bitonic "
    + "Subarray is " + bitonic(A, n));

// This code is contributed by gfgking

</script>
```

**输出:**

```
Length of max length bitonic subarray is 5
```

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。