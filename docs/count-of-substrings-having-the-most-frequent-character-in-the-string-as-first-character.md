# 将字符串中最频繁的字符作为第一个字符的子字符串计数

> 原文:[https://www . geesforgeks . org/子字符串计数-以字符串中最频繁的字符作为第一个字符/](https://www.geeksforgeeks.org/count-of-substrings-having-the-most-frequent-character-in-the-string-as-first-character/)

给定一个由大小为 **N** 的小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是将字符串中包含[最频繁字符的所有](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)计数为第一个字符。

**注意:**如果多个字符具有最大频率，则考虑其中字典序最小的字符。

**示例:**

> **输入:** S = "abcab"
> **输出:** 7
> **说明:**
> 有两个字符 a 和 b 出现次数最多，即 2 次。
> 选择字典上较小的字符，即“a”。
> 以‘a’开头的子串有:“a”、“ab”、“abc”、“abca”、“abcab”、“a”、“ab”。
> 因此计数为 7。
> 
> **输入:**S = " cccc "
> T3】输出 : 10

**方法:**思路是先找到出现次数最多的[字符](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)，然后统计字符串中以该字符开始的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)。按照以下步骤解决问题:

*   将**计数**初始化为 **0** ，将存储字符串的总计数。
*   在字符串 S 中找到[最大出现字符。让那个角色成为 **ch** 。](https://www.geeksforgeeks.org/maximum-occurring-character-in-an-input-string-set-2/)
*   使用变量 **i** 遍历字符串，如果 **i <sup>th</sup> 索引**处的字符与 **ch** 相同，则将计数增加**(N–I)**。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find all substrings
// whose first character occurs
// maximum number of times
int substringCount(string s)
{

    // Stores frequency of characters
    vector<int> freq(26, 0);

    // Stores character that appears
    // maximum number of times
    char max_char = '#';

    // Stores max frequency of character
    int maxfreq = INT_MIN;

    // Updates frequency of characters
    for(int i = 0; i < s.size(); i++)
    {
        freq[s[i] - 'a']++;

        // Update maxfreq
        if (maxfreq < freq[s[i] - 'a'])
            maxfreq = freq[s[i] - 'a'];
    }

    // Character that occurs
    // maximum number of times
    for(int i = 0; i < 26; i++)
    {

        // Update the maximum frequency
        // character
        if (maxfreq == freq[i])
        {
            max_char = (char)(i + 'a');
            break;
        }
    }

    // Stores all count of substrings
    int ans = 0;

    // Traverse over string
    for(int i = 0; i < s.size(); i++)
    {

        // Get the current character
        char ch = s[i];

        // Update count of substrings
        if (max_char == ch)
        {
            ans += (s.size() - i);
        }
    }

    // Return the count of all
    // valid substrings
    return ans;
}

// Driver Code
int main()
{
    string S = "abcab";

    // Function Call
    cout << (substringCount(S));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find all substrings
    // whose first character occurs
    // maximum number of times
    static int substringCount(String s)
    {

        // Stores frequency of characters
        int[] freq = new int[26];

        // Stores character that appears
        // maximum number of times
        char max_char = '#';

        // Stores max frequency of character
        int maxfreq = Integer.MIN_VALUE;

        // Updates frequency of characters
        for (int i = 0;
             i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;

            // Update maxfreq
            if (maxfreq
                < freq[s.charAt(i) - 'a'])
                maxfreq
                    = freq[s.charAt(i) - 'a'];
        }

        // Character that occurs
        // maximum number of times
        for (int i = 0; i < 26; i++) {

            // Update the maximum frequency
            // character
            if (maxfreq == freq[i]) {
                max_char = (char)(i + 'a');
                break;
            }
        }

        // Stores all count of substrings
        int ans = 0;

        // Traverse over string
        for (int i = 0;
             i < s.length(); i++) {

            // Get the current character
            char ch = s.charAt(i);

            // Update count of substrings
            if (max_char == ch) {
                ans += (s.length() - i);
            }
        }

        // Return the count of all
        // valid substrings
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "abcab";

        // Function Call
        System.out.println(substringCount(S));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find all substrings
# whose first character occurs
# maximum number of times
def substringCount(s):

    # Stores frequency of characters
    freq = [0 for i in range(26)]

    # Stores character that appears
    # maximum number of times
    max_char = '#'

    # Stores max frequency of character
    maxfreq = -sys.maxsize - 1

    # Updates frequency of characters
    for i in range(len(s)):
        freq[ord(s[i]) - ord('a')] += 1

        # Update maxfreq
        if (maxfreq < freq[ord(s[i]) - ord('a')]):
            maxfreq = freq[ord(s[i]) - ord('a')]

    # Character that occurs
    # maximum number of times
    for i in range(26):

        # Update the maximum frequency
        # character
        if (maxfreq == freq[i]):
            max_char = chr(i + ord('a'))
            break

    # Stores all count of substrings
    ans = 0

    # Traverse over string
    for i in range(len(s)):

        # Get the current character
        ch = s[i]

        # Update count of substrings
        if (max_char == ch):
            ans += (len(s) - i)

    # Return the count of all
    # valid substrings
    return ans

# Driver Code
if __name__ == '__main__':

    S = "abcab"

    # Function Call
    print(substringCount(S))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find all substrings
// whose first character occurs
// maximum number of times
static int substringCount(string s)
{

    // Stores frequency of characters
    int[] freq = new int[26];

    // Stores character that appears
    // maximum number of times
    char max_char = '#';

    // Stores max frequency of character
    int maxfreq = Int32.MinValue;

    // Updates frequency of characters
    for(int i = 0; i < s.Length; i++)
    {
        freq[s[i] - 'a']++;

        // Update maxfreq
        if (maxfreq < freq[s[i] - 'a'])
            maxfreq = freq[s[i] - 'a'];
    }

    // Character that occurs
    // maximum number of times
    for(int i = 0; i < 26; i++)
    {

        // Update the maximum frequency
        // character
        if (maxfreq == freq[i])
        {
            max_char = (char)(i + 'a');
            break;
        }
    }

    // Stores all count of substrings
    int ans = 0;

    // Traverse over string
    for(int i = 0; i < s.Length; i++)
    {

        // Get the current character
        char ch = s[i];

        // Update count of substrings
        if (max_char == ch)
        {
            ans += (s.Length - i);
        }
    }

    // Return the count of all
    // valid substrings
    return ans;
}

// Driver Code
public static void Main()
{
    string S = "abcab";

    // Function Call
    Console.WriteLine(substringCount(S));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find all substrings
// whose first character occurs
// maximum number of times
function substringCount(s)
{

    // Stores frequency of characters
    var freq = new Array(26).fill(0);

    // Stores character that appears
    // maximum number of times
    var max_char = "#";

    // Stores max frequency of character
    var maxfreq = -21474836487;

    // Updates frequency of characters
    for(var i = 0; i < s.length; i++)
    {
        freq[s[i].charCodeAt(0) -
              "a".charCodeAt(0)]++;

        // Update maxfreq
        if (maxfreq < freq[s[i].charCodeAt(0) -
                            "a".charCodeAt(0)])
            maxfreq = freq[s[i].charCodeAt(0) -
                            "a".charCodeAt(0)];
    }

    // Character that occurs
    // maximum number of times
    for(var i = 0; i < 26; i++)
    {

        // Update the maximum frequency
        // character
        if (maxfreq === freq[i])
        {
            max_char = String.fromCharCode(
                i + "a".charCodeAt(0));
            break;
        }
    }

    // Stores all count of substrings
    var ans = 0;

    // Traverse over string
    for(var i = 0; i < s.length; i++)
    {

        // Get the current character
        var ch = s[i];

        // Update count of substrings
        if (max_char === ch)
        {
            ans += s.length - i;
        }
    }

    // Return the count of all
    // valid substrings
    return ans;
}

// Driver Code
var S = "abcab";

// Function Call
document.write(substringCount(S));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*