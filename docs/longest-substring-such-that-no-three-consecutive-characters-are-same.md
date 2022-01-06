# 最长的子串，这样没有三个连续的字符是相同的

> 原文:[https://www . geeksforgeeks . org/最长子串-这样-没有-三个连续字符是相同的/](https://www.geeksforgeeks.org/longest-substring-such-that-no-three-consecutive-characters-are-same/)

给定字符串 **str** ，任务是找到 **str** 的最长子串的长度，使得子串中没有三个连续的字符相同。
**例:**

> **输入:**str = " baababbb "
> **输出:**7
> “aabbbb”为必输子串。
> **输入:** str = "babba"
> **输出:** 5
> 给定的字符串本身就是最长的子串。

**方法:**可以按照以下步骤解决问题:

*   如果给定字符串的长度小于 **3** ，那么字符串的长度就是答案。
*   最初将 **temp** 和 **ans** 初始化为 **2** ，因为当给定字符串的长度大于 **2** 时，这是最长子字符串的最小长度。
*   重复从 **2** 到**N–1**的字符串，如果**字符串为【I】，则将温度增加 **1** ！= str[I–1]**或 **str[i]！= str[I–2]**。
*   Else 重新初始化 **temp = 2** 和 ans = max(ans，temp)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the
// longest substring such that no three
// consecutive characters are same
int maxLenSubStr(string& s)
{
    // If the length of the given string
    // is less than 3
    if (s.length() < 3)
        return s.length();

    // Initialize temporary and final ans
    // to 2 as this is the minimum length
    // of substring when length of the given
    // string is greater than 2
    int temp = 2;
    int ans = 2;

    // Traverse the string from the
    // third character to the last
    for (int i = 2; i < s.length(); i++) {

        // If no three consecutive characters
        // are same then increment temporary count
        if (s[i] != s[i - 1] || s[i] != s[i - 2])
            temp++;

        // Else update the final ans and
        // reset the temporary count
        else {
            ans = max(temp, ans);
            temp = 2;
        }
    }

    ans = max(temp, ans);

    return ans;
}

// Driver code
int main()
{
    string s = "baaabbabbb";

    cout << maxLenSubStr(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the length of the
// longest substring such that no three
// consecutive characters are same
static int maxLenSubStr(String s)
{
    // If the length of the given string
    // is less than 3
    if (s.length() < 3)
        return s.length();

    // Initialize temporary and final ans
    // to 2 as this is the minimum length
    // of substring when length of the given
    // string is greater than 2
    int temp = 2;
    int ans = 2;

    // Traverse the string from the
    // third character to the last
    for (int i = 2; i < s.length(); i++)
    {

        // If no three consecutive characters
        // are same then increment temporary count
        if (s.charAt(i) != s.charAt(i - 1) ||
            s.charAt(i) != s.charAt(i - 2))
            temp++;

        // Else update the final ans and
        // reset the temporary count
        else
        {
            ans = Math.max(temp, ans);
            temp = 2;
        }
    }
    ans = Math.max(temp, ans);

    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "baaabbabbb";

    System.out.println(maxLenSubStr(s));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of the
# longest substring such that no three
# consecutive characters are same
def maxLenSubStr(s):

    # If the length of the given string
    # is less than 3
    if (len(s) < 3):
        return len(s)

    # Initialize temporary and final ans
    # to 2 as this is the minimum length
    # of substring when length of the given
    # string is greater than 2
    temp = 2
    ans = 2

    # Traverse the string from the
    # third character to the last
    for i in range(2, len(s)):

        # If no three consecutive characters
        # are same then increment temporary count
        if (s[i] != s[i - 1] or s[i] != s[i - 2]):
            temp += 1

        # Else update the final ans and
        # reset the temporary count
        else:
            ans = max(temp, ans)
            temp = 2
    ans = max(temp, ans)

    return ans

# Driver code
s = "baaabbabbb"

print(maxLenSubStr(s))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the length of the
// longest substring such that no three
// consecutive characters are same
static int maxLenSubStr(String s)
{
    // If the length of the given string
    // is less than 3
    if (s.Length < 3)
        return s.Length;

    // Initialize temporary and final ans
    // to 2 as this is the minimum length
    // of substring when length of the given
    // string is greater than 2
    int temp = 2;
    int ans = 2;

    // Traverse the string from the
    // third character to the last
    for (int i = 2; i < s.Length; i++)
    {

        // If no three consecutive characters
        // are same then increment temporary count
        if (s[i] != s[i - 1] ||
            s[i] != s[i - 2])
            temp++;

        // Else update the final ans and
        // reset the temporary count
        else
        {
            ans = Math.Max(temp, ans);
            temp = 2;
        }
    }
    ans = Math.Max(temp, ans);

    return ans;
}

// Driver code
static public void Main ()
{
    String s = "baaabbabbb";
    Console.Write(maxLenSubStr(s));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the length of the
    // longest substring such that no three
    // consecutive characters are same
    function maxLenSubStr(s)
    {
        // If the length of the given string
        // is less than 3
        if (s.length < 3)
            return s.length;

        // Initialize temporary and final ans
        // to 2 as this is the minimum length
        // of substring when length of the given
        // string is greater than 2
        let temp = 2;
        let ans = 2;

        // Traverse the string from the
        // third character to the last
        for (let i = 2; i < s.length; i++)
        {

            // If no three consecutive characters
            // are same then increment temporary count
            if (s[i] != s[i - 1] ||
                s[i] != s[i - 2])
                temp++;

            // Else update the final ans and
            // reset the temporary count
            else
            {
                ans = Math.max(temp, ans);
                temp = 2;
            }
        }
        ans = Math.max(temp, ans);

        return ans;
    }

    let s = "baaabbabbb";
    document.write(maxLenSubStr(s));

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N)，其中 N 是字符串的长度。
**空间复杂度:** O(1)