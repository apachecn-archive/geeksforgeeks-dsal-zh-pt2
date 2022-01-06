# 最小压缩弦长

> 原文:[https://www . geesforgeks . org/最小化压缩字符串长度/](https://www.geeksforgeeks.org/length-of-minimized-compressed-string/)

给定一根[弦](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到长度最短的压缩[弦](https://www.geeksforgeeks.org/string-data-structure/)。[弦](https://www.geeksforgeeks.org/string-data-structure/)可以通过以下方式压缩:

*   如果 S =**“ABCDABCD”**，那么[弦](https://www.geeksforgeeks.org/string-data-structure/)可以压缩为 **(ABCD) <sup>2</sup>** ，那么压缩后的[弦](https://www.geeksforgeeks.org/string-data-structure/)的长度将为 **4** 。
*   如果 S =**【AABBCCDD】**则[弦](https://www.geeksforgeeks.org/string-data-structure/)压缩形式为**A<sup>2</sup>B<sup>2</sup>C<sup>2</sup>D<sup>2</sup>T13】因此，压缩后的[弦](https://www.geeksforgeeks.org/string-data-structure/)长度为 **4** 。**

**示例:**

> **输入:**S = " aaba "
> T3】输出: 3
> **解释:**可以改写为一个 <sup>2</sup> ba 因此答案为 3。
> 
> **输入:**S = " aaabaabcdaabaabcd "
> T3】输出: 4
> **说明:**字符串可以改写为(((a)<sup>3</sup>b)<sup>2</sup>(c)<sup>2</sup>d)<sup>2</sup>。因此，答案将是 4。

**逼近**:问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决，因为它有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。按照以下步骤解决问题:

*   初始化一个 **dp[][]** 向量，其中 **dp[i][j]** 存储压缩子串 **s[i]，s[i+1]，…，s[j]的长度。**
*   [使用变量 **l** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**中迭代，并执行以下步骤:
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-l】**中迭代，并执行以下步骤:
        *   初始化一个变量，比如说， **j** 为 **i+l-1。**
        *   如果 **i** 等于 **j、**，则**T5】更新**DP【I】【j】**为**1****继续**。**
        *   [使用变量 **k** 在](https://www.geeksforgeeks.org/range-based-loop-c/)**【I，j-1】**范围内迭代，并将 **dp[i][j]** 更新为[min](https://www.geeksforgeeks.org/stdmin_element-in-cpp/) 的 **dp[i][j]** 和 **dp[i][k] + dp[k][j]。**
        *   初始化一个变量，比如说， **temp** 为 **s.substr(i，l)。**
        *   然后，找到[最长的前缀，也是子串 **temp** 的后缀](https://www.geeksforgeeks.org/longest-prefix-also-suffix/)。
        *   如果子串的形式为**dp[i][k]^n(l%(l–pref[l-1])= 0)**，则将 **dp[i][j]** 的值更新为 **min(dp[i][j]，DP[I][I+(l-pref[l-1]–1)]。**
*   最后打印 **dp[0][N-1]** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Prefix function to calculate
// longest prefix that is also
// the suffix of the substring S
vector<int> prefix_function(string s)
{

    int n = (int)s.length();

    vector<int> pi(n);

    for (int i = 1; i < n; i++) {

        int j = pi[i - 1];

        while (j > 0 && s[i] != s[j])
            j = pi[j - 1];
        if (s[i] == s[j])
            j++;
        pi[i] = j;
    }

    return pi;
}

// Function to find the length of the
// shortest compressed string
void minLength(string s, int n)
{
    // Declare a 2D dp vector
    vector<vector<int> > dp(n + 1, vector<int>(n + 1, 10000));

    // Traversing substring on the basis of length
    for (int l = 1; l <= n; l++) {
        // For loop for each substring of length l
        for (int i = 0; i < n - l + 1; i++) {
            // Second substring coordinate
            int j = i + l - 1;

            // If the length of the string is 1
            // then dp[i][j] = 1
            if (i == j) {
                dp[i][j] = 1;
                continue;
            }

            // Finding smallest dp[i][j] value
            // by breaking it in two substrings
            for (int k = i; k < j; k++) {
                dp[i][j] = min(dp[i][j],
                               dp[i][k] + dp[k + 1][j]);
            }

            // Substring starting with i of length L
            string temp = s.substr(i, l);

            // Prefix function of the substring temp
            auto pref = prefix_function(temp);

            // Checking if the substring is
            // of the form of dp[i][k]^n
            if (l % (l - pref[l - 1]) == 0) {
                // If yes, check if dp[i][k] is
                // less than dp[i][j]
                dp[i][j] = min(dp[i][j],
                               dp[i][i + (l - pref[l - 1] - 1)]);
            }
        }
    }

    // Finally, print the required answer
    cout << dp[0][n - 1] << endl;
}

// Driver Code
int main()
{
    // Given Input
    int n = 4;
    string s = "aaba";

    // Function Call
    minLength(s, n);
}
```

**Output:**

```
3

```

***时间复杂度:**o(n^3)*
*T6】辅助空间: O(N^2)*