# 通过最多删除一个字符形成的字典上最小的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小字符串-通过最多删除一个字符形成/](https://www.geeksforgeeks.org/lexicographically-smallest-string-formed-by-removing-at-most-one-character/)

给定一个字符串 **str** ，任务是找到字典上最小的字符串，该字符串可以通过从给定字符串中最多移除一个字符来形成。

**示例:**

```
Input: str = "abcda"  
Output: abca
One can remove 'd' to get "abca" which is 
the lexicographically smallest string possible. 

Input: str = "aaa' 
Output: aa
```

**逼近**:遍历字符串，在第一个点**s【I】>s【I+1】**处删除第 I 个字符。如果没有这样的字符，则删除字符串中的最后一个字符。

下面是上述方法的实现:

## C++

```
// C++ program to find the lexicographically
// smallest string by removing at most one character
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest string
string smallest(string s)
{
    int l = s.length();
    string ans = "";

    // iterate the string
    for (int i = 0; i < l-1; i++) {

        // first point where s[i]>s[i+1]
        if (s[i] > s[i + 1]) {

            // append the string without
            // i-th character in it
            for (int j = 0; j < l; j++) {
                if (i != j)
                    ans += s[j];
            }
            return ans;
        }
    }

    // leave the last character
    ans = s.substr(0., l - 1);
    return ans;
}

// Driver Code
int main()
{
    string s = "abcda";

    cout << smallest(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the lexicographically
// smallest String by removing at most one character

class GFG {

// Function to return the smallest String
    static String smallest(String s) {
        int l = s.length();
        String ans = "";

        // iterate the String
        for (int i = 0; i < l-1; i++) {

            // first point where s[i]>s[i+1]
            if (s.charAt(i) > s.charAt(i + 1)) {

                // append the String without
                // i-th character in it
                for (int j = 0; j < l; j++) {
                    if (i != j) {
                        ans += s.charAt(j);
                    }
                }
                return ans;
            }
        }

        // leave the last character
        ans = s.substring(0, l - 1);
        return ans;
    }

// Driver Code
    public static void main(String[] args) {

        String s = "abcda";
        System.out.println(smallest(s));
    }
}
/* This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python3 program to find the lexicographically
# smallest string by removing at most one character

# Function to return the smallest string
def smallest(s):

    l = len(s)
    ans = ""

    # iterate the string
    for i in range (l-1):

        # first point where s[i]>s[i+1]
        if (s[i] > s[i + 1]):

            # append the string without
            # i-th character in it
            for j in range (l):
                if (i != j):
                    ans += s[j]

            return ans

    # leave the last character
    ans = s[0: l - 1]
    return ans

# Driver Code
if __name__ == "__main__":

    s = "abcda"

    print (smallest(s))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the lexicographically
// smallest String by removing at most
// one character
using System;

class GFG
{

// Function to return the
// smallest String
static String smallest(String s)
{
    int l = s.Length;
    String ans = "";

    // iterate the String
    for (int i = 0; i < l-1; i++)
    {

        // first point where s[i]>s[i+1]
        if (s[i] > s[i + 1])
        {

            // append the String without
            // i-th character in it
            for (int j = 0; j < l; j++)
            {
                if (i != j)
                {
                    ans += s[j];
                }
            }
            return ans;
        }
    }

    // leave the last character
    ans = s.Substring(0, l - 1);
    return ans;
}

// Driver Code
public static void Main()
{
    String s = "abcda";
    Console.Write(smallest(s));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the lexicographically
// smallest String by removing at most one character

    // Function to return the smallest String
    function smallest(s)
    {
        let l = s.length;
        let ans = "";

        // iterate the String
        for (let i = 0; i < l-1; i++)
        {

            // first point where s[i]>s[i+1]
            if (s[i] > s[i+1]) {

                // append the String without
                // i-th character in it
                for (let j = 0; j < l; j++) {
                    if (i != j) {
                        ans += s[j];
                    }
                }
                return ans;
            }
        }

        // leave the last character
        ans = s.substring(0, l - 1);
        return ans;
    }

    // Driver Code
    let s = "abcda";
    document.write(smallest(s));

// This code is contributed by rag2127
</script>
```

**Output**

```
abca
```