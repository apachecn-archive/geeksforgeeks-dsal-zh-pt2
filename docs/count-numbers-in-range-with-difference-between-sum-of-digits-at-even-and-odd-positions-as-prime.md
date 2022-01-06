# 将偶数和奇数位置的数字之和之差的范围内的数字计为质数

> 原文:[https://www . geeksforgeeks . org/count-在偶数和奇数位置的数字总和与素数之差范围内的数字/](https://www.geeksforgeeks.org/count-numbers-in-range-with-difference-between-sum-of-digits-at-even-and-odd-positions-as-prime/)

给定一个范围**【L，R】**。任务是计算在偶数位置的数字和与奇数位置的数字和之差的范围内的数字是素数。将数字中最低有效数字的位置视为奇数位置。
**例:**

```
Input : L = 1, R = 50
Output : 6
Explanation : Only, 20, 30, 31, 41, 
42 and 50 are valid numbers. 

Input : L = 50, R = 100
Output : 18
```

**先决条件:** [数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)
**方法:**首先，如果我们能够将所需的数字计数到 R，即在[0，R]范围内，我们可以通过从 0 到 R 求解，然后减去从 0 到 L–1 求解后得到的答案，轻松得出我们在[L，R]范围内的答案。现在，我们需要定义 DP 状态。
**DP 状态:**

*   因为我们可以把我们的数字看作一个数字序列，一个状态是我们当前所处的**位置**。如果我们处理的数字高达 10 <sup>18</sup> ，则该位置的值可以从 0 到 18。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第一个状态是我们到目前为止在**甚至**位置的数字的**和**。
*   第二种状态是到目前为止我们已经放置的奇数**位置的数字的**和**。**
*   另一个状态是布尔变量**紧密**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数。

同样，当我们达到基本条件时，我们需要检查所需的差是否是素数。由于范围内的最大数是 10 <sup>18</sup> ，偶数或奇数位置的最大和最大为 9 乘以 9，因此最大差为 9。所以，我们只需要在基本条件下检查 100 以内的素数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

const int M = 18;
int a, b, dp[M][90][90][2];

// Prime numbers upto 100
int prime[] = { 2, 3, 5, 7, 11, 13, 17, 19, 23,
                29, 31, 37, 43, 47, 53, 59, 61,
                67, 71, 73, 79, 83, 89, 97 };

// Function to return the count of
// required numbers from 0 to num
int count(int pos, int even, int odd, int tight,
        vector<int> num)
{
    // Base Case
    if (pos == num.size()) {
        if (num.size() & 1)
            swap(odd, even);
        int d = even - odd;

        // check if the difference is equal
        // to any prime number
        for (int i = 0; i < 24; i++)
            if (d == prime[i])
                return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][even][odd][tight] != -1)
        return dp[pos][even][odd][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int d = 0; d <= limit; d++) {
        int currF = tight, currEven = even;
        int currOdd = odd;

        if (d < num[pos])
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if (pos & 1)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1, currEven, currOdd,
                    currF, num);
    }

    return dp[pos][even][odd][tight] = ans;
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
    return count(0, 0, 0, 0, num);
}

// Driver Code
int main()
{
    int L = 1, R = 50;
    cout << solve(R) - solve(L - 1) << endl;

    L = 50, R = 100;
    cout << solve(R) - solve(L - 1) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

static int M = 18;
static int a, b, dp[][][][] = new int[M][90][90][2];

// Prime numbers upto 100
static int prime[] = { 2, 3, 5, 7, 11, 13, 17, 19, 23,
                29, 31, 37, 43, 47, 53, 59, 61,
                67, 71, 73, 79, 83, 89, 97 };

// Function to return the count of
// required numbers from 0 to num
static int count(int pos, int even, int odd, int tight,
        Vector<Integer> num)
{
    // Base Case
    if (pos == num.size())
    {
        if ((num.size() & 1) != 0)
        {
            int t = odd;
            odd = even;
            even = t;

        }
        int d = even - odd;

        // check if the difference is equal
        // to any prime number
        for (int i = 0; i < 24; i++)
            if (d == prime[i])
                return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][even][odd][tight] != -1)
        return dp[pos][even][odd][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight != 0 ? 9 : num.get(pos));

    for (int d = 0; d <= limit; d++)
    {
        int currF = tight, currEven = even;
        int currOdd = odd;

        if (d < num.get(pos))
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if ((pos & 1) != 0)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1, currEven, currOdd,
                    currF, num);
    }

    return dp[pos][even][odd][tight] = ans;
}

// Function to convert x into its digit vector
// and uses count() function to return the
// required count
static int solve(int x)
{
    Vector<Integer> num = new Vector<Integer>();

    while (x != 0)
    {
        num.add(x % 10);
        x /= 10;
    }

    Collections.reverse(num);

    // Initialize dp
    for(int i = 0; i < dp.length; i++)
        for(int j = 0; j < dp[i].length; j++)
            for(int k = 0; k < dp[i][j].length; k++)
                for(int k1 = 0; k1 < dp[i][j][k].length; k1++)
                    dp[i][j][k][k1] = -1;

    return count(0, 0, 0, 0, num);
}

