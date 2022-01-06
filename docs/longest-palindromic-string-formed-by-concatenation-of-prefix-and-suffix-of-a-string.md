# 由一个字符串的前缀和后缀串联而成的最长回文字符串

> 原文:[https://www . geesforgeks . org/最长回文字符串由字符串的前缀和后缀串联而成/](https://www.geeksforgeeks.org/longest-palindromic-string-formed-by-concatenation-of-prefix-and-suffix-of-a-string/)

给定字符串 **str** ，任务是找到由给定字符串 **str** 的前缀和后缀串联而成的[最长回文子串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)。

**示例:**

> **输入:**str = " rombobinimor "
> **输出:**romannimor
> **解释:**
> 字符串“rombob”(前缀)和“mor”(后缀)的串联就是“rombobmor”，是回文字符串。
> 字符串“rom”(前缀)和“innimor”(后缀)的串联就是“rominnimor”，它是一个回文字符串。
> 但“rominnimor”的长度大于“rombobmor”。
> 因此，“rominnimor”是必需的字符串。
> 
> **输入:** str = "geekinakeeg"
> **输出:**geek akeeg
> **解释:**
> 字符串“geek”(前缀)和“akeg”(后缀)的串联是“geek akeg”，是回文字符串。
> 字符串“geeki”(前缀)和“keeg”(后缀)的串联就是“geekigeek”，它是一个回文字符串。
> 但是“极客”的长度等于“极客”。
> 因此，以上任意一个字符串都是必选字符串。

**方法:**思路是利用 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)找到最长的合适前缀，它是给定字符串后缀在 O(N)时间内的回文。

1.  找出最长的前缀(比如 **s[0，l]** )，它也是字符串后缀(比如 **s[n-l，n-1]** )的回文。前缀和后缀不重叠。
2.  从剩余的子串( **s[l+1，n-l-1]** )中，找出最长的回文子串(比如 **ans** )，它要么是剩余串的后缀，要么是前缀。
3.  **s[0，l]** 、 **ans** 和 **s[n-l，n-l-1]** 的串联是最长的回文子串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function used to calculate the longest prefix
// which is also a suffix
int kmp(string s)
{
    vector<int> lps(s.size(), 0);

    // Traverse the string
    for (int i = 1; i < s.size(); i++) {

        int previous_index = lps[i - 1];

        while (previous_index > 0
               && s[i] != s[previous_index]) {

            previous_index = lps[previous_index - 1];
        }

        // Update the lps size
        lps[i] = previous_index
                 + (s[i] == s[previous_index] ? 1 : 0);
    }

    // Returns size of lps
    return lps[lps.size() - 1];
}

// Function to calculate the length of longest
// palindromic substring which is either a
// suffix or prefix
int remainingStringLongestPallindrome(string s)
{
    // Append a character to separate the string
    // and reverse of the string
    string t = s + "?";

    // Reverse the string
    reverse(s.begin(), s.end());

    // Append the reversed string
    t += s;

    return kmp(t);
}

// Function to find the Longest palindromic
// string formed from concatenation of prefix
// and suffix of a given string
string longestPrefixSuffixPallindrome(string s)
{
    int length = 0;
    int n = s.size();

    // Calculating the length for which prefix
    // is reverse of suffix
    for (int i = 0, j = n - 1; i < j; i++, j--) {
        if (s[i] != s[j]) {
            break;
        }
        length++;
    }

    // Append prefix to the answer
    string ans = s.substr(0, length);

    // Store the remaining string
    string remaining = s.substr(length,
                                (n - (2 * length)));

    // If the remaining string is not empty
    // that means that there can be a palindrome
    // substring which can be added between the
    // suffix & prefix
    if (remaining.size()) {

        // Calculate the length of longest prefix
        // palindromic substring
        int longest_prefix
            = remainingStringLongestPallindrome(remaining);

        // Reverse the given string to find the
        // longest palindromic suffix
        reverse(remaining.begin(), remaining.end());

        // Calculate the length of longest prefix
        // palindromic substring
        int longest_suffix
            = remainingStringLongestPallindrome(remaining);

        // If the prefix palindrome is greater
        // than the suffix palindrome
        if (longest_prefix > longest_suffix) {

            reverse(remaining.begin(), remaining.end());

            // Append the prefix to the answer
            ans += remaining.substr(0, longest_prefix);
        }

        // If the suffix palindrome is greater than
        // the prefix palindrome

        else {

            // Append the suffix to the answer
            ans += remaining.substr(0, longest_suffix);
        }
    }

    // Finally append the suffix to the answer
    ans += s.substr(n - length, length);

    // Return the answer string
    return ans;
}

// Driver Code
int main()
{
    string str = "rombobinnimor";

    cout << longestPrefixSuffixPallindrome(str)
         << endl;
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function used to calculate
# the longest prefix
# which is also a suffix
def kmp(s):

    lps = [0] * (len(s))

    # Traverse the string
    for i in range (1 , len(s)):

        previous_index = lps[i - 1]

        while (previous_index > 0 and
               s[i] != s[previous_index]):

            previous_index = lps[previous_index - 1]

        # Update the lps size
        lps[i] = previous_index
        if (s[i] == s[previous_index]):
            lps[i] += 1

    # Returns size of lps
    return lps[- 1]

# Function to calculate the length of
# longest palindromic substring which
# is either a suffix or prefix
def remainingStringLongestPallindrome(s):

    # Append a character to separate
    # the string and reverse of the string
    t = s + "?"

    # Reverse the string
    s = s[: : -1]

    # Append the reversed string
    t += s

    return kmp(t)

# Function to find the Longest
# palindromic string formed from
# concatenation of prefix
# and suffix of a given string
def longestPrefixSuffixPallindrome(s):

    length = 0
    n = len(s)

    # Calculating the length
    # for which prefix
    # is reverse of suffix
    i = 0
    j = n - 1
    while i < j:
        if (s[i] != s[j]):
            break
        i += 1
        j -= 1

        length += 1

    # Append prefix to the answer
    ans = s[0 : length]

    # Store the remaining string
    remaining = s[length :  length + (n - (2 * length))]

    # If the remaining string is not empty
    # that means that there can be a palindrome
    # substring which can be added between the
    # suffix & prefix
    if (len(remaining)):

        # Calculate the length of longest prefix
        # palindromic substring
        longest_prefix = remainingStringLongestPallindrome(remaining);

        # Reverse the given string to find the
        # longest palindromic suffix
        remaining = remaining[: : -1]

        # Calculate the length of longest prefix
        # palindromic substring
        longest_suffix = remainingStringLongestPallindrome(remaining);

        # If the prefix palindrome is greater
        # than the suffix palindrome
        if (longest_prefix > longest_suffix):

            remaining = remaining[: : -1]

            # Append the prefix to the answer
            ans += remaining[0 : longest_prefix]

        # If the suffix palindrome is
        # greater than the prefix palindrome
        else:

            # Append the suffix to the answer
            ans += remaining[0 : longest_suffix]

    # Finally append the suffix to the answer
    ans += s[n - length : n]

    # Return the answer string
    return ans

# Driver Code
if __name__ == "__main__": 
    st = "rombobinnimor"
    print (longestPrefixSuffixPallindrome(st))

# This code is contributed by Chitranayal
```

**Output:** 

```
rominnimor
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(N)。