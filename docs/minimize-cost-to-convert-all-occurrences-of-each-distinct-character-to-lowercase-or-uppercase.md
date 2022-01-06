# 最小化将每个不同字符的所有出现转换为小写或大写的成本

> 原文:[https://www . geesforgeks . org/最小化将每个不同字符的所有出现转换为小写或大写的成本/](https://www.geeksforgeeks.org/minimize-cost-to-convert-all-occurrences-of-each-distinct-character-to-lowercase-or-uppercase/)

给定一个由 **N** 个字母和两个正整数 **L** 和 **U** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，分别代表[将任意字符转换为小写和大写](https://www.geeksforgeeks.org/convert-alternate-characters-string-upper-case/)的成本，任务是修改字符串 **S** ，使得字符串 **S** 中字母的每次出现要么是小写要么是大写，并且将原始字符串转换为修改后的字符串的成本必须最小。

**示例:**

> **输入:**S =“AAbbAA”，L = 1，U = 1
> **输出:** AAbbAA
> **说明:**
> 将“aabbAA”转换为“aabbAA”的成本为 1*2 = 2，在所有可能的转换组合中是最小的。
> 
> **输入:**S =“aApbBp”，L = 1，U = 2
> T3】输出: aapbbp

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，思路是检查将一个字符的所有出现转换为小写的[的成本是否小于大写的成本，然后将其所有出现转换为小写。否则，将其所有匹配项转换为大写。按照以下步骤解决问题:](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-in-a-string/)

*   将所有小写和大写字符的[频率分别存储在数组](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) **【下限请求【26】**和**上限请求【26】**中。
*   初始化另一个数组，说**结果【26】**为 **0** ，其中**结果【I】= 1**表示 **i <sup>th</sup>** 字符需要小写，否则需要大写。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**，并执行以下步骤:
    *   在变量**中存储将字符 **i** 的每次出现分别转换为小写和大写的成本【低成本】**和**客户**。
    *   通过乘以将 **1** 字符转换为小写，即 **L** 及其大写频率，即**upper req[I]**的成本，找到**cost low**的值。同样，通过将 **U** 乘以**lower req【I】**求出**客户**的值。
    *   如果**的值降低<客户**，那么将**结果【I】**的值更新为 **1** 。
*   使用变量 **i** 遍历字符串 **S** ，并执行以下步骤:
    *   将 **S[i]** 的索引存储在变量 **X** 中。
    *   如果**结果【I】**的值等于 **1** ，[将**S【I】**转换为小写](https://www.geeksforgeeks.org/isupper-islower-application-c/)。否则，[将 S[i]转换为大写](https://www.geeksforgeeks.org/conversion-whole-string-uppercase-lowercase-using-stl-c/)。
*   完成上述步骤后，将字符串 **S** 打印为修改后的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to convert all distinct characters
// to either uppercase or lowercase
void minimumCost(string s, int L, int U)
{
    // Store the size of the string
    int N = s.size();

    string ans = "";

    // Stores the frequency of lowercase
    // & uppercase characters respectively
    int lowerFreq[26] = { 0 };
    int upperFreq[26] = { 0 };

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Update uppercase
        // frequency of s[i]
        if (isupper(s[i]))
            upperFreq[s[i] - 'A']++;

        // Otherwise, update lowercase
        // frequency of s[i]
        else
            lowerFreq[s[i] - 'a']++;
    }

    // Stores if the i-th character
    //should be lowercase or not
    int result[26] = { 0 };

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++) {

        // If the character is present
        // in the string
        if (lowerFreq[i] != 0
            || upperFreq[i] != 0) {

            // Store the cost to convert
            // every occurence of i to
            // uppercase and lowercase
            int costToUpper = U * lowerFreq[i];
            int costToLower = L * upperFreq[i];

            // Update result[i] to 1 if
            // lowercase cost is less
            if (costToLower < costToUpper) {
                result[i] = 1;
            }
        }
    }

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Store the index
        // of the character
        int index = 0;

        if (islower(s[i]))
            index = s[i] - 'a';
        else
            index = s[i] - 'A';

        // Convert the current character
        // to uppercase or lowercase
        // according to the condition
        if (result[index] == 1) {

            // Update s[i]
            s[i] = tolower(s[i]);
        }
        else {

            // Update s[i]
            s[i] = toupper(s[i]);
        }
    }

    // Print the modified string
    cout << s;
}

