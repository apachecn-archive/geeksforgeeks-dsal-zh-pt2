# 通过替换外卡，使回文二进制串恰好为 a 0 和 b 1？

> 原文:[https://www . geesforgeks . org/make-回文-binary-string-with-a-0s-和-b-1s-by-replace-wild-card/](https://www.geeksforgeeks.org/make-palindrome-binary-string-with-exactly-a-0s-and-b-1s-by-replacing-wild-card/)

给定一串由**“？”组成的 **N** 字符的[T2 S](https://www.geeksforgeeks.org/stdstring-class-in-c/)**、“ **0** ”、“ **1** 和两个整数 **a** 和 **b** ，任务是通过替换“**”找到一个与**a**T20】0s**和 **b** **1s** 完全一致的[回文二进制字符串？带“ **0** 或“ **1** ”。](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)

**示例:**

> ***输入:*** *S = "10？？？？？1 "，a = 4，b = 4*
> ***输出:****10100101*
> ***解释:*** *输出字符串是一个回文二进制字符串，正好有 4 个 0 和 4 个 1 .*
> 
> ***输入:*** *S =？？？？？?"，a = 5，b = 1*
> ***输出:****-1*
> ***解释:*** *不存在任何一个回文串恰好有 0 和 b 的 1 .*

**方法:**给定的问题可以通过使用以下观察值来解决:

*   要使 **N** 字符的字符串 **S** 成为回文， **S[i] = S[N-i-1]** 必须对范围**【0，N)** 内的所有 **i** 值有效。
*   如果 **S[i]** 和 **S[N-i-1]** 中只有一个等于'**？**’，则必须替换为其他索引的对应字符。
*   如果 **S[i]** 和 **S[N-i-1]** 的值都是'**？**’，最理想的选择是用需要计数较多的字符替换两者。

根据上述观察，按照以下步骤解决问题:

*   遍历**【0，N/2)** 范围内的字符串，对于**S【I】**和**S【N–I–1】**中只有一个等于“**的情况？**'，替换为对应的字符。
*   通过减去上述操作后的“ **0** ”和“ **1** 的计数，更新 **a** 和 **b** 的值。使用 [std::count](https://www.geeksforgeeks.org/std-count-cpp-stl/) 功能可以轻松计算计数。
*   现在遍历范围**【0，N/2)** 内的给定字符串，如果两个 **S[i] =** ' **？**'和**S【N-I-1】**= '**？**'，用需要计数较多的字符更新它们的值(即如果 **a > b** 则用“ **0** ”否则用“ **1** ”)。
*   中间字符为“**”的奇数字符串长度的情况下？**'，用剩余计数的字符更新。
*   如果 **a = 0** 和 **b = 0** 的值，则存储在 **S** 中的字符串是所需的字符串。否则，所需字符串不存在，因此返回 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert the given string
// to a palindrome with a 0's and b 1's
string convertString(string S, int a, int b)
{
    // Stores the size of the string
    int N = S.size();

    // Loop to iterate over the string
    for (int i = 0; i < N / 2; ++i) {

        // If one of S[i] or S[N-i-1] is
        // equal to '?', replace it with
        // corresponding character
        if (S[i] == '?'
            && S[N - i - 1] != '?') {
            S[i] = S[N - i - 1];
        }
        else if (S[i] != '?'
                 && S[N - i - 1] == '?') {
            S[N - i - 1] = S[i];
        }
    }

    // Subtract the count of 0 from the
    // required number of zeroes
    a = a - count(S.begin(), S.end(), '0');

    // Subtract the count of 1 from
    // required number of ones
    b = b - count(S.begin(), S.end(), '1');

    // Traverse the string
    for (int i = 0; i < N / 2; ++i) {

        // If both S[i] and S[N-i-1] are '?'
        if (S[i] == '?' && S[N - i - 1] == '?') {

            // If a is greater than b
            if (a > b) {

                // Update S[i] and S[N-i-1] to '0'
                S[i] = S[N - i - 1] = '0';

                // Update the value of a
                a -= 2;
            }
            else {

                // Update S[i] and S[N-i-1] to '1'
                S[i] = S[N - i - 1] = '1';

                // Update the value of b
                b -= 2;
            }
        }
    }

    // Case with middle character '?'
    // in case of odd length string
    if (S[N / 2] == '?') {

        // If a is greater than b
        if (a > b) {

            // Update middle character
            // with '0'
            S[N / 2] = '0';
            a--;
        }
        else {

            // Update middle character
            // by '1'
            S[N / 2] = '1';
            b--;
        }
    }

    // Return Answer
    if (a == 0 && b == 0) {
        return S;
    }
    else {
        return "-1";
    }
}

