# 对 str1 中的字符进行计数，以便在删除其中任何一个字符后，str1 成为 str2

> 原文:[https://www . geesforgeks . org/str 1 中的字符数-这样-删除其中任何一个字符后-str 1-就会变成-str2/](https://www.geeksforgeeks.org/count-of-characters-in-str1-such-that-after-deleting-anyone-of-them-str1-becomes-str2/)

给定两个字符串 **str1** 和 **str2** ，任务是对 **str1** 中的字符进行计数，以便在移除其中任何一个后 **str1** 变得与 **str2** 相同。另外，打印这些字符的位置。如果不可能，则打印 **-1** 。
**示例:**

> **输入:**str 1 =“abdrakadabra”，str 2 =“abrakadabra”
> **输出:** 1
> 唯一有效的字符位于索引 2，即 str1[2]
> **输入:**str 1 =“aa”，str 2 =“a”
> **输出:** 2
> **输入:**str 1 =“geeks”，str 2 =“competitions”【T15

**逼近:**求两个字符串中最长公共前缀的长度让它为 l，最长公共后缀的长度让它为 r。如果
解决方案显然是不可能的

1.  len(字符串)！= len(str2) + 1
2.  len(ST R1)+1 < n–r

否则，有效索引从 max(len(str 1)–r，1)到 min(l + 1，len(str1))
以下是上述方法的实现:

## C++

```
// Below is C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required indices
int Find_Index(string str1, string str2)
{
    int n = str1.size();
    int m = str2.size();
    int l = 0;
    int r = 0;

    // Solution doesn't exist
    if (n != m + 1) {
        return -1;
    }

    // Find the length of the longest
    // common prefix of strings
    for (int i = 0; i < m; i++) {
        if (str1[i] == str2[i]) {
            l += 1;
        }
        else {
            break;
        }
    }

    // Find the length of the longest
    // common suffix of strings
    int i = n - 1;
    int j = m - 1;
    while (i >= 0 && j >= 0 && str1[i] == str2[j]) {
        r += 1;
        i -= 1;
        j -= 1;
    }

    // If solution does not exist
    if (l + r < m) {
        return -1;
    }

    // Return the count of indices
    else {
        i = max(n - r, 1);
        j = min(l + 1, n);
        return (j - i + 1);
    }
}

// Driver code
int main()
{
    string str1 = "aaa", str2 = "aa";

    cout << Find_Index(str1, str2);

    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count
    // of required indices
    static int Find_Index(String str1, String str2)
    {
        int n = str1.length();
        int m = str2.length();
        int l = 0;
        int r = 0;

        // Solution doesn't exist
        if (n != m + 1) {
            return -1;
        }

        // Find the length of the longest
        // common prefix of strings
        for (int i = 0; i < m; i++) {
            if (str1.charAt(i) == str2.charAt(i)) {
                l += 1;
            }
            else {
                break;
            }
        }

        // Find the length of the longest
        // common suffix of strings
        int i = n - 1;
        int j = m - 1;
        while (i >= 0 && j >= 0
               && str1.charAt(i) == str2.charAt(j)) {
            r += 1;
            i -= 1;
            j -= 1;
        }

        // If solution does not exist
        if (l + r < m) {
            return -1;
        }

        // Return the count of indices
        else {
            i = Math.max(n - r, 1);
            j = Math.min(l + 1, n);
            return (j - i + 1);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "aaa", str2 = "aa";
        System.out.println(Find_Index(str1, str2));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of required indices

def Find_Index(str1, str2):

    n = len(str1)
    m = len(str2)
    l = 0
    r = 0

    # Solution doesn't exist
    if(n != m + 1):
        return -1

    # Find the length of the longest
    # common prefix of strings
    for i in range(m):
        if str1[i] == str2[i]:
            l += 1
        else:
            break

    # Find the length of the longest
    # common suffix of strings
    i = n-1
    j = m-1
    while i >= 0 and j >= 0 and str1[i] == str2[j]:
        r += 1
        i -= 1
        j -= 1

    # If solution does not exist
    if l + r < m:
        return -1

    # Return the count of indices
    else:
        i = max(n-r, 1)
        j = min(l + 1, n)
        return (j-i + 1)

# Driver code
if __name__ == "__main__":
    str1 = "aaa"
    str2 = "aa"
    print(Find_Index(str1, str2))
```

## C#

```
// Program to print the given pattern
using System;

class GFG {

    // Function to return the count
    // of required indices
    static int Find_Index(String str1, String str2)
    {
        int n = str1.Length;
        int m = str2.Length;
        int l = 0;
        int r = 0;
        int i, j;

        // Solution doesn't exist
        if (n != m + 1) {
            return -1;
        }

        // Find the length of the longest
        // common prefix of strings
        for (i = 0; i < m; i++) {
            if (str1[i] == str2[i]) {
                l += 1;
            }
            else {
                break;
            }
        }

        // Find the length of the longest
        // common suffix of strings
        i = n - 1;
        j = m - 1;
        while (i >= 0 && j >= 0 && str1[i] == str2[j]) {
            r += 1;
            i -= 1;
            j -= 1;
        }

        // If solution does not exist
        if (l + r < m) {
            return -1;
        }

        // Return the count of indices
        else {
            i = Math.Max(n - r, 1);
            j = Math.Min(l + 1, n);
            return (j - i + 1);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str1 = "aaa", str2 = "aa";
        Console.WriteLine(Find_Index(str1, str2));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the count
// of required indices
function Find_index(str1,str2)
{
    var n = str1.length;
    var m = str2.length;
    var l = 0;
    var r = 0;

    // Solution doesn't exist
    if (n != m + 1)
    {
        return -1;
    }

    // Find the length of the longest
    // common prefix of strings
    for (var i = 0; i < m; i++)
    {
        if (str1[i] == str2[i])
        {
            l += 1;
        }
        else
        {
            break;
        }
    }

    // Find the length of the longest
    // common suffix of strings
    var i = n - 1;
    var j = m - 1;
    while (i >= 0 && j >= 0 &&
           str1[i] == str2[j])
    {
        r += 1;
        i -= 1;
        j -= 1;
    }

    // If solution does not exist
    if (l + r < m)
    {
        return -1;
    }

    // Return the count of indices
    else
    {
        i = Math.max(n - r, 1);
        j = Math.min(l + 1, n);
        return (j - i + 1);
    }
}
// Driver code  

// Given Strings
var str1 = "aaa";
var str2 = "aa";

// Function call
var result = Find_index(str1,str2);

// Print the answer
document.write(result);

// This code is contributed by rj13to
</script>
```

**Output:** 

```
3
```