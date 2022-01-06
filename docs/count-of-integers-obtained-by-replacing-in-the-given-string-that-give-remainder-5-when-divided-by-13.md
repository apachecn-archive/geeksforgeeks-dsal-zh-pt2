# 替换得到的整数个数？在给定的字符串中，除以 13 得到余数 5

> 原文:[https://www . geeksforgeeks . org/整数计数-通过在给定字符串中替换给定余数-13 除以 5 获得/](https://www.geeksforgeeks.org/count-of-integers-obtained-by-replacing-in-the-given-string-that-give-remainder-5-when-divided-by-13/)

给定长度为 **N** 的弦**弦**。任务是找出通过替换**“？”得到的整数个数**任意数字，当被 **13** 除时，形成的整数给出余数 **5** 。
数字也可以从零开始。答案可以很大，所以，输出答案模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** str =？44"
> **输出:** 1
> 唯一可能的数字是 044
> **输入:** str = "7？4"
> **输出:** 0
> **输入:** str = "8？3?4233?4?"
> **输出:** 770

**方法:**让 **dp[i][j]** 为创建与给定图案的第一个 **i** 数字一致并与 **j** 模 **13** 一致的 I 位数的方法数。作为我们的基本情况， **dp[0][i]=0** 为 **i** 从 **1** 到 **12** ， **dp[0][0]=1** (作为我们的长度-零号有值零，因此是**零 mod 13** 。)
请注意，在数字 **j mod 13** 的末尾添加一个数字 **k** 会给出一个与 **10j+k mod 13** 一致的数字。我们用这个事实来执行我们的转换。对于每个状态， **dp[i][j]** 与 **i < N** 一起，迭代 **k** 的可能值。(如果 **s[i]= '？'****k**会有十个选择，否则只会有一个选择。)然后，我们将 **dp[i][j]** 添加到 **dp[i+1][(10j+k)%13]。**
要得到我们最终的答案，我们可以简单的打印 **dp[N][5]** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MOD (int)(1e9 + 7)

// Function to find the count of integers
// obtained by replacing '?' in a given
// string such that formed integer
// gives remainder 5 when it is divided by 13
int modulo_13(string s, int n)
{
    long long dp[n + 1][13] = { { 0 } };

    // Initialise
    dp[0][0] = 1;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < 10; j++) {
            int nxt = s[i] - '0';

            // Place digit j at ? position
            if (s[i] == '?')
                nxt = j;

            // Get the remainder
            for (int k = 0; k < 13; k++) {
                int rem = (10 * k + nxt) % 13;
                dp[i + 1][rem] += dp[i][k];
                dp[i + 1][rem] %= MOD;
            }
            if (s[i] != '?')
                break;
        }
    }

    // Return the required answer
    return (int)dp[n][5];
}

// Driver code
int main()
{
    string s = "?44";
    int n = s.size();

    cout << modulo_13(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MOD = (int)(1e9 + 7);

// Function to find the count of integers
// obtained by replacing '?' in a given
// string such that formed integer
// gives remainder 5 when it is divided by 13
static int modulo_13(String s, int n)
{
    long [][]dp = new long[n + 1][13];

    // Initialise
    dp[0][0] = 1;

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            int nxt = s.charAt(i) - '0';

            // Place digit j at ? position
            if (s.charAt(i) == '?')
                nxt = j;

            // Get the remainder
            for (int k = 0; k < 13; k++)
            {
                int rem = (10 * k + nxt) % 13;
                dp[i + 1][rem] += dp[i][k];
                dp[i + 1][rem] %= MOD;
            }
            if (s.charAt(i) != '?')
                break;
        }
    }

    // Return the required answer
    return (int)dp[n][5];
}

// Driver code
public static void main(String []args)
{
    String s = "?44";
    int n = s.length();

    System.out.println(modulo_13(s, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

MOD = (int)(1e9 + 7)

# Function to find the count of integers
# obtained by replacing '?' in a given
# string such that formed integer
# gives remainder 5 when it is divided by 13
def modulo_13(s, n) :

    dp = np.zeros((n + 1, 13));

    # Initialise
    dp[0][0] = 1;

    for i in range(n) :
        for j in range(10) :
            nxt = ord(s[i]) - ord('0');

            # Place digit j at ? position
            if (s[i] == '?') :
                nxt = j;

            # Get the remainder
            for k in range(13) :
                rem = (10 * k + nxt) % 13;
                dp[i + 1][rem] += dp[i][k];
                dp[i + 1][rem] %= MOD;

            if (s[i] != '?') :
                break;

    # Return the required answer
    return int(dp[n][5]);

# Driver code
if __name__ == "__main__" :
    s = "?44";
    n = len(s);

    print(modulo_13(s, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MOD = (int)(1e9 + 7);

// Function to find the count of integers
// obtained by replacing '?' in a given
// string such that formed integer
// gives remainder 5 when it is divided by 13
static int modulo_13(String s, int n)
{
    long [,]dp = new long[n + 1, 13];

    // Initialise
    dp[0, 0] = 1;

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            int nxt = s[i] - '0';

            // Place digit j at ? position
            if (s[i] == '?')
                nxt = j;

            // Get the remainder
            for (int k = 0; k < 13; k++)
            {
                int rem = (10 * k + nxt) % 13;
                dp[i + 1, rem] += dp[i, k];
                dp[i + 1, rem] %= MOD;
            }
            if (s[i] != '?')
                break;
        }
    }

    // Return the required answer
    return (int)dp[n,5];
}

// Driver code
public static void Main(String []args)
{
    String s = "?44";
    int n = s.Length;

    Console.WriteLine(modulo_13(s, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    var MOD = parseInt(1e9 + 7);

    // Function to find the count of integers
    // obtained by replacing '?' in a given
    // string such that formed integer
    // gives remainder 5 when it is divided by 13
    function modulo_13( s , n) {
        var dp = Array(n + 1).fill().map(()=>Array(13).fill(0));

        // Initialise
        dp[0][0] = 1;

        for (i = 0; i < n; i++) {
            for (j = 0; j < 10; j++) {
                var nxt = s.charAt(i) - '0';

                // Place digit j at ? position
                if (s.charAt(i) == '?')
                    nxt = j;

                // Get the remainder
                for (k = 0; k < 13; k++) {
                    var rem = (10 * k + nxt) % 13;
                    dp[i + 1][rem] += dp[i][k];
                    dp[i + 1][rem] %= MOD;
                }
                if (s.charAt(i) != '?')
                    break;
            }
        }

        // Return the required answer
        return parseInt( dp[n][5]);
    }

    // Driver code

        var s = "?44";
        var n = s.length;

        document.write(modulo_13(s, n));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(100 * N)

**辅助空间:** O(100 * N)