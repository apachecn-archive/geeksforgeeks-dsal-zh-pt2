# 建造一根绳子的最小成本

> 原文:[https://www . geesforgeks . org/mini-cost-construct-string/](https://www.geeksforgeeks.org/minimum-cost-construct-string/)

给定一个字符串 s(只包含小写字母)，我们必须找到构造给定字符串的最小成本。可以使用以下操作来确定成本:
1。追加单个字符花费 1 个单位
2。新字符串的子字符串(中间字符串)可以免费追加
注*中间字符串是到目前为止形成的字符串。
**示例:**

```
Input : "geks"
Output : cost: 4
Explanation:
appending 'g' cost 1, string "g"
appending 'e' cost 1, string "ge"
appending 'k' cost 1, string "gek"
appending 's' cost 1, string "geks"
Hence, Total cost to construct "geks" is 4

Input :  "abab"
Output : cost: 2
Explanation: 
Appending 'a' cost 1, string "a"
Appending 'b' cost 1, string "ab"
Appending  "ab" cost nothing as it 
is substring of intermediate.
Hence, Total cost to construct "abab" is 2
```

**天真方法**:检查剩余的待构造字符串中是否有子字符串，该子字符串也是中间字符串中的子字符串，如果有，则免费追加，如果没有，则以每字符 1 个单位的代价追加。
在上面的例子中，当中间字符串是“ab”并且我们需要构造“abab”时，剩下的字符串是“ab”。因此，剩余字符串中有一个子字符串，它也是中间字符串(即“ab”)的子字符串，因此我们不需要花费任何费用。
**更好的方法**:我们将使用哈希技术，来维护我们是否见过一个角色。如果我们已经看到了这个角色，那么添加这个角色就没有成本，如果没有，那么我们就要花费 1 个单位。
现在在这种方法中，我们一次取一个字符，而不是一个字符串。这是因为如果“ab”是“abab”的子串，那么‘a’和‘b’也是单独的，因此没有区别。
这也让我们得出结论，如果字符串包含所有字母(a-z)，构建字符串的成本永远不会超过 26。

## C++

```
// C++ Program to find minimum cost to
// construct a string
#include <iostream>
using namespace std;

int minCost(string& s)
{
    // Initially all characters are un-seen
    bool alphabets[26] = { false };

    // Marking seen characters
    for (int i = 0; i < s.size(); i++)
        alphabets[s[i] - 97] = true;

    // Count total seen character, and that
    // is the cost
    int count = 0;
    for (int i = 0; i < 26; i++)
        if (alphabets[i])
            count++;

    return count;
}

int main()
{
    // s is the string that needs to be constructed
    string s = "geeksforgeeks";

    cout << "Total cost to construct "
         << s << " is " << minCost;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find minimum cost to
// construct a string

class GFG
{

    static int minCost(char[] s)
    {

        // Initially all characters are un-seen
        boolean alphabets[] = new boolean[26];

        // Marking seen characters
        for (int i = 0; i < s.length; i++)
        {
            alphabets[(int) s[i] - 97] = true;
        }

        // Count total seen character,
        // and that is the cost
        int count = 0;
        for (int i = 0; i < 26; i++)
        {
            if (alphabets[i])
            {
                count++;
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        // s is the string that needs to be constructed
        String s = "geeksforgeeks";
        System.out.println("Total cost to construct " +
                s + " is " + minCost(s.toCharArray()));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 Program to find minimum cost to
# construct a string

def minCost(s):

    # Initially all characters are un-seen
    alphabets = [False for i in range(26)]

    # Marking seen characters
    for i in range(len(s)):
        alphabets[ord(s[i]) - 97] = True

    # Count total seen character, and that
    # is the cost
    count = 0
    for i in range(26):
        if (alphabets[i]):
            count += 1

    return count

# Driver Code
if __name__ == '__main__':

    # s is the string that needs to
    # be constructed
    s = "geeksforgeeks"

    print("Total cost to construct", s,
                      "is", minCost(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find minimum cost to
// construct a string
using System;

class GFG
{

    static int minCost(char[] s)
    {

        // Initially all characters are un-seen
        bool []alphabets = new bool[26];

        // Marking seen characters
        for (int i = 0; i < s.Length; i++)
        {
            alphabets[(int) s[i] - 97] = true;
        }

        // Count total seen character,
        // and that is the cost
        int count = 0;
        for (int i = 0; i < 26; i++)
        {
            if (alphabets[i])
            {
                count++;
            }
        }

        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // s is the string that
        // needs to be constructed
        String s = "geeksforgeeks";
        Console.WriteLine("Total cost to construct " +
                s + " is " + minCost(s.ToCharArray()));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript Program to find minimum cost to
      // construct a string
      function minCost(s)
      {

        // Initially all characters are un-seen
        var alphabets = new Array(26).fill(0);

        // Marking seen characters
        for (var i = 0; i < s.length; i++) {
          alphabets[s[i].charCodeAt(0) - 97] = true;
        }

        // Count total seen character,
        // and that is the cost
        var count = 0;
        for (var i = 0; i < 26; i++) {
          if (alphabets[i]) {
            count++;
          }
        }

        return count;
      }

      // Driver code
      // s is the string that
      // needs to be constructed
      var s = "geeksforgeeks";
      document.write(
        "Total cost to construct " + s + " is " + minCost(s.split(""))
      );

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
Total cost to construct geeksforgeeks is 7
```