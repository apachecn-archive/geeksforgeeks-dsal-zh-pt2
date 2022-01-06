# 将一个字符串的每个字符映射到另一个字符串，这样所有出现的字符都映射到同一个字符

> 原文:[https://www . geeksforgeeks . org/将一个字符串中的每个字符映射到另一个字符串，以便所有出现的字符都映射到同一个字符/](https://www.geeksforgeeks.org/map-every-character-of-one-string-to-another-such-that-all-occurrences-are-mapped-to-the-same-character/)

给定两个字符串 **s1** 和 **s2** ，任务是检查第一个字符串的字符是否可以与第二个字符串的字符映射，这样如果一个字符 **ch1** 与某个字符 **ch2** 映射，那么所有出现的 **ch1** 将只与两个字符串的 **ch2** 映射。

**示例:**

> **输入:**S1 =“axx”，s2 =“CBC”
> **输出:**是
> S1 中的‘a’可以映射到 s2 中的‘b’
> S1 中的‘x’可以映射到 S2 中的‘c’。
> 
> **输入:**S1 =“a”，S2 =“df”
> T3】输出:否

**方法:**如果两个字符串的长度不相等，那么字符串不能被映射，否则创建两个频率数组 **freq1[]** 和 **freq2[]** ，它们将分别存储给定字符串的所有字符的频率 **s1** 和 **s2** 。现在，对于 **freq1[]** 中的每个非零值，在 **freq2[]** 中找到一个相等的值。如果 **freq1[]** 中的所有非零值都可以映射到 **freq2[]** 中的某个值，那么答案是可能的，否则不是。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 26

// Function that returns true if the mapping is possible
bool canBeMapped(string s1, int l1, string s2, int l2)
{

    // Both the strings are of un-equal lengths
    if (l1 != l2)
        return false;

    // To store the frequencies of the
    // characters in both the string
    int freq1[MAX] = { 0 };
    int freq2[MAX] = { 0 };

    // Update frequencies of the characters
    for (int i = 0; i < l1; i++)
        freq1[s1[i] - 'a']++;
    for (int i = 0; i < l2; i++)
        freq2[s2[i] - 'a']++;

    // For every character of s1
    for (int i = 0; i < MAX; i++) {

        // If current character is
        // not present in s1
        if (freq1[i] == 0)
            continue;
        bool found = false;

        // Find a character in s2 that has frequency
        // equal to the current character's
        // frequency in s1
        for (int j = 0; j < MAX; j++) {

            // If such character is found
            if (freq1[i] == freq2[j]) {

                // Set the frequency to -1 so that
                // it doesn't get picked again
                freq2[j] = -1;

                // Set found to true
                found = true;
                break;
            }
        }

        // If there is no character in s2
        // that could be mapped to the
        // current character in s1
        if (!found)
            return false;
    }

    return true;
}

// Driver code
int main()
{
    string s1 = "axx";
    string s2 = "cbc";
    int l1 = s1.length();
    int l2 = s2.length();

    if (canBeMapped(s1, l1, s2, l2))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int MAX = 26;

    // Function that returns true if the mapping is possible
    public static boolean canBeMapped(String s1, int l1,
                                        String s2, int l2)
    {

        // Both the strings are of un-equal lengths
        if (l1 != l2)
            return false;

        // To store the frequencies of the
        // characters in both the string
        int[] freq1 = new int[MAX];
        int[] freq2 = new int[MAX];

        // Update frequencies of the characters
        for (int i = 0; i < l1; i++)
            freq1[s1.charAt(i) - 'a']++;
        for (int i = 0; i < l2; i++)
            freq2[s2.charAt(i) - 'a']++;

        // For every character of s1
        for (int i = 0; i < MAX; i++) {

            // If current character is
            // not present in s1
            if (freq1[i] == 0)
                continue;
            boolean found = false;

            // Find a character in s2 that has frequency
            // equal to the current character's
            // frequency in s1
            for (int j = 0; j < MAX; j++)
            {

                // If such character is found
                if (freq1[i] == freq2[j])
                {

                    // Set the frequency to -1 so that
                    // it doesn't get picked again
                    freq2[j] = -1;

                    // Set found to true
                    found = true;
                    break;
                }
            }

            // If there is no character in s2
            // that could be mapped to the
            // current character in s1
            if (!found)
                return false;
        }

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s1 = "axx";
        String s2 = "cbc";
        int l1 = s1.length();
        int l2 = s2.length();

        if (canBeMapped(s1, l1, s2, l2))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

MAX = 26

# Function that returns true if the mapping is possible
def canBeMapped(s1, l1, s2, l2):
    # Both the strings are of un-equal lengths
    if (l1 != l2):
        return False

    # To store the frequencies of the
    # characters in both the string
    freq1 = [0 for i in range(MAX)]
    freq2 = [0 for i in range(MAX)]

    # Update frequencies of the characters
    for i in range(l1):
        freq1[ord(s1[i]) - ord('a')] += 1
    for i in range(l2):
        freq2[ord(s2[i]) - ord('a')] += 1

    # For every character of s1
    for i in range(MAX):
        # If current character is
        # not present in s1
        if (freq1[i] == 0):
            continue
        found = False

        # Find a character in s2 that has frequency
        # equal to the current character's
        # frequency in s1
        for j in range(MAX):
            # If such character is found
            if (freq1[i] == freq2[j]):
                # Set the frequency to -1 so that
                # it doesn't get picked again
                freq2[j] = -1

                # Set found to true
                found = True
                break

        # If there is no character in s2
        # that could be mapped to the
        # current character in s1
        if (found==False):
            return False

    return True

# Driver code
if __name__ == '__main__':
    s1 = "axx"
    s2 = "cbc"
    l1 = len(s1)
    l2 = len(s2)

    if (canBeMapped(s1, l1, s2, l2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MAX = 26;

    // Function that returns true
    // if the mapping is possible
    public static Boolean canBeMapped(String s1, int l1,
                                      String s2, int l2)
    {

        // Both the strings are of un-equal lengths
        if (l1 != l2)
            return false;

        // To store the frequencies of the
        // characters in both the string
        int[] freq1 = new int[MAX];
        int[] freq2 = new int[MAX];

        // Update frequencies of the characters
        for (int i = 0; i < l1; i++)
            freq1[s1[i] - 'a']++;
        for (int i = 0; i < l2; i++)
            freq2[s2[i] - 'a']++;

        // For every character of s1
        for (int i = 0; i < MAX; i++)
        {

            // If current character is
            // not present in s1
            if (freq1[i] == 0)
                continue;
            Boolean found = false;

            // Find a character in s2 that has frequency
            // equal to the current character's
            // frequency in s1
            for (int j = 0; j < MAX; j++)
            {

                // If such character is found
                if (freq1[i] == freq2[j])
                {

                    // Set the frequency to -1 so that
                    // it doesn't get picked again
                    freq2[j] = -1;

                    // Set found to true
                    found = true;
                    break;
                }
            }

            // If there is no character in s2
            // that could be mapped to the
            // current character in s1
            if (!found)
                return false;
        }
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s1 = "axx";
        String s2 = "cbc";
        int l1 = s1.Length;
        int l2 = s2.Length;

        if (canBeMapped(s1, l1, s2, l2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 26;

// Function that returns true if the mapping is possible
function canBeMapped(s1, l1, s2, l2)
{

    // Both the strings are of un-equal lengths
    if (l1 != l2)
        return false;

    // To store the frequencies of the
    // characters in both the string
    var freq1 = Array(MAX).fill(0);
    var freq2 = Array(MAX).fill(0);

    // Update frequencies of the characters
    for (var i = 0; i < l1; i++)
        freq1[s1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    for (var i = 0; i < l2; i++)
        freq2[s2[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // For every character of s1
    for (var i = 0; i < MAX; i++) {

        // If current character is
        // not present in s1
        if (freq1[i] == 0)
            continue;
        var found = false;

        // Find a character in s2 that has frequency
        // equal to the current character's
        // frequency in s1
        for (var j = 0; j < MAX; j++) {

            // If such character is found
            if (freq1[i] == freq2[j]) {

                // Set the frequency to -1 so that
                // it doesn't get picked again
                freq2[j] = -1;

                // Set found to true
                found = true;
                break;
            }
        }

        // If there is no character in s2
        // that could be mapped to the
        // current character in s1
        if (!found)
            return false;
    }

    return true;
}

// Driver code
var s1 = "axx";
var s2 = "cbc";
var l1 = s1.length;
var l2 = s2.length;
if (canBeMapped(s1, l1, s2, l2))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```