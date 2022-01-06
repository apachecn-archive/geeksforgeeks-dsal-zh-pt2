# Q 查询范围[L，R]内给定字符串的字典最小字谜

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的范围内给定字符串的最小字谜-l-r-for-q-query/](https://www.geeksforgeeks.org/lexicographically-smallest-anagram-of-given-string-in-range-l-r-for-q-queries/)

给定一个大小为 **N** 的字符串 **S** 和一个数组**查询**，包含 **Q** 形式的查询 **L** ， **R** 。任务是为每个查询找到从 **L** 到 **R** 的按字典顺序最小的字符串字谜。

**示例:**

> **输入:** S = "bbaacd"
> 查询[]={{1，3}，{2，5}}
> **输出:**
> aab
> aacd
> 
> **输入:** S="bbdfaaacaed"
> 查询[]={{0，4}，{4，8}}
> **输出:**
> abb df
> aaaaac

**方法:**这个问题可以通过**预计算**到 ***出现的所有字符的[频率与字符串 **S** 中的](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)*** 索引来解决，因为这样做，在每个查询中计算 **L** 到 **R** 之间的字符频率既方便又省时。现在，要解决这个问题，请按照以下步骤操作:

*   创建一个函数**预计算频率**，为每个索引 **i** 存储字符串 **S** 中的字符频率。
*   创建一个名为 **smallestAnagram** 的函数，并为每个查询运行它。在此功能中:
    *   创建一个字符串**和**，它将存储从 **L** 到 **R** 的字典上最小的字谜。
    *   查找频率，直到索引 **R** 和直到索引 **L-1** ，得到 **L** 到 **R** 之间的频率。
    *   从 0 到该字符的频率运行一个循环，并将其添加到字符串**和**中。
    *   返回字符串**和**作为每个查询的答案。
*   根据以上观察打印答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the frequencies of all
// characters till each index in string
void preComputeFreq(string& S,
                    vector<vector<int> >& freq)
{
    vector<int> f(26, 0);
    for (int i = 0; i < S.size(); ++i) {
        freq[i] = f;
        freq[i][S[i] - 'a']++;

        f = freq[i];
    }
}

// Function to get the
// smallest anagram from L to R
string smallestAnagram(string& S, int L, int R,
                       vector<vector<int> >& freq)
{
    string ans;

    // Finding net frequencies
    // of character from L to R
    for (int i = 0; i < 26; i++) {
        int low = 0;
        if (L > 0) {
            low = freq[L - 1][i];
        }

        // Adding characters to string ans
        for (int j = 0; j < freq[R][i] - low; j++) {
            ans += (char)('a' + i);
        }
    }

    return ans;
}

void smallestAnagramUtil(string& S, int N,
                         vector<pair<int, int> >& queries)
{
    vector<vector<int> > freq(N, vector<int>(26, 0));
    preComputeFreq(S, freq);

    for (auto x : queries) {
        int L = x.first;
        int R = x.second;
        cout << smallestAnagram(S, L, R, freq)
          << endl;
    }
}

// Driver Code
int main()
{
    string S = "bbdfaaacaed";
    int N = S.size();
    vector<pair<int, int> > queries
        = { { 0, 4 }, { 4, 8 } };
    smallestAnagramUtil(S, N, queries);
}
```

## java 描述语言

```
<script>

    // JavaScript Program to implement
    // the above approach

    // Function to calculate the frequencies of all
    // characters till each index in string
    function preComputeFreq(S, freq)
    {
        let f = new Array(26).fill(0);
        for (let i = 0; i < S.length; ++i) {
            freq[i] = [...f];
            freq[i][S[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

            f = [...freq[i]];
        }
        return freq;
    }

    // Function to get the
    // smallest anagram from L to R
    function smallestAnagram(S, L, R,
        freq) {
        let ans = '';

        // Finding net frequencies
        // of character from L to R
        for (let i = 0; i < 26; i++) {
            let low = 0;
            if (L > 0) {
                low = freq[L - 1][i];
            }

            // Adding characters to string ans
            for (let j = 0; j < freq[R][i] - low; j++) {
                ans = ans + String.fromCharCode('a'.charCodeAt(0) + i);
            }
        }

        return ans;
    }

    function smallestAnagramUtil(S, N,
        queries) {
        let freq = new Array(N);

        for (let i = 0; i < freq.length; i++) {
            freq[i] = new Array(26).fill(0);
        }
        freq = preComputeFreq(S, freq);

        for (let i = 0; i < queries.length; i++) {
            let L = queries[i][0];
            let R = queries[i][1];
            document.write(smallestAnagram(S, L, R, freq) + '<br>');
        }
    }

    // Driver Code
    let S = "bbdfaaacaed";
    let N = S.length;
    let queries
        = [[0, 4], [4, 8]];
    smallestAnagramUtil(S, N, queries);

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
abbdf
aaaac
```

**时间复杂度:**O(Q * N)
T3】辅助空间: O(26*N)