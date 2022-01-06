# 使用相同字符集的字典顺序下一个更大的字符串

> 原文:[https://www . geeksforgeeks . org/词典-下一个更大的字符串-使用相同的字符集/](https://www.geeksforgeeks.org/lexicographically-next-greater-string-using-same-character-set/)

给定一个数字 K 和一个字符串 S，我们必须找到字典上最小的长度为 K 的字符串，这样它的字母集就是 S 的字母集的子集，并且 S 在字典上小于 str。
**例:**

```
Input :k = 3
       s = zbf
Output: zbz
Explanation: zbz is greater than zbf and it is
smaller than any other lexicographically greater
string than zbf

Input :k = 3
       s = gi
Output: gig
Explanation: gig > gi and size is 3.
```

**方法:**如果字符串的大小小于 k，我们应该简单地添加来自 s.
的 k–s . size()最小符号，如果字符串的大小大于或等于 k，那么我们需要替换字符串最小符号的前 k 个符号后缀中的所有符号，并用字符串中存在的下一个更大的字符替换该后缀之前的字符。
**注意:**如果字符串中的 k-1 索引包含最大的字符，那么我们向后移动一个索引，直到找到不等于最大字符的字符。

## C++

```
// C++ implementation of above algorithm.
#include <bits/stdc++.h>
using namespace std;

// function to print output
void lexoString(string s, int k)
{

    int n = s.size();

    // to store unique characters of the string
    vector<char> v;

    // to check uniqueness
    map<char, int> mp;

    for (int i = 0; i < s.size(); i++) {

        if (mp[s[i]] == 0) {

            // if mp[s[i]] = 0 then it is
            // first time
            mp[s[i]] = 1;
            v.push_back(s[i]);
        }
    }

    // sort the unique characters
    sort(v.begin(), v.end());

    // simply add n-k smallest characters
    if (k > n)
    {
        cout << s;
        for (int i = n; i < k; i++) {
            cout << v[0];
        }

        return; // end the program
    }

    // searching the first character left of
    // index k and not equal to greatest
    // character of the string
    for (int i = k - 1; i >= 0; i--) {
        if (s[i] != v[v.size() - 1]) {
            for (int j = 0; j < i; j++) {
                cout << s[j];
            }

            // finding the just next greater
            // character than s[i]
            for (int j = 0; j < v.size(); j++) {
                if (v[j] > s[i]) {
                    cout << v[j];
                    break;
                }
            }

            // suffix with smallest character
            for (int j = i + 1; j < k; j++)
                cout << v[0];        

            return;
        }
    }

    // if we reach here then all indices to the left
    // of k had the greatest character
    cout << "No lexicographically greater string of length "
         << k << " possible here.";

}

// Driver code
int main()
{
    string s = "gi";
    int k = 3;

    // Function call
    lexoString(s, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above algorithm.
import java.util.*;

class GFG
{

    // function to print output
    static void lexoString(char[] s, int k)
    {

        int n = s.length;

        // to store unique characters of the string
        Vector<Character> v = new Vector<>();

        // to check uniqueness
        Map<Character, Integer> mp = new HashMap<>();

        for (int i = 0; i < s.length; i++)
        {

            if (!mp.containsKey(s[i]))
            {

                // if mp[s[i]] = 0 then it is
                // first time
                mp.put(s[i], 1);
                v.add(s[i]);
            }
        }

        // sort the unique characters
        Collections.sort(v);

        // simply add n-k smallest characters
        if (k > n)
        {
            System.out.print(String.valueOf(s));
            for (int i = n; i < k; i++)
            {
                System.out.print(v.get(0));
            }

            return; // end the program
        }

        // searching the first character left of
        // index k and not equal to greatest
        // character of the string
        for (int i = k - 1; i >= 0; i--)
        {
            if (s[i] != v.get(v.size() - 1))
            {
                for (int j = 0; j < i; j++)
                {
                    System.out.print(s[j]);
                }

                // finding the just next greater
                // character than s[i]
                for (int j = 0; j < v.size(); j++)
                {
                    if (v.get(j) > s[i])
                    {
                        System.out.print(v.get(j));
                        break;
                    }
                }

                // suffix with smallest character
                for (int j = i + 1; j < k; j++)
                {
                    System.out.print(v.get(0));
                }

                return;
            }
        }

        // if we reach here then all indices to the left
        // of k had the greatest character
        System.out.print("No lexicographically greater string of length "
                + k + " possible here.");

    }

    // Driver code
    public static void main(String arr[])
    {
        String s = "gi";
        int k = 3;

        // Function call
        lexoString(s.toCharArray(), k);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of above algorithm.

# function to print output
def lexoString(s, k):
    n = len(s)

    # to store unique characters
    # of the string
    v = []

    # to check uniqueness
    mp = {s[i]:0 for i in range(len(s))}

    for i in range(len(s)):
        if (mp[s[i]] == 0):

            # if mp[s[i]] = 0 then it is
            # first time
            mp[s[i]] = 1
            v.append(s[i])

    # sort the unique characters
    v.sort(reverse = False)

    # simply add n-k smallest characters
    if (k > n):
        print(s, end = "")
        for i in range(n, k, 1):
            print(v[0], end = "")

        return;

    # end the program

    # searching the first character left of
    # index k and not equal to greatest
    # character of the string
    i = k - 1
    while(i >= 0):
        if (s[i] != v[len(v) - 1]):
            for j in range(0, i, 1):
                print(s[j], end = " ")

            # finding the just next greater
            # character than s[i]
            for j in range(0, len(v), 1):
                if (v[j] > s[i]):
                    print(v[j], end = " ")
                    break

            # suffix with smallest character
            for j in range(i + 1, k, 1):
                print(v[0], end = " ")    

            re1turn
        i -= 1

    # if we reach here then all indices to
    # the left of k had the greatest character
    print("No lexicographically greater",
          "string of length", k, "possible here.")

# Driver code
if __name__ == '__main__':
    s = "gi"
    k = 3

    # Function call
    lexoString(s, k)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of above algorithm.
using System;
using System.Collections.Generic;

class GFG
{

    // function to print output
    static void lexoString(char[] s, int k)
    {

        int n = s.Length;

        // to store unique characters of the string
        List<char> v = new List<char>();

        // to check uniqueness
        Dictionary<char,
                   int> mp = new Dictionary<char,
                                            int>();

        for (int i = 0; i < s.Length; i++)
        {
            if (!mp.ContainsKey(s[i]))
            {

                // if mp[s[i]] = 0 then it is
                // first time
                mp.Add(s[i], 1);
                v.Add(s[i]);
            }
        }

        // sort the unique characters
        v.Sort();

        // simply add n-k smallest characters
        if (k > n)
        {
            Console.Write(String.Join("", s));
            for (int i = n; i < k; i++)
            {
                Console.Write(v[0]);
            }

            return; // end the program
        }

        // searching the first character left of
        // index k and not equal to greatest
        // character of the string
        for (int i = k - 1; i >= 0; i--)
        {
            if (s[i] != v[v.Count - 1])
            {
                for (int j = 0; j < i; j++)
                {
                    Console.Write(s[j]);
                }

                // finding the just next greater
                // character than s[i]
                for (int j = 0; j < v.Count; j++)
                {
                    if (v[j] > s[i])
                    {
                        Console.Write(v[j]);
                        break;
                    }
                }

                // suffix with smallest character
                for (int j = i + 1; j < k; j++)
                {
                    Console.Write(v[0]);
                }
                return;
            }
        }

        // if we reach here then all indices to the left
        // of k had the greatest character
        Console.Write("No lexicographically greater " +
                              "string of length " + k +
                                    " possible here.");

    }

    // Driver code
    public static void Main(String []arr)
    {
        String s = "gi";
        int k = 3;

        // Function call
        lexoString(s.ToCharArray(), k);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
      // JavaScript implementation of above algorithm.
      // function to print output
      function lexoString(s, k) {
        var n = s.length;

        // to store unique characters of the string
        var v = [];

        // to check uniqueness
        var mp = {};

        for (var i = 0; i < s.length; i++) {
          if (!mp.hasOwnProperty(s[i])) {
            // if mp[s[i]] = 0 then it is
            // first time
            mp[s[i]] = 1;
            v.push(s[i]);
          }
        }

        // sort the unique characters
        v.sort((a, b) => a - b);

        // simply add n-k smallest characters
        if (k > n) {
          document.write(s.join(""));
          for (var i = n; i < k; i++) {
            document.write(v[0]);
          }

          return; // end the program
        }

        // searching the first character left of
        // index k and not equal to greatest
        // character of the string
        for (var i = k - 1; i >= 0; i--) {
          if (s[i] !== v[v.length - 1]) {
            for (var j = 0; j < i; j++) {
              document.write(s[j]);
            }

            // finding the just next greater
            // character than s[i]
            for (var j = 0; j < v.length; j++) {
              if (v[j] > s[i]) {
                document.write(v[j]);
                break;
              }
            }

            // suffix with smallest character
            for (var j = i + 1; j < k; j++) {
              document.write(v[0]);
            }
            return;
          }
        }

        // if we reach here then all indices to the left
        // of k had the greatest character
        document.write(
          "No lexicographically greater " +
            "string of length " +
            k +
            " possible here."
        );
      }

      // Driver code
      var s = "gi";
      var k = 3;

      // Function call
      lexoString(s.split(""), k);
    </script>
```

**Output:** 

```
gig
```

**时间复杂度:** O(k + s.size())