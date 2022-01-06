# 不同的字符串，它们包含给定的字符串作为子序列

> 原文:[https://www . geesforgeks . org/distinct-strings-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-these-](https://www.geeksforgeeks.org/distinct-strings-such-that-they-contains-given-strings-as-sub-sequences/)

分别给定长度为 **M** 和 **N** 的两根弦 **str1** 和 **str2** 。任务是找到所有长度不同的字符串 **M + N** ，使得结果字符串中任何字符的频率等于给定字符串中相同字符的频率之和，并且这两个给定字符串都作为子序列出现在所有生成的字符串中。
**举例:**

> **输入:**【str = " aa】，【str 2 = " ab】
> **输出:**
> 【ABA】
> 【aaab】
> 【aaba】**输入:**【str 1 = " ab】，str2 = "de" 【T】

**方法:**这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)解决。将两个指针 **i** 和 **j** 分别设置到琴弦 **str1** 和 **str2** 的开始处。现在，在每次递归调用中，我们有两个选择，要么选择 **str1[i]** 处的字符，要么选择 **str2[j]** 处的字符，终止条件是结果字符串的长度等于 **len(str1) + len(str2)** 。使用[无序集](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)以避免重复。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Set to store strings
// and avoid duplicates
set<string> stringSet;

// Recursive function to generate the required strings
void find_permutation(string& str1, string& str2, int len1,
                      int len2, int i, int j, string res)
{
    // If current string is part of the result
    if (res.length() == len1 + len2) {

        // Insert it into the set
        stringSet.insert(res);
        return;
    }

    // If character from str1 can be chosen
    if (i < len1)
        find_permutation(str1, str2, len1, len2,
                         i + 1, j, res + str1[i]);

    // If character from str2 can be chosen
    if (j < len2)
        find_permutation(str1, str2, len1, len2,
                         i, j + 1, res + str2[j]);
}

// Function to print the generated
// strings from the set
void print_set()
{
    set<string>::iterator itr;
    for (itr = stringSet.begin(); itr != stringSet.end(); itr++)
        cout << (*itr) << endl;
}

// Driver code
int main()
{
    string str1 = "aa", str2 = "ab";
    int len1 = str1.length();
    int len2 = str2.length();

    find_permutation(str1, str2, len1,
                     len2, 0, 0, "");
    print_set();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashSet;

class GFG
{

    // Set to store strings
    // and avoid duplicates
    static HashSet<String> stringSet = new HashSet<>();

    // Recursive function to generate the required strings
    public static void find_permutation(String str1, String str2,
                                        int len1, int len2, int i,
                                        int j, String res)
    {

        // If current string is part of the result
        if (res.length() == len1 + len2)
        {

            // Insert it into the set
            stringSet.add(res);
            return;
        }

        // If character from str1 can be chosen
        if (i < len1)
            find_permutation(str1, str2, len1, len2, i + 1,
                                    j, res + str1.charAt(i));

        // If character from str2 can be chosen
        if (j < len2)
            find_permutation(str1, str2, len1, len2, i, j + 1,
                                           res + str2.charAt(j));
    }

    // Function to print the generated
    // strings from the set
    public static void print_set()
    {
        for (String s : stringSet)
            System.out.println(s);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "aa", str2 = "ab";
        int len1 = str1.length();
        int len2 = str2.length();

        find_permutation(str1, str2, len1, len2, 0, 0, "");

        print_set();
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Set to store strings
# and aduplicates
stringSet=dict()

# Recursive function to generate the required strings
def find_permutation( str1,str2,len1,len2,i,j,res):
    # If currentis part of the result
    if (len(res) == len1 + len2):

        # Insert it into the set
        stringSet[res]=1
        return

    # If character from str1 can be chosen
    if (i < len1):
        find_permutation(str1, str2, len1, len2,i + 1, j, res + str1[i])

    # If character from str2 can be chosen
    if (j < len2):
        find_permutation(str1, str2, len1, len2,i, j + 1, res + str2[j])

# Function to print the generated
# strings from the set
def print_set():

    for i in stringSet:
        print(i)

# Driver code

str1 = "aa"
str2 = "ab"
len1 = len(str1)
len2 = len(str2)

find_permutation(str1, str2, len1,len2, 0, 0, "")
print_set()

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Set to store strings
    // and avoid duplicates
    static HashSet<String> stringSet = new HashSet<String>();

    // Recursive function to generate the required strings
    public static void find_permutation(String str1, String str2,
                                        int len1, int len2, int i,
                                        int j, String res)
    {

        // If current string is part of the result
        if (res.Length == len1 + len2)
        {

            // Insert it into the set
            stringSet.Add(res);
            return;
        }

        // If character from str1 can be chosen
        if (i < len1)
            find_permutation(str1, str2, len1, len2, 
                             i + 1, j, res + str1[i]);

        // If character from str2 can be chosen
        if (j < len2)
            find_permutation(str1, str2, len1, len2,
                             i, j + 1, res + str2[j]);
    }

    // Function to print the generated
    // strings from the set
    public static void print_set()
    {
        foreach (String s in stringSet)
            Console.WriteLine(s);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str1 = "aa", str2 = "ab";
        int len1 = str1.Length;
        int len2 = str2.Length;

        find_permutation(str1, str2,
                         len1, len2, 0, 0, "");

        print_set();
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Set to store strings
    // and avoid duplicates
let stringSet = new Set();

// Recursive function to generate the required strings
function find_permutation(str1,str2,len1,len2,i,j,res)
{
    // If current string is part of the result
        if (res.length == len1 + len2)
        {

            // Insert it into the set
            stringSet.add(res);
            return;
        }

        // If character from str1 can be chosen
        if (i < len1)
            find_permutation(str1, str2, len1, len2, i + 1,
                                    j, res + str1[i]);

        // If character from str2 can be chosen
        if (j < len2)
            find_permutation(str1, str2, len1, len2, i, j + 1,
                                           res + str2[j]);
}

// Function to print the generated
    // strings from the set
function print_set()
{
    for(let s of stringSet.values())
    {
        document.write(s+"<br>");
    }
}

// Driver code
let str1 = "aa", str2 = "ab";
let len1 = str1.length;
let len2 = str2.length;

find_permutation(str1, str2, len1, len2, 0, 0, "");

print_set();

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
aaab
aaba
abaa
```