// Driver Code
int main()
{
    string S = "aabbAA";
    int L = 1, U = 1;
    minimumCost(S, L, U);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the minimum cost
// to convert all distinct characters
// to either uppercase or lowercase
static void minimumCost(String str, int L, int U)
{

    // Store the size of the string
    int N = str.length();
    char s[] = str.toCharArray();

    String ans = "";

    // Stores the frequency of lowercase
    // & uppercase characters respectively
    int lowerFreq[] = new int[26];
    int upperFreq[] = new int[26];

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Update uppercase
        // frequency of s[i]
        if (Character.isUpperCase(s[i]))
            upperFreq[s[i] - 'A']++;

        // Otherwise, update lowercase
        // frequency of s[i]
        else
            lowerFreq[s[i] - 'a']++;
    }

    // Stores if the i-th character
    // should be lowercase or not
    int result[] = new int[26];

    // Iterate over the range [0, 25]
    for(int i = 0; i < 26; i++)
    {

        // If the character is present
        // in the string
        if (lowerFreq[i] != 0 || upperFreq[i] != 0)
        {

            // Store the cost to convert
            // every occurence of i to
            // uppercase and lowercase
            int costToUpper = U * lowerFreq[i];
            int costToLower = L * upperFreq[i];

            // Update result[i] to 1 if
            // lowercase cost is less
            if (costToLower < costToUpper)
            {
                result[i] = 1;
            }
        }
    }

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Store the index
        // of the character
        int index = 0;

        if (Character.isLowerCase(s[i]))
            index = s[i] - 'a';
        else
            index = s[i] - 'A';

        // Convert the current character
        // to uppercase or lowercase
        // according to the condition
        if (result[index] == 1)
        {

            // Update s[i]
            s[i] = Character.toLowerCase(s[i]);
        }
        else
        {

            // Update s[i]
            s[i] = Character.toUpperCase(s[i]);
        }
    }

    // Print the modified string
    System.out.println(new String(s));
}

