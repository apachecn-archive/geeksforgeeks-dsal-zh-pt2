# 两个数字的最大和最小和，数字替换

> 原文:[https://www . geeksforgeeks . org/最大-最小-总和-两位数-数字-替换/](https://www.geeksforgeeks.org/maximum-minimum-sums-two-numbers-digit-replacements/)

给定两个正数，计算两个数的最小和最大可能和。在给定的数字中，我们可以用数字 6 替换数字 5，反之亦然。
**例:**

```
Input  : x1 = 645 x2 = 666
Output : Minimum Sum: 1100 (545 + 555)
         Maximum Sum: 1312 (646 + 666)

Input: x1 = 5466 x2 = 4555
Output: Minimum sum: 10010
        Maximum Sum: 11132
```

因为两个数都是正的，所以如果把两个数中的 5 换成 6，我们总是得到最大和。如果我们用两个数字中的 5 代替 6，我们得到一个最小和。下面是基于这个事实的 C++实现。

## C++

```
// C++ program to find maximum and minimum
// possible sums of two numbers that we can
// get if replacing digit from 5 to 6 and vice
// versa are allowed.
#include<bits/stdc++.h>
using namespace std;

// Find new value of x after replacing digit
// "from" to "to"
int replaceDig(int x, int from, int to)
{
    int result = 0;
    int multiply = 1;

    while (x > 0)
    {
        int reminder = x % 10;

        // Required digit found, replace it
        if (reminder == from)
            result = result + to * multiply;

        else
            result = result + reminder * multiply;

        multiply *= 10;
        x = x / 10;
    }
    return result;
}

// Returns maximum and minimum possible sums of
// x1 and x2 if digit replacements are allowed.
void calculateMinMaxSum(int x1, int x2)
{
    // We always get minimum sum if we replace
    // 6 with 5.
    int minSum = replaceDig(x1, 6, 5) +
                 replaceDig(x2, 6, 5);

    // We always get maximum sum if we replace
    // 5 with 6.
    int maxSum = replaceDig(x1, 5, 6) +
                 replaceDig(x2, 5, 6);
    cout << "Minimum sum = " << minSum;
    cout << "nMaximum sum = " << maxSum;
}

// Driver code
int main()
{
    int x1 = 5466, x2 = 4555;
    calculateMinMaxSum(x1, x2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum and minimum
// possible sums of two numbers that we can
// get if replacing digit from 5 to 6 and vice
// versa are allowed.
class GFG {

    // Find new value of x after replacing digit
    // "from" to "to"
    static int replaceDig(int x, int from, int to)
    {

        int result = 0;
        int multiply = 1;

        while (x > 0)
        {
            int reminder = x % 10;

            // Required digit found, replace it
            if (reminder == from)
                result = result + to * multiply;

            else
                result = result + reminder * multiply;

            multiply *= 10;
            x = x / 10;
        }
        return result;
    }

    // Returns maximum and minimum possible sums of
    // x1 and x2 if digit replacements are allowed.
    static void calculateMinMaxSum(int x1, int x2)
    {

        // We always get minimum sum if we replace
        // 6 with 5.
        int minSum = replaceDig(x1, 6, 5) +
                    replaceDig(x2, 6, 5);

        // We always get maximum sum if we replace
        // 5 with 6.
        int maxSum = replaceDig(x1, 5, 6) +
                    replaceDig(x2, 5, 6);
        System.out.print("Minimum sum = " + minSum);
        System.out.print("\nMaximum sum = " + maxSum);
    }

    // Driver code
    public static void main (String[] args)
    {
        int x1 = 5466, x2 = 4555;
        calculateMinMaxSum(x1, x2);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# and minimum possible sums of
# two numbers that we can get if
# replacing digit from 5 to 6
# and vice versa are allowed.

# Find new value of x after
# replacing digit "from" to "to"
def replaceDig(x, from1, to):
    result = 0
    multiply = 1

    while (x > 0):
        reminder = x % 10

        # Required digit found,
        # replace it
        if (reminder == from1):
            result = result + to * multiply

        else:
            result = result + reminder * multiply

        multiply *= 10
        x = int(x / 10)
    return result

# Returns maximum and minimum
# possible sums of x1 and x2
# if digit replacements are allowed.
def calculateMinMaxSum(x1, x2):

    # We always get minimum sum
    # if we replace 6 with 5.
    minSum = replaceDig(x1, 6, 5) +replaceDig(x2, 6, 5)

    # We always get maximum sum
    # if we replace 5 with 6.
    maxSum = replaceDig(x1, 5, 6) +replaceDig(x2, 5, 6)
    print("Minimum sum =" , minSum)
    print("Maximum sum =" , maxSum,end=" ")

# Driver code
if __name__=='__main__':
    x1 = 5466
    x2 = 4555
    calculateMinMaxSum(x1, x2)

# This code is contributed
# by mits
```

## C#

```
// C# program to find maximum and minimum
// possible sums of two numbers that we can
// get if replacing digit from 5 to 6 and vice
// versa are allowed.
using System;

class GFG {

    // Find new value of x after
    // replacing digit "from" to "to"
    static int replaceDig(int x, int from,
                                 int to)
    {
        int result = 0;
        int multiply = 1;

        while (x > 0)
        {
            int reminder = x % 10;

            // Required digit found,
            // replace it
            if (reminder == from)
                result = result + to * multiply;

            else
                result = result + reminder * multiply;

            multiply *= 10;
            x = x / 10;
        }
        return result;
    }

    // Returns maximum and minimum
    // possible sums of x1 and x2
    // if digit replacements are allowed.
    static void calculateMinMaxSum(int x1, int x2)
    {

        // We always get minimum sum if
        // we replace 6 with 5.
        int minSum = replaceDig(x1, 6, 5) +
                     replaceDig(x2, 6, 5);

        // We always get maximum sum if
        //  we replace 5 with 6.
        int maxSum = replaceDig(x1, 5, 6) +
                       replaceDig(x2, 5, 6);
        Console.Write("Minimum sum = " + minSum);
        Console.Write("\nMaximum sum = " + maxSum);
    }

    // Driver code
    public static void Main ()
    {
        int x1 = 5466, x2 = 4555;
        calculateMinMaxSum(x1, x2);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// and minimum possible sums of
// two numbers that we can get if
// replacing digit from 5 to 6
// and vice versa are allowed.

// Find new value of x after
// replacing digit "from" to "to"
function replaceDig($x, $from, $to)
{
    $result = 0;
    $multiply = 1;

    while ($x > 0)
    {
        $reminder = $x % 10;

        // Required digit found,
        // replace it
        if ($reminder == $from)
            $result = $result + $to *
                           $multiply;

        else
            $result = $result +
                      $reminder *
                      $multiply;

        $multiply *= 10;
        $x = $x / 10;
    }
    return $result;
}

// Returns maximum and minimum
// possible sums of x1 and x2
// if digit replacements are allowed.
function calculateMinMaxSum($x1, $x2)
{
    // We always get minimum sum
    // if we replace 6 with 5.
$minSum = replaceDig($x1, 6, 5) +
           replaceDig($x2, 6, 5);

    // We always get maximum sum
    // if we replace 5 with 6.
    $maxSum = replaceDig($x1, 5, 6) +
               replaceDig($x2, 5, 6);
    echo "Minimum sum = " , $minSum,"\n";
    echo "Maximum sum = " , $maxSum;
}

// Driver code
$x1 = 5466; $x2 = 4555;
calculateMinMaxSum($x1, $x2);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum and minimum
// possible sums of two numbers that we can
// get if replacing digit from 5 to 6 and vice
// versa are allowed.

// Find new value of x after replacing digit
// "from" to "to"
function replaceDig(x , from , to)
{

    var result = 0;
    var multiply = 1;

    while (x > 0)
    {
        var reminder = x % 10;

        // Required digit found, replace it
        if (reminder == from)
            result = result + to * multiply;

        else
            result = result + reminder * multiply;

        multiply *= 10;
        x = parseInt(x / 10);
    }
    return result;
}

// Returns maximum and minimum possible sums of
// x1 and x2 if digit replacements are allowed.
function calculateMinMaxSum(x1 , x2)
{

    // We always get minimum sum if we replace
    // 6 with 5.
    var minSum = replaceDig(x1, 6, 5) +
                replaceDig(x2, 6, 5);

    // We always get maximum sum if we replace
    // 5 with 6.
    var maxSum = replaceDig(x1, 5, 6) +
                replaceDig(x2, 5, 6);
    document.write("Minimum sum = " + minSum);
    document.write("<br>Maximum sum = " + maxSum);
}

// Driver code
var x1 = 5466, x2 = 4555;
calculateMinMaxSum(x1, x2);

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
Minimum sum = 10010
Maximum sum = 11132
```

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。