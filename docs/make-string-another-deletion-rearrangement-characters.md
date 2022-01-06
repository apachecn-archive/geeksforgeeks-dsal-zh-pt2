# 通过删除和重新排列字符从另一个字符串中生成一个字符串

> 原文:[https://www . geesforgeks . org/make-string-other-delete-重排-characters/](https://www.geeksforgeeks.org/make-string-another-deletion-rearrangement-characters/)

给定两个字符串，通过从第二个字符串中删除一些字符并重新排列剩余的字符，找出我们是否可以从第二个字符串中创建第一个字符串。
**例:**

```
Input : s1 = ABHISHEKsinGH
      : s2 = gfhfBHkooIHnfndSHEKsiAnG
Output : Possible

Input : s1 = Hello
      : s2 = dnaKfhelddf
Output : Not Possible

Input : s1 = GeeksforGeeks
      : s2 = rteksfoGrdsskGeggehes
Output : Possible
```

我们基本上需要找到一个字符串是否包含第二个字符串中的字符子集。首先，我们计算第二个字符串中所有字符的出现次数。然后我们遍历第一个字符串，减少第一个字符串中出现的每个字符的数量。如果在任何时刻，计数小于 0，我们返回 false。如果所有计数都大于或等于 0，我们返回 true。

## C++

```
// CPP program to find if it is possible to
// make a string from characters present in
// other string.
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 256;

// Returns true if it is possible to make
// s1 from characters present in s2.
bool isPossible(string& s1, string& s2)
{
    // Count occurrences of all characters
    // present in s2..
    int count[MAX_CHAR] = { 0 };
    for (int i = 0; i < s2.length(); i++)
        count[s2[i]]++;

    // For every character, present in s1,
    // reduce its count if count is more
    // than 0.
    for (int i = 0; i < s1.length(); i++) {
        if (count[s1[i]] == 0)
            return false;
        count[s1[i]]--;
    }

    return true;
}

// Driver code
int main()
{
    string s1 = "GeeksforGeeks",
           s2 = "rteksfoGrdsskGeggehes";
    if (isPossible(s1, s2))
        cout << "Possible";
    else
        cout << "Not Possible\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if it is possible to
// make a string from characters present in
// other string.
class StringfromCharacters
{
    static final int MAX_CHAR = 256;

    // Returns true if it is possible to make
    // s1 from characters present in s2.
    static boolean isPossible(String s1, String s2)
    {
        // Count occurrences of all characters
        // present in s2..
        int count[] = new int[MAX_CHAR];
        for (int i = 0; i < s2.length(); i++)
            count[(int)s2.charAt(i)]++;

        // For every character, present in s1,
        // reduce its count if count is more
        // than 0.
        for (int i = 0; i < s1.length(); i++) {
            if (count[(int)s1.charAt(i)] == 0)
                return false;
            count[(int)s1.charAt(i)]--;
        }

        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        String s1 = "GeeksforGeeks",
            s2 = "rteksfoGrdsskGeggehes";
        if (isPossible(s1, s2))
            System.out.println("Possible");
        else
            System.out.println("Not Possible");
    }
}

/* This code is contributed by Danish Kaleem */
```

## 蟒蛇 3

```
# Python 3 program to find if it is possible
# to make a string from characters present
# in other string.
MAX_CHAR = 256

# Returns true if it is possible to make
# s1 from characters present in s2.
def isPossible(s1, s2):

    # Count occurrences of all characters
    # present in s2..
    count = [0] * MAX_CHAR
    for i in range(len(s2)):
        count[ord(s2[i])] += 1

    # For every character, present in s1,
    # reduce its count if count is more
    # than 0.
    for i in range(len(s1)):
        if (count[ord(s1[i])] == 0):
            return False
        count[ord(s1[i])] -= 1

    return True

# Driver code
if __name__ == "__main__":

    s1 = "GeeksforGeeks"
    s2 = "rteksfoGrdsskGeggehes"
    if (isPossible(s1, s2)):
        print("Possible")
    else:
        print("Not Possible")

# This code is contributed by ita_c
```

## C#

```
// C# program to find if it is possible to
// make a string from characters present
// in other string.
using System;

class GFG {

    static int MAX_CHAR = 256;

    // Returns true if it is possible to
    // make s1 from characters present
    // in s2.
    static bool isPossible(String s1, String s2)
    {

        // Count occurrences of all characters
        // present in s2..
        int []count = new int[MAX_CHAR];

        for (int i = 0; i < s2.Length; i++)
            count[(int)s2[i]]++;

        // For every character, present in s1,
        // reduce its count if count is more
        // than 0.
        for (int i = 0; i < s1.Length; i++)
        {
            if (count[(int)s1[i]] == 0)
                return false;

            count[(int)s1[i]]--;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        string s1 = "GeeksforGeeks",
               s2 = "rteksfoGrdsskGeggehes";

        if (isPossible(s1, s2))
            Console.WriteLine("Possible");
        else
            Console.WriteLine("Not Possible");
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
// Javascript program to find if it is possible to
// make a string from characters present in
// other string.

    let MAX_CHAR = 256;

    // Returns true if it is possible to make
    // s1 from characters present in s2.
    function isPossible(s1, s2)
    {
        // Count occurrences of all characters
        // present in s2..
        let count = new Array(MAX_CHAR);
        for(let i = 0; i < count.length; i++)
        {
            count[i] = 0;
        }
        for (let i = 0; i < s2.length; i++)
            count[s2[i].charCodeAt(0)]++;

        // For every character, present in s1,
        // reduce its count if count is more
        // than 0.
        for (let i = 0; i < s1.length; i++) {
            if (count[s1[i].charCodeAt(0)] == 0)
                return false;
            count[s1[i].charCodeAt(0)]--;
        }

        return true;
    }

    // Driver code
    let s1 = "GeeksforGeeks",
            s2 = "rteksfoGrdsskGeggehes";
    if (isPossible(s1, s2))
        document.write("Possible");
    else
        document.write("Not Possible");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Possible
```

**时间复杂度为:** O(n)
本文由**普拉巴·库马尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。