// Driver Code
public static void main(String[] args)
{
    String S = "aabbAA";
    int L = 1, U = 1;
    minimumCost(S, L, U);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find the minimum cost
# to convert all distinct characters
# to either uppercase or lowercase
def minimumCost(s, L, U):

    ans = []

    # Stores the frequency of lowercase
    # & uppercase characters respectively
    lowerFreq = [0] * 26
    upperFreq = [0] * 26

    # Traverse the string S
    for c in s:
        if c.isupper():

        # Update uppercase
        # frequency of s[i]
            upperFreq[ord(c) - ord('A')] += 1

        # Otherwise, update lowercase
        # frequency of s[i]
        else:
            lowerFreq[ord(c) - ord('a')] += 1

    # stores if the i-th character
    # should be lowercase or not
    result = [0] * 26

    # Iterate over the range [0, 25]
    for i in range(26):

        # If the character is present
        # in the string
        if lowerFreq[i] != 0 or upperFreq[i] != 0:

            # Store the cost to convert
            # every occurence of i to
            # uppercase and lowercase
            costToUpper = U * lowerFreq[i];
            costToLower = L * upperFreq[i];

            # Update result[i] to 1 if
            # lowercase cost is less
            if costToLower < costToUpper:
                result[i] = 1

    # Traverse the string S
    for i in range(len(s)):

        # Store the index
        # of the character
        index = 0

        if s[i].islower():
            index = ord(s[i]) - ord('a')
        else:
            index = ord(s[i]) - ord('A')

        # Convert the current character
        # to uppercase or lowercase
        # according to the condition
        if result[index] == 1:

            # Update the character at the
            # ith index of s
            ans.append(s[i].lower())
        else:

            # Update the character at the
            # ith index of s
            ans.append(s[i].upper())

    s = ''.join(ans)

    # Print the modified string
    print(s)

# Driver code
S = "aabbAA"
L = 1
U = 1

minimumCost(S, L, U)

# This code is contributed by Md Zaid Alam
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the minimum cost
    // to convert all distinct characters
    // to either uppercase or lowercase
    static void minimumCost(string str, int L, int U)
    {

        // Store the size of the string
        int N = str.Length;
        char[] s = str.ToCharArray();

        // string ans = "";

        // Stores the frequency of lowercase
        // & uppercase characters respectively
        int[] lowerFreq = new int[26];
        int[] upperFreq = new int[26];

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // Update uppercase
            // frequency of s[i]
            if (char.IsUpper(s[i]))
                upperFreq[s[i] - 'A']++;

            // Otherwise, update lowercase
            // frequency of s[i]
            else
                lowerFreq[s[i] - 'a']++;
        }

        // Stores if the i-th character
        // should be lowercase or not
        int[] result = new int[26];

        // Iterate over the range [0, 25]
        for (int i = 0; i < 26; i++) {

            // If the character is present
            // in the string
            if (lowerFreq[i] != 0 || upperFreq[i] != 0) {

                // Store the cost to convert
                // every occurence of i to
                // uppercase and lowercase
                int costToUpper = U * lowerFreq[i];
                int costToLower = L * upperFreq[i];

                // Update result[i] to 1 if
                // lowercase cost is less
                if (costToLower < costToUpper) {
                    result[i] = 1;
                }
            }
        }

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // Store the index
            // of the character
            int index = 0;

            if (char.IsLower(s[i]))
                index = s[i] - 'a';
            else
                index = s[i] - 'A';

            // Convert the current character
            // to uppercase or lowercase
            // according to the condition
            if (result[index] == 1) {

                // Update s[i]
                s[i] = char.ToLower(s[i]);
            }
            else {

                // Update s[i]
                s[i] = char.ToUpper(s[i]);
            }
        }

        // Print the modified string
        Console.WriteLine(new string(s));
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string S = "aabbAA";
        int L = 1, U = 1;
        minimumCost(S, L, U);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find the minimum cost
      // to convert all distinct characters
      // to either uppercase or lowercase
      function minimumCost(str, L, U) {
        // Store the size of the string
        var N = str.length;
        var s = str.split("");

        // string ans = "";

        // Stores the frequency of lowercase
        // & uppercase characters respectively
        var lowerFreq = new Array(26).fill(0);
        var upperFreq = new Array(26).fill(0);

        // Traverse the string S
        for (var i = 0; i < N; i++) {
          // Update uppercase
          // frequency of s[i]
          if (s[i] === s[i].toUpperCase())
            upperFreq[s[i].charCodeAt(0) - "A".charCodeAt(0)]++;
          // Otherwise, update lowercase
          // frequency of s[i]
          else lowerFreq[s[i].charCodeAt(0) - "a".charCodeAt(0)]++;
        }

        // Stores if the i-th character
        // should be lowercase or not
        var result = new Array(26).fill(0);

        // Iterate over the range [0, 25]
        for (var i = 0; i < 26; i++) {
          // If the character is present
          // in the string
          if (lowerFreq[i] !== 0 || upperFreq[i] !== 0) {
            // Store the cost to convert
            // every occurence of i to
            // uppercase and lowercase
            var costToUpper = U * lowerFreq[i];
            var costToLower = L * upperFreq[i];

            // Update result[i] to 1 if
            // lowercase cost is less
            if (costToLower < costToUpper) {
              result[i] = 1;
            }
          }
        }

        // Traverse the string S
        for (var i = 0; i < N; i++) {
          // Store the index
          // of the character
          var index = 0;

          if (s[i] === s[i].toLowerCase())
            index = s[i].charCodeAt(0) - "a".charCodeAt(0);
          else index = s[i].charCodeAt(0) - "A".charCodeAt(0);

          // Convert the current character
          // to uppercase or lowercase
          // according to the condition
          if (result[index] === 1)
          {

            // Update s[i]
            s[i] = s[i].toLowerCase();
          }
          else
          {

            // Update s[i]
            s[i] = s[i].toUpperCase();
          }
        }

        // Print the modified string
        document.write(s.join(""));
      }

      // Driver Code
      var S = "aabbAA";
      var L = 1,
        U = 1;
      minimumCost(S, L, U);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
AAbbAA
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)