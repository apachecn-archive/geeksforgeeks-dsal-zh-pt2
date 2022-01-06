# 只有非零数字的范围内的数字计数，这些数字的总和为 N，并且数字可被 M 整除

> 原文:[https://www . geesforgeks . org/范围之间的数字计数只有非零数字，其数字总和为 n，并且数字可被 m 整除/](https://www.geeksforgeeks.org/count-of-numbers-between-range-having-only-non-zero-digits-whose-sum-of-digits-is-n-and-number-is-divisible-by-m/)

给定一个范围**【L，R】**和两个正整数 **N** 和 **M** 。任务是统计仅包含非零数字的范围内的数字，这些数字的**位数和等于 N** ，**数可被 M** 整除。
**举例:**

> **输入:** L = 1，R = 100，N = 8，M = 2
> **输出:** 4
> 只有 8，26，44 和 62 是有效数字
> **输入:** L = 1，R = 200，N = 4，M = 11
> **输出:** 2
> 只有 22 和 121 是有效数字

**先决条件:** [数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)

**方法:**首先，如果我们能够将所需的数字计数到 R，即在[0，R]的范围内，我们可以通过从 0 到 R 求解，然后减去从 0 到 L–1 求解后得到的答案，很容易地得出我们在[L，R]范围内的答案。现在，我们需要定义 DP 状态。
T3【DP 州】T4:

*   因为我们可以把我们的数字看作一个数字序列，一个状态是我们当前所处的**位置**。如果我们处理的数字高达 10 <sup>18</sup> ，则该位置的值可以从 0 到 18。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第二种状态是我们到目前为止放置的数字的**和**。
*   第三种状态是**余数**，它定义了我们到目前为止以 m 为模的数的模
*   另一个状态是布尔变量**紧密**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数。

对于只有非零数字的号码，我们维护一个变量 **nonz** ，它的值如果为 1，则表明我们已拨号码的第一个数字是非零数字，因此，现在我们不能在即将到来的呼叫中拨任何零数字。否则，我们可以将一个零位数作为前导零，使当前数字的位数小于上限的位数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int M = 20;

// states - position, sum, rem, tight
// sum can have values upto 162, if we
// are dealing with numbers upto 10^18
// when all 18 digits are 9, then sum
// is 18 * 9 = 162
int dp[M][165][M][2];

// n is the sum of digits and number should
// be divisible by m
int n, m;

// Function to return the count of
// required numbers from 0 to num
int count(int pos, int sum, int rem, int tight,
          int nonz, vector<int> num)
{
    // Last position
    if (pos == num.size()) {
        if (rem == 0 && sum == n)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][sum][rem][tight] != -1)
        return dp[pos][sum][rem][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int d = 0; d <= limit; d++) {

        // If the current digit is zero
        // and nonz is 1, we can't place it
        if (d == 0 && nonz)
            continue;
        int currSum = sum + d;
        int currRem = (rem * 10 + d) % m;
        int currF = tight || (d < num[pos]);
        ans += count(pos + 1, currSum, currRem,
                     currF, nonz || d, num);
    }
    return dp[pos][sum][rem][tight] = ans;
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
    return count(0, 0, 0, 0, 0, num);
}

// Driver code
int main()
{
    int L = 1, R = 100;
    n = 8, m = 2;
    cout << solve(R) - solve(L);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int M = 20;

// states - position, sum, rem, tight
// sum can have values upto 162, if we
// are dealing with numbers upto 10^18
// when all 18 digits are 9, then sum
// is 18 * 9 = 162
static int dp[][][][] = new int [M][165][M][2];

// n is the sum of digits and number should
// be divisible by m
static int n, m;

// Function to return the count of
// required numbers from 0 to num
static int count(int pos, int sum, int rem, int tight,
        int nonz, Vector<Integer> num)
{
    // Last position
    if (pos == num.size())
    {
        if (rem == 0 && sum == n)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][sum][rem][tight] != -1)
        return dp[pos][sum][rem][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight != 0 ? 9 : num.get(pos));

    for (int d = 0; d <= limit; d++)
    {

        // If the current digit is zero
        // and nonz is 1, we can't place it
        if (d == 0 && nonz != 0)
            continue;
        int currSum = sum + d;
        int currRem = (rem * 10 + d) % m;
        int currF = (tight != 0 || (d < num.get(pos))) ? 1 : 0;
        ans += count(pos + 1, currSum, currRem,
                    currF, (nonz != 0 || d != 0) ? 1 : 0, num);
    }
    return dp[pos][sum][rem][tight] = ans;
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
    for(int i = 0; i < M; i++)
        for(int j = 0; j < 165; j++)
            for(int k = 0; k < M; k++)
                for(int l = 0; l < 2; l++)
                    dp[i][j][k][l]=-1;

    return count(0, 0, 0, 0, 0, num);
}

