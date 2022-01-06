# 将所有 1 保持在一个二进制串中所需的最小翻转次数

> 原文:[https://www . geesforgeks . org/minimum-flips-要求在二进制字符串中保留全 1/](https://www.geeksforgeeks.org/minimum-flips-required-to-keep-all-1s-together-in-a-binary-string/)

给定[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是找到在给定的二进制字符串中保持所有 1 在一起所需的最小翻转次数，即字符串中的 1 之间不能有任何 0。

**示例:**

> **输入:** str = "0011111100"
> **输出:** 0
> **解释:**我们不需要翻转任何位，因为所有的 1 都分组在一起，任何两个 1 之间都没有零。
> 
> **输入:** str = "11100111000101"
> **输出:** 4
> **解释:**我们可以翻转第 4 位和第 5 位使其为 1，翻转第 12 位和第 14 位使其为 0。因此得到的字符串是“11111111000000”，有 4 个可能的翻转。

**方法:**为了解决上述问题，我们将实施[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法，其中我们将具有以下状态:

*   **第一个状态是 dp[i][0]** ，表示到第 ith 位时将所有 0 清零所需的翻转次数。
*   **第二状态 dp[i][1]** ，表示使当前位 1 满足问题中给出的条件所需的翻转次数。

因此，对于 i 的所有值，要求的答案将是*最小翻转使当前位 1 +最小翻转使当前位 0 之后的所有位。但是如果给定字符串中的所有位都是 0，那么我们不需要改变任何东西，所以我们可以检查我们的答案和使字符串全为零所需的翻转次数之间的最小值。所以我们可以通过迭代字符串中的所有字符来计算答案，*

> **答案= min(答案，DP[I][1]+DP[n-1][0]–DP[I][0])**
> 其中
> dp[i][1] =将当前位设为 1 的最小翻转次数
> DP[n-1][0]–DP[I][0]=将 I 之后的所有位设为 0 所需的最小翻转次数

下面是上述方法的实现:

## C++

```
//cpp implementation for Minimum number of
//flips required in a binary string such
//that all the 1’s are together
#include <bits/stdc++.h>
using namespace std;
int minFlip(string a)
{
     //Length of the binary string
    int n = a.size();

    vector<vector<int>> dp(n + 1,vector<int>(2, 0));

    //Initial state of the dp
    //dp[0][0] will be 1 if the current
    //bit is 1 and we have to flip it
    dp[0][0] = (a[0] == '1');

    //Initial state of the dp
    //dp[0][1] will be 1 if the current
    //bit is 0 and we have to flip it
    dp[0][1] = (a[0] == '0');

    for (int i = 1; i < n; i++)
    {
        //dp[i][0] = Flips required to
        //make all previous bits zero
        //+ Flip required to make current bit zero
        dp[i][0] = dp[i - 1][0] + (a[i] == '1');

        //dp[i][1] = minimum flips required
        //to make all previous states 0 or make
        //previous states 1 satisfying the condition
        dp[i][1] = min(dp[i - 1][0],
                       dp[i - 1][1]) + (a[i] == '0');

    }
    int answer = INT_MAX;
    for (int i=0;i<n;i++)
    {
        answer = min(answer, dp[i][1] +
                             dp[n - 1][0] - dp[i][0]);
     }

    //Minimum of answer and flips
    //required to make all bits 0
    return min(answer, dp[n - 1][0]);
}

//Driver Code
int main()
{
  string s = "1100111000101";
  cout<<(minFlip(s));
}

// This code is contributed by Mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for
// Minimum number of flips
// required in a binary string
// such that all the 1’s are together
import java.io.*;
import java.util.*;
class GFG{

static int minFlip(String a)
{
  // Length of the binary string
  int n = a.length();

  int dp[][] = new int[n + 1][2];

  // Initial state of the dp
  // dp[0][0] will be 1 if
  // the current bit is 1
  // and we have to flip it
  if(a.charAt(0) == '1')
  {
    dp[0][0] = 1 ;
  }
  else dp[0][0] = 0;

  // Initial state of the dp
  // dp[0][1] will be 1 if
  // the current bit is 0
  // and we have to flip it
  if(a.charAt(0) == '0')
    dp[0][1] = 1;
  else dp[0][1] = 0;

  for (int i = 1; i < n; i++)
  {
    // dp[i][0] = Flips required to
    // make all previous bits zero
    // Flip required to make current
    // bit zero
    if(a.charAt(i) == '1')
    {
      dp[i][0] = dp[i - 1][0] + 1;
    }
    else dp[i][0] = dp[i - 1][0];

    // dp[i][1] = minimum flips
    // required to make all previous
    // states 0 or make previous states
    // 1 satisfying the condition
    if(a.charAt(i) == '0')
    {
      dp[i][1] = Math.min(dp[i - 1][0],
                          dp[i - 1][1]) + 1;
    }
    else dp[i][1] = Math.min(dp[i - 1][0],
                             dp[i - 1][1]);
  }

  int answer = Integer.MAX_VALUE;
  for (int i = 0; i < n; i++)
  {
    answer = Math.min(answer, dp[i][1] +
                      dp[n - 1][0] -
                      dp[i][0]);
  }

  //Minimum of answer and flips
  //required to make all bits 0
  return Math.min(answer,
                  dp[n - 1][0]);
}

// Driver code
public static void main (String[] args)
{
  String s = "1100111000101";
  System.out.println(minFlip(s));
}
}

// This code is contributed by satvikshrivas26
```

## 蟒蛇 3

```
# Python implementation for Minimum number of
# flips required in a binary string such
# that all the 1’s are together

def minFlip(a):

     # Length of the binary string
    n = len(a)

    dp =[[0, 0] for i in range(n)]

    # Initial state of the dp
    # dp[0][0] will be 1 if the current
    # bit is 1 and we have to flip it
    dp[0][0]= int(a[0]=='1')

    # Initial state of the dp
    # dp[0][1] will be 1 if the current
    # bit is 0 and we have to flip it
    dp[0][1]= int(a[0]=='0')

    for i in range(1, n):

        # dp[i][0] = Flips required to
        # make all previous bits zero
        # + Flip required to make current bit zero
        dp[i][0]= dp[i-1][0]+int(a[i]=='1')

        # dp[i][1] = minimum flips required
        # to make all previous states 0 or make
        # previous states 1 satisfying the condition
        dp[i][1]= min(dp[i-1])+int(a[i]=='0')

    answer = 10**18

    for i in range(n):
        answer = min(answer,
                     dp[i][1]+dp[n-1][0]-dp[i][0])

    # Minimum of answer and flips
    # required to make all bits 0
    return min(answer, dp[n-1][0])

# Driver code
s = "1100111000101"

print(minFlip(s))
```

## C#

```
// C# implementation for
// Minimum number of
// flips required in
// a binary string such
// that all the 1’s are together
using System;
class GFG{

static int minFlip(string a)
{
  //Length of the binary string
  int n = a.Length;

  int [,]dp=new int[n + 1, 2];

  //Initial state of the dp
  //dp[0][0] will be 1 if the current
  //bit is 1 and we have to flip it
  dp[0, 0] = (a[0] == '1' ? 1 : 0);

  //Initial state of the dp
  //dp[0][1] will be 1 if the current
  //bit is 0 and we have to flip it
  dp[0, 1] = (a[0] == '0' ? 1 : 0);

  for (int i = 1; i < n; i++)
  {
    //dp[i][0] = Flips required to
    //make all previous bits zero
    //+ Flip required to make current bit zero
    dp[i, 0] = dp[i - 1, 0] +
                 (a[i] == '1' ? 1 : 0);

    //dp[i][1] = minimum flips required
    //to make all previous states 0 or make
    //previous states 1 satisfying the condition
    dp[i, 1] = Math.Min(dp[i - 1, 0],
                        dp[i - 1, 1]) +
                       (a[i] == '0' ? 1 : 0);

  }
  int answer = int.MaxValue;

  for (int i = 0; i < n; i++)
  {
    answer = Math.Min(answer, dp[i, 1] +
                      dp[n - 1, 0] - dp[i, 0]);
  }

  //Minimum of answer and flips
  //required to make all bits 0
  return Math.Min(answer, dp[n - 1, 0]);
}

// Driver code
public static void Main(string[] args)
{
  string s = "1100111000101";
  Console.Write(minFlip(s));
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation for
// Minimum number of flips
// required in a binary string
// such that all the 1’s are together
function minFlip(a)
{

    // Length of the binary string
    let n = a.length;
    let dp = new Array(n + 2).fill(0).map((t) => new Array(2).fill(0))

    // Initial state of the dp
    // dp[0][0] will be 1 if
    // the current bit is 1
    // and we have to flip it
    if (a.charAt(0) == '1') {
        dp[0][0] = 1;
    }
    else dp[0][0] = 0;

    // Initial state of the dp
    // dp[0][1] will be 1 if
    // the current bit is 0
    // and we have to flip it
    if (a.charAt(0) == '0')
        dp[0][1] = 1;
    else dp[0][1] = 0;

    for (let i = 1; i < n; i++)
    {

        // dp[i][0] = Flips required to
        // make all previous bits zero
        // Flip required to make current
        // bit zero
        if (a.charAt(i) == '1') {
            dp[i][0] = dp[i - 1][0] + 1;
        }
        else dp[i][0] = dp[i - 1][0];

        // dp[i][1] = minimum flips
        // required to make all previous
        // states 0 or make previous states
        // 1 satisfying the condition
        if (a.charAt(i) == '0') {
            dp[i][1] = Math.min(dp[i - 1][0],
                dp[i - 1][1]) + 1;
        }
        else dp[i][1] = Math.min(dp[i - 1][0],
            dp[i - 1][1]);
    }

    let answer = Number.MAX_SAFE_INTEGER;
    for (let i = 0; i < n; i++) {
        answer = Math.min(answer, dp[i][1] +
            dp[n - 1][0] -
            dp[i][0]);
    }

    // Minimum of answer and flips
    // required to make all bits 0
    return Math.min(answer,
        dp[n - 1][0]);
}

// Driver code
let s = "1100111000101";
document.write(minFlip(s));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
4
```