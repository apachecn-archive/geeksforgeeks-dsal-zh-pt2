# 通过一次添加一个字符来合并两个字符串，在词典上可能最大

> 原文:[https://www . geeksforgeeks . org/按字典顺序一次添加一个字符合并两个字符串最大可能数/](https://www.geeksforgeeks.org/lexicographically-largest-possible-by-merging-two-strings-by-adding-one-character-at-a-time/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T，**的任务是通过从任一[字符串](https://www.geeksforgeeks.org/string-data-structure/)的开头一次添加一个字符来合并这两个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，以形成合成的[字符串](https://www.geeksforgeeks.org/string-data-structure/)。合成的[串](https://www.geeksforgeeks.org/string-data-structure/)应该是[字典上最大的串](https://www.geeksforgeeks.org/lexicographically-largest-string-formed-from-the-characters-in-range-l-and-r/) ，可以由[串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** 合并而成。

**示例:**

> **输入:** S = "dbcbb "，t = " cdbbb "
> T3】输出:dcdbcbbb
> 
> **输入:**S =**“**极客**”，**T =**“**伪造者”
> **输出:**gforgeeckmous

**方法:**解决问题最简单的思路就是贪婪地从字典序上比其他字符大的字符串中选择第一个字符。因此，可以使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)和[递归](https://www.geeksforgeeks.org/recursion/)来解决问题。按照以下步骤解决问题:

*   如果[弦](https://www.geeksforgeeks.org/string-data-structure/)长度中的任意一个为 **0** ，则返回 **S + T** 作为答案。
*   如果 **S** 在词典上大于 **T，**则返回**S【0】+****large stmerge(S . substr(1)，T)** 。
*   否则，取 **T** 的第一个字符，调用递归函数 **largestMerge(S，T.substr(1))。**

下面是上述方法的实现:

## C++

```
// C++ program for the approach

#include <bits/stdc++.h>
using namespace std;

// Recursive  bfunction for finding
// the lexicographically largest string
string largestMerge(string s1, string s2)
{
    // If either of the string length is 0,
    // return the other string
    if (s1.size() == 0 || s2.size() == 0)
        return s1 + s2;

    // If s1 is lexicographically
    // larger than s2
    if (s1 > s2) {

        // Take first character of s1
        // and call the function
        return s1[0] + largestMerge(s1.substr(1), s2);
    }

    // Take first character of s2
    // and recursively call function for
    // remaining string
    return s2[0] + largestMerge(s1, s2.substr(1));
}

// Driver Code
int main()
{
    // Given Input
    string s1 = "geeks";
    string s2 = "forgeeks";

    // Function Call
    cout << largestMerge(s1, s2) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the approach
public class Main
{
    // Recursive  bfunction for finding
    // the lexicographically largest string
    static String largestMerge(String s1, String s2)
    {

        // If either of the string length is 0,
        // return the other string
        if (s1.length() == 0 || s2.length() == 0)
            return s1 + s2;

        // If s1 is lexicographically
        // larger than s2
        if (s1.compareTo(s2) > 0) {

            // Take first character of s1
            // and call the function
            return s1.charAt(0)
                + largestMerge(s1.substring(1), s2);
        }

        // Take first character of s2
        // and recursively call function for
        // remaining string
        return s2.charAt(0) + largestMerge(s1, s2.substring(1));
    }

    public static void main(String[] args)
    {

        // Given Input
        String s1 = "geeks";
        String s2 = "forgeeks";

        // Function Call
        System.out.print(largestMerge(s1, s2));
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python program for the above approach

# Recursive function for finding
# the lexicographically largest string
def largestMerge(s1, s2):

    # If either of the string length is 0,
    # return the other string
    if len(s1) == 0 or len(s2) == 0:
        return s1+s2

    # If s1 is lexicographically
    # larger than s2
    if(s1 > s2):

        # Take first character of s1
        # and call the function
        return s1[0]+largestMerge(s1[1:], s2)

    # Take first character of s2
    # and recursively call function for
    # remaining string
    return s2[0]+largestMerge(s1, s2[1:])

# Driver code
if __name__ == '__main__':

    # Given Input
    s1 = "geeks"
    s2 = "forgeeks"

    # Function call
    print(largestMerge(s1, s2))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the approach
using System;
class GFG {
    // Recursive  bfunction for finding
    // the lexicographically largest string
    static string largestMerge(string s1, string s2)
    {
        // If either of the string length is 0,
        // return the other string
        if (s1.Length == 0 || s2.Length == 0)
            return s1 + s2;

        // If s1 is lexicographically
        // larger than s2
        if (string.Compare(s1, s2) == 1) {

            // Take first character of s1
            // and call the function
            return s1[0]
                + largestMerge(s1.Substring(1), s2);
        }

        // Take first character of s2
        // and recursively call function for
        // remaining string
        return s2[0] + largestMerge(s1, s2.Substring(1));
    }

    // Driver Code
    public static void Main()
    {
        // Given Input
        string s1 = "geeks";
        string s2 = "forgeeks";

        // Function Call
        Console.Write(largestMerge(s1, s2));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript program for the approach

    // Recursive bfunction for finding
    // the lexicographically largest string
    const largestMerge = (s1, s2) =>
    {

        // If either of the string length is 0,
        // return the other string
        if (s1.length == 0 || s2.length == 0)
            return s1 + s2;

        // If s1 is lexicographically
        // larger than s2
        if (s1 > s2) {

            // Take first character of s1
            // and call the function
            return s1[0] + largestMerge(s1.substr(1), s2);
        }

        // Take first character of s2
        // and recursively call function for
        // remaining string
        return s2[0] + largestMerge(s1, s2.substr(1));
    }

    // Driver Code
    // Given Input
    s1 = "geeks";
    s2 = "forgeeks";

    // Function Call
    document.write(largestMerge(s1, s2));

    // This code is contributed by rakeshsahni
</script>
```

**Output**

```
gforgeekseeks
```

***时间复杂度:** O(M×N)，其中 **M** 和 **N** 分别为弦 **s1** 和 **s2** 的长度。*
***辅助空间:** O(1)*