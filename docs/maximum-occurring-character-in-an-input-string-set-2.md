# 输入字符串中出现的最大字符数| Set-2

> 原文:[https://www . geesforgeks . org/输入字符串中出现最多的字符集-2/](https://www.geeksforgeeks.org/maximum-occurring-character-in-an-input-string-set-2/)

给定包含小写字符的字符串。任务是打印输入字符串中出现最多的字符。如果两个或两个以上的字符出现相同的次数，则打印字典顺序(按字母顺序)最低的(第一个)字符。
**例:**

> **输入:**测试样本
> **输出:**e
> ‘t’、‘e’和‘s’出现 2 次，但‘e’是字典上最小的字符。
> **输入:**样本程序
> **输出:** a

在[之前的](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)文章中，如果出现的字符超过了最大次数，则返回任意字符。在这篇文章中，所有字符中字典最小的字符被返回。
**方法:**声明一个**freq【26】**数组，用作哈希表来存储输入字符串中每个字符的频率。迭代字符串，增加每个字符的 *freq[s[i]]* 的数量。从左到右遍历 **freq[]** 数组，跟踪到目前为止出现频率最高的字符。freq[i]处的值代表字符(i + 'a ')的频率。
以下是上述方法的实施:

## C++

```
// C++ implementation to find
// the maximum occurring character in
// an input string which is lexicographically first
#include <bits/stdc++.h>
using namespace std;

// function to find the maximum occurring character in
// an input string which is lexicographically first
char getMaxOccurringChar(char str[])
{
    // freq[] used as hash table
    int freq[26] = { 0 };

    // to store maximum frequency
    int max = -1;

    // to store the maximum occurring character
    char result;

    // length of 'str'
    int len = strlen(str);

    // get frequency of each character of 'str'
    for (int i = 0; i < len; i++)
        freq[str[i] - 'a']++;

    // for each character, where character is obtained by
    // (i + 'a') check whether it is the maximum character
    // so far and accodingly update 'result'
    for (int i = 0; i < 26; i++)
        if (max < freq[i]) {
            max = freq[i];
            result = (char)(i + 'a');
        }

    // maximum occurring character
    return result;
}

// Driver Code
int main()
{
    char str[] = "sample program";
    cout << "Maximum occurring character = "
         << getMaxOccurringChar(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the maximum occurring character in
// an input string which is lexicographically first

class GFG {

// function to find the maximum occurring character in
// an input string which is lexicographically first
    static char getMaxOccurringChar(char str[]) {
        // freq[] used as hash table
        int freq[] = new int[26];

        // to store maximum frequency
        int max = -1;

        // to store the maximum occurring character
        char result = 0;

        // length of 'str'
        int len = str.length;

        // get frequency of each character of 'str'
        for (int i = 0; i < len; i++) {
            if (str[i] != ' ') {
                freq[str[i] - 'a']++;
            }
        }

        // for each character, where character is obtained by
        // (i + 'a') check whether it is the maximum character
        // so far and accodingly update 'result'
        for (int i = 0; i < 26; i++) {
            if (max < freq[i]) {
                max = freq[i];
                result = (char) (i + 'a');
            }
        }

        // maximum occurring character
        return result;
    }

// Driver Code
    public static void main(String[] args) {
        char str[] = "sample program".toCharArray();
        System.out.println("Maximum occurring character = "
                + getMaxOccurringChar(str));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to find the
# maximum occurring character in an input
# string which is lexicographically first

# function to find the maximum occurring
# character in an input string which is
# lexicographically first
def getMaxOccurringChar(str):

    # freq[] used as hash table
    freq = [0 for i in range(100)]

    # to store maximum frequency
    max = -1

    # to store the maximum occurring
    # character length of 'str'
    len__ = len(str)

    # get frequency of each character of 'str'
    for i in range(0, len__, 1):
        freq[ord(str[i]) - ord('a')] += 1

    # for each character, where character
    # is obtained by (i + 'a') check whether
    # it is the maximum character so far and
    # accodingly update 'result'
    for i in range(26):
        if (max < freq[i]):
            max = freq[i]
            result = chr(ord('a') + i)

    # maximum occurring character
    return result

# Driver Code
if __name__ == '__main__':
    str = "sample program"
    print("Maximum occurring character =",
                 getMaxOccurringChar(str))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation to find
// the maximum occurring character in
// an input string which is lexicographically first

using System;
class GFG {

// function to find the maximum occurring character in
// an input string which is lexicographically first
    static char getMaxOccurringChar(string str) {
        // freq[] used as hash table
        int[] freq = new int[26];

        // to store maximum frequency
        int max = -1;

        // to store the maximum occurring character
        char result = (char)0;

        // length of 'str'
        int len = str.Length;

        // get frequency of each character of 'str'
        for (int i = 0; i < len; i++) {
            if (str[i] != ' ') {
                freq[str[i] - 'a']++;
            }
        }

        // for each character, where character is obtained by
        // (i + 'a') check whether it is the maximum character
        // so far and accodingly update 'result'
        for (int i = 0; i < 26; i++) {
            if (max < freq[i]) {
                max = freq[i];
                result = (char) (i + 'a');
            }
        }

        // maximum occurring character
        return result;
    }

// Driver Code
    public static void Main() {
        string str = "sample program";
        Console.WriteLine("Maximum occurring character = "
                + getMaxOccurringChar(str));
    }
}
```

## java 描述语言

```
<script>
// Javascript implementation to find
// the maximum occurring character in
// an input string which is lexicographically first

    // function to find the maximum occurring character in
    // an input string which is lexicographically first
    function getMaxOccurringChar(str)
    {
        // freq[] used as hash table
        let freq = new Array(26);
        for(let i=0;i<freq.length;i++)
        {
            freq[i]=0;
        }

        // to store maximum frequency
        let max = -1;

        // to store the maximum occurring character
        let result = 0;

        // length of 'str'
        let len = str.length;

        // get frequency of each character of 'str'
        for (let i = 0; i < len; i++) {
            if (str[i] != ' ') {
                freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
            }
        }

        // for each character, where character is obtained by
        // (i + 'a') check whether it is the maximum character
        // so far and accodingly update 'result'
        for (let i = 0; i < 26; i++) {
            if (max < freq[i]) {
                max = freq[i];
                result =  String.fromCharCode(i + 'a'.charCodeAt(0));
            }
        }

        // maximum occurring character
        return result;
    }

    // Driver Code
    let str="sample program".split("");
    document.write("Maximum occurring character = "
                + getMaxOccurringChar(str));

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
Maximum occurring character = a
```

**时间复杂度:** O(n)。
**辅助空间:** O(1)。
**来源:** [佩刀面试经验|第二集](https://www.geeksforgeeks.org/sabre-interview-experience-set-2-for-associate-software-developer/)