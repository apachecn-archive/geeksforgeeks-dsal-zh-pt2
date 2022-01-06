# 执行给定操作后不同可能字符串的计数

> 原文:[https://www . geeksforgeeks . org/执行给定操作后可能出现的不同字符串计数/](https://www.geeksforgeeks.org/count-of-distinct-possible-strings-after-performing-given-operations/)

给定一个数字字符串 **S** ，该字符串最初仅包含三种类型的字符 **0、1** 和 **2** ，并执行以下两个操作:

*   两个连续 1 的出现可以用 3 代替。
*   连续出现两个 2 可以用 4 代替。

给定的任务是找到通过使用操作可以形成的不同字符串的总数。
**例:**

> **输入:** S = "0110000022"
> **输出:** 4
> **解释:**
> 使用运算可以形成四种不同的形式，这四个字符串分别是
> “01100000022”“030000022”“03000004”“011000004”
> **输入:**S =“111”

**方法:**
为了解决这个问题，我们采用了动态规划的方法。我们定义一个数组 **dp** 来存储长度等于其各自索引的可能字符串的计数。

*   初始化 dp[0] = dp[1] = 1。
*   对于在**【1，N-1】**之间的任何索引 I，如果该索引处的字符是“1”或“2”，并且等于其先前索引的字符，则添加可能由长度 **i-1** 和 **i-2** 组成的字符串。否则与长度 **i-1** 相同。

> dp[i + 1] = dp[i] + dp[i-1]如果 S[i] == S[i-1]，其中 S[i]是' 1 '或' 2 '。
> dp[i + 1] = dp[i]否则。

*   返回 **dp[n]** 作为可能的不同字符串的计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include
using namespace std;

// Function that prints the
// number of different strings
// that can be formed
void differentStrings(string s)
{
    // Computing the length of
    // the given string
    int n = s.length();

    vector dp(n + 1);

    // Base case
    dp[0] = dp[1] = 1;

    // Traverse the given string
    for (int i = 1; i < n; i++) {

        // If two consecutive 1's
        // or 2's are present
        if (s[i] == s[i - 1]
            && (s[i] == '1'
                || s[i] == '2'))

            dp[i + 1]
                = dp[i] + dp[i - 1];

        // Otherwise take
        // the previous value
        else
            dp[i + 1] = dp[i];
    }

    cout << dp[n] << "\n";
}

// Driver Code
int main()
{
    string S = "0111022110";

    differentStrings(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG{

// Function that prints the
// number of different strings
// that can be formed
static void differentStrings(String s)
{

    // Computing the length of
    // the given string
    int n = s.length();

    int[] dp = new int[n + 1];

    // Base case
    dp[0] = dp[1] = 1;

    // Traverse the given string
    for(int i = 1; i < n; i++)
    {

       // If two consecutive 1's
       // or 2's are present
       if (s.charAt(i) == s.charAt(i - 1) &&
          (s.charAt(i) == '1' ||
           s.charAt(i) == '2'))
           dp[i + 1] = dp[i] + dp[i - 1];

       // Otherwise take the
       // previous value
       else
           dp[i + 1] = dp[i];
    }
    System.out.println(dp[n]);
}

// Driver code
public static void main(String[] args)
{
    String S = "0111022110";

    differentStrings(S);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function that prints the
# number of different strings
# that can be formed
def differentStrings(s):

    # Computing the length of
    # the given string
    n = len(s)

    dp = [0] * (n + 1)

    # Base case
    dp[0] = dp[1] = 1

    # Traverse the given string
    for i in range (1, n):

        # If two consecutive 1's
        # or 2's are present
        if (s[i] == s[i - 1] and
           (s[i] == '1' or
            s[i] == '2')):

            dp[i + 1] = dp[i] + dp[i - 1]

        # Otherwise take
        # the previous value
        else:
            dp[i + 1] = dp[i]

    print (dp[n])

# Driver Code
if __name__ == "__main__": 
    S = "0111022110"
    differentStrings(S)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Function that prints the
// number of different strings
// that can be formed
static void differentStrings(string s)
{

    // Computing the length of
    // the given string
    int n = s.Length;

    int[] dp = new int[n + 1];

    // Base case
    dp[0] = dp[1] = 1;

    // Traverse the given string
    for(int i = 1; i < n; i++)
    {

       // If two consecutive 1's
       // or 2's are present
       if (s[i] == s[i - 1] &&
          (s[i] == '1' ||
           s[i] == '2'))
           dp[i + 1] = dp[i] + dp[i - 1];

       // Otherwise take the
       // previous value
       else
           dp[i + 1] = dp[i];
    }
    Console.Write(dp[n]);
}

// Driver code
public static void Main()
{
    string S = "0111022110";

    differentStrings(S);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

// Function that prints the
// number of different strings
// that can be formed
function differentStrings(s)
{
    // Computing the length of
    // the given string
    var n = s.length;

    var dp = Array(n + 1);

    // Base case
    dp[0] = dp[1] = 1;

    // Traverse the given string
    for (var i = 1; i < n; i++) {

        // If two consecutive 1's
        // or 2's are present
        if (s[i] == s[i - 1]
            && (s[i] == '1'
                || s[i] == '2'))

            dp[i + 1]
                = dp[i] + dp[i - 1];

        // Otherwise take
        // the previous value
        else
            dp[i + 1] = dp[i];
    }

    document.write( dp[n] + "<br>");
}

// Driver Code
var S = "0111022110";
differentStrings(S);

</script>
```

**Output:** 

```
12
```

**时间复杂度:** *O(N)*