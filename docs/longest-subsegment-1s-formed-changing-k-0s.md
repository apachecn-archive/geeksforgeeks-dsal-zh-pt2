# 最多改变 k '0 '形成的' 1 '的最长亚段

> 原文:[https://www . geesforgeks . org/long-subsegment-1s-formed-changing-k-0s/](https://www.geeksforgeeks.org/longest-subsegment-1s-formed-changing-k-0s/)

给定一个二进制数组 a[]和一个数字 k，我们需要通过最多改变 k 个‘0’来找到可能的‘1’的最长子段的长度。
示例:

```
Input : a[] = {1, 0, 0, 1, 1, 0, 1}, 
          k = 1.
Output : 4
Explanation : Here, we should only change 1
zero(0). Maximum possible length we can get
is by changing the 3rd zero in the array, 
we get a[] = {1, 0, 0, 1, 1, 1, 1}

Input : a[] = {1, 0, 0, 1, 0, 1, 0, 1, 0, 1}, 
         k = 2.
Output : 5
Output: Here, we can change only 2 zeros. 
Maximum possible length we can get is by 
changing the 3rd and 4th (or) 4th and 5th 
zeros.
```

我们可以使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)技术来解决这个问题。让我们拿一个最多包含 k 个零的子阵列[l，r]来说。让我们的左指针为 l，右指针为 r。我们总是通过移动左指针 l 来保持我们的子段[l，r]包含不超过 k 个零。在每一步检查最大大小(即 r-l+1)。

## C++

```
// CPP program to find length of longest
// subsegment of all 1's by changing at
// most k 0's
#include <iostream>
using namespace std;

int longestSubSeg(int a[], int n, int k)
{
    int cnt0 = 0;
    int l = 0;
    int max_len = 0;

    // i decides current ending point
    for (int i = 0; i < n; i++) {
        if (a[i] == 0)
            cnt0++;

        // If there are more 0's move
        // left point for current ending
        // point.
        while (cnt0 > k) {
            if (a[l] == 0)
                cnt0--;
            l++;
        }

        max_len = max(max_len, i - l + 1);
    }

    return max_len;
}

// Driver code
int main()
{
    int a[] = { 1, 0, 0, 1, 0, 1, 0, 1 };
    int k = 2;
    int n = sizeof(a) / sizeof(a[0]);
    cout << longestSubSeg(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of
// longest subsegment of all 1's
// by changing at most k 0's
import java.io.*;

class GFG {

static int longestSubSeg(int a[], int n,
                                  int k)
{
    int cnt0 = 0;
    int l = 0;
    int max_len = 0;

    // i decides current ending point
    for (int i = 0; i < n; i++) {
        if (a[i] == 0)
            cnt0++;

        // If there are more 0's move
        // left point for current ending
        // point.
        while (cnt0 > k) {
            if (a[l] == 0)
                cnt0--;
            l++;
        }

        max_len = Math.max(max_len, i - l + 1);
    }

    return max_len;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 0, 0, 1, 0, 1, 0, 1 };
    int k = 2;
    int n = a.length;
    System.out.println( longestSubSeg(a, n, k));

}
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to find length
# of longest subsegment of all 1's 
# by changing at most k 0's

def longestSubSeg(a, n, k):

    cnt0 = 0
    l = 0
    max_len = 0;

    # i decides current ending point
    for i in range(0, n):
        if a[i] == 0:
            cnt0 += 1

        # If there are more 0's move
        # left point for current
        # ending point.
        while (cnt0 > k):
            if a[l] == 0:
                cnt0 -= 1
            l += 1

        max_len = max(max_len, i - l + 1);

    return max_len

# Driver code
a = [1, 0, 0, 1, 0, 1, 0, 1 ]
k = 2
n = len(a)
print(longestSubSeg(a, n, k))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find length of
// longest subsegment of all 1's
// by changing at most k 0's
using System;

class GFG {

    static int longestSubSeg(int[] a, int n,
                                      int k)
    {
        int cnt0 = 0;
        int l = 0;
        int max_len = 0;

        // i decides current ending point
        for (int i = 0; i < n; i++)
        {
            if (a[i] == 0)
                cnt0++;

            // If there are more 0's move
            // left point for current ending
            // point.
            while (cnt0 > k) {
                if (a[l] == 0)
                    cnt0--;
                l++;
            }

            max_len = Math.Max(max_len, i - l + 1);
        }

        return max_len;
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 1, 0, 0, 1, 0, 1, 0, 1 };
        int k = 2;
        int n = a.Length;
        Console.WriteLine(longestSubSeg(a, n, k));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of longest
// subsegment of all 1's by changing at
// most k 0's

function longestSubSeg( $a, $n, $k)
{
    $cnt0 = 0;
    $l = 0;
    $max_len = 0;

    // i decides current ending point
    for($i = 0; $i < $n; $i++)
    {
        if ($a[$i] == 0)
            $cnt0++;

        // If there are more 0's move
        // left point for current ending
        // point.
        while ($cnt0 > $k)
        {
            if ($a[$l] == 0)
                $cnt0--;
            $l++;
        }

        $max_len = max($max_len, $i - $l + 1);
    }

    return $max_len;
}

    // Driver code
    $a = array(1, 0, 0, 1, 0, 1, 0, 1);
    $k = 2;
    $n = count($a);
    echo longestSubSeg($a, $n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find length of
    // longest subsegment of all 1's
    // by changing at most k 0's

    function longestSubSeg(a, n, k)
    {
        let cnt0 = 0;
        let l = 0;
        let max_len = 0;

        // i decides current ending point
        for (let i = 0; i < n; i++)
        {
            if (a[i] == 0)
                cnt0++;

            // If there are more 0's move
            // left point for current ending
            // point.
            while (cnt0 > k) {
                if (a[l] == 0)
                    cnt0--;
                l++;
            }

            max_len = Math.max(max_len, i - l + 1);
        }

        return max_len;
    }

    let a = [ 1, 0, 0, 1, 0, 1, 0, 1 ];
    let k = 2;
    let n = a.length;
    document.write(longestSubSeg(a, n, k));

</script>
```

**输出:**

```
5
```