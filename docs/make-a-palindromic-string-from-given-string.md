# 用给定的字符串

制作回文字符串

> 原文:[https://www . geesforgeks . org/make-a-回文-string-from-given-string/](https://www.geeksforgeeks.org/make-a-palindromic-string-from-given-string/)

给定一个只包含小写英文字母的字符串 **S** ，我们有两个玩家在玩这个游戏。规则如下:

*   玩家可以**从给定的字符串 **S** 中移除任意字符**，并将其写在空字符串的任意一侧(左或右)的纸上。
*   玩家赢得游戏，如果在任何移动中他能得到一个长度为第一的[回文串](https://www.geeksforgeeks.org/string-palindrome/)>1。
*   如果无法形成回文字符串，玩家 2 将被宣布为赢家。

两人都在玩家 1 开始游戏时发挥最佳。任务是找到游戏的赢家。

**示例:**

> **输入:**S = " ABC "
> T3】输出: Player-2
> **解释:**
> 所有字符都是唯一的，因此
> 无法形成长度为> 1 的回文串
> 
> **输入:**S =【abccab】
> T3】输出:玩家-2
> **说明:**
> 最初，newString =“”为空。
> 让 Player-1 选择人物‘a’，写在纸上。
> 然后，S = "bccab "和 newString = "a "。
> 现在玩家 2 从 S 中选择字符‘a’，并将其写在 newString 的左侧。
> 因此，S =“bccb”和 newString =“aa”。
> 现在，newString =“aa”是一个长度为 2 的回文。
> 因此，玩家 2 获胜。

**方法:**想法是制定一个条件，在这个条件下，玩家-1 总是赢家。如果条件失败，那么玩家 2 将赢得游戏。

*   如果在给定的字符串中只有一个唯一的字符出现一次，而其余的字符出现超过 1 次，那么玩家 1 将成为赢家，否则玩家 2 将永远获胜。
*   如果我们有在给定字符串中出现不止一次的所有角色，那么玩家 2 总是可以在玩家 1 的第一回合中复制他的移动并获胜。
*   此外，如果字符串中不止一个字符只出现一次，那么回文字符串就永远不会形成(在最佳情况下)。因此，玩家 2 再次获胜。

下面是上述方法的实现:

## C++

```
// C++ Implementation to find
// which player can form a palindromic
// string first in a game

#include <bits/stdc++.h>

using namespace std;

// Function to find
// winner of the game
int palindromeWinner(string& S)
{
    // Array to Maintain frequency
    // of the characters in S
    int freq[26];

    // Initialise freq array with 0
    memset(freq, 0, sizeof freq);

    // Maintain count of all
    // distinct characters
    int count = 0;

    // Finding frequency of each character
    for (int i = 0; i < (int)S.length();
                                   ++i) {
        if (freq[S[i] - 'a'] == 0)
            count++;

        freq[S[i] - 'a']++;
    }

    // Count unique duplicate
    // characters
    int unique = 0;
    int duplicate = 0;

    // Loop to count the unique
    // duplicate characters
    for (int i = 0; i < 26; ++i) {
        if (freq[i] == 1)
            unique++;
        else if (freq[i] >= 2)
            duplicate++;
    }

    // Condition for Player-1
    // to be winner
    if (unique == 1 &&
     (unique + duplicate) == count)
        return 1;

    // Else Player-2 is
    // always winner
    return 2;
}

// Driven Code
int main()
{
    string S = "abcbc";

    // Function call
    cout << "Player-"
         << palindromeWinner(S)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find which
// player can form a palindromic
// string first in a game
import java.util.*;

class GFG{

// Function to find
// winner of the game
static int palindromeWinner(String S)
{

    // Array to maintain frequency
    // of the characters in S
    int freq[] = new int[26];

    // Initialise freq array with 0
    Arrays.fill(freq, 0);

    // Maintain count of all
    // distinct characters
    int count = 0;

    // Finding frequency of each character
    for(int i = 0; i < (int)S.length(); ++i)
    {
        if (freq[S.charAt(i) - 'a'] == 0)
            count++;

        freq[S.charAt(i) - 'a']++;
    }

    // Count unique duplicate
    // characters
    int unique = 0;
    int duplicate = 0;

    // Loop to count the unique
    // duplicate characters
    for(int i = 0; i < 26; ++i)
    {
        if (freq[i] == 1)
            unique++;

        else if (freq[i] >= 2)
            duplicate++;
    }

    // Condition for Player-1
    // to be winner
    if (unique == 1 &&
       (unique + duplicate) == count)
        return 1;

    // Else Player-2 is
    // always winner
    return 2;
}

// Driver Code
public static void main(String s[])
{
    String S = "abcbc";

    // Function call
    System.out.println("Player-" + palindromeWinner(S));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation to find
# which player can form a palindromic
# string first in a game

# Function to find
# winner of the game
def palindromeWinner(S):

    # Array to Maintain frequency
    # of the characters in S
    # initialise freq array with 0
    freq = [0 for i in range(0, 26)]

    # Maintain count of all
    # distinct characters
    count = 0

    # Finding frequency of each character
    for i in range(0, len(S)):
        if (freq[ord(S[i]) - 97] == 0):
            count += 1

        freq[ord(S[i]) - 97] += 1

    # Count unique duplicate
    # characters
    unique = 0
    duplicate = 0

    # Loop to count the unique
    # duplicate characters
    for i in range(0, 26):
        if (freq[i] == 1):
            unique += 1

        elif (freq[i] >= 2):
            duplicate += 1

    # Condition for Player-1
    # to be winner
    if (unique == 1 and
       (unique + duplicate) == count):
        return 1

    # Else Player-2 is
    # always winner
    return 2

# Driven Code
S = "abcbc";

# Function call
print("Player-", palindromeWinner(S))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to find which
// player can form a palindromic
// string first in a game
using System;
class GFG{

// Function to find
// winner of the game
static int palindromeWinner(string S)
{
  // Array to maintain frequency
  // of the characters in S
  int[] freq = new int[26];

  // Maintain count of all
  // distinct characters
  int count = 0;

  // Finding frequency of
  // each character
  for (int i = 0;
           i < (int)S.Length; ++i)
  {
    if (freq[S[i] - 'a'] == 0)
      count++;

    freq[S[i] - 'a']++;
  }

  // Count unique duplicate
  // characters
  int unique = 0;
  int duplicate = 0;

  // Loop to count the unique
  // duplicate characters
  for (int i = 0; i < 26; ++i)
  {
    if (freq[i] == 1)
      unique++;

    else if (freq[i] >= 2)
      duplicate++;
  }

  // Condition for Player-1
  // to be winner
  if (unique == 1 &&
     (unique + duplicate) ==
      count)
    return 1;

  // Else Player-2 is
  // always winner
  return 2;
}

// Driver Code
public static void Main(string[] s)
{
  string S = "abcbc";

  // Function call
  Console.Write("Player-" +
                 palindromeWinner(S));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript implementation to find which
// player can form a palindromic
// string first in a game

// Function to find
// winner of the game
function palindromeWinner(S)
{
    // Array to maintain frequency
    // of the characters in S
    let freq = new Array(26);

    // Initialise freq array with 0
    for(let i=0;i<26;i++)
    {
        freq[i]=0;
    }

    // Maintain count of all
    // distinct characters
    let count = 0;

    // Finding frequency of each character
    for(let i = 0; i < S.length; ++i)
    {
        if (freq[S[i].charCodeAt(0) - 'a'.charCodeAt(0)] == 0)
            count++;

        freq[S[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    // Count unique duplicate
    // characters
    let unique = 0;
    let duplicate = 0;

    // Loop to count the unique
    // duplicate characters
    for(let i = 0; i < 26; ++i)
    {
        if (freq[i] == 1)
            unique++;

        else if (freq[i] >= 2)
            duplicate++;
    }

    // Condition for Player-1
    // to be winner
    if (unique == 1 &&
       (unique + duplicate) == count)
        return 1;

    // Else Player-2 is
    // always winner
    return 2;
}

// Driver Code
let S = "abcbc";
// Function call
document.write("Player-" + palindromeWinner(S));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Player-1
```

**时间复杂度:** O(N)