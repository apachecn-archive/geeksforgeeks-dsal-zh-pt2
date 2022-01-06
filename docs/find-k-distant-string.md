# K 远方串

> 原文:[https://www.geeksforgeeks.org/find-k-distant-string/](https://www.geeksforgeeks.org/find-k-distant-string/)

给定一个长度为 n 的字符串和一个非负整数 k。找到给定字符串的 k 个远处的字符串。

两个字母之间的距离是它们在字母表中位置的差异。例如:

*   dist(c，e) = dist(e，c) = 2。
*   距离(a，z) =距离(z，a) = 25。

利用这个概念，两个字符串之间的距离就是对应字母的距离之和。例如:

*   距离(af，hf) =距离(a，h) +距离(f，f) = 7 + 0 = 7。

给定一个字符串和距离 k。任务是找到一个字符串，使得结果字符串与给定字符串的距离为 k。如果 k 距离字符串不可能，则打印“否”。
**注:**可能存在多解。我们需要找到其中一个。

**示例:**

```
Input : bear
        k = 26
Output : zcar
Here, dist(bear, zcar) = 
      dist(b, z) + dist(e, c) +
      + dist(a, a) + dist(r, r)
      = 24 + 2 + 0 + 0 
      = 26

Input : af
        k = 7
Output : hf
Here, dist(af, hf) = dist(a, h) + dist(f, f) 
                   = 7 + 0             
                   = 7

Input : hey
        k = 1000
Output : No
Explanation :
No such string exists.

```

如果给定的所需距离太大，则没有解决方案。考虑给定字符串的最大可能距离。或者更有用的事情——如何构造丢失的字符串以最大化距离？分别对待每个字母，用距离最远的字母替换。例如，我们应该用“z”代替“c”，用“a”代替“y”。更准确地说，对于字母表的前 13 个字母，最远的字母是“z”，而对于其他字母，它是“a”。

方法很简单，迭代给定字符串的字母，然后贪婪地改变它们。一个词“贪婪地”意味着在换一个字母时，不要在意下一个字母。一般来说，必须有遥远的字母，因为否则可能没有解决办法。对于给定字符串的每个字母，将其转换为最远的字母，除非总距离太大。随着字母的变化，减少剩余的所需距离。因此，对于给定字符串的每个字母，只考虑不超过剩余距离的字母，并从中选择距离最远的一个。

CPP 和 JAVA 实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find the k distant string
#include <bits/stdc++.h>
using namespace std;

// function to find the
// lost string
string findKDistantString(string str, int k)
{
    int n = str.length();

    for (int i = 0; i < n; ++i) {

        char best_letter = str[i];
        int best_distance = 0;

        for (char maybe = 'a'; 
             maybe <= 'z'; ++maybe) 
        {
            int distance = abs(maybe - str[i]);

            // check if "distance <= k",
            // so that, the total distance
            // will not exceed among
            // letters with "distance <= k"
            if (distance <= k && distance >
                              best_distance) 
            {
                best_distance = distance;
                best_letter = maybe;
            }
        }

        // decrease the remaining
        // distance
        k -= best_distance;
        str[i] = best_letter;

    }

    assert(k >= 0);
    // we found a correct
    // string only if "k == 0"
    if (k > 0)
        return "No";
    else
        return str;
}

// driver function
int main()
{
    string str = "bear";
    int k = 26;
    cout << findKDistantString(str, k) << endl;

    str = "af";
    k = 7;

    cout << findKDistantString(str, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k distant string
import java.util.*;
import java.lang.*;

public class GfG {

    // function to find
    // the lost string
    public static String findKDistantString
                       (String str1, int k)
    {
        int n = str1.length();
        char[] str = str1.toCharArray();

        for (int i = 0; i < n; ++i) {
            char best_letter = str[i];
            int best_distance = 0;

            for (char maybe = 'a'; 
                 maybe <= 'z'; ++maybe) 
            {
                int distance = 
                    Math.abs(maybe - str[i]);

                // Check if "distance <= k"
                // so that it should not
                // exceed the total distance
                // among letters with "distance
                // <= k" we choose the most
                // distant one
                if (distance <= k && distance 
                                > best_distance) 
                {
                    best_distance = distance;
                    best_letter = maybe;
                }
            }

            // we decrease the remaining
            // distance
            k -= best_distance;
            str[i] = best_letter;
        }

        assert(k >= 0);

        // Correct string only
        // if "k == 0"
        if (k > 0)
            return "No";
        else
            return (new String(str));
    }
    public static void main(String argc[])
    {
        String str = "bear";
        int k = 26;
        System.out.println(findKDistantString(str, k));

        str = "af";
        k = 7;
        System.out.println(findKDistantString(str, k));
    }
}
```

## 蟒蛇 3

```
# Python implementation to check if
# both halves of the string have
# at least one different character

MAX = 26

# Function which break string into two halves
# Counts frequency of characters in each half
# Compares the two counter array and returns
# true if these counter arrays differ
def function(st):
    global MAX
    l = len(st)

    # Declaration and initialization
    # of counter array
    counter1, counter2 = [0]*MAX, [0]*MAX

    for i in range(l//2):
        counter1[ord(st[i]) - ord('a')] += 1

    for i in range(l//2, l):
        counter2[ord(st[i]) - ord('a')] += 1

    for i in range(MAX):
        if (counter2[i] != counter1[i]):
            return True

    return False

# Driver function
st = "abcasdsabcae"
if function(st): print("Yes, both halves differ by at least one character")
else: print("No, both halves do not differ at all")

# This code is contributed by Ansu Kumari
```

## C#

```
// C# program to find k distant string
using System;

class GfG {

    // function to find the lost string
    public static String findKDistantString
                       (string str1, int k)
    {
        int n = str1.Length;
        char []str = str1.ToCharArray();

        for (int i = 0; i < n; ++i) {
            char best_letter = str[i];
            int best_distance = 0;

            for (char maybe = 'a'; 
                maybe <= 'z'; ++maybe) 
            {
                int distance = 
                    Math.Abs(maybe - str[i]);

                // Check if "distance <= k"
                // so that it should not
                // exceed the total distance
                // among letters with "distance
                // <= k" we choose the most
                // distant one
                if (distance <= k && distance 
                                > best_distance) 
                {
                    best_distance = distance;
                    best_letter = maybe;
                }
            }

            // we decrease the remaining
            // distance
            k -= best_distance;
            str[i] = best_letter;
        }

        //(k >= 0);

        // Correct string only
        // if "k == 0"
        if (k > 0)
            return "No";
        else
            return (new string(str));
    }

    // Driver code
    public static void Main()
    {
        string str = "bear";
        int k = 26;
        Console.WriteLine(
              findKDistantString(str, k));

        str = "af";
        k = 7;
        Console.Write(
              findKDistantString(str, k));
    }
}

// This code is contributed by Nitin millal. 
```

Output:

```
zcar
hf

```