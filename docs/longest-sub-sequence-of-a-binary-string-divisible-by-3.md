# 可被 3 整除的二进制串的最长子序列

> 原文:[https://www . geesforgeks . org/最长二进制字符串子序列可被 3 整除/](https://www.geeksforgeeks.org/longest-sub-sequence-of-a-binary-string-divisible-by-3/)

给定一个长度为 **N** 的二进制字符串 **S** ，任务是找出其中最长的子序列的长度，该长度可被 **3** 整除。子序列中的前导零是允许的。
**举例:**

> **输入:**S = " 1001 "
> T3】输出: 4
> 最长可被 3 整除的子序列是“1001”。
> 1001 = 9，可被 3 整除。
> **输入:** S = "1011"
> **输出:** 3

**天真方法:**生成所有可能的子序列，检查它们是否可以被 **3** 整除。时间复杂度为 **O((2 <sup>N</sup> ) * N)** 。
**高效的方法:** [动态编程](https://www.geeksforgeeks.org/dynamic-programming/)可以用来解决这个问题。我们来看看 DP 的状态。
**DP[i][r]** 将存储子串 **S[i…N-1]** 的最长子序列，这样当除以 **3** 时，它给出**(3–r)% 3**的余数。
现在写递归关系。

> DP[i][r] = max（1 + DP[i + 1][（r * 2 + s[i]） % 3]， DP[i + 1][r]）

递归是由以下两个选择导出的:

1.  将当前索引 **i** 包含在子序列中。因此， **r** 将更新为 **r = (r * 2 + s[i]) % 3** 。
2.  不要将当前索引包含在子序列中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100

int dp[N][3];
bool v[N][3];

// Function to return the length of the
// largest sub-string divisible by 3
int findLargestString(string& s, int i, int r)
{
    // Base-case
    if (i == s.size()) {
        if (r == 0)
            return 0;
        else
            return INT_MIN;
    }

    // If the state has been solved
    // before then return its value
    if (v[i][r])
        return dp[i][r];

    // Marking the state as solved
    v[i][r] = 1;

    // Recurrence relation
    dp[i][r]
        = max(1 + findLargestString(s, i + 1,
                                    (r * 2 + (s[i] - '0')) % 3),
              findLargestString(s, i + 1, r));
    return dp[i][r];
}

// Driver code
int main()
{
    string s = "101";

    cout << findLargestString(s, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of th approach
class GFG
{

    final static int N = 100 ;
    final static int INT_MIN = Integer.MIN_VALUE;

    static int dp[][] = new int[N][3];
    static int v[][] = new int[N][3];

    // Function to return the length of the
    // largest sub-string divisible by 3
    static int findLargestString(String s, int i, int r)
    {
        // Base-case
        if (i == s.length())
        {
            if (r == 0)
                return 0;
            else
                return INT_MIN;
        }

        // If the state has been solved
        // before then return its value
        if (v[i][r] == 1)
            return dp[i][r];

        // Marking the state as solved
        v[i][r] = 1;

        // Recurrence relation
        dp[i][r] = Math.max(1 + findLargestString(s, i + 1,
                          (r * 2 + (s.charAt(i) - '0')) % 3),
                            findLargestString(s, i + 1, r));
        return dp[i][r];
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "101";

        System.out.print(findLargestString(s, 0, 0));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np
import sys

N = 100
INT_MIN = -(sys.maxsize - 1)

dp = np.zeros((N, 3));
v = np.zeros((N, 3));

# Function to return the length of the
# largest sub-string divisible by 3
def findLargestString(s, i, r) :

    # Base-case
    if (i == len(s)) :
        if (r == 0) :
            return 0;
        else :
            return INT_MIN;

    # If the state has been solved
    # before then return its value
    if (v[i][r]) :
        return dp[i][r];

    # Marking the state as solved
    v[i][r] = 1;

    # Recurrence relation
    dp[i][r] = max(1 + findLargestString(s, i + 1,
                  (r * 2 + (ord(s[i]) - ord('0'))) % 3),
                       findLargestString(s, i + 1, r));

    return dp[i][r];

# Driver code
if __name__ == "__main__" :

    s = "101";

    print(findLargestString(s, 0, 0));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of th approach
using System;
using System.Collections.Generic;

class GFG
{

    readonly static int N = 100 ;
    readonly static int INT_MIN = int.MinValue;

    static int [,]dp = new int[N, 3];
    static int [,]v = new int[N, 3];

    // Function to return the length of the
    // largest sub-string divisible by 3
    static int findLargestString(String s, int i, int r)
    {
        // Base-case
        if (i == s.Length)
        {
            if (r == 0)
                return 0;
            else
                return INT_MIN;
        }

        // If the state has been solved
        // before then return its value
        if (v[i, r] == 1)
            return dp[i, r];

        // Marking the state as solved
        v[i, r] = 1;

        // Recurrence relation
        dp[i, r] = Math.Max(1 + findLargestString(s, i + 1,
                                (r * 2 + (s[i] - '0')) % 3),
                            findLargestString(s, i + 1, r));
        return dp[i, r];
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "101";

        Console.Write(findLargestString(s, 0, 0));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
var N = 100

var dp = Array.from(Array(N), ()=>Array(3));
var v = Array.from(Array(N), ()=>Array(3));

// Function to return the length of the
// largest sub-string divisible by 3
function findLargestString(s, i, r)
{
    // Base-case
    if (i == s.length) {
        if (r == 0)
            return 0;
        else
            return -1000000000;
    }

    // If the state has been solved
    // before then return its value
    if (v[i][r])
        return dp[i][r];

    // Marking the state as solved
    v[i][r] = 1;

    // Recurrence relation
    dp[i][r]
        = Math.max(1 + findLargestString(s, i + 1,
                                    (r * 2 + (s[i].charCodeAt(0) - '0'.charCodeAt(0))) % 3),
              findLargestString(s, i + 1, r));
    return dp[i][r];
}

// Driver code
var s = "101";
document.write( findLargestString(s, 0, 0));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n)