# 删除给定子串需要替换的最少字符数

> 原文:[https://www . geeksforgeeks . org/给定子串的最小替换移除字符数/](https://www.geeksforgeeks.org/minimum-characters-to-be-replaced-to-remove-the-given-substring/)

给定两根弦 **str1** 和 **str2** 。任务是在字符串 **str1** 中找到要被 **$** 替换的最小字符数，使得 **str1** 不包含字符串 **str2** 作为任何子字符串。

**示例:**

```
Input: str1 = "intellect", str2 = "tell"
Output: 1
4th character of string "str1" can be replaced by $
such that "int$llect" it does not contain "tell" 
as a substring.
 Input: str1 = "google", str2 = "apple"
Output: 0

```

**方法**类似于[搜索模式|集合 1(朴素模式搜索)](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)。
想法是找到字符串“str1”中最左边出现的字符串“str2”。如果“str1”的所有字符都与“str2”匹配，我们将替换(或用一个增加我们的答案)最后出现的符号，并增加字符串“str1”的索引，这样它将再次检查替换字符后的子字符串(即索引 I 将等于**I+长度(b)-1** )。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to calculate minimum
// characters to replace
int replace(string A, string B)
{

    int n = A.length(), m = B.length();
    int count = 0, i, j;

    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {

            // mismatch occurs
            if (A[i + j] != B[j]) 
                break;
        }

        // if all characters matched, i.e,
        // there is a substring of 'a' which
        // is same as string 'b'
        if (j == m) {
            count++;

             // increment i to index m-1 such that
            // minimum characters are replaced
            // in 'a'
            i += m - 1;

        }
    }

    return count;
}

// Driver Code
int main()
{
    string str1 = "aaaaaaaa";
    string str2 = "aaa";

    cout << replace(str1 , str2);

  return 0;
}
```