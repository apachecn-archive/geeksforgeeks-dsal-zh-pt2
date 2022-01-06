# 总字谜子串的计数

> 原文:[https://www . geesforgeks . org/count-total-anagram-substrings/](https://www.geeksforgeeks.org/count-total-anagram-substrings/)

给定一串较低字母的字符，计算该串的全部子串，这些子串相互之间是[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。

**示例:**

```
Input  : str = “xyyx”
Output : 4
Total substrings of this string which
are anagram to each other are 4 which 
can be enumerated as,
{“x”, “x”}, {"y", "y"}, {“xy”, “yx”}, 
{“xyy”, “yyx”}

Input  : str = "geeg"
Output : 4

```

这个想法是创建一个地图。我们使用字符频率作为键，相应的计数作为值。我们可以通过迭代所有子串并计算每个子串中字符的频率来解决这个问题。我们可以在循环子串时更新字符的频率，也就是说，不会有额外的循环来计算字符的频率。
在下面的代码中，键“向量类型”和值“int 类型”的映射用于存储子串字符的“长度为 26 的频率数组”的出现。一旦每个频率数组的出现“o”被存储，总字谜将是所有不同频率数组的 o*(o-1)/2 的总和，因为如果特定子串在字符串中具有“o”字谜，则可以形成总 o*(o-1)/2 字谜对。

以下是上述想法的实现。

## C++

```
// C++ program to count total anagram
// substring of a string
#include <bits/stdc++.h>
using namespace std;

// Total number of lowercase characters
#define MAX_CHAR 26

// Utility method to return integer index
// of character 'c'
int toNum(char c)
{
    return (c - 'a');
}

// Returns count of total number of anagram
// substrings of string str
int countOfAnagramSubstring(string str)
{
    int N = str.length();

    // To store counts of substrings with given
    // set of frequencies.
    map<vector<int>, int> mp;

    // loop for starting index of substring
    for (int i=0; i<N; i++)
    {
        vector<int> freq(MAX_CHAR, 0);

        // loop for length of substring
        for (int j=i; j<N; j++)
        {
            // update freq array of current
            // substring
            freq[toNum(str[j])]++;

            // increase count corresponding
            // to this freq array
            mp[freq]++;
        }
    }

    // loop over all different freq array and
    // aggregate substring count
    int result = 0;
    for (auto it=mp.begin(); it!=mp.end(); it++)
    {
        int freq = it->second;
        result += ((freq) * (freq-1))/2;
    }
    return result;
}

//  Driver code to test above methods
int main()
{
    string str = "xyyx";
    cout << countOfAnagramSubstring(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
import java.util.HashMap;

public class anagramPairCount {
    public static void main(String[] args) {
        subString("kkkk");
    }

    static void subString(String s){
        HashMap<String, Integer> map= new HashMap<>();

        for(int i = 0; i < s.length(); i++){
            for(int j = i; j < s.length(); j++){
                char[] valC = s.substring(i, j+1).toCharArray();
                Arrays.sort(valC);
                String val = new String(valC);
                if (map.containsKey(val)) 
                    map.put(val, map.get(val)+1);
                else 
                    map.put(val, 1);
            }
        }
        int anagramPairCount = 0;
        for(String key: map.keySet()){
            int n = map.get(key);
            anagramPairCount += (n * (n-1))/2;
        }
        System.out.println(anagramPairCount);
    }
}
```

## 蟒蛇 3

```
# Python3 program to count total anagram
# substring of a string
def countOfAnagramSubstring(s):

    # Returns total number of anagram
    # substrings in s
    n = len(s)
    mp = dict()

    # loop for length of substring
    for i in range(n):
        sb = ''
        for j in range(i, n):
            sb = ''.join(sorted(sb + s[j]))
            mp[sb] = mp.get(sb, 0)

            # increase count corresponding
            # to this dict array
            mp[sb] += 1

    anas = 0

    # loop over all different dictionary 
    # items and aggregate substring count
    for k, v in mp.items():
        anas += (v*(v-1))//2
    return anas

# Driver Code
s = "xyyx"
print(countOfAnagramSubstring(s))

# This code is contributed by fgaim
```

## C#

```
using System;
using System.Collections.Generic;

public class anagramPairCount {
    public static void Main() {
        subString("kkkk");
    }

    static void subString(String s){
        Dictionary<string, int> map= new Dictionary<string, int>();

        for(int i = 0; i < s.Length; i++){
            for(int j = i; j < s.Length; j++){
                char[] valC = s.Substring(i, j+1-i).ToCharArray();
                Array.Sort(valC);
                string val = new string(valC);
                if (map.ContainsKey(val)) 
                    map[val]=map[val]+1;
                else
                    map.Add(val, 1);
            }
        }
        int anagramPairCount = 0;
        foreach(string key in map.Keys){
            int n = map[key];
            anagramPairCount += (n * (n-1))/2;
        }
        Console.Write(anagramPairCount);
    }
}

// This code is contributed by AbhiThakur
```

**Output:**

```
4

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。