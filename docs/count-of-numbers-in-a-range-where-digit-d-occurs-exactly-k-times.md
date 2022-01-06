# 数字 d 恰好出现 K 次的范围内的数字计数

> 原文:[https://www . geeksforgeeks . org/范围内数字的计数-数字-d-出现-精确-k-次/](https://www.geeksforgeeks.org/count-of-numbers-in-a-range-where-digit-d-occurs-exactly-k-times/)

给定代表一个范围的两个正整数 **L** 和 **R** 以及另外两个正整数 **d** 和 **K** 。任务是在数字 **d** 恰好出现 **K** 次的范围内找到数字的个数。
**示例:**

> **输入:** L = 11，R = 100，d = 2，k = 1
> **输出:** 17
> 所需数字为 12、20、21、23、24、25、26、27、28、29、32、42、52、62、72、82 和 92。
> **输入:** L = 95，R = 1005，d = 0，k = 2
> **输出:** 14

先决条件:[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)

**方法:**首先，如果我们能够将所需的数字计数到 R，即在[0，R]范围内，我们可以通过从 0 到 R 求解，然后减去从 0 到 L–1 求解后得到的答案，很容易地得出我们在[L，R]范围内的答案。现在，我们需要定义 DP 状态。
T3【DP 州】T4:

*   既然我们可以把我们的数字看作一个数字序列，那么一个状态就是我们当前所处的 ***位置*** 。如果我们处理的是 10 <sup>到 18</sup> 的数字，这个位置可以有 0 到 18 的值。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第二个状态是 ***计数*** 它定义了次数，到目前为止我们已经放置了数字 d。
*   另一个状态是布尔变量**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数**
*   **最后一个状态也是布尔变量 ***nonz*** ，这有助于考虑我们正在构建的数字中是否有任何前导零，我们不需要对它们进行计数。**

**在最后一次递归调用中，当我们在最后一个位置时，如果数字 d 的计数等于 K，返回 1，否则返回 0。
以下是上述方法的实现:** 

## **C++**

```
// CPP Program to find the count of
// numbers in a range where digit d
// occurs exactly K times
#include <bits/stdc++.h>
using namespace std;

const int M = 20;

// states - position, count, tight, nonz
int dp[M][M][2][2];

// d is required digit and K is occurrence
int d, K;

// This function returns the count of
// required numbers from 0 to num
int count(int pos, int cnt, int tight,
          int nonz, vector<int> num)
{
    // Last position
    if (pos == num.size()) {
        if (cnt == K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][cnt][tight][nonz] != -1)
        return dp[pos][cnt][tight][nonz];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int dig = 0; dig <= limit; dig++) {
        int currCnt = cnt;

        // Nonz is true if we placed a non
        // zero digit at the starting of
        // the number
        if (dig == d) {
            if (d != 0 || (!d && nonz))
                currCnt++;
        }

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call, also set nonz
        // to 1 if current digit is non zero
        ans += count(pos + 1, currCnt,
                     currTight, nonz || (dig != 0), num);
    }
    return dp[pos][cnt][tight][nonz] = ans;
}

// Function to convert x into its digit vector and uses
// count() function to return the required count
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

// Driver Code to test above functions
int main()
{
    int L = 11, R = 100;
    d = 2, K = 1;
    cout << solve(R) - solve(L - 1) << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to find the count of
// numbers in a range where digit d
// occurs exactly K times
import java.util.*;
class Solution
{
static final int M = 20;

// states - position, count, tight, nonz
static int dp[][][][]= new int[M][M][2][2];

// d is required digit and K is occurrence
static int d, K;

// This function returns the count of
// required numbers from 0 to num
static int count(int pos, int cnt, int tight,
          int nonz, Vector<Integer> num)
{
    // Last position
    if (pos == num.size()) {
        if (cnt == K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][cnt][tight][nonz] != -1)
        return dp[pos][cnt][tight][nonz];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = ((tight !=0)? 9 : num.get(pos));

    for (int dig = 0; dig <= limit; dig++) {
        int currCnt = cnt;

        // Nonz is true if we placed a non
        // zero digit at the starting of
        // the number
        if (dig == d) {
            if (d != 0 || (d==0 && nonz!=0))
                currCnt++;
        }

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num.get(pos))
            currTight = 1;

        // Next recursive call, also set nonz
        // to 1 if current digit is non zero
        ans += count(pos + 1, currCnt,
                     currTight, (dig != 0?1:0), num);
    }
    return dp[pos][cnt][tight][nonz] = ans;
}

// Function to convert x into its digit vector and uses
// count() function to return the required count
static int solve(int x)
{
    Vector<Integer> num= new Vector<Integer>();
    while (x!=0) {
        num.add(x % 10);
        x /= 10;
    }
    Collections.reverse(num);

    // Initialize dp
    for(int i=0;i<M;i++)
        for(int j=0;j<M;j++)
            for(int k=0;k<2;k++)
                for(int l=0;l<2;l++)
                dp[i][j][k][l]=-1;

    return count(0, 0, 0, 0, num);
}

// Driver Code to test above functions
public static void main(String args[])
{
    int L = 11, R = 100;
    d = 2; K = 1;
    System.out.print( solve(R) - solve(L - 1) );
}

}
//contributed by Arnab Kundu
```

## **蟒蛇 3**

```
# Python Program to find the count of
# numbers in a range where digit d
# occurs exactly K times
M = 20

# states - position, count, tight, nonz
dp = []

# d is required digit and K is occurrence
d, K = None, None

# This function returns the count of
# required numbers from 0 to num
def count(pos, cnt, tight, nonz, num: list):

    # Last position
    if pos == len(num):
        if cnt == K:
            return 1
        return 0

    # If this result is already computed
    # simply return it
    if dp[pos][cnt][tight][nonz] != -1:
        return dp[pos][cnt][tight][nonz]

    ans = 0

    # Maximum limit upto which we can place
    # digit. If tight is 1, means number has
    # already become smaller so we can place
    # any digit, otherwise num[pos]
    limit = 9 if tight else num[pos]

    for dig in range(limit + 1):
        currCnt = cnt

        # Nonz is true if we placed a non
        # zero digit at the starting of
        # the number
        if dig == d:
            if d != 0 or not d and nonz:
                currCnt += 1

        currTight = tight

        # At this position, number becomes
        # smaller
        if dig < num[pos]:
            currTight = 1

        # Next recursive call, also set nonz
        # to 1 if current digit is non zero
        ans += count(pos + 1, currCnt,
                currTight, (nonz or dig != 0), num)

    dp[pos][cnt][tight][nonz] = ans
    return dp[pos][cnt][tight][nonz]

# Function to convert x into its digit vector and uses
# count() function to return the required count
def solve(x):
    global dp, K, d

    num = []
    while x:
        num.append(x % 10)
        x //= 10

    num.reverse()

    # Initialize dp
    dp = [[[[-1, -1] for i in range(2)]
            for j in range(M)] for k in range(M)]
    return count(0, 0, 0, 0, num)

# Driver Code
if __name__ == "__main__":

    L = 11
    R = 100
    d = 2
    K = 1
    print(solve(R) - solve(L - 1))

# This code is contributed by
# sanjeev2552
```

## **C#**

```
// C# Program to find the count of
// numbers in a range where digit d
// occurs exactly K times
using System;
using System.Collections.Generic;

class GFG
{
    static readonly int M = 20;

    // states - position, count, tight, nonz
    static int [,,,]dp= new int[M, M, 2, 2];

    // d is required digit and K is occurrence
    static int d, K;

    // This function returns the count of
    // required numbers from 0 to num
    static int count(int pos, int cnt, int tight,
            int nonz, List<int> num)
    {
        // Last position
        if (pos == num.Count)
        {
            if (cnt == K)
                return 1;
            return 0;
        }

        // If this result is already computed
        // simply return it
        if (dp[pos, cnt, tight, nonz] != -1)
            return dp[pos, cnt, tight, nonz];

        int ans = 0;

        // Maximum limit upto which we can place
        // digit. If tight is 1, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = ((tight != 0) ? 9 : num[pos]);

        for (int dig = 0; dig <= limit; dig++)
        {
            int currCnt = cnt;

            // Nonz is true if we placed a non
            // zero digit at the starting of
            // the number
            if (dig == d)
            {
                if (d != 0 || (d == 0 && nonz != 0))
                    currCnt++;
            }

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (dig < num[pos])
                currTight = 1;

            // Next recursive call, also set nonz
            // to 1 if current digit is non zero
            ans += count(pos + 1, currCnt,
                        currTight, (dig != 0 ? 1 : 0), num);
        }
        return dp[pos, cnt, tight, nonz] = ans;
    }

    // Function to convert x into its
    // digit vector and uses count()
    // function to return the required count
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
            for(int j = 0; j < M; j++)
                for(int k = 0; k < 2; k++)
                    for(int l = 0; l < 2; l++)
                        dp[i, j, k, l]=-1;

        return count(0, 0, 0, 0, num);
    }

    // Driver Code
    public static void Main()
    {
        int L = 11, R = 100;
        d = 2; K = 1;
        Console.Write( solve(R) - solve(L - 1) );
    }
}

// This code is contributed by Rajput-JI
```

## **java 描述语言**

```
<script>

// JavaScript Program to find the count of
// numbers in a range where digit d
// occurs exactly K times

var M = 20;

// states - position, count, tight, nonz
var dp = Array.from(Array(M), ()=>Array(M));

// d is required digit and K is occurrence
var d, K;

// This function returns the count of
// required numbers from 0 to num
function count( pos, cnt, tight, nonz, num)
{
    // Last position
    if (pos == num.length) {
        if (cnt == K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][cnt][tight][nonz] != -1)
        return dp[pos][cnt][tight][nonz];

    var ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    var limit = (tight ? 9 : num[pos]);

    for (var dig = 0; dig <= limit; dig++) {
        var currCnt = cnt;

        // Nonz is true if we placed a non
        // zero digit at the starting of
        // the number
        if (dig == d) {
            if (d != 0 || (!d && nonz))
                currCnt++;
        }

        var currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call, also set nonz
        // to 1 if current digit is non zero
        ans += count(pos + 1, currCnt,
                     currTight, nonz || (dig != 0?1:0), num);
    }
    return dp[pos][cnt][tight][nonz] = ans;
}

// Function to convert x into its digit vector and uses
// count() function to return the required count
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
            dp[i][j] = Array.from(Array(2), ()=>Array(2).fill(-1))

    return count(0, 0, 0, 0, num);
}

// Driver Code to test above functions
var L = 11, R = 100;
d = 2, K = 1;
document.write( solve(R) - solve(L - 1));

</script>
```

****Output:** 

```
17
```**