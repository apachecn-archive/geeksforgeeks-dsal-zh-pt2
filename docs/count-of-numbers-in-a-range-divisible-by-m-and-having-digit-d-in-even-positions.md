# 可被 m 整除且偶数位置有数字 d 的范围内的数字计数

> 原文:[https://www . geeksforgeeks . org/范围内可被 m 整除且偶数位置有数字 d 的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-in-a-range-divisible-by-m-and-having-digit-d-in-even-positions/)

给定由两个正整数 **l** 和 **r** 以及两个整数 **d** 和 **m** 表示的范围。找出可被 m 整除且在偶数位置有数字 d 的数字的个数。(即数字 d 不应出现在奇数位置)。**注:**数字 l 和 r 的位数相同。

> **例:**
> **输入:** l = 10，r = 99，d = 8，m = 2
> **输出:** 8
> **说明:**有效数字为 18、28、38、48、58、68、78、98。
> 88 不是有效数字，因为 8 也出现在奇数位置。
> **输入:** l = 1000，r = 9999，d = 7，m = 19
> **输出:** 6

**先决条件:** [数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)
**方法:**首先，如果我们能够将所需的数字计数到 R，即在[0，R]范围内，我们可以通过从 0 到 R 求解，然后减去从 0 到 L–1 求解后得到的答案，很容易得出我们在[L，R]范围内的答案。现在，我们需要定义 DP 状态。
**DP 状态:**

*   因为我们可以把我们的数字看作一个数字序列，所以一个状态就是我们当前所处的位置。如果我们处理的数字高达 1018，这个位置可以有从 0 到 18 的值。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第二状态是余数，它定义了我们到目前为止对 m 取模的数的模。
*   另一个状态是布尔变量紧密，它告诉我们试图构建的数字已经变得小于 R，这样在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数。

如果当前位置是偶数位置，我们只需放置数字 d 并递归求解下一个位置。但是如果当前位置是奇数位置，我们可以放置除 d 之外的任何数字，并求解下一个位置。
以下是上述办法的实施情况。

## C++

```
// CPP Program to find the count of
// numbers in a range divisible by m
// having digit d at even positions
#include <bits/stdc++.h>
using namespace std;

const int M = 20;

// states - position, rem, tight
int dp[M][M][2];

// d is required digit and number should
// be divisible by m
int d, m;

// This function returns the count of
// required numbers from 0 to num
int count(int pos, int rem, int tight,
          vector<int> num)
{
    // Last position
    if (pos == num.size()) {
        if (rem == 0)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][rem][tight] != -1)
        return dp[pos][rem][tight];

    // If the current position is even, place
    // digit d, but since we have considered
    // 0-indexing, check for odd positions
    if (pos % 2) {
        if (tight == 0 && d > num[pos])
            return 0;

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (d < num[pos])
            currTight = 1;

        int res = count(pos + 1, (10 * rem + d)
                                     % m,
                        currTight, num);
        return dp[pos][rem][tight] = res;
    }

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int dig = 0; dig <= limit; dig++) {

        if (dig == d)
            continue;

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call, also set nonz
        // to 1 if current digit is non zero
        ans += count(pos + 1, (10 * rem + dig)
                                  % m,
                     currTight, num);
    }
    return dp[pos][rem][tight] = ans;
}

// Function to convert x into its digit vector
// and uses count() function to return the
// required count
int solve(int x)
{
    vector<int> num;
    while (x) {
        num.push_back(x % 10);
        x /= 10;
    }
    reverse(num.begin(), num.end());

    // Initialize dp
    memset(dp, -1, sizeof(dp));
    return count(0, 0, 0, num);
}

// Driver Code to test above functions
int main()
{
    int L = 10, R = 99;
    d = 8, m = 2;
    cout << solve(R) - solve(L) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the count of
// numbers in a range divisible by m
// having digit d at even positions

import java.util.*;

class GFG
{

    static int M = 20;

    // states - position, rem, tight
    static Integer[][][] dp = new Integer[M][M][2];

    // d is required digit and number should
    // be divisible by m
    static int d, m;

    // This function returns the count of
    // required numbers from 0 to num
    static int count(int pos, int rem, int tight,
                            Vector<Integer> num)
    {

        // Last position
        if (pos == num.size())
        {
            if (rem == 0)
                return 1;
            return 0;
        }

        // If this result is already computed
        // simply return it
        if (dp[pos][rem][tight] != -1)
            return dp[pos][rem][tight];

        // If the current position is even, place
        // digit d, but since we have considered
        // 0-indexing, check for odd positions
        if (pos % 2 == 1)
        {
            if (tight == 0 && d > num.elementAt(pos))
                return 0;

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (d < num.elementAt(pos))
                currTight = 1;

            int res = count(pos + 1, (10 * rem + d) % m,
                                        currTight, num);
            return dp[pos][rem][tight] = res;
        }

        int ans = 0;

        // Maximum limit upto which we can place
        // digit. If tight is 1, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = (tight != 0) ? 9 : num.elementAt(pos);
        for (int dig = 0; dig <= limit; dig++)
        {

            if (dig == d)
                continue;

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (dig < num.elementAt(pos))
                currTight = 1;

            // Next recursive call, also set nonz
            // to 1 if current digit is non zero
            ans += count(pos + 1, (10 * rem + dig) % m,
                                        currTight, num);
        }
        return dp[pos][rem][tight] = ans;
    }

    // Function to convert x into its digit vector
    // and uses count() function to return the
    // required count
    static int solve(int x)
    {
        Vector<Integer> num = new Vector<>();
        while (x > 0)
        {
            num.add(x % 10);
            x /= 10;
        }
        Collections.reverse(num);

        // Initialize dp
        for (int i = 0; i < dp.length; i++)
            for (int j = 0; j < dp[i].length; j++)
                for (int k = 0; k < dp[i][j].length; k++)
                    dp[i][j][k] = -1;

        return count(0, 0, 0, num);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int L = 10, R = 99;
        d = 8;
        m = 2;
        System.out.println(solve(R) - solve(L));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 Program to find the count of
# numbers in a range divisible by m
# having digit d at even positions

# This Function returns the count of
# required numbers from 0 to num
def count(pos, rem, tight, num):

    # Last position
    if pos == len(num):
        if rem == 0:
            return 1
        return 0

    # If this result is already
    # computed simply return it
    if dp[pos][rem][tight] != -1:
        return dp[pos][rem][tight]

    # If the current position is even,
    # place digit d, but since we have
    # considered 0-indexing, check for
    # odd positions
    if pos % 2 == 1:
        if tight == 0 and d > num[pos]:
            return 0

        currTight = tight

        # At this position, number
        # becomes smaller
        if d < num[pos]:
            currTight = 1

        res = count(pos + 1, (10 * rem + d) % m,
                                 currTight, num)

        dp[pos][rem][tight] = res        
        return res

    ans = 0

    # Maximum limit upto which we can place
    # digit. If tight is 1, means number has
    # already become smaller so we can place
    # any digit, otherwise num[pos]
    limit = 9 if tight else num[pos]

    for dig in range(0, limit + 1):
        if dig == d:
            continue

        currTight = tight

        # At this position, number becomes
        # smaller
        if dig < num[pos]:
            currTight = 1

        # Next recursive call, also set nonz
        # to 1 if current digit is non zero
        ans += count(pos + 1, (10 * rem + dig) % m,
                                    currTight, num)

    dp[pos][rem][tight] = ans
    return ans

# Function to convert x into its digit
# vector and uses count() function to
# return the required count
def solve(x):

    global dp
    num = []
    while x > 0:
        num.append(x % 10)
        x = x // 10

    num.reverse()
    # Initialize dp with -1
    dp = [[[-1, -1] for x in range(M)]
                    for y in range(M)]

    return count(0, 0, 0, num)

# Driver Code
if __name__ == "__main__":

    L, R = 10, 99

    # d is required digit and number
    # should be divisible by m
    d, m = 8, 2
    M = 20

    # states - position, rem, tight
    dp = []
    print(solve(R) - solve(L))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# Program to find the count of
// numbers in a range divisible by m
// having digit d at even positions
using System;
using System.Collections.Generic;

class GFG
{

    static int M = 20;

    // states - position, rem, tight
    static int[,,] dp = new int[M, M, 2];

    // d is required digit and number should
    // be divisible by m
    static int d, m;

    // This function returns the count of
    // required numbers from 0 to num
    static int count(int pos, int rem, int tight,
                            List<int> num)
    {

        // Last position
        if (pos == num.Count)
        {
            if (rem == 0)
                return 1;
            return 0;
        }

        // If this result is already computed
        // simply return it
        if (dp[pos, rem, tight] != -1)
            return dp[pos, rem, tight];

        // If the current position is even, place
        // digit d, but since we have considered
        // 0-indexing, check for odd positions
        if (pos % 2 == 1)
        {
            if (tight == 0 && d > num[pos])
                return 0;

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (d < num[pos])
                currTight = 1;

            int res = count(pos + 1, (10 * rem + d) % m,
                                        currTight, num);
            return dp[pos, rem, tight] = res;
        }

        int ans = 0;

        // Maximum limit upto which we can place
        // digit. If tight is 1, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = (tight != 0) ? 9 : num[pos];
        for (int dig = 0; dig <= limit; dig++)
        {

            if (dig == d)
                continue;

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (dig < num[pos])
                currTight = 1;

            // Next recursive call, also set nonz
            // to 1 if current digit is non zero
            ans += count(pos + 1, (10 * rem + dig) % m,
                                        currTight, num);
        }
        return dp[pos, rem, tight] = ans;
    }

    // Function to convert x into its digit vector
    // and uses count() function to return the
    // required count
    static int solve(int x)
    {
        List<int> num = new List<int>();
        while (x > 0)
        {
            num.Add(x % 10);
            x /= 10;
        }
        num.Reverse();

        // Initialize dp
        for (int i = 0; i < dp.GetLength(0); i++)
            for (int j = 0; j < dp.GetLength(1); j++)
                for (int k = 0; k < dp.GetLength(2); k++)
                    dp[i, j, k] = -1;

        return count(0, 0, 0, num);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int L = 10, R = 99;
        d = 8;
        m = 2;
        Console.WriteLine(solve(R) - solve(L));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the count of
// numbers in a range divisible by m
// having digit d at even positions

// This function returns the count of
// required numbers from 0 to num
function count_num($pos, $rem, $tight, $num)
{
    // Last position
    if ($pos == sizeof($num))
    {
        if ($rem == 0)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if ( $GLOBALS['dp'][$pos][$rem][$tight] != -1)
        return $GLOBALS['dp'][$pos][$rem][$tight];

    // If the current position is even, place
    // digit d, but since we have considered
    // 0-indexing, check for odd positions
    if ($pos % 2)
    {
        if ($tight == 0 &&
            $GLOBALS['d'] > $num[$pos])
            return 0;

        $currTight = $tight;

        // At this position, number becomes
        // smaller
        if ($GLOBALS['d'] < $num[$pos])
            $currTight = 1;

        $res = count_num($pos + 1, (10 * $rem +
                         $GLOBALS['d']) % $GLOBALS['m'],
                         $currTight, $num);
        return $dp[$pos][$rem][$tight] = $res;
    }

    $ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    $limit = ($tight ? 9 : $num[$pos]);

    for ($dig = 0; $dig <= $limit; $dig++)
    {

        if ($dig == $GLOBALS['d'])
            continue;

        $currTight = $tight;

        // At this position, number becomes
        // smaller
        if ($dig < $num[$pos])
            $currTight = 1;

        // Next recursive call, also set nonz
        // to 1 if current digit is non zero
        $ans += count_num($pos + 1, (10 * $rem + $dig) %
                          $GLOBALS['m'], $currTight, $num);
    }
    return $dp[$pos][$rem][$tight] = $ans;
}

// Function to convert x into its digit
// vector and uses count() function to
// return the required count
function solve($x)
{
    $num = array() ;
    while ($x)
    {
        array_push($num, $x % 10);
        $x = floor($x / 10);
    }
    $num = array_reverse($num) ;

    // Initialize dp
    for($i = 0 ; $i < $GLOBALS['M'] ; $i++)
        for($j = 0; $j < $GLOBALS['M']; $j++)
            for($k = 0; $k < 2; $k ++)
                $GLOBALS['dp'][$i][$j][$k] = -1;

    return count_num(0, 0, 0, $num);
}

// Driver Code
$GLOBALS['M'] = 20;

// states - position, rem, tight
$GLOBALS['dp'] = array(array(array()));

$L = 10;
$R = 99;

// d is required digit and number
// should be divisible by m
$GLOBALS['d'] = 8 ;
$GLOBALS['m'] = 2;

echo solve($R) - solve($L) ;

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find the count of
// numbers in a range divisible by m
// having digit d at even positions

var M = 20;

// states - position, rem, tight
var dp = Array.from(Array(M), ()=> Array(M))

// d is required digit and number should
// be divisible by m
var d, m;

// This function returns the count of
// required numbers from 0 to num
function count(pos, rem, tight, num)
{
    // Last position
    if (pos == num.length) {
        if (rem == 0)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][rem][tight] != -1)
        return dp[pos][rem][tight];

    // If the current position is even, place
    // digit d, but since we have considered
    // 0-indexing, check for odd positions
    if (pos % 2) {
        if (tight == 0 && d > num[pos])
            return 0;

        var currTight = tight;

        // At this position, number becomes
        // smaller
        if (d < num[pos])
            currTight = 1;

        var res = count(pos + 1, (10 * rem + d)
                                     % m,
                        currTight, num);
        return dp[pos][rem][tight] = res;
    }

    var ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    var limit = (tight ? 9 : num[pos]);

    for (var dig = 0; dig <= limit; dig++) {

        if (dig == d)
            continue;

        var currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call, also set nonz
        // to 1 if current digit is non zero
        ans += count(pos + 1, (10 * rem + dig)
                                  % m,
                     currTight, num);
    }
    return dp[pos][rem][tight] = ans;
}

// Function to convert x into its digit vector
// and uses count() function to return the
// required count
function solve(x)
{
    var num = [];
    while (x) {
        num.push(x % 10);
        x = parseInt(x/10);
    }
    num.reverse();
    for(var i =0; i<M; i++)
        for(var j =0; j<M; j++)
            dp[i][j] = new Array(2).fill(-1);
    return count(0, 0, 0, num);
}

// Driver Code to test above functions
var L = 10, R = 99;
d = 8, m = 2;
document.write( solve(R) - solve(L));

</script>
```

**输出:**

```
8
```

**时间复杂度:**O(18 *(m–1)* 2)，如果我们处理的数字是 10 <sup>18</sup>

**辅助空间:** O(m <sup>2</sup>