// Driver code
public static void main(String args[])
{
    int L = 1, R = 100;
    n = 8; m = 2;
    System.out.print( solve(R) - solve(L));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# required numbers from 0 to num
def count(pos, Sum, rem, tight, nonz, num):

    # Last position
    if pos == len(num):
        if rem == 0 and Sum == n:
            return 1
        return 0

    # If this result is already computed
    # simply return it
    if dp[pos][Sum][rem][tight] != -1:
        return dp[pos][Sum][rem][tight]

    ans = 0

    # Maximum limit upto which we can place
    # digit. If tight is 1, means number has
    # already become smaller so we can place
    # any digit, otherwise num[pos]
    if tight:
        limit = 9
    else:
        limit = num[pos]

    for d in range(0, limit + 1):

        # If the current digit is zero
        # and nonz is 1, we can't place it
        if d == 0 and nonz:
            continue

        currSum = Sum + d
        currRem = (rem * 10 + d) % m
        currF = int(tight or (d < num[pos]))
        ans += count(pos + 1, currSum, currRem,
                     currF, nonz or d, num)

    dp[pos][Sum][rem][tight] = ans
    return ans

# Function to convert x into its digit
# vector and uses count() function to
# return the required count
def solve(x):

    num = []
    global dp

    while x > 0:
        num.append(x % 10)
        x //= 10

    num.reverse()

    # Initialize dp
    dp = [[[[-1, -1] for i in range(M)]
                     for j in range(165)]
                     for k in range(M)]
    return count(0, 0, 0, 0, 0, num)

# Driver code
if __name__ == "__main__":

    L, R = 1, 100

    # n is the sum of digits and number
    # should be divisible by m
    n, m, M = 8, 2, 20

    # States - position, sum, rem, tight
    # sum can have values upto 162, if we
    # are dealing with numbers upto 10^18
    # when all 18 digits are 9, then sum
    # is 18 * 9 = 162
    dp = []

    print(solve(R) - solve(L))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int M = 20;

// states - position, sum, rem, tight
// sum can have values upto 162, if we
// are dealing with numbers upto 10^18
// when all 18 digits are 9, then sum
// is 18 * 9 = 162
static int [,,,]dp = new int [M, 165, M, 2];

// n is the sum of digits and number should
// be divisible by m
static int n, m;

// Function to return the count of
// required numbers from 0 to num
static int count(int pos, int sum, int rem, int tight,
                            int nonz, List<int> num)
{
    // Last position
    if (pos == num.Count)
    {
        if (rem == 0 && sum == n)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos,sum,rem,tight] != -1)
        return dp[pos,sum,rem,tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight != 0 ? 9 : num[pos]);

    for (int d = 0; d <= limit; d++)
    {

        // If the current digit is zero
        // and nonz is 1, we can't place it
        if (d == 0 && nonz != 0)
            continue;
        int currSum = sum + d;
        int currRem = (rem * 10 + d) % m;
        int currF = (tight != 0 || (d < num[pos])) ? 1 : 0;
        ans += count(pos + 1, currSum, currRem,
                    currF, (nonz != 0 || d != 0) ? 1 : 0, num);
    }
    return dp[pos, sum, rem, tight] = ans;
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
    for(int i = 0; i < M; i++)
        for(int j = 0; j < 165; j++)
            for(int k = 0; k < M; k++)
                for(int l = 0; l < 2; l++)
                    dp[i, j, k, l] = -1;

    return count(0, 0, 0, 0, 0, num);
}

// Driver code
public static void Main(String []args)
{
    int L = 1, R = 100;
    n = 8; m = 2;
    Console.Write( solve(R) - solve(L));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

var M = 20;

// states - position, sum, rem, tight
// sum can have values upto 162, if we
// are dealing with numbers upto 10^18
// when all 18 digits are 9, then sum
// is 18 * 9 = 162
var dp = Array.from(Array(M), ()=>Array(165));

// n is the sum of digits and number should
// be divisible by m
var n, m;

// Function to return the count of
// required numbers from 0 to num
function count( pos, sum, rem, tight, nonz, num)
{
    // Last position
    if (pos == num.length) {
        if (rem == 0 && sum == n)
            return 1;
        return 0;
    }
    // If this result is already computed
    // simply return it
    if (dp[pos][sum][rem][tight] != -1)
        return dp[pos][sum][rem][tight];

    var ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    var limit = (tight ? 9 : num[pos]);

    for (var d = 0; d <= limit; d++) {

        // If the current digit is zero
        // and nonz is 1, we can't place it
        if (d == 0 && nonz)
            continue;
        var currSum = sum + d;
        var currRem = (rem * 10 + d) % m;
        var currF = (tight != 0 || (d < num[pos])) ? 1 : 0;
        ans += count(pos + 1, currSum, currRem,
                    currF, (nonz != 0 || d != 0) ? 1 : 0, num);
    }
    dp[pos][sum][rem][tight] = ans;
    return ans;
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
        for(var j =0; j<165; j++)
            dp[i][j] = Array.from(Array(M), ()=>Array(2).fill(-1));
    return count(0, 0, 0, 0, 0, num);
}

// Driver code
var L = 1, R = 100;
n = 8, m = 2;
document.write( solve(R) - solve(L));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(M * M)
T3】辅助空间: O(M*M)

**短 Python 实现:**

## 蟒蛇 3

```
# User Input
l, r, n, m = 1, 100, 8, 2

# Initialize Result
output = []

# Traverse through all numbers
for x in range(l, r+1):

    # Check for all conditions in every number
    if sum([int(k) for k in str(x)]) == n and x % m == 0 and '0' not in str(x): # Check conditions
        output.append(x)

print(len(output)) 

# This code is contributed by mailprakashindia
```