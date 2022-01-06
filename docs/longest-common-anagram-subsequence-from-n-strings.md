# N 个字符串中最长的常见字谜子序列

> 原文:[https://www . geesforgeks . org/long-common-anagram-subsequence-from-n-strings/](https://www.geeksforgeeks.org/longest-common-anagram-subsequence-from-n-strings/)

给定 N 个字符串。从这 N 个字符串中找出最长的可能子序列，这样它们彼此之间就是[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。任务是打印所有子序列中字典顺序最大的子序列。

**示例:**

> **输入:** s[] = { geeks，esrka，efrsk }
> **输出:** ske
> 第一个字符串有“eks”，第二个字符串有“esk”，第三个字符串有“esk”。这三个是字谜。“ske”的尺寸很大。
> 
> **输入:**字符串 s[] = { loop，lol，olive }
> T3】输出: ol

**进场:**

*   制作一个 **n*26** 的二维数组，以字符串的形式存储每个字符的频率。
*   制作频率数组后，对每个数字进行反向遍历，找到该类型字符最少的字符串。
*   完成反向遍历后，打印出现次数最少的字符，因为它给出了字典中最大的字符串。

下面是上述方法的实现。

## C++

```
// C++ program to find longest possible
// subsequence anagram of N strings.
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// function to store frequency of
// each character in each string
void frequency(int fre[][MAX_CHAR], string s[], int n)
{
    for (int i = 0; i < n; i++) {
        string str = s[i];
        for (int j = 0; j < str.size(); j++)
            fre[i][str[j] - 'a']++;       
    }
}

// function to Find longest possible sequence of N
// strings which is anagram to each other
void LongestSequence(int fre[][MAX_CHAR], int n)
{
    // to get lexicographical largest sequence.
    for (int i = MAX_CHAR-1; i >= 0; i--) {

        // find minimum of that character
        int mi = fre[0][i];
        for (int j = 1; j < n; j++)
            mi = min(fre[j][i], mi);       

        // print that character
        // minimum number of times
        while (mi--)
            cout << (char)('a' + i);       
    }
}

// Driver code
int main()
{

    string s[] = { "loo", "lol", "olive" };
    int n = sizeof(s)/sizeof(s[0]);

    // to store frequency of each character in each string
    int fre[n][26] = { 0 };

    // to get frequency of each character
    frequency(fre, s, n);

    // function call
    LongestSequence(fre, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest
// possible subsequence anagram
// of N strings.
class GFG
{
final int MAX_CHAR = 26;

// function to store frequency
// of each character in each
// string
static void frequency(int fre[][],
                      String s[], int n)
{
    for (int i = 0; i < n; i++)
    {
        String str = s[i];
        for (int j = 0;
                 j < str.length(); j++)
            fre[i][str.charAt(j) - 'a']++;    
    }
}

// function to Find longest
// possible sequence of N
// strings which is anagram
// to each other
static void LongestSequence(int fre[][],
                            int n)
{
    // to get lexicographical
    // largest sequence.
    for (int i = 24; i >= 0; i--)
    {

        // find minimum of
        // that character
        int mi = fre[0][i];
        for (int j = 1; j < n; j++)
            mi = Math.min(fre[j][i], mi);    

        // print that character
        // minimum number of times
        while (mi--!=0)
            System.out.print((char)('a' + i));    
    }
}

// Driver code
public static void main(String args[])
{

    String s[] = { "loo", "lol", "olive" };
    int n = s.length;

    // to store frequency of each
    // character in each string
    int fre[][] = new int[n][26] ;

    // to get frequency
    // of each character
    frequency(fre, s, n);

    // function call
    LongestSequence(fre, n);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find longest possible
# subsequence anagram of N strings.

# Function to store frequency of
# each character in each string
def frequency(fre, s, n):

    for i in range(0, n):
        string = s[i]
        for j in range(0, len(string)):
            fre[i][ord(string[j]) - ord('a')] += 1       

# Function to Find longest possible sequence 
# of N strings which is anagram to each other
def LongestSequence(fre, n):

    # to get lexicographical largest sequence.
    for i in range(MAX_CHAR-1, -1, -1):

        # find minimum of that character
        mi = fre[0][i]
        for j in range(1, n):
            mi = min(fre[j][i], mi)        

        # print that character
        # minimum number of times
        while mi:
            print(chr(ord('a') + i), end = "")
            mi -= 1

# Driver code
if __name__ == "__main__":

    s = ["loo", "lol", "olive"]
    n = len(s)
    MAX_CHAR = 26

    # to store frequency of each
    # character in each string
    fre = [[0 for i in range(26)]
              for j in range(n)]

    # To get frequency of each character
    frequency(fre, s, n)

    # Function call
    LongestSequence(fre, n)

# This code is contributed by
# Rituraj Jain
```

## C#

```
// c# program to find longest
// possible subsequence anagram
// of N strings.
using System;

class GFG
{
public readonly int MAX_CHAR = 26;

// function to store frequency
// of each character in each
// string
public static void frequency(int[,] fre,
                             string[] s, int n)
{
    for (int i = 0; i < n; i++)
    {
        string str = s[i];
        for (int j = 0;
                 j < str.Length; j++)
        {
            fre[i, str[j] - 'a']++;
        }
    }
}

// function to Find longest
// possible sequence of N
// strings which is anagram
// to each other
public static void LongestSequence(int[, ] fre,
                                   int n)
{
    // to get lexicographical
    // largest sequence.
    for (int i = 24; i >= 0; i--)
    {

        // find minimum of
        // that character
        int mi = fre[0, i];
        for (int j = 1; j < n; j++)
        {
            mi = Math.Min(fre[j, i], mi);
        }

        // print that character
        // minimum number of times
        while (mi--!=0)
        {
            Console.Write((char)('a' + i));
        }
    }
}

// Driver code
public static void Main(string[] args)
{

    string[] s = new string[] {"loo", "lol", "olive"};
    int n = s.Length;

    // to store frequency of each
    // character in each string
    int[, ] fre = new int[n, 26];

    // to get frequency
    // of each character
    frequency(fre, s, n);

    // function call
    LongestSequence(fre, n);
}
}

// This code is contributed by Shrikanth13
```

## java 描述语言

```
<script>

// JavaScript program to find longest
// possible subsequence anagram
// of N strings.

let MAX_CHAR = 26;

// function to store frequency
// of each character in each
// string
function frequency(fre,s,n)
{
    for (let i = 0; i < n; i++)
    {
        let str = s[i];
        for (let j = 0;
                 j < str.length; j++)
            fre[i][str[j].charCodeAt(0) - 'a'.charCodeAt(0)]++;   
    }
}

// function to Find longest
// possible sequence of N
// strings which is anagram
// to each other
function LongestSequence(fre,n)
{
    // to get lexicographical
    // largest sequence.
    for (let i = 24; i >= 0; i--)
    {

        // find minimum of
        // that character
        let mi = fre[0][i];
        for (let j = 1; j < n; j++)
            mi = Math.min(fre[j][i], mi);   

        // print that character
        // minimum number of times
        while (mi--!=0)
            document.write(String.fromCharCode
            ('a'.charCodeAt(0) + i));   
    }
}

// Driver code
let s=["loo", "lol", "olive"];
let n = s.length;

// to store frequency of each
// character in each string
let fre = new Array(n) ;
for(let i=0;i<n;i++)
{
    fre[i]=new Array(26);
    for(let j=0;j<26;j++)
        fre[i][j]=0;
}

// to get frequency
// of each character
frequency(fre, s, n);

// function call
LongestSequence(fre, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
ol
```