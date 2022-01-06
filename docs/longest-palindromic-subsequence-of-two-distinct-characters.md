# 两个不同字符的最长回文子序列

> 原文:[https://www . geesforgeks . org/两个不同字符的最长回文子序列/](https://www.geeksforgeeks.org/longest-palindromic-subsequence-of-two-distinct-characters/)

给定一串小写字母 **S** ，任务是找出[最长回文子序列](https://www.geeksforgeeks.org/longest-palindromic-subsequence-dp-12/)的长度，该序列仅由两个不同的字符组成。
**例:**

> **输入:**S = " bbcccbb "
> T3】输出: 7
> **解释:**
> 所需形式最长的回文子序列是“bbcccbb”，长度为 7。
> **输入:** S = "aeea"
> **输出:** 4
> **解释:**
> 期望形式的最长回文子序列是“aeea”，长度为 4。

**进场:**
为了解决问题，我们需要遵循以下步骤:

*   将每个字符的[出现次数存储在一个](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/) [**前缀数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 中，也将每个字符的位置存储在另一个数组中。
*   现在，对于每对相等的字符，计算它们之间字符出现的最大次数。

以下是上述方法的实现:

## C++

```
// C++ implementation to find Longest
// Palindromic Subsequence consisting
// of two distinct characters only

#include <bits/stdc++.h>
using namespace std;

// Function that prints the length of
// maximum required subsequence
void longestPalindrome(string s)
{
    // Calculate length of string
    int n = s.length();

    vector<vector<int> > pref(
        26,
        vector<int>(n, 0));
    vector<vector<int> > pos(26);

    pref[s[0] - 'a'][0]++;
    pos[s[0] - 'a'].push_back(0);

    // Store number of occurrences of each
    // character and position of each
    // character in string
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < 26; j++)
            pref[j][i] += pref[j][i - 1];

        int index = s[i] - 'a';
        pref[index][i]++;
        pos[index].push_back(i);
    }

    int ans = 0;

    // Iterate all characters
    for (int i = 0; i < 26; i++) {

        // Calculate number of
        // occurences of the
        // current character
        int size = pos[i].size();
        ans = max(ans, size);

        // Iterate half of the
        // number of positions
        // of current character
        for (int j = 0; j < size / 2; j++) {
            int l = pos[i][j];
            int r = pos[i][size - j - 1] - 1;

            // Determine maximum length
            // of a character between
            // l and r position
            for (int k = 0; k < 26; k++) {

                int sum = pref[k][r] - pref[k][l];

                // Compute the maximum from all
                ans = max(ans, 2 * (j + 1) + sum);
            }
        }
    }

    // Printing maximum length
    cout << ans << "\n";
}

// Driver Code
int main()
{
    string S = "bbccdcbb";

    longestPalindrome(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find Longest
// Palindromic Subsequence consisting
// of two distinct characters only
import java.util.*;
class GFG{

// Function that prints the length of
// maximum required subsequence
static void longestPalindrome(String s)
{
  // Calculate length of String
  int n = s.length();

  int [][]pref = new int[26][n];

  Vector<Integer> []pos = new Vector[26];
  for (int i = 0; i < pos.length; i++)
    pos[i] = new Vector<Integer>();

  pref[s.charAt(0) - 'a'][0]++;
  pos[s.charAt(0) - 'a'].add(0);

  // Store number of occurrences of each
  // character and position of each
  // character in String
  for (int i = 1; i < n; i++)
  {
    for (int j = 0; j < 26; j++)
      pref[j][i] += pref[j][i - 1];

    int index = s.charAt(i) - 'a';
    pref[index][i]++;
    pos[index].add(i);
  }

  int ans = 0;

  // Iterate all characters
  for (int i = 0; i < 26; i++)
  {
    // Calculate number of
    // occurences of the
    // current character
    int size = pos[i].size();
    ans = Math.max(ans, size);

    // Iterate half of the
    // number of positions
    // of current character
    for (int j = 0; j < size / 2; j++)
    {
      int l = pos[i].elementAt(j);
      int r = pos[i].elementAt(size - j - 1) - 1;

      // Determine maximum length
      // of a character between
      // l and r position
      for (int k = 0; k < 26; k++)
      {
        int sum = pref[k][r] - pref[k][l];

        // Compute the maximum from all
        ans = Math.max(ans, 2 *
                      (j + 1) + sum);
      }
    }
  }

  // Printing maximum length
  System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{
  String S = "bbccdcbb";
  longestPalindrome(S);
}
}

// This code is contributed by Princi Singh
```

## C#

```
// C# implementation to find longest
// Palindromic Subsequence consisting
// of two distinct characters only
using System;
using System.Collections.Generic;
class GFG{

// Function that prints
// the length of maximum
// required subsequence
static void longestPalindrome(String s)
{
  // Calculate length of String
  int n = s.Length;

  int [,]pref = new int[26, n];
  List<int> []pos = new List<int>[26];

  for (int i = 0; i < pos.Length; i++)
    pos[i] = new List<int>();

  pref[s[0] - 'a', 0]++;
  pos[s[0] - 'a'].Add(0);

  // Store number of occurrences of each
  // character and position of each
  // character in String
  for (int i = 1; i < n; i++)
  {
    for (int j = 0; j < 26; j++)
      pref[j, i] += pref[j, i - 1];

    int index = s[i] - 'a';
    pref[index, i]++;
    pos[index].Add(i);
  }

  int ans = 0;

  // Iterate all characters
  for (int i = 0; i < 26; i++)
  {
    // Calculate number of
    // occurences of the
    // current character
    int size = pos[i].Count;
    ans = Math.Max(ans, size);

    // Iterate half of the
    // number of positions
    // of current character
    for (int j = 0; j < size / 2; j++)
    {
      int l = pos[i][j];
      int r = pos[i][size -
                     j - 1] - 1;

      // Determine maximum length
      // of a character between
      // l and r position
      for (int k = 0; k < 26; k++)
      {
        int sum = pref[k, r] -
                  pref[k, l];

        // Compute the maximum from all
        ans = Math.Max(ans, 2 *
                      (j + 1) + sum);
      }
    }
  }

  // Printing maximum length
  Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  String S = "bbccdcbb";
  longestPalindrome(S);
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
7
```