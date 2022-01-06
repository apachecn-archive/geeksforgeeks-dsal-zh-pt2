# n 个范围内出现的最大整数| Set-2

> 原文:[https://www . geesforgeks . org/maximum-increated-整数 in-n-ranges-set-2/](https://www.geeksforgeeks.org/maximum-occurred-integer-in-n-ranges-set-2/)

给定 N 个范围的左-右。任务是打印在给定范围内出现次数最多的数字。
**注:**1<= L<= R<= 10<sup>6</sup>T5**例:**

> **输入:**范围[] = { {1，6}、{2，3}、{2，5}、{3，8} }
> 输出: 3
> 1 出现在 1 范围内{1，6}
> 2 出现在 3 范围内{1，6}、{2，3}、{2，5}
> 3 出现在 4 范围内{1，6}、{2，3}、{2，5}、{3，8}
> 4 出现在 3 范围内 8}
> 6 在 2 个范围{1，6}中出现 2 个，{3，8}
> 7 在 1 个范围{3，8}中出现 1 个
> 8 在 1 个范围{3，8}
> **中出现 1 个输入:**范围[] = { {1，4}，{1，9}，{1，2 } }；
> **输出:** 1

**逼近:**逼近类似于[n 范围内最大出现整数](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)。唯一不同的是找到范围的下限和上限。所以不需要从 1 遍历到 MAX。
下面是解决这个问题的分步算法:

1.  用 0 初始化一个 freq 数组，让数组的大小为 10^6，因为这是最大可能值。
2.  对于给定范围的每个起始指数，将*频率[l]增加 1* 。
3.  对于给定范围的每个结束指数，将*频率[r+1]减少 1* 。
4.  从最小 L 迭代到最大 R，将频率相加 **freq[i] += freq[i-1]** 。
5.  最大值为 freq[i]的指数将是答案。
6.  存储索引并返回。

以下是上述方法的实现:

## C++

```
// C++ program to check the most occurring
// element in given range
#include <bits/stdc++.h>
using namespace std;

// Function that returns the maximum element.
int maxOccurring(int range[][2], int n)
{

    // freq array to store the frequency
    int freq[(int)(1e6 + 2)] = { 0 };

    int first = 0, last = 0;

    // iterate and mark the hash array
    for (int i = 0; i < n; i++) {
        int l = range[i][0];
        int r = range[i][1];

        // increase the hash array by 1 at L
        freq[l] += 1;

        // Decrease the hash array by 1 at R
        freq[r + 1] -= 1;

        first = min(first, l);
        last = max(last, r);
    }

    // stores the maximum frequency
    int maximum = 0;
    int element = 0;

    // check for the most occurring element
    for (int i = first; i <= last; i++) {

        // increase the frequency
        freq[i] = freq[i - 1] + freq[i];

        // check if is more than the previous one
        if (freq[i] > maximum) {
            maximum = freq[i];
            element = i;
        }
    }

    return element;
}

// Driver code
int main()
{
    int range[][2] = { { 1, 6 }, { 2, 3 }, { 2, 5 }, { 3, 8 } };
    int n = 4;

    // function call
    cout << maxOccurring(range, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check the most occurring
// element in given range
class GFG
{

// Function that returns the maximum element.
static int maxOccurring(int range[][], int n)
{

    // freq array to store the frequency
    int []freq = new int[(int)(1e6 + 2)];

    int first = 0, last = 0;

    // iterate and mark the hash array
    for (int i = 0; i < n; i++)
    {
        int l = range[i][0];
        int r = range[i][1];

        // increase the hash array by 1 at L
        freq[l] += 1;

        // Decrease the hash array by 1 at R
        freq[r + 1] -= 1;

        first = Math.min(first, l);
        last = Math.max(last, r);
    }

    // stores the maximum frequency
    int maximum = 0;
    int element = 0;

    // check for the most occurring element
    for (int i = first+1; i <= last; i++)
    {

        // increase the frequency
        freq[i] = freq[i - 1] + freq[i];

        // check if is more than the previous one
        if (freq[i] > maximum)
        {
            maximum = freq[i];
            element = i;
        }
    }
    return element;
}

// Driver code
public static void main(String[] args)
{
    int range[][] = { { 1, 6 }, { 2, 3 },
                      { 2, 5 }, { 3, 8 } };
    int n = 4;

    // function call
    System.out.println(maxOccurring(range, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to check the most
# occurring element in given range

# Function that returns the
# maximum element.
def maxOccurring(range1, n):

    # freq array to store the frequency
    freq = [0] * 1000002;

    first = 0;
    last = 0;

    # iterate and mark the hash array
    for i in range(n):
        l = range1[i][0];
        r = range1[i][1];

        # increase the hash array by 1 at L
        freq[l] += 1;

        # Decrease the hash array by 1 at R
        freq[r + 1] -= 1;
        first = min(first, l);
        last = max(last, r);

    # stores the maximum frequency
    maximum = 0;
    element = 0;

    # check for the most occurring element
    for i in range(first, last + 1):

        # increase the frequency
        freq[i] = freq[i - 1] + freq[i];

        # check if is more than the
        # previous one
        if(freq[i] > maximum):
            maximum = freq[i];
            element = i;
    return element;

# Driver code
range1= [[ 1, 6 ], [ 2, 3 ],
         [ 2, 5 ], [ 3, 8 ]];
n = 4;

# function call
print(maxOccurring(range1, n));

# This code is contributed by mits
```

