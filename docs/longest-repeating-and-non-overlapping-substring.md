# 最长重复且不重叠的子串

> 原文:[https://www . geesforgeks . org/最长重复且不重叠的子串/](https://www.geeksforgeeks.org/longest-repeating-and-non-overlapping-substring/)

给定一个字符串 **str** ，找出其中重复最长的非重叠子字符串。换句话说，找到两个最大长度不重叠的相同子串。如果存在多个这样的子串，返回其中任何一个。
**例:**

```
Input : str = "geeksforgeeks"
Output : geeks

Input : str = "aab"
Output : a

Input : str = "aabaabaaba"
Output : aaba

Input : str = "aaaaaaaaaaa"
Output : aaaaa

Input : str = "banana"
Output : an 
         or na
```

**天真的解决方案**:通过获取所有可能的子串，并且对于所有子串，如果存在相同的子串，则检查剩余的(非重叠的)串，可以很容易地解决问题。总共有 0(n)<sup>2</sup>个子字符串，对照剩余字符串检查它们需要 0(n)个时间。所以上述解的整体时间复杂度为 O(n <sup>3</sup> )。
**动态编程**:这个问题可以用动态编程在 O(n <sup>2</sup> 时间内解决。基本思想是为字符串中的所有前缀找到最长的重复后缀。

```
Length of longest non-repeating substring can be recursively
defined as below.

LCSRe(i, j) stores length of the matching and
            non-overlapping substrings ending 
            with i'th and j'th characters.

If str[i-1] == str[j-1] && (j-i) > LCSRe(i-1, j-1)
     LCSRe(i, j) = LCSRe(i-1, j-1) + 1, 
Else
     LCSRe(i, j) = 0

Where i varies from 1 to n and 
      j varies from i+1 to n
```

为了避免重叠，我们必须确保后缀的长度在任何时刻都小于(j-i)。
LCSRe(I，j)的最大值提供了最长重复子串的长度，子串本身可以利用公共后缀的长度和结束索引找到。
下面是递归的实现。

## C++

```
// C++ program to find the longest repeated
// non-overlapping substring
#include<bits/stdc++.h>
using namespace std;

// Returns the longest repeating non-overlapping
// substring in str
string longestRepeatedSubstring(string str)
{
    int n = str.length();
    int LCSRe[n+1][n+1];

    // Setting all to 0
    memset(LCSRe, 0, sizeof(LCSRe));

    string res; // To store result
    int res_length  = 0; // To store length of result

    // building table in bottom-up manner
    int i, index = 0;
    for (i=1; i<=n; i++)
    {
        for (int j=i+1; j<=n; j++)
        {
            // (j-i) > LCSRe[i-1][j-1] to remove
            // overlapping
            if (str[i-1] == str[j-1] &&
                LCSRe[i-1][j-1] < (j - i))
            {
                LCSRe[i][j] = LCSRe[i-1][j-1] + 1;

                // updating maximum length of the
                // substring and updating the finishing
                // index of the suffix
                if (LCSRe[i][j] > res_length)
                {
                    res_length = LCSRe[i][j];
                    index = max(i, index);
                }
            }
            else
                LCSRe[i][j] = 0;
        }
    }

    // If we have non-empty result, then insert all
    // characters from first character to last
    // character of string
    if (res_length > 0)
        for (i = index - res_length + 1; i <= index; i++)
            res.push_back(str[i-1]);

    return res;
}

// Driver program to test the above function
int main()
{
    string str = "geeksforgeeks";
    cout << longestRepeatedSubstring(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest repeated
// non-overlapping substring

class GFG {

// Returns the longest repeating non-overlapping
// substring in str
    static String longestRepeatedSubstring(String str) {
        int n = str.length();
        int LCSRe[][] = new int[n + 1][n + 1];

        String res = ""; // To store result
        int res_length = 0; // To store length of result

        // building table in bottom-up manner
        int i, index = 0;
        for (i = 1; i <= n; i++) {
            for (int j = i + 1; j <= n; j++) {
                // (j-i) > LCSRe[i-1][j-1] to remove
                // overlapping
                if (str.charAt(i - 1) == str.charAt(j - 1)
                        && LCSRe[i - 1][j - 1] < (j - i)) {
                    LCSRe[i][j] = LCSRe[i - 1][j - 1] + 1;

                    // updating maximum length of the
                    // substring and updating the finishing
                    // index of the suffix
                    if (LCSRe[i][j] > res_length) {
                        res_length = LCSRe[i][j];
                        index = Math.max(i, index);
                    }
                } else {
                    LCSRe[i][j] = 0;
                }
            }
        }

        // If we have non-empty result, then insert all
        // characters from first character to last
        // character of String
        if (res_length > 0) {
            for (i = index - res_length + 1; i <= index; i++) {
                res += str.charAt(i - 1);
            }
        }

        return res;
    }

// Driver program to test the above function
    public static void main(String[] args) {
        String str = "geeksforgeeks";
        System.out.println(longestRepeatedSubstring(str));
    }
}
// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python 3 program to find the longest repeated
# non-overlapping substring

# Returns the longest repeating non-overlapping
# substring in str
def longestRepeatedSubstring(str):

    n = len(str)
    LCSRe = [[0 for x in range(n + 1)]
                for y in range(n + 1)]

    res = "" # To store result
    res_length = 0 # To store length of result

    # building table in bottom-up manner
    index = 0
    for i in range(1, n + 1):
        for j in range(i + 1, n + 1):

            # (j-i) > LCSRe[i-1][j-1] to remove
            # overlapping
            if (str[i - 1] == str[j - 1] and
                LCSRe[i - 1][j - 1] < (j - i)):
                LCSRe[i][j] = LCSRe[i - 1][j - 1] + 1

                # updating maximum length of the
                # substring and updating the finishing
                # index of the suffix
                if (LCSRe[i][j] > res_length):
                    res_length = LCSRe[i][j]
                    index = max(i, index)

            else:
                LCSRe[i][j] = 0

    # If we have non-empty result, then insert
    # all characters from first character to
    # last character of string
    if (res_length > 0):
        for i in range(index - res_length + 1,
                                    index + 1):
            res = res + str[i - 1]

    return res

# Driver Code
if __name__ == "__main__":

    str = "geeksforgeeks"
    print(longestRepeatedSubstring(str))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the longest repeated
// non-overlapping substring
using System;

public class GFG {

// Returns the longest repeating non-overlapping
// substring in str
    static String longestRepeatedSubstring(String str) {
        int n = str.Length;
        int [,]LCSRe = new int[n + 1,n + 1];

        String res = ""; // To store result
        int res_length = 0; // To store length of result

        // building table in bottom-up manner
        int i, index = 0;
        for (i = 1; i <= n; i++) {
            for (int j = i + 1; j <= n; j++) {
                // (j-i) > LCSRe[i-1][j-1] to remove
                // overlapping
                if (str[i - 1] == str[j - 1]
                        && LCSRe[i - 1,j - 1] < (j - i)) {
                    LCSRe[i,j] = LCSRe[i - 1,j - 1] + 1;

                    // updating maximum length of the
                    // substring and updating the finishing
                    // index of the suffix
                    if (LCSRe[i,j] > res_length) {
                        res_length = LCSRe[i,j];
                        index = Math.Max(i, index);
                    }
                } else {
                    LCSRe[i,j] = 0;
                }
            }
        }

        // If we have non-empty result, then insert all
        // characters from first character to last
        // character of String
        if (res_length > 0) {
            for (i = index - res_length + 1; i <= index; i++) {
                res += str[i - 1];
            }
        }

        return res;
    }

// Driver program to test the above function
    public static void Main() {
        String str = "geeksforgeeks";
        Console.WriteLine(longestRepeatedSubstring(str));
    }
}
// This code is contributed by Rajput-JI
```

## java 描述语言

```
<script>
// Javascript program to find the longest repeated
// non-overlapping substring

    // Returns the longest repeating non-overlapping
    // substring in str
    function longestRepeatedSubstring(str)
    {
        let n = str.length;
        let LCSRe = new Array(n+1);
        for(let i = 0; i < n + 1; i++)
        {
            LCSRe[i] = new Array(n+1);
        }
        for(let i = 0; i < n + 1; i++)
        {
            for(let j = 0; j < n + 1; j++)
            {
                LCSRe[i][j] = 0;
            }
        }

        let res = ""; // To store result
        let res_length = 0; // To store length of result

        // building table in bottom-up manner
        let i, index = 0;
        for (i = 1; i <= n; i++)
        {
            for (let j = i + 1; j <= n; j++)
            {

                // (j-i) > LCSRe[i-1][j-1] to remove
                // overlapping
                if (str[i-1] == str[j-1]
                        && LCSRe[i - 1][j - 1] < (j - i))
                {
                    LCSRe[i][j] = LCSRe[i - 1][j - 1] + 1;

                    // updating maximum length of the
                    // substring and updating the finishing
                    // index of the suffix
                    if (LCSRe[i][j] > res_length)
                    {
                        res_length = LCSRe[i][j];
                        index = Math.max(i, index);
                    }
                }
                else
                {
                    LCSRe[i][j] = 0;
                }
            }
        }

        // If we have non-empty result, then insert all
        // characters from first character to last
        // character of String
        if (res_length > 0) {
            for (i = index - res_length + 1; i <= index; i++) {
                res += str.charAt(i - 1);
            }
        }

        return res;
    }

    // Driver program to test the above function
    let str= "geeksforgeeks";
    document.write(longestRepeatedSubstring(str));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
geeks
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup> )
**参考文献:**
[https://www.geeksforgeeks.org/longest-common-substring/](https://www.geeksforgeeks.org/longest-common-substring/)
本文由**阿尤什·坎德里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。