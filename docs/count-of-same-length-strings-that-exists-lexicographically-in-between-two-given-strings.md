# 两个给定字符串之间存在的相同长度字符串的计数

> 原文:[https://www . geeksforgeeks . org/相同长度字符串的计数存在于两个给定字符串之间的词典中/](https://www.geeksforgeeks.org/count-of-same-length-strings-that-exists-lexicographically-in-between-two-given-strings/)

给定两个长度为 **L** 的字符串 **S1** 和 **S2** ，任务是计算长度为 L 的字符串的数量，这些字符串存在于 S1 和 S2 之间，在词典上大于 S1，但小于 S2。
**举例:**

> **输入:**S1 =【b】、S2 =【f】
> **输出:** 3
> **解释:**
> 这是 3 个按字典顺序位于 S1 和 S2 之间的字符串，即“c”、“d”&【e】
> **输入:**S1 =【aby】，S2 =【ace】
> **输出:** 5
> **解释:**T18

**进场:**

1.  First, find out the number of strings lexicographically smaller than the first string S1, as:

    ```
    Let the String S1 of length L 
    be represented as c<sub>0c1c2...cL-1</sub>
    where ci is the character in S1 at index i

    Therefore, To get the number of strings less than S1,
    we will calculate it as 
    N(S1) = (number of letters less than c0 * 26L-1)
          + (number of letters less than c1 * 26L-2)
          + (number of letters less than c2 * 26L-3)
          +  ... 
          + (number of letters less than cL-2 * 26)
          + (number of letters less than cL-1)
    ```

    **例如:**

    ```
    Let S1 = "cbd"

    Number of strings less than S1
    N(S1) = (number of letters less than 'c' * 262)
          + (number of letters less than 'b' * 26)
          + (number of letters less than 'd')

    N(S1) = (2 * 26 * 26) + (1 * 26) + (3) 
          = 1352 + 26 + 3 = 1381.
    ```

2.  同样，找出字典上比 S2 小的字符串。
3.  然后只要找出上面两个值的区别，就可以得到字典上大于 S1 但小于 S2 的字符串数。

以下是上述方法的实现:

## C++

```
    // C++ program to find the count of
// same length Strings that exists lexicographically
// in between two given Strings

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of strings less
// than given string lexicographically
int LexicoLesserStrings(string s)
{
    int count = 0;
    int len;

    // Find length of string s
    len = s.size();

    // Looping over the string characters and
    // finding strings less than that character
    for (int i = 0; i < len; i++) {
        count += (s[i] - 'a')
                * pow(26, len - i - 1);
    }

    return count;
}

// Function to find the count of
// same length Strings that exists
// lexicographically in between two given Strings
int countString(string S1, string S2)
{
    int countS1, countS2, totalString;

    // Count string less than S1
    countS1 = LexicoLesserStrings(S1);

    // Count string less than S2
    countS2 = LexicoLesserStrings(S2);

    // Total strings between S1 and S2 would
    // be difference between the counts - 1
    totalString = countS2 - countS1 - 1;

    // If S1 is lexicographically greater
    // than S2 then return 0, otherwise return
    // the value of totalString
    return (totalString < 0 ? 0 : totalString);
}

// Driver code
int main()
{
    string S1, S2;
    S1 = "cda";
    S2 = "cef";

    cout << countString(S1, S2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of same length
// Strings that exists lexicographically
// in between two given Strings
import java.util.*;

class GFG{

// Function to find the count of strings less
// than given string lexicographically
static int LexicoLesserStrings(String s)
{
    int count = 0;
    int len;

    // Find length of string s
    len = s.length();

    // Looping over the string characters and
    // finding strings less than that character
    for(int i = 0; i < len; i++)
    {
        count += (s.charAt(i) - 'a') *
                Math.pow(26, len - i - 1);
    }
    return count;
}

// Function to find the count of
// same length Strings that exists
// lexicographically in between two
// given Strings
static int countString(String S1, String S2)
{
    int countS1, countS2, totalString;

    // Count string less than S1
    countS1 = LexicoLesserStrings(S1);

    // Count string less than S2
    countS2 = LexicoLesserStrings(S2);

    // Total strings between S1 and S2 would
    // be difference between the counts - 1
    totalString = countS2 - countS1 - 1;

    // If S1 is lexicographically greater
    // than S2 then return 0, otherwise return
    // the value of totalString
    return (totalString < 0 ? 0 : totalString);
}

// Driver code
public static void main(String args[])
{
    String S1, S2;
    S1 = "cda";
    S2 = "cef";

    System.out.println(countString(S1, S2));
}
}

// This code is contributed by apurva raj
```

## 蟒蛇 3

```
# Python3 program to find the count of same
# length Strings that exists lexicographically
# in between two given Strings

# Function to find the count of strings less
# than given string lexicographically
def LexicoLesserStrings(s):

    count = 0

    # Find length of string s
    length = len(s)

    # Looping over the string characters and
    # finding strings less than that character
    for i in range(length):
        count += ((ord(s[i]) - ord('a')) *
                pow(26, length - i - 1))

    return count

# Function to find the count of
# same length Strings that exists
# lexicographically in between two
# given Strings
def countString(S1, S2):

    # Count string less than S1
    countS1 = LexicoLesserStrings(S1)

    # Count string less than S2
    countS2 = LexicoLesserStrings(S2)

    # Total strings between S1 and S2 would
    # be difference between the counts - 1
    totalString = countS2 - countS1 - 1;

    # If S1 is lexicographically greater
    # than S2 then return 0, otherwise return
    # the value of totalString
    return (0 if totalString < 0 else totalString)

# Driver code
S1 = "cda";
S2 = "cef";

print(countString(S1, S2))

# This code is contributed by apurva raj
```

## C#

```
// C# program to find the count of same length
// Strings that exists lexicographically
// in between two given Strings
using System;

class GFG{

// Function to find the count of strings less
// than given string lexicographically
static int LexicoLesserStrings(String s)
{
    int count = 0;
    int len;

    // Find length of string s
    len = s.Length;

    // Looping over the string characters and
    // finding strings less than that character
    for(int i = 0; i < len; i++)
    {
        count += ((s[i] - 'a') *
                (int)Math.Pow(26, len - i - 1));
    }
    return count;
}

// Function to find the count of
// same length Strings that exists
// lexicographically in between two
// given Strings
static int countString(String S1, String S2)
{
    int countS1, countS2, totalString;

    // Count string less than S1
    countS1 = LexicoLesserStrings(S1);

    // Count string less than S2
    countS2 = LexicoLesserStrings(S2);

    // Total strings between S1 and S2 would
    // be difference between the counts - 1
    totalString = countS2 - countS1 - 1;

    // If S1 is lexicographically greater
    // than S2 then return 0, otherwise return
    // the value of totalString
    return (totalString < 0 ? 0 : totalString);
}

// Driver code
public static void Main()
{
    String S1, S2;
    S1 = "cda";
    S2 = "cef";

    Console.Write(countString(S1, S2));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
      // JavaScript program to find the count of
      // same length Strings that exists lexicographically
      // in between two given Strings

      // Function to find the count of strings less
      // than given string lexicographically
      function LexicoLesserStrings(s) {
        var count = 0;
        var len;

        // Find length of string s
        len = s.length;

        // Looping over the string characters and
        // finding strings less than that character
        for (var i = 0; i < len; i++) {
          count +=
            (s[i].charCodeAt(0) - "a".charCodeAt(0)) *
            Math.pow(26, len - i - 1);
        }

        return count;
      }

      // Function to find the count of
      // same length Strings that exists
      // lexicographically in between two given Strings
      function countString(S1, S2) {
        var countS1, countS2, totalString;

        // Count string less than S1
        countS1 = LexicoLesserStrings(S1);

        // Count string less than S2
        countS2 = LexicoLesserStrings(S2);

        // Total strings between S1 and S2 would
        // be difference between the counts - 1
        totalString = countS2 - countS1 - 1;

        // If S1 is lexicographically greater
        // than S2 then return 0, otherwise return
        // the value of totalString
        return totalString < 0 ? 0 : totalString;
      }

      // Driver code
      var S1, S2;
      S1 = "cda";
      S2 = "cef";

      document.write(countString(S1, S2));
</script>

```

**Output:** 

```
30
```

**性能分析:**
**时间复杂度**:在上面的方法中，我们是循环长度为 N 的两个字符串，因此需要 **O(N)** 的时间，其中 **N** 是每个字符串的长度。
**辅助空间复杂度**:和上述方法一样，没有使用额外的空间，因此辅助空间复杂度为 **O(1)** 。