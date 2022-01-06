# 由范围为 L 和 R 的字符组成的字典上最大的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大字符串-由范围内的字符组成-l 和-r/](https://www.geeksforgeeks.org/lexicographically-largest-string-formed-from-the-characters-in-range-l-and-r/)

给定一个字符串 S 和一个范围 L 和 R，任务是打印从范围 L 和 R 中的字符组成的字典式最大字符串。
**示例**:

```
Input: str = "thgyfh", L = 2, R = 6  
Output: yhhgf

Input: str = "striver", L = 3, R = 5
Output: vri
```

**接近**:

*   从 **min(L，R)** 迭代到 **max(L，R)** ，增加 freq[]数组中字符的出现频率。
*   从 25 到 0 迭代，并打印每个字符出现的次数，以获得字典中最大的字符串。

每个人都会犯的一个常见错误是，他们从 *L 迭代到 R，而不是从 min(L，R)迭代到 max(L，R)* 。
以下是上述办法的实施情况:

## C++

```
// C++ program to print the
// lexicographically largest string that
// can be formed from the characters
// in range L and R

#include <bits/stdc++.h>
using namespace std;

// Function to return the lexicographically largest string
string printLargestString(string s, int l, int r)
{
    // hash array
    int freq[26] = { 0 };

    // make 0-based indexing
    l--;
    r--;

    // iterate and count frequencies of character
    for (int i = min(l, r); i <= max(l, r); i++) {
        freq[s[i] - 'a']++;
    }

    // ans string
    string ans = "";

    // iterate in frequency array
    for (int i = 25; i >= 0; i--) {

        // add til all characters
        // are added
        while (freq[i]) {
            ans += char('a' + i);
            freq[i]--;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    string s = "striver";
    int l = 3, r = 5;
    cout << printLargestString(s, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// lexicographically largest String that
// can be formed from the characters
// in range L and R 

class GFG {

// Function to return the lexicographically largest String
    static String printLargestString(String s, int l, int r) {
        // hash array
        int freq[] = new int[26];

        // make 0-based indexing
        l--;
        r--;

        // iterate and count frequencies of character
        for (int i = Math.min(l, r); i <= Math.max(l, r); i++) {
            freq[s.charAt(i) - 'a']++;
        }

        // ans String
        String ans = "";

        // iterate in frequency array
        for (int i = 25; i >= 0; i--) {

            // add til all characters
            // are added
            while (freq[i] > 0) {
                ans += (char) ('a' + i);
                freq[i]--;
            }
        }

        return ans;
    }

// Driver Code
    public static void main(String[] args) {

        String s = "striver";
        int l = 3, r = 5;
        System.out.println(printLargestString(s, l, r));

    }
}
/* This JAVA code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 program to print the
# lexicographically largest string that
# can be formed from the characters
# in range L and R

# Function to return the lexicographically
# largest string
def printLargestString(s, l, r):

    # hash array
    freq = [0] * 26

    # make 0-based indexing
    l -= 1
    r -= 1

    # iterate and count frequencies of character
    for i in range(min(l, r), max(l, r) + 1) :
        freq[ord(s[i]) - ord('a')] += 1

    # ans string
    ans = ""

    # iterate in frequency array
    for i in range(25, -1, -1):

        # add til all characters are added
        while (freq[i]):
            ans += chr(ord('a') + i)
            freq[i] -= 1

    return ans

# Driver Code
if __name__ == "__main__":

    s = "striver"
    l = 3
    r = 5
    print(printLargestString(s, l, r))

# This code is contributed by ita_c
```

## C#

```
// C# program to print the lexicographically
// largest String that can be formed from the
// characters in range L and R
using System;

class GFG
{

// Function to return the lexicographically
// largest String
static String printLargestString(String s,
                                 int l, int r)
{
    // hash array
    int []freq = new int[26];

    // make 0-based indexing
    l--;
    r--;

    // iterate and count frequencies
    // of character
    for (int i = Math.Min(l, r);
             i <= Math.Max(l, r); i++)
    {
        freq[s[i] - 'a']++;
    }

    // ans String
    String ans = "";

    // iterate in frequency array
    for (int i = 25; i >= 0; i--)
    {

        // add til all characters
        // are added
        while (freq[i] > 0)
        {
            ans += (char) ('a' + i);
            freq[i]--;
        }
    }

    return ans;
}

// Driver Code
public static void Main()
{
    String s = "striver";
    int l = 3, r = 5;
    Console.Write(printLargestString(s, l, r));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to print the
// lexicographically largest String that
// can be formed from the characters
// in range L and R 
    // Function to return the lexicographically largest String
     function printLargestString( s , l , r) {
        // hash array
        var freq = Array(26).fill(0);

        // make 0-based indexing
        l--;
        r--;

        // iterate and count frequencies of character
        for (i = Math.min(l, r); i <= Math.max(l, r); i++) {
            freq[s.charCodeAt(i) - 'a'.charCodeAt(0)]++;
        }

        // ans String
        var ans = "";

        // iterate in frequency array
        for (var i = 25; i >= 0; i--) {

            // add til all characters
            // are added
            while (freq[i] > 0) {
                ans += String.fromCharCode('a'.charCodeAt(0) + i);
                freq[i]--;
            }
        }

        return ans;
    }

    // Driver Code

        var s = "striver";
        var l = 3, r = 5;
        document.write(printLargestString(s, l, r));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
vri
```

**时间复杂度**–O(N)
每个元素只被添加到频率表中一次，取 0(1)，并被附加到同样取 0(1)的字符串中。