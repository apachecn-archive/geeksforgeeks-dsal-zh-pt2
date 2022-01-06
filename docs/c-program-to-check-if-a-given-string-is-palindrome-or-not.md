# 检查给定字符串是否回文的 C++程序

> 原文:[https://www . geesforgeks . org/c-程序检查给定字符串是否是回文/](https://www.geeksforgeeks.org/c-program-to-check-if-a-given-string-is-palindrome-or-not/)

给定一个由英文字母表中的 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) **S** ，任务是[检查给定的字符串是否是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。如果给定的字符串是回文，则打印“**是**”。否则，打印“**否**”。

**注:**如果一个字符串的反串与该字符串相同，则称该字符串为回文。

**示例:**

> **输入:**S = " abdcba "
> **输出:**是
> **说明:**
> 给定字符串的反码等于等于给定字符串的(abdcba)。因此，给定的字符串是回文。
> 
> **输入:**S = " geeksforgeks "
> **输出:**否
> **说明:**
> 给定字符串的反方向等于(skeeGrofskeeG)不等于给定字符串。因此，给定的字符串不是回文。

**简单方法:**最简单的方法是使用 [STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 中内置的[反向功能](https://www.geeksforgeeks.org/stdreverse-in-c/)。按照以下步骤解决问题:

*   [将弦](https://www.geeksforgeeks.org/different-ways-to-copy-a-string-in-c-c/) **S** 复制到另一根弦上，说 **P、**然后[反转弦 S](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/) 。
*   现在检查**字符串 S 是否等于字符串 P** ，然后打印“**是**”。否则，打印“ **No** ”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// the string is palindrome
string isPalindrome(string S)
{
    // Stores the reverse of the
    // string S
    string P = S;

    // Reverse the string P
    reverse(P.begin(), P.end());

    // If S is equal to P
    if (S == P) {
        // Return "Yes"
        return "Yes";
    }
    // Otherwise
    else {
        // return "No"
        return "No";
    }
}

// Driver Code
int main()
{
    string S = "ABCDCBA";
    cout << isPalindrome(S);

    return 0;
}
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**高效方法:**通过[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并针对范围**【0，N/2】**中的每个索引检查**I<sup>th</sup>T7】索引处的字符是否等于 **(N-i-1) <sup>th</sup>** 索引处的字符，可以在空间复杂度上优化上述方法。按照以下步骤解决问题:**

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N/2】**，在每次迭代中检查索引 **i** 和 **N-i-1** 处的字符是否不相等，然后打印“ **No** ”和 [break](https://www.geeksforgeeks.org/break-statement-cc/) 。
*   如果以上情况都不满足，则打印“**是**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether string
// is palindrome
string isPalindrome(string S)
{
    // Iterate over the range [0, N/2]
    for (int i = 0; i < S.length() / 2; i++) {

        // If S[i] is not equal to
        // the S[N-i-1]
        if (S[i] != S[S.length() - i - 1]) {
            // Return No
            return "No";
        }
    }
    // Return "Yes"
    return "Yes";
}

// Driver Code
int main()
{
    string S = "ABCDCBA";
    cout << isPalindrome(S);

    return 0;
}
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)