# 一个数的二进制表示中最长的连续零的长度。

> 原文:[https://www . geesforgeks . org/数字的二进制表示中最长连续零的长度/](https://www.geeksforgeeks.org/length-of-longest-consecutive-zeroes-in-the-binary-representation-of-a-number/)

我们有一个数 n。确定其二进制表示中最长的连续 0 的长度。

**示例:**

```
Input  : N = 14
Output : 1
Binary representation of 14 is 
1110\. There is only one 0 in
the binary representation.

Input : N = 9 
Output : 2
```

一种简单的方法是遍历所有的位并记录最大数量的连续 0。

## C++

```
// C++ code to determine Length of
// longest consecutive zeroes in the
// binary representation of a number.
#include <bits/stdc++.h>
using namespace std;

int maxZeros(int N)
{
    // variable to store the length of
    // longest consecutive 0's
    int maxm = -1;

    // to temporary store the consecutive 0's
    int cnt = 0;

    while (N) {
        if (!(N & 1)) {
            cnt++;
            N >>= 1;
            maxm = max(maxm, cnt);
        }
        else {

            maxm = max(maxm, cnt);
            cnt = 0;
            N >>= 1;
        }
    }
    return maxm;
}

// Driver code
int main()
{
    int N = 14;
    cout << maxZeros(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to determine Length of 
// longest consecutive zeroes in the
// binary representation of a number.

public class GFG {

    static int maxZeros(int N)
    {
        // variable to store the length of
        // longest consecutive 0's
        int maxm = -1;

        // to temporary store the consecutive 0's
        int cnt = 0;

        while (N != 0) {
            if ((N & 1) == 0 ) {
                cnt++;
                N >>= 1;
                maxm = Math.max(maxm, cnt);
            }
            else {

                maxm = Math.max(maxm, cnt);
                cnt = 0;
                N >>= 1;
            }
        }
        return maxm;
    }

    // Driver code
    public static void main(String args[])
    {
         int N = 14;
         System.out.println(maxZeros(N));

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 code to determine Length of
# longest consecutive zeroes in the
# binary representation of a number.
def maxZeros(N):

    # variable to store the length
    # of longest consecutive 0's
    maxm = -1

    # to temporary store the
    # consecutive 0's
    cnt = 0
    while(N):
        if(not(N & 1)):
            cnt += 1
            N >>= 1
            maxm = max(maxm,cnt)
        else:
            maxm = max(maxm,cnt)
            cnt = 0
            N >>= 1

    return maxm

# Driver Code
N = 14
print(maxZeros(N))

# This code is written by Shrikant13
```

## C#

```
// C# code to determine Length of
// longest consecutive zeroes in the
// binary representation of a number.
using System;

class GFG
{
static int maxZeros(int N)
{
    // variable to store the length
    // of longest consecutive 0's
    int maxm = -1;

    // to temporary store the
    // consecutive 0's
    int cnt = 0;

    while (N != 0)
    {
        if ((N & 1) == 0 )
        {
            cnt++;
            N >>= 1;
            maxm = Math.Max(maxm, cnt);
        }
        else
        {
            maxm = Math.Max(maxm, cnt);
            cnt = 0;
            N >>= 1;
        }
    }
    return maxm;
}

// Driver code
public static void Main()
{
    int N = 14;
    Console.WriteLine(maxZeros(N));
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to determine Length of
// longest consecutive zeroes in the
// binary representation of a number.
function maxZeros($N)
{
    // variable to store the length
    // of longest consecutive 0's
    $maxm = -1;

    // to temporary store the
    // of consecutive 0's
    $cnt = 0;

    while ($N)
    {
        if (!($N & 1))
        {
            $cnt++;
            $N >>= 1;
            $maxm = max($maxm, $cnt);
        }
        else
        {
            $maxm = max($maxm, $cnt);
            $cnt = 0;
            $N >>= 1;
        }
    }
    return $maxm;
}

// Driver code
$N = 14;
echo (maxZeros($N));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript code to determine Length of
    // longest consecutive zeroes in the
    // binary representation of a number.

    function maxZeros(N)
    {
        // variable to store the length
        // of longest consecutive 0's
        let maxm = -1;

        // to temporary store the
        // consecutive 0's
        let cnt = 0;

        while (N != 0)
        {
            if ((N & 1) == 0 )
            {
                cnt++;
                N >>= 1;
                maxm = Math.max(maxm, cnt);
            }
            else
            {
                maxm = Math.max(maxm, cnt);
                cnt = 0;
                N >>= 1;
            }
        }
        return maxm;
    }

    let N = 14;
    document.write(maxZeros(N));

</script>
```

**Output:** 

```
1
```