# 对二进制串 S 求和所需的最小运算次数

> 原文:[https://www . geesforgeks . org/最小操作数-要求将二进制字符串求和-s/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-sum-to-binary-string-s/)

给定一个二进制字符串，求数字**零**上需要执行的最小操作数，将其转换为 s
表示的数字。允许执行两种类型的操作:

*   **增加** 2 <sup>x</sup>
*   **减去** 2 <sup>x</sup>

**注意**:开始对 0 进行操作。

**示例:**

> **输入:** 100
> **输出:** 1
> **解释**:我们只执行一个操作，即加 4 (2^2)
> 
> **输入:** 111
> **输出:** 2
> **解释**:我们执行以下两个操作:
> 1)加 8(2^3)
> 2)减 1(2^0)

思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。
**注**:在下面的分析中，我们考虑到所有的二进制字符串都是从 LSB 到 MSB(从 LHS 到 RHS)表示的，即 2(二进制形式:“10”)表示为“01”。
让给定的二进制字符串为 S。
让 **dp[i][0]** 表示生成二进制字符串 R 所需的最小操作数，使得 R[0…i]与 S[0…i]相同，R[i+1…] = "00..0"
类似地，让 **dp[i][1]** 表示生成二进制字符串 R 所需的最小操作数，使得 R[0…i]与 S[0…i]和 R[i+1…] = "11 相同..1"
如果 S <sub>i</sub> 为‘0’，则 DP[I][0]= DP[I–1][0]。因为我们不需要任何额外的操作。现在我们考虑 dp[i][1]的值，这有点棘手。对于 dp[i][1]，我们可以从 DP[I–1][1]开始转换，只需将 dp[i-1][1]形成的字符串的第 I<sup>个字符设为“0”。从早些时候开始，我的第一个字是“1”。我们只需要从 dp[i-1][0]表示的字符串中减去 2 <sup>i</sup> 。因此，我们执行一个不同于 dp[i-1][0]表示的操作。
另一个转变可能来自 dp[i-1][0]。让 dp[i-1][1]代表字符串 R。然后我们需要保持 R[i] = 0，因为它已经是，但是 R[i + 1…..]当前为“000..0”，需要改为“111…1”，这可以通过从 r 中减去 2 <sup>(i+1)</sup> 来完成，因此我们只需要 dp[i-1][0]表示的操作之外的一个操作。
类似 S <sub>i</sub> 为‘1’的情况。
最终答案是 dp[l-1][0]表示的答案，其中 l 是二进制字符串 s 的长度。
下面是上述方法的实现:</sup>

## C++

