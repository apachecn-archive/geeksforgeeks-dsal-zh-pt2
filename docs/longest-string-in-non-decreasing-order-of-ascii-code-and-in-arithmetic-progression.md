# ASCII 码非递减顺序和算术级数中最长的字符串

> 原文:[https://www . geesforgeks . org/ascii 码非递减顺序中的最长字符串和算术级数/](https://www.geeksforgeeks.org/longest-string-in-non-decreasing-order-of-ascii-code-and-in-arithmetic-progression/)

给定一个长度为 L 的大写字母组成的非空字符串 S，任务是从给定的字符串中找到最长的字符串，该字符串中的字符按照 ASCII 码的降序排列，并以算术级数排列，这样公共差应该尽可能小，字符串中的字符应该具有更高的 ASCII 值。
**注意**:字符串至少包含三个不同的字符。

**示例**:

> **输入**:S =“ABCPQR”
> **输出**:“RQP”
> 两个最大长度的字符串都是可能的——“CBA”和“RPQ”。但是由于
> 字符串应该具有更高的 ASCII 值，因此输出是“RPQ”。
> 
> **输入**:S =“ADGJPRT”
> T3】输出:JGDA

**接近**:算术级数中最少 3 个字符的最大可能公差带为 12。因此，使用 hashmap 预先计算字符串中存在的所有字符，然后从具有最大 ASCII 值的字符(即“Z”)迭代到具有最小 ASCII 值的字符(即“A”)。如果给定字符串中存在当前字符，将其视为算术级数序列的起始字符，并再次迭代所有可能的公共差异，即从 1 到 12。检查每个当前常见的差异，如果字符存在于给定的字符串中，则增加所需最长字符串的当前长度。现在存在最大长度*和最小公差*需要更新的两种情况。

1.  当当前长度大于最大长度时。
2.  当当前长度等于最大长度且当前公共差小于最小公共差时，则需要更新公共差。

此外，在这两个参数每次更新时，字符串或算术级数序列的起始字符也必须更新。

以下是上述方法的实现:

## C++

```
// C++ Program to find the longest string
// with characters arranged in non-decreasing
// order of ASCII and in arithmetic progression
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest String
string findLongestString(string S)
{
    // Stores the maximum length of required string
    int maxLen = 0;

    // Stores the optimal starting character of
    // required string or arithmetic progression sequence
    int bestStartChar;

    // Stores the optimal i.e. minimum common difference
    // of required string
    int minCommonDifference = INT_MAX;

    unordered_map<char, bool> mp;
    for (int i = 0; i < S.size(); i++)
        mp[S[i]] = true;

    // Iterate over the loop in non decreasing order
    for (int startChar = 'Z'; startChar > 'A'; startChar--) {

        // Process further only if current character
        // exists in the given string
        if (mp[startChar]) {

            // Iterate over all possible common differences
            // of AP sequence and update maxLen accordingly
            for (int currDiff = 1; currDiff <= 12; currDiff++) {
                int currLen = 1;

                // Iterate over the characters at any interval
                // of current common difference
                for (int ch = startChar - currDiff; ch >= 'A';
                     ch -= currDiff) {
                    if (mp[ch])
                        currLen++;
                    else
                        break;
                }

                // Update maxLen and other parameters if the currLen
                // is greater than maxLen or if the current
                // difference is smaller than minCommonDifference
                if (currLen > maxLen || (currLen == maxLen
                                         && currDiff < minCommonDifference)) {
                    minCommonDifference = currDiff;
                    maxLen = currLen;
                    bestStartChar = startChar;
                }
            }
        }
    }
    string longestString = "";

    // Store the string in decreasing order of
    // arithmetic progression
    for (int i = bestStartChar;
         i >= (bestStartChar - (maxLen - 1) * minCommonDifference);
         i -= minCommonDifference)
        longestString += char(i);

    return longestString;
}

// Driver Code
int main()
{
    string S = "ADGJPRT";
    cout << findLongestString(S) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the longest string
// with characters arranged in non-decreasing
// order of ASCII and in arithmetic progression
import java.util.*;
import java.lang.*;

public class GFG {
    // Function to find the longest String
    static String findLongestString(String S)
    {
        // Stores the maximum length of required string
        int maxLen = 0;

        // Stores the optimal starting character of
        // required string or arithmetic progression sequence
        int bestStartChar = 0;

        // Stores the optimal i.e. minimum common difference
        // of required string
        int minCommonDifference = Integer.MAX_VALUE;

        HashMap <Character, Boolean> hm = new HashMap
                                <Character, Boolean>();
        for (int i = 0; i < S.length(); i++)
            hm.put(S.charAt(i), true);

        // Iterate over the loop in non decreasing order
        for (int startChar = 'Z'; startChar > 'A'; startChar--) {

            // Process further only if current character
            // exists in the given string
            if (hm.containsKey((char)startChar)) {

                // Iterate over all possible common differences
                // of AP sequence and update maxLen accordingly
                for (int currDiff = 1; currDiff <= 12; currDiff++) {
                    int currLen = 1;

                    // Iterate over the characters at any interval
                    // of current common difference
                    for (int ch = startChar - currDiff; ch >= 'A';
                        ch -= currDiff) {
                        if (hm.containsKey((char)ch))
                            currLen++;
                        else
                            break;
                    }

                    // Update maxLen and other parameters if the currLen
                    // is greater than maxLen or if the current
                    // difference is smaller than minCommonDifference
                    if (currLen > maxLen || (currLen == maxLen
                                 && currDiff < minCommonDifference)) {
                        minCommonDifference = currDiff;
                        maxLen = currLen;
                        bestStartChar = startChar;
                    }
                }
            }
        }
        String longestString = "";

        // Store the string in decreasing order of
        // arithmetic progression
        char ch;
        for (int i = bestStartChar; 
         i >= (bestStartChar - (maxLen - 1) * minCommonDifference); 
         i -= minCommonDifference)
        {
            ch = (char)i;
            longestString += ch;
        }
        return longestString;
    }

    // Driver Code
    public static void main(String args[])
    {
        String S = "ADGJPRT";
        System.out.println(findLongestString(S));
    }
}
// This code is contributed by Nishant Tanwar
```

## C#

```
// C# Program to find the longest string 
// with characters arranged in non-decreasing 
// order of ASCII and in arithmetic progression

using System;
using System.Collections ;

public class GFG { 
    // Function to find the longest String 
    static String findLongestString(String S) 
    { 
        // Stores the maximum length of required string 
        int maxLen = 0; 

        // Stores the optimal starting character of 
        // required string or arithmetic progression sequence 
        int bestStartChar = 0; 

        // Stores the optimal i.e. minimum common difference 
        // of required string 
        int minCommonDifference = Int32.MaxValue ; 

        Hashtable hm = new Hashtable (); 
        for (int i = 0; i < S.Length; i++) 
            hm.Add(S[i], true); 

        // Iterate over the loop in non decreasing order 
        for (int startChar = 'Z'; startChar > 'A'; startChar--) { 

            // Process further only if current character 
            // exists in the given string 
            if (hm.ContainsKey((char)startChar)) { 

                // Iterate over all possible common differences 
                // of AP sequence and update maxLen accordingly 
                for (int currDiff = 1; currDiff <= 12; currDiff++) { 
                    int currLen = 1; 

                    // Iterate over the characters at any interval 
                    // of current common difference 
                    for (int ch = startChar - currDiff; ch >= 'A'; 
                        ch -= currDiff) { 
                        if (hm.ContainsKey((char)ch)) 
                            currLen++; 
                        else
                            break; 
                    } 

                    // Update maxLen and other parameters if the currLen 
                    // is greater than maxLen or if the current 
                    // difference is smaller than minCommonDifference 
                    if (currLen > maxLen || (currLen == maxLen 
                                && currDiff < minCommonDifference)) { 
                        minCommonDifference = currDiff; 
                        maxLen = currLen; 
                        bestStartChar = startChar; 
                    } 
                } 
            } 
        } 
        String longestString = ""; 

        // Store the string in decreasing order of 
        // arithmetic progression 
        char ch1; 
        for (int i = bestStartChar; 
        i >= (bestStartChar - (maxLen - 1) * minCommonDifference); 
        i -= minCommonDifference) 
        { 
            ch1 = (char)i; 
            longestString += ch1; 
        } 
        return longestString; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        String S = "ADGJPRT"; 
        Console.WriteLine(findLongestString(S)); 
    }
    // This code is contributed by Ryuga 
} 
```

**Output:**

```
JGDA

```

**时间复杂度** : O(|S| + 26*12*26)，其中|S|是字符串的大小。