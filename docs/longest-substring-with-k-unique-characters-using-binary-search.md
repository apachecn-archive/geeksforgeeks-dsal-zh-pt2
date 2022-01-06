# 使用二分搜索法的 K 个唯一字符的最长子串

> 原文:[https://www . geesforgeks . org/最长-子串-带-k-唯一-字符-使用-二进制-搜索/](https://www.geeksforgeeks.org/longest-substring-with-k-unique-characters-using-binary-search/)

给定一个字符串 **str** 和一个整数 **K** ，任务是打印可能最长的子字符串的长度，该子字符串正好具有 **K** 个唯一字符。如果有多个可能长度最长的子串，则打印其中任何一个，如果没有可能的子串，则打印 **-1** 。

**示例:**

> **输入:**str = " aabacbebe "，K = 3
> **输出:**7
> “cbebbe”为必输子串。
> 
> **输入:** str = "aabc "，K = 4
> **输出:** -1

**方法:**在[这篇](https://www.geeksforgeeks.org/find-the-longest-substring-with-k-unique-characters-in-a-given-string/)文章中已经讨论了解决这个问题的方法。在本文中，将讨论基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的方法。二分搜索法将应用于至少具有 **K** 个唯一字符的子串的长度。假设我们尝试长度 **len** 并检查大小为 **len** 的子串是否存在，该子串具有至少 k 个唯一字符。如果可能，则通过搜索最大可能长度(即输入字符串的大小)来尝试最大化大小。如果不可能，那么就寻找一个尺寸更小的镜头。
为了检查二分搜索法给出的长度是否有 k 个唯一的字符，可以用一个集合来插入所有的字符，然后如果集合的大小小于 k，那么答案是不可能的，否则二分搜索法给出的答案就是最大答案。
二分搜索法在这里是适用的，因为我们知道对于某个镜头，答案是否可能，我们希望最大化镜头，因此搜索域发生变化，我们从这个镜头搜索到 n。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if there
// is a substring of length len
// with <=k unique characters
bool isValidLen(string s, int len, int k)
{

    // Size of the string
    int n = s.size();

    // Map to store the characters
    // and their frequency
    unordered_map<char, int> mp;
    int right = 0;

    // Update the map for the
    // first substring
    while (right < len) {
        mp[s[right]]++;
        right++;
    }

    if (mp.size() <= k)
        return true;

    // Check for the rest of the substrings
    while (right < n) {

        // Add the new character
        mp[s[right]]++;

        // Remove the first character
        // of the previous window
        mp[s[right - len]]--;

        // Update the map
        if (mp[s[right - len]] == 0)
            mp.erase(s[right - len]);
        if (mp.size() <= k)
            return true;
        right++;
    }
    return mp.size() <= k;
}

// Function to return the length of the
// longest substring which has K
// unique characters
int maxLenSubStr(string s, int k)
{

    // Check if the complete string
    // contains K unique characters
    set<char> uni;
    for (auto x : s)
        uni.insert(x);
    if (uni.size() < k)
        return -1;

    // Size of the string
    int n = s.size();

    // Apply binary search
    int lo = -1, hi = n + 1;
    while (hi - lo > 1) {
        int mid = lo + hi >> 1;
        if (isValidLen(s, mid, k))
            lo = mid;
        else
            hi = mid;
    }
    return lo;
}

// Driver code
int main()
{
    string s = "aabacbebebe";
    int k = 3;

    cout << maxLenSubStr(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true if there
    // is a subString of length len
    // with <=k unique characters
    static boolean isValidLen(String s,
                              int len, int k)
    {

        // Size of the String
        int n = s.length();

        // Map to store the characters
        // and their frequency
        Map<Character,
            Integer> mp = new HashMap<Character,
                                      Integer>();
        int right = 0;

        // Update the map for the
        // first subString
        while (right < len)
        {
            if (mp.containsKey(s.charAt(right)))
            {
                mp.put(s.charAt(right),
                mp.get(s.charAt(right)) + 1);
            }
            else
            {
                mp.put(s.charAt(right), 1);
            }
            right++;
        }

        if (mp.size() <= k)
            return true;

        // Check for the rest of the subStrings
        while (right < n)
        {

            // Add the new character
            if (mp.containsKey(s.charAt(right)))
            {
                mp.put(s.charAt(right),
                mp.get(s.charAt(right)) + 1);
            }
            else
            {
                mp.put(s.charAt(right), 1);
            }

            // Remove the first character
            // of the previous window
            if (mp.containsKey(s.charAt(right - len)))
            {
                mp.put(s.charAt(right - len),
                mp.get(s.charAt(right - len)) - 1);
            }

            // Update the map
            if (mp.get(s.charAt(right - len)) == 0)
                mp.remove(s.charAt(right - len));
            if (mp.size() <= k)
                return true;
            right++;
        }
        return mp.size() <= k;
    }

    // Function to return the length of the
    // longest subString which has K
    // unique characters
    static int maxLenSubStr(String s, int k)
    {

        // Check if the complete String
        // contains K unique characters
        Set<Character> uni = new HashSet<Character>();
        for (Character x : s.toCharArray())
            uni.add(x);
        if (uni.size() < k)
            return -1;

        // Size of the String
        int n = s.length();

        // Apply binary search
        int lo = -1, hi = n + 1;
        while (hi - lo > 1)
        {
            int mid = lo + hi >> 1;
            if (isValidLen(s, mid, k))
                lo = mid;
            else
                hi = mid;
        }
        return lo;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "aabacbebebe";
        int k = 3;

        System.out.print(maxLenSubStr(s, k));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns True if there
# is a sub of length len
# with <=k unique characters
def isValidLen(s, lenn, k):

    # Size of the
    n = len(s)

    # Map to store the characters
    # and their frequency
    mp = dict()
    right = 0

    # Update the map for the
    # first sub
    while (right < lenn):
        mp[s[right]] = mp.get(s[right], 0) + 1
        right += 1

    if (len(mp) <= k):
        return True

    # Check for the rest of the subs
    while (right < n):

        # Add the new character
        mp[s[right]] = mp.get(s[right], 0) + 1

        # Remove the first character
        # of the previous window
        mp[s[right - lenn]] -= 1

        # Update the map
        if (mp[s[right - lenn]] == 0):
            del mp[s[right - lenn]]
        if (len(mp) <= k):
            return True
        right += 1

    return len(mp)<= k

# Function to return the length of the
# longest sub which has K
# unique characters
def maxLenSubStr(s, k):

    # Check if the complete
    # contains K unique characters
    uni = dict()
    for x in s:
        uni[x] = 1
    if (len(uni) < k):
        return -1

    # Size of the
    n = len(s)

    # Apply binary search
    lo = -1
    hi = n + 1
    while (hi - lo > 1):
        mid = lo + hi >> 1
        if (isValidLen(s, mid, k)):
            lo = mid
        else:
            hi = mid

    return lo

# Driver code
s = "aabacbebebe"
k = 3

print(maxLenSubStr(s, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function that returns true if there
    // is a subString of length len
    // with <=k unique characters
    static bool isValidLen(String s,
                           int len, int k)
    {

        // Size of the String
        int n = s.Length;

        // Map to store the characters
        // and their frequency
        Dictionary<char,
                   int> mp = new Dictionary<char,
                                            int>();
        int right = 0;

        // Update the map for the
        // first subString
        while (right < len)
        {
            if (mp.ContainsKey(s[right]))
            {
                mp[s[right]] = mp[s[right]] + 1;
            }
            else
            {
                mp.Add(s[right], 1);
            }
            right++;
        }

        if (mp.Count <= k)
            return true;

        // Check for the rest of the subStrings
        while (right < n)
        {

            // Add the new character
            if (mp.ContainsKey(s[right]))
            {
                mp[s[right]] = mp[s[right]] + 1;
            }
            else
            {
                mp.Add(s[right], 1);
            }

            // Remove the first character
            // of the previous window
            if (mp.ContainsKey(s[right - len]))
            {
                mp[s[right - len]] = mp[s[right - len]] - 1;
            }

            // Update the map
            if (mp[s[right - len]] == 0)
                mp.Remove(s[right - len]);
            if (mp.Count <= k)
                return true;
            right++;
        }
        return mp.Count <= k;
    }

    // Function to return the length of the
    // longest subString which has K
    // unique characters
    static int maxLenSubStr(String s, int k)
    {

        // Check if the complete String
        // contains K unique characters
        HashSet<char> uni = new HashSet<char>();
        foreach (char x in s.ToCharArray())
            uni.Add(x);
        if (uni.Count < k)
            return -1;

        // Size of the String
        int n = s.Length;

        // Apply binary search
        int lo = -1, hi = n + 1;
        while (hi - lo > 1)
        {
            int mid = lo + hi >> 1;
            if (isValidLen(s, mid, k))
                lo = mid;
            else
                hi = mid;
        }
        return lo;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "aabacbebebe";
        int k = 3;

        Console.Write(maxLenSubStr(s, k));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if there
// is a substring of length len
// with <=k unique characters
function isValidLen(s, len, k)
{

    // Size of the string
    var n = s.length;

    // Map to store the characters
    // and their frequency
    var mp = new Map();
    var right = 0;

    // Update the map for the
    // first substring
    while (right < len) {
        if(mp.has(s[right]))
            mp.set(s[right],mp.get(s[right])+1)
        else
            mp.set(s[right], 1)
        right++;
    }

    if (mp.size <= k)
        return true;

    // Check for the rest of the substrings
    while (right < n) {

        // Add the new character
        if(mp.has(s[right]))
            mp.set(s[right],mp.get(s[right])+1)
        else
            mp.set(s[right], 1)

        // Remove the first character
        // of the previous window
        if(mp.has(s[right - len]))
            mp.set(s[right - len], mp.get(s[right - len])-1)

        // Update the map
        if(mp.has(s[right - len]) && mp.get(s[right - len])==0)
            mp.delete(s[right - len]);
        if (mp.size <= k)
            return true;
        right++;
    }
    return mp.size <= k;
}

// Function to return the length of the
// longest substring which has K
// unique characters
function maxLenSubStr(s, k)
{

    // Check if the complete string
    // contains K unique characters
    var uni = new Set();
    s.split('').forEach(x => {
        uni.add(x);
    });

    if (uni.size < k)
        return -1;

    // Size of the string
    var n = s.length;

    // Apply binary search
    var lo = -1, hi = n + 1;
    while (hi - lo > 1) {
        var mid = lo + hi >> 1;
        if (isValidLen(s, mid, k))
            lo = mid;
        else
            hi = mid;
    }
    return lo;
}

// Driver code
var s = "aabacbebebe";
var k = 3;
document.write( maxLenSubStr(s, k));

</script>
```

**Output:** 

```
7
```