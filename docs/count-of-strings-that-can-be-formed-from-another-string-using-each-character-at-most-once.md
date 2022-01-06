# 使用每个字符最多一次由另一个字符串组成的字符串的数量

> 原文:[https://www . geesforgeks . org/最多使用一次每个字符从另一个字符串形成的字符串数/](https://www.geeksforgeeks.org/count-of-strings-that-can-be-formed-from-another-string-using-each-character-at-most-once/)

给定两个字符串 str1 和 str2，任务是使用 *str1* 的字符打印 *str2* 可以形成的次数。然而，在 str1 的任何索引处的字符在 str2 的形成中只能使用一次。

**示例:**

> **输入:**str1 =“arajhupoot”，str 2 =“Raj put”
> T3】输出: 1
> **说明:**
> str2 只能用 str 1 的字符组成一次。
> 
> **输入:**str 1 =“foreeksgeksegg”，str2 =“极客”
> T3】输出: 2

**方法:**由于问题限制只能使用一次 str1 的字符组成 str2。如果一个字符已被用于形成一个 str2，则不能用于形成另一个 str2。str2 的每个字符都必须出现在 str1 中，至少形成一个 str1。如果 str2 的所有字符都已经出现在 str1 中，那么在 str1 中出现次数最少的字符将是可以使用 str1 的字符一次形成的 str2 的数量。以下是步骤:

*   创建一个存储字符串中每个字符出现次数的散列数组。
*   迭代 str2 的所有字符，找出 str1 中每个字符出现次数最少的地方。
*   返回最小出现次数作为答案。

下面是上述方法的实现:

## C++

```
/// C++ program to print the number of times
// str2 can be formed from str1 using the
// characters of str1 only once
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of str2
// that can be formed using characters of str1
int findNumberOfTimes(string str1, string str2)
{
    int freq[26] = { 0 };
    int freq2[26] = { 0 };

    int l1 = str1.length();
    int l2 = str2.length();
    // iterate and mark the frequencies of
    // all characters in str1
    for (int i = 0; i < l1; i++)
        freq[str1[i] - 'a'] += 1;

  for (int i = 0; i < l2; i++)
        freq2[str2[i] - 'a'] += 1;

    int count = INT_MAX;

    // find the minimum frequency of
    // every character in str1
    for (int i = 0; i < l2; i++)
    {
      if(freq2[str2[i]-'a']!=0)
      count = min(count, freq[str2[i] - 'a']/freq2[str2[i]-'a']);
    }
    return count;
}

// Driver Code
int main()
{
    string str1 = "foreeksgekseg";
    string str2 = "geeks";

    cout << findNumberOfTimes(str1, str2)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the number of times
// str2 can be formed from str1 using the
// characters of str1 only once

class GFG {

// Function to find the number of str2
// that can be formed using characters of str1
    static int findNumberOfTimes(String str1, String str2)
    {
        int freq[] = new int[26];
        int freq2[] = new int[26];

        int l1 = str1.length();

        // iterate and mark the frequencies of
        // all characters in str1
        for (int i = 0; i < l1; i++)
        {
            freq[str1.charAt(i) - 'a'] += 1;
        }
            int l2 = str2.length();
        for (int i = 0; i < l2; i++)
        {
            freq2[str2.charAt(i) - 'a'] += 1;
        }

        int count = Integer.MAX_VALUE;

        // find the minimum frequency of
        // every character in str1
        for (int i = 0; i < l2; i++)
        {
            if(freq2[str2.charAt(i)-'a']!=0)
              count = Math.min(count,
                               freq[str2.charAt(i) - 'a']/freq2[str2.charAt(i)-'a']);
        }

        return count;
    }

    public static void main(String[] args) {

        String str1 = "foreeksgekseg";
        String str2 ="geeks";
        System.out.println(findNumberOfTimes(str1, str2));

    }
}
/* This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python3 program to print the number of
# times str2 can be formed from str1 using
# the characters of str1 only once
import sys

# Function to find the number of str2
# that can be formed using characters of str1
def findNumberOfTimes(str1, str2):

    freq = [0] * 26
    l1 = len(str1)

    freq2= [0] * 26
    l2 = len(str2)

    # iterate and mark the frequencies
    # of all characters in str1
    for i in range(l1):
        freq[ord(str1[i]) - ord("a")] += 1
    for i in range(l2):
        freq2[ord(str2[i]) - ord("a")] += 1

    count = sys.maxsize

    # find the minimum frequency of
    # every character in str1
    for i in range(l2):
      count = min(count, freq[ord(str2[i])
                              -  ord('a')]/freq2[ord(str2[i])-ord('a')])

    return count

# Driver Code
if __name__ == '__main__':
    str1 = "foreeksgekseg"
    str2 = "geeks"
    print(findNumberOfTimes(str1, str2))

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to print the number of
// times str2 can be formed from str1
// using the characters of str1 only once
using System;

class GFG {

    // Function to find the number of
    // str2 that can be formed using
    // characters of str1
    static int findNumberOfTimes(String str1, String str2)
    {
        int[] freq = new int[26];

        int l1 = str1.Length;
        int[] freq2 = new int[26];

        int l2 = str2.Length;

        // iterate and mark the frequencies
        // of all characters in str1
        for (int i = 0; i < l1; i++)
        {
            freq[str1[i] - 'a'] += 1;
        }
        for (int i = 0; i < l2; i++)
        {
            freq2[str2[i] - 'a'] += 1;
        }

        int count = int.MaxValue;

        // find the minimum frequency of
        // every character in str1
        for (int i = 0; i < l2; i++)
        {
            if (freq2[str2[i] - 'a'] != 0)
                count = Math.Min(
                    count, freq[str2[i] - 'a']
                               / freq2[str2[i] - 'a']);
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {
        String str1 = "foreeksgekseg";
        String str2 = "geeks";
        Console.Write(findNumberOfTimes(str1, str2));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the number of times
// str2 can be formed from str1 using the
// characters of str1 only once

// Function to find the number of str2
// that can be formed using characters of str1
function findNumberOfTimes($str1, $str2)
{
    $freq = array_fill(0, 26, NULL);

    $l1 = strlen($str1);

   $freq2 = array_fill(0, 26, NULL);

    $l2 = strlen($str2);

    // iterate and mark the frequencies
    // of all characters in str1
    for ($i = 0; $i < $l1; $i++)
        $freq[ord($str1[$i]) - ord('a')] += 1;

    for ($i = 0; $i < $l2; $i++)
        $freq2[ord($str2[$i]) - ord('a')] += 1;

    $count = PHP_INT_MAX;

    // find the minimum frequency of
    // every character in str1
    for ($i = 0; $i < $l2; $i++)
        $count = min($count, $freq[ord($str2[$i]) -
                                   ord('a')]/$freq2[ord($str2[$i]) -
                                   ord('a')]);

    return $count;
}

// Driver Code
$str1 = "foreeksgekseg";
$str2 = "geeks";

echo findNumberOfTimes($str1, $str2) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to print the number of times
// str2 can be formed from str1 using the
// characters of str1 only once

    // Function to find the number of str2
    // that can be formed using characters of str1
    function findNumberOfTimes(str1, str2)
    {
        let freq = new Array(26);
        let freq2 = new Array(26);
        for(let i = 0; i < 26; i++)
        {
            freq[i] = 0;
            freq2[i] = 0;
        }

        let l1 = str1.length;

        // iterate and mark the frequencies of
        // all characters in str1
        for (let i = 0; i < l1; i++)
        {
            freq[str1[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
        }
            let l2 = str2.length;
        for (let i = 0; i < l2; i++)
        {
            freq2[str2[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
        }

        let count = Number.MAX_VALUE;

        // find the minimum frequency of
        // every character in str1
        for (let i = 0; i < l2; i++)
        {
            if(freq2[str2[i].charCodeAt(0)-'a'.charCodeAt(0)]!=0)
              count = Math.min(count,
                               freq[str2[i].charCodeAt(0) - 'a'.charCodeAt(0)]/freq2[str2[i].charCodeAt(0)-'a'.charCodeAt(0)]);
        }

        return count;
    }

    let str1 = "foreeksgekseg";
    let str2 ="geeks";
    document.write(findNumberOfTimes(str1, str2));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
2
```

**时间复杂度:** O(max(l1，l2))，其中 l1 和 l2 分别是 str1 和 str2 的长度。