```
// CPP program to find the minimum number
// of operations required to sum to N
#include <bits/stdc++.h>

using namespace std;

// Function to return the minimum operations required
// to sum to a number represented by the binary string S
int findMinOperations(string S)
{
    // Reverse the string to consider
    // it from LSB to MSB
    reverse(S.begin(), S.end());
    int n = S.length();

    // initialise the dp table
    int dp[n + 1][2];

    // If S[0] = '0', there is no need to
    // perform any operation
    if (S[0] == '0') {
        dp[0][0] = 0;
    }

    else {
        // If S[0] = '1', just perform a single
        // operation(i.e Add 2^0)
        dp[0][0] = 1;
    }

    // Irrespective of the LSB, dp[0][1] is always
    // 1 as there is always the need of making the
    // suffix of the binary string of the form "11....1"
    // as suggested by the definition of dp[i][1]
    dp[0][1] = 1;

    for (int i = 1; i < n; i++) {
        if (S[i] == '0') {

            // Transition from dp[i - 1][0]
            dp[i][0] = dp[i - 1][0];

            /* 1\. Transition from dp[i - 1][1] by just doing
                  1 extra operation of subtracting 2^i
               2\. Transition from dp[i - 1][0] by just doing
                  1 extra operation of subtracting 2^(i+1) */
            dp[i][1] = 1 + min(dp[i - 1][1], dp[i - 1][0]);
        }
        else {

            // Transition from dp[i - 1][1]
            dp[i][1] = dp[i - 1][1];

            /* 1\. Transition from dp[i - 1][1] by just doing
                  1 extra operation of adding 2^(i+1)
               2\. Transition from dp[i - 1][0] by just doing
                  1 extra operation of adding 2^i */
            dp[i][0] = 1 + min(dp[i - 1][0], dp[i - 1][1]);
        }
    }

    return dp[n - 1][0];
}

// Driver Code
int main()
{
    string S = "100";
    cout << findMinOperations(S) << endl;

    S = "111";
    cout << findMinOperations(S) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of operations required to sum to N

class GFG
{

    // Function to return the minimum operations required
    // to sum to a number represented by the binary string S
    static int findMinOperations(String S)
    {

        // Reverse the string to consider
        // it from LSB to MSB
        S = reverse(S);
        int n = S.length();

        // initialise the dp table
        int dp[][] = new int[n + 1][2];

        // If S[0] = '0', there is no need to
        // perform any operation
        if (S.charAt(0) == '0')
        {
            dp[0][0] = 0;
        }
        else
        {
            // If S[0] = '1', just perform a single
            // operation(i.e Add 2^0)
            dp[0][0] = 1;
        }

        // Irrespective of the LSB, dp[0][1] is always
        // 1 as there is always the need of making the
        // suffix of the binary string of the form "11....1"
        // as suggested by the definition of dp[i][1]
        dp[0][1] = 1;

        for (int i = 1; i < n; i++)
        {
            if (S.charAt(i) == '0')
            {
                // Transition from dp[i - 1][0]
                dp[i][0] = dp[i - 1][0];

                /* 1\. Transition from dp[i - 1][1] by just doing
                1 extra operation of subtracting 2^i
                2\. Transition from dp[i - 1][0] by just doing
                1 extra operation of subtracting 2^(i+1) */
                dp[i][1] = 1 + Math.min(dp[i - 1][1], dp[i - 1][0]);
            }
            else
            {

                // Transition from dp[i - 1][1]
                dp[i][1] = dp[i - 1][1];

                /* 1\. Transition from dp[i - 1][1] by just doing
                1 extra operation of adding 2^(i+1)
                2\. Transition from dp[i - 1][0] by just doing
                1 extra operation of adding 2^i */
                dp[i][0] = 1 + Math.min(dp[i - 1][0], dp[i - 1][1]);
            }
        }

        return dp[n - 1][0];
    }

    static String reverse(String input)
    {
        char[] temparray = input.toCharArray();
        int left, right = 0;
        right = temparray.length - 1;
        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.valueOf(temparray);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "100";
        System.out.println(findMinOperations(S));
        S = "111";
        System.out.println(findMinOperations(S));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of operations required to sum to N

# Function to return the minimum
# operations required to sum to a
# number represented by the binary string S
def findMinOperations(S) :

    # Reverse the string to consider
    # it from LSB to MSB
    S = S[: : -1]
    n = len(S)

    # initialise the dp table
    dp = [[0] * 2] * (n + 1)

    # If S[0] = '0', there is no need
    # to perform any operation
    if (S[0] == '0') :
        dp[0][0] = 0

    else :

        # If S[0] = '1', just perform a
        # single operation(i.e Add 2^0)
        dp[0][0] = 1

    # Irrespective of the LSB, dp[0][1] is
    # always 1 as there is always the need
    # of making the suffix of the binary
    # string of the form "11....1" as
    # suggested by the definition of dp[i][1]
    dp[0][1] = 1

    for i in range(1, n) :

        if (S[i] == '0') :

            # Transition from dp[i - 1][0]
            dp[i][0] = dp[i - 1][0]

            """
            1\. Transition from dp[i - 1][1]
                by just doing 1 extra operation
                of subtracting 2^i
            2\. Transition from dp[i - 1][0] by
                just doing 1 extra operation of
                subtracting 2^(i+1)
            """
            dp[i][1] = 1 + min(dp[i - 1][1],
                               dp[i - 1][0])

        else :

            # Transition from dp[i - 1][1]
            dp[i][1] = dp[i - 1][1];

            """
            1\. Transition from dp[i - 1][1] by
                just doing 1 extra operation
                of adding 2^(i+1)
            2\. Transition from dp[i - 1][0] by
                just doing 1 extra operation
                of adding 2^i
            """
            dp[i][0] = 1 + min(dp[i - 1][0],
                               dp[i - 1][1])

    return dp[n - 1][0]

# Driver Code
if __name__ == "__main__" :

    S = "100"
    print(findMinOperations(S))

    S = "111";
    print(findMinOperations(S))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the minimum number
// of operations required to sum to N
using System;

class GFG
{

    // Function to return the minimum
    // operations required to sum
    // to a number represented by
    // the binary string S
    static int findMinOperations(String S)
    {

        // Reverse the string to consider
        // it from LSB to MSB
        S = reverse(S);
        int n = S.Length;

        // initialise the dp table
        int [,]dp = new int[n + 1, 2];

        // If S[0] = '0', there is no need to
        // perform any operation
        if (S[0] == '0')
        {
            dp[0, 0] = 0;
        }
        else
        {
            // If S[0] = '1', just perform a single
            // operation(i.e Add 2^0)
            dp[0, 0] = 1;
        }

        // Irrespective of the LSB, dp[0,1] is always
        // 1 as there is always the need of making the
        // suffix of the binary string of the form "11....1"
        // as suggested by the definition of dp[i,1]
        dp[0, 1] = 1;

        for (int i = 1; i < n; i++)
        {
            if (S[i] == '0')
            {
                // Transition from dp[i - 1,0]
                dp[i, 0] = dp[i - 1, 0];

                /* 1\. Transition from dp[i - 1,1] by just doing
                1 extra operation of subtracting 2^i
                2\. Transition from dp[i - 1,0] by just doing
                1 extra operation of subtracting 2^(i+1) */
                dp[i, 1] = 1 + Math.Min(dp[i - 1, 1], dp[i - 1, 0]);
            }
            else
            {

                // Transition from dp[i - 1,1]
                dp[i, 1] = dp[i - 1, 1];

                /* 1\. Transition from dp[i - 1,1] by just doing
                1 extra operation of adding 2^(i+1)
                2\. Transition from dp[i - 1,0] by just doing
                1 extra operation of adding 2^i */
                dp[i, 0] = 1 + Math.Min(dp[i - 1, 0], dp[i - 1, 1]);
            }
        }
        return dp[n - 1, 0];
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;
        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver Code
    public static void Main()
    {
        String S = "100";
        Console.WriteLine(findMinOperations(S));
        S = "111";
        Console.WriteLine(findMinOperations(S));
    }
}

//This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum number
// of operations required to sum to N

// Function to return the minimum operations required
// to sum to a number represented by the binary string S
function findMinOperations($S)
{
    // Reverse the string to consider
    // it from LSB to MSB
    $p= strrev($S);
    $n = strlen($p);

    // initialise the dp table
    $dp = array_fill(0,$n + 1,array_fill(0,2,NULL));

    // If S[0] = '0', there is no need to
    // perform any operation
    if ($p[0] == '0') {
        $dp[0][0] = 0;
    }

    else {
        // If S[0] = '1', just perform a single
        // operation(i.e Add 2^0)
        $dp[0][0] = 1;
    }

    // Irrespective of the LSB, dp[0][1] is always
    // 1 as there is always the need of making the
    // suffix of the binary string of the form "11....1"
    // as suggested by the definition of dp[i][1]
    $dp[0][1] = 1;

    for ($i = 1; $i < $n; $i++) {
        if ($p[$i] == '0') {

            // Transition from dp[i - 1][0]
            $dp[$i][0] = $dp[$i - 1][0];

            /* 1\. Transition from dp[i - 1][1] by just doing
                  1 extra operation of subtracting 2^i
               2\. Transition from dp[i - 1][0] by just doing
                  1 extra operation of subtracting 2^(i+1) */
            $dp[$i][1] = 1 + min($dp[$i - 1][1], $dp[$i - 1][0]);
        }
        else {

            // Transition from dp[i - 1][1]
            $dp[$i][1] = $dp[$i - 1][1];

            /* 1\. Transition from dp[i - 1][1] by just doing
                  1 extra operation of adding 2^(i+1)
               2\. Transition from dp[i - 1][0] by just doing
                  1 extra operation of adding 2^i */
            $dp[$i][0] = 1 + min($dp[$i - 1][0], $dp[$i - 1][1]);
        }
    }

    return $dp[$n - 1][0];
}

// Driver Code

$S = "100";
echo findMinOperations($S)."\n";

$S = "111";
echo findMinOperations($S)."\n";

return 0;

// This code is contributed by Ita_c.
?>
```

