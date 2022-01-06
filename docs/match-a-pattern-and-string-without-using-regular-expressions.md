# 在不使用正则表达式的情况下匹配模式和字符串

> 原文:[https://www . geesforgeks . org/match-a-pattern-and-string-不使用正则表达式/](https://www.geeksforgeeks.org/match-a-pattern-and-string-without-using-regular-expressions/)

给定一个字符串，在不使用任何正则表达式的情况下，找出该字符串是否遵循给定的模式。
示例:

```
Input: 
string - GraphTreesGraph
pattern - aba
Output: 
a->Graph
b->Trees

Input: 
string - GraphGraphGraph
pattern - aaa
Output: 
a->Graph

Input: 
string - GeeksforGeeks
pattern - GfG
Output: 
G->Geeks
f->for

Input: 
string - GeeksforGeeks
pattern - GG
Output: 
No solution exists
```

我们可以借助回溯来解决这个问题。对于模式中的每个字符，如果之前没有看到该字符，我们会考虑所有可能的子字符串，并递归查看它是否会导致解决方案。我们维护一个存储映射到模式字符的子字符串的映射。如果之前见过模式字符，我们使用地图中的相同子字符串。如果我们找到了一个解决方案，对于模式中的每个不同字符，我们使用我们的映射来打印映射到它的字符串。
以下是上述思路的 C++实现–

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find out if string follows
// a given pattern or not
#include <bits/stdc++.h>
using namespace std;

/*  Function to find out if string follows a given
    pattern or not

    str - given string
    n - length of given string
    i - current index in input string
    pat - given pattern
    m - length of given pattern
    j - current index in given pattern
    map - stores mapping between pattern and string */
bool patternMatchUtil(string str, int n, int i,
                    string pat, int m, int j,
                    unordered_map<char, string>& map)
{
    // If both string and pattern reach their end
    if (i == n && j == m)
        return true;

    // If either string or pattern reach their end
    if (i == n || j == m)
        return false;

    // read next character from the pattern
    char ch = pat[j];

    // if character is seen before
    if (map.find(ch)!= map.end())
    {
        string s = map[ch];
        int len = s.size();

        // consider next len characters of str
        string subStr = str.substr(i, len);

        // if next len characters of string str
        // don't match with s, return false
        if (subStr.compare(s))
            return false;

        // if it matches, recurse for remaining characters
        return patternMatchUtil(str, n, i + len, pat, m,
                                            j + 1, map);
    }

    // If character is seen for first time, try out all
    // remaining characters in the string
    for (int len = 1; len <= n - i; len++)
    {
        // consider substring that starts at position i
        // and spans len characters and add it to map
        map[ch] = str.substr(i, len);

        // see if it leads to the solution
        if (patternMatchUtil(str, n, i + len, pat, m,
                                          j + 1, map))
            return true;

        // if not, remove ch from the map
        map.erase(ch);
    }

    return false;
}

// A wrapper over patternMatchUtil()function
bool patternMatch(string str, string pat, int n, int m)
{
    if (n < m)
    return false;

    // create an empty hashmap
    unordered_map<char, string> map;

    // store result in a boolean variable res
    bool res = patternMatchUtil(str, n, 0, pat, m, 0, map);

    // if solution exists, print the mappings
    for (auto it = map.begin(); res && it != map.end(); it++)
        cout << it->first << "->" << it->second << endl;

    // return result
    return res;
}

// Driver code
int main()
{
    string str = "GeeksforGeeks", pat = "GfG";

    int n = str.size(), m = pat.size();

    if (!patternMatch(str, pat, n, m))
        cout << "No Solution exists";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;
import java.util.Map;

class Main
{
  // Function to determine if given pattern matches with a string or not
  public static boolean match(String str, int i,
                              String pat, int j,
                              Map<Character, String> map)
  {
    int n = str.length(), m = pat.length();

    // base condition
    if (n < m) {
      return false;
    }

    // if both pattern and the string reaches end
    if (i == n && j == m) {
      return true;
    }

    // if either string or pattern reaches end
    if (i == n || j == m) {
      return false;
    }

    // consider next character from the pattern
    char curr = pat.charAt(j);

    // if the character is seen before
    if (map.containsKey(curr))
    {
      String s = map.get(curr);
      int k = s.length();

      // ss stores next k characters of the given string
      String ss;
      if (i + k < str.length()) {
        ss = str.substring(i, i + k);
      } else {
        ss = str.substring(i);
      }

      // return false if next k characters doesn't match with s
      if (ss.compareTo(s) != 0) {
        return false;
      }

      // recur for remaining characters if next k characters matches
      return match(str, i + k, pat, j + 1, map);
    }

    // process all remaining characters in the string if current
    // character is never seen before
    for (int k = 1; k <= n - i; k++)
    {
      // insert substring formed by next k characters of the string
      // into the map
      map.put(curr, str.substring(i, i + k));

      // check if it leads to the solution
      if (match(str, i + k, pat, j + 1, map)) {
        return true;
      }

      // else backtrack - remove current character from the map
      map.remove(curr);
    }

    return false;
  }

  public static void main(String[] args)
  {
    // input string and pattern
    String str = "GeeksforGeeks";
    String pat = "GfG";

    // create a map to store mappings between the pattern and string
    Map<Character, String> map = new HashMap<>();

    // check for solution
    if (match(str, 0, pat, 0, map))
    {
      for (Map.Entry<Character, String> entry: map.entrySet()) {
        System.out.println(entry.getKey() + "->" + entry.getValue());
      }
    }
    else {
      System.out.println("Solution doesn't exist");
    }
  }
}

//This code is contributed by Priyadarshini Kumari
```

## 蟒蛇 3

```
# Function to determine if given pattern matches with a string or not
def match(str, pat, dict, i=0, j=0):

    n = len(str)
    m = len(pat)

    # base condition
    if n < m:
        return False

    # if both pattern and the string reaches end
    if i == n and j == m:
        return True

    # if either string or pattern reaches end
    if i == n or j == m:
        return False

    # consider next character from the pattern
    curr = pat[j]

    # if the character is seen before
    if curr in dict:

        s = dict[curr]
        k = len(s)

        # ss stores next k characters of the given string
        if i + k < len(str):
            ss = str[i:i + k]
        else:
            ss = str[i:]

        # return false if next k characters doesn't match with s
        if ss != s:
            return False

        # recur for remaining characters if next k characters matches
        return match(str, pat, dict, i + k, j + 1)

    # process all remaining characters in the string if current
    # character is never seen before
    for k in range(1, n - i + 1):

        # insert substring formed by next k characters of the string
        # into the dictionary
        dict[curr] = str[i:i + k]

        # check if it leads to the solution
        if match(str, pat, dict, i + k, j + 1):
            return True

        # else backtrack - remove current character from the dictionary
        dict.pop(curr)

    return False

if __name__ == '__main__':

    # input string and pattern
    str = "GeeksforGeeks"
    pat = "GfG"

    # create a dictionary to store mappings between the pattern and string
    dict = {}

    # check for solution
    if match(str, pat, dict):
        print(dict)
    else:
        print("Solution doesn't exist")

# This code is contributed by Priyadarshini Kumari
```

输出:

```
f->for
G->Geeks
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。