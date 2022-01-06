# 查找数组是否包含一个不匹配的字符串

> 原文:[https://www . geesforgeks . org/find-array-contains-string-one-mismatch/](https://www.geeksforgeeks.org/find-array-contains-string-one-mismatch/)

给定字符串和字符串数组，查找数组是否包含与给定字符串有一个字符差异的字符串。数组可以包含不同长度的字符串。
**例:**

```
Input : str = "banana"
        arr[] = {"bana", "apple", "banaba",
                    bonanzo", "banamf"}
Output :True
Explanation:-There is only a one character difference
between banana and banaba

Input : str = "banana"
        arr[] = {"bana", "apple", "banabb", bonanzo",
                                           "banamf"}
Output : False
```

我们遍历给定的字符串并检查 arr 中的每个字符串。对于 arr 中包含的每个字符串，请遵循下面给出的两个步骤:-
1)检查 arr 中包含的字符串是否与目标字符串具有相同的长度。
2)如果是，则检查是否只有一个字符不匹配，如果是，则返回真，否则返回假。

## C++

```
// C++ program to find if given string is present
// with one mismatch.
#include <bits/stdc++.h>
using namespace std;

bool check(vector<string> list, string s)
{
    int n = (int)list.size();

    // If the array is empty   
    if (n == 0)
        return false;

    for (int i = 0; i < n; i++) {

        // If sizes are same
        if (list[i].size() != s.size())
            continue;

        bool diff = false;
        for (int j = 0; j < (int)list[i].size(); j++) {

            if (list[i][j] != s[j]) {

                // If first mismatch  
                if (!diff)
                    diff = true;

                // Second mismatch
                else {
                    diff = false;
                    break;
                }
            }
        }

        if (diff)
            return true;
    }

    return false;
}

// Driver code
int main()
{
    vector<string> s;
    s.push_back("bana");
    s.push_back("apple");
    s.push_back("banacb");
    s.push_back("bonanza");
    s.push_back("banamf");

    cout << check(s, "banana");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java program to find if
// given string is present
// with one mismatch.
class GFG
{

    static boolean check(Vector<String> list, String s)
    {
        int n = (int) list.size();

        // If the array is empty
        if (n == 0)
        {
            return false;
        }

        for (int i = 0; i < n; i++)
        {

            // If sizes are same
            if (list.get(i).length() != s.length())
            {
                continue;
            }

            boolean diff = false;
            for (int j = 0; j < (int) list.get(i).length(); j++)
            {

                if (list.get(i).charAt(j) != s.charAt(j))
                {

                    // If first mismatch
                    if (!diff)
                    {
                        diff = true;
                    }

                    // Second mismatch
                    else
                    {
                        diff = false;
                        break;
                    }
                }
            }

            if (diff) {
                return true;
            }
        }

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        Vector<String> s = new Vector<>();
        s.add("bana");
        s.add("apple");
        s.add("banacb");
        s.add("bonanza");
        s.add("banamf");

        System.out.println(check(s, "banana") == true ? 1 : 0);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 program to find if given
# string is present with one mismatch.

def check(list, s):
    n = len(list)

    # If the array is empty
    if (n == 0):
        return False

    for i in range(0, n, 1):

        # If sizes are same
        if (len(list[i]) != len(s)):
            continue

        diff = False
        for j in range(0, len(list[i]), 1):
            if (list[i][j] != s[j]):

                # If first mismatch
                if (diff == False):
                    diff = True

                # Second mismatch
                else:
                    diff = False
                    break

        if (diff):
            return True

    return False

# Driver code
if __name__ == '__main__':
    s = []
    s.append("bana")
    s.append("apple")
    s.append("banacb")
    s.append("bonanza")
    s.append("banamf")

    print(int(check(s, "banana")))

# This code is contributed by
# Sahil_shelangia
```

## C#

```
// C# program to find if
// given string is present
// with one mismatch.
using System;   
using System.Collections.Generic;
public class GFG
{

    static bool check(List<String> list, String s)
    {
        int n = (int) list.Count;

        // If the array is empty
        if (n == 0)
        {
            return false;
        }

        for (int i = 0; i < n; i++)
        {

            // If sizes are same
            if (list[i].Length != s.Length)
            {
                continue;
            }

            bool diff = false;
            for (int j = 0; j < (int) list[i].Length; j++)
            {

                if (list[i][j] != s[j])
                {

                    // If first mismatch
                    if (!diff)
                    {
                        diff = true;
                    }

                    // Second mismatch
                    else
                    {
                        diff = false;
                        break;
                    }
                }
            }

            if (diff) {
                return true;
            }
        }

        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        List<String> s = new List<String>();
        s.Add("bana");
        s.Add("apple");
        s.Add("banacb");
        s.Add("bonanza");
        s.Add("banamf");

        Console.WriteLine(check(s, "banana") == true ? 1 : 0);
    }
}
// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to find if
    // given string is present
    // with one mismatch.

    function check(list, s)
    {
        let n = list.length;

        // If the array is empty
        if (n == 0)
        {
            return false;
        }

        for (let i = 0; i < n; i++)
        {

            // If sizes are same
            if (list[i].length != s.length)
            {
                continue;
            }

            let diff = false;
            for (let j = 0; j < list[i].length; j++)
            {

                if (list[i][j] != s[j])
                {

                    // If first mismatch
                    if (!diff)
                    {
                        diff = true;
                    }

                    // Second mismatch
                    else
                    {
                        diff = false;
                        break;
                    }
                }
            }

            if (diff) {
                return true;
            }
        }

        return false;
    }

    let s = [];
    s.push("bana");
    s.push("apple");
    s.push("banacb");
    s.push("bonanza");
    s.push("banamf");

    document.write(check(s, "banana") == true ? 1 : 0);

</script>
```

**输出:**

```
0
```

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。