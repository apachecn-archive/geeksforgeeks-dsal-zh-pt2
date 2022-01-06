# 计算字谜的出现次数

> 原文:[https://www . geeksforgeeks . org/count-occurs-of-anagrams/](https://www.geeksforgeeks.org/count-occurrences-of-anagrams/)

给定一个单词和一个文本，返回该单词在文本中出现的字谜计数(例如:单词 for 的字谜有 For、ofr、rof 等。))

示例:

```
Input : forxxorfxdofr
        for
Output : 3
Explanation : Anagrams of the word for - for, orf, 
ofr appear in the text and hence the count is 3.

Input : aabaabaa
        aaba
Output : 4
Explanation : Anagrams of the word aaba - aaba, 
abaa each appear twice in the text and hence the
count is 4.
```

一个简单的方法是从字符串的开始遍历，考虑长度等于给定单词长度的子字符串，然后检查这个子字符串是否包含单词的所有字符。

## C++

```
// A Simple C++ program to count anagrams of a
// pattern in a text.
#include<bits/stdc++.h>
using namespace std;

// Function to find if two strings are equal
bool areAnagram(string s1, string s2)
{
    map<char, int> m;
    for(int i = 0; i < s1.length(); i++)
        m[s1[i]]++;

    for(int i = 0; i < s2.length(); i++)
        m[s2[i]]--;

    for(auto it = m.begin(); it != m.end(); it++)
        if(it -> second != 0)
            return false;

        return true;
}

int countAnagrams(string text, string word)
{

    // Initialize result
    int res = 0;
    for(int i = 0;
            i < text.length() - word.length() + 1;
            i++)
    {

        // Check if the word and substring are
        // anagram of each other.
        if (areAnagram(text.substr(i, word.length()),
                                      word))
            res++;
    }
    return res;
}

// Driver Code
int main()
{
    string text = "forxxorfxdofr";
    string word = "for";

    cout << countAnagrams(text, word);

    return 0;
}

// This code is contributed by probinsah
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program to count anagrams of a
// pattern in a text.
import java.io.*;
import java.util.*;

public class GFG {

    // Function to find if two strings are equal
    static boolean araAnagram(String s1,
                              String s2)
    {
        // converting strings to char arrays
        char[] ch1 = s1.toCharArray();
        char[] ch2 = s2.toCharArray();

        // sorting both char arrays
        Arrays.sort(ch1);
        Arrays.sort(ch2);

        // Check for equality of strings
        if (Arrays.equals(ch1, ch2))
            return true;
        else
            return false;
    }

    static int countAnagrams(String text, String word)
    {
        int N = text.length();
        int n = word.length();

        // Initialize result
        int res = 0;

        for (int i = 0; i <= N - n; i++) {

            String s = text.substring(i, i + n);

            // Check if the word and substring are
            // anagram of each other.
            if (araAnagram(word, s))
                res++;
        }

        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        String text = "forxxorfxdofr";
        String word = "for";
        System.out.print(countAnagrams(text, word));
    }
}
```

**Output:** 

```
3
```

一个**高效的解决方案**是使用计数数组来检查字谜，我们可以使用滑动窗口的概念在 O(1)时间内从以前的窗口构建当前计数窗口。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to count anagrams of a
// pattern in a text.
import java.io.*;
import java.util.*;

class Solution {
    public static int countAnagrams(String s, String p)
    {
        // change CHARACTERS to support range of supported
        // characters
        int CHARACTERS = 256;
        int sn = s.length();
        int pn = p.length();
        int count = 0;
        if (sn < 0 || pn < 0 || sn < pn)
            return 0;

        char[] pArr = new char[CHARACTERS];
        char[] sArr = new char[CHARACTERS];
        int i = 0;
        // till window size
        for (; i < pn; i++) {
            sArr[CHARACTERS - s.charAt(i)]++;
            pArr[CHARACTERS - p.charAt(i)]++;
        }
        if (Arrays.equals(pArr, sArr))
            count += 1;
        // next window
        for (; i < sn; i++) {
            sArr[CHARACTERS - s.charAt(i)]++;
            sArr[CHARACTERS - s.charAt(i - pn)]--;

            if (Arrays.equals(pArr, sArr))
                count += 1;
        }
        return count;
    }
    // Driver code
    public static void main(String args[])
    {
        String text = "forxxorfxdofr";
        String word = "for";
        System.out.print(countAnagrams(text, word));
    }
}
```

## C++

```
#include <bits/stdc++.h>
using namespace std;
class Solution {
public:
    static int findAnagrams(const std::string& text,
                            const std::string& word)
    {
        int text_length = text.length();
        int word_length = word.length();
        if (text_length < 0 || word_length < 0
            || text_length < word_length)
            return 0;

        constexpr int CHARACTERS = 256;
        int count = 0;
        int index = 0;
        std::array<char, CHARACTERS> wordArr;
        wordArr.fill(0);
        std::array<char, CHARACTERS> textArr;
        textArr.fill(0);

        // till window size
        for (; index < word_length; index++) {
            wordArr[CHARACTERS - word[index]]++;
            textArr[CHARACTERS - text[index]]++;
        }
        if (wordArr == textArr)
            count += 1;
        // next window
        for (; index < text_length; index++) {
            textArr[CHARACTERS - text[index]]++;
            textArr[CHARACTERS
                    - text[index - word_length]]--;

            if (wordArr == textArr)
                count += 1;
        }
        return count;
    }
};

int main()
{
    const std::string& text = "forxxorfxdofr";
    const std::string& word = "for";

    cout << Solution::findAnagrams(text, word);
    return 0;
}
```

## 蟒蛇 3

```
# A Simple Python program to count anagrams of a
# pattern in a text with the help of sliding window problem
string = "forxxorfxdofr"
ptr = "for"
n = len(string)
k = len(ptr)
temp = []
d = {}
for i in ptr:
    if i in d:
        d[i] += 1
    else:
        d[i] = 1
i = 0
j = 0
count = len(d)

ans = 0

while j < n:
    if string[j] in d:
        d[string[j]] -= 1
        if d[string[j]] == 0:
            count -= 1
    if (j-i+1) < k:
        j += 1
    elif (j-i+1) == k:
        if count == 0:
            ans += 1

        if string[i] in d:
            d[string[i]] += 1
            if d[string[i]] == 1:
                count += 1

        i += 1
        j += 1
print(ans)
```

**Output:** 

```
3
```