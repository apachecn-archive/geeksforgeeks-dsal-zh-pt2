# 最长不常见子序列

> 原文:[https://www.geeksforgeeks.org/longest-uncommon-subsequence/](https://www.geeksforgeeks.org/longest-uncommon-subsequence/)

给定两个字符串，找出两个字符串中最长**不常见**子序列的长度。最长的不常见子序列被定义为这些字符串之一的最长子序列，它不是其他字符串的子序列。
**例:**

```
Input : "abcd", "abc"
Output : 4
The longest subsequence is 4 because "abcd"
is a subsequence of first string, but not
a subsequence of second string.

Input : "abc", "abc"
Output : 0
Both strings are same, so there is no 
uncommon subsequence.
```

**蛮力:**一般来说，有些人可能首先想到的是生成两个字符串的所有可能的 2 <sup>n</sup> 子序列，并将它们的频率存储在一个 hashmap 中。频率等于 1 的最长子序列将是所需的子序列。

## C++

```
// CPP program to find longest uncommon
// subsequence using naive method
#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

// function to calculate length of longest uncommon subsequence
int findLUSlength(string a, string b)
{
    /* creating an unordered map to map
       strings to their frequency*/
    unordered_map<string, int> map;
    vector<string> strArr;
    strArr.push_back(a);
    strArr.push_back(b);

    // traversing all elements of vector strArr
    for (string s : strArr)
    {
        /* Creating all possible subsequences, i.e 2^n*/
        for (int i = 0; i < (1 << s.length()); i++)
        {
            string t = "";
            for (int j = 0; j < s.length(); j++) {

                /* ((i>>j) & 1) determines which 
                   character goes into string t*/
                if (((i >> j) & 1) != 0) 
                    t += s[j];
            }

            /* If common subsequence is found,
               increment its frequency*/
            if (map.count(t))
                map[t]++;
            else
                map[t] = 1;
        }
    }
    int res = 0;
    for (auto a : map) // traversing the map
    {
         // if frequency equals 1  
        if (a.second == 1)
            res = max(res, (int)a.first.length());
    }
    return res;
}
int main()
{
    // Your C++ Code
    string a = "abcdabcd", b = "abcabc"; // input strings
    cout << findLUSlength(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest uncommon
// subsequence using naive method
import java.io.*;
import java.util.*;

class GfG{

// function to calculate length of
// longest uncommon subsequence
static int findLUSlength(String a, String b)
{
    // creating an unordered map to map
    // strings to their frequency
    HashMap<String, Integer> map= new HashMap<String, Integer>();
    Vector<String> strArr= new Vector<String>();
    strArr.add(a);
    strArr.add(b);

    // traversing all elements of vector strArr
    for (String s : strArr)
    {
        // Creating all possible subsequences, i.e 2^n
        for (int i = 0; i < (1 << s.length()); i++)
        {
            String t = "";
            for (int j = 0; j < s.length(); j++) {

                // ((i>>j) & 1) determines which
                // character goes into string t
                if (((i >> j) & 1) != 0)
                    t += s.charAt(j);
            }

            // If common subsequence is found,
            // increment its frequency
            if (map.containsKey(t))
                map.put(t,map.get(t)+1);
            else
                map.put(t,1);
        }
    }
    int res = 0;
    for (HashMap.Entry<String, Integer> entry : map.entrySet())

    // traversing the map
    {
        // if frequency equals 1
        if (entry.getValue() == 1)
            res = Math.max(res, entry.getKey().length());
    }
    return res;
}

    // Driver code
    public static void main (String[] args) {

    // input strings
    String a = "abcdabcd", b = "abcabc";
       System.out.println(findLUSlength(a, b));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 program to find longest uncommon
# subsequence using naive method

# function to calculate length of
# longest uncommon subsequence
def findLUSlength(a, b):

    ''' creating an unordered map to map
    strings to their frequency'''
    map = dict()
    strArr = []
    strArr.append(a)
    strArr.append(b)

    # traversing all elements of vector strArr
    for s in strArr:

        ''' Creating all possible subsequences, i.e 2^n'''
        for i in range(1 << len(s)):
            t = ""
            for j in range(len(s)):

                ''' ((i>>j) & 1) determines which
                character goes into t'''
                if (((i >> j) & 1) != 0):
                    t += s[j]

            # If common subsequence is found,
            # increment its frequency
            if (t in map.keys()):
                map[t] += 1;
            else:
                map[t] = 1

    res = 0
    for a in map: # traversing the map
                  # if frequency equals 1
        if (map[a] == 1):
            res = max(res, len(a))

    return res

# Driver Code
a = "abcdabcd"
b = "abcabc" # input strings
print(findLUSlength(a, b))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find longest
// uncommon subsequence using
// naive method
using System;
using System.Collections.Generic;

class GFG
{    
    // function to calculate
    // length of longest
    // uncommon subsequence
    static int findLUSlength(string a,
                             string b)
    {
        // creating an unordered
        // map to map strings to
        // their frequency
        Dictionary<string, int> map =
                   new Dictionary<string, int>();
        List<string> strArr =
                 new List<string>();
        strArr.Add(a);
        strArr.Add(b);

        // traversing all elements
        // of vector strArr
        foreach (string s in strArr)
        {
            // Creating all possible
            // subsequences, i.e 2^n
            for (int i = 0;
                     i < (1 << s.Length); i++)
            {
                string t = "";
                for (int j = 0;
                         j < s.Length; j++)
                {

                    // ((i>>j) & 1) determines
                    // which character goes
                    // into string t
                    if (((i >> j) & 1) != 0)
                        t += s[j];
                }

                // If common subsequence
                // is found, increment
                // its frequency
                if (map.ContainsKey(t))
                {
                    int value = map[t] + 1;
                    map.Remove(t);
                    map.Add(t, value);
                }
                else
                    map.Add(t, 1);
            }
        }
        int res = 0;
        foreach (KeyValuePair<string, int>
                             entry in map)
        // traversing the map
        {
            // if frequency equals 1
            if (entry.Value == 1)
                res = Math.Max(res,
                           entry.Key.Length);
        }
        return res;
    }

    // Driver code
    static void Main ()
    {

        // input strings
        string a = "abcdabcd",
               b = "abcabc";

        Console.Write(findLUSlength(a, b));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// JavaScript program to find longest uncommon
// subsequence using naive method

    // function to calculate length of
// longest uncommon subsequence
    function findLUSlength(a,b)
    {
        // creating an unordered map to map
    // strings to their frequency
    let map= new Map();
    let strArr= [];
    strArr.push(a);
    strArr.push(b);

    // traversing all elements of vector strArr
    for (let s=0; s<strArr.length;s++)
    {
        // Creating all possible subsequences, i.e 2^n
        for (let i = 0; i < (1 << strArr[s].length); i++)
        {
            let t = "";
            for (let j = 0; j < strArr[s].length; j++) {

                // ((i>>j) & 1) determines which
                // character goes into string t
                if (((i >> j) & 1) != 0)

                    t += strArr[s][j];

            }

            // If common subsequence is found,
            // increment its frequency
            if (map.has(t))
                map.set(t,map.get(t)+1);
            else
                map.set(t,1);
        }
    }
    let res = 0;
    for (let [key, value] of map.entries())

    // traversing the map
    {
        // if frequency equals 1
        if (value == 1)
            res = Math.max(res, key.length);
    }
    return res;
    }

    // Driver code

    // input strings
    let a = "abcdabcd", b = "abcabc";
    document.write(findLUSlength(a, b));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
8
```

*   时间复杂度:O(2 <sup>x</sup> + 2 <sup>y</sup> ，其中 x 和 y 为两根弦的长度。
*   辅助空间:O(2 <sup>x</sup> + 2 <sup>y</sup> )。

**高效算法:**如果我们仔细分析这个问题，它看起来会比看起来容易得多。所有三种可能的情况如下所述；

1.  如果两个字符串相同，例如:“ac”和“ac”，很明显没有子序列是不常见的。因此，返回 0。
2.  如果长度(a) =长度(b)和 a？b，例如:“abcdef”和“defghi”，在这两个字符串中，一个字符串永远不会是另一个字符串的子序列。
    因此，返回长度(a)或长度(b)。
3.  如果长度(a)？长度(b)，例如:“abcdabcd”和“abcabc”，在这种情况下，我们可以将较大的字符串视为必需的子序列，因为较大的字符串不能是较小字符串的子序列。因此，返回最大值(长度(a)，长度(b))。

## C++

```
// CPP Program to find longest uncommon
// subsequence.
#include <iostream>
using namespace std;

// function to calculate length of longest
// uncommon subsequence
int findLUSlength(string a, string b)
{
    // Case 1: If strings are equal
    if (!a.compare(b))
        return 0;

     // for case 2 and case 3
    return max(a.length(), b.length());
}

// Driver code
int main()
{
    string a = "abcdabcd", b = "abcabc";
    cout << findLUSlength(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest uncommon
// subsequence using naive method

import java.io.*;
import java.util.*;

class GfG{

// function to calculate length of longest
// uncommon subsequence
static int findLUSlength(String a, String b)
{
    // Case 1: If strings are equal
    if (a.equals(b)==true)
        return 0;

     // for case 2 and case 3
    return Math.max(a.length(), b.length());
}
    // Driver code
    public static void main (String[] args) {

    // input strings
    String a = "abcdabcd", b = "abcabc";
       System.out.println(findLUSlength(a, b));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python program to find
# longest uncommon
# subsequence using naive method

import math

# function to calculate
# length of longest
# uncommon subsequence
def findLUSlength( a, b):

    # Case 1: If strings are equal
    if (a==b) :
        return 0

     # for case 2 and case 3
    return max(len(a), len(b))

# Driver code

#input strings
a = "abcdabcd"
b = "abcabc"
print (findLUSlength(a, b))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to find longest uncommon
// subsequence using naive method.
using System;

class GfG {

    // function to calculate length
    // of longest uncommon subsequence
    static int findLUSlength(String a, String b)
    {

        // Case 1: If strings are equal
        if (a.Equals(b)==true)
            return 0;

        // for case 2 and case 3
        return Math.Max(a.Length, b.Length);
    }

    // Driver code
    public static void Main ()
    {

        // input strings
        String a = "abcdabcd", b = "abcabc";
        Console.Write(findLUSlength(a, b));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find longest
// uncommon subsequence.

// function to calculate length
// of longest uncommon subsequence
function findLUSlength($a, $b)
{
    // Case 1: If strings
    // are equal
    if (!strcmp($a, $b))
        return 0;

    // for case 2
    // and case 3
    return max(strlen($a),
               strlen($b));
}

// Driver code
$a = "abcdabcd";
$b = "abcabc";
echo (findLUSlength($a, $b));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find longest uncommon
// subsequence.

// function to calculate length of longest
// uncommon subsequence
function findLUSlength(a, b)
{
    // Case 1: If strings are equal
    if (a===b)
        return 0;

     // for case 2 and case 3
    return Math.max(a.length, b.length);
}

// Driver code
var a = "abcdabcd", b = "abcabc";
document.write( findLUSlength(a, b));

</script>
```

**输出:**

```
8
```

**复杂度分析:**

*   时间复杂度:O(min(x，y))，其中 x 和 y 是两个字符串的长度。
*   辅助空间:0(1)。