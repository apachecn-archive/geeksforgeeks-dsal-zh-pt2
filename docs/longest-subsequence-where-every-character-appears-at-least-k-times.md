# 每个字符出现至少 k 次的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列-每个字符出现的位置-至少-k 次/](https://www.geeksforgeeks.org/longest-subsequence-where-every-character-appears-at-least-k-times/)

给定一个字符串和一个数字 k，找到字符串中最长的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其中每个字符至少出现 k 次。

示例:

```
Input : str = "geeksforgeeks"
         k = 2
Output : geeksgeeks
Every character in the output
subsequence appears at-least 2
times.

Input : str = "aabbaabacabb"
          k = 5
Output : aabbaabaabb
```

**方法 1(蛮力)**
我们[生成所有子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。对于每个子序列，计算其中不同的字符，并找到每个字符出现至少 k 次的最长子序列。

**方法 2(高效方式)**
1。找到字符串的频率，并将其存储在代表字母的 26 位整数数组中。
2。找到频率后，逐个字符地重复字符串，如果该字符的频率大于或等于所需的重复次数，则只打印该字符。

## 蟒蛇 3

```
// C++ program to Find longest subsequence where
//  every character appears at-least k times
#include<bits/stdc++.h>
using namespace std;

const int MAX_CHARS = 26;

void longestSubseqWithK(string str, int k)   
{
    int n = str.size();                  

    // Count frequencies of all characters
    int freq[MAX_CHARS] = {0};                   
    for (int i = 0 ; i < n; i++)   
        freq[str[i] - 'a']++;             

    // Traverse given string again and print
    // all those characters whose frequency
    // is more than or equal to k.
    for (int i = 0 ; i < n ; i++)  
        if (freq[str[i] - 'a'] >= k)              
            cout << str[i];     
}

// Driver code
int main() {
    string str = "geeksforgeeks";
    int k = 2;
    longestSubseqWithK(str, k);      
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find longest subsequence where
//  every character appears at-least k times

class GFG {

    static final int MAX_CHARS = 26;

    static void longestSubseqWithK(String str, int k) {
        int n = str.length();

        // Count frequencies of all characters
        int freq[] = new int[MAX_CHARS];
        for (int i = 0; i < n; i++) {
            freq[str.charAt(i) - 'a']++;
        }

        // Traverse given string again and print
        // all those characters whose frequency
        // is more than or equal to k.
        for (int i = 0; i < n; i++) {
            if (freq[str.charAt(i) - 'a'] >= k) {
                System.out.print(str.charAt(i));
            }
        }
    }

// Driver code
    static public void main(String[] args) {
        String str = "geeksforgeeks";
        int k = 2;
        longestSubseqWithK(str, k);

    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to Find longest subsequence where
#  every character appears at-least k times

MAX_CHARS = 26

def longestSubseqWithK(s, k):   

    n = len(s)                 

    # Count frequencies of all characters
    freq = [0]*MAX_CHARS                
    for i in range(n): 
        freq[ord(s[i]) - ord('a')]+=1             

    # Traverse given string again and print
    # all those characters whose frequency
    # is more than or equal to k.
    for i in range(n ):
        if (freq[ord(s[i]) - ord('a')] >= k):              
            print(s[i],end="")

# Driver code
if __name__ == "__main__":

    s = "geeksforgeeks"
    k = 2
    longestSubseqWithK(s, k)
```

## C#

```

// C# program to Find longest subsequence where
//  every character appears at-least k times
using System;
public class GFG {

    static readonly int MAX_CHARS = 26;

    static void longestSubseqWithK(String str, int k) {
        int n = str.Length;

        // Count frequencies of all characters
        int []freq = new int[MAX_CHARS];
        for (int i = 0; i < n; i++) {
            freq[str[i]- 'a']++;
        }

        // Traverse given string again and print
        // all those characters whose frequency
        // is more than or equal to k.
        for (int i = 0; i < n; i++) {
            if (freq[str[i] - 'a'] >= k) {
                Console.Write(str[i]);
            }
        }
    }

// Driver code
    static public void Main() {
        String str = "geeksforgeeks";
        int k = 2;
        longestSubseqWithK(str, k);

    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find longest subsequence
// where every character appears at-least k times
let MAX_CHARS = 26;

function longestSubseqWithK(str, k)
{
    let n = str.length;

    // Count frequencies of all characters
    let freq = new Array(MAX_CHARS);
    for(let i = 0; i < freq.length; i++)
    {
        freq[i] = 0
    }

    for(let i = 0; i < n; i++)
    {
        freq[str[i].charCodeAt(0) -
                'a'.charCodeAt(0)]++;
    }

    // Traverse given string again and print
    // all those characters whose frequency
    // is more than or equal to k.
    for(let i = 0; i < n; i++)
    {
        if (freq[str[i].charCodeAt(0) -
                    'a'.charCodeAt(0)] >= k)
        {
            document.write(str[i]);
        }
    }
}

// Driver code
let str = "geeksforgeeks";
let k = 2;

longestSubseqWithK(str, k);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
geeksgeeks
```

这段代码的时间复杂度为 O(n)，其中 n 是字符串的大小。

方法 3(有效的方法——使用哈希映射)

## C++

```
// C++ program to Find longest subsequence where every
// character appears at-least k times
#include <bits/stdc++.h>
using namespace std;

void longestSubseqWithK(string str, int k)
{
  int n = str.size();
  map<char, int> hm;

  // Count frequencies of all characters
  for (int i = 0; i < n; i++) {
    char c = str[i];
    hm++;
  }

  // Traverse given string again and print
  // all those characters whose frequency
  // is more than or equal to k.
  for (int i = 0; i < n; i++) {
    char c = str[i];
    if (hm >= k) {
      cout << c;
    }
  }
}

// Driver code
int main()
{
  string str = "geeksforgeeks";
  int k = 2;
  longestSubseqWithK(str, k);

  return 0;
}

// This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
// Java program to Find longest subsequence where every
// character appears at-least k times

import java.io.*;
import java.util.HashMap;

class GFG {

    static void longestSubseqWithK(String str, int k)
    {
        int n = str.length();
        HashMap<Character, Integer> hm = new HashMap<>();

        // Count frequencies of all characters
        for (int i = 0; i < n; i++) {
            char c = str.charAt(i);
            if (hm.containsKey(c))
                hm.put(c, hm.get(c) + 1);
            else
                hm.put(c, 1);
        }

        // Traverse given string again and print
        // all those characters whose frequency
        // is more than or equal to k.
        for (int i = 0; i < n; i++) {
            char c = str.charAt(i);
            if (hm.get(c) >= k) {
                System.out.print(c);
            }
        }
    }

    // Driver code
    static public void main(String[] args)
    {
        String str = "geeksforgeeks";
        int k = 2;
        longestSubseqWithK(str, k);
    }
}

// This code is contributed by Chandan-Bedi
```

**Output**

```
geeksgeeks
```

**时间复杂度:O(n)，其中 n 是字符串的大小。**

本文由 **Mohak Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。