# 通过改变字符

在 AP 中制作字符串

> 原文:[https://www . geesforgeks . org/通过更改字符使字符串成为 AP/](https://www.geeksforgeeks.org/make-the-string-in-ap-by-changing-a-character/)

给定一个由字母组成的字符串，它们的 ASCII 值遵循算术级数。任务是找到不服从 AP 的字母和字母的索引。另外，用适当的字母替换这个字母，并打印字符串。

**示例:**

> **输入:**S =“abcdfghijkl”
> **输出:**4->f
> abcdefghijkl
> **说明:**
> 在给定的字符串 S 中，每个具有索引 **i** 的字符与其先前的索引 **i-1** 相比向前变化一个字符。
> 对于 i = 4，S[4] = 'f '和 S[3] = 'd '，而 S[i]应该是' e '，因此它会遵循模式。因此用“e”代替 S[4]。因此，修改后的字符串 S 是“abcdefghijkl”。
> 
> **输入:**S = " aeimqux "
> T3】输出: 6 - > x
> aeimquy
> 
> **输入:**S =
> **输出:**0->B
> Ae quy
> 
> **输入:**S = " xyzac "
> T3】输出: 4 - > c
> xyzab

**进场:**

1.  创建一个数组来存储从**a–z**开始的字母表的 ASCII 值。
2.  遍历字符串 **S** ，使用前面创建的数组找到字符串中两个连续字符的 ASCII 值之间的差异，并将这些值存储在一个集合中。
3.  对于集合中的每个值，如 **D** ，构造一个字符串 **T** ，其字符在其 ASCII 值中具有 **D** 单位的共同差异。
4.  每次构造新字符串 **T** 时，其起始字符应该与给定字符串 **S** 的起始字符相同。
5.  如果字符串 **T** 与字符串 **S** 相差 1 个字符，那么 **T** 就是需要修改的字符串。找到这两个字符串不同的唯一索引。打印索引及其相应字符。
6.  如果 **T** 与 **S** 相差超过 1 个字符，则丢弃字符串 **T** ，转到步骤 3。
7.  如果重构的字符串中没有一个与原始字符串相差 1 个字符，那么字符串 **S** 的第一个字符就是不符合 AP 的字符串。

> **用一个例子解释上述方法:**T2【S = " abcdfghijkl "
> set = { 0，1，2}
> 将固定差视为 0 重构的字符串为“aaaaaaaaaa”。该字符串与原始字符串相差 11 个位置，因此它不是必需的字符串。
> 考虑固定差值为 1 时重构的字符串为“abcdefghijkl”。该字符串与原始字符串相差 1 个位置，因此它是必需的字符串。需要修改字符的索引是 4。

以下是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to modify the given
// string and find the index
// where modification is needed
void string_modify(string s)
{

    // Array to store the ASCII
    // values of alphabets
    char alphabets[26];

    int flag = 0, hold_i;
    char hold_l;
    int i;

    // loop to compute the ASCII
    // values of characters a-z
    for (i = 0; i < 26; i++) {
        alphabets[i] = i + 'a';
    }

    // Set to store all the
    // possible differences
    // between consecutive elements
    set<int> difference;

    string reconstruct = "";

    // Loop to find out the
    // differences between
    // consecutive elements
    // and storing them in the set
    for (int i = 1;
        i < s.size(); i++) {
        difference.insert(s[i] - s[i - 1]);
    }

    // Checks if any character of the
    // string disobeys the pattern
    if (difference.size() == 1) {
        cout << "No modifications required";
        return;
    }

    // Constructing the strings with
    // all possible values of consecutive
    // difference and comparing them
    // with starting string S.
    for (auto it = difference.begin();
        it != difference.end(); it++) {

        int index = s[0] - 'a';
        reconstruct = "";
        flag = 0;

        for (int i = 0;
            i < s.size()
            && flag <= 1;
            i++) {

            reconstruct += alphabets[index];
            index += *it;

            if (index < 0) {
                index += 26;
            }

            index %= 26;
            if (reconstruct[i] != s[i]) {

                flag++;
                hold_i = i;
                hold_l = s[i];
            }
        }

        if (flag == 1) {

            s[hold_i] = reconstruct[hold_i];
            break;
        }
    }

    if (flag > 1) {
        hold_i = 0;
        hold_l = s[0];

        int temp = (s[1] - 'a' - (s[2] - s[1])) % 26;

        if (temp < 0) {
            temp += 26;
        }
        s[0] = alphabets[temp];
    }

    cout << hold_i << " -> "
        << hold_l << endl
        << s << endl;
}

// Driver Code
int main()
{
    string s = "aeimqux";
    string_modify(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;

class GFG{

// Function to modify the given
// String and find the index
// where modification is needed
static void string_modify(char[] s)
{

    // Array to store the ASCII
    // values of alphabets
    char []alphabets = new char[26];

    int flag = 0, hold_i = 0;
    char hold_l = 0;
    int i;

    // loop to compute the ASCII
    // values of characters a-z
    for(i = 0; i < 26; i++)
    {
        alphabets[i] = (char)(i + 'a');
    }

    // Set to store all the
    // possible differences
    // between consecutive elements
    HashSet<Integer>difference = new HashSet<Integer>();

    String reconstruct = "";

    // Loop to find out the
    // differences between
    // consecutive elements
    // and storing them in the set
    for(i = 1; i < s.length; i++)
    {
        difference.add(s[i] - s[i - 1]);
    }

    // Checks if any character of the
    // String disobeys the pattern
    if (difference.size() == 1)
    {
        System.out.print("No modifications required");
        return;
    }

    // Constructing the Strings with
    // all possible values of consecutive
    // difference and comparing them
    // with starting String S.
    for(int it : difference)
    {
        int index = s[0] - 'a';
        reconstruct = "";
        flag = 0;

        for(i = 0; i < s.length && flag <= 1; i++)
        {
            reconstruct += alphabets[index];
            index += it;

            if (index < 0)
            {
                index += 26;
            }
            index %= 26;

            if (reconstruct.charAt(i) != s[i])
            {
                flag++;
                hold_i = i;
                hold_l = s[i];
            }
        }
        if (flag == 1)
        {
            s[hold_i] = reconstruct.charAt(hold_i);
            break;
        }
    }
    if (flag < 1)
    {
        hold_i = 0;
        hold_l = s[0];

        int temp = (s[1] - 'a' - (s[2] - s[1])) % 26;
        if (temp < 0)
        {
            temp += 26;
        }
        s[0] = alphabets[temp];
    }

    System.out.print(hold_i + " -> " +
                     hold_l + "\n" +
                     String.valueOf(s) + "\n");
}

// Driver Code
public static void main(String[] args)
{
    String s = "aeimqux";

    string_modify(s.toCharArray());
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Function to modify the given
# string and find the index
# where modification is needed
def string_modify(s):

    # Array to store the ASCII
    # values of alphabets
    alphabets = []

    flag, hold_i = 0, 0
    hold_l = s[0]

    # Loop to compute the ASCII
    # values of characters a-z
    for i in range(26):
        alphabets.append(chr(i + ord('a')))

    # Set to store all the
    # possible differences
    # between consecutive elements
    difference = set()

    reconstruct = ""

    # Loop to find out the
    # differences between
    # consecutive elements
    # and storing them in the set
    for i in range(1, len(s)):
        difference.add(ord(s[i]) -
                       ord(s[i - 1]))

    # Checks if any character of the
    # string disobeys the pattern
    if (len(difference) == 1):
        print("No modifications required")
        return

    # Constructing the strings with
    # all possible values of consecutive
    # difference and comparing them
    # with starting string S.
    for it in difference:
        index = ord(s[0]) - ord('a')
        reconstruct = ""
        flag = 0
        i = 0

        while ((i < len(s)) and (flag <= 1)):
            reconstruct += alphabets[index]
            index += it

            if (index < 0):
                index += 26

            index %= 26
            if (reconstruct[i] != s[i]):
                flag += 1
                hold_i = i
                hold_l = s[i]

            i += 1

        if (flag == 1):
            s[hold_i] = reconstruct[hold_i]
            break

    if (flag > 1):
        hold_i = 0
        hold_l = s[0]

        temp = (ord(s[1]) - ord('a') -
               (ord(s[2]) - ord(s[1]))) % 26

        if (temp < 0):
            temp += 26

        s[0] = alphabets[temp]

    print(hold_i, "->", hold_l)
    print("".join(s))

# Driver code
s = list("aeimqux")

string_modify(s)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above problem
using System;
using System.Collections.Generic;
class GFG{

// Function to modify the given
// String and find the index
// where modification is needed
static void string_modify(char[] s)
{

    // Array to store the ASCII
    // values of alphabets
    char []alphabets = new char[26];

    int flag = 0, hold_i = 0;
    char hold_l = (char)0;
    int i;

    // loop to compute the ASCII
    // values of characters a-z
    for(i = 0; i < 26; i++)
    {
        alphabets[i] = (char)(i + 'a');
    }

    // Set to store all the
    // possible differences
    // between consecutive elements
    HashSet<int>difference = new HashSet<int>();

    String reconstruct = "";

    // Loop to find out the
    // differences between
    // consecutive elements
    // and storing them in the set
    for(i = 1; i < s.Length; i++)
    {
        difference.Add(s[i] - s[i - 1]);
    }

    // Checks if any character of the
    // String disobeys the pattern
    if (difference.Count == 1)
    {
        Console.Write("No modifications required");
        return;
    }

    // Constructing the Strings with
    // all possible values of consecutive
    // difference and comparing them
    // with starting String S.
    foreach(int it in difference)
    {
        int index = s[0] - 'a';
        reconstruct = "";
        flag = 0;

        for(i = 0; i < s.Length && flag <= 1; i++)
        {
            reconstruct += alphabets[index];
            index += it;

            if (index < 0)
            {
                index += 26;
            }
            index %= 26;

            if (reconstruct[i] != s[i])
            {
                flag++;
                hold_i = i;
                hold_l = s[i];
            }
        }
        if (flag == 1)
        {
            s[hold_i] = reconstruct[hold_i];
            break;
        }
    }
    if (flag < 1)
    {
        hold_i = 0;
        hold_l = s[0];

        int temp = (s[1] - 'a' - (s[2] - s[1])) % 26;
        if (temp < 0)
        {
            temp += 26;
        }
        s[0] = alphabets[temp];
    }

    Console.Write(hold_i + " -> " +
                     hold_l + "\n" +
                     String.Join("", s) + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    String s = "aeimqux";

    string_modify(s.ToCharArray());
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above problem

// Function to modify the given
// string and find the index
// where modification is needed
function string_modify(s)
{

    // Array to store the ASCII
    // values of alphabets
    var alphabets = Array(26).fill(0);

    var flag = 0, hold_i;
    var hold_l;
    var i;

    // loop to compute the ASCII
    // values of characters a-z
    for (i = 0; i < 26; i++) {
        alphabets[i] =
        String.fromCharCode(i + 'a'.charCodeAt(0));
    }

    // Set to store all the
    // possible differences
    // between consecutive elements
    var difference = new Set();

    var reconstruct = "";

    // Loop to find out the
    // differences between
    // consecutive elements
    // and storing them in the set
    for (var i = 1;
        i < s.length; i++) {
        difference.add(s[i].charCodeAt(0) -
        s[i - 1].charCodeAt(0));
    }

    // Checks if any character of the
    // string disobeys the pattern
    if (difference.size == 1) {
        document.write( "No modifications required");
        return;
    }

    // Constructing the strings with
    // all possible values of consecutive
    // difference and comparing them
    // with starting string S.
    [...difference].sort((a,b)=>a-b).forEach(it => {

        if(flag!=1)
        {
        var index = s[0].charCodeAt(0) - 'a'.charCodeAt(0);
        reconstruct = "";
        flag = 0;

        for (var i = 0;
            i < s.length
            && flag <= 1;
            i++) {

            reconstruct += alphabets[index];
            index += it;

            if (index < 0) {
                index += 26;
            }

            index %= 26;
            if (reconstruct[i] != s[i]) {

                flag++;
                hold_i = i;
                hold_l = s[i];
            }
        }

        if (flag == 1) {

            s[hold_i] = reconstruct[hold_i];
        }
        }
    });

    if (flag > 1) {
        hold_i = 0;
        hold_l = s[0];

        var temp = (s[1].charCodeAt(0) - 'a'.charCodeAt(0) -
        (s[2].charCodeAt(0) - s[1].charCodeAt(0))) % 26;

        if (temp < 0) {
            temp += 26;
        }
        s[0] = alphabets[temp];
    }

    document.write( hold_i + " -> "
        + hold_l + "<br>"
        + s.join('') + "<br>");
}

// Driver Code
var s = "aeimqux";
string_modify(s.split(''));

</script>
```

**Output:** 

```
6 -> x
aeimquy
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*