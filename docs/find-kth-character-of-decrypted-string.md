# 查找解密字符串的第 k 个字符|集合 1

> 原文:[https://www . geesforgeks . org/find-kth-解密字符串字符/](https://www.geeksforgeeks.org/find-kth-character-of-decrypted-string/)

给定一个编码字符串，其中子字符串的重复表示为子字符串，后跟子字符串的计数。例如，如果加密字符串为“ab2cd2”且 k=4，则输出将为“b”，因为解密字符串为“ababcdcd”，第 4 个字符为“b”。
**<u>注意:</u>** 加密子串的出现频率可以超过一位数。例如在“ab12c3”中，ab 重复 12 次。子字符串的频率中没有前导 0。
**例:**

```
Input: "a2b2c3", k = 5
Output: c
Decrypted string is "aabbccc"

Input : "ab4c2ed3", k = 9
Output : c
Decrypted string is "ababababccededed"

Input: "ab4c12ed3", k = 21
Output: e
Decrypted string is "ababababccccccccccccededed"
```

想法很简单。首先获取空的解密字符串，然后通过逐个读取子串及其频率来解压缩该字符串，并通过其频率将当前子串附加到解密字符串中。重复该过程，直到字符串结束，并打印解密字符串的第 K 个字符。

## C++

```
// C++ program to find K'th character in
// decrypted string
#include<bits/stdc++.h>
using namespace std;

// Function to find K'th character in Encoded String
char encodedChar(string str,int k)
{
    // expand string variable is used to
    // store final string after decompressing string str
    string expand = "";

    string temp;  // Current substring
    int freq = 0; // Count of current substring

    for (int i=0; str[i]!='\0'; )
    {
        temp = ""; // Current substring
        freq = 0; // count frequency of current substring

        // read characters until you find a number
        // or end of string
        while (str[i]>='a' && str[i]<='z')
        {
            // push character in temp
            temp.push_back(str[i]);
            i++;
        }

        // read number for how many times string temp
        // will be repeated in decompressed string
        while (str[i]>='1' && str[i]<='9')
        {
            // generating frequency of temp
            freq = freq*10 + str[i] - '0';
            i++;
        }

        // now append string temp into expand
        // equal to its frequency
        for (int j=1; j<=freq; j++)
            expand.append(temp);
    }

    // this condition is to handle the case
    // when string str is ended with alphabets
    // not with numeric value
    if (freq==0)
        expand.append(temp);

    return expand[k-1];
}

// Driver program to test the string
int main()
{
    string str = "ab4c12ed3";
    int k = 21;
    cout << encodedChar(str, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find K'th character in
// decrypted string
public class GFG {

    // Function to find K'th character in
    // Encoded String
    static char encodedChar(String str,int k)
    {
        // expand string variable is used to
        // store final string after decompressing
        // string str
        String expand = "";

        String temp = "";  // Current substring
        int freq = 0; // Count of current substring

        for (int i=0; i < str.length() ; )
        {
            temp = ""; // Current substring
            freq = 0; // count frequency of current
                      // substring

            // read characters until you find a number
            // or end of string
            while (i < str.length() && str.charAt(i)>='a'
                                && str.charAt(i)<='z')
            {
                // push character in temp
                temp += str.charAt(i);
                i++;
            }

            // read number for how many times string temp
            // will be repeated in decompressed string
            while (i < str.length() && str.charAt(i)>='1'
                                && str.charAt(i)<='9')
            {
                // generating frequency of temp
                freq = freq*10 + str.charAt(i) - '0';
                i++;
            }

            // now append string temp into expand
            // equal to its frequency
            for (int j=1; j<=freq; j++)
                 expand += temp;
        }

        // this condition is to handle the case
        // when string str is ended with alphabets
        // not with numeric value
        if (freq==0)
            expand += temp;

        return expand.charAt(k-1);
    }

    // Driver program to test the string
    public static void main(String args[])
    {
        String str = "ab4c12ed3";
        int k = 21;
        System.out.println(encodedChar(str, k));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to find K'th character
# in decrypted string

# Function to find K'th character
# in Encoded String
def encodedChar(str, k):

    # expand string variable is used
    # to store final string after
    # decompressing string str
    expand = ""

    # Current substring
    freq = 0 # Count of current substring
    i = 0
    while(i < len(str)):
        temp = "" # Current substring
        freq = 0 # count frequency of current substring

        # read characters until you find
        # a number or end of string
        while (i < len(str) and
               ord(str[i]) >= ord('a') and
               ord(str[i]) <= ord('z')):

            # push character in temp
            temp += str[i]
            i += 1

        # read number for how many times string temp
        # will be repeated in decompressed string
        while (i < len(str) and
               ord(str[i]) >= ord('1') and
               ord(str[i]) <= ord('9')):

            # generating frequency of temp
            freq = freq * 10 + ord(str[i]) - ord('0')
            i += 1

        # now append string temp into expand
        # equal to its frequency
        for j in range(1, freq + 1, 1):
            expand += temp

    # this condition is to handle the case
    # when string str is ended with alphabets
    # not with numeric value
    if (freq == 0):
        expand += temp

    return expand[k - 1]

# Driver Code
if __name__ == '__main__':
    str = "ab4c12ed3"
    k = 21
    print(encodedChar(str, k))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find K'th
// character in decrypted string
using System;

class GFG
{

    // Function to find K'th
    // character in Encoded String
    static char encodedChar(string str, int k)
    {
        // expand string variable is
        // used to store final string
        // after decompressing string str
        String expand = "";

        String temp = ""; // Current substring
        int freq = 0; // Count of current substring

        for (int i = 0; i < str.Length ; )
        {
            temp = ""; // Current substring
            freq = 0; // count frequency of current
                      // substring

            // read characters until you
            // find a number or end of string
            while (i < str.Length && str[i]>='a'
                                  && str[i]<='z')
            {
                // push character in temp
                temp += str[i];
                i++;
            }

            // read number for how many times
            // string temp will be repeated
            // in decompressed string
            while (i < str.Length && str[i] >= '1'
                                  && str[i] <= '9')
            {
                // generating frequency of temp
                freq = freq * 10 + str[i] - '0';
                i++;
            }

            // now append string temp into
            // expand equal to its frequency
            for (int j = 1; j <= freq; j++)
                expand += temp;
        }

        // this condition is to handle
        // the case when string str is
        // ended with alphabets not
        // with numeric value
        if (freq == 0)
            expand += temp;

        return expand[k - 1];
    }

    // Driver Code
    public static void Main()
    {
        string str = "ab4c12ed3";
        int k = 21;
        Console.Write(encodedChar(str, k));
    }
}

// This code is contributed
// by ChitraNayal
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

        // expand string variable is used to
        // store final string after decompressing
        // string str
        let expand = "";
        let temp = "";  // Current substring
        let freq = 0; // Count of current substring
        for (let i=0; i < str.length ; )
        {
            temp = ""; // Current substring
            freq = 0; // count frequency of current
                      // substring

            // read characters until you find a number
            // or end of string
            while (i < str.length && str[i].charCodeAt(0)>='a'.charCodeAt(0)
                                && str[i].charCodeAt(0)<='z'.charCodeAt(0))
            {
                // push character in temp
                temp += str[i];
                i++;
            }

            // read number for how many times string temp
            // will be repeated in decompressed string
            while (i < str.length && str[i].charCodeAt(0)>='1'.charCodeAt(0)
                                && str[i].charCodeAt(0)<='9'.charCodeAt(0))
            {
                // generating frequency of temp
                freq = freq*10 + str[i].charCodeAt(0) - '0'.charCodeAt(0);
                i++;
            }

            // now append string temp into expand
            // equal to its frequency
            for (let j=1; j<=freq; j++)
                 expand += temp;
        }

        // this condition is to handle the case
        // when string str is ended with alphabets
        // not with numeric value
        if (freq==0)
            expand += temp;

        return expand[k-1];
    }

    // Driver program to test the string
    let str = "ab4c12ed3";
    let k = 21;
    document.write(encodedChar(str, k));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
e
```

**练习:**上面的解决方案构建解码后的字符串来查找第 k 个字符。将解决方案扩展到在 O(1)个额外空间中工作。
[找到解密字符串的第 k 个字符| Set–2](https://www.geeksforgeeks.org/find-k-th-character-of-decrypted-string-set-2/)
本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿，团队 GeeksforGeeks 审核。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。