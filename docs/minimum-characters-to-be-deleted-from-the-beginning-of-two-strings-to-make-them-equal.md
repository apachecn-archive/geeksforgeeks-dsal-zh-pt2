# 从两个字符串的开头删除的最少字符，使它们相等

> 原文:[https://www . geeksforgeeks . org/从两个字符串的开头删除最少字符以使它们相等/](https://www.geeksforgeeks.org/minimum-characters-to-be-deleted-from-the-beginning-of-two-strings-to-make-them-equal/)

给定两个字符串 **S** 和 **T** ，任务是从这些字符串的开头找到要删除的最小字符数，使这两个字符串相同。

> 两个空字符串总是相同的字符串。

**例:**

> **输入:**S = " geeks forgeeks " T = " peeks "
> **输出:** 10
> **解释:**
> 删除来自 S 的子串“geeksforg”和来自 T 的“p”，使两个字符串都等于“eeks”
> **输入:**S = " geeks forgeeks " T = " code "
> **输出:** 17
> **解释:…**

**方法:**
从末尾同时遍历两个字符串，比较两个字符串的字符。两个字符串的字符不同的第一个索引**I**(S1 的索引)和**j**(S2 的索引)是 S1 和 S2 的字符需要删除的长度。因此， **i + j** 的最终值就是需要的答案。
以下是上述方法的实施:

## C++

```
// C++ Program to count minimum
// number of characters to be deleted
// from the beginning of the two strings
// to make the strings equal
#include <bits/stdc++.h>
using namespace std;

// Function that finds minimum
// character required to be deleted
int minDel(string s1, string s2)
{
    int i = s1.length();
    int j = s2.length();

    // Iterate in the strings
    while (i > 0 && j > 0) {

        // Check if the characters are
        // not equal
        if (s1[i - 1] != s2[j - 1]) {
            break;
        }

        i--;
        j--;
    }

    // Return the result
    return i + j;
}

// Driver Program
int main()
{
    string s1 = "geeksforgeeks",
           s2 = "peeks";

    cout << minDel(s1, s2) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count minimum
// number of characters to be deleted
// from the beginning of the two strings
// to make the strings equal
import java.util.*;
class GFG{

// Function that finds minimum
// character required to be deleted
static int minDel(String s1, String s2)
{
    int i = s1.length();
    int j = s2.length();

    // Iterate in the strings
    while (i > 0 && j > 0)
    {

        // Check if the characters are
        // not equal
        if (s1.charAt(i - 1) != s2.charAt(j - 1))
        {
            break;
        }

        i--;
        j--;
    }

    // Return the result
    return i + j;
}

// Driver Code
public static void main(String args[])
{
    String s1 = "geeksforgeeks",
           s2 = "peeks";

    System.out.print(minDel(s1, s2));
}
}

// This code is contributed by Nidhi_biet
```

## 蟒蛇 3

```
# Python3 program to count minimum
# number of characters to be deleted
# from the beginning of the two strings
# to make the strings equal

# Function that finds minimum
# character required to be deleted
def minDel(s1, s2):

    i = len(s1)
    j = len(s2)

    # Iterate in the strings
    while (i > 0 and j > 0):

        # Check if the characters are
        # not equal
        if (s1[i - 1] != s2[j - 1]):
            break

        i -= 1
        j -= 1

    # Return the result
    return i + j

# Driver code
if __name__ == '__main__':

    s1 = "geeksforgeeks"
    s2 = "peeks"

    print(minDel(s1, s2))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# Program to count minimum
// number of characters to be deleted
// from the beginning of the two strings
// to make the strings equal
using System;
class GFG{

// Function that finds minimum
// character required to be deleted
static int minDel(string s1, string s2)
{
    int i = s1.Length;
    int j = s2.Length;

    // Iterate in the strings
    while (i > 0 && j > 0)
    {

        // Check if the characters are
        // not equal
        if (s1[i - 1] != s2[j - 1])
        {
            break;
        }

        i--;
        j--;
    }

    // Return the result
    return i + j;
}

// Driver Code
public static void Main()
{
    string s1 = "geeksforgeeks",
           s2 = "peeks";

    Console.Write(minDel(s1, s2));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript Program to count minimum
// number of characters to be deleted
// from the beginning of the two strings
// to make the strings equal

// Function that finds minimum
// character required to be deleted
function minDel(s1, s2)
{
    var i = s1.length;
    var j = s2.length;

    // Iterate in the strings
    while (i > 0 && j > 0) {

        // Check if the characters are
        // not equal
        if (s1[i - 1] != s2[j - 1]) {
            break;
        }

        i--;
        j--;
    }

    // Return the result
    return i + j;
}

// Driver Program
var s1 = "geeksforgeeks",
       s2 = "peeks";
document.write( minDel(s1, s2) );

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O( min(len(S1)，len(S2))*
***辅助空间:** O(1)*