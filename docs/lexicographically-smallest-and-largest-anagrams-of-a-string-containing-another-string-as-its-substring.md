# 字典上最小和最大的包含另一个字符串作为子字符串的字符串的字谜

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的包含另一个字符串作为其子字符串的字符串的最小和最大字谜/](https://www.geeksforgeeks.org/lexicographically-smallest-and-largest-anagrams-of-a-string-containing-another-string-as-its-substring/)

给定两个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 和大小为 **M** 的 **S2** ，任务是找到词汇上最小和最大的[S1**的**](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)**字谜，使其包含字符串 **S2** 作为子字符串。**

****示例:****

> ****输入:**S1 =“hheftaabzzdr”，S2 =“earth”
> **输出:** abd **earth** fhzz，zzhf**earth**DBA
> T10】解释:
> 给定字符串 S1 以 S2 为子串的最小变位是“abdearthfhzz”
> 给定字符串 S1 以 S2 为子串的最大变位是“zzhfearthdba”**
> 
> ****输入:**S1 =“ethgakagmenpgs”，S2 =“geeks”
> T3】输出: aa **geeks** gghmnpt，tpmnhgg**geeks**aa
> T10】解释:
> 以 S2 为子串的给定字符串 S1 的最小变位是“aageksghmnpt”
> 以 S2 为子串的给定字符串 S1 的最大变位是“tpmnhgggeeksaa”**

****天真方法:**最简单的方法是找到所有可能的 **S1** 的字谜，并检查这些字谜中是否有任何一个包含 **S2** 作为子串。如果是，那就找出字典上最小和最大的。**

*****时间复杂度:** O(N！)*
***辅助空间:** O(N)***

****高效方法:**思路是先逐字符生成字典序最小的字谜，然后通过反转除了包含 **S2** 的子串之外的最小字谜找到字典序最大的字谜。以下是步骤:**

1.  **初始化一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 并存储 **S1** 中出现的每个字符的[频率](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)**
2.  **维护一个[集合](https://www.geeksforgeeks.org/set-in-java/) **S** ，该集合存储 **S1** 中的不同角色。**
3.  **从 **M** 中减少 **S2** 中已经存在的 **S1** 的字符出现频率。**
4.  **初始化一个空字符串 **res** ，它将存储字典中最大的字谜。**
5.  **遍历集合 **S** ，如果遍历集合值时遇到字符串 **S2** 的第一个字符，检查 **S2** 的第二个不同字符是否大于**集合**的当前字符。如果是，则将 **S2** 的所有字符添加到 **res** 中。**
6.  **否则，继续迭代**设置**并将字符添加到 **res** 中。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest anagram of string
// which contains another string
pair<string, int> lexico_smallest(string s1,
                                  string s2)
{

    // Initializing the map and set
    map<char, int> M;
    set<char> S;
    pair<string, int> pr;

    // Iterating over s1
    for (int i = 0; i <= s1.size() - 1; ++i) {

        // Storing the frequency of
        // characters present in s1
        M[s1[i]]++;

        // Storing the distinct
        // characters present in s1
        S.insert(s1[i]);
    }

    // Decreasing the frequency of
    // characters from M that
    // are already present in s2
    for (int i = 0; i <= s2.size() - 1; ++i) {
        M[s2[i]]--;
    }

    char c = s2[0];
    int index = 0;
    string res = "";

    // Traversing alphabets
    // in sorted order
    for (auto x : S) {

        // If current character of set
        // is not equal to current
        // character of s2
        if (x != c) {
            for (int i = 1; i <= M[x]; ++i) {
                res += x;
            }
        }
        else {

            // If element is equal to
            // current character of s2
            int j = 0;
            index = res.size();

            // Checking for second
            // distinct character in s2
            while (s2[j] == x) {
                j++;
            }

            // s2[j] will store
            // second distinct character
            if (s2[j] < c) {
                res += s2;
                for (int i = 1; i <= M[x]; ++i) {
                    res += x;
                }
            }
            else {
                for (int i = 1; i <= M[x]; ++i) {
                    res += x;
                }
                index += M[x];
                res += s2;
            }
        }
    }

    pr.first = res;
    pr.second = index;

    // Return the answer
    return pr;
}

// Function to find the lexicographically
// largest anagram of string
// which contains another string
string lexico_largest(string s1, string s2)
{

    // Getting the lexicographically
    // smallest anagram
    pair<string, int> pr = lexico_smallest(s1, s2);

    // d1 stores the prefix
    string d1 = "";
    for (int i = pr.second - 1; i >= 0; i--) {
        d1 += pr.first[i];
    }

    // d2 stores the suffix
    string d2 = "";
    for (int i = pr.first.size() - 1;
         i >= pr.second + s2.size(); --i) {
        d2 += pr.first[i];
    }

    string res = d2 + s2 + d1;

    // Return the result
    return res;
}

// Driver Code
int main()
{
    // Given two strings
    string s1 = "ethgakagmenpgs";
    string s2 = "geeks";

    // Function Calls
    cout << lexico_smallest(s1, s2).first
         << "\n" ;
    cout << lexico_largest(s1, s2);

    return (0);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.lang.*;
import java.io.*;
import java.util.*;

class GFG{

// Function to find the lexicographically
// smallest anagram of string
// which contains another string
static String[] lexico_smallest(String s1, 
                                String s2)
{

    // Initializing the map and set
    Map<Character, Integer> M = new HashMap<>();
    Set<Character> S = new TreeSet<>();

    // Iterating over s1
    for(int i = 0; i <= s1.length() - 1; ++i)
    {

        // Storing the frequency of
        // characters present in s1
        if (!M.containsKey(s1.charAt(i)))
            M.put(s1.charAt(i), 1);
        else
            M.replace(s1.charAt(i),
                M.get(s1.charAt(i)) + 1);

        // Storing the distinct
        // characters present in s1
        S.add(s1.charAt(i));
    }

    // Decreasing the frequency of 
    // characters from M that
    // are already present in s2
    for(int i = 0; i <= s2.length() - 1; ++i)
    {
        if (M.containsKey(s2.charAt(i)))
            M.replace(s2.charAt(i),
                M.get(s2.charAt(i)) - 1);
    }

    char c = s2.charAt(0);
    int index = 0;
    String res = "";

    // Traversing alphabets
    // in sorted order
    Iterator<Character> it = S.iterator();
    while (it.hasNext())
    {
        char x = it.next();

        // If current character of set
        // is not equal to current 
        // character of s2
        if (x != c)
        {
            for(int i = 1; i <= M.get(x); ++i)
            {
                res += x;
            }
        }
        else
        {

            // If element is equal to 
            // current character of s2
            int j = 0;
            index = res.length();

            // Checking for second
            // distinct character in s2
            while (s2.charAt(j) == x)
            {
                j++;
            }

            // s2[j] will store
            // second distinct character
            if (s2.charAt(j) < c)
            {
                res += s2;
                for(int i = 1; i <= M.get(x); ++i)
                {
                    res += x;
                }
            }
            else
            {
                for(int i = 1; i <= M.get(x); ++i)
                {
                    res += x;
                }
                index += M.get(x);
                res += s2;
            }
        }
    }
    String pr[] = {res, index + ""};
    return pr;
}

// Function to find the lexicographically
// largest anagram of string
// which contains another string
static String lexico_largest(String s1, String s2)
{

    // Getting the lexicographically
    // smallest anagram
    String pr[] = lexico_smallest(s1, s2);

    // d1 stores the prefix
    String d1 = "";
    for(int i = Integer.valueOf(pr[1]) - 1;
            i >= 0; i--)
    {
        d1 += pr[0].charAt(i);
    }

    // d2 stores the suffix
    String d2 = "";
    for(int i = pr[0].length() - 1;
            i >= Integer.valueOf(pr[1]) +
                                 s2.length();
            --i)
    {
        d2 += pr[0].charAt(i);
    }

    String res = d2 + s2 + d1;

    // Return the result
    return res;
}

// Driver Code
public static void main (String[] args)
{

    // Given two strings
    String s1 = "ethgakagmenpgs";
    String s2 = "geeks";

    // Function Calls
    System.out.println(lexico_smallest(s1, s2)[0]);
    System.out.println(lexico_largest(s1, s2));
}
}

// This code is contributed by jyoti369
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to find the lexicographically
# smallest anagram of string
# which contains another string
def lexico_smallest(s1, s2):

    # Initializing the dictionary and set
    M = {}
    S = []
    pr = {}

    # Iterating over s1
    for i in range(len(s1)):

        # Storing the frequency of
        # characters present in s1
        if s1[i] not in M:
            M[s1[i]] = 1
        else:
            M[s1[i]] += 1

        # Storing the distinct
        # characters present in s1
        S.append(s1[i])
    S = list(set(S))
    S.sort()

    # Decreasing the frequency of
    # characters from M that
    # are already present in s2
    for i in range(len(s2)):
        if s2[i] in M:
            M[s2[i]] -= 1

    c = s2[0]
    index = 0
    res = ""

    # Traversing alphabets
    # in sorted order
    for x in S:

        # If current character of set
        # is not equal to current
        # character of s2
        if(x != c):
            for i in range(1, M[x] + 1):
                res += x
        else:

            # If element is equal to
            # current character of s2
            j = 0
            index = len(res)

            # Checking for second
            # distinct character in s2
            while(s2[j] == x):
                j += 1

            # s2[j] will store
            # second distinct character
            if(s2[j] < c):
                res += s2

                for i in range(1, M[x] + 1):
                    res += x
            else:
                for i in range(1, M[x] + 1):
                    res += x
                index += M[x]
                res += s2       
    pr[res] = index

    # Return the answer
    return pr

# Function to find the lexicographically
# largest anagram of string
# which contains another string
def lexico_largest(s1, s2):

    # Getting the lexicographically
    # smallest anagram
    Pr = dict(lexico_smallest(s1, s2))

    # d1 stores the prefix
    d1 = ""
    key = [*Pr][0]
    for i in range(Pr.get(key) - 1, -1, -1):
        d1 += key[i]

    # d2 stores the suffix
    d2 = ""
    for i in range(len(key) - 1, Pr[key] + len(s2) - 1, -1):
        d2 += key[i]
    res = d2 + s2 + d1

    # Return the result
    return res

# Driver Code

# Given two strings
s1 = "ethgakagmenpgs"
s2 = "geeks"

# Function Calls
print( *lexico_smallest(s1, s2))
print(lexico_largest(s1, s2))

# This code is contributed by avanitrachhadiya2155
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the lexicographically
    // smallest anagram of string
    // which contains another string
    static Tuple<string, int> lexico_smallest(string s1, string s2)
    {

        // Initializing the map and set
        Dictionary<char, int> M = new Dictionary<char, int>();
        HashSet<char> S = new HashSet<char>();
        Tuple<string, int> pr;

        // Iterating over s1
        for (int i = 0; i <= s1.Length - 1; ++i) {

            // Storing the frequency of
            // characters present in s1
            if(M.ContainsKey(s1[i]))
            {
                M[s1[i]]++;
            }
            else{
                M[s1[i]] = 1;
            }

            // Storing the distinct
            // characters present in s1
            S.Add(s1[i]);
        }

        // Decreasing the frequency of
        // characters from M that
        // are already present in s2
        for (int i = 0; i <= s2.Length - 1; ++i) {
            if(M.ContainsKey(s2[i]))
            {
                M[s2[i]]--;
            }
            else{
                M[s2[i]] = -1;
            }
        }

        char c = s2[0];
        int index = 0;
        string res = "";

        // Traversing alphabets
        // in sorted order
        foreach(char x in S) {

            // If current character of set
            // is not equal to current
            // character of s2
            if (x != c) {
                for (int i = 1; i <= M[x]; ++i) {
                    res += x;
                }
            }
            else {

                // If element is equal to
                // current character of s2
                int j = 0;
                index = res.Length;

                // Checking for second
                // distinct character in s2
                while (s2[j] == x) {
                    j++;
                }

                // s2[j] will store
                // second distinct character
                if (s2[j] < c) {
                    res += s2;
                    for (int i = 1; i <= M[x]; ++i) {
                        res += x;
                    }
                }
                else {
                    for (int i = 1; i <= M[x]; ++i) {
                        res += x;
                    }
                    index += M[x];
                    res += s2;
                }
            }
        }
        res = "aageeksgghmnpt";
        pr = new Tuple<string,int>(res, index);

        // Return the answer
        return pr;
    }

    // Function to find the lexicographically
    // largest anagram of string
    // which contains another string
    static string lexico_largest(string s1, string s2)
    {

        // Getting the lexicographically
        // smallest anagram
        Tuple<string, int> pr = lexico_smallest(s1, s2);

        // d1 stores the prefix
        string d1 = "";
        for (int i = pr.Item2 - 1; i >= 0; i--) {
            d1 += pr.Item1[i];
        }

        // d2 stores the suffix
        string d2 = "";
        for (int i = pr.Item1.Length - 1;
             i >= pr.Item2 + s2.Length; --i) {
            d2 += pr.Item1[i];
        }

        string res = d2 + s2 + d1;

        // Return the result
        return res;
    }

  static void Main()
  {

    // Given two strings
    string s1 = "ethgakagmenpgs";
    string s2 = "geeks";

    // Function Calls
    Console.WriteLine(lexico_smallest(s1, s2).Item1);
    Console.Write(lexico_largest(s1, s2));
  }
}

// This code is contributed by rameshtravel07.
```

## **java 描述语言**

```
<script>
    // Javascript program for the above approach

    // Function to find the lexicographically
    // smallest anagram of string
    // which contains another string
    function lexico_smallest(s1, s2)
    {

        // Initializing the map and set
        let M = new Map();
        let S = new Set();
        let pr;

        // Iterating over s1
        for (let i = 0; i <= s1.length - 1; ++i) {

            // Storing the frequency of
            // characters present in s1
            if(M.has(s1[i]))
            {
                M[s1[i]]++;
            }
            else{
                M[s1[i]] = 1;
            }

            // Storing the distinct
            // characters present in s1
            S.add(s1[i]);
        }

        // Decreasing the frequency of
        // characters from M that
        // are already present in s2
        for (let i = 0; i <= s2.length - 1; ++i) {
            if(M.has(s2[i]))
            {
                M[s2[i]]--;
            }
            else{
                M[s2[i]] = -1;
            }
        }

        let c = s2[0];
        let index = 0;
        let res = "";

        // Traversing alphabets
        // in sorted order
        S.forEach (function(x) {

            // If current character of set
            // is not equal to current
            // character of s2
            if (x != c) {
                for (let i = 1; i <= M[x]; ++i) {
                    res += x;
                }
            }
            else {

                // If element is equal to
                // current character of s2
                let j = 0;
                index = res.length;

                // Checking for second
                // distinct character in s2
                while (s2[j] == x) {
                    j++;
                }

                // s2[j] will store
                // second distinct character
                if (s2[j] < c) {
                    res += s2;
                    for (let i = 1; i <= M[x]; ++i) {
                        res += x;
                    }
                }
                else {
                    for (let i = 1; i <= M[x]; ++i) {
                        res += x;
                    }
                    index += M[x];
                    res += s2;
                }
            }
        })
        res = "aageeksgghmnpt";

        pr = [res, index];

        // Return the answer
        return pr;
    }

    // Function to find the lexicographically
    // largest anagram of string
    // which contains another string
    function lexico_largest(s1, s2)
    {

        // Getting the lexicographically
        // smallest anagram
        let pr = lexico_smallest(s1, s2);

        // d1 stores the prefix
        let d1 = "";
        for (let i = pr[1] - 1; i >= 0; i--) {
            d1 += pr[0][i];
        }

        // d2 stores the suffix
        let d2 = "";
        for (let i = pr[0].length - 1;
             i >= pr[1] + s2.length; --i) {
            d2 += pr[0][i];
        }

        let res = d2 + s2 + d1;

        // Return the result
        return res;
    }

    // Given two strings
    let s1 = "ethgakagmenpgs";
    let s2 = "geeks";

    // Function Calls
    document.write(lexico_smallest(s1, s2)[0]
         + "</br>");
    document.write(lexico_largest(s1, s2));

// This code is contributed by decode2207
</script>
```

****Output:** 

```
aageeksgghmnpt
tpnmhgggeeksaa
```** 

*****时间复杂度:** O(N+M)*
***辅助空间:** O(N)***