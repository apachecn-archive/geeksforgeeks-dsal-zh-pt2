# 大小为 k 的字典最小和最大子串

> 原文:[https://www . geesforgeks . org/按字典顺序排列的大小最小和最大的子串-k/](https://www.geeksforgeeks.org/lexicographically-smallest-and-largest-substring-of-size-k/)

给定 String str 和一个整数 k，求长度为 k 的字典最小和最大的子串
字典顺序，也称为字母顺序或字典顺序，

```
 A < B <... < Y < Z < a < b <.. < y < z
```

**例:**

```
Input : String: hello
        Size: 2
        Distinct Substring: [el, he, ll, lo]
Output : Smallest Substring: el
         Largest Substring: lo

Input : String: geeksforgeeks
        Size: 3
        Distinct Substring: [eek, eks, for, gee, ksf, org, rge, sfo]
Output : Smallest Substring: eek
         Largest Substring: sfo
```

我们将 max 和 min 初始化为大小为 k 的第一个子字符串。我们遍历剩余的子字符串，方法是删除前一个子字符串的第一个字符，并添加新字符串的最后一个字符。我们跟踪字典上最大的和最小的。

## C++

```
// CPP program to find lexicographically
// largest and smallest substrings of size k.
#include<bits/stdc++.h>

using namespace std;

    void getSmallestAndLargest(string s, int k)
    {

        // Initialize min and max as
        // first substring of size k
        string currStr = s.substr(0, k);
        string lexMin = currStr;
        string lexMax = currStr;

        // Consider all remaining substrings. We consider
        // every substring ending with index i.
        for (int i = k; i < s.length(); i++)
        {
            currStr = currStr.substr(1, k) + s[i];
            if (lexMax < currStr)    
                lexMax = currStr;
            if (lexMin >currStr)
                lexMin = currStr;    
        }

        // Print result.
        cout << (lexMin) << endl;
        cout << (lexMax) << endl;
    }

    // Driver Code
    int main()
    {
        string str = "GeeksForGeeks";
        int k = 3;
        getSmallestAndLargest(str, k);
    }

// This code is contributed by
// Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lexicographically largest and smallest
// substrings of size k.

public class GFG {

    public static void getSmallestAndLargest(String s, int k)
    {
        // Initialize min and max as first substring of size k
        String currStr = s.substring(0, k);
        String lexMin = currStr;
        String lexMax = currStr;

        // Consider all remaining substrings. We consider
        // every substring ending with index i.
        for (int i = k; i < s.length(); i++) {
            currStr = currStr.substring(1, k) + s.charAt(i);
            if (lexMax.compareTo(currStr) < 0)    
                 lexMax = currStr;
            if (lexMin.compareTo(currStr) > 0)
                 lexMin = currStr;           
        }

        // Print result.
        System.out.println(lexMin);
        System.out.println(lexMax);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "GeeksForGeeks";
        int k = 3;
        getSmallestAndLargest(str, k);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find lexicographically
# largest and smallest substrings of size k.
def getSmallestAndLargest(s, k):

    # Initialize min and max as
    # first substring of size k
    currStr = s[:k]
    lexMin = currStr
    lexMax = currStr

    # Consider all remaining substrings.
    # We consider every substring ending
    # with index i.
    for i in range(k, len(s)):
        currStr = currStr[1 : k] + s[i]
        if (lexMax < currStr):
            lexMax = currStr
        if (lexMin >currStr):
            lexMin = currStr

    # Print result.
    print(lexMin)
    print(lexMax)

# Driver Code
if __name__ == '__main__':
    str1 = "GeeksForGeeks"
    k = 3
    getSmallestAndLargest(str1, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find lexicographically
// largest and smallest substrings of size k.
using System;

class GFG
{
    // Function to compare two strings
    static int CompareTo(String s1, String s2)
    {
        for (int i = 0; i < s1.Length ||
                        i < s2.Length; i++)
        {
            if (s1[i] < s2[i])
                return -1;
            else if (s1[i] > s2[i])
                return 1;
        }
        return 0;
    }

    static void getSmallestAndLargest(String s, int k)
    {
        // Initialize min and max as
        // first substring of size k
        String currStr = s.Substring(0, k);
        String lexMin = currStr;
        String lexMax = currStr;

        // Consider all remaining substrings.
        // We consider every substring
        // ending with index i.
        for (int i = k; i < s.Length; i++)
        {
            currStr = currStr.Substring(1, k - 1) + "" + s[i];
            if (CompareTo(lexMax, currStr) < 0)
                lexMax = currStr;
            if (CompareTo(lexMin, currStr) > 0)
                lexMin = currStr;
        }

        // Print result.
        Console.WriteLine(lexMin);
        Console.WriteLine(lexMax);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "GeeksForGeeks";
        int k = 3;
        getSmallestAndLargest(str, k);
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

      // JavaScript program to find lexicographically
      // largest and smallest substrings of size k.

      function getSmallestAndLargest(s, k) {
        // Initialize min and max as
        // first substring of size k
        var currStr = s.substring(0, k);
        var lexMin = currStr;
        var lexMax = currStr;

        // Consider all remaining substrings.
        // We consider every substring
        // ending with index i.
        for (var i = k; i < s.length; i++) {
          currStr = currStr.substring(1, k) + s[i];
          if (lexMax < currStr) lexMax = currStr;
          if (lexMin > currStr) lexMin = currStr;
        }

        // Print result.
        document.write(lexMin + "<br>");
        document.write(lexMax + "<br>");
      }

      // Driver Code
      var str = "GeeksForGeeks";
      var k = 3;
      getSmallestAndLargest(str, k);

</script>
```

**Output:** 

```
For
sFo
```