// Driver Code
int main()
{
    string S = "10?????1";
    int a = 4, b = 4;

    cout << convertString(S, a, b);

    return 0;
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to convert the given string
# to a palindrome with a 0's and b 1's
def convertString(S, a, b):
    print(S)

    # Stores the size of the string
    N = len(S)

    # Loop to iterate over the string
    for i in range(0, N // 2):

        # If one of S[i] or S[N-i-1] is
        # equal to '?', replace it with
        # corresponding character
        if (S[i] == '?' and S[N - i - 1] != '?'):
            S[i] = S[N - i - 1]
        elif (S[i] != '?' and S[N - i - 1] == '?'):
            S[N - i - 1] = S[i]

    # Subtract the count of 0 from the
    # required number of zeroes
    cnt_0 = 0
    for i in range(0, N):
        if (S[i] == '0'):
            cnt_0 += 1

    a = a - cnt_0

    # Subtract the count of 1 from
    # required number of ones
    cnt_1 = 0

    for i in range(0, N):
        if (S[i] == '0'):
             cnt_1 += 1

    b = b - cnt_1

        # Traverse the string
    for i in range(0, N // 2):

        # If both S[i] and S[N-i-1] are '?'
        if (S[i] == '?' and S[N - i - 1] == '?'):

            # If a is greater than b
            if (a > b):

                # Update S[i] and S[N-i-1] to '0'
                S[i] = S[N - i - 1] = '0'

                # Update the value of a
                a -= 2
            else:

                # Update S[i] and S[N-i-1] to '1'
                S[i] = S[N - i - 1] = '1'

                # Update the value of b
                b -= 2

    # Case with middle character '?'
    # in case of odd length string
    if (S[N // 2] == '?'):

            # If a is greater than b
            if (a > b):

                # Update middle character
                # with '0'
                S[N // 2] = '0'
                a -= 1
            else:

                # Update middle character
                # by '1'
                S[N // 2] = '1'
                b -= 1

    # Return Answer
    if (a == 0 and b == 0):
            return S
    else:
            return "-1"

# Driver Code
S = "10?????1"
S = list(S)
a = 4
b = 4

print("".join(convertString(S, a, b)))

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to convert the given string
    // to a palindrome with a 0's and b 1's
    const convertString = (S, a, b) => {
        // Stores the size of the string
        let N = S.length;

        // Loop to iterate over the string
        for (let i = 0; i < parseInt(N / 2); ++i) {

            // If one of S[i] or S[N-i-1] is
            // equal to '?', replace it with
            // corresponding character
            if (S[i] == '?'
                && S[N - i - 1] != '?') {
                S[i] = S[N - i - 1];
            }
            else if (S[i] != '?'
                && S[N - i - 1] == '?') {
                S[N - i - 1] = S[i];
            }
        }

        // Subtract the count of 0 from the
        // required number of zeroes
        let cnt_0 = 0;
        for (let i = 0; i < N; ++i) {
            if (S[i] == '0') cnt_0++;
        }
        a = a - cnt_0;

        // Subtract the count of 1 from
        // required number of ones
        let cnt_1 = 0;
        for (let i = 0; i < N; ++i) {
            if (S[i] == '0') cnt_1++;
        }
        b = b - cnt_1;

        // Traverse the string
        for (let i = 0; i < parseInt(N / 2); ++i) {

            // If both S[i] and S[N-i-1] are '?'
            if (S[i] == '?' && S[N - i - 1] == '?') {

                // If a is greater than b
                if (a > b) {

                    // Update S[i] and S[N-i-1] to '0'
                    S[i] = S[N - i - 1] = '0';

                    // Update the value of a
                    a -= 2;
                }
                else {

                    // Update S[i] and S[N-i-1] to '1'
                    S[i] = S[N - i - 1] = '1';

                    // Update the value of b
                    b -= 2;
                }
            }
        }

        // Case with middle character '?'
        // in case of odd length string
        if (S[parseInt(N / 2)] == '?') {

            // If a is greater than b
            if (a > b) {

                // Update middle character
                // with '0'
                S[parseInt(N / 2)] = '0';
                a--;
            }
            else {

                // Update middle character
                // by '1'
                S[parseInt(N / 2)] = '1';
                b--;
            }
        }

        // Return Answer
        if (a == 0 && b == 0) {
            return S;
        }
        else {
            return "-1";
        }
    }

    // Driver Code
    let S = "10?????1";
    S = S.split('');
    let a = 4, b = 4;

    document.write(convertString(S, a, b).join(''));

// This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
10100101
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)