## C#

```
// C# program to check the most occurring
// element in given range
using System;

class GFG
{

// Function that returns the maximum element.
static int maxOccurring(int [,]range, int n)
{

    // freq array to store the frequency
    int []freq = new int[(int)(1e6 + 2)];

    int first = 0, last = 0;

    // iterate and mark the hash array
    for (int i = 0; i < n; i++)
    {
        int l = range[i, 0];
        int r = range[i, 1];

        // increase the hash array by 1 at L
        freq[l] += 1;

        // Decrease the hash array by 1 at R
        freq[r + 1] -= 1;

        first = Math.Min(first, l);
        last = Math.Max(last, r);
    }

    // stores the maximum frequency
    int maximum = 0;
    int element = 0;

    // check for the most occurring element
    for (int i = first + 1; i <= last; i++)
    {

        // increase the frequency
        freq[i] = freq[i - 1] + freq[i];

        // check if is more than the previous one
        if (freq[i] > maximum)
        {
            maximum = freq[i];
            element = i;
        }
    }
    return element;
}

// Driver code
public static void Main(String[] args)
{
    int [,]range = {{ 1, 6 }, { 2, 3 },
                    { 2, 5 }, { 3, 8 }};
    int n = 4;

    // function call
    Console.WriteLine(maxOccurring(range, n));
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check the most occurring
// element in given range

// Function that returns the maximum element.
function maxOccurring(&$range, $n)
{
    // freq array to store the frequency
    $freq = array(0, 1000002, NULL);

    $first = 0;
    $last = 0;

    // iterate and mark the hash array
    for ($i = 0; $i < $n; $i++)
    {
        $l = $range[$i][0];
        $r = $range[$i][1];

        // increase the hash array
        // by 1 at L
        $freq[$l] += 1;

        // Decrease the hash array
        // by 1 at R
        $freq[$r + 1] -= 1;

        $first = min($first, $l);
        $last = max($last, $r);
    }

    // stores the maximum frequency
    $maximum = 0;
    $element = 0;

    // check for the most occurring element
    for ($i = $first; $i <= $last; $i++)
    {

        // increase the frequency
        $freq[$i] = $freq[$i - 1] + $freq[$i];

        // check if is more than the
        // previous one
        if ($freq[$i] > $maximum)
        {
            $maximum = $freq[$i];
            $element = $i;
        }
    }

    return $element;
}

// Driver code
$range = array(array( 1, 6 ),
               array( 2, 3 ),
               array( 2, 5 ),
               array( 3, 8 ));
$n = 4;

// function call
echo maxOccurring($range, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to check the most occurring
// element in given range   

// Function that returns the maximum element.
    function maxOccurring(range , n)
    {

        // freq array to store the frequency
        var freq = Array(parseInt(1e6 + 2)).fill(0);

        var first = 0, last = 0;

        // iterate and mark the hash array
        for (i = 0; i < n; i++) {
            var l = range[i][0];
            var r = range[i][1];

            // increase the hash array by 1 at L
            freq[l] += 1;

            // Decrease the hash array by 1 at R
            freq[r + 1] -= 1;

            first = Math.min(first, l);
            last = Math.max(last, r);
        }

        // stores the maximum frequency
        var maximum = 0;
        var element = 0;

        // check for the most occurring element
        for (i = first + 1; i <= last; i++) {

            // increase the frequency
            freq[i] = freq[i - 1] + freq[i];

            // check if is more than the previous one
            if (freq[i] > maximum) {
                maximum = freq[i];
                element = i;
            }
        }
        return element;
    }

    // Driver code

        var range = [ [ 1, 6 ], [ 2, 3 ],
                      [ 2, 5 ], [ 3, 8 ] ];
        var n = 4;

        // function call
        document.write(maxOccurring(range, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
3
```

**注意:如果 L 和 T 的值是 10 <sup>8</sup> 的数量级，那么上述方法将不起作用，因为会出现内存错误。对于这些限制，我们需要一种不同但相似的方法。你可以从散列的角度来考虑。**