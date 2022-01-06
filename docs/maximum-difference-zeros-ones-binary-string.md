# 二进制字符串中 0 和 1 的最大差值

> 原文:[https://www . geesforgeks . org/最大差值-0-1-二进制-字符串/](https://www.geeksforgeeks.org/maximum-difference-zeros-ones-binary-string/)

给定 0 和 1 的二进制字符串。任务是找出 0 数和 1 数(0 数-1 数)相差最大的子串长度。如果是全 1 打印-1。
示例:

```
Input : S = "11000010001"
Output : 6
From index 2 to index 9, there are 7
0s and 1 1s, so number of 0s - number
of 1s is 6.

Input : S = "1111"
Output : -1
```

这个想法是用动态规划来解决这个问题。
在此之前，我们将给定的二进制字符串转换为值为 1 和-1 的整数数组，比如 arr[]。这可以很容易地通过遍历给定的二进制字符串来完成，如果索引在数组的相应位置包含' 0' make -1。同样，如果索引包含“1”，则在数组中取 1。
现在，在每个指数 I，我们需要决定是接受它还是跳过它。因此，声明一个大小为 n×2 的 2D 数组，其中 n 是给定二进制字符串的长度，比如 dp[n][2]。

```
dp[i][0] define the maximum value upto 
         index i, when we skip the i-th
         index element.
dp[i][1] define the maximum value upto 
         index i after taking the i-th
         index element.

Therefore, we can derive dp[i][] as:
dp[i][0] = max(dp[i+1][0], dp[i+1][1] + arr[i])
dp[i][1] = max(dp[i+1][1] + arr[i], 0)
```

对于所有的，我们明确地检查这个情况。

## C++

```
// CPP Program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.
#include <bits/stdc++.h>
#define MAX 100
using namespace std;

// Return true if there all 1s
bool allones(string s, int n)
{
    // Checking each index is 0 or not.
    int co = 0;
    for (int i = 0; i < s.size(); i++)
        co += (s[i] == '1');

    return (co == n);
}

// Find the length of substring with maximum
// difference of zeroes and ones in binary
// string
int findlength(int arr[], string s, int n,
              int ind, int st, int dp[][3])
{
    // If string is over.
    if (ind >= n)
        return 0;

    // If the state is already calculated.
    if (dp[ind][st] != -1)
        return dp[ind][st];

    if (st == 0)
        return dp[ind][st] = max(arr[ind] +
          findlength(arr, s, n, ind + 1, 1, dp),
          findlength(arr, s, n, ind + 1, 0, dp));

    else
        return dp[ind][st] = max(arr[ind] +
       findlength(arr, s, n, ind + 1, 1, dp), 0);
}

// Returns length of substring which is
// having maximum difference of number
// of 0s and number of 1s
int maxLen(string s, int n)
{
    // If all 1s return -1.
    if (allones(s, n))
        return -1;   

    // Else find the length.
    int arr[MAX] = { 0 };
    for (int i = 0; i < n; i++)
        arr[i] = (s[i] == '0' ? 1 : -1);   

    int dp[MAX][3];
    memset(dp, -1, sizeof dp);
    return findlength(arr, s, n, 0, 0, dp);
}

// Driven Program
int main()
{
    string s = "11000010001";
    int n = 11;
    cout << maxLen(s, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.
import java.util.Arrays;

class GFG
{
static final int MAX=100;

// Return true if there all 1s
static boolean allones(String s, int n)
{
    // Checking each index is 0 or not.
    int co = 0;
    for (int i = 0; i < s.length(); i++)
        if(s.charAt(i) == '1')
            co +=1;    

    return (co == n);
}

// Find the length of substring with maximum
// difference of zeroes and ones in binary
// string
static int findlength(int arr[], String s, int n,
                     int ind, int st, int dp[][])
{
    // If string is over.
    if (ind >= n)
        return 0;

    // If the state is already calculated.
    if (dp[ind][st] != -1)
        return dp[ind][st];

    if (st == 0)
        return dp[ind][st] = Math.max(arr[ind] +
                             findlength(arr, s, n,
                                   ind + 1, 1, dp),
                             findlength(arr, s, n,
                                   ind + 1, 0, dp));

    else
        return dp[ind][st] = Math.max(arr[ind] +
                             findlength(arr, s, n,
                               ind + 1, 1, dp), 0);
}

// Returns length of substring which is
// having maximum difference of number
// of 0s and number of 1s
static int maxLen(String s, int n)
{
    // If all 1s return -1.
    if (allones(s, n))
        return -1;

    // Else find the length.
    int arr[] = new int[MAX];
    for (int i = 0; i < n; i++)
        arr[i] = (s.charAt(i) == '0' ? 1 : -1);

    int dp[][] = new int[MAX][3];
    for (int[] row : dp)
            Arrays.fill(row, -1);
    return findlength(arr, s, n, 0, 0, dp);
}

// Driver code
public static void main (String[] args)
{
    String s = "11000010001";
    int n = 11;
    System.out.println(maxLen(s, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python Program to find the length of
# substring with maximum difference of
# zeroes and ones in binary string.
MAX = 100

# Return true if there all 1s
def allones(s, n):

    # Checking each index
    # is 0 or not.
    co = 0

    for i in s:
        co += 1 if i == '1' else 0

    return co == n

# Find the length of substring with
# maximum difference of zeroes and
# ones in binary string
def findlength(arr, s, n, ind, st, dp):

    # If string is over
    if ind >= n:
        return 0

    # If the state is already calculated.
    if dp[ind][st] != -1:
        return dp[ind][st]

    if not st:
        dp[ind][st] = max(arr[ind] +
           findlength(arr, s, n, ind + 1, 1, dp),
            (findlength(arr, s, n, ind + 1, 0, dp)))
    else:
        dp[ind][st] = max(arr[ind] +
         findlength(arr, s, n, ind + 1, 1, dp), 0)

    return dp[ind][st]

# Returns length of substring which is
# having maximum difference of number
# of 0s and number of 1s
def maxLen(s, n):

    # If all 1s return -1.
    if allones(s, n):
        return -1

    # Else find the length.
    arr = [0] * MAX
    for i in range(n):
        arr[i] = 1 if s[i] == '0' else -1

    dp = [[-1] * 3 for _ in range(MAX)]
    return findlength(arr, s, n, 0, 0, dp)

# Driven Program
s = "11000010001"
n = 11
print(maxLen(s, n))

# This code is contributed by Ansu Kumari.
```

## C#

```
// C# Program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.
using System;

class GFG
{
    static int MAX = 100;

    // Return true if there all 1s
    public static bool allones(string s, int n)
    {
        // Checking each index is 0 or not.
        int co = 0;
        for (int i = 0; i < s.Length; i++)
            co += (s[i] == '1' ? 1 : 0);

        return (co == n);
    }

    // Find the length of substring with maximum
    // difference of zeroes and ones in binary
    // string
    public static int findlength(int[] arr, string s,
                    int n, int ind, int st, int[,] dp)
    {
        // If string is over.
        if (ind >= n)
            return 0;

        // If the state is already calculated.
        if (dp[ind,st] != -1)
            return dp[ind,st];

        if (st == 0)
            return dp[ind,st] = Math.Max(arr[ind] +
            findlength(arr, s, n, ind + 1, 1, dp),
            findlength(arr, s, n, ind + 1, 0, dp));

        else
            return dp[ind,st] = Math.Max(arr[ind] +
        findlength(arr, s, n, ind + 1, 1, dp), 0);
    }

    // Returns length of substring which is
    // having maximum difference of number
    // of 0s and number of 1s
    public static int maxLen(string s, int n)
    {
        // If all 1s return -1.
        if (allones(s, n))
            return -1;    

        // Else find the length.
        int[] arr = new int[MAX];

        for (int i = 0; i < n; i++)
            arr[i] = (s[i] == '0' ? 1 : -1);    

        int[,] dp = new int[MAX,3];
        for(int i = 0; i < MAX; i++)
            for(int j = 0; j < 3; j++)
                dp[i,j] = -1;

        return findlength(arr, s, n, 0, 0, dp);
    }

    // Driven Program

    static void Main()
    {
        string s = "11000010001";
        int n = 11;
        Console.Write(maxLen(s, n));
    }
    // This code is contributed by DrRoot_
}
```

## java 描述语言

```
<script>

// Javascript Program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.
var MAX = 100;

// Return true if there all 1s
function allones( s,  n)
{
    // Checking each index is 0 or not.
    var co = 0;
    for (var i = 0; i < s.length; i++)
        co += (s[i] == '1');

    return (co == n);
}

// Find the length of substring with maximum
// difference of zeroes and ones in binary
// string
function findlength(arr, s, n, ind, st, dp)
{
    // If string is over.
    if (ind >= n)
        return 0;

    // If the state is already calculated.
    if (dp[ind][st] != -1)
        return dp[ind][st];

    if (st == 0)
        return dp[ind][st] = Math.max(arr[ind] +
          findlength(arr, s, n, ind + 1, 1, dp),
          findlength(arr, s, n, ind + 1, 0, dp));

    else
        return dp[ind][st] = Math.max(arr[ind] +
       findlength(arr, s, n, ind + 1, 1, dp), 0);
}

// Returns length of substring which is
// having maximum difference of number
// of 0s and number of 1s
function maxLen( s,  n)
{
    // If all 1s return -1.
    if (allones(s, n))
        return -1;   

    // Else find the length.
    var arr = Array(MAX).fill(0);
    for (var i = 0; i < n; i++)
        arr[i] = (s[i] == '0' ? 1 : -1);   

    var dp = Array.from(Array(MAX), ()=> Array(3).fill(-1));
    return findlength(arr, s, n, 0, 0, dp);
}

// Driven Program
var s = "11000010001";
var n = 11;
document.write( maxLen(s, n));

</script>
```

**输出:**

```
6
```

[二进制字符串中 0 和 1 的最大差值|集合 2 (O(n)时间)](https://www.geeksforgeeks.org/maximum-difference-zeros-ones-binary-string-set-2-time/)