# 通过替换“？”可能出现的周期为 K 的字典最小字符串 s 来自给定的字符串

> 原文:[https://www . geeksforgeeks . org/按字母顺序排列的最小字符串-通过替换给定字符串中的-s-k-可能/](https://www.geeksforgeeks.org/lexicographically-smallest-string-with-period-k-possible-by-replacing-s-from-a-given-string/)

给定一个由 **N** 小写字符和字符**“？”组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/)T2 S**和正整数 **K** ，任务是替换每个字符**'？'**加上一些小写字母，这样给定的字符串就变成了一个 **K** 的周期。如果不可能，则打印**-1”**。

> 如果且仅当字符串的长度是 **K** 的倍数，并且对于范围**【0，K】**上的所有可能的 **i** 值，S[i + K]，S[i + 2*K]，S[i + 3*K]，…，则字符串被称为 **K** 的周期。

**示例:**

> **输入:**S =“ab？?"，K = 2
> T3【输出: abab
> 
> **输入:** S =？？？？？?"，K = 3
> T3【输出:AAA

**天真方法:**给定的方法也可以通过[通过替换每个字符**“？”来生成所有可能的字符串组合**](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)来解决使用任意小写字符，打印出大小为 K 的每个[子串](https://www.geeksforgeeks.org/substring-in-cpp/)相同的字符串。

***时间复杂度:** O(26 <sup>M</sup> ，其中 **M** 为**的编号'？'**中弦 **S** 。*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)进行优化，遍历方式为遍历第一、第二、第三等字符，如果所有字符都是“？”然后将其替换为字符**‘a’**，否则，如果在每个相应位置仅存在一个不同的字符，则替换**’？”**用那个字符，否则，不能按照给定的标准修改字符串，因此，打印“-1”。按照以下步骤解决问题:

*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K】**内循环迭代，并执行以下步骤:
    *   初始化一张[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，说 **M** 来存储子串 **i** 位置的[字符频率](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)。
    *   [使用变量 **j** 在范围**【I，N】**上遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，增量为 **K** ，并将字符**S【j】**的频率通过 **1** 存储在地图 **M** 中。
    *   完成上述步骤后，请执行以下操作:
        *   如果地图的[尺寸大于 **2** ，则打印“-1”](https://www.geeksforgeeks.org/mapsize-c-stl/)[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
        *   否则，如果地图尺寸为 **2** ，则更换每个**？”**性格不同。
        *   否则，更换所有**'？'**带字符**‘一’**。
*   完成上述步骤后，如果字符串可以修改，则打印字符串 **S** 作为结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to modify the given string
// such that string S is a period of K
string modifyString(string& S, int K)
{

    int N = S.length();

    // Iterate over the range [0, K]
    for (int i = 0; i < K; i++) {

        // Stores the frequency of the
        // characters S[i + j*K]
        map<char, int> M;

        // Iterate over the string with
        // increment of K
        for (int j = i; j < N; j += K) {
            M[S[j]]++;
        }

        // Print "-1"
        if (M.size() > 2) {
            return "-1";
        }
        else if (M.size() == 1) {
            if (M['?'] != 0) {

                // Replace all characters
                // of the string with '?'
                // to 'a' to make it smallest
                for (int j = i; j < N; j += K) {
                    S[j] = 'a';
                }
            }
        }

        // Otherwise
        else if (M.size() == 2) {
            char ch;

            // Find the character other
            // than '?'
            for (auto& it : M) {
                if (it.first != '?') {
                    ch = it.first;
                }
            }

            // Replace all characters
            // of the string with '?'
            // to character ch
            for (int j = i; j < N; j += K) {
                S[j] = ch;
            }
        }

        // Clear the map M
        M.clear();
    }

    // Return the modified string
    return S;
}

// Driver Code
int main()
{

    string S = "ab??";
    int K = 2;
    cout << modifyString(S, K);

    return 0;
}
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to modify the given string
// such that string S is a period of K
function modifyString(S, K)
{
    let N = S.length;

    // Iterate over the range [0, K]
    for(let i = 0; i < K; i++)
    {

        // Stores the frequency of the
        // characters S[i + j*K]
        let M = new Map();

        // Iterate over the string with
        // increment of K
        for(let j = i; j < N; j += K)
        {
            if (M.has(S[j]))
            {
                M.set(M.get(S[j]),
                      M.get(S[j]) + 1);
            }
            else
            {
                M.set(S[j], 1);
            }
        }

        // Print "-1"
        if (M.size > 2)
        {
            return "-1";
        }
        else if (M.size == 1)
        {
            if (M.has('?'))
            {

                // Replace all characters
                // of the string with '?'
                // to 'a' to make it smallest
                for(let j = i; j < N; j += K)
                {
                    S = S.replace(S[j], 'a');
                }
            }
        }

        // Otherwise
        else if (M.size == 2)
        {
            let ch;

            // Find the character other
            // than '?'
            for(let it of M.keys())
            {
                if (it != '?')
                {
                    ch = it;
                }
            }

            // Replace all characters
            // of the string with '?'
            // to character ch
            for(let j = i; j < N; j += K)
            {
                S = S.replace(S[j], ch);
            }
        }

        // Clear the map M
        M.clear();
    }

    // Return the modified string
    return S;
}

// Driver Code
let S = "ab??";
let K = 2;

document.write(modifyString(S, K));

// This code is contributed by Potta Lokesh

</script>
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to modify the given string
# such that string S is a period of K
def modifyString(S,K):
    N = len(S)
    S = list(S)

    # Iterate over the range [0, K]
    for i in range(K):
        # Stores the frequency of the
        # characters S[i + j*K]
        M = {}

        # Iterate over the string with
        # increment of K
        for j in range(i,N,K):
            if S[j] in M:
                M[S[j]] += 1
            else:
                M[S[j]] = 1

        # Print "-1"
        if (len(M) > 2):
            return "-1"

        elif (len(M) == 1):
            if (M['?'] != 0):

                # Replace all characters
                # of the string with '?'
                # to 'a' to make it smallest
                for j in range(i,N,K):
                    S[j] = 'a'

        # Otherwise
        elif(len(M) == 2):
            ch = ''

            # Find the character other
            # than '?'
            for key,value in M.items():
                if (key != '?'):
                    ch = key
            # Replace all characters
            # of the string with '?'
            # to character ch
            for j in range(i,N,K):
                S[j] = ch

        # Clear the map M
        M.clear()
    S = ''.join(S)

    # Return the modified string
    return S

# Driver Code
if __name__ == '__main__':
    S = "ab??"
    K = 2
    print(modifyString(S, K))

    # This code is contributed by ipg2016107.
```

**Output:** 

```
abab
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)