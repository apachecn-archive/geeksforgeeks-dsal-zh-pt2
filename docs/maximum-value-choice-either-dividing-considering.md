# 最大值，可选择除或按原样考虑

> 原文:[https://www . geesforgeks . org/最大值-选择-非此即彼-考虑/](https://www.geeksforgeeks.org/maximum-value-choice-either-dividing-considering/)

给我们一个数 n，我们需要借助以下函数求最大可能和:
**F(n)= max((F(n/2)+F(n/3)+F(n/4)+F(n/5))、n)** 。为了计算 F(n)，我们可以用 n 作为我们的结果，或者我们可以按照给定的函数定义进一步把 n 分成四部分。我们可以花尽可能多的时间来做这件事。找出你能从给定的 n 中得到的最大可能和。注意:1 不能被进一步分解，所以 F(1) = 1 作为基本情况。

**示例:**

```
Input : n = 10
Output : MaxSum = 12
Explanation: 
f(10) = f(10/2) + f(10/3) + f(10/4) + f(10/5)
      = f(5)  +   f(3)  +  f(2)   +  f(2)
      = 12
5, 3 and 2 cannot be further divided.

Input : n = 2
Output : MaxSum = 2
```

**方法:**这个问题可以用递归方法来解决，但是这将花费我们很高的复杂性，因为它有重叠的子问题。因此，我们应用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)概念，以自下而上的方式解决这个问题，如下所示:

## C++

```
// CPP program for maximize result when
// we have choice to divide or consider
// as it is.
#include <bits/stdc++.h>
using namespace std;

// function for calculating max possible result
int maxDP(int n)
{
    int res[n + 1];
    res[0] = 0;
    res[1] = 1;

    // Compute remaining values in bottom
    // up manner.
    for (int i = 2; i <= n; i++)
        res[i] = max(i, (res[i / 2]
                         + res[i / 3]
                         + res[i / 4]
                         + res[i / 5]));

    return res[n];
}

// Driver Code
int main()
{
    int n = 60;
    cout << "MaxSum =" << maxDP(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximize result when
// we have choice to divide or consider
// as it is.
import java.io.*;

class GFG {

    // function for calculating max
    // possible result
    static int maxDP(int n)
    {
        int res[] = new int[n + 1];
        res[0] = 0;
        res[1] = 1;

        // Compute remaining values in
        // bottom up manner.
        for (int i = 2; i <= n; i++)
            res[i]
                = Math.max(i, (res[i / 2]
                               + res[i / 3]
                               + res[i / 4]
                               + res[i / 5]));

        return res[n];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 60;
        System.out.println("MaxSum = " + maxDP(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 code to maximize result when
# we have choice to divide or consider
# as it is.

# function for calculating max
# possible result
def maxDP (n):
    res = list()
    res.append(0)
    res.append(1)

    # Compute remaining values in
    # bottom up manner.
    i = 2
    while i<n + 1:
        res.append(max(i, (res[int(i / 2)]
                           + res[int(i / 3)] +
                             res[int(i / 4)]
                           + res[int(i / 5)])))
        i = i + 1

    return res[n]

# driver code
n = 60
print("MaxSum =", maxDP(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program for maximize result when
// we have choice to divide or consider
// as it is.
using System;

class GFG {

    // function for calculating max
    // possible result
    static int maxDP(int n)
    {
        int[] res = new int[n + 1];
        res[0] = 0;
        res[1] = 1;

        // Compute remaining values in
        // bottom up manner.
        for (int i = 2; i <= n; i++)
            res[i] = Math.Max(i, (res[i / 2]
                                  + res[i / 3]
                                  + res[i / 4]
                                  + res[i / 5]));

        return res[n];
    }

    // Driver code
    public static void Main()
    {
        int n = 60;
        Console.WriteLine("MaxSum = " + maxDP(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to maximize
// result when we have choice
// to divide or consider as it is.

// function for calculating
// max possible result

function maxDP ($n)
{

    $res[0] = 0;
    $res[1] = 1;

    // Compute remaining values 
    // in bottom up manner.
    for ($i = 2; $i <= $n; $i++)
    $res[$i] = max($i, ($res[$i / 2] +
                        $res[$i / 3] +
                        $res[$i / 4] +
                        $res[$i / 5]));

    return $res[$n];
}

// Driver Code
$n = 60;
echo "MaxSum =", maxDP ($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// javascript program for maximize result when
// we have choice to divide or consider
// as it is.

    // function for calculating max
    // possible result
    function maxDP(n)
    {
        let res = [];

        res[0] = 0;
        res[1] = 1;

        // Compute remaining values in
        // bottom up manner.
        for (let i = 2; i <= n; i++){
            res[i]
                = Math.max(i, (res[Math.floor(i / 2)]
                               + res[Math.floor(i / 3)]
                               + res[Math.floor(i / 4)]
                               + res[Math.floor(i / 5)]));
          }

        return res[n];
    }

// Driver code

    let n = 60;
    document.write("MaxSum = " + maxDP(n));

</script>
```

**Output**

```
MaxSum =106
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)