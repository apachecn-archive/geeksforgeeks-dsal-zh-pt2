# 使用二分搜索法语由元音组成的最长子串

> 原文:[https://www . geesforgeks . org/最长子串-由-元音组成-使用-二进制-搜索/](https://www.geeksforgeeks.org/longest-substring-consisting-of-vowels-using-binary-search/)

给定长度为 **N** 的字符串 **str** ，任务是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)技术找到只包含元音的最长子字符串。
**示例:**

> **输入:** str = "baeicba"
> **输出:** 3
> **解释:**
> 只包含元音的最长子串是“aei”。
> **输入:** str = "aeiou"
> **输出:** 5

**方法:**参考元音的[最长子串](https://www.geeksforgeeks.org/longest-substring-vowels/)以获得 O(N)复杂度的方法。
**二分搜索法方法:**在本文中，我们使用基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的方法:
按照以下步骤解决问题:

1.  将二分搜索法涂抹在从 1 到 **N** 的长度范围内。
2.  对于每个**mid**-值，检查是否存在长度为 **mid** 的子串，该子串仅由元音组成。
3.  如果存在长度为 **mid** 的子串，则更新 **max** 的值，并将 **l** 更新为 **mid+1** ，检查是否存在长度大于 **mid** 的仅由元音组成的子串。
4.  如果不存在长度为 **mid** 的子串，将 **r** 更新为**mid 1**，检查是否存在长度小于 **mid** 且仅由元音组成的子串。
5.  重复以上三个步骤，直到 l 小于或等于 r。
6.  返回最终获得的**最大**长度。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a character
// is vowel or not
bool vowel(int vo)
{
    // 0-a 1-b 2-c and so on 25-z
    if (vo == 0 || vo == 4
        || vo == 8 || vo == 14
        || vo == 20)
        return true;
    else
        return false;
}

// Function to check if any
// substring of length k exists
// which contains only vowels
bool check(string s, int k)
{
    vector<int> cnt(26, 0);
    for (int i = 0; i < k - 1; i++) {
        cnt[s[i] - 'a']++;
    }

    // Applying sliding window to get
    // all substrings of length K
    for (int i = k - 1; i < s.size();
         i++) {
        cnt[s[i] - 'a']++;
        int flag1 = 0;
        for (int j = 0; j < 26; j++) {
            if (vowel(j) == false
                && cnt[j] > 0) {
                flag1 = 1;
                break;
            }
        }
        if (flag1 == 0)
            return true;

        // Remove the occurence of
        // (i-k+1)th character
        cnt[s[i - k + 1] - 'a']--;
    }

    return false;
}

// Function to perform  Binary Search
int longestSubstring(string s)
{
    int l = 1, r = s.size();
    int maxi = 0;

    // Doing binary search on the lengths
    while (l <= r) {
        int mid = (l + r) / 2;
        if (check(s, mid)) {
            l = mid + 1;
            maxi = max(maxi, mid);
        }
        else
            r = mid - 1;
    }
    return maxi;
}

// Driver Code
int main()
{
    string s = "sedrewaefhoiu";
    cout << longestSubstring(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to check if a character
// is vowel or not
static boolean vowel(int vo)
{
    // 0-a 1-b 2-c and so on 25-z
    if (vo == 0 || vo == 4 ||
        vo == 8 || vo == 14 ||
        vo == 20)
        return true;
    else
        return false;
}

// Function to check if any
// subString of length k exists
// which contains only vowels
static boolean check(String s, int k)
{
    int []cnt = new int[26];
    for (int i = 0; i < k - 1; i++)
    {
        cnt[s.charAt(i) - 'a']++;
    }

    // Applying sliding window to get
    // all subStrings of length K
    for (int i = k - 1; i < s.length(); i++)
    {
        cnt[s.charAt(i) - 'a']++;
        int flag1 = 0;
        for (int j = 0; j < 26; j++)
        {
            if (vowel(j) == false && cnt[j] > 0)
            {
                flag1 = 1;
                break;
            }
        }
        if (flag1 == 0)
            return true;

        // Remove the occurence of
        // (i-k+1)th character
        cnt[s.charAt(i - k + 1) - 'a']--;
    }

    return false;
}

// Function to perform Binary Search
static int longestSubString(String s)
{
    int l = 1, r = s.length();
    int maxi = 0;

    // Doing binary search on the lengths
    while (l <= r)
    {
        int mid = (l + r) / 2;
        if (check(s, mid))
        {
            l = mid + 1;
            maxi = Math.max(maxi, mid);
        }
        else
            r = mid - 1;
    }
    return maxi;
}

// Driver Code
public static void main(String[] args)
{
    String s = "sedrewaefhoiu";
    System.out.print(longestSubString(s));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to check if a character
# is vowel or not
def vowel(vo):

    # 0-a 1-b 2-c and so on 25-z
    if (vo == 0 or vo == 4 or
        vo == 8 or vo == 14 or
        vo == 20):
        return True
    else:
        return False

# Function to check if any
# substring of length k exists
# which contains only vowels
def check(s, k):

    cnt = [0] * 26
    for i in range (k - 1):
        cnt[ord(s[i]) - ord('a')] += 1

    # Applying sliding window to get
    # all substrings of length K
    for i in range (k - 1, len(s)):
        cnt[ord(s[i]) - ord('a')] += 1
        flag1 = 0
        for j in range (26):
            if (vowel(j) == False
                and cnt[j] > 0):
                flag1 = 1
                break

        if (flag1 == 0):
            return True

        # Remove the occurence of
        # (i-k+1)th character
        cnt[ord(s[i - k + 1]) - ord('a')] -= 1

    return False

# Function to perform  Binary Search
def longestSubstring(s):

    l = 1
    r = len(s)
    maxi = 0

    # Doing binary search on the lengths
    while (l <= r):
        mid = (l + r) // 2
        if (check(s, mid)):
            l = mid + 1
            maxi = max(maxi, mid)
        else:
            r = mid - 1
    return maxi

# Driver Code
if __name__ == "__main__": 
    s = "sedrewaefhoiu"
    print (longestSubstring(s))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to check if a character
// is vowel or not
static bool vowel(int vo)
{
    // 0-a 1-b 2-c and so on 25-z
    if (vo == 0 || vo == 4 ||
        vo == 8 || vo == 14 ||
        vo == 20)
        return true;
    else
        return false;
}

// Function to check if any
// subString of length k exists
// which contains only vowels
static bool check(String s, int k)
{
    int []cnt = new int[26];
    for (int i = 0; i < k - 1; i++)
    {
        cnt[s[i] - 'a']++;
    }

    // Applying sliding window to get
    // all subStrings of length K
    for (int i = k - 1; i < s.Length; i++)
    {
        cnt[s[i] - 'a']++;
        int flag1 = 0;
        for (int j = 0; j < 26; j++)
        {
            if (vowel(j) == false && cnt[j] > 0)
            {
                flag1 = 1;
                break;
            }
        }
        if (flag1 == 0)
            return true;

        // Remove the occurence of
        // (i-k+1)th character
        cnt[s[i - k + 1] - 'a']--;
    }

    return false;
}

// Function to perform Binary Search
static int longestSubString(String s)
{
    int l = 1, r = s.Length;
    int maxi = 0;

    // Doing binary search on the lengths
    while (l <= r)
    {
        int mid = (l + r) / 2;
        if (check(s, mid))
        {
            l = mid + 1;
            maxi = Math.Max(maxi, mid);
        }
        else
            r = mid - 1;
    }
    return maxi;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "sedrewaefhoiu";
    Console.Write(longestSubString(s));
}
}

// This code is contributed by sapnasingh4991
```

**Output:** 

```
3

```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*