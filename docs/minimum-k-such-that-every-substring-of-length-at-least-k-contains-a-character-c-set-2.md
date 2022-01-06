# 最小 K，使得长度至少为 K 的每个子串包含一个字符 c | Set-2

> 原文:[https://www . geesforgeks . org/minimum-k-so-长度至少为-k-的每个子串都包含一个字符-c-set-2/](https://www.geeksforgeeks.org/minimum-k-such-that-every-substring-of-length-at-least-k-contains-a-character-c-set-2/)

给定一个由 **N** 个小写英文字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，同时也给定一个字符 **C** 叫做**K-惊人的**，如果每个长度至少为 **K** 的子串都包含这个字符 **C，**的任务是找到最小可能的 **K** 使得至少存在一个**K-惊人的**字符。

**示例:**

> ***输入:** S = "abcde"*
> ***输出:** 3*
> ***解释:***
> *每一个，长度至少为 3 的子串，都有一个 K-惊艳字符，‘c’:{“ABC”、“bcd”、“cde”、“abcd”、“bcde”、“abcde”}。*
> 
> ***输入:** S = "aaaa"*
> ***输出:** 1*
> ***解释:***
> *每一个，长度至少为 1 的子串，都有一个 K-惊艳字符，‘a’:{“a”、“aa”、“aaa”、“AAAA”}。*

对于天真和二分搜索法的方法，请参考 [**第 1 集**](https://www.geeksforgeeks.org/minimum-k-such-that-every-substring-of-length-atleast-k-contains-a-character-c/)

**方法:**可以基于以下观察来优化朴素方法:对于长度为 **K** 的每个子串中存在的字符“ **C** ，两个连续的“ **C** 的位置之间的距离不能超过 **K** 。按照以下步骤解决问题:

*   初始化一个整数变量，比如说 **ans** 为 **N** ，它将存储可能的子串的最小大小，这样每个大小为 **ans** 的子串至少有一个**K-惊人的**字符。
*   将字符“ **0** ”插入到字符串**s**的前面和末端
*   [使用变量 **c** 迭代范围【a，z】](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)内的字符，并执行以下步骤:
    *   将字符 **c** 分配给**S【0】**和**S【N+1】。**
    *   初始化两个变量，说 **prev** 为 **0** 和 **maxLen** 为 **0、**其中 **prev** 将存储字符 **c** 的最后一个索引， **maxLen** 将存储两个最近的 **c** 的位置之间的最大距离。
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N+1】**，并执行以下步骤:
        *   如果 **S[i] = c，**则将 **maxLen** 的值修改为 **max(maxLen，I–prev)**和，然后将 **i** 分配给 **prev** 。
    *   现在将 **ans** 的值修改为 **min(ans，max_len)** 。
*   最后，完成上述步骤后，打印得到的**和**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum value of K
// such that there exist atleast one K
// amazing character

int MinimumLengthSubstring(string S, int N)
{
    // Stores the answer
    int ans = N;

    // Update the string S
    S = "0" + S + "0";

    // Iterate over the characters
    // in range [a, z]
    for (char c = 'a'; c <= 'z'; ++c) {

        // Stores the last index where
        // c appears
        int prev = 0;

        // Stores the maximum possible length
        int max_len = 0;

        // Update string S
        S[0] = c;
        S[N + 1] = c;

        // Iterate over characters of string
        // S
        for (int i = 1; i <= N + 1; ++i) {
            // If S[i] is equal to c
            if (S[i] == c) {

                // Stores the distance between
                // positions of two same c
                int len = i - prev;

                // Update max_len
                max_len = max(max_len, len);

                // Update the value of prev
                prev = i;
            }
        }

        // Update the value of ans
        ans = min(ans, max_len);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    string S = "abcde";
    int N = S.length();

    // Function Call
    cout << MinimumLengthSubstring(S, N);
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum value of K
# such that there exist atleast one K
# amazing character
def MinimumLengthSubstring(S, N):

    # Stores the answer
    ans = N

    # Update the S
    S = "0" + S + "0"
    S = [i for i in S]

    # Iterate over the characters
    # in range [a, z]
    for c in range(ord('a'), ord('z') + 1):

        # Stores the last index where
        # c appears
        prev = 0

        # Stores the maximum possible length
        max_len = 0

        # Update S
        S[0] = chr(c)
        S[N + 1] = chr(c)

        # Iterate over characters of string
        # S
        for i in range(1, N + 2):

            # If S[i] is equal to c
            if (S[i] == chr(c)):

                # Stores the distance between
                # positions of two same c
                len = i - prev

                # Update max_len
                max_len = max(max_len, len)

                # Update the value of prev
                prev = i

        # Update the value of ans
        ans = min(ans, max_len)

    # Return the answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    S = "abcde"
    N = len(S)

    # Function Call
    print(MinimumLengthSubstring(S, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum value of K
// such that there exist atleast one K
// amazing character

static int MinimumLengthSubstring(string S, int N)
{
    // Stores the answer
    int ans = N;

    // Update the string S
    S = "0" + S + "0";

    // Iterate over the characters
    // in range [a, z]
    for (char c = 'a'; c <= 'z'; ++c) {

        // Stores the last index where
        // c appears
        int prev = 0;

        // Stores the maximum possible length
        int max_len = 0;

        // Update string S
       S = S.Substring(0,0) + c + S.Substring(1);
       S = S.Substring(0, N+1) + c + S.Substring(N + 2);

        // Iterate over characters of string
        // S
        for (int i = 1; i <= N + 1; ++i) {
            // If S[i] is equal to c
            if (S[i] == c) {

                // Stores the distance between
                // positions of two same c
                int len = i - prev;

                // Update max_len
                max_len = Math.Max(max_len, len);

                // Update the value of prev
                prev = i;
            }
        }

        // Update the value of ans
        ans = Math.Min(ans, max_len);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main()
{
    // Given Input
    string S = "abcde";
    int N = S.Length;

    // Function Call
    Console.Write(MinimumLengthSubstring(S, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum value of K
// such that there exist atleast one K
// amazing character

function MinimumLengthSubstring(S, N) {
    // Stores the answer
    let ans = N;

    // Update the string S
    S = "0" + S + "0";
    S = S.split("")

    // Iterate over the characters
    // in range [a, z]
    for (let c = 'a'.charCodeAt(0); c <= 'z'.charCodeAt(0); ++c) {

        // Stores the last index where
        // c appears
        let prev = 0;

        // Stores the maximum possible length
        let max_len = 0;

        // Update string S
        S[0] = String.fromCharCode(c);
        S[N + 1] = String.fromCharCode(c);

        // Iterate over characters of string
        // S
        for (let i = 1; i <= N + 1; ++i) {
            // If S[i] is equal to c
            if (S[i] == String.fromCharCode(c)) {

                // Stores the distance between
                // positions of two same c
                let len = i - prev;

                // Update max_len
                max_len = Math.max(max_len, len);

                // Update the value of prev
                prev = i;
            }
        }

        // Update the value of ans
        ans = Math.min(ans, max_len);
    }

    // Return the answer
    return ans;
}

// Driver Code

// Given Input
let S = "abcde";
let N = S.length;

// Function Call
document.write(MinimumLengthSubstring(S, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)