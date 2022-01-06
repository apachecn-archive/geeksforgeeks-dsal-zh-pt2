# 对长度为 1 到 N 的每个前缀执行所述操作后，对每个小写字符进行计数

> 原文:[https://www . geeksforgeeks . org/对每个长度为 1 到 n 的前缀执行描述操作后每个小写字符的计数/](https://www.geeksforgeeks.org/count-of-each-lowercase-character-after-performing-described-operations-for-each-prefix-of-length-1-to-n/)

给定一个包含 **N** 小写英文字母的字符串 **S** 和一个将所有小写英文字母从“a”到“z”映射到 **1** 或 **-1** 的字典 **Dict** 。对于长度为 **K** 的字符串，可以进行以下操作:

1.  找到从索引 **1** 到 **K** 的最大字符，找到各自最大字符的字典映射。
2.  如果字典映射为 **1** ，则将所有字符从 **1** 递增至 **K** ，即‘a’变为‘b’，‘b’变为‘c’。。。，‘z’变成了‘a’。
3.  如果字典映射为 **-1** ，则将所有字符从 **1** 递减至 **K** 。即‘a’变成‘z’，‘b’变成‘a’，。。。，z 变成了 y

对长度为 **1** 至**n**的字符串的每个前缀执行所述操作

任务是在对长度为 **1** 到 **N** 的字符串的每个前缀执行所述操作后，确定每个小写英文字母的计数。

**示例:**

> **输入:** S="ab "，Dict[] = [1，-1，1，1，1，1，1，1，1，-1，1，-1，1，1，1，1，-1，-1，-1，1，1，-1，1-1，1-1]
> T3】输出:2 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
> T6】解释:T8】长度为 1 的前缀:Max 所以，递增前缀字符串。s =“bb”。
> 对于长度为 2 的前缀:最大字符= 'b '，映射= -1。所以，减少前缀字符串。s =“aa”。
> 
> **输入:** S="abcb "，Dict[] = [1，-1，1，1，1，-1，1，1，-1，1，-1，1，-1，1，1，1，1，-1，-1，-1，1，1，-1，1-1，1-1-1]
> T3】输出:0 0 3 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
> **解释:**
> 对于长度为 1 的前缀:所以，递增前缀字符串。S="bbcb "。
> 对于长度为 2 的前缀:最大字符= 'b '，映射= -1。所以，减少前缀字符串。S = "aacb "。
> 对于长度为 3 的前缀:最大字符= 'c '，映射= 1。所以，递增前缀字符串。s =“bbdb”。
> 对于长度为 4 的前缀:最大字符= 'd '，映射= 1。所以，递增前缀字符串。s =“ccec”。

**进场:**解决方案基于[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。请按照以下步骤解决此问题:

1.  运行一个从 **i = 0** 到 **i < N** 的循环，并在该循环中运行另一个从 **j = i** 到 **j > = 0** 的循环(遍历前缀)。
2.  现在找到前缀中的最大元素和它在**字典**中被映射到的数字，比如 **mp** 。
3.  然后根据编号 **mp** 进行递增或递减操作。
4.  现在，创建一个向量**和**，来存储每个元素的频率。
5.  遍历整个字符串并填充向量**和**。
6.  打印矢量**和**的元素。

下面是上述方法的实现:

## C++

```
// C++ prgram for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the frequency of
// all character after performig N operations
void processString(string& S, vector<int>& Dict)
{
    int N = S.length();
    char mx;

    // Vector to store the frequency 
    // of all characters
    vector<int> ans(26, 0);
    for (int i = 0; i < N; i++) {
        mx = 96;
        for (int j = 0; j <= i; j++) {
            mx = max(mx, S[j]);
        }

        for (int j = 0; j <= i; j++) {
            // If S[j] is 'a' and 
            // Dict[S[j]] is -1 then 
            // make S[j] equals to 'z'
            if (S[j] + Dict[mx - 'a'] < 97) {
                S[j] = S[j] + 
                    Dict[mx - 'a'] + 26;
            }

            // If S[j] is 'z' and 
            // Dict[S[j]] is 1
            // then make S[j] equals to 'a'
            else if (S[j] + Dict[mx - 'a'] 
                     > 122) {
                S[j] = S[j] + 
                    Dict[mx - 'a'] - 26;
            }

            else {
                S[j] += Dict[mx - 'a'];
            }
        }
    }
    for (int i = 0; i < N; i++) {
        ans[S[i] - 'a']++;
    }

    for (auto x : ans) {
        cout << x << ' ';
    }
}

// Driver code
int main()
{

    string S = "ab";
    vector<int> Dict
        = { 1,  -1, 1, 1, 1, -1, 1,  1,  
           1, -1, 1,  -1,   1, -1, 1,  1, 1, 
           1, -1, -1, -1, 1, 1,  -1, 1 - 1 };
    processString(S, Dict);

    return 0;
}
```

**Output**

```
2 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
```

***时间复杂度:*****O(N<sup>2</sup>)
***辅助空间:*** O(1)**