## java 描述语言

```
<script>
// Javascript program to find the minimum number
// of operations required to sum to N

    // Function to return the minimum operations required
    // to sum to a number represented by the binary string S
    function findMinOperations(S)
    {
        // Reverse the string to consider
        // it from LSB to MSB
        S = reverse(S);
        let n = S.length;

        // initialise the dp table
        let dp = new Array(n + 1);
        for(let i=0;i<dp.length;i++)
        {
            dp[i]=new Array(2);
            for(let j=0;j<2;j++)
            {
                dp[i][j]=0;
            }
        }

        // If S[0] = '0', there is no need to
        // perform any operation
        if (S[0] == '0')
        {
            dp[0][0] = 0;
        }
        else
        {
            // If S[0] = '1', just perform a single
            // operation(i.e Add 2^0)
            dp[0][0] = 1;
        }

        // Irrespective of the LSB, dp[0][1] is always
        // 1 as there is always the need of making the
        // suffix of the binary string of the form "11....1"
        // as suggested by the definition of dp[i][1]
        dp[0][1] = 1;

        for (let i = 1; i < n; i++)
        {
            if (S[i] == '0')
            {
                // Transition from dp[i - 1][0]
                dp[i][0] = dp[i - 1][0];

                /* 1\. Transition from dp[i - 1][1] by just doing
                1 extra operation of subtracting 2^i
                2\. Transition from dp[i - 1][0] by just doing
                1 extra operation of subtracting 2^(i+1) */
                dp[i][1] = 1 + Math.min(dp[i - 1][1], dp[i - 1][0]);
            }
            else
            {

                // Transition from dp[i - 1][1]
                dp[i][1] = dp[i - 1][1];

                /* 1\. Transition from dp[i - 1][1] by just doing
                1 extra operation of adding 2^(i+1)
                2\. Transition from dp[i - 1][0] by just doing
                1 extra operation of adding 2^i */
                dp[i][0] = 1 + Math.min(dp[i - 1][0], dp[i - 1][1]);
            }
        }

        return dp[n - 1][0];
    }

    function reverse(input)
    {
        let temparray = input.split("");
        let left, right = 0;
        right = temparray.length - 1;
        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            let temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return (temparray).join("");
    }

    // Driver Code
    let S = "100";
    document.write(findMinOperations(S)+"<br>");

    S = "111";
    document.write(findMinOperations(S)+"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1
2
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)