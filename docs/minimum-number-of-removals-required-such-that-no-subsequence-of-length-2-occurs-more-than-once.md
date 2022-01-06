# 长度为 2 的子序列出现不超过一次所需的最小移除次数

> 原文:[https://www . geeksforgeeks . org/最小移除次数-必需-这样-长度为 2 的子序列不会出现多次/](https://www.geeksforgeeks.org/minimum-number-of-removals-required-such-that-no-subsequence-of-length-2-occurs-more-than-once/)

给定一个由 **N** 个小写字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是修改给定的字符串，通过删除最少数量的字符，使得字符串中没有长度为两个重复的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:**S = " abcaadcd "
> **输出:** abcd
> **解释:**删除索引{2，3，4，5，6，7}处的字符将字符串修改为“abcd”，该字符串包含长度为 2 的每个子序列恰好一次。
> 
> **输入:**S = " cadbcc "
> T3】输出: cadbc

**方法:**给定的问题可以基于观察来解决，即最终字符串只能包含[唯一字符](https://www.geeksforgeeks.org/determine-string-unique-characters/)，例外是第一个字符可以在字符串中出现两次，一次在开始，另一次在结束(如果可能)。按照以下步骤解决问题:

*   初始化一个空的[字符串](https://www.geeksforgeeks.org/string-data-structure/)，比如**和**来存储最终的字符串。
*   初始化一个大小为 **26** 的布尔[数组](https://www.geeksforgeeks.org/array-data-structure/) **C[]** ，以检查字符是否出现在最终字符串中。
*   初始化一个变量，说 **pos** 为 **0** 来存储添加到字符串中的最后一个字符的索引， **ans** 。
*   [遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果当前字符不在 **ans** 中，则将其追加到 **ans** 中，在数组**C【】**中标记为已访问，并将 **pos** 的值更新为 **i** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【pos+1，N–1】**，如果**S【I】**等于**S【0】**，则将其附加到最后一个字符串 **ans** 和[中，断开循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印字符串**和**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to remove the minimum count
// of characters from the string such
// that no subsequence of length 2 repeats
void RemoveCharacters(string s)
{
    // Initialize the final string
    string ans = "";

    // Stores if any character occurs
    // in the final string or not
    bool c[26];

    for (int i = 0; i < 26; i++)
        c[i] = 0;

    // Store the index of the last
    // character added in the string
    int pos = 0;

    // Traverse the string
    for (int i = 0; i < s.size(); i++) {

        // Add all the unique
        // characters
        if (c[s[i] - 'a'] == 0) {
            c[s[i] - 'a'] = 1;
            pos = i;
            ans += s[i];
        }
    }

    // Check if S[0] appears in the
    // range [pos+1, N-1]
    for (int i = pos + 1;
         i < (int)s.size(); i++) {

        // If the characters are the
        // same
        if (s[i] == s[0]) {
            ans += s[i];
            break;
        }
    }

    // Print the resultant string
    cout << ans;
}

// Driver Code
int main()
{
    string S = "abcaadbcd";
    RemoveCharacters(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to remove the minimum count
// of characters from the string such
// that no subsequence of length 2 repeats
static void RemoveCharacters(String s)
{

    // Initialize the final string
    String ans = "";

    // Stores if any character occurs
    // in the final string or not
    int []c = new int[26];

    for (int i = 0; i < 26; i++)
        c[i] = 0;

    // Store the index of the last
    // character added in the string
    int pos = 0;

    // Traverse the string
    for (int i = 0; i < s.length(); i++) {

        // Add all the unique
        // characters
        if (c[(int)s.charAt(i) - 97] == 0) {
            c[(int)s.charAt(i) - 97] = 1;
            pos = i;
            ans += s.charAt(i);
        }
    }

    // Check if S[0] appears in the
    // range [pos+1, N-1]
    for (int i = pos + 1;
         i < s.length(); i++) {

        // If the characters are the
        // same
        if (s.charAt(i) == s.charAt(0)) {
            ans += s.charAt(i);
            break;
        }
    }

    // Print the resultant string
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    String S = "abcaadbcd";
    RemoveCharacters(S);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to remove the minimum count
# of characters from the string such
# that no subsequence of length 2 repeats
def RemoveCharacters(s):

    # Initialize the final string
    ans = ""

    # Stores if any character occurs
    # in the final string or not
    c = [0 for i in range(26)]

    # Store the index of the last
    # character added in the string
    pos = 0

    # Traverse the string
    for i in range(len(s)):

        # Add all the unique
        # characters
        if (c[ord(s[i]) - 97] == 0):
            c[ord(s[i]) - 97] = 1
            pos = i
            ans += s[i]

    # Check if S[0] appears in the
    # range [pos+1, N-1]
    for i in range(pos + 1, len(s), 1):

        # If the characters are the
        # same
        if (s[i] == s[0]):
            ans += s[i]
            break

    # Print the resultant string
    print(ans)

# Driver Code
if __name__ == '__main__':
    S = "abcaadbcd"
    RemoveCharacters(S)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to remove the minimum count
// of characters from the string such
// that no subsequence of length 2 repeats
static void RemoveCharacters(string s)
{

    // Initialize the final string
    string ans = "";

    // Stores if any character occurs
    // in the final string or not
    int []c = new int[26];

    for (int i = 0; i < 26; i++)
        c[i] = 0;

    // Store the index of the last
    // character added in the string
    int pos = 0;

    // Traverse the string
    for (int i = 0; i < s.Length; i++) {

        // Add all the unique
        // characters
        if (c[(int)s[i] - 97] == 0) {
            c[(int)s[i] - 97] = 1;
            pos = i;
            ans += s[i];
        }
    }

    // Check if S[0] appears in the
    // range [pos+1, N-1]
    for (int i = pos + 1;
         i < s.Length; i++) {

        // If the characters are the
        // same
        if (s[i] == s[0]) {
            ans += s[i];
            break;
        }
    }

    // Print the resultant string
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    string S = "abcaadbcd";
    RemoveCharacters(S);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to remove the minimum count
// of characters from the string such
// that no subsequence of length 2 repeats
function RemoveCharacters(s)
{
    // Initialize the final string
    var ans = "";

    // Stores if any character occurs
    // in the final string or not
    var c = new Array(26);
    var i;
    for (i = 0; i < 26; i++)
        c[i] = 0;

    // Store the index of the last
    // character added in the string
    var pos = 0;

    // Traverse the string
    for (i = 0; i < s.length; i++) {

        // Add all the unique
        // characters
        if (c[s[i].charCodeAt() - 97] == 0) {
            c[s[i].charCodeAt() - 97] = 1;
            pos = i;
            ans += s[i];
        }
    }

    // Check if S[0] appears in the
    // range [pos+1, N-1]
    for (i = pos + 1;
         i < s.length; i++) {

        // If the characters are the
        // same
        if (s[i] == s[0]) {
            ans += s[i];
            break;
        }
    }

    // Print the resultant string
    document.write(ans);
}

// Driver Code
    var S = "abcaadbcd";
    RemoveCharacters(S);

// This code is contributed by bgangwar59.
</script>
```

**Output:** 

```
abcd
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)