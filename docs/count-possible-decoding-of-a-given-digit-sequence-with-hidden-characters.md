# 计算带有隐藏字符的给定数字序列的可能解码次数

> 原文:[https://www . geeksforgeeks . org/给定数字序列的计数-可能解码-带隐藏字符/](https://www.geeksforgeeks.org/count-possible-decoding-of-a-given-digit-sequence-with-hidden-characters/)

给定一个包含数字和字符**' ***即隐藏字符的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到解码给定字符串的这个隐藏字符的方法数。

因为答案可能很大，所以返回**模** 10 <sup>9</sup> +7。

> 包含来自 **A-Z** 的字母的字符串[可以通过以下映射被**编码为数字:**](https://www.geeksforgeeks.org/string-data-structure/)
> 
> a '-> " 1 "
> ' B '->" 2 "
> ' C '->" 3 "
> ' D '->" 4 "
> ……
> ……
> ' Z '->" 26 "
> **注:**包含 0 的字符不像 **(J → 10)** 那样包含在问题中。

**示例:**

> **输入:**s =“*”
> **输出:** 9
> **解释:**编码消息可以表示编码消息“1”、“2”、“3”、“4”、“5”、“6”、“7”、“8”或“9”中的任何一个。
> 这些都可以分别解码为字符串“A”、“B”、“C”、“D”、“E”、“F”、“G”、“H”和“I”。
> 因此，共有 9 种解码“*”的方法。
> 
> **输入:** s = "1*"
> **输出:** 18
> **解释:**编码消息可以表示编码消息“11”、“12”、“13”、“14”、“15”、“16”、“17”、“18”或“19”中的任何一个。
> 这些编码消息中的每一个都有 2 种解码方式(例如，“11”可以解码为“AA”或“K”)。
> 因此，总共有 9 × 2 = 18 种解码“1*”的方法。

**进场:**

这个问题可以通过观察任何一个常数，如果 **(i-1)第**个字符是**【1】**或者 **(i-1)第**个字符是**【2】**和**个字符在 **1 和 6 之间，那么这个常数既可以被解码成一个一位数的字符，也可以被解码成一个两位数的数字来解决。**因此，当前状态依赖于之前的状态，[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。按照以下步骤解决问题:**

**1.让 **dp[i]** 表示从 **0** 到 **i** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)字符的解码方式数。**

**2.如果带有字符的**是**' *:******

*   ****dp[i] = dp[i-1]*9** 考虑到**' ***可以是 **1 到 9** ，单独作为一个人物考虑。**
*   **现在，如果将 **i** 和 **i-1** 字符组合起来，那么，

    *   如果 **(i-1)第**个字符是**' ***，那么这两个**“* ***在一起就可以形成 **15** 个可能的字符(就像 13 会形成字符‘M’)，所以我们在**DP【I】**上加上**15×DP【I-2】**。
    *   如果第 **(i-1)个**字符是 **'1'** ，那么 **dp[i] = dp[i] + 9×dp[i-2]** ，因为可以解码的可能字符是 **11 到 19** (K 到 S)。
    *   如果第 **(i-1)个**字符是 **'2'** ，那么 **dp[i] = dp[i] + 6×dp[i-2]** ，因为它可以取值从 **21 到 26。**** 

**3.如果带有字符的**不是**' *:******

*   ****dp[i] = dp[i] + dp[i-1]** 仅考虑带有字符的**作为数字。****
*   **现在，如果可以将第 **(i-1)个**字符和第个**字符组合在一起，那么将 **dp[i-2]添加到 dp[i]中。******

**下面是上述方法的实现:**

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

int M = 1000000007;
int waysOfDecoding(string s)
{

    vector<int> dp((int)s.size()+1);
    dp[0] = 1;

    // check the first character of the string
    // if it is '*' then 9 ways

    dp[1] = s[0] == '*'
                ? 9
                : s[0] == '0' ? 0 : 1;

    // traverse the string
    for (int i = 1; i < (int)s.size(); i++) {

        // If s[i] == '*' there can be
        // 9 possible values of *
        if (s[i] == '*') {
            dp[i + 1] = 9 * dp[i];

            // If previous character is 1
            // then words that can be formed
            // are K(11), L(12), M(13), N(14)
            // O(15), P(16), Q(17), R(18), S(19)
            if (s[i - 1] == '1')
                dp[i + 1]
                    = (dp[i + 1] + 9 * dp[i - 1]) % M;

            // If previous character is 2
            // then the words that can be formed
            // are U(21), V(22), W(23), X(24)Y(25), Z(26)
            else if (s[i - 1] == '2')
                dp[i + 1]
                    = (dp[i + 1] + 6 * dp[i - 1]) % M;

            // If the previous digit is * then
            // all 15 2- digit characters can be
            // formed
            else if (s[i - 1] == '*')
                dp[i + 1]
                    = (dp[i + 1] + 15 * dp[i - 1]) % M;
        }
        else {
            // taking the value from previous step
            dp[i + 1] = s[i] != '0' ? dp[i] : 0;

            // If previous character is 1 then
            // the i-1th character and ith
            // character can be decoded in
            // a single character therefore,
            // adding dp[i-1].
            if (s[i - 1] == '1')
                dp[i + 1]
                    = (dp[i + 1] + dp[i - 1])
                      % M;

            // If previous character is 2
            // and ith character is less than
            // 6
            // then the i-1th character and
            // ith character can be decoded in
            // a single character therefore,
            // adding dp[i-1].
            else if (s[i - 1] == '2'
                     && s[i] <= '6')
                dp[i + 1]
                    = (dp[i + 1] + dp[i - 1]) % M;

            // If previous character is * then
            // it will contain the above 2 cases
            else if (s[i - 1] == '*')
                dp[i + 1]
                    = (dp[i + 1]
                       + (s[i] <= '6' ? 2 : 1)
                             * dp[i - 1])
                      % M;
        }
    }
    return dp[(int)s.size()];
}

int main()
{
  string s = "12";
  cout<<waysOfDecoding(s);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.io.*;

class GFG {
    static int M = 1000000007;
    static int waysOfDecoding(String s)
    {

        long[] dp = new long[s.length() + 1];
        dp[0] = 1;

        // check the first character of the string
        // if it is '*' then 9 ways

        dp[1] = s.charAt(0) == '*'
                    ? 9
                    : s.charAt(0) == '0' ? 0 : 1;

        // traverse the string
        for (int i = 1; i < s.length(); i++) {

            // If s[i] == '*' there can be
            // 9 possible values of *
            if (s.charAt(i) == '*') {
                dp[i + 1] = 9 * dp[i];

                // If previous character is 1
                // then words that can be formed
                // are K(11), L(12), M(13), N(14)
                // O(15), P(16), Q(17), R(18), S(19)
                if (s.charAt(i - 1) == '1')
                    dp[i + 1]
                        = (dp[i + 1] + 9 * dp[i - 1]) % M;

                // If previous character is 2
                // then the words that can be formed
                // are U(21), V(22), W(23), X(24)Y(25), Z(26)
                else if (s.charAt(i - 1) == '2')
                    dp[i + 1]
                        = (dp[i + 1] + 6 * dp[i - 1]) % M;

                // If the previous digit is * then
                // all 15 2- digit characters can be
                // formed
                else if (s.charAt(i - 1) == '*')
                    dp[i + 1]
                        = (dp[i + 1] + 15 * dp[i - 1]) % M;
            }
            else {
                // taking the value from previous step
                dp[i + 1] = s.charAt(i) != '0' ? dp[i] : 0;

                // If previous character is 1 then
                // the i-1th character and ith
                // character can be decoded in
                // a single character therefore,
                // adding dp[i-1].
                if (s.charAt(i - 1) == '1')
                    dp[i + 1]
                        = (dp[i + 1] + dp[i - 1])
                          % M;

                // If previous character is 2
                // and ith character is less than
                // 6
                // then the i-1th character and
                // ith character can be decoded in
                // a single character therefore,
                // adding dp[i-1].
                else if (s.charAt(i - 1) == '2'
                         && s.charAt(i) <= '6')
                    dp[i + 1]
                        = (dp[i + 1] + dp[i - 1]) % M;

                // If previous character is * then
                // it will contain the above 2 cases
                else if (s.charAt(i - 1) == '*')
                    dp[i + 1]
                        = (dp[i + 1]
                           + (s.charAt(i) <= '6' ? 2 : 1)
                                 * dp[i - 1])
                          % M;
            }
        }
        return (int)dp[s.length()];
    }
    public static void main(String[] args)
    {
        String s = "12";
        System.out.println(waysOfDecoding(s));
    }
}
```

## **蟒蛇 3**

```
# Python program for the above approach
M = 1000000007
def waysOfDecoding(s):

    dp = [0]*(len(s)+1)
    dp[0] = 1

    # check the first character of the string
    # if it is '*' then 9 ways
    if s[0] == '*':
        dp[1] = 9
    elif s[0] == '0':
        dp[1] = 0
    else:
        dp[1] = 1

    # traverse the string
    for i in range(len(s)):

        # If s[i] == '*' there can be
        # 9 possible values of *
        if (s[i] == '*'):
            dp[i + 1] = 9 * dp[i]

            # If previous character is 1
            # then words that can be formed
            # are K(11), L(12), M(13), N(14)
            # O(15), P(16), Q(17), R(18), S(19)
            if (s[i - 1] == '1'):
                dp[i + 1] = (dp[i + 1] + 9 * dp[i - 1]) % M

            # If previous character is 2
            # then the words that can be formed
            # are U(21), V(22), W(23), X(24)Y(25), Z(26)
            elif (s[i - 1] == '2'):
                dp[i + 1] = (dp[i + 1] + 6 * dp[i - 1]) % M

            # If the previous digit is * then
            # all 15 2- digit characters can be
            # formed
            elif (s[i - 1] == '*'):
                dp[i + 1] = (dp[i + 1] + 15 * dp[i - 1]) % M

        else:
            # taking the value from previous step
            if s[i] != '0':
                dp[i+1] = dp[i]
            else:
                dp[i+1] = 0

            # If previous character is 1 then
            # the i-1th character and ith
            # character can be decoded in
            # a single character therefore,
            # adding dp[i-1].
            if (s[i - 1] == '1'):
                dp[i + 1] = (dp[i + 1] + dp[i - 1]) % M

            # If previous character is 2
            # and ith character is less than
            # 6
            # then the i-1th character and
            # ith character can be decoded in
            # a single character therefore,
            # adding dp[i-1].
            elif (s[i - 1] == '2'
                  and s[i] <= '6'):
                dp[i + 1] = (dp[i + 1] + dp[i - 1]) % M

            # If previous character is * then
            # it will contain the above 2 cases
            elif (s[i - 1] == '*'):
                if (s[i] <= '6'):
                    dp[i + 1] = dp[i + 1] + 2 * dp[i - 1]
                else:
                    dp[i + 1] = dp[i + 1] + 1 * dp[i - 1]

                dp[i+1] = dp[i+1] % M

    return dp[len(s)]

if __name__ == "__main__":

    s = "12"
    print(waysOfDecoding(s))

    # This code is contributed by ukasp.
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

static int M = 1000000007;
static int waysOfDecoding(String s)
{
    long[] dp = new long[s.Length + 1];
    dp[0] = 1;

    // Check the first character of the string
    // if it is '*' then 9 ways
    dp[1] = s[0] == '*' ? 9 : s[0] == '0' ? 0 : 1;

    // Traverse the string
    for(int i = 1; i < s.Length; i++)
    {

        // If s[i] == '*' there can be
        // 9 possible values of *
        if (s[i] == '*')
        {
            dp[i + 1] = 9 * dp[i];

            // If previous character is 1
            // then words that can be formed
            // are K(11), L(12), M(13), N(14)
            // O(15), P(16), Q(17), R(18), S(19)
            if (s[i - 1] == '1')
                dp[i + 1] = (dp[i + 1] + 9 *
                             dp[i - 1]) % M;

            // If previous character is 2
            // then the words that can be formed
            // are U(21), V(22), W(23), X(24)Y(25),
            // Z(26)
            else if (s[i - 1] == '2')
                dp[i + 1] = (dp[i + 1] + 6 *
                             dp[i - 1]) % M;

            // If the previous digit is * then
            // all 15 2- digit characters can be
            // formed
            else if (s[i - 1] == '*')
                dp[i + 1] = (dp[i + 1] + 15 *
                             dp[i - 1]) % M;
        }
        else
        {

            // Taking the value from previous step
            dp[i + 1] = s[i] != '0' ? dp[i] : 0;

            // If previous character is 1 then
            // the i-1th character and ith
            // character can be decoded in
            // a single character therefore,
            // adding dp[i-1].
            if (s[i - 1] == '1')
                dp[i + 1] = (dp[i + 1] + dp[i - 1]) % M;

            // If previous character is 2
            // and ith character is less than
            // 6
            // then the i-1th character and
            // ith character can be decoded in
            // a single character therefore,
            // adding dp[i-1].
            else if (s[i - 1] == '2' && s[i] <= '6')
                dp[i + 1] = (dp[i + 1] + dp[i - 1]) % M;

            // If previous character is * then
            // it will contain the above 2 cases
            else if (s[i - 1] == '*')
                dp[i + 1] = (dp[i + 1] + (s[i] <= '6' ? 2 : 1) *
                             dp[i - 1]) % M;
        }
    }
    return (int)dp[s.Length];
}

// Driver code
public static void Main()
{
    String s = "12";
    Console.WriteLine(waysOfDecoding(s));
}
}

// This code is contributed by rishavmahato348
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

let M = 1000000007;
function waysOfDecoding(s)
{
    let dp = new Array(s.length + 1);
    for(let i=0;i<s.length+1;i++)
        dp[i] = 0;
        dp[0] = 1;

        // check the first character of the string
        // if it is '*' then 9 ways

        dp[1] = s[0] == '*'
                    ? 9
                    : s[0] == '0' ? 0 : 1;

        // traverse the string
        for (let i = 1; i < s.length; i++) {

            // If s[i] == '*' there can be
            // 9 possible values of *
            if (s[i] == '*') {
                dp[i + 1] = 9 * dp[i];

                // If previous character is 1
                // then words that can be formed
                // are K(11), L(12), M(13), N(14)
                // O(15), P(16), Q(17), R(18), S(19)
                if (s[i-1] == '1')
                    dp[i + 1]
                        = (dp[i + 1] + 9 * dp[i - 1]) % M;

                // If previous character is 2
                // then the words that can be formed
                // are U(21), V(22), W(23), X(24)Y(25), Z(26)
                else if (s[i-1] == '2')
                    dp[i + 1]
                        = (dp[i + 1] + 6 * dp[i - 1]) % M;

                // If the previous digit is * then
                // all 15 2- digit characters can be
                // formed
                else if (s[i-1] == '*')
                    dp[i + 1]
                        = (dp[i + 1] + 15 * dp[i - 1]) % M;
            }
            else {
                // taking the value from previous step
                dp[i + 1] = s[i] != '0' ? dp[i] : 0;

                // If previous character is 1 then
                // the i-1th character and ith
                // character can be decoded in
                // a single character therefore,
                // adding dp[i-1].
                if (s[i-1] == '1')
                    dp[i + 1]
                        = (dp[i + 1] + dp[i - 1])
                          % M;

                // If previous character is 2
                // and ith character is less than
                // 6
                // then the i-1th character and
                // ith character can be decoded in
                // a single character therefore,
                // adding dp[i-1].
                else if (s[i-1] == '2'
                         && s[i] <= '6')
                    dp[i + 1]
                        = (dp[i + 1] + dp[i - 1]) % M;

                // If previous character is * then
                // it will contain the above 2 cases
                else if (s[i-1] == '*')
                    dp[i + 1]
                        = (dp[i + 1]
                           + (s[i] <= '6' ? 2 : 1)
                                 * dp[i - 1])
                          % M;
            }
        }
        return dp[s.length];
}

let s = "12";
document.write(waysOfDecoding(s));

// This code is contributed by unknown2108
</script>
```

****Output**

```
2
```** 

*****时间复杂度:**O(n)*
T5**辅助空间:** O(n)**

****空间的进一步优化****

**如果仔细观察上述代码，可以发现 **dp[i]** 的值是使用 **dp[i-1]** 和 **dp[i-2]** 找到的。因此，为了进一步优化空间，我们可以使用三个变量–**第二个**(存储 **dp[i]** 的值)、**第一个**(存储 **dp[i-2]** 的值)和**温度**(存储 **dp[i-1]的值)，而不是创建长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)所以在找到**秒(dp[i])** 的值后，修改 **first = temp** 和 **temp = second** ，然后使用变量 **first** 和 **temp** 再次计算**秒(dp[i])** 的值。****

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int M = 1000000007;
int waysOfDecoding(string s)
{
    long first = 1,
    second = s[0] == '*' ? 9 : s[0] == '0' ? 0 : 1;

    for(int i = 1; i < s.size(); i++)
    {
        long temp = second;

        // If s[i] == '*' there can be
        // 9 possible values of *
        if (s[i] == '*')
        {
            second = 9 * second;

            // If previous character is 1
            // then words that can be formed
            // are K(11), L(12), M(13), N(14)
            // O(15), P(16), Q(17), R(18), S(19)
            if (s[i - 1] == '1')
                second = (second + 9 * first) % M;

            // If previous character is 2
            // then the words that can be formed
            // are U(21), V(22), W(23), X(24)Y(25), Z(26)
            else if (s[i - 1] == '2')
                second = (second + 6 * first) % M;

            // If the previous digit is * then
            // all 15 2- digit characters can be
            // formed
            else if (s[i - 1] == '*')
                second = (second + 15 * first) % M;
        }

        // If s[i] != '*'
        else
        {
            second = s[i] != '0' ? second : 0;

            // Adding first in second
            // if s[i-1]=1
            if (s[i - 1] == '1')
                second = (second + first) % M;

            // Adding first in second if
            // s[i-1] == 2 and s[i]<='6'
            else if (s[i - 1] == '2' && s[i] <= '6')
                second = (second + first) % M;

            // If s[i-1] == '*' the union
            // of above 2 cases has to be done
            else if (s[i - 1] == '*')
                second = (second + (s[i] <= '6' ? 2 : 1) *
                          first) % M;
        }
        first = temp;
    }
    return(int)second;
}

// Driver code
int main()
{
    string s = "*";
    cout << waysOfDecoding(s);
    return 0;
}

// This code is contributed by rishavmahato348
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG {
    static int M = 1000000007;
    static int waysOfDecoding(String s)
    {
        long first = 1, second
                        = s.charAt(0) == '*'
                              ? 9
                              : s.charAt(0) == '0' ? 0 : 1;
        for (int i = 1; i < s.length(); i++) {
            long temp = second;

            // If s[i] == '*' there can be
            // 9 possible values of *
            if (s.charAt(i) == '*') {
                second = 9 * second;

                // If previous character is 1
                // then words that can be formed
                // are K(11), L(12), M(13), N(14)
                // O(15), P(16), Q(17), R(18), S(19)
                if (s.charAt(i - 1) == '1')
                    second = (second + 9 * first) % M;

                // If previous character is 2
                // then the words that can be formed
                // are U(21), V(22), W(23), X(24)Y(25), Z(26)
                else if (s.charAt(i - 1) == '2')
                    second = (second + 6 * first) % M;

                // If the previous digit is * then
                // all 15 2- digit characters can be
                // formed
                else if (s.charAt(i - 1) == '*')
                    second = (second + 15 * first) % M;
            }
            // If s[i] != '*'
            else {
                second = s.charAt(i) != '0' ? second : 0;

                // Adding first in second
                // if s[i-1]=1
                if (s.charAt(i - 1) == '1')
                    second = (second + first) % M;

                // Adding first in second if
                // s[i-1] == 2 and s[i]<='6'
                else if (s.charAt(i - 1) == '2'
                         && s.charAt(i) <= '6')
                    second = (second + first) % M;

                // if s[i-1] == '*' the union
                // of above 2 cases has to be done
                else if (s.charAt(i - 1) == '*')
                    second = (second
                              + (s.charAt(i) <= '6' ? 2 : 1)
                                    * first)
                             % M;
            }
            first = temp;
        }
        return (int)second;
    }
    public static void main(String[] args)
    {
        String s = "*";
        System.out.println(waysOfDecoding(s));
    }
}
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

static int M = 1000000007;

static int waysOfDecoding(string s)
{
    long first = 1,
    second = s[0] == '*' ? 9 : s[0] == '0' ? 0 : 1;
    for(int i = 1; i < s.Length; i++)
    {
        long temp = second;

        // If s[i] == '*' there can be
        // 9 possible values of *
        if (s[i] == '*')
        {
            second = 9 * second;

            // If previous character is 1
            // then words that can be formed
            // are K(11), L(12), M(13), N(14)
            // O(15), P(16), Q(17), R(18), S(19)
            if (s[i - 1] == '1')
                second = (second + 9 * first) % M;

            // If previous character is 2
            // then the words that can be formed
            // are U(21), V(22), W(23), X(24)Y(25), Z(26)
            else if (s[i - 1] == '2')
                second = (second + 6 * first) % M;

            // If the previous digit is * then
            // all 15 2- digit characters can be
            // formed
            else if (s[i - 1] == '*')
                second = (second + 15 * first) % M;
        }

        // If s[i] != '*'
        else
        {
            second = s[i] != '0' ? second : 0;

            // Adding first in second
            // if s[i-1]=1
            if (s[i - 1] == '1')
                second = (second + first) % M;

            // Adding first in second if
            // s[i-1] == 2 and s[i]<='6'
            else if (s[i - 1] == '2' && s[i] <= '6')
                second = (second + first) % M;

            // if s[i-1] == '*' the union
            // of above 2 cases has to be done
            else if (s[i - 1] == '*')
                second = (second + (s[i] <= '6' ? 2 : 1) *
                          first) % M;
        }
        first = temp;
    }
    return (int)second;
}

// Driver code
static public void Main()
{
    string s = "*";

    Console.WriteLine(waysOfDecoding(s));
}
}

// This code is contributed by patel2127
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach
let M = 1000000007;

function waysOfDecoding(s)
{
    let first = 1,
    second = s[0] == '*' ? 9 : s[0] == '0' ? 0 : 1;
    for(let i = 1; i < s.length; i++)
    {
        let temp = second;

        // If s[i] == '*' there can be
        // 9 possible values of *
        if (s[i] == '*')
        {
            second = 9 * second;

            // If previous character is 1
            // then words that can be formed
            // are K(11), L(12), M(13), N(14)
            // O(15), P(16), Q(17), R(18), S(19)
            if (s[i - 1] == '1')
                second = (second + 9 * first) % M;

            // If previous character is 2
            // then the words that can be formed
            // are U(21), V(22), W(23), X(24)Y(25), Z(26)
            else if (s[i - 1] == '2')
                second = (second + 6 * first) % M;

            // If the previous digit is * then
            // all 15 2- digit characters can be
            // formed
            else if (s[i - 1] == '*')
                second = (second + 15 * first) % M;
        }

        // If s[i] != '*'
        else
        {
            second = s[i] != '0' ? second : 0;

            // Adding first in second
            // if s[i-1]=1
            if (s[i - 1] == '1')
                second = (second + first) % M;

            // Adding first in second if
            // s[i-1] == 2 and s[i]<='6'
            else if (s[i - 1] == '2' && s[i] <= '6')
                second = (second + first) % M;

            // if s[i-1] == '*' the union
            // of above 2 cases has to be done
            else if (s[i - 1] == '*')
                second = (second + (s[i] <= '6' ? 2 : 1) *
                          first) % M;
        }
        first = temp;
    }
    return second;
}

// Driver Code
let s = "*";

document.write(waysOfDecoding(s));

// This code is contributed by code_hunt

</script>
```

****Output**

```
9
```** 

*****时间复杂度:**O(n)*
T5**辅助空间:** O(1)**