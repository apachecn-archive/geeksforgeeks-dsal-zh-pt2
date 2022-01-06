# 三进制字符串中要替换的最少字符，以删除 Q 查询的所有回文子字符串

> 原文:[https://www . geeksforgeeks . org/用于 q 查询的三进制字符串中最少要替换的字符-移除所有回文-子字符串/](https://www.geeksforgeeks.org/minimum-characters-to-be-replaced-in-ternary-string-to-remove-all-palindromic-substrings-for-q-queries/)

给定长度为 **N** 的三元[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，其中只包含**【0】**、**【1】**和**【2】**字符和 **Q** 包含[范围的索引](https://www.geeksforgeeks.org/range-and-indices-in-c-sharp-8-0/)**【L，R】**的查询，每个查询的任务是找到要转换的最小字符数**【L，R】**

**示例:**

> **输入:** N = 10，Q = 3，S =“0200011011”，查询= {0，4}、{1，6}、{2，8}
> **输出:**2 3
> **解释:**
> 查询 1: {0，4 } S =“02000”出现的回文子串有“020”、“00”、“000”。子串 s 可以更改为“02 **1** 0 **2** ”，更改 2 次。“acbac”没有回文子串。
> 查询 2: {1，6 } s =“200011”出现的回文子串为“00”、“000”、“11”。子串 s 可以更改为“20 **120** 1”，更改 3 次。”cabcab "没有回文子串。
> 查询 3: {2，8 } s =“aabbab”出现的回文子串有“00”、“000”、“0110”、“11”、“101”。子串 s 可以修改为“ **12** 01 **2** 01”，修改 3 次。”1201201”没有回文子串。
> 
> **输入:** N = 5，Q = 2，S =“bccab”，查询= {0，4}，{1，2 }
> T3】输出: 2 1

**天真方法:**给定的问题可以通过[递归地](https://www.geeksforgeeks.org/recursion/)修改给定查询的[子串](https://www.geeksforgeeks.org/substring-in-java/)的每个[字符](https://www.geeksforgeeks.org/character-arithmetic-c-c/)，并检查结果[子串](https://www.geeksforgeeks.org/substring-in-java/)是否具有[回文子串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)来解决。

**时间复杂度:**O(Q * 3<sup>N</sup>)
T5】辅助空间: O(N)

**高效方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决，其思想是使用以下观察值对所有子串的可能答案进行预处理:

*   如果 s <sub>i</sub> ≠ s <sub>i-1</sub> 和 s <sub>i</sub> ≠ s <sub>i-2</sub> 相同，即没有两个相邻字符相同，也没有两个替代字符相同，原因如下:
    *   如果[相邻字符](https://www.geeksforgeeks.org/rearrange-characters-string-no-two-adjacent/)相同，则形成偶数长度回文。
    *   如果[交替字符](https://www.geeksforgeeks.org/check-if-a-given-string-is-made-up-of-two-alternating-characters/)相同，则形成奇数长度回文。
*   如果字符串的第一个字符是“0”，那么下一个字符必须是“1”或“2”(因为 s<sub>I</sub>s<sub>I-1</sub>
*   如果第二个字符是“1”，那么第三个字符不能是“0”(自 s<sub>I</sub>s<sub>I-2</sub>或“1”(自 s<sub>I</sub>s<sub>I-1</sub>)
*   因此，第三个字符将是“2”。那么第四个字符只能是‘1’。形成的字符串是“012012012 ..”
*   类似地，在置换字符‘0’、‘1’和‘2’并重复每个置换几次后，我们得到目标字符串“012012012……”、“120120120……”、“021021021……”等
*   有六种可能的[排列](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)带有‘0’、‘1’和‘2’字符，因此有六个目标字符串

现在，每个查询都可以通过将从 **L** 到 **R** 字符的子串转换成六个目标字符串并检查哪一个需要最少的操作来解决。这种方法对于每个查询需要 O(N)个时间。通过预处理给定的字符串，可以进一步优化该方法。以下是优化的解决方案:

*   假设**前缀【I】**是包含将字符串转换为目标字符串 **i** 所需的最小操作数的数组。因此，**前缀【I】【j】**是将字符串的第一个 **j** 字符转换为目标字符串 **i** 所需的操作数。
*   在上述步骤的预处理之后，每个查询 **j** 可以在 O(1)时间内求解，使用每个可能的预处理字符串的公式作为所有可能序列的 **currentCost** 和**(前缀[I][r<sub>j</sub>–前缀[I][l<sub>j</sub>–1])**的最小值，并打印成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define SIZE 100005
using namespace std;

// Function to preprocess the cost of
// converting the first j character to
// each sequence prefix[i]
void preprocess(string& s, string& t,
                int prefix[][SIZE],
                int n, int i)
{
    // Initialize DP array
    prefix[i][0] = (s[0] != t[0]);

    for (int j = 1; j < n; j++) {

        // prefix[i][j] defines minimum
        // operations to transform first j
        // characters of s into sequence i
        prefix[i][j]
            = prefix[i][j - 1]
              + (s[j] != t[j % 3]);
    }
    return;
}

// Function to find the minimum number of
// changes required to make each substring
// between [L, R] non-palindromic
void minChangesNonPalindrome(
    string str, int N, int Q,
    vector<pair<int, int> > queries)
{

    // Initialize the DP array
    int prefix[6][SIZE];

    // Initialize the 6 different patterns
    // that can be formed to make substrings
    // non palindromic
    vector<string> sequences
        = { "012", "021", "102",
            "120", "201", "210" };

    for (int i = 0; i < 6; i++) {

        // Preprocess the string with
        // the ith sequence
        preprocess(str, sequences[i],
                   prefix, N, i);
    }

    // Iterate through queries
    for (int i = 0; i < Q; i++) {

        int l = queries[i].first + 1,
            r = queries[i].second + 1;
        int cost = INT_MAX;

        // Find the minimum operations by
        // comparing 6 different patterns
        // of the substrings
        for (int j = 0; j < 6; j++) {

            // Find the cost
            cost
                = min(
                    cost,
                    prefix[j][r]
                        - prefix[j][l]
                        + (str[l] != sequences[j][l % 3]));
        }
        cout << cost << '\n';
    }
}

// Driver Code
int main()
{
    string S = "0200011011";
    vector<pair<int, int> > queries
        = { { 0, 4 }, { 1, 6 }, { 2, 8 } };
    int N = S.length();
    int Q = queries.size();

    minChangesNonPalindrome(
        S, N, Q, queries);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys
SIZE = 100005

# Function to preprocess the cost of
# converting the first j character to
# each sequence prefix[i]
def preprocess(s,  t,
               prefix,
               n, i):

    # Initialize DP array
    prefix[i][0] = (s[0] != t[0])

    for j in range(1, n):

        # prefix[i][j] defines minimum
        # operations to transform first j
        # characters of s into sequence i
        prefix[i][j] = prefix[i][j - 1] + (s[j] != t[j % 3])
    return

# Function to find the minimum number of
# changes required to make each substring
# between [L, R] non-palindromic
def minChangesNonPalindrome(
        st, N, Q,
        queries):

    # Initialize the DP array
    prefix = [[0 for x in range(SIZE)]for y in range(6)]

    # Initialize the 6 different patterns
    # that can be formed to make substrings
    # non palindromic
    sequences = ["012", "021", "102",
                 "120", "201", "210"]

    for i in range(6):

        # Preprocess the string with
        # the ith sequence
        preprocess(st, sequences[i],
                   prefix, N, i)

    # Iterate through queries
    for i in range(Q):

        l = queries[i][0] + 1
        r = queries[i][1] + 1
        cost = sys.maxsize-1

        # Find the minimum operations by
        # comparing 6 different patterns
        # of the substrings
        for j in range(6):

            # Find the cost
            cost = min(cost, prefix[j][r] - prefix[j][l]
                       + (st[l] != sequences[j][l % 3]))

        print(cost)

# Driver Code
if __name__ == "__main__":

    S = "0200011011"
    queries = [[0, 4], [1, 6], [2, 8]]
    N = len(S)
    Q = len(queries)

    minChangesNonPalindrome(
        S, N, Q, queries)

    # This code is contributed by ukasp.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach
        let SIZE = 100005

        // Function to preprocess the cost of
        // converting the first j character to
        // each sequence prefix[i]
        function preprocess(s, t,
            prefix, n, i)
           {

            // Initialize DP array
            prefix[i][0] = (s[0] != t[0]);

            for (let j = 1; j < n; j++) {

                // prefix[i][j] defines minimum
                // operations to transform first j
                // characters of s into sequence i
                prefix[i][j]
                    = prefix[i][j - 1]
                    + (s[j] != t[j % 3]);
            }
            return prefix;
        }

        // Function to find the minimum number of
        // changes required to make each substring
        // between [L, R] non-palindromic
        function minChangesNonPalindrome(
            str, N, Q, queries)
        {

            // Initialize the DP array
            let prefix = new Array(6);
            for (let i = 0; i < prefix.length; i++)
                prefix[i] = new Array(SIZE).fill(0);

            // Initialize the 6 different patterns
            // that can be formed to make substrings
            // non palindromic
            let sequences
                = ["012", "021", "102",
                    "120", "201", "210"];

            for (let i = 0; i < 6; i++) {

                // Preprocess the string with
                // the ith sequence
                prefix = preprocess(str, sequences[i],
                    prefix, N, i);
            }

            // Iterate through queries
            for (let i = 0; i < Q; i++) {

                let l = queries[i].first + 1,
                    r = queries[i].second + 1;
                let cost = Number.MAX_VALUE;

                // Find the minimum operations by
                // comparing 6 different patterns
                // of the substrings
                for (let j = 0; j < 6; j++) {

                    // Find the cost
                    cost
                        = Math.min(
                            cost,
                            prefix[j][r]
                            - prefix[j][l]
                            + (str[l] != sequences[j][l % 3]));
                }
                document.write(cost + '<br>');
            }
        }

        // Driver Code
        let S = "0200011011";
        let queries
            = [{ first: 0, second: 4 }, { first: 1, second: 6 }, { first: 2, second: 8 }];
        let N = S.length;
        let Q = queries.length;

        minChangesNonPalindrome(
            S, N, Q, queries);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
3
3
```

**时间复杂度:**O(N+Q)
T3】辅助空间: O(N)