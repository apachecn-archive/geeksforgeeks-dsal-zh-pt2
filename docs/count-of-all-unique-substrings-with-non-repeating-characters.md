# 计数所有具有非重复字符的唯一子串

> 原文:[https://www . geesforgeks . org/count-of-all-unique-substrings-with-non-repeating-characters/](https://www.geeksforgeeks.org/count-of-all-unique-substrings-with-non-repeating-characters/)

给定一个由小写字符组成的字符串 **str** ，任务是找出具有不重复字符的唯一子字符串的总数。
**例:**

> **输入:** str = "abba"
> **输出:** 4
> **说明:**
> 有 4 个唯一的子串。它们是:“a”、“ab”、“b”、“ba”。
> **输入:** str = "acbacbacaa"
> **输出:** 10

**方法:**想法是[迭代所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)。对于每个子串，检查每个特定的字符以前是否出现过。如果是，则增加所需子字符串的数量。最后，将此计数作为包含非重复字符的所有唯一子字符串的计数返回。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the count of
// all unique sub-strings with
// non-repeating characters

#include <bits/stdc++.h>
using namespace std;

// Function to count all unique
// distinct character substrings
int distinctSubstring(string& P, int N)
{
    // Hashmap to store all substrings
    unordered_set<string> S;

    // Iterate over all the substrings
    for (int i = 0; i < N; ++i) {

        // Boolean array to maintain all
        // characters encountered so far
        vector<bool> freq(26, false);

        // Variable to maintain the
        // substring till current position
        string s;

        for (int j = i; j < N; ++j) {

            // Get the position of the
            // character in the string
            int pos = P[j] - 'a';

            // Check if the character is
            // encountred
            if (freq[pos] == true)
                break;

            freq[pos] = true;

            // Add the current character
            // to the substring
            s += P[j];

            // Insert substring in Hashmap
            S.insert(s);
        }
    }

    return S.size();
}

// Driver code
int main()
{
    string S = "abba";
    int N = S.length();

    cout << distinctSubstring(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// all unique sub-Strings with
// non-repeating characters
import java.util.*;

class GFG{

// Function to count all unique
// distinct character subStrings
static int distinctSubString(String P, int N)
{
    // Hashmap to store all subStrings
    HashSet<String> S = new HashSet<String>();

    // Iterate over all the subStrings
    for (int i = 0; i < N; ++i) {

        // Boolean array to maintain all
        // characters encountered so far
        boolean []freq = new boolean[26];

        // Variable to maintain the
        // subString till current position
        String s = "";

        for (int j = i; j < N; ++j) {

            // Get the position of the
            // character in the String
            int pos = P.charAt(j) - 'a';

            // Check if the character is
            // encountred
            if (freq[pos] == true)
                break;

            freq[pos] = true;

            // Add the current character
            // to the subString
            s += P.charAt(j);

            // Insert subString in Hashmap
            S.add(s);
        }
    }

    return S.size();
}

// Driver code
public static void main(String[] args)
{
    String S = "abba";
    int N = S.length();

    System.out.print(distinctSubString(S, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the count of
# all unique sub-strings with
# non-repeating characters

# Function to count all unique
# distinct character substrings
def distinctSubstring(P, N):

    # Hashmap to store all substrings
    S = dict()

    # Iterate over all the substrings
    for i in range(N):

        # Boolean array to maintain all
        # characters encountered so far
        freq = [False]*26

        # Variable to maintain the
        # subtill current position
        s = ""

        for j in range(i,N):

            # Get the position of the
            # character in the string
            pos = ord(P[j]) - ord('a')

            # Check if the character is
            # encountred
            if (freq[pos] == True):
                break

            freq[pos] = True

            # Add the current character
            # to the substring
            s += P[j]

            # Insert subin Hashmap
            S[s] = 1

    return len(S)

# Driver code
S = "abba"
N = len(S)

print(distinctSubstring(S, N))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to find the count of
// all unique sub-Strings with
// non-repeating characters
using System;
using System.Collections.Generic;

class GFG{

// Function to count all unique
// distinct character subStrings
static int distinctSubString(String P, int N)
{
    // Hashmap to store all subStrings
    HashSet<String> S = new HashSet<String>();

    // Iterate over all the subStrings
    for (int i = 0; i < N; ++i) {

        // Boolean array to maintain all
        // characters encountered so far
        bool []freq = new bool[26];

        // Variable to maintain the
        // subString till current position
        String s = "";

        for (int j = i; j < N; ++j) {

            // Get the position of the
            // character in the String
            int pos = P[j] - 'a';

            // Check if the character is
            // encountred
            if (freq[pos] == true)
                break;

            freq[pos] = true;

            // Add the current character
            // to the subString
            s += P[j];

            // Insert subString in Hashmap
            S.Add(s);
        }
    } 
    return S.Count;
}

// Driver code
public static void Main(String[] args)
{
    String S = "abba";
    int N = S.Length;

    Console.Write(distinctSubString(S, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the count of
// all unique sub-strings with
// non-repeating characters

// Function to count all unique
// distinct character substrings
function distinctSubstring(P, N)
{
    // Hashmap to store all substrings
    var S = new Set();

    // Iterate over all the substrings
    for (var i = 0; i < N; ++i) {

        // Boolean array to maintain all
        // characters encountered so far
        var freq = Array(26).fill(false);

        // Variable to maintain the
        // substring till current position
        var s = "";

        for (var j = i; j < N; ++j) {

            // Get the position of the
            // character in the string
            var pos = P[j].charCodeAt(0) - 'a'.charCodeAt(0);

            // Check if the character is
            // encountred
            if (freq[pos] == true)
                break;

            freq[pos] = true;

            // Add the current character
            // to the substring
            s += P[j];

            // Insert substring in Hashmap
            S.add(s);
        }
    }

    return S.size;
}

// Driver code
var S = "abba";
var N = S.length;
document.write( distinctSubstring(S, N));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N <sup>2</sup> )，其中 N 为弦的长度。