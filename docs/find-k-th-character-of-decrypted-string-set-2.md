# 查找解密字符串的第 k 个字符| Set–2

> 原文:[https://www . geesforgeks . org/find-k-th-字符解密字符串集-2/](https://www.geeksforgeeks.org/find-k-th-character-of-decrypted-string-set-2/)

给定一个编码字符串，其中子字符串的重复表示为子字符串，后跟子字符串的计数。例如，如果加密字符串为“ab2cd2”且 k=4，则输出将为“b”，因为解密字符串为“ababcdcd”，第 4 个字符为“b”。
**注意:**加密子串的出现频率可以超过一位数。例如在“ab12c3”中，ab 重复 12 次。子字符串的频率中没有前导 0。

**示例:**

```
Input:  "a2b2c3", k = 5
Output:  c
Decrypted string is "aabbccc"

Input:  "ab4c2ed3", k = 9
Output :  c
Decrypted string is "ababababccededed"
```

上一篇文章中讨论的解决方案需要额外的 O(n)空间。下面的帖子讨论了一个需要恒定空间的解决方案。逐步算法是:

1.  查找当前子字符串的长度。使用两个指针。在子串的开头固定一个指针，移动另一个指针，直到找不到一个数字。
2.  通过进一步移动第二个指针找到重复频率，直到没有找到字母表。
3.  如果子串是通过频率和它的原始长度相乘而重复的，则找到子串的长度。
4.  如果这个长度小于 k，那么所需的字符位于后面的子串中。从 k 中减去这个长度，以记录需要覆盖的字符数。
5.  如果长度小于或等于 k，则所需字符位于当前子串中。因为 k 是 1 索引的，所以把它减少 1，然后用原始子串长度取它的模。必选字符是从第一个指针指向的子串开始的第 k 个字符。

下面是上述方法的实现:

## C++

```
// C++ program to find K'th character in
// decrypted string
#include <bits/stdc++.h>
using namespace std;

// Function to find K'th character in
// Encoded String
char encodedChar(string str, int k)
{
    int i, j;

    int n = str.length();

    // To store length of substring
    int len;

    // To store length of substring when
    // it is repeated
    int num;

    // To store frequency of substring
    int freq;

    i = 0;

    while (i < n) {
        j = i;
        len = 0;
        freq = 0;

        // Find length of substring by
        // traversing the string until
        // no digit is found.
        while (j < n && isalpha(str[j])) {
            j++;
            len++;
        }

        // Find frequency of preceding substring.
        while (j < n && isdigit(str[j])) {
            freq = freq * 10 + (str[j] - '0');
            j++;
        }

        // Find length of substring when
        // it is repeated.
        num = freq * len;

        // If length of repeated substring is less than
        // k then required character is present in next
        // substring. Subtract length of repeated
        // substring from k to keep account of number of
        // characters required to be visited.
        if (k > num) {
            k -= num;
            i = j;
        }

        // If length of repeated substring is
        // more or equal to k then required
        // character lies in current substring.
        else {
            k--;
            k %= len;
            return str[i + k];
        }
    }

    // This is for the case when there
    // are no repetition in string.
    // e.g. str="abced".
    return str[k - 1];
}

// Driver Code
int main()
{
    string str = "abced";
    int k = 4;

    cout << encodedChar(str, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find K'th character in
// decrypted string
import java.util.*;

class GFG
{

// Function to find K'th character in
// Encoded String
static char encodedChar(char[] str, int k)
{
    int i, j;

    int n = str.length;

    // To store length of substring
    int len;

    // To store length of substring when
    // it is repeated
    int num;

    // To store frequency of substring
    int freq;

    i = 0;

    while (i < n)
    {
        j = i;
        len = 0;
        freq = 0;

        // Find length of substring by
        // traversing the string until
        // no digit is found.
        while (j < n && Character.isAlphabetic(str[j]))
        {
            j++;
            len++;
        }

        // Find frequency of preceding substring.
        while (j < n && Character.isDigit(str[j]))
        {
            freq = freq * 10 + (str[j] - '0');
            j++;
        }

        // Find length of substring when
        // it is repeated.
        num = freq * len;

        // If length of repeated substring is less than
        // k then required character is present in next
        // substring. Subtract length of repeated
        // substring from k to keep account of number of
        // characters required to be visited.
        if (k > num)
        {
            k -= num;
            i = j;
        }

        // If length of repeated substring is
        // more or equal to k then required
        // character lies in current substring.
        else
        {
            k--;
            k %= len;
            return str[i + k];
        }
    }

    // This is for the case when there
    // are no repetition in string.
    // e.g. str="abced".
    return str[k - 1];
}

// Driver Code
public static void main(String[] args)
{
    String str = "abced";
    int k = 4;

    System.out.println(encodedChar(str.toCharArray(), k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find K'th
# character in decrypted string

# Function to find K'th character
# in Encoded String
def encodedChar(string, k):

    n = len(string)

    i = 0
    while i < n:
        j = i
        length = 0
        freq = 0

        # Find length of substring by
        # traversing the string until
        # no digit is found.
        while j < n and string[j].isalpha():
            j += 1
            length += 1

        # Find frequency of preceding substring.
        while j < n and string[j].isdigit():
            freq = freq * 10 + int(string[j])
            j += 1

        # Find the length of the substring
        # when it is repeated.
        num = freq * length

        # If the length of the repeated substring
        # is less than k then required character
        # is present in next substring. Subtract
        # the length of repeated substring from
        # k to keep account of the number
        # of characters required to be visited.
        if k > num:
            k -= num
            i = j

        # If length of repeated substring is
        # more or equal to k then required
        # character lies in current substring.
        else:
            k -= 1
            k %= length
            return string[i + k]

    # This is for the case when there are no
    # repetition in string. e.g. str="abced".
    return string[k - 1]

# Driver Code
if __name__ == "__main__":

    string = "abced"
    k = 4

    print(encodedChar(string, k))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find K'th character in
// decrypted string
using System;

class GFG
{

// Function to find K'th character in
// Encoded String
static char encodedChar(char[] str, int k)
{
    int i, j;

    int n = str.Length;

    // To store length of substring
    int len;

    // To store length of substring when
    // it is repeated
    int num;

    // To store frequency of substring
    int freq;

    i = 0;

    while (i < n)
    {
        j = i;
        len = 0;
        freq = 0;

        // Find length of substring by
        // traversing the string until
        // no digit is found.
        while (j < n && char.IsLetter(str[j]))
        {
            j++;
            len++;
        }

        // Find frequency of preceding substring.
        while (j < n && char.IsDigit(str[j]))
        {
            freq = freq * 10 + (str[j] - '0');
            j++;
        }

        // Find length of substring when
        // it is repeated.
        num = freq * len;

        // If length of repeated substring is less than
        // k then required character is present in next
        // substring. Subtract length of repeated
        // substring from k to keep account of number of
        // characters required to be visited.
        if (k > num)
        {
            k -= num;
            i = j;
        }

        // If length of repeated substring is
        // more or equal to k then required
        // character lies in current substring.
        else
        {
            k--;
            k %= len;
            return str[i + k];
        }
    }

    // This is for the case when there
    // are no repetition in string.
    // e.g. str="abced".
    return str[k - 1];
}

// Driver Code
public static void Main(String[] args)
{
    String str = "abced";
    int k = 4;

    Console.WriteLine(encodedChar(str.ToCharArray(), k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find K'th character in
// decrypted string

// Function to find K'th character in
// Encoded String
function encodedChar(str, k)
{
    var i, j;

    var n = str.length;

    // To store length of substring
    var len;

    // To store length of substring when
    // it is repeated
    var num;

    // To store frequency of substring
    var freq;

    i = 0;

    while (i < n)
    {
        j = i;
        len = 0;
        freq = 0;

        // Find length of substring by
        // traversing the string until
        // no digit is found.
        while (j < n && str[j].match(/^[0-9a-z]+$/))
        {
            j++;
            len++;
        }

        // Find frequency of preceding substring.
        while (j < n && str[j].match(/^[0-9]+$/))
        {
            freq = freq * 10 + (str[j] - '0');
            j++;
        }

        // Find length of substring when
        // it is repeated.
        num = freq * len;

        // If length of repeated substring is less than
        // k then required character is present in next
        // substring. Subtract length of repeated
        // substring from k to keep account of number of
        // characters required to be visited.
        if (k > num)
        {
            k -= num;
            i = j;
        }

        // If length of repeated substring is
        // more or equal to k then required
        // character lies in current substring.
        else
        {
            k--;
            k %= len;
            return str[i + k];
        }
    }

    // This is for the case when there
    // are no repetition in string.
    // e.g. str="abced".
    return str[k - 1];
}

// Driver Code
var str = "abced";
var k = 4;

document.write(encodedChar(str, k));

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
e
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)