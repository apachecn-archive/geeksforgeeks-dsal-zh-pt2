# 长度至多为 K 的字典最短字符串，它不是给定字符串的子串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最多 k 个长度的字符串-哪个不是给定字符串的子字符串/](https://www.geeksforgeeks.org/lexicographically-shortest-string-of-length-at-most-k-which-is-not-a-substring-of-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到长度小于或等于 **K** 的字典最短字符串，该字符串不是给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。如果不可能，打印-1。

**示例:**

> **输入:** *S = zxabcehgf，K = 2*
> **输出:** d
> **解释:**从词典上看，*不是给定字符串的子串的最短字符串是 d.*
> 
> **输入:**T2【S = sdhacbdefghijklmnopqrstuvwxyz，K = 3T4**输出:** ab

**方法:**找到给定的[串](https://www.geeksforgeeks.org/string-data-structure/) **S** 的所有长度小于或等于 **K** 的子串即可解决问题。然后从字典上最小的[串](https://www.geeksforgeeks.org/string-data-structure/) ' **a** '开始，继续形成下一个[串](https://www.geeksforgeeks.org/string-data-structure/)，直到我们没有找到答案。按照以下步骤解决问题。

*   初始化一组[字符串](https://www.geeksforgeeks.org/string-data-structure/)的，比如 **st、**，最多存储所有[长度的子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)**K**。
*   从 **1** 迭代到 **K** 以创建从 **1** 到**K**的所有[字符串](https://www.geeksforgeeks.org/string-data-structure/)可能的长度
*   检查当前形成的[串](https://www.geeksforgeeks.org/string-data-structure/)是否存在于[组](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。如果没有，那么打印出来并返回。
*   否则，形成下一个字典式的[字符串](https://www.geeksforgeeks.org/string-data-structure/)，重复这个过程，直到找到一个**答案**。

下面是上述方法的实现。

## C++

```
// C++ implementation for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return a set of all
// substrings of given string which have
// length less than or equal to k
set<string> presentSubstring(string s, int k)
{
    set<string> st;
    int n = s.length();

    for (int i = 0; i < n; i++) {
        string s1 = "";

        for (int j = 0; j < k && i + j < n; j++) {
            s1.push_back(s[i + j]);

            st.insert(s1);
        }
    }

    return st;
}

// Function to print the lexicographically
// smallest substring of length atmost k
// which is not present in given string s
string smallestSubstring(string s, int k)
{
    set<string> st;

    // All substrings of length atmost k
    // present in string s are stored in
    // this set
    st = presentSubstring(s, k);

    int index;

    // Loop to change length of substring
    for (int len = 1; len <= k; len++) {

        // String with length=len which has
        // all characters as 'a'
        string t(len, 'a');

        while (true) {

            // If the substrings set does
            // not contain this string then
            // we have found the answer
            if (st.count(t) == 0) {
                return t;
            }

            index = len - 1;

            // Changing the likes of 'azz'
            // and 'daz' to 'baa' and 'dba'
            // respectively
            while (index >= 0 && t[index] == 'z') {
                t[index] = 'a';
                index--;
            }

            if (index >= 0)
                t[index]++;

            // Reached a string like 'zz'
            // or 'zzz' increase the length
            // of the substring
            else
                break;
        }
    }
    return "-1";
}

// Driver Code
int main()
{

    // Given Input
    string s = "sdhaacbdefghijklmnopqrstuvwxyz";
    int K = 3;

    // Function Call
    cout << smallestSubstring(s, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
import java.util.*;

class GFG
{

// Function to return a set of all
// subStrings of given String which have
// length less than or equal to k
static HashSet<String> presentSubString(String s, int k)
{
    HashSet<String> st = new HashSet<String>();
    int n = s.length();

    for (int i = 0; i < n; i++) {
        String s1 = "";

        for (int j = 0; j < k && i + j < n; j++) {
            s1 += s.charAt(i + j);

            st.add(s1);
        }
    }

    return st;
}

// Function to print the lexicographically
// smallest subString of length atmost k
// which is not present in given String s
static String smallestSubString(String s, int k)
{
    HashSet<String> st = new HashSet<String>();

    // All subStrings of length atmost k
    // present in String s are stored in
    // this set
    st = presentSubString(s, k);

    int index;

    // Loop to change length of subString
    for (int len = 1; len <= k; len++) {

        // String with length=len which has
        // all characters as 'a'
        String t = "";
        for(int i=0;i<len;i++)
            t+='a';

        while (true) {

            // If the subStrings set does
            // not contain this String then
            // we have found the answer
            if (!st.contains(t)) {
                return t;
            }

            index = len - 1;

            // Changing the likes of 'azz'
            // and 'daz' to 'baa' and 'dba'
            // respectively
            while (index >= 0 && t.charAt(index) == 'z') {
                t=t.substring(0,index)+'a'+t.substring(index+1);
                index--;
            }

            if (index >= 0)
                t=t.substring(0,index)+ (char)((t.charAt(index))+1) + t.substring(index+1);

            // Reached a String like 'zz'
            // or 'zzz' increase the length
            // of the subString
            else
                break;
        }
    }
    return "-1";
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    String s = "sdhaacbdefghijklmnopqrstuvwxyz";
    int K = 3;

    // Function Call
    System.out.print(smallestSubString(s, K) +"\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 implementation for above approach

# Function to return a set of all
# substrings of given string which have
# length less than or equal to k
def presentSubstring(s, k):
    st = set()
    n = len(s)
    s = list(s)

    for i in range(n):
        s1 = ""
        j = 0
        while(j < k and i + j < n):
            s1 += s[i + j]

            st.add(s1)
            j += 1

    s = ''.join(s)
    return st

# Function to print the lexicographically
# smallest substring of length atmost k
# which is not present in given string s
def smallestSubstring(s, k):
    st = set()

    # All substrings of length atmost k
    # present in string s are stored in
    # this set
    st = presentSubstring(s, k)

    index = 0

    # Loop to change length of substring
    for len1 in range(1,k+1,1):
        # String with length=len which has
        # all characters as 'a'
        t = []
        for x in range(len1):
            t.append('a')

        while (True):
            # If the substrings set does
            # not contain this string then
            # we have found the answer
            if (''.join(t) not in st):
                return ''.join(t)

            index = len1 - 1

            # Changing the likes of 'azz'
            # and 'daz' to 'baa' and 'dba'
            # respectively
            while (index >= 0 and t[index] == 'z'):
                t[index] = 'a'
                index -= 1

            if (index >= 0):
                t[index] = chr(ord(t[index])+1)

            # Reached a string like 'zz'
            # or 'zzz' increase the length
            # of the substring
            else:
                break
    return "-1"

# Driver Code
if __name__ == '__main__':
    # Given Input
    s = "sdhaacbdefghijklmnopqrstuvwxyz"
    K = 3

    # Function Call
    print(smallestSubstring(s, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# implementation for above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to return a set of all
    // substrings of given string which have
    // length less than or equal to k
    static HashSet<string> presentSubstring(string s, int k)
    {
        HashSet<string> st = new HashSet<string>();
        int n = s.Length;

        for (int i = 0; i < n; i++) {
            string s1 = "";

            for (int j = 0; j < k && i + j < n; j++) {
                s1 += s[i + j];

                st.Add(s1);
            }
        }

        return st;
    }

    // Function to print the lexicographically
    // smallest substring of length atmost k
    // which is not present in given string s
    static string smallestSubstring(string s, int k)
    {
        HashSet<string> st = new HashSet<string>();

        // All substrings of length atmost k
        // present in string s are stored in
        // this set
        st = presentSubstring(s, k);

        int index;

        // Loop to change length of substring
        for (int len = 1; len <= k; len++) {

            // String with length=len which has
            // all characters as 'a'
            string t = "";
            for (int i = 0; i < len; i++)
                t += 'a';

            while (true) {

                // If the substrings set does
                // not contain this string then
                // we have found the answer
                if (st.Contains(t)==false) {
                    return t;
                }

                index = len - 1;

                // Changing the likes of 'azz'
                // and 'daz' to 'baa' and 'dba'
                // respectively
                while (index >= 0 && t[index] == 'z') {
                    t = t.Substring(0, index) + 'a'
                        + t.Substring(index + 1);
                    index--;
                }

                if (index >= 0) {
                    t = t.Substring(0, index)
                        + Convert.ToChar((int)t[index] + 1)
                        + t.Substring(index + 1);
                }

                // Reached a string like 'zz'
                // or 'zzz' increase the length
                // of the substring
                else
                    break;
            }
           // t += 'b';
        }
        return "-1";
    }

    // Driver Code
    public static void Main()
    {

        // Given Input
        string s = "sdhaacbdefghijklmnopqrstuvwxyz";
        int K = 3;

        // Function Call
        Console.Write(smallestSubstring(s, K));
    }
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript implementation for above approach

// Function to return a set of all
// substrings of given string which have
// length less than or equal to k
function presentSubstring(s, k) {
  let st = new Set();
  let n = s.length;
  s = s.split("");

  for (let i = 0; i < n; i++) {
    let s1 = "";

    for (let j = 0; j < k && i + j < n; j++) {
      s1 += s[i + j];

      st.add(s1);
    }
  }

  return st;
}

// Function to print the lexicographically
// smallest substring of length atmost k
// which is not present in given string s
function smallestSubstring(s, k) {
  let st = new Set();

  // All substrings of length atmost k
  // present in string s are stored in
  // this set
  st = presentSubstring(s, k);

  let index = 0;

  // Loop to change length of substring
  for (let len = 1; len <= k; len++)
  {

    // String with length=len which has
    // all characters as 'a'
    let t = new Array(len).fill("a");

    while (true)
    {

      // If the substrings set does
      // not contain this string then
      // we have found the answer

      if (!st.has(t.join(""))) {
        return t.join("");
      }

      index = len - 1;

      // Changing the likes of 'azz'
      // and 'daz' to 'baa' and 'dba'
      // respectively
      while (index >= 0 && t[index] == "z") {
        t[index] = "a";
        index--;
      }

      if (index >= 0)
        t[index] = String.fromCharCode(t[index].charCodeAt(0) + 1);

      // Reached a string like 'zz'
      // or 'zzz' increase the length
      // of the substring
      else break;
    }
  }
  return "-1";
}

// Driver Code

// Given Input
let s = "sdhaacbdefghijklmnopqrstuvwxyz";
let K = 3;

// Function Call
document.write(smallestSubstring(s, K));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
ab
```

***时间复杂度:**O(K * N)*
T5**辅助空间:** O(K*N)