// Driver Code
public static void main(String args[])
{
    int L = 1, R = 50;
    System.out.println( solve(R) - solve(L - 1));

    L = 50; R = 100;
    System.out.println( solve(R) - solve(L - 1));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the above approach

M = 18

# Prime numbers upto 100
prime = [ 2, 3, 5, 7, 11, 13, 17, 19, 23,
        29, 31, 37, 43, 47, 53, 59, 61,
        67, 71, 73, 79, 83, 89, 97 ]

# Function to return the count of
# required numbers from 0 to num
def count(pos, even, odd, tight, num):

    # Base Case
    if pos == len(num):
        if len(num) & 1:
            odd, even = even, odd

        d = even - odd

        # check if the difference is equal
        # to any prime number
        for i in range(24):
            if d == prime[i]:
                return 1
        return 0

    # If this result is already computed
    # simply return it
    if dp[pos][even][odd][tight] != -1:
        return dp[pos][even][odd][tight]

    ans = 0

    # Maximum limit upto which we can place
    # digit. If tight is 1, means number has
    # already become smaller so we can place
    # any digit, otherwise num[pos]
    limit = 9 if tight else num[pos]

    for d in range(limit + 1):
        currF = tight
        currEven = even
        currOdd = odd

        if d < num[pos]:
            currF = 1

        # If the current position is odd
        # add it to currOdd, otherwise to
        # currEven
        if pos & 1:
            currOdd += d
        else:
            currEven += d

        ans += count(pos + 1, currEven, currOdd, currF, num)

    dp[pos][even][odd][tight] = ans
    return dp[pos][even][odd][tight]

# Function to convert x into its digit vector
# and uses count() function to return the
# required count
def solve(x):
    global dp
    num = []
    while x:
        num.append(x % 10)
        x //= 10

    num.reverse()

    # Initialize dp
    dp = [[[[-1, -1] for i in range(90)]
            for j in range(90)] for k in range(M)]
    return count(0, 0, 0, 0, num)

# Driver Code
if __name__ == "__main__":
    dp = []

    L = 1
    R = 50
    print(solve(R) - solve(L - 1))

    L = 50
    R = 100
    print(solve(R) - solve(L - 1))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{
static int M = 18;
static int a, b;
static int [,,,]dp = new int[M, 90, 90, 2];

// Prime numbers upto 100
static int []prime = { 2, 3, 5, 7, 11, 13, 17, 19, 23,
                       29, 31, 37, 43, 47, 53, 59, 61,
                       67, 71, 73, 79, 83, 89, 97 };

// Function to return the count of
// required numbers from 0 to num
static int count(int pos, int even,
                 int odd, int tight,
                 List<int> num)
{
    // Base Case
    if (pos == num.Count)
    {
        if ((num.Count & 1) != 0)
        {
            int t = odd;
            odd = even;
            even = t;

        }

        int d = even - odd;

        // check if the difference is equal
        // to any prime number
        for (int i = 0; i < 24; i++)
            if (d == prime[i])
                return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos, even, odd, tight] != -1)
        return dp[pos, even, odd, tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight != 0 ? 9 : num[pos]);

    for (int d = 0; d <= limit; d++)
    {
        int currF = tight, currEven = even;
        int currOdd = odd;

        if (d < num[pos])
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if ((pos & 1) != 0)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1, currEven,
                     currOdd, currF, num);
    }

    return dp[pos, even, odd, tight] = ans;
}

// Function to convert x into its digit vector
// and uses count() function to return the
// required count
static int solve(int x)
{
    List<int> num = new List<int>();

    while (x != 0)
    {
        num.Add(x % 10);
        x /= 10;
    }

    num.Reverse();

    // Initialize dp
    for(int i = 0; i < dp.GetLength(0); i++)
        for(int j = 0; j < dp.GetLength(1); j++)
            for(int k = 0; k < dp.GetLength(2); k++)
                for(int k1 = 0; k1 < dp.GetLength(3); k1++)
                    dp[i, j, k, k1] = -1;

    return count(0, 0, 0, 0, num);
}

// Driver Code
public static void Main(String []args)
{
    int L = 1, R = 50;
    Console.WriteLine(solve(R) - solve(L - 1));

    L = 50; R = 100;
    Console.WriteLine(solve(R) - solve(L - 1));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
var M = 18;
var a, b;
var dp = Array.from(Array(M), ()=>Array(90));

// Prime numbers upto 100
var prime = [2, 3, 5, 7, 11, 13, 17, 19, 23,
                29, 31, 37, 43, 47, 53, 59, 61,
                67, 71, 73, 79, 83, 89, 97 ];

// Function to return the count of
// required numbers from 0 to num
function count(pos, even, odd, tight, num)
{
    // Base Case
    if (pos == num.length) {
        if (num.length & 1)
            [odd, even] = [even, odd]
        var d = even - odd;

        // check if the difference is equal
        // to any prime number
        for (var i = 0; i < 24; i++)
            if (d == prime[i])
                return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][even][odd][tight] != -1)
        return dp[pos][even][odd][tight];

    var ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    var limit = (tight ? 9 : num[pos]);

    for (var d = 0; d <= limit; d++) {
        var currF = tight, currEven = even;
        var currOdd = odd;

        if (d < num[pos])
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if (pos & 1)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1, currEven, currOdd,
                    currF, num);
    }

    return dp[pos][even][odd][tight] = ans;
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

    // Initialize dp
    for(var i =0; i<M; i++)
        for(var j =0; j<90; j++)
            dp[i][j] = Array.from(Array(90),  ()=>Array(2).fill(-1))
    return count(0, 0, 0, 0, num);
}

// Driver Code
var L = 1, R = 50;
document.write( solve(R) - solve(L - 1) + "<br>");
L = 50, R = 100;
document.write( solve(R) - solve(L - 1));

</script>
```

**Output**

```
6
18
```

**时间复杂度:**O(pos *限制)

**辅助空间:** O(M*90*90*2)