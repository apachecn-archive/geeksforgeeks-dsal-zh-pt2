# 包含给定字符 K 次的子串计数

> 原文:[https://www . geesforgeks . org/count-of-substrings-其中包含给定字符-k-times/](https://www.geeksforgeeks.org/count-of-substrings-which-contains-a-given-character-k-times/)

给定一个由数字字母、一个字符 **C** 和一个整数 **K** 组成的字符串，任务是找到包含字符 **C** 的可能子字符串的数量，精确到 **K** 次。

**示例:**

```
Input : str = "212", c = '2', k = 1 
Output : 4
Possible substrings are {"2", "21", "12", "2"}
that contains 2 exactly 1 time.

Input  : str = "55555", c = '5', k = 4
Output : 2
Possible substrings are {"5555", "5555"} 
that contains 5 exactly 4 times
```

**天真方法:**一个简单的解决方法是生成字符串的所有子串，并计算给定字符恰好出现 k 次的子串数量。

这个解的时间复杂度是 O(N <sup>2</sup> )，其中 N 是字符串的长度。

**有效方法:**一种有效的解决方案是使用滑动窗口技术。找到包含字符 C 的子字符串，从字符 C 开始精确 K 次。计算子字符串两边的字符数。将计数相乘，得到给定子串的可能子串数

下面是上述方法的实现:

## C++

```
// C++ program to count the number of substrings
// which contains the character C exactly K times

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of substrings
// which contains the character C exactly K times
int countSubString(string s, char c, int k)
{
    // left and right counters for characters on
    // both sides of substring window
    int leftCount = 0, rightCount = 0;

    // left and right pointer on both sides
    // of substring window
    int left = 0, right = 0;

    // initialize the frequency
    int freq = 0;

    // result and length of string
    int result = 0, len = s.length();

    // initialize the left pointer
    while (s[left] != c && left < len) {
        left++;
        leftCount++;
    }

    // initialize the right pointer
    right = left + 1;
    while (freq != (k - 1) && (right - 1) < len) {
        if (s[right] == c)
            freq++;
        right++;
    }

    // traverse all the window substrings
    while (left < len && (right - 1) < len) {

        // counting the characters on leftSide
        // of substring window
        while (s[left] != c && left < len) {
            left++;
            leftCount++;
        }

        // counting the characters on rightSide of
        // substring window
        while (right < len && s[right] != c) {
            if (s[right] == c)
                freq++;
            right++;
            rightCount++;
        }

        // Add the possible substrings on both
        // sides to result
        result = result + (leftCount + 1) * (rightCount + 1);

        // Setting the frequency for next
        // substring window
        freq = k - 1;

        // reset the left, right counters
        leftCount = 0;
        rightCount = 0;

        left++;
        right++;
    }

    return result;
}

// Driver code
int main()
{
    string s = "3123231";
    char c = '3';
    int k = 2;

    cout << countSubString(s, c, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of substrings
// which contains the character C exactly K times
class GFG
{

    // Function to count the number of substrings
    // which contains the character C exactly K times
    static int countSubString(String s, char c, int k)
    {
        // left and right counters for characters on
        // both sides of substring window
        int leftCount = 0, rightCount = 0;

        // left and right pointer on both sides
        // of substring window
        int left = 0, right = 0;

        // initialize the frequency
        int freq = 0;

        // result and length of string
        int result = 0, len = s.length();

        // initialize the left pointer
        while (s.charAt(left) != c && left < len)
        {
            left++;
            leftCount++;
        }

        // initialize the right pointer
        right = left + 1;
        while (freq != (k - 1) && (right - 1) < len)
        {
            if (s.charAt(right) == c)
            {
                freq++;
            }
            right++;
        }

        // traverse all the window substrings
        while (left < len && (right - 1) < len)
        {

            // counting the characters on leftSide
            // of substring window
            while (s.charAt(left) != c && left < len)
            {
                left++;
                leftCount++;
            }

            // counting the characters on rightSide of
            // substring window
            while (right < len && s.charAt(right) != c)
            {
                if (s.charAt(right) == c)
                {
                    freq++;
                }
                right++;
                rightCount++;
            }

            // Add the possible substrings on both
            // sides to result
            result = result + (leftCount + 1) * (rightCount + 1);

            // Setting the frequency for next
            // substring window
            freq = k - 1;

            // reset the left, right counters
            leftCount = 0;
            rightCount = 0;

            left++;
            right++;
        }

        return result;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "3123231";
        char c = '3';
        int k = 2;

        System.out.println(countSubString(s, c, k));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to count the number of substrings
# which contains the character C exactly K times

# Function to count the number of substrings
# which contains the character C exactly K times
def countSubString(s, c, k):

    # left and right counters for characters
    # on both sides of subwindow
    leftCount = 0
    rightCount = 0

    # left and right pointer on both sides
    # of subwindow
    left = 0
    right = 0

    # Initialize the frequency
    freq = 0

    # result and Length of string
    result = 0
    Len = len(s)

    # initialize the left pointer
    while (s[left] != c and left < Len):
        left += 1
        leftCount += 1

    # initialize the right pointer
    right = left + 1
    while (freq != (k - 1) and (right - 1) < Len):
        if (s[right] == c):
            freq += 1
        right += 1

    # traverse all the window substrings
    while (left < Len and (right - 1) < Len):

        # counting the characters on leftSide
        # of subwindow
        while (s[left] != c and left < Len):
            left += 1
            leftCount += 1

        # counting the characters on rightSide of
        # subwindow
        while (right < Len and s[right] != c):
            if (s[right] == c):
                freq += 1
            right += 1
            rightCount += 1

        # Add the possible substrings on both
        # sides to result
        result = (result + (leftCount + 1) *
                           (rightCount + 1))

        # Setting the frequency for next
        # subwindow
        freq = k - 1

        # reset the left, right counters
        leftCount = 0
        rightCount = 0

        left += 1
        right += 1

    return result

# Driver code
s = "3123231"
c = '3'
k = 2

print(countSubString(s, c, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to count the number of substrings
// which contains the character C exactly K times
using System;

class GFG
{

    // Function to count the number of substrings
    // which contains the character C exactly K times
    static int countSubString(string s, char c, int k)
    {
        // left and right counters for characters on
        // both sides of substring window
        int leftCount = 0, rightCount = 0;

        // left and right pointer on both sides
        // of substring window
        int left = 0, right = 0;

        // initialize the frequency
        int freq = 0;

        // result and length of string
        int result = 0, len = s.Length;

        // initialize the left pointer
        while (s[left] != c && left < len)
        {
            left++;
            leftCount++;
        }

        // initialize the right pointer
        right = left + 1;
        while (freq != (k - 1) && (right - 1) < len)
        {
            if (s[right] == c)
                freq++;
            right++;
        }

        // traverse all the window substrings
        while (left < len && (right - 1) < len)
        {

            // counting the characters on leftSide
            // of substring window
            while (s[left] != c && left < len)
            {
                left++;
                leftCount++;
            }

            // counting the characters on rightSide of
            // substring window
            while (right < len && s[right] != c)
            {
                if (s[right] == c)
                    freq++;
                right++;
                rightCount++;
            }

            // Add the possible substrings on both
            // sides to result
            result = result + (leftCount + 1) * (rightCount + 1);

            // Setting the frequency for next
            // substring window
            freq = k - 1;

            // reset the left, right counters
            leftCount = 0;
            rightCount = 0;

            left++;
            right++;
        }

        return result;
    }

    // Driver code
    static public void Main ()
    {
        string s = "3123231";
        char c = '3';
        int k = 2;

        Console.WriteLine(countSubString(s, c, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to count the number of substrings
// which contains the character C exactly K times

// Function to count the number of substrings
// which contains the character C exactly K times
function countSubString(s, c, k)
{

    // left and right counters for characters
    // on both sides of substring window
    var leftCount = 0,
    rightCount = 0;

    // left and right pointer on both
    // sides of substring window
    var left = 0,
    right = 0;

    // Initialize the frequency
    var freq = 0;

    // Result and length of string
    var result = 0,
    len = s.length;

    // Initialize the left pointer
    while (s[left] !== c && left < len)
    {
        left++;
        leftCount++;
    }

    // Initialize the right pointer
    right = left + 1;

    while (freq !== k - 1 && right - 1 < len)
    {
        if (s[right] === c) freq++;
            right++;
    }

    // Traverse all the window substrings
    while (left < len && right - 1 < len)
    {

        // Counting the characters on leftSide
        // of substring window
        while (s[left] !== c && left < len)
        {
            left++;
            leftCount++;
        }

        // Counting the characters on rightSide of
        // substring window
        while (right < len && s[right] !== c)
        {
            if (s[right] === c)
                freq++;

            right++;
            rightCount++;
        }

        // Add the possible substrings on both
        // sides to result
        result = result + (leftCount + 1) *
                         (rightCount + 1);

        // Setting the frequency for next
        // substring window
        freq = k - 1;

        // Reset the left, right counters
        leftCount = 0;
        rightCount = 0;

        left++;
        right++;
    }
    return result;
}

// Driver code
var s = "3123231";
var c = "3";
var k = 2;

document.write(countSubString(s, c, k));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
8
```

**时间复杂度** : O(N)