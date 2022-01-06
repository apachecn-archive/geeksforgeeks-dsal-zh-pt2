# 满足给定条件的给定字符串可以拆分的最小子字符串数

> 原文:[https://www . geesforgeks . org/最小子字符串数-给定字符串可以拆分成满足给定条件的字符串/](https://www.geeksforgeeks.org/minimum-number-of-substrings-the-given-string-can-be-splitted-into-that-satisfy-the-given-conditions/)

给定一个字符串**字符串**和一个字符串数组 **arr[]** ，任务是找到可以拆分的子字符串的最小数量，这样每个子字符串都出现在给定的字符串数组 **arr[]** 中。

**示例:**

> **输入:**str =“111112”，arr[]= {“11”、“111”、“11111”、“2”}
> **输出:**2
> “11111”和“2”为必输子串。
> “11”“111”“2”也可以是有效答案
> 但不是最小值。
> 
> **输入:** str = "123456 "，arr[] = {"1 "、" 12345 "、" 2345 "、" 56 "、" 23 "、" 456"}
> **输出:** 3

**方法:**从索引 **0** 迭代字符串并构建前缀字符串，如果前缀字符串存在于给定数组中(可以使用集合来检查这一点)，则从字符串中的下一个位置再次调用该函数，并跟踪子字符串的总最小计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Set to store all the strings
// from the given array
unordered_set<string> uSet;

// To store the required count
int minCnt = INT_MAX;

// Recursive function to find the count of
// substrings that can be splitted starting
// from the index start such that all
// the substrings are present in the map
void findSubStr(string str, int cnt, int start)
{

    // All the chosen substrings
    // are present in the map
    if (start == str.length()) {

        // Update the minimum count
        // of substrings
        minCnt = min(cnt, minCnt);
    }

    // Starting from the substrings of length 1
    // that start with the given index
    for (int len = 1; len <= (str.length() - start); len++) {

        // Get the substring
        string subStr = str.substr(start, len);

        // If the substring is present in the set
        if (uSet.find(subStr) != uSet.end()) {

            // Recursive call for the
            // rest of the string
            findSubStr(str, cnt + 1, start + len);
        }
    }
}

// Function that inserts all the strings
// from the given array in a set and calls
// the recursive function to find the
// minimum count of substrings str can be
// splitted into that satisfy the given condition
void findMinSubStr(string arr[], int n, string str)
{

    // Insert all the strings from
    // the given array in a set
    for (int i = 0; i < n; i++)
        uSet.insert(arr[i]);

    // Find the required count
    findSubStr(str, 0, 0);
}

// Driver code
int main()
{
    string str = "123456";
    string arr[] = { "1", "12345", "2345",
                     "56", "23", "456" };
    int n = sizeof(arr) / sizeof(string);

    findMinSubStr(arr, n, str);

    cout << minCnt;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
import java.util.*;

class GFG
{

// Set to store all the Strings
// from the given array
static Set<String> uSet = new HashSet<String>();

// To store the required count
static int minCnt = Integer.MAX_VALUE;

// Recursive function to find the count of
// subStrings that can be splitted starting
// from the index start such that all
// the subStrings are present in the map
static void findSubStr(String str, int cnt, int start)
{

    // All the chosen subStrings
    // are present in the map
    if (start == str.length())
    {

        // Update the minimum count
        // of subStrings
        minCnt = Math.min(cnt, minCnt);
    }

    // Starting from the subStrings of length 1
    // that start with the given index
    for (int len = 1;
             len <= (str.length() - start); len++)
    {

        // Get the subString
        String subStr = str.substring(start, start + len);

        // If the subString is present in the set
        if (uSet.contains(subStr))
        {

            // Recursive call for the
            // rest of the String
            findSubStr(str, cnt + 1, start + len);
        }
    }
}

// Function that inserts all the Strings
// from the given array in a set and calls
// the recursive function to find the
// minimum count of subStrings str can be
// splitted into that satisfy the given condition
static void findMinSubStr(String arr[],
                   int n, String str)
{

    // Insert all the Strings from
    // the given array in a set
    for (int i = 0; i < n; i++)
        uSet.add(arr[i]);

    // Find the required count
    findSubStr(str, 0, 0);
}

// Driver code
public static void main(String args[])
{
    String str = "123456";
    String arr[] = {"1", "12345", "2345",
                    "56", "23", "456" };
    int n = arr.length;

    findMinSubStr(arr, n, str);

    System.out.print(minCnt);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Set to store all the strings
# from the given array
uSet = set();

# To store the required count
minCnt = sys.maxsize;

# Recursive function to find the count of
# substrings that can be splitted starting
# from the index start such that all
# the substrings are present in the map
def findSubStr(string, cnt, start) :

    global minCnt;

    # All the chosen substrings
    # are present in the map
    if (start == len(string)) :

        # Update the minimum count
        # of substrings
        minCnt = min(cnt, minCnt);

    # Starting from the substrings of length 1
    # that start with the given index
    for length in range(1, len(string) - start + 1) :

        # Get the substring
        subStr = string[start : start + length];

        # If the substring is present in the set
        if subStr in uSet :

            # Recursive call for the
            # rest of the string
            findSubStr(string, cnt + 1, start + length);

# Function that inserts all the strings
# from the given array in a set and calls
# the recursive function to find the
# minimum count of substrings str can be
# splitted into that satisfy the given condition
def findMinSubStr(arr, n, string) :

    # Insert all the strings from
    # the given array in a set
    for i in range(n) :
        uSet.add(arr[i]);

    # Find the required count
    findSubStr(string, 0, 0);

# Driver code
if __name__ == "__main__" :

    string = "123456";
    arr = ["1", "12345", "2345",
           "56", "23", "456" ];

    n = len(arr);

    findMinSubStr(arr, n, string);

    print(minCnt);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Set to store all the Strings
// from the given array
static HashSet<String> uSet = new HashSet<String>();

// To store the required count
static int minCnt = int.MaxValue;

// Recursive function to find the count of
// subStrings that can be splitted starting
// from the index start such that all
// the subStrings are present in the map
static void findSubStr(String str, int cnt, int start)
{

    // All the chosen subStrings
    // are present in the map
    if (start == str.Length)
    {

        // Update the minimum count
        // of subStrings
        minCnt = Math.Min(cnt, minCnt);
    }

    // Starting from the subStrings of length 1
    // that start with the given index
    for (int len = 1;
            len <= (str.Length - start); len++)
    {

        // Get the subString
        String subStr = str.Substring(start, len);

        // If the subString is present in the set
        if (uSet.Contains(subStr))
        {

            // Recursive call for the
            // rest of the String
            findSubStr(str, cnt + 1, start + len);
        }
    }
}

// Function that inserts all the Strings
// from the given array in a set and calls
// the recursive function to find the
// minimum count of subStrings str can be
// splitted into that satisfy the given condition
static void findMinSubStr(String []arr,
                          int n, String str)
{

    // Insert all the Strings from
    // the given array in a set
    for (int i = 0; i < n; i++)
        uSet.Add(arr[i]);

    // Find the required count
    findSubStr(str, 0, 0);
}

// Driver code
public static void Main(String []args)
{
    String str = "123456";
    String []arr = {"1", "12345", "2345",
                    "56", "23", "456" };
    int n = arr.Length;

    findMinSubStr(arr, n, str);

    Console.WriteLine(minCnt);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Set to store all the strings
// from the given array
var uSet = new Set();

// To store the required count
var minCnt = 1000000000;

// Recursive function to find the count of
// substrings that can be splitted starting
// from the index start such that all
// the substrings are present in the map
function findSubStr( str,  cnt, start)
{

    // All the chosen substrings
    // are present in the map
    if (start == str.length) {

        // Update the minimum count
        // of substrings
        minCnt = Math.min(cnt, minCnt);
    }

    // Starting from the substrings of length 1
    // that start with the given index
    for (var len = 1; len <= (str.length - start); len++) {

        // Get the substring
        var subStr = str.substring(start, start+len);

        // If the substring is present in the set
        if (uSet.has(subStr)) {

            // Recursive call for the
            // rest of the string
            findSubStr(str, cnt + 1, start + len);
        }
    }
}

// Function that inserts all the strings
// from the given array in a set and calls
// the recursive function to find the
// minimum count of substrings str can be
// splitted into that satisfy the given condition
function findMinSubStr(arr, n, str)
{

    // Insert all the strings from
    // the given array in a set
    for (var i = 0; i < n; i++)
        uSet.add(arr[i]);

    // Find the required count
    findSubStr(str, 0, 0);
}

// Driver code
 var str = "123456";
 var arr = ["1", "12345", "2345",
                  "56", "23", "456"];
 var n = arr.length;
 findMinSubStr(arr, n, str);
 document.write( minCnt);

</script>
```

**Output:** 

```
3
```