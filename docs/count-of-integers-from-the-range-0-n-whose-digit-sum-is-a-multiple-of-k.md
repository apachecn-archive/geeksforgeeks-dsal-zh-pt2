# 数字和是 K 的倍数的[0，N]范围内的整数计数

> 原文:[https://www . geesforgeks . org/从 0 到 n 范围内的整数计数，其数字总和是 k 的倍数/](https://www.geeksforgeeks.org/count-of-integers-from-the-range-0-n-whose-digit-sum-is-a-multiple-of-k/)

给定两个整数 **N** 和 **K** ，任务是计算**【0，N】**范围内的整数个数，其数字和是 **K** 的倍数。答案可能很大，所以以 **10 <sup>9</sup> +7** 为模打印答案。

**示例:**

> **输入:** N = 10，K = 5
> **输出:** 2
> 0 和 5 是唯一可能的整数。
> 
> **输入:** N = 30，K = 4
> T3】输出: 7

**天真法:**对于 **N** 的小值，循环遍历**【0，N】**的范围，检查数字的位数之和是否为 **K** 的倍数。

**高效途径:**思路是用[数字 dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 来解决这个问题。从给定整数的左边或最高有效数字(MSD)开始迭代所有索引值的子问题将被解决，并且对于每个索引，存储方式的数量使得(到当前索引的数字总和)mod **K** 为零。动力定位状态将为:

> DP[idx][sum][紧绷]
> idx =位置，它讲述给定整数中从左到右的索引值
> sum =位数 mod k 的总和，如果当前值是否跨越范围(1，n)则该参数将存储生成的整数中从最高有效位(MSD)到 p
> 紧绷=标志的(位数 mod k 的总和)
> 对于无限制范围紧绷= 0
> 对于受限范围紧绷= 1

假设我们在 MSD 拥有指数 **idx** 。所以最初的总数是 **0** 。在每个位置，设定一个始终在**【0，9】**范围内的极限。
因此，用从 **0** 开始的范围内的数字来填充索引处的数字，以限制并从下一状态获取答案，下一状态的**索引= idx + 1** 和**new _ 紧绷**是分开计算的。dp 状态定义将是:

> DP[idx][sum][紧密]+= DP[idx+1][(sum+d)% k][new _ 紧密]
> 为 d in [0，极限]

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 100005
#define MOD 1000000007

// To store the states of the dp
int dp[MAX][101][2];

// Function to return the count of numbers
// from the range [0, n] whose digit sum
// is a multiple of k using bottom-up dp
int countNum(int idx, int sum, int tight,
             vector<int> num, int len, int k)
{
    if (len == idx) {
        if (sum == 0)
            return 1;
        else
            return 0;
    }
    if (dp[idx][sum][tight] != -1)
        return dp[idx][sum][tight];
    int res = 0, limit;

    // The digit in this index can
    // only be from [0, num[idx]]
    if (tight == 0) {
        limit = num[idx];
    }

    // The digit in this index can
    // be anything from [0, 9]
    else {
        limit = 9;
    }
    for (int i = 0; i <= limit; i++) {

        // new_tight is the flag value
        // for the next position
        int new_tight = tight;
        if (tight == 0 && i < limit)
            new_tight = 1;
        res += countNum(idx + 1,
                        (sum + i) % k, new_tight,
                        num, len, k);
        res %= MOD;
    }

    // res can't be negative
    if (res < 0)
        res += MOD;
    return dp[idx][sum][tight] = res;
}

// Function to process the string to
// a vector of digits from MSD to LSD
vector<int> process(string s)
{
    vector<int> num;
    for (int i = 0; i < s.length(); i++) {
        num.push_back(s[i] - '0');
    }
    return num;
}

// Driver code
int main()
{

    // For large input number n
    string n = "98765432109876543210";

    // Total number of digits in n
    int len = n.length();

    int k = 58;

    // Clean dp table
    memset(dp, -1, sizeof(dp));

    // Process the string to a vector
    // of digits from MSD to LSD
    vector<int> num = process(n);

    cout << countNum(0, 0, 0, num, len, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static final int MAX = 100005;
static final int MOD = 1000000007;

// To store the states of the dp
static int [][][]dp = new int[MAX][101][2];

// Function to return the count of numbers
// from the range [0, n] whose digit sum
// is a multiple of k using bottom-up dp
static int countNum(int idx, int sum, int tight,
            Vector<Integer> num, int len, int k)
{
    if (len == idx)
    {
        if (sum == 0)
            return 1;
        else
            return 0;
    }
    if (dp[idx][sum][tight] != -1)
        return dp[idx][sum][tight];
    int res = 0, limit;

    // The digit in this index can
    // only be from [0, num[idx]]
    if (tight == 0)
    {
        limit = num.get(idx);
    }

    // The digit in this index can
    // be anything from [0, 9]
    else
    {
        limit = 9;
    }
    for (int i = 0; i <= limit; i++)
    {

        // new_tight is the flag value
        // for the next position
        int new_tight = tight;
        if (tight == 0 && i < limit)
            new_tight = 1;
        res += countNum(idx + 1,
                        (sum + i) % k, new_tight,
                        num, len, k);
        res %= MOD;
    }

    // res can't be negative
    if (res < 0)
        res += MOD;
    return dp[idx][sum][tight] = res;
}

// Function to process the String to
// a vector of digits from MSD to LSD
static Vector<Integer> process(String s)
{
    Vector<Integer> num = new Vector<Integer>();
    for (int i = 0; i < s.length(); i++)
    {
        num.add(s.charAt(i) - '0');
    }
    return num;
}

// Driver code
public static void main(String[] args)
{

    // For large input number n
    String n = "98765432109876543210";

    // Total number of digits in n
    int len = n.length();

    int k = 58;

    // Clean dp table
    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < 101; j++)
        {
            for(int l = 0; l < 2; l++)
            dp[i][j][l] = -1;
        }
    }

    // Process the String to a vector
    // of digits from MSD to LSD
    Vector<Integer> num = process(n);

    System.out.print(countNum(0, 0, 0, num, len, k));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 10005
MOD = 1000000007

# Function to return the count of numbers
# from the range [0, n] whose digit sum
# is a multiple of k using bottom-up dp
def countNum(idx, sum, tight, num, len1, k):
    if (len1 == idx):
        if (sum == 0):
            return 1
        else:
            return 0
    if (dp[idx][sum][tight] != -1):
        return dp[idx][sum][tight]
    res = 0

    # The digit in this index can
    # only be from [0, num[idx]]
    if (tight == 0):
        limit = num[idx]

    # The digit in this index can
    # be anything from [0, 9]
    else:
        limit = 9
    for i in range(limit + 1):

        # new_tight is the flag value
        # for the next position
        new_tight = tight
        if (tight == 0 and i < limit):
            new_tight = 1
        res += countNum(idx + 1,(sum + i) % k,
                      new_tight, num, len1, k)
        res %= MOD

    # res can't be negative
    if (res < 0):
        res += MOD
    dp[idx][sum][tight] = res
    return dp[idx][sum][tight]

# Function to process the string to
# a vector of digits from MSD to LSD
def process(s):
    num = []
    for i in range(len(s)):
        num.append(ord(s[i]) - ord('0'))
    return num

# Driver code
if __name__ == '__main__':

    # For large input number n
    n = "98765432109876543210"

    # Total number of digits in n
    len1 = len(n)

    k = 58

    # To store the states of the dp
    dp = [[[-1 for i in range(2)]
               for j in range(101)]
               for k in range(MAX)]

    # Process the string to a vector
    # of digits from MSD to LSD
    num = process(n)

    print(countNum(0, 0, 0, num, len1, k))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static readonly int MAX = 10005;
static readonly int MOD = 1000000007;

// To store the states of the dp
static int [,,]dp = new int[MAX, 101, 2];

// Function to return the count of numbers
// from the range [0, n] whose digit sum
// is a multiple of k using bottom-up dp
static int countNum(int idx, int sum, int tight,
              List<int> num, int len, int k)
{
    if (len == idx)
    {
        if (sum == 0)
            return 1;
        else
            return 0;
    }

    if (dp[idx, sum, tight] != -1)
        return dp[idx, sum, tight];
    int res = 0, limit;

    // The digit in this index can
    // only be from [0, num[idx]]
    if (tight == 0)
    {
        limit = num[idx];
    }

    // The digit in this index can
    // be anything from [0, 9]
    else
    {
        limit = 9;
    }
    for (int i = 0; i <= limit; i++)
    {

        // new_tight is the flag value
        // for the next position
        int new_tight = tight;
        if (tight == 0 && i < limit)
            new_tight = 1;
        res += countNum(idx + 1,
                       (sum + i) % k, new_tight,
                        num, len, k);
        res %= MOD;
    }

    // res can't be negative
    if (res < 0)
        res += MOD;
    return dp[idx, sum, tight] = res;
}

// Function to process the String to
// a vector of digits from MSD to LSD
static List<int> process(String s)
{
    List<int> num = new List<int>();
    for (int i = 0; i < s.Length; i++)
    {
        num.Add(s[i] - '0');
    }
    return num;
}

// Driver code
public static void Main(String[] args)
{

    // For large input number n
    String n = "98765432109876543210";

    // Total number of digits in n
    int len = n.Length;

    int k = 58;

    // Clean dp table
    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < 101; j++)
        {
            for(int l = 0; l < 2; l++)
            dp[i, j, l] = -1;
        }
    }

    // Process the String to a vector
    // of digits from MSD to LSD
    List<int> num = process(n);

    Console.Write(countNum(0, 0, 0, num, len, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 100005;
var MOD = 1000000007;

// To store the states of the dp
var dp = Array.from(Array(MAX), () => Array(101));
for(var i =0; i<MAX; i++)
        for(var j =0; j<101; j++)
            dp[i][j] = new Array(2).fill(-1);

// Function to return the count of numbers
// from the range [0, n] whose digit sum
// is a multiple of k using bottom-up dp
function countNum(idx, sum, tight, num, len, k)
{
    if (len == idx) {
        if (sum == 0)
            return 1;
        else
            return 0;
    }
    if (dp[idx][sum][tight] != -1)
        return dp[idx][sum][tight];
    var res = 0, limit;

    // The digit in this index can
    // only be from [0, num[idx]]
    if (tight == 0) {
        limit = num[idx];
    }

    // The digit in this index can
    // be anything from [0, 9]
    else {
        limit = 9;
    }
    for (var i = 0; i <= limit; i++) {

        // new_tight is the flag value
        // for the next position
        var new_tight = tight;
        if (tight == 0 && i < limit)
            new_tight = 1;
        res += countNum(idx + 1,
                        (sum + i) % k, new_tight,
                        num, len, k);
        res %= MOD;
    }

    // res can't be negative
    if (res < 0)
        res += MOD;
    return dp[idx][sum][tight] = res;
}

// Function to process the string to
// a vector of digits from MSD to LSD
function process(s)
{
    var num = [];
    for (var i = 0; i < s.length; i++) {
        num.push(s[i].charCodeAt(0) - '0'.charCodeAt(0));
    }
    return num;
}

// Driver code
// For large input number n
var n = "98765432109876543210";
// Total number of digits in n
var len = n.length;
var k = 58;
// Process the string to a vector
// of digits from MSD to LSD
var num = process(n);
document.write( countNum(0, 0, 0, num, len, k));

</script>
```

**Output:** 

```
635270835
```