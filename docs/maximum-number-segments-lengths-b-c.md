# 长度为 a、b 和 c 的线段的最大数量

> 原文:[https://www . geesforgeks . org/maximum-number-segments-length-B- c/](https://www.geeksforgeeks.org/maximum-number-segments-lengths-b-c/)

给定一个正整数 N，求 N 可以构成的长度为 a、b、c 的最大线段数
**例:**

```
Input : N = 7, a = 5, b, = 2, c = 5 
Output : 2 
N can be divided into 2 segments of lengths
2 and 5\. For the second example,

Input : N = 17, a = 2, b = 1, c = 3 
Output : 17 
N can be divided into 17 segments of 1 or 8 
segments of 2 and 1 segment of 1\. But 17 segments
of 1 is greater than 9 segments of 2 and 1\.  
```

**方法:**采用的方法是**动态规划**。基本 dp <sub>0</sub> 将为 0，因为它最初没有线段。之后，从 1 到 n 迭代，对于 dp <sub>i+a</sub> 、dp <sub>i+b</sub> 和 dp <sub>i+c</sub> 三种状态中的每一种状态，存储使用或不使用 a、b 或 c 段获得的最大值。
需要处理的 3 种状态是:

> DP<sub>I+a</sub>= max(DP<sub>I</sub>+1，DP<sub>I+a</sub>)；
> DP<sub>【I+b】</sub>= max(DP<sub>【I】</sub>+1，DP<sub>【I+b】</sub>)；
> DP<sub>I+c</sub>= max(DP<sub>I</sub>+1，DP<sub>I+c</sub>)；

以下是上述思路的实现:

## C++

```
// C++ implementation to divide N into
// maximum number of segments
// of length a, b and c
#include <bits/stdc++.h>
using namespace std;

// function to find the maximum
// number of segments
int maximumSegments(int n, int a,
                    int b, int c)
{
    // stores the maximum number of
    // segments each index can have
    int dp[n + 1];

    // initialize with -1
    memset(dp, -1, sizeof(dp));

    // 0th index will have 0 segments
    // base case
    dp[0] = 0;

    // traverse for all possible
    // segments till n
    for (int i = 0; i < n; i++)
    {
        if (dp[i] != -1) {

            // conditions
        if(i + a <= n )    //avoid buffer overflow
                dp[i + a] = max(dp[i] + 1,
                            dp[i + a]);

        if(i + b <= n ) //avoid buffer overflow
                dp[i + b] = max(dp[i] + 1,
                            dp[i + b]);

        if(i + c <= n )    //avoid buffer overflow
                dp[i + c] = max(dp[i] + 1,
                            dp[i + c]);
        }
    }
    return dp[n];
}

// Driver code
int main()
{
    int n = 7, a = 5, b = 2, c = 5;
    cout << maximumSegments(n, a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to divide N into
// maximum number of segments
// of length a, b and c
import java.util.*;

class GFG
{

    // function to find the maximum
    // number of segments
    static int maximumSegments(int n, int a,
                            int b, int c)
    {
        // stores the maximum number of
        // segments each index can have
        int dp[] = new int[n + 10];

        // initialize with -1
        Arrays.fill(dp, -1);

        // 0th index will have 0 segments
        // base case
        dp[0] = 0;

        // traverse for all possible
        // segments till n
        for (int i = 0; i < n; i++)
        {
            if (dp[i] != -1)
            {

                // conditions
                if(i + a <= n )    //avoid buffer overflow
                dp[i + a] = Math.max(dp[i] + 1,
                                    dp[i + a]);

                if(i + b <= n )    //avoid buffer overflow
                dp[i + b] = Math.max(dp[i] + 1,    
                                    dp[i + b]);

                if(i + c <= n )    //avoid buffer overflow
                dp[i + c] = Math.max(dp[i] + 1,
                                    dp[i + c]);
            }
        }
        return dp[n];
    }

    // Driver code
    public static void main(String arg[])
    {
        int n = 7, a = 5, b = 2, c = 5;
        System.out.print(maximumSegments(n, a, b, c));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python implementation
# to divide N into maximum
# number of segments of
# length a, b and c

# function to find
# the maximum number
# of segments
def maximumSegments(n, a, b, c) :

    # stores the maximum
    # number of segments
    # each index can have
    dp = [-1] * (n + 10)

    # 0th index will have
    # 0 segments base case
    dp[0] = 0

    # traverse for all possible
    # segments till n
    for i in range(0, n) :

        if (dp[i] != -1) :

            # conditions
            if(i + a <= n ): # avoid buffer overflow   
                dp[i + a] = max(dp[i] + 1,
                            dp[i + a])

            if(i + b <= n ): # avoid buffer overflow   
                dp[i + b] = max(dp[i] + 1,
                            dp[i + b])

            if(i + c <= n ): # avoid buffer overflow   
                dp[i + c] = max(dp[i] + 1,
                            dp[i + c])

    return dp[n]

# Driver code
n = 7
a = 5
b = 2
c = 5
print (maximumSegments(n, a,
                    b, c))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# implementation to divide N into
// maximum number of segments
// of length a, b and c
using System;

class GFG
{

    // function to find the maximum
    // number of segments
    static int maximumSegments(int n, int a,
                            int b, int c)
    {
        // stores the maximum number of
        // segments each index can have
        int []dp = new int[n + 10];

        // initialize with -1
        for(int i = 0; i < n + 10; i++)
        dp[i]= -1;

        // 0th index will have 0 segments
        // base case
        dp[0] = 0;

        // traverse for all possible
        // segments till n
        for (int i = 0; i < n; i++)
        {
            if (dp[i] != -1)
            {

                // conditions
                if(i + a <= n )    // avoid buffer overflow
                dp[i + a] = Math.Max(dp[i] + 1,
                                    dp[i + a]);

                if(i + b <= n )    // avoid buffer overflow
                dp[i + b] = Math.Max(dp[i] + 1,
                                    dp[i + b]);

                if(i + c <= n )    // avoid buffer overflow
                dp[i + c] = Math.Max(dp[i] + 1,
                                    dp[i + c]);
            }
        }
        return dp[n];
    }

    // Driver code
    public static void Main()
    {
        int n = 7, a = 5, b = 2, c = 5;
        Console.Write(maximumSegments(n, a, b, c));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to divide
// N into maximum number of
// segments of length a, b and c

// function to find the maximum
// number of segments
function maximumSegments($n, $a,
                        $b, $c)
{
    // stores the maximum
    // number of segments
    // each index can have
    $dp = array();

    // initialize with -1
    for($i = 0; $i < $n + 10; $i++)
        $dp[$i]= -1;

    // 0th index will have
    // 0 segments base case
    $dp[0] = 0;

    // traverse for all possible
    // segments till n
    for ($i = 0; $i < $n; $i++)
    {
        if ($dp[$i] != -1)
        {
            // conditions
            if($i + $a <= $n )    // avoid buffer overflow
            $dp[$i + $a] = max($dp[$i] + 1,
                            $dp[$i + $a]);

            if($i + $b <= $n )    // avoid buffer overflow
            $dp[$i + $b] = max($dp[$i] + 1,
                            $dp[$i + $b]);

            if($i + $c <= $n )    // avoid buffer overflow
            $dp[$i + $c] = max($dp[$i] + 1,
                            $dp[$i + $c]);
        }
    }
    return $dp[$n];
}

// Driver code
$n = 7; $a = 5;
$b = 2; $c = 5;
echo (maximumSegments($n, $a,
                    $b, $c));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// JavaScript program implementation to divide N into
// maximum number of segments
// of length a, b and c

    // function to find the maximum
    // number of segments
    function maximumSegments(n, a, b, c)
    {
        // stores the maximum number of
        // segments each index can have
        let dp = [];

        // initialize with -1
        for(let i = 0; i < n + 10; i++)
        dp[i]= -1;

        // 0th index will have 0 segments
        // base case
        dp[0] = 0;

        // traverse for all possible
        // segments till n
        for (let i = 0; i < n; i++)
        {
            if (dp[i] != -1)
            {

                // conditions
                if(i + a <= n )    //avoid buffer overflow
                dp[i + a] = Math.max(dp[i] + 1,
                                    dp[i + a]);

                if(i + b <= n )    //avoid buffer overflow
                dp[i + b] = Math.max(dp[i] + 1,    
                                    dp[i + b]);

                if(i + c <= n )    //avoid buffer overflow
                dp[i + c] = Math.max(dp[i] + 1,
                                    dp[i + c]);
            }
        }
        return dp[n];
    }

// Driver Code

        let n = 7, a = 5, b = 2, c = 5;
        document.write(maximumSegments(n, a, b, c));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
2
```

**时间复杂度** : O(n)