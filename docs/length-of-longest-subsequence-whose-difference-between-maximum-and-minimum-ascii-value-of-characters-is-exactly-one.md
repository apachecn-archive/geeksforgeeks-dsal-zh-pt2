# 字符的最大和最小 ASCII 值之差正好为 1 的最长子序列的长度

> 原文:[https://www . geesforgeks . org/最长子序列长度-其最大和最小 ascii 字符值之差正好为 1/](https://www.geeksforgeeks.org/length-of-longest-subsequence-whose-difference-between-maximum-and-minimum-ascii-value-of-characters-is-exactly-one/)

给定一个由小写英文字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从给定的字符串中找到最长的[子序列的长度，使得最大和最小的](https://www.geeksforgeeks.org/print-subsequences-string/) [**ASCII 值**](https://www.geeksforgeeks.org/program-print-ascii-value-character/) 之间的差值正好是 **1** 。

**示例:**

> **输入:**S = " acbbebbcg "
> T3】输出: 5
> **说明:**所需类型最长的子序列为“cbbbc”，长度为 5。
> 最大( **'c'** )和最小( **'b'** ) ASCII 值之间的差值为 c–b = 99–98 = 1，这是最小可能值。
> 
> **输入:**S = " ABCD "
> T3】输出: 2
> **说明:**所需类型最长的子序列为“ab”，长度为 2。其他可能的子序列是“bc”和“cd”。
> 最大(' b ')和最小(' a') ASCII 值之间的差异是 b–a = 98–97 = 1。

**天真方法:**解决问题最简单的方法是[生成给定字符串的所有可能的子序列 **S**](https://www.geeksforgeeks.org/print-subsequences-string/) 并打印[子序列](https://www.geeksforgeeks.org/tag/subsequence/)的长度，该长度是最大长度，并且最大和最小字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)之间的差异正好等于 **1** 。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**对上述途径进行优化，主要思路是使用一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)对上述途径进行优化。按照以下步骤解决问题:

*   初始化一个变量，比如说**最大长度**，它存储最终[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大长度。
*   将字符的[频率存储在](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，比如 **M** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，对于每个字符，说出 **ch** ，检查地图 **M** 中是否存在 ASCII 值为**(ch–1)**的字符 **c** 。如果发现为真，则更新**最大长度**为**最大长度**和**(M[ch]+M[ch–1])**的最大值。
*   完成上述步骤后，打印**最大长度**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length of
// subsequence having difference of ASCII
// value of longest and smallest character as 1
int maximumLengthSubsequence(string str)
{
    // Stores frequency of characters
    unordered_map<char, int> mp;

    // Iterate over characters
    // of the string
    for (char ch : str) {
        mp[ch]++;
    }
    // Stores the resultant
    // length of subsequence
    int ans = 0;

    for (char ch : str) {
        // Check if there exists any
        // elements with ASCII value
        // one less than character ch
        if (mp.count(ch - 1)) {
            // Size of current subsequence

            int curr_max = mp[ch] + mp[ch - 1];
            // Update the value of ans
            ans = max(ans, curr_max);
        }
    }

    // Print the resultant count
    cout << ans;
}

// Driver Code
int main()
{
    string S = "acbbebcg";
    maximumLengthSubsequence(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum length of
// subsequence having difference of ASCII
// value of longest and smallest character as 1
static void maximumLengthSubsequence(String str)
{

    // Stores frequency of characters
    HashMap<Character, Integer> mp = new HashMap<>();
    for(char ch : str.toCharArray())
    {
        mp.put(ch, mp.getOrDefault(ch, 0) + 1);
    }

    // Stores the resultant
    // length of subsequence
    int ans = 0;

    for(char ch : str.toCharArray())
    {

        // Check if there exists any
        // elements with ASCII value
        // one less than character ch
        if (mp.containsKey((char)(ch - 1)))
        {

            // Size of current subsequence
            int curr_max = mp.get(ch) +
                    mp.get((char)(ch - 1));

            // Update the value of ans
            ans = Math.max(ans, curr_max);
        }
    }

    // Print the resultant count
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    String S = "acbbebcg";

    maximumLengthSubsequence(S);
}
}

// This code is contributed by aadityapburujwale
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum length of
# subsequence having difference of ASCII
# value of longest and smallest character as 1
def maximumLengthSubsequence(str):

    # Stores frequency of characters
    mp = {}

    # Iterate over characters
    # of the string
    for ch in str:
        if ch in mp.keys():
            mp[ch] += 1
        else:
            mp[ch] = 1

    # Stores the resultant
    # length of subsequence
    ans = 0

    for ch in str:

        # Check if there exists any
        # elements with ASCII value
        # one less than character ch
        if chr(ord(ch) - 1) in mp.keys():

            # Size of current subsequence
            curr_max = mp[ch]

            if chr(ord(ch) - 1) in mp.keys():
                 curr_max += mp[chr(ord(ch) - 1)]

            # Update the value of ans
            ans = max(ans, curr_max)

    # Print the resultant count
    print(ans)

# Driver Code
S = "acbbebcg"

maximumLengthSubsequence(S)

# This code is contributed by Stream_Cipher
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find the maximum length of
// subsequence having difference of ASCII
// value of longest and smallest character as 1
static void maximumLengthSubsequence(String str)
{

    // Stores frequency of characters
    Dictionary<char, int> mp = new Dictionary<char, int>();
    foreach(char ch in str.ToCharArray())
    {
        if(mp.ContainsKey(ch))
            mp[ch] = mp[ch] + 1;
        else
            mp.Add(ch, 1);
    }

    // Stores the resultant
    // length of subsequence
    int ans = 0;
    foreach(char ch in str.ToCharArray())
    {

        // Check if there exists any
        // elements with ASCII value
        // one less than character ch
        if (mp.ContainsKey((char)(ch - 1)))
        {

            // Size of current subsequence
            int curr_max = mp[ch] +
                    mp[(char)(ch - 1)];

            // Update the value of ans
            ans = Math.Max(ans, curr_max);
        }
    }

    // Print the resultant count
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "acbbebcg";  
    maximumLengthSubsequence(S);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find the maximum length of
      // subsequence having difference of ASCII
      // value of longest and smallest character as 1
      function maximumLengthSubsequence(str) {
        // Stores frequency of characters
        var mp = {};

        var temp = str.split("");
        for (const ch of temp) {
          if (mp.hasOwnProperty(ch)) mp[ch] = mp[ch] + 1;
          else mp[ch] = 1;
        }

        // Stores the resultant
        // length of subsequence
        var ans = 0;
        for (const ch of temp) {
          // Check if there exists any
          // elements with ASCII value
          // one less than character ch
          if (mp.hasOwnProperty(String.fromCharCode(ch.charCodeAt(0) - 1))) {
            // Size of current subsequence
            var curr_max =
              mp[ch] + mp[String.fromCharCode(ch.charCodeAt(0) - 1)];

            // Update the value of ans
            ans = Math.max(ans, curr_max);
          }
        }

        // Print the resultant count
        document.write(ans);
      }

      // Driver Code
      var S = "acbbebcg";
      maximumLengthSubsequence(S);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*