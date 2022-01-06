# 查找并替换给定字符串中所有出现的子字符串

> 原文:[https://www . geesforgeks . org/查找并替换给定字符串中出现的所有子字符串/](https://www.geeksforgeeks.org/find-and-replace-all-occurrence-of-a-substring-in-the-given-string/)

给定分别由 **N** 、 **M** 和 **K** 字符组成的三个[字符串 **S** 、 **S1** 和 **S2** ，任务是通过将字符串 **S** 中的所有子字符串 **S1** 替换为字符串 **S2** 来修改字符串 **S** 。](https://www.geeksforgeeks.org/stdstring-class-in-c/)

**示例:**

> **输入:** S =“阿巴巴巴”，S1 =“阿坝”，S2 =“a”
> **输出:**阿坝
> **解释:**
> 将子字符串 S[0，2]和 S[4，6](= S1)改为字符串 S2(=“a”)将字符串 S 修改为“阿坝”。因此，打印“阿坝”。
> 
> **输入:** S = 【极客 forgeeks】，S1 =【eek】，S2 =【ok】
> **输出:**goksforkeks

**天真方法:**解决给定问题最简单的方法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，当发现任意字符串 **S1** 为字符串 **S** 中的子字符串时，则替换为 **S2** 。按照以下步骤解决这个问题:

*   在替换字符串 **S** 中的子串 **S1** 到 **S2** 的所有出现后，初始化一个[字符串**和**来存储结果](https://www.geeksforgeeks.org/category/data-structures/c-strings/)[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)。
*   [使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下步骤:
    *   如果字符串 **S** 的[前缀子字符串](https://www.geeksforgeeks.org/string-from-prefix-and-suffix-of-given-two-strings/)等于索引 **i** 中的 **S1** ，则在[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)和 **ans** 中添加字符串 **S2** 。
    *   否则，将当前字符添加到字符串**和**中。
*   完成上述步骤后，打印字符串**和**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to replace all the occurrences
// of the substring S1 to S2 in string S
void modifyString(string& s, string& s1,
                  string& s2)
{
    // Stores the resultant string
    string ans = "";

    // Traverse the string s
    for (int i = 0; i < s.length(); i++) {

        int k = 0;

        // If the first character of
        // string s1 matches with the
        // current character in string s
        if (s[i] == s1[k]
            && i + s1.length()
                   <= s.length()) {

            int j;

            // If the complete string
            // matches or not
            for (j = i; j < i + s1.length(); j++) {

                if (s[j] != s1[k]) {
                    break;
                }
                else {
                    k = k + 1;
                }
            }

            // If complete string matches
            // then replace it with the
            // string s2
            if (j == i + s1.length()) {
                ans.append(s2);
                i = j - 1;
            }

            // Otherwise
            else {
                ans.push_back(s[i]);
            }
        }

        // Otherwise
        else {
            ans.push_back(s[i]);
        }
    }

    // Print the resultant string
    cout << ans;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    string S1 = "eek";
    string S2 = "ok";
    modifyString(S, S1, S2);

    return 0;
}
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to replace all the occurrences
// of the sublet S1 to S2 in let S
function modifylet(s, s1,
                  s2)
{
    // Stores the resultant let
    let ans = "";

    // Traverse the let s
    for (let i = 0; i < s.length; i++) {

        let k = 0;

        // If the first character of
        // let s1 matches with the
        // current character in let s
        if (s[i] == s1[k]
            && i + s1.length
                   <= s.length) {

            let j;

            // If the complete let
            // matches or not
            for (j = i; j < i + s1.length; j++) {

                if (s[j] != s1[k]) {
                    break;
                }
                else {
                    k = k + 1;
                }
            }

            // If complete let matches
            // then replace it with the
            // let s2
            if (j == i + s1.length) {
                ans = ans + s2;
                i = j - 1;
            }

            // Otherwise
            else {
                ans = ans + s[i];
            }
        }

        // Otherwise
        else {
            ans = ans + s[i];
        }
    }

    // Print the resultant let
    document.write(ans);
}

// Driver Code
    let S = "geeksforgeeks";
    let S1 = "eek";
    let S2 = "ok";
    modifylet(S, S1, S2);

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
goksforgoks
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过为[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S1** 创建[最长适当前缀](https://www.geeksforgeeks.org/longest-prefix-also-suffix/)和[后缀数组](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)然后执行 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)来查找字符串 **S1** 在字符串 **S** 中的出现次数来进行优化。按照以下步骤解决此问题:

*   创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **lps[]** ，为每个字符存储[最长的正确前缀和后缀](https://www.geeksforgeeks.org/longest-prefix-also-suffix/)，并使用字符串 **S1** 的 [KMP](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/) 算法填充这个向量。
*   初始化两个变量，比如 **i** 和 **j** 为 **0** ，分别存储当前字符在 **s** 和 **s1** 中的位置。
*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **找到**来存储所有起始索引，字符串 **S1** 出现在 **S** 中。
*   [使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下步骤:
    *   如果**S【I】**等于**S1【j】**，那么将 **i** 和 **j** 增加 **1。**
    *   如果 **j** 等于 **s1** 的长度，则将值**(I–j)**添加到找到的向量**中，并将 **j** 更新为**LPS【j–1】**。**
    *   **否则，如果**S【I】**的值不等于**S1【j】**，那么如果 **j** 等于 **0** ，那么将 **i** 的值增加 **1** 。否则，将 **j** 更新为**LPS【j–1】**。**
*   **在 **s.** 中将 **s1** 的所有初始外观替换为 **s2** 后，初始化一个变量 say、 **prev** 为 **0** 以存储最后更改的索引和一个空的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **ans** 以存储结果[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)**
*   **[遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **找到[]** ，如果**找到的【I】**的值大于 **prev** ，则在 **ans** 中添加字符串 **S2** 代替 **S1** 。**
*   **完成上述步骤后，打印字符串**和**作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the LPS array
// for the given string S1
vector<int> computeLPS(string& s1)
{
    // Stores the longest proper prefix
    // and suffix for each character
    // in the string s1
    vector<int> lps(s1.length());
    int len = 0;

    // Set lps value 0 for the first
    // character of the string s1
    lps[0] = 0;

    int i = 1;

    // Iterate to fill the lps vector
    while (i < s1.length()) {
        if (s1[i] == s1[len]) {
            len = len + 1;
            lps[i] = len;
            i = i + 1;
        }
        else {

            // If there is no longest
            // proper prefix which is
            // suffix, then set lps[i] = 0
            if (len == 0) {
                lps[i] = 0;
                i = i + 1;
            }

            // Otherwise
            else
                len = lps[len - 1];
        }
    }

    return lps;
}

// Function to replace all the occurrences
// of the substring S1 to S2 in string S
void modifyString(string& s, string& s1,
                  string& s2)
{
    vector<int> lps = computeLPS(s1);
    int i = 0;
    int j = 0;

    // Stores all the starting index
    // from character S1 occurs in S
    vector<int> found;

    // Iterate to find all starting
    // indexes and store all indices
    // in a vector found
    while (i < s.length()) {
        if (s[i] == s1[j]) {
            i = i + 1;
            j = j + 1;
        }

        // The string s1 occurrence is
        // found and store it in found[]
        if (j == s1.length()) {
            found.push_back(i - j);
            j = lps[j - 1];
        }
        else if (i < s.length()
                 && s1[j] != s[i]) {
            if (j == 0)
                i = i + 1;
            else
                j = lps[j - 1];
        }
    }

    // Stores the resultant string
    string ans = "";
    int prev = 0;

    // Traverse the vector found[]
    for (int k = 0; k < found.size(); k++) {
        if (found[k] < prev)
            continue;
        ans.append(s.substr(prev, found[k] - prev));
        ans.append(s2);
        prev = found[k] + s1.size();
    }

    ans.append(s.substr(prev,
                        s.length() - prev));

    // Print the resultant string
    cout << ans << endl;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    string S1 = "eek";
    string S2 = "ok";
    modifyString(S, S1, S2);

    return 0;
}
```

****Output:** 

```
goksforgoks
```** 

*****时间复杂度:** O(N + M)*
***辅助空间:** O(N)***