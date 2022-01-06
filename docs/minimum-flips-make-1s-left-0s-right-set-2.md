# 最小翻转，使所有 1 在左边，0 在右边|第 2 组

> 原文:[https://www . geesforgeks . org/minimum-flips-make-1s-left-0s-right-set-2/](https://www.geeksforgeeks.org/minimum-flips-make-1s-left-0s-right-set-2/)

给定一个二进制数组，我们可以将所有的 1 翻转到左边，将所有的 0 翻转到右边。计算左全 1 和右全 0 所需的最小翻转次数。
**例:**

```
Input: 1011000  
Output: 1
1 flip is required to make it 1111000.

Input : 00001 
Output : 2
2 flips required to make it 10000.
```

我们已经在下面的帖子中讨论了基于位掩码的解决方案。[最小翻转，使左 1 全 1，右 0 全 1 |设置 1(使用位掩码)](https://www.geeksforgeeks.org/minimum-flips-make-1s-left-0s-right-set-1-using-bitmask/)
可以用 O(N)个时间复杂度(其中 N 为位数)和 O(N)个额外内存
来完成

1.  计算从左向右移动时需要完成的“0”翻转次数，以使所有“1”都以位为单位。
2.  计算从右向左移动时需要完成的“1”翻转次数，以使所有“0”都以位为单位。
3.  遍历位与位之间的所有位置，找到两个数组中“0”-翻转+“1”-翻转的最小和。

## C++

```
// CPP program to find minimum flips required
// to make all 1s in left and 0s in right.
#include <bits/stdc++.h>
using namespace std;

int minimalFilps(string bits)
{
    int n = bits.length();

    // two arrays will keep the count for number
    // of 0s' and 1s' to be flipped while
    // traversing from left to right and right to
    // left respectively
    int flipsFromLeft[n];
    int flipsFromRight[n];

    // Fill flipsFromLeft[]
    int flips = 0;
    for (int i = 0; i < n; i++) {
        if (bits[i] == '0')
            flips++;        
        flipsFromLeft[i] = flips;
    }

    // Fill flipsFromRight[]
    flips = 0;
    for (int i = n - 1; i >= 0; i--) {
        if (bits[i] == '1')
            flips++;        
        flipsFromRight[i] = flips;
    }

    // initialize minFlip to highest int value. If sum
    // of leftflip and rightFlip is smaller than minflips,
    // then update minFlips
    int minFlips = INT_MAX;
    for (int i = 1; i < n; i++) {
        if (flipsFromLeft[i - 1] + flipsFromRight[i] < minFlips)
            minFlips = flipsFromLeft[i - 1] + flipsFromRight[i];
    }

    return minFlips;
}

// Driver code
int main()
{
    string bits = "00001";
    cout << minimalFilps(bits) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum flips required
// to make all 1s in left and 0s in right.
import java.io.*;

class GFG
{
    static int minimalFilps(String bits)
    {
        int n = bits.length();

        // two arrays will keep the count
        // for number of 0s' and 1s' to be
        // flipped while traversing from
        // left to right and right to
        // left respectively
        int flipsFromLeft[] = new int[n];
        int flipsFromRight[] =new int[n] ;

        // Fill flipsFromLeft[]
        int flips = 0;
        for (int i = 0; i < n; i++)
        {
            if (bits.charAt(i) == '0')
                flips++;        
            flipsFromLeft[i] = flips;
        }

        // Fill flipsFromRight[]
        flips = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            if (bits.charAt(i) == '1')
                flips++;        
            flipsFromRight[i] = flips;
        }

        // initialize minFlip to highest int value. If sum
        // of leftflip and rightFlip is smaller than minflips,
        // then update minFlips
        int minFlips = Integer.MAX_VALUE;
        for (int i = 1; i < n; i++)
        {
            if (flipsFromLeft[i - 1] + flipsFromRight[i]
                                              < minFlips)
                minFlips = flipsFromLeft[i - 1]
                           + flipsFromRight[i];
        }

        return minFlips;
    }

    // Driver code
    public static void main (String[] args)
    {
        String bits = "00001";
        System.out.println(minimalFilps(bits));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find minimum flips required
# to make all 1s in left and 0s in right.
import sys

def minimalFilps(bits):
    n = len(bits)

    # two arrays will keep the count for number
    # of 0s' and 1s' to be flipped while
    # traversing from left to right and right to
    # left respectively
    flipsFromLeft = [0 for i in range(n)]
    flipsFromRight = [0 for i in range(n)]

    # Fill flipsFromLeft[]
    flips = 0
    for i in range(0, n, 1):
        if (bits[i] == '0'):
            flips = flips + 1   
        flipsFromLeft[i] = flips

    # Fill flipsFromRight[]
    flips = 0
    i = n - 1
    while(i >= 0):
        if (bits[i] == '1'):
            flips = flips + 1
        i = i - 1
        flipsFromRight[i] = flips

    # initialize minFlip to highest int value.
    # If sum of leftflip and rightFlip is smaller
    # than minflips, then update minFlips
    minFlips = sys.maxsize
    for i in range(1, n, 1):
        if (flipsFromLeft[i - 1] +
            flipsFromRight[i] < minFlips):
            minFlips = (flipsFromLeft[i - 1] +
                        flipsFromRight[i])

    return minFlips

# Driver code
if __name__ == '__main__':
    bits = "00001"
    print(minimalFilps(bits))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find minimum flips required
// to make all 1s in left and 0s in right.
using System;

class GFG
{
    static int minimalFilps(String bits)
    {
        int n = bits.Length;

        // two arrays will keep the count
        // for number of 0s' and 1s' to be
        // flipped while traversing from
        // left to right and right to
        // left respectively
        int []flipsFromLeft = new int[n];
        int []flipsFromRight =new int[n] ;

        // Fill flipsFromLeft[]
        int flips = 0;
        for (int i = 0; i < n; i++)
        {
            if (bits[i] == '0')
                flips++;        
            flipsFromLeft[i] = flips;
        }

        // Fill flipsFromRight[]
        flips = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            if (bits[i] == '1')
                flips++;        
            flipsFromRight[i] = flips;
        }

        // initialize minFlip to highest int value.
        // If sum of leftflip and rightFlip is smaller
        // than minflips, then update minFlips
        int minFlips = int.MaxValue;
        for (int i = 1; i < n; i++)
        {
            if (flipsFromLeft[i - 1] + flipsFromRight[i] < minFlips)
            minFlips = flipsFromLeft[i - 1] + flipsFromRight[i];
        }

        return minFlips;
    }

    // Driver code
    public static void Main ()
    {
        string bits = "00001";
        Console.WriteLine(minimalFilps(bits));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// flips required to make all
// 1s in left and 0s in right.

function minimalFilps($bits)
{
    $n = strlen($bits);

    // two arrays will keep the
    // count for number of 0s'
    // and 1s' to be flipped
    // while traversing from
    // left to right and right
    // to left respectively
    $flipsFromLeft[$n] = 0;
    $flipsFromRight[$n] = 0;

    // Fill flipsFromLeft[]
    $flips = 0;
    for ($i = 0; $i < $n; $i++) {
        if ($bits[$i] == '0')
            $flips++;        
        $flipsFromLeft[$i] = $flips;
    }

    // Fill flipsFromRight[]
    $flips = 0;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        if ($bits[$i] == '1')
            $flips++;        
        $flipsFromRight[$i] = $flips;
    }

    // initialize minFlip to
    // highest int value. If sum
    // of leftflip and rightFlip
    // is smaller than minflips,
    // then update minFlips
    $INT_MAX=2147483647;
    $minFlips = $INT_MAX;
    for ($i = 1; $i < $n; $i++)
    {
        if ($flipsFromLeft[$i - 1] +
            $flipsFromRight[$i] < $minFlips)
            $minFlips = $flipsFromLeft[$i - 1] +
                        $flipsFromRight[$i];
    }

    return $minFlips;
}

    // Driver Code
    $bits = "00001";
    echo minimalFilps($bits) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum flips required
    // to make all 1s in left and 0s in right.

    function minimalFilps(bits)
    {
        let n = bits.length;

        // two arrays will keep the count
        // for number of 0s' and 1s' to be
        // flipped while traversing from
        // left to right and right to
        // left respectively
        let flipsFromLeft = new Array(n);
        flipsFromLeft.fill(0);
        let flipsFromRight =new Array(n);
        flipsFromRight.fill(0);

        // Fill flipsFromLeft[]
        let flips = 0;
        for (let i = 0; i < n; i++)
        {
            if (bits[i] == '0')
                flips++;        
            flipsFromLeft[i] = flips;
        }

        // Fill flipsFromRight[]
        flips = 0;
        for (let i = n - 1; i >= 0; i--)
        {
            if (bits[i] == '1')
                flips++;        
            flipsFromRight[i] = flips;
        }

        // initialize minFlip to highest int value.
        // If sum of leftflip and rightFlip is smaller
        // than minflips, then update minFlips
        let minFlips = Number.MAX_VALUE;
        for (let i = 1; i < n; i++)
        {
            if (flipsFromLeft[i - 1] + flipsFromRight[i] < minFlips)
                minFlips = flipsFromLeft[i - 1] + flipsFromRight[i];
        }

        return minFlips;
    }

    let bits = "00001";
      document.write(minimalFilps(bits));

 // This code is contributed by divyesh072019.
</script>
```

输